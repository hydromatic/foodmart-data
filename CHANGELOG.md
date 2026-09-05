<!--
{% comment %}
Licensed to Julian Hyde under one or more contributor license
agreements.  See the NOTICE file distributed with this work
for additional information regarding copyright ownership.
Julian Hyde licenses this file to you under the Apache
License, Version 2.0 (the "License"); you may not use this
file except in compliance with the License.  You may obtain a
copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,
either express or implied.  See the License for the specific
language governing permissions and limitations under the
License.
{% endcomment %}
-->
# Foodmart data release history and change log

For a full list of releases, see
[GitHub](https://github.com/hydromatic/foodmart-data/releases).

## <a id="v0.6.1" href="https://github.com/hydromatic/foodmart-data/releases/tag/v0.6.1">v0.6.1</a> / 2026-09-05

Adds a Rust crate,
[foodmart-data](https://crates.io/crates/foodmart-data). Like the Go
module, it embeds the CSV files and has no dependencies.

It requires Rust 1.71 or higher.

The Go module is unchanged.

* Add a Rust crate,
  [`foodmart-data`](https://crates.io/crates/foodmart-data)
* Generate `src/schema.rs`, as well as `schema.go`, from the schema in
  `tools/schema.py`
* In `HOWTO.md`, describe the Rust release process, and the policy the
  minimum supported versions follow

## <a id="v0.6.0" href="https://github.com/hydromatic/foodmart-data/releases/tag/v0.6.0">v0.6.0</a> / 2026-09-05

First release. It provides the Foodmart data set as CSV files, one
per table, embedded in a Go module that has no dependencies.

It requires Go 1.22 or higher.

The version number matches
[foodmart-data-hsqldb](https://github.com/julianhyde/foodmart-data-hsqldb)
0.6, from which the CSV files are taken.

* Add the Foodmart data set as 26 CSV files
* Add a Go module, `github.com/hydromatic/foodmart-data`
* Generate `schema.go` from the schema in `tools/schema.py`
* Add a `golangci-lint` configuration enabling most linters
* Add a lint test that ensures that every source file has a header
* Add `HOWTO.md`, describing the Go release process

<!-- End CHANGELOG.md -->
