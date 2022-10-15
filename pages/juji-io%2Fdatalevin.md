description:: Simple durable Datalog database
link:: https://github.com/juji-io/datalevin
platform:: [[babashka]], [[jvm]], [[Native-image]]
tags:: [[Database]], [[Datalog]], [[Key-value store]], [[Persistent]]
type:: [[CLI]], [[library]]
title:: juji-io/datalevin

- Comments
	- Started out as a port of [[tonsky/datascript]] to Lightning Memory-Mapped Database (LMDB)
	- Embedded and does not have time-travel like [[cognitect/datomic]]
		- Great alternative to an embedded SQL database
	- Also has an API for a key-value store
	- Has a native command line interface
		- Useful for scripting