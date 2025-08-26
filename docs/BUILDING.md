# Building Spotube

This document provides instructions for building Spotube from source. We strongly recommend using FVM (Flutter Version Manager) for a consistent development environment.

## Prerequisites

### Install FVM (Flutter Version Manager)

FVM helps manage Flutter SDK versions and ensures everyone uses the same Flutter version for development.

```bash
# On macOS/Linux using Homebrew
$ brew tap leoafarias/fvm
$ brew install fvm

# On Windows using Chocolatey
$ choco install fvm

# Using pub (Dart package manager)
$ dart pub global activate fvm
```

### Install Flutter SDK using FVM

Spotube uses a specific Flutter version as defined in the `.fvmrc` file. FVM will automatically use this version.

```bash
# Install the Flutter version specified in .fvmrc
$ fvm install

# Verify installation
$ fvm flutter --version
```

### Platform-specific Dependencies

#### Linux

- Debian (>=12/Bookworm)/Ubuntu
  ```bash
  $ apt-get install mpv libmpv-dev libappindicator3-1 gir1.2-appindicator3-0.1 libappindicator3-dev libsecret-1-0 libjsoncpp25 libsecret-1-dev libjsoncpp-dev libnotify-bin libnotify-dev avahi-daemon avahi-discover avahi-utils libnss-mdns mdns-scan libwebkit2gtk-4.1-0 libwebkit2gtk-4.1-dev libsoup-3.0-0 libsoup-3.0-dev
  ```
  - Use `libjsoncpp1` instead of `libjsoncpp25` (for Ubuntu < 22.04)

- Arch/Manjaro
  ```bash
  $ yay -S mpv libappindicator-gtk3 libsecret jsoncpp libnotify avahi nss-mdns mdns-scan webkit2gtk-4.1 libsoup3
  ```

- Fedora
  ```bash
  $ dnf install mpv mpv-devel libappindicator-gtk3 libappindicator-gtk3-devel libsecret libsecret-devel jsoncpp jsoncpp-devel libnotify libnotify-devel avahi mdns-scan nss-mdns webkit2gtk4.1 webkit2gtk4.1-devel libsoup3 libsoup3-devel
  ```

## Building Spotube

### Setup

1. Clone the repository
   ```bash
   $ git clone https://github.com/KRTirtho/spotube.git
   $ cd spotube
   ```

2. Create a `.env` file in the root of the project following the `.env.example` template

3. Bootstrap the project
   ```bash
   $ fvm flutter pub get
   $ fvm dart run build_runner build --delete-conflicting-outputs --enable-experiment=records,patterns
   ```

### Running in Development Mode

```bash
$ fvm flutter run -d <window|macos|linux|android-device-id>
```

### Building for Production

#### Android

```bash
$ fvm flutter build apk --release
```

#### Linux

```bash
$ fvm flutter build linux --release
```

#### Windows

```bash
$ fvm flutter build windows --release
```

#### macOS

```bash
$ fvm flutter build macos --release
```

## Troubleshooting

If you encounter issues with Flutter or Dart commands, make sure you're using the FVM-managed version:

```bash
# Instead of
$ flutter pub get

# Use
$ fvm flutter pub get
```

For any other build issues, please check the [GitHub issues](https://github.com/KRTirtho/spotube/issues) or create a new one.

## Branch and Commit Message for FVM Update

When submitting a PR for this FVM update, use:

- Branch name: `feature/add-fvm-support`
- Commit message: "Add FVM support for consistent Flutter version management"