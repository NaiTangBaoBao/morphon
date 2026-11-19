# Install Morphon

## Downloads

Open [Morphon Releases](https://github.com/NaiTangBaoBao/morphon/releases) and choose the package for your computer:

| Platform | Package |
| --- | --- |
| macOS with Apple Silicon | `darwin_arm64` |
| Linux x86-64 | `linux_amd64` |
| Windows x86-64 | `windows_amd64` |

Every release includes SHA-256 checksums. Compare the downloaded package with `SHA256SUMS` before installing it.

## macOS and Linux

Extract the downloaded archive, then run Morphon from the extracted directory:

```sh
./morphon version
```

You can move the `morphon` executable to a directory on your `PATH`.

## Windows

Extract the ZIP archive and run `morphon.exe version` from a terminal.

## Early preview

Version 0.1.0 Alpha 1 is intended for evaluation. It is not yet a stable production release. Product features and configuration may change while the workspace is being refined.

Provider credentials are supplied by the user and are never included in release packages.
