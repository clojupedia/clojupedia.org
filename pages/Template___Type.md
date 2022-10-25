description:: Template for page types
see:: [[Type]]

- ---
- template:: Type
  template-including-parent:: false
	- filters:: {"type" false}
	  description::
	  link::
	  type:: [[Type]]
	- ---
	- {{query (page-property type "COPY PAGE TITLE")}}
	- #+BEGIN_COMMENT
	  Ensure:
	  - All properties are completed
	  - Query points to this page type
	  #+END_COMMENT