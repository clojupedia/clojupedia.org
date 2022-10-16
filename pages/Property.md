filters:: {"type" false}
description:: All pages have properties near the title, like `type::`

- ---
- {{query (page-property type "Property")}}
  query-properties:: [:page :description]
  query-sort-by:: page
  query-sort-desc:: false