description:: GraphQL implementation in pure Clojure
link:: https://github.com/walmartlabs/lacinia
platform:: [[JVM]],
status:: active, 
tags:: [[GraphQL]],
type:: library,

- [Documentation](https://lacinia.readthedocs.io/en/latest/overview.html)
-
- Comments
	- Also provides an integration with [[Pedestal]]
	- Valid identifier name contains only letters, numbers, and _
		- That's why snake case is often used in spite of not being idiomatic
-
- Summary
	- Parses [[GraphQL]] queries and guides the execution through ((620783a1-40c5-443e-bf7f-c00f375830b7))
	- **Schema written in EDN**
		- Declarative and self-descriptive
		  
		  ```clojure
		  {;; Types, shape of data
		   :objects {:Person {:description "Regular person"
		                      :fields      {:id   {:type (non-null ID)}
		                                    :name {:type (non-null String)}
		                                    :age  {:type (non-null Int)}}}}
		   
		   ;; Queries, how to retrieve data
		   :queries {:person_by_id {:type 	   :Person
		                            :description "Finds a person given its ID"
		                            :args        {:id {:type (non-null ID)}}
		                            :resolve     :keyword-of-resolver-function}}
		   
		   ;; Mutations, how to alter data (same syntax as `:queries`)
		   :mutations {:add_person {:type        :Person
		                            :description "Adds a new client"
		                            :args        {:name {:type (non-null String)}
		                                          :age  {:type (non-null Int)}}
		                            :resolve     :another-keyword-of-resolver-function}}}
		  
		  ;; Query a client
		  "{ person_by_id(id: \"1234\") { age name }}"
		  
		  ;; Add a client
		  "mutation { add_person(name: \"John Doe\", age: 30)}"
		  ```
		- Defines the shape of the accessible data
			- Types of data that can be returned
				- Built-in scalar types
					- `Boolean`
					- `Float`
					- `ID`
						- String that is not intended to be human-readable
					- `Int`
					- `String`
					- Modifiers on top of the scalar types
						- `(non-null Int)`
						- `(list (non-null String)`
				- Keywords
					- `:enums`
						- Enumerated types
						- Strings internally converted to keywords
							- ((620783a1-40c5-443e-bf7f-c00f375830b7)) receive them as keywords and must return keywords
						- ```clojure
						  {:enums
						   {:episode
						    {:description "The episodes of the original Star Wars trilogy."
						     :values      [:NEWHOPE :EMPIRE :JEDI]}}}}
						  
						  ;; Alternative syntax providing a finer description
						  {:enums
						   {:episode
						    {:description "The episodes of the original Star Wars trilogy."
						     :values [{:enum-value  :NEWHOPE
						               :description "The first one you saw."}
						              {:enum-value  :EMPIRE
						               :description "The good one."}
						              {:enum-value  :JEDI
						               :description "The one with the killer teddy bears."}]}}}
						  ```
					- `:interfaces`
						- Similar to interfaces found in object-oriented programming
						- Declares some fields that implementing objects must have
						- Optional `:description` on those fields are inherited by implementers
							- Avoids duplication of documentation
						- An interface cannot implements another interface
						- ((6207847c-a89b-4bcd-a01d-0124905792a4)) can only implement interfaces
							- Cannot extend other objects
						- ```clojure
						  {:interfaces
						   {:named
						    {:fields {:name {:type String}}}}
						  
						   :objects
						   {:person
						    {:implements [:named]
						     :fields {:name {:type String}
						              :age  {:type Int}}}
						  
						    :business
						    {:implements [:named]
						     :fields {:name           {:type String}
						              :employee_count {:type Int}}}}}
						  ```
					- `:objects`
					  id:: 6207847c-a89b-4bcd-a01d-0124905792a4
						- A object is a set of fields acting as a composite data structure
					- `:unions`
						- Between several ((6207847c-a89b-4bcd-a01d-0124905792a4))
						- ```clojure
						  :unions
						   {:search_result
						    {:members [:person :photo]}}
						  ```
			- `:queries`
			  id:: 620782e3-3d86-4146-a1ac-327eca09df42
				- Retrieve data, idempotent
				- Can pass arguments
				- Identify fields to return
				- Returns a map
					- On success, contains `:data` matching the shape of the query
					- On error, contains `:error`
					- Both if partially successful
			- `:mutations`
			  id:: 6207c42b-8e9e-4cb6-9a81-917b42817e78
				- Meant to produce side-effects
				- In practice, very similar to ((620782e3-3d86-4146-a1ac-327eca09df42))
					- Same syntax
					- Use ((620783a1-40c5-443e-bf7f-c00f375830b7)) as well
			- `:subscriptions`
				- Similar to `:queries` but meant for server push
				- *Streamer functions*
					- Initialize a subscription
					- Receive a callback to invoke on new data
						- If a resolver is not provided, new data is returned as is
					- Indicated by a keyword on `:stream`
				- ```clojure
				  {:objects
				   {:LogEvent
				    {:fields
				     {:severity {:type String}
				      :message {:type String}}}}
				  
				   :subscriptions
				   {:logs
				    {:type :LogEvent
				     :args {:severity {:type String}}
				     :stream :stream-logs}}}
				  ```
			- `:directive-defs`
				- Describe additional options to the [[GraphQL]] executor
				- [[Lacinia]] supports the current standard query directives
					- `@include`
					- `@skip`
				- Custom directives can be added to the schema
					- ```clojure
					  ;; Defines a field definition direct @access.
					  ;; Applied to the `:ultimate_answer` field.
					  {:directive-defs
					   {:access
					    {:locations #{:field-definition}
					     :args {:role {:type (non-null String)}}}}
					  
					   :queries
					   {:ultimate_answer
					    {:type String
					     :directives [{:directive-type :access
					                   :directive-args {:role "deep-thought"}}]}}}
					  ```
			- `:input-objects`
				- By default, arguments for ((620782e3-3d86-4146-a1ac-327eca09df42)) and ((6207c42b-8e9e-4cb6-9a81-917b42817e78)) are scalar
				- Input objects define composite types specially for inputs
			- `:scalars`
				- Custom scalar types can be defined with ser/de functions
				- ```clojure
				  {:scalars
				       {:Date
				        {:parse #(when (string? %)
				                   (try
				                     (.parse date-formatter %)
				                     (catch Throwable _
				                       nil)))
				         :serialize #(try
				                       (.format date-formatter %)
				                       (catch Throwable _
				                         nil))}}}
				  ```
				- In case of invalid values
					- Returning `nil` will make [[Lacinia]] create a generic type error
					- `ex-data` from a thrown exception is merged into the error map
	- **Field resolvers**
	  id:: 620783a1-40c5-443e-bf7f-c00f375830b7
		- Source of actual data
		- Regular Clojure functions identified by keywords in query descriptions, taking 3 arguments
			- Application context map
				- Allows some global state to be passed down into field resolvers at execution
				- [[Lacinia]] uses it for its own book-keeping with namespaces keys
			- Query arguments
				- Map `keyword -> argument`, provided by clients according to the query
			- Container value
				- Resolving can happen on several levels, can even be recursive
				- #+BEGIN_QUOTE
				  A book is being resolved. It contains an author which is also an object to resolve. The container value when resolving the author would be the already resolved book. It could contain the author as an ID the resolver would use to retrieve the actual author from a database.
				  #+END_QUOTE
		- Attached to the schema before it is compiled by [[Lacinia]]
			- Typically, those functions close over a data source like a database connection pool
		- It is possible to inspect what fields are to be returned
			- Notably useful for optimizating database queries
		- Using `com.walmartlabs.lacinia.resolve/with-extensions`, resolvers can return data beyond a query/mutation
			- E.g. Measuring the execution time
		- Return value
			- Interpreted as a successful case
			- `com.walmartlabs.lacinia.resolve/resolve-as`  wrapper
				- Resolve value
				- Resolve error
				- Both in case of partial success
			- Can be async (see `com.walmartlabs.lacinia.resolve/resolve-promise`)
		- Fields can also `:resolve`
			- More commonly useful for key re-mapping
			- It is a [[GraphQL]] property that even fiels can receive arguments when they have a resolver
-
- Closing thoughts
	- Many place, like type declaration, allow an optional `:description` (string for documentation)
	- Can include a `:deprecated` key set to true or a reason (string) for documentation
		- Fields
		- Enums
		- Queries
		- Mutations
		- Subscriptions
	- [[Lacinia]] can collect tracing information and execution time
		- Very usefl when scaling
-
-
- deprecation
- :description
- arguments on fields
- errors