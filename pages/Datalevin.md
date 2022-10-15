description:: Simple durable Datalog database
link:: https://github.com/juji-io/datalevin
platform:: [[babashka]], [[jvm]], [[native-image]]
tags:: [[disk]], [[database]], [[datalog]], [[key-value store]]
type:: [[CLI,]] [[library]]

- Comments
	- Started out as a port of [[Datascript]] to Lightning Memory-Mapped Database (LMDB)
	- Embedded and does not have time-travel like [[Datomic]]
		- Great alternative to an embedded SQL database
	- Also has an API for a key-value store
	- Has a native command line interface
		- Useful for scripting