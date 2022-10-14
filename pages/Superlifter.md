description:: A `DataLoader` for Clojure/script
link:: https://github.com/oliyh/superlifter
platform:: [[Browser]] , [[JVM]], [[NodeJS]]
status:: active, 
tags:: [[Data access]], [[GraphQL]] 
type:: library,

-
- **DataLoader** pattern is a way for batching data access
- Often associated with [[GraphQL]]
	- Instead of retrieving data separately in each resolver, operations can be batched together
	- Has explicit support for [[Lacinia]]
	- Links
		- https://www.juxt.pro/blog/superlifter
			- Describes using this library with [[Lacinia]]
		- https://xuorig.medium.com/the-graphql-dataloader-pattern-visualized-3064a00f319f
		- https://github.com/graphql/dataloader