---
warning: DO NOT CHANGE THIS MANUALLY, THIS IS GENERATED BY https://github/duckdb/community-extensions repository, check README there
title: splink_udfs
excerpt: |
  DuckDB Community Extensions
  Record linkage functions for use in Splink

extension:
  name: splink_udfs
  description: Record linkage functions for use in Splink
  version: 0.0.1
  language: C++
  build: cmake
  license: MIT
  maintainers:
    - RobinL

repo:
  github: moj-analytical-services/splink_udfs
  ref: 08cc43c05af5cfeaa885f4fcad2da335e2e3856f

docs:
  hello_world: |
    LOAD splink_udfs;
    SELECT soundex('Robert');  -- returns 'R163'
  extended_description: |
    The initial version of the splink_udfs extension provides
    a scalar function `soundex(VARCHAR) → VARCHAR` implementing
    the Soundex phonetic algorithm. Other record linkage-related
    functions will be added to this extension as it develops.

extension_star_count: 2
extension_star_count_pretty: 2
extension_download_count: null
extension_download_count_pretty: n/a
image: '/images/community_extensions/social_preview/preview_community_extension_splink_udfs.png'
layout: community_extension_doc
---

### Installing and Loading
```sql
INSTALL {{ page.extension.name }} FROM community;
LOAD {{ page.extension.name }};
```

{% if page.docs.hello_world %}
### Example
```sql
{{ page.docs.hello_world }}```
{% endif %}

{% if page.docs.extended_description %}
### About {{ page.extension.name }}
{{ page.docs.extended_description }}
{% endif %}

### Added Functions

<div class="extension_functions_table"></div>

| function_name | function_type | description | comment | examples |
|---------------|---------------|-------------|---------|----------|
| soundex       | scalar        | NULL        | NULL    |          |


