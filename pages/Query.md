title:: Learn/Query

- Queries notably allow searching pages based on their tags and various properties
- Users can write their own queries using the desktop [[Logseq]] application
- ---
- [Advanced queries](https://docs.logseq.com/#/page/advanced%20queries) allow running actual [[Datalog]] and even presenting results using [[Hiccup]] syntax
- However, Clojupedia uses [simple queries](https://docs.logseq.com/#/page/queries) since they are a lot more concise and amply sufficient
- ---
- Commonly used "closes" are
	- `page-property`
		- For filtering pages based on their [[Learn/Properties]]
		- E.g. `(page-property "platform" "Browser")`
	- `and`
		- For combining and repeating any of the above
			- {{query (and (page-property tag  "Datalog") (page-property platform "Browser"))}}
			  query-sort-by:: page
			  query-sort-desc:: false
			  query-properties:: [:page :description :platform]