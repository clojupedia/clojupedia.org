title:: Learn/Query

- Queries notably allow searching pages based on their tags and properties
- Users can write their own queries in [[Learn/Write mode]]
- ---
- [Advanced queries](https://docs.logseq.com/#/page/advanced%20queries) allow running actual [[Datalog]] and even presenting results using [[Hiccup]] syntax
- However, Clojupedia uses [simple queries](https://docs.logseq.com/#/page/queries) since they are a lot more concise and amply sufficient
	- See [[Query]] and its whole hierarchy of prepared queries
	- Commonly used "closes" are
		- `pages-tags`
			- For filtering pages based on their [[Learn/Tags]]
			- E.g. `(page-tags "Datalog")`
		- `page-property`
			- For filtering pages based on their [[Learn/Properties]]
			- E.g. `(page-property "platform" "Browser")`
		- `and`
			- For combining and repeating any of the above
			- {{query (and (page-tags  "Datalog") (page-property "platform" "browser"))}}
			  query-sort-by:: page
			  query-sort-desc:: false
			  query-properties:: [:page :description :platform]