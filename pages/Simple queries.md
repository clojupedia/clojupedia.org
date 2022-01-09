- Follow a simple syntax for simple but often sufficient queries
- Offer quick answers
- See [this tutorial](https://docs.logseq.com/#/page/queries)
-
- Examples
	- All libraries related to Datalog databases working in the browser
		- {{query (and (property type library) (page-tags database datalog) (property platform browser))}}
		  query-table:: false
	- All actively maintained libraries related to SQL
		- {{query (and (property type library) (page-tags SQL) (property status active))}}
		  query-table:: false