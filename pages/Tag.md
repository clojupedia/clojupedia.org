filters:: {}
description:: All existing tags
---

- {{query (page-property type Tag)}}
  query-sort-by:: page
  query-sort-desc:: false
  query-properties:: [:page :description]