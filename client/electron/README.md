# Electron Development Instructions

Unlike the Android and Apple clients, the Windows and Linux clients use the Electron framework, rather than Cordova.

To build the Electron clients, run (it will also package an installer executable into `output/client/electron/build`):

```sh
npm run action client/electron/build [windows|linux]
```

To run the Electron clients, run:

```sh
npm run action client/electron/start [windows|linux]
```

## Cross-Compiling

To build the app for a platform target on a different host target, you will need a cross-compiler. We use [zig to cross-compile with cgo](https://dev.to/kristoff/zig-makes-go-cross-compilation-just-work-29ho).

[Install zig](https://ziglang.org/learn/getting-started/#installing-zig) and make sure it's in the PATH.

You can download the binary tarball, or [use a package manager](https://github.com/ziglang/zig/wiki/Install-Zig-from-a-Package-Manager), like Homebrew:

```sh
brew install zig 
```

## Requirements

### Windows

- Visual Studio 2022 or later

If you see an error about `node-gyp` not finding Visual Studio, try one of the following:

- (Recommended) Install the VSSetup PowerShell package using `Install-Module VSSetup -Scope CurrentUser`
- Change PowerShell LanguageMode using `$ExecutionContext.SessionState.LanguageMode="FullLanguage"`

### Linux

- `patchelf` 0.14+ is required for building the Debian package:
  - Debian/Ubuntu: `sudo apt install patchelf`
  - macOS: `brew install patchelf`
  - Windows: https://github.com/NixOS/patchelf/releases

## Release

To build the _release_ version of Windows installer, you'll also need:

- [Java 8+ Runtime](https://www.java.com/en/download/). This is required for the cross-platform Windows executable signing tool [Jsign](https://ebourg.github.io/jsign/). If you don't need to sign the executables, feel free to skip this.
