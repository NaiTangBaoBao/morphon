# Install Morphon

## Downloads

Open [Morphon Releases](https://github.com/NaiTangBaoBao/morphon/releases) and choose the package for your computer:

| Platform | Package |
| --- | --- |
| macOS with Apple Silicon | `morphon_0.1.0-alpha.1_darwin_arm64.tar.gz` |
| Linux x86-64 | `morphon_0.1.0-alpha.1_linux_amd64.tar.gz` |

Download `SHA256SUMS` from the same release and save it alongside the package.

## macOS and Linux

Run this block from the download directory. On macOS, set `archive` to the macOS filename in the table.

```sh
archive=morphon_0.1.0-alpha.1_linux_amd64.tar.gz
(
  entry=$(awk -v file="$archive" '$2 == file { print; count++ } END { if (count != 1) exit 1 }' SHA256SUMS) || {
    printf '%s\n' "Expected exactly one checksum for $archive in SHA256SUMS" >&2
    exit 1
  }
  case "$(uname -s)" in
    Linux) printf '%s\n' "$entry" | sha256sum -c - ;;
    Darwin) printf '%s\n' "$entry" | shasum -a 256 -c - ;;
    *) exit 1 ;;
  esac &&
    tar -xzf "$archive" &&
    ./morphon version
)
```

For Alpha 1, the checksum check prints `OK` next to the package filename and `morphon version` prints `0.1.0-alpha.1`.

You can move the `morphon` executable to a directory on your `PATH`.

## Early preview

Version 0.1.0 Alpha 1 is intended for evaluation. It is not yet a stable production release. Product features and configuration may change while the workspace is being refined.

Provider credentials are supplied by the user and are never included in release packages.
