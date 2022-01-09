- Powered by [[Datascript]] and [SCI](https://github.com/babashka/sci)
- Results can even be formatted in Hiccup for customized UIs
- See [this tutorial](https://docs.logseq.com/#/page/advanced%20queries)
-
- Example
	- [[Libraries]] is an example that can be refined to more complex queries
	- Code
		- ```clojure
		  #+BEGIN_QUERY
		  {:title [:h2 "All currently listed libraries"]
		   :query [:find (pull ?b [*])
		  		 :where [?b :block/properties ?props]
		  		        [(get ?props :type) ?type]
		                  [(get ?type "library")]]
		  :result-transform (fn [results]
		                      (sort-by :block/name (filter :block/name results)))}
		  #+END_QUERY
		  ```
		-