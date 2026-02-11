# Changelog

## [1.0.0] - 2026-02-11

### Added

- Initial release of nfx-meta metapackage
- Version-locked nfx library dependencies with guaranteed compatibility
- Support for 10 nfx libraries:
  - nfx-containers (v0.4.1) - High-performance hash containers
  - nfx-cpu (v0.1.4) - CPU feature detection and utilities
  - nfx-datatypes (v0.4.0) - Common data types (Int128, Decimal)
  - nfx-datetime (v0.4.2) - Date, time, and duration types
  - nfx-hashing (v0.2.0) - Hashing algorithms and utilities
  - nfx-json (v1.3.4) - JSON parsing and generation
  - nfx-resource (v1.1.0) - Resource embedding and management
  - nfx-serialization (v0.9.1) - C++ type serialization with JSON support
  - nfx-stringbuilder (v0.6.0) - Efficient string building and concatenation
  - nfx-stringutils (v0.6.2) - String manipulation utilities
- Configurable library inclusion via CMake options (NFX_META_ENABLE_*)
- Build control options for tests, samples, benchmarks, and documentation
- Single unified meta target (nfx::meta) for simplified dependency management
- Cross-platform support (Linux, Windows)
