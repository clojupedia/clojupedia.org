description:: Type for libraries
filters:: {"type" false}
type:: [[Type]]

- ---
- {{query (page-property type Library)}}
  query-sort-by:: page
  query-sort-desc:: false
  query-properties:: [:page :description :platform]