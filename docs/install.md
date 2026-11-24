# Install Morphon

## Downloads

Open [Morphon Releases](https://github.com/NaiTangBaoBao/morphon/releases) and choose the package for your computer:

| Platform | Package |
| --- | --- |
| macOS with Apple Silicon | `morphon_0.1.0-alpha.1_darwin_arm64.tar.gz` |
| Linux x86-64 | `morphon_0.1.0-alpha.1_linux_amd64.tar.gz` |

Download `SHA256SUMS` from the same release and save it alongside the package.

## macOS and Linux

Run this block from the directory containing both downloaded files. Set `archive` to the package for your platform before running it. The checksum must print `OK`; the command stops before extraction or launch if verification fails. It extracts into a new temporary directory so an existing `morphon` file is left untouched.

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
  esac || exit 1
  install_dir=$(mktemp -d "${TMPDIR:-/tmp}/morphon-alpha1.XXXXXX") || exit 1
  tar -xzf "$archive" -C "$install_dir" &&
    "$install_dir/morphon" version &&
    printf 'Extracted to: %s\n' "$install_dir"
)
```

For Alpha 1, the checksum check prints `OK` next to the package filename and the version command prints `0.1.0-alpha.1`. Run the executable from the printed directory, or move it to a permanent location after confirming the version output. The operating system may clear temporary files.

### Troubleshooting

- **Checksum command reports `FAILED` or cannot find the file:** confirm that the archive and `SHA256SUMS` came from the same release, that both downloads completed, and that `archive` exactly matches the filename in the table. Download them again if needed; do not extract or run an archive whose checksum does not match.
- **`Permission denied` on Linux:** check that the extracted `morphon` file is executable and is on a filesystem that permits execution. To restore its executable bit, use `chmod +x /path/to/extracted/morphon`.
- **macOS blocks startup:** confirm the expected archive and checksum, then follow [Apple’s guidance for the specific alert](https://support.apple.com/en-us/102445).
- **`Exec format error` or `bad CPU type`:** the package does not match the computer's operating system or processor. Alpha 1 provides only Apple Silicon macOS and x86-64 Linux packages; check the selected filename.
- **`morphon: command not found` after moving it:** run it as `./morphon` in its directory or ensure its destination directory is on `PATH`.

## Early preview

Version 0.1.0 Alpha 1 is intended for evaluation. It is not yet a stable production release. Product features and configuration may change while the workspace is being refined.

Provider credentials are supplied by the user and are never included in release packages.
