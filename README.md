# Sumokoin

**Sumokoin** is a privacy-centric cryptocurrency forked from [Monero](https://github.com/monero-project/monero), built on the CryptoNote protocol. It is designed to provide untraceable, unlinkable, and fungible digital transactions.

> **Note:** This is a test modification to demonstrate file update tracking and diff display functionality.

---

## Table of Contents

- [About](#about)
- [Features](#features)
- [Dependencies](#dependencies)
- [Building from Source](#building-from-source)
  - [Linux (Ubuntu/Debian)](#linux-ubuntudebian)
  - [macOS](#macos)
  - [Windows (MSYS2/MinGW)](#windows-msys2mingw)
  - [Android](#android)
  - [iOS](#ios)
  - [Cross-compilation (using depends)](#cross-compilation-using-depends)
- [Build Targets](#build-targets)
- [License](#license)

## About

**Sumokoin** leverages the CryptoNote technology with advanced cryptographic features:
- **Ring Signatures** — Hide sender identity among a group of possible signers
- **Stealth Addresses** — Protect recipient privacy with one-time addresses
- **RingCT (Ring Confidential Transactions)** — Conceal transaction amounts

It uses the **LMDB database** for efficient blockchain storage and supports a wide range of platforms and architectures.

## Features

- **Privacy by default** — Ring signatures, stealth addresses, and RingCT
- **CryptoNote protocol** — Proven cryptographic foundation
- **LMDB database** — Fast and reliable blockchain storage
- **Multi-platform** — Linux, Windows, macOS, FreeBSD, OpenBSD, DragonFly BSD, Android, iOS
- **Multi-architecture** — x86-64, ARM (v6/v7/v8/aarch64), POWER (ppc64le/ppc64/ppc), s390x
- **Security hardened** — Stack protector, ASLR, RELRO, and other compile-time protections

## Dependencies

| Dependency       | Min. Version | Purpose                          |
|------------------|--------------|----------------------------------|
| GCC              | 7.0          | C/C++ compiler                   |
| Clang (alt.)     | 8.0          | C/C++ compiler                   |
| CMake            | 3.5          | Build system                     |
| Boost            | 1.62         | System, filesystem, thread, etc. |
| OpenSSL          | —            | SHA-256, SSL/TLS                 |
| libzmq           | —            | ZeroMQ messaging                 |
| libunbound       | —            | DNS resolution                   |
| libsodium        | —            | Cryptography                     |
| HIDAPI           | —            | Hardware wallet support           |
| GNU Readline     | —            | Interactive CLI (optional)       |

> **Note:** Building Sumokoin requires at least **3.5 GB** of available memory (physical + virtual).

### Installing dependencies on Ubuntu/Debian

```bash
sudo apt update && sudo apt install -y \
  build-essential cmake git pkg-config \
  libboost-all-dev libssl-dev libzmq3-dev \
  libunbound-dev libsodium-dev libhidapi-dev \
  libreadline-dev libpgm-dev
```

### Installing dependencies on macOS

```bash
brew install cmake boost openssl zmq libsodium hidapi readline
```

## Building from Source

### Linux (Ubuntu/Debian)

```bash
git clone --recursive https://github.com/marcellinuswiray/marcellinuswiray.git
cd marcellinuswiray
make release -j$(nproc)
```

The resulting binaries will be in `build/<platform>/release/bin/`.

### macOS

```bash
git clone --recursive https://github.com/marcellinuswiray/marcellinuswiray.git
cd marcellinuswiray
make release-static-mac-x86_64
```

### Windows (MSYS2/MinGW)

**64-bit:**
```bash
make release-static-win64
```

**32-bit:**
```bash
make release-static-win32
```

### Android

**ARMv7:**
```bash
make release-static-android-armv7
```

**ARMv8 (arm64):**
```bash
make release-static-android-armv8
```

> Set the `ANDROID_STANDALONE_TOOLCHAIN_PATH` environment variable to your Android NDK standalone toolchain path (default: `/usr/local/toolchain`).

### iOS

Build with CMake using the iOS toolchain:

```bash
mkdir -p build/ios && cd build/ios
cmake -D IOS=ON -D ARCH=arm64 -D IOS_PLATFORM=OS ../..
make
```

Supported `IOS_PLATFORM` values: `OS` (device), `SIMULATOR`, `SIMULATOR64`.

### Cross-compilation (using depends)

```bash
make depends target=<host-triplet>
```

For backwards-compatible builds:
```bash
make depends-backcompat target=<host-triplet>
```

## Build Targets

| Target                            | Description                          |
|-----------------------------------|--------------------------------------|
| `make release`                    | Release build                        |
| `make debug`                      | Debug build                          |
| `make release-static`             | Static release build (x86-64)        |
| `make release-static-linux-x86_64`| Static build for Linux x86-64       |
| `make release-static-linux-armv6` | Static build for Linux ARMv6         |
| `make release-static-linux-armv7` | Static build for Linux ARMv7         |
| `make release-static-linux-armv8` | Static build for Linux ARMv8         |
| `make release-static-win64`       | Static build for Windows 64-bit      |
| `make release-static-win32`       | Static build for Windows 32-bit      |
| `make release-static-mac-x86_64`  | Static build for macOS x86-64        |
| `make release-static-freebsd-x86_64` | Static build for FreeBSD x86-64  |
| `make release-test`               | Release build + run tests            |
| `make debug-test`                 | Debug build + run tests              |
| `make coverage`                   | Debug build with code coverage       |
| `make fuzz`                       | Fuzz testing build (AFL)             |
| `make clean`                      | Clean build directory                |

## License

```
Copyright (c) 2017-2021, Sumokoin Projects
Copyright (c) 2014-2021, The Monero Project
Parts originally copyright (c) 2012-2013 The Cryptonote developers
Parts originally copyright (c) 2014 The Boolberry developers (MIT License)
```

Licensed under the **BSD 3-Clause License**. See [LICENSE](LICENSE) for details.
