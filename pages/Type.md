filters:: {"tag" false, "description" false}
query-sort-by:: page
query-sort-desc:: false
query-properties:: [:page :description]
Description:: Used as a property for pages representing types of pages
title:: type

- ---
- {{query (page-property type "Type")}}
  query-properties:: [:page :description]
  query-sort-by:: page
  query-sort-desc:: false