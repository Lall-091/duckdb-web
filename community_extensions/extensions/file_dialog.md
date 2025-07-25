---
warning: DO NOT CHANGE THIS MANUALLY, THIS IS GENERATED BY https://github/duckdb/community-extensions repository, check README there
title: file_dialog
excerpt: |
  DuckDB Community Extensions
  Choose a file via native file dialog

extension:
  name: file_dialog
  description: Choose a file via native file dialog
  version: 0.0.3
  language: Rust
  build: cargo
  license: MIT
  excluded_platforms: "wasm_mvp;wasm_eh;wasm_threads;linux_amd64_musl"
  requires_toolchains: "rust;python3"
  maintainers:
    - yutannihilation

repo:
  github: yutannihilation/duckdb-ext-file-dialog
  ref: 7e9d768e805b9b4853b28778debef7dee333e936

docs:
  hello_world: |
    FROM read_csv(choose_file());

    -- Optionally, you can filter files by the extension. For example, this
    -- makes the dialog list CSV files only
    FROM read_csv(choose_file('csv'));
  extended_description: |
    This extension is a tiny utility to choose a file interactively.

extension_star_count: 13
extension_star_count_pretty: 13
extension_download_count: null
extension_download_count_pretty: n/a
image: '/images/community_extensions/social_preview/preview_community_extension_file_dialog.png'
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

| function_name | function_type |             description              | comment |            examples             |
|---------------|---------------|--------------------------------------|---------|---------------------------------|
| choose_file   | scalar        | Choose a file via native file dialog | NULL    | [FROM read_csv(choose_file());] |


