# PxScanner Office Engine

Builds the [LibreOffice](https://www.libreoffice.org) core for Android so PxScanner can open and convert Office documents on device.

## Building

Run the **Build engine** workflow from the Actions tab and pick a LibreOffice core tag. It builds `arm64-v8a`, `armeabi-v7a` and `x86_64` with NDK 27.1.12297006 and publishes a release named `engine-<tag>`.

## Release contents

- `pxscanner-office-engine-<abi>.tar.gz` — `jniLibs/<abi>` (`liblo-native-code.so` and its runtime libraries), `assets`, `assets_strippedUI`, `licenses` and `BUILD_INFO`
- `pxscanner-office-bindings.tar.gz` — the matching `org.libreoffice.kit` Java bindings
- `SHA256SUMS`

## License

The binaries are built from unmodified LibreOffice sources, which are available under the [Mozilla Public License 2.0](https://www.mozilla.org/MPL/2.0/) at https://github.com/LibreOffice/core. Bundled third-party components keep their own licenses, included in each archive under `licenses/`.
