# PxScanner Office Engine

Builds the [LibreOffice](https://www.libreoffice.org) core for Android and iOS so PxScanner can open and convert Office documents on device.

## Building

Run the **Build engine** workflow from the Actions tab and pick a LibreOffice core tag. It builds `arm64-v8a`, `armeabi-v7a` and `x86_64` with NDK 28.2.13676358, applies the fixes in `patches/`, checks that the 64-bit libraries are 16 KB page aligned, and publishes a release named `engine-<tag>-r<run>`.

Run the **Build iOS engine** workflow for iOS. It builds the `LibreOfficeiOS` distro for arm64 devices with Xcode 27.1, raising LibreOffice's iOS deployment target from 14.5 to 18.0 because Xcode 27's libc++ no longer supports iOS versions before 15, enabling the bundled OpenSSL because curl no longer has another TLS backend on Apple platforms, and building that OpenSSL with its `ios64-xcrun` target because LibreOffice names one that OpenSSL 3.5 doesn't have, and publishes a release named `engine-ios-<tag>-r<run>`. LibreOffice only supports x86_64 for the iOS simulator, so there is no simulator build.

## Release contents

- `pxscanner-office-engine-<abi>.tar.gz` — `jniLibs/<abi>` (`liblo-native-code.so` and its runtime libraries), `assets`, `assets_strippedUI`, `licenses` and `BUILD_INFO`
- `pxscanner-office-bindings.tar.gz` — the matching `org.libreoffice.kit` Java bindings
- `SHA256SUMS`

iOS releases contain `pxscanner-office-engine-ios-arm64.tar.gz` with `lib` (every static archive from `ios-all-static-libs.list`, at its path in the build tree), `static-libs.list`, `include` (`native-code.h` and the LibreOfficeKit headers), `resources`, `licenses` and `BUILD_INFO`, plus `SHA256SUMS`.

## License

The binaries are built from LibreOffice sources (unmodified, apart from the Android fixes in `patches/` and the iOS deployment target and OpenSSL target described above), which are available under the [Mozilla Public License 2.0](https://www.mozilla.org/MPL/2.0/) at https://github.com/LibreOffice/core. Bundled third-party components keep their own licenses, included in each archive under `licenses/`.
