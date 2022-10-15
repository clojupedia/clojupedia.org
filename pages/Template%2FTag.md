title:: Template/Tag

- ---
- template:: Tag
  template-including-parent:: false
	- description::
	  link::
	  title:: (copy page title) 
	  type:: [[Tag]]
	- ---
	- {{query (page-property tag "COPY PAGE TITLE")}}
	- #+BEGIN_COMMENT
	  Ensure:
	  - All properties are completed
	  - Query points to this tag
	  #+END_COMMENT