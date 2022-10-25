query-sort-by:: page
query-sort-desc:: false
query-properties:: [:page :description]
filters:: {"tag" false, "description" false}
Description:: Used as a property for pages representing types of pages

- ---
- {{query (page-property type "Type")}}
  query-properties:: [:page :description]
  query-sort-by:: page
  query-sort-desc:: false