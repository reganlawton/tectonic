# Change Log
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/) 
and this project adheres to [Semantic Versioning](http://semver.org/).

## [2.1.2] - 2017-08-16
### Fixed
- #87 - When params change we now make new requests. Thanks @aindeev
- #88 - Fixed infinite loop error when adding cache-control header. 
Thanks @aindeev again!
- Fixed an issue in which submodule field values were sometimes instantiated
incorrectly

## [2.1.1] - 2017-08-04
### Fixed
- Set query cache property based on lowest cacheFor TTL in source definitioon or
models.

## [2.1] - 2017-08-04
### Added
- Allow routes and models to define their own cache TTL
### Fixed
- No longer pass tectonic state down to wrapped components
### Changed
- Change from GPL to MIT license.  Go nuts.

## [2.0.2] - 2016-02-07
### Fixed
- Removed PropType helpers from models to comply with React 15 [#60]
- Queries with empty responses have their status updated [#58]

## [2.0.1] - 2016-02-04
### Fixed
- Apply model filtering before instantiating sub-models [#55]

## [2.0.0] - 2016-01-30
### Added
- Added .query prop, standardized the way we make non-GET queries in
components [#42]
- Drivers can now have default parameters [#40]

### Changed
- Throw an error when providing source definitions for nameless models [#32]
- Driver functions are now added to `manager.drivers` vs `manager` [#39]
- Made the ingoring query log a warning for better dev [#28]

### Fixed
- Saving query responses should remove deleted IDs from blacklist [#37]


## [1.2.1] - 2016-10-21
### Added
- Allow @load() to connect to state via @load((props, state) => {})

## [1.2.0] - 2016-10-21
### Added
- Added new Status object injected for each @load query key. This replaces
  string statuses with new information including the HTTP status code and error
  message.
- Added flow

## [1.1.13] - 2016-10-04
### Changed
- Ensure manager always adds props for PENDING and ERROR states

## [1.1.11] - 2016-10-04
### Changed
- Changed queries to include a _force property and force() function, ensuring
  that any queries created through .props.load() are forced to resolve despite
  potentially having parent queries.

## [1.1.10] - 2016-10-04
### Added
- Added .load() to component props (see
  #5ccc6c5123a0c43bd3a7d67fed3e52e825e06a55)

## [1.1.9] - 2016-09-21
### Fixed
- Fixed undefined val submodule assignment error in model.js

## [1.1.8] - 2016-09-21
### Changed
- Removed `setTimeout` call in decorator by adding in-flight query
  deduplication. We now track all in-flight queries and match duplicates to
  their predecessors, ensuring that when the original query succeeds it marks
  all duplicates as successful (even if they were created after the initial
  resolution).

## [1.1.7] - 2016-09-21
### Added
- Added static `filter` method to models for per-model data filtering, prior to
  setting model data. This allows you to write custom transform logic for each
  model

### Changed
- We now set internal query statuses to PENDING, allowing us to skip these
  queries in the resolver

## [1.1.6] - 2016-09-21
### Changed
- Always re-request GET queries with ERROR cache status
- Never re-request queries with ERROR status set internally; these queries were
  pre-existing from an existing component's render

## [1.1.5]
### Fixed
- Ensure DELETE queries have their status set to SUCCESS in reducer for
  repeatable queries

## [1.1.4] - 2016-09-19
### Fixed
- Broken release! Apologies.

## [1.1.3] - 2016-09-19
### Added
- Added `getModel` to wrapped component for manually fetching

## [1.1.2] - 2016-09-14
### Added
- Added support for submodels inside tectonic models

## [1.1.1] - 2016-09-11
### Fixed
- Ensures queries are cached with `null` response (HTTP 204)

## [1.1.0] - 2016-09-11
### Added
- Ensures deleted models via `deleteModel` mark models as deleted in the
  reducer
- Update getQueryData to respect deleted models and model-specific cache
  expiration.
  Components will now never receive data from deleted or expired models
