description:: Simple durable Datalog database
link:: https://github.com/juji-io/datalevin
platform:: [[Babashka]], [[jvm]], [[Native-image]]
tag:: [[Database]], [[Datalog]], [[Key-value store]], [[Persistent]]
type:: [[CLI]], [[Library]]

- ---
- Started out as a port of [[tonsky/datascript]] to Lightning Memory-Mapped Database (LMDB)
- Embedded and does not have time-travel like [[cognitect/datomic]]
	- Great alternative to an embedded SQL database
- Also has an API for a key-value store
- Has a native command line interface
	- Useful for scripting