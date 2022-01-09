- Follow a simple syntax for simple but often sufficient queries
- See [this. tutorial](https://docs.logseq.com/#/page/queries)
-
- Examples
	- All libraries related to Datalog databases supporting Clojurescript
		- {{query (and (property type library) (page-tags database datalog) (property platform browser))}}
		  query-table:: false
	- All libraries related to SQL
		- {{query (and (property type library) (page-tags SQL))}}