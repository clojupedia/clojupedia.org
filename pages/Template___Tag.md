description:: Template for tag pages
see:: [[Tag]]

- ---
- template:: Tag
  template-including-parent:: false
	- filters:: {"type" false}
	  description::
	  link::
	  type:: [[Tag]]
	- ---
	- {{query (page-property tag "COPY PAGE TITLE")}}
	- #+BEGIN_COMMENT
	  Ensure:
	  - All properties are completed
	  - Query points to this tag
	  #+END_COMMENT