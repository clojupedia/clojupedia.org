description:: Template for platforms
see:: [[Platform]]
title:: Template/Platform

- ---
- template:: Platform
  template-including-parent:: false
	- filters:: {"type" false}
	  description::
	  link::
	  title:: (copy page title) 
	  type:: [[Platform]]
	- ---
	- {{query (page-property platform "COPY PAGE TITLE")}}
	- #+BEGIN_COMMENT
	  Ensure:
	  - All properties are completed
	  - Query points to this platform
	  #+END_COMMENT