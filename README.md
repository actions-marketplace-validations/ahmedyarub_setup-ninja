![Main Workflow](https://github.com/ahmedyarub/setup-ninja/workflows/Main%20Workflow/badge.svg)

# setup-ninja

Github Action for configuring ninja build tool into PATH

Official ninja-build binaries are downloaded from [ninja-build](https://github.com/ninja-build/ninja/releases) github releases and added to the PATH of runner.

## Quickstart
A simple matrix workflow which build CMake project with Ninja
```yaml
jobs:
  build:
    runs-on: ${{ matrix.config.os }}
    strategy:
      matrix:
        config:
          - { name: "Windows MSVC", os: windows-latest, cc: "cl", cxx: "cl" }
          - { name: "Ubuntu gcc", os: ubuntu-latest, cc: "gcc", cxx: "g++" }
          - { name: "MacOS clang", os: macos-latest, cc: "clang", cxx: "clang++" }
        
    steps:
      - name: Setup Ninja
        uses: ahmedyarub/setup-ninja@master
        with:
          # ninja version to download. Default: 1.11.1
          version: 1.11.1

      - name: Build with CMake
        uses: ahmedyarub/action-cmake-build@master
        with:
          build-dir: ${{ runner.workspace }}/build
          cc: ${{ matrix.config.cc }}
          cxx: ${{ matrix.config.cxx }}
          configure-options: -G Ninja
          build-type: Release
        
```

### Action Reference: All Input/Output & Defaults
[action.yml](https://github.com/ahmedyarub/setup-ninja/blob/master/action.yml) 

## License
All the content in this repository is licensed under the MIT License.

Copyright (c) 2019-2020 Ashutosh Varma