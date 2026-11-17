# Install rhtop

Use your preferred package manager or download a standalone binary from
[Releases](https://github.com/formaggio-software/rhtop/releases).
Check the release notes for available packages and supported operating-system
versions. Subscriptions and account management are at [rhtop.dev](https://rhtop.dev).

| Channel | Install command | Platform notes |
| --- | --- | --- |
| Homebrew | `brew install formaggio-software/tap/rhtop` | macOS Intel/Apple Silicon; Linux amd64/arm64 |
| APT | `sudo apt install rhtop` | Debian 12+ / compatible Ubuntu; amd64/arm64; [configure the signed repository first](https://github.com/formaggio-software/apt-repo#install) |
| PyPI | `pipx install rhtop` | Platform wheels bundle the native executable |
| npm | `npm install -g @formaggio-software/rhtop` | Node 18+; enable optional dependencies |
| Chocolatey | `choco install rhtop` | Windows amd64 |

Package-manager downloads contain the native executable, launcher where needed,
and proprietary/third-party notices.
Keep those notices with the binary. See [NOTICE](NOTICE) for licensing information.

## Platform requirements

Intel and Apple Silicon Macs use the same universal2 binary and run natively
without Rosetta. Consult the release notes for the minimum supported macOS version.

Linux binaries require glibc 2.36+ (Debian 12 Bookworm or newer). Alpine/musl is
unsupported. Choose the matching amd64 or arm64 download.

Windows packages contain the native amd64 executable. Consult the release notes
for tested Windows versions and console requirements.

The standalone binary bundles Python. PyPI installation uses pipx or a Python
virtual environment to isolate its launcher. Only the listed platforms are supported. npm selects a platform-specific
optional package and does not download an executable through an install script.

## Start the dashboard

```sh
rhtop --version
rhtop --demo
rhtop login
rhtop
```

The offline demo uses sample data without connecting an account. `rhtop login`
authorizes your Robinhood MCP connection on your machine; this is separate from
your website subscription account. See [README.md](README.md) for authentication,
keyboard controls, and manual archive installation.

## Support

Email [contact@formaggio.software](mailto:contact@formaggio.software) with your
app version, operating system, architecture, and sanitized error text. Never
include credentials, authorization URLs, or unmasked account screenshots.
See [SECURITY.md](SECURITY.md) for private vulnerability reporting.

## License location

Read [LICENSE.txt](LICENSE.txt) before use. Manual archives keep it beside the
binary; Homebrew installs it under the formula prefix, APT under
`/usr/share/doc/rhtop/LICENSE.txt`, and wheels/npm retain it in the package.
The same agreement is published at https://rhtop.dev/terms/.
