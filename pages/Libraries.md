- In write-mode using [[Logseq]], can serve as a base for elaborated queries
	- For more examples, see [[Queries]]
- This is only a tiny set acting as a demonstration for this prototype
-
- query-table:: true
  query-properties:: [:page :description]
  #+BEGIN_QUERY
  {:title [:h2 "All currently listed libraries"]
   :query [:find (pull ?b [:block/name :block/properties])
  			  :where [?b :block/properties ?props]
  				           [(get ?props :type) ?type]
                             [(get ?type "library")]]
  :result-transform (fn [results]
                                  (sort-by :block/name (filter :block/name results)))}
  #+END_QUERY