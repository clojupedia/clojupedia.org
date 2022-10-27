alias:: Tag
filters:: {"type" false}
description:: All existing tags
type:: [[Property]]
---

- {{query (page-property type Tag)}}
  query-sort-by:: page
  query-sort-desc:: false
  query-properties:: [:page :description]