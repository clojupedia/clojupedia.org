filters:: {"type" false}
description:: Any software meant to run on its own
type:: [[Type]]

- ---
- {{query (page-property type "Application")}}
  query-sort-by:: page
  query-sort-desc:: false
  query-properties:: [:page :description :platform]