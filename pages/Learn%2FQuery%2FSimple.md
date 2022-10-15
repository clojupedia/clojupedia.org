title:: Learn/Query/Simple

- Powerful way for searching projects based on their properties
- With time, a collection of commonly used queries will be built and maintained
	- Useful for the read-only website
	- Will also serve as examples for users opening this project in [[Logseq]] (write-mode)
- See [this tutorial](https://docs.logseq.com/#/page/queries) about queries for more details
- ---
-
- Powered by [[tonsky/datascript]] and [SCI](https://github.com/babashka/sci)
- Results can even be formatted in Hiccup for customized UIs
- See [this tutorial](https://docs.logseq.com/#/page/advanced%20queries)
-
- Example
	- Code
		- #+BEGIN_QUERY
		  {:title [:h2 "All currently listed libraries"]
		   :query [:find (pull ?b [*])
		  		 :where (property ?b :type "library")]
		  :result-transform (fn [results]
		                      (sort-by :block/name (filter :block/name results)))}
		  #+END_QUERY
		-
-
- E.g. All Datalog-related libraries supporting the browser
	- {{{query (and (page-property type library) (page-tags database datalog) (page-property platform browser))}}}
	  query-table:: false
	  query-properties:: [:page :description :platform]
	  query-sort-by:: page
	  query-sort-desc:: false
-
-
-
- #+BEGIN_QUERY
  {:title [:h2 "All currently listed libraries"]
   :query [:find (pull ?b [*])
  		 :where [?b :block/properties ?props]
  		        [(get ?props :type) ?type]
                  [(get ?type "library")]]
  :result-transform (fn [results]
                      (sort-by :block/name (filter :block/name results)))}
  #+END_QUERY
-
-
- query-table:: false
  #+BEGIN_QUERY
  {:title [:h2 "Programming languages list"]
  
  :collapsed? true
   :query [:find (pull ?b [*])
           :where
           (property ?b :type "library")]}
  #+END_QUERY
-