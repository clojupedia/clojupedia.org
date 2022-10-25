description:: Template for platforms
see:: [[Platform]]

- ---
- template:: Platform
  template-including-parent:: false
	- filters:: {"type" false}
	  description::
	  link::
	  type:: [[Platform]]
	- ---
	- {{query (page-property platform "COPY PAGE TITLE")}}
	- #+BEGIN_COMMENT
	  Ensure:
	  - All properties are completed
	  - Query points to this platform
	  #+END_COMMENT