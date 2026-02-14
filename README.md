# nfx-meta

## Overview

nfx-meta is a CMake metapackage that provides a single dependency point for all nfx libraries with version-locked combinations that are tested and guaranteed to work together. It eliminates dependency conflicts, simplifies integration, and ensures version compatibility across the entire nfx ecosystem.

## Included Libraries

This metapackage includes the following nfx libraries with locked compatible versions:

| Library                                                            | Version | Description                                 |
| ------------------------------------------------------------------ | ------- | ------------------------------------------- |
| [nfx-containers](https://github.com/nfx-libs/nfx-containers)       | 0.5.1   | High-performance hash containers            |
| [nfx-cpu](https://github.com/nfx-libs/nfx-cpu)                     | 0.1.4   | CPU feature detection and utilities         |
| [nfx-datatypes](https://github.com/nfx-libs/nfx-datatypes)         | 0.4.1   | Common data types (Int128, Decimal)         |
| [nfx-datetime](https://github.com/nfx-libs/nfx-datetime)           | 0.5.0   | Date, time, and duration types              |
| [nfx-hashing](https://github.com/nfx-libs/nfx-hashing)             | 0.3.1   | Hashing algorithms and utilities            |
| [nfx-json](https://github.com/nfx-libs/nfx-json)                   | 1.4.1   | JSON parsing and generation                 |
| [nfx-resource](https://github.com/nfx-libs/nfx-resource)           | 1.1.0   | Resource embedding and management           |
| [nfx-serialization](https://github.com/nfx-libs/nfx-serialization) | 0.9.2   | C++ type serialization with JSON support    |
| [nfx-stringbuilder](https://github.com/nfx-libs/nfx-stringbuilder) | 0.6.2   | Efficient string building and concatenation |
| [nfx-stringutils](https://github.com/nfx-libs/nfx-stringutils)     | 0.6.4   | String manipulation utilities               |

## Requirements

- **CMake** 3.20 or later
- **C++20 compiler** with concepts support

## Usage

### Basic Integration

```cmake
include(FetchContent)

FetchContent_Declare(nfx-meta
    GIT_REPOSITORY https://github.com/nfx-libs/nfx-meta.git
    GIT_TAG        1.2.0
)
FetchContent_MakeAvailable(nfx-meta)

# Link against all enabled nfx libraries
target_link_libraries(your-target PRIVATE nfx::meta)
```

### Selective Library Inclusion

Control which libraries are included via CMake options:

```cmake
# Enable only specific libraries
set(NFX_META_ENABLE_SERIALIZATION ON CACHE BOOL  "" FORCE)
set(NFX_META_ENABLE_CONTAINERS    ON CACHE BOOL  "" FORCE)
set(NFX_META_ENABLE_RESOURCE      OFF CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(nfx-meta)
```

### Build Options

Control what gets built for enabled libraries:

```cmake
# Build tests for all enabled libraries
set(NFX_META_BUILD_TESTS ON CACHE BOOL "" FORCE)

# Build benchmarks for performance testing
set(NFX_META_BUILD_BENCHMARKS ON CACHE BOOL "" FORCE)

# Build samples and documentation
set(NFX_META_BUILD_SAMPLES       ON CACHE BOOL "" FORCE)
set(NFX_META_BUILD_DOCUMENTATION ON CACHE BOOL "" FORCE)

FetchContent_MakeAvailable(nfx-meta)
```

### Individual Library Access

All individual libraries remain accessible even when using the metapackage:

```cmake
target_link_libraries(your-target PRIVATE
    nfx::serialization  # Just JSON serialization
    nfx::containers     # Just hash containers
    # ... or use nfx::meta for everything
)
```

## CMake Options

### Library Selection

| Option                          | Description                      | Default |
| ------------------------------- | -------------------------------- | ------- |
| `NFX_META_ENABLE_CONTAINERS`    | Enable nfx-containers library    | `OFF`   |
| `NFX_META_ENABLE_CPU`           | Enable nfx-cpu library           | `OFF`   |
| `NFX_META_ENABLE_DATATYPES`     | Enable nfx-datatypes library     | `OFF`   |
| `NFX_META_ENABLE_DATETIME`      | Enable nfx-datetime library      | `OFF`   |
| `NFX_META_ENABLE_HASHING`       | Enable nfx-hashing library       | `OFF`   |
| `NFX_META_ENABLE_JSON`          | Enable nfx-json library          | `OFF`   |
| `NFX_META_ENABLE_RESOURCE`      | Enable nfx-resource library      | `OFF`   |
| `NFX_META_ENABLE_SERIALIZATION` | Enable nfx-serialization library | `OFF`   |
| `NFX_META_ENABLE_STRINGBUILDER` | Enable nfx-stringbuilder library | `OFF`   |
| `NFX_META_ENABLE_STRINGUTILS`   | Enable nfx-stringutils library   | `OFF`   |

### Build Control

| Option                             | Description                               | Default |
| ---------------------------------- | ----------------------------------------- | ------- |
| `NFX_META_BUILD_TESTS`             | Build tests for enabled libraries         | `OFF`   |
| `NFX_META_BUILD_SAMPLES`           | Build samples for enabled libraries       | `OFF`   |
| `NFX_META_BUILD_BENCHMARKS`        | Build benchmarks for enabled libraries    | `OFF`   |
| `NFX_META_BUILD_DOCUMENTATION`     | Build documentation for enabled libraries | `OFF`   |
| `NFX_META_WITH_JSON_SERIALIZATION` | Enable JSON support in serialization      | `OFF`   |

### Installation

| Option                      | Description                          | Default |
| --------------------------- | ------------------------------------ | ------- |
| `NFX_META_INSTALL_PROJECT`  | Install nfx-meta with unified export | `OFF`   |
| `NFX_META_ENABLE_PACKAGING` | Enable CPack packaging support       | `OFF`   |

**Note:** When `NFX_META_INSTALL_PROJECT=ON`, all enabled libraries are installed together in a single unified CMake export (`nfx-meta-targets`). This avoids CMake export conflicts and provides a clean installation that can be used with `find_package(nfx-meta)`.

## Installation

### Installing the Metapackage

To install nfx-meta system-wide with all libraries:

```bash
cmake -B build \
  -DNFX_META_ENABLE_CONTAINERS=ON \
  -DNFX_META_ENABLE_CPU=ON \
  -DNFX_META_ENABLE_DATATYPES=ON \
  -DNFX_META_ENABLE_DATETIME=ON \
  -DNFX_META_ENABLE_HASHING=ON \
  -DNFX_META_ENABLE_JSON=ON \
  -DNFX_META_ENABLE_RESOURCE=ON \
  -DNFX_META_ENABLE_SERIALIZATION=ON \
  -DNFX_META_ENABLE_STRINGBUILDER=ON \
  -DNFX_META_ENABLE_STRINGUTILS=ON \
  -DNFX_META_WITH_JSON_SERIALIZATION=ON \
  -DNFX_META_INSTALL_PROJECT=ON \
  -DCMAKE_BUILD_TYPE=Release

cmake --build build
sudo cmake --install build
```

### Using Installed Metapackage

After installation, use it in your project:

```cmake
cmake_minimum_required(VERSION 3.20)
project(MyProject)

find_package(nfx-meta REQUIRED)

add_executable(myapp main.cpp)
target_link_libraries(myapp PRIVATE nfx::meta)
```

## Versioning

The metapackage uses **semantic versioning** (MAJOR.MINOR.PATCH):

- **MAJOR**: Breaking changes in any included library or version combinations
- **MINOR**: New library versions (backward compatible)
- **PATCH**: Bug fixes, documentation updates

### Version History

See [CHANGELOG.md](CHANGELOG.md) for detailed version history and release notes.

## Building from Source

```bash
# Clone the repository
git clone https://github.com/nfx-libs/nfx-meta.git
cd nfx-meta

# Configure with all libraries enabled
cmake -B build \
  -DNFX_META_ENABLE_CONTAINERS=ON \
  -DNFX_META_ENABLE_CPU=ON \
  -DNFX_META_ENABLE_DATATYPES=ON \
  -DNFX_META_ENABLE_DATETIME=ON \
  -DNFX_META_ENABLE_HASHING=ON \
  -DNFX_META_ENABLE_JSON=ON \
  -DNFX_META_ENABLE_RESOURCE=ON \
  -DNFX_META_ENABLE_SERIALIZATION=ON \
  -DNFX_META_ENABLE_STRINGBUILDER=ON \
  -DNFX_META_ENABLE_STRINGUTILS=ON

# Build
cmake --build build
```

## Packaging

### Creating Distribution Packages

To create binary and source packages (TGZ, DEB, RPM):

```bash
# Configure with packaging enabled
cmake -B build \
  -DNFX_META_ENABLE_CONTAINERS=ON \
  -DNFX_META_ENABLE_CPU=ON \
  -DNFX_META_ENABLE_DATATYPES=ON \
  -DNFX_META_ENABLE_DATETIME=ON \
  -DNFX_META_ENABLE_HASHING=ON \
  -DNFX_META_ENABLE_JSON=ON \
  -DNFX_META_ENABLE_RESOURCE=ON \
  -DNFX_META_ENABLE_SERIALIZATION=ON \
  -DNFX_META_ENABLE_STRINGBUILDER=ON \
  -DNFX_META_ENABLE_STRINGUTILS=ON \
  -DNFX_META_WITH_JSON_SERIALIZATION=ON \
  -DNFX_META_INSTALL_PROJECT=ON \
  -DNFX_META_ENABLE_PACKAGING=ON \
  -DCMAKE_BUILD_TYPE=Release

# Build the project
cmake --build build

# Create packages
cd build
cpack
```

This will generate:
- **Source packages**: `nfx-meta-1.2.0.tar.gz`, `nfx-meta-1.2.0.zip`
- **Binary archive**: `nfx-meta-1.2.0-Linux.tar.gz`
- **DEB package** (Linux): `nfx-meta_1.2.0_amd64.deb`
- **RPM package** (Linux): `nfx-meta-1.2.0-1.x86_64.rpm`

## License

MIT License - See [LICENSE](LICENSE) file for details

---

_Updated on February 14, 2026_
