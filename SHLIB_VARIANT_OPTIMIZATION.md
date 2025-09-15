# Building OpenSSL with SHLIB_VARIANT

## Overview

SHLIB_VARIANT allows building multiple OpenSSL variants with different library suffixes for parallel installation.

## Basic Usage

```bash
# Configure with variant
./Configure [platform] --shlib-variant=debug
make && make install

# Produces: libcrypto-debug.so, libssl-debug.so
```

## Using Variant Libraries

### pkg-config
```bash
pkg-config --libs openssl-debug
# Output: -lssl-debug -lcrypto-debug
```

### CMake
```cmake
find_package(OpenSSL REQUIRED)
target_link_libraries(app OpenSSL::SSL OpenSSL::Crypto)
```

### Manual Linking
```bash
gcc app.c -lssl-debug -lcrypto-debug
```

## Examples

```bash
# Debug variant
./Configure linux-x86_64 --shlib-variant=debug

# Production variant  
./Configure linux-x86_64 --shlib-variant=prod

# FIPS variant
./Configure linux-x86_64 --shlib-variant=fips enable-fips
```

## Multiple Variants

```bash
# Install multiple variants with different prefixes
./Configure linux-x86_64 --shlib-variant=debug --prefix=/opt/openssl-debug
./Configure linux-x86_64 --shlib-variant=prod --prefix=/opt/openssl-prod
```

## Troubleshooting

Check installed libraries:
```bash
ls -la /usr/local/lib/libssl-*
pkg-config --list-all | grep openssl
```
