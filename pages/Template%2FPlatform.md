description:: Template for platforms
title:: Template/Platform

- description:: Template for tag pages
  title:: Template/Tag
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