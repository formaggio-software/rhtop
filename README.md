# rhtop

A read-only Robinhood MCP terminal dashboard for macOS, Linux, and Windows. View accounts,
positions, orders, assets, and watchlists. rhtop never submits, previews, or
cancels orders or changes watchlists.

```text
┌─ Overview ────┐ ┌─ Positions ─────────────────┐ ┌─ Assets & Watchlists─┐
│               │ │ Symbol  Asset   Qty  Value  │ │ Crypto ▾             │
│ Account   *** │ │ AAPL    equity  ***  ***    │ │ Search / filter      │
│ Portfolio *** │ │ BTC     crypto  ***  ***    │ │ BTC-USD · Bitcoin    │
│ Cash      *** │ └─────────────────────────────┘ │ ETH-USD · Ethereum   │
│ Buying power  │ ┌─ Orders ────────────────────┐ │ DEMO-USD … 🚫 ALL    │
│           *** │ │ Symbol  Side  State   Qty   │ │                      │
│               │ │ AAPL    buy   queued  ***   │ │ Recent selections    │
└───────────────┘ └─────────────────────────────┘ └──────────────────────┘
q Quit   m Mask   r Refresh   p Pause   a Account   / Filter   l Layout   ? Help
```

This repository contains documentation and binary downloads for rhtop,
proprietary, paid software owned by Formaggio LLC.
Product, subscription, and account information: [rhtop.dev](https://rhtop.dev).
See the website for subscription and licensing information. Keep the proprietary
and third-party notices supplied with your download.

## Installation

Find versioned downloads, checksums, and platform support in
[Releases](https://github.com/formaggio-software/rhtop/releases).

```sh
pipx install rhtop
```

```sh
choco install rhtop
```

```sh
npm install -g @formaggio-software/rhtop
```

For Debian/Ubuntu, follow [signed APT setup](https://github.com/formaggio-software/apt-repo#install).
PyPI, npm, and Chocolatey install commands are documented in
[INSTALLERS.md](INSTALLERS.md). Windows assets use a native Windows build.
Linux release builds target Debian 12 Bookworm or newer (glibc 2.36+); Alpine/musl
is unsupported. Windows amd64 builds target a modern Windows console;
supported minimum Windows and macOS versions are recorded per release.
Python is bundled; no Python installation is needed.

For manual installation, choose the matching asset from Releases:

| System | Archive name (example version) |
| --- | --- |
| macOS Intel and Apple Silicon | `rhtop-v0.1.0-darwin-universal2.tar.gz` |
| Linux x86-64 | `rhtop-v0.1.0-linux-amd64.tar.gz` |
| Linux ARM64 | `rhtop-v0.1.0-linux-arm64.tar.gz` |
| Windows x86-64 | `rhtop-v0.1.0-windows-amd64.zip` |

Download `SHA256SUMS` from the same release and verify the downloaded archive
reports `OK` using `sha256sum --ignore-missing --check SHA256SUMS` on Linux or
`shasum -a 256 --check SHA256SUMS` on macOS (which may also report missing assets).
Then extract into a new directory and install, substituting your asset name:

```sh
mkdir rhtop-download
tar -xzf rhtop-v0.1.0-linux-amd64.tar.gz -C rhtop-download
mkdir -p "$HOME/.local/bin"
install -m 0755 rhtop-download/rhtop "$HOME/.local/bin/rhtop"
# Ensure $HOME/.local/bin is on PATH. Retain LICENSE.txt, NOTICE, and THIRD_PARTY_NOTICES.
rhtop --version
rhtop --demo
```

Linux releases also include `rhtop_0.1.0_amd64.deb` and
`rhtop_0.1.0_arm64.deb`; install the matching file with
`sudo apt install ./rhtop_0.1.0_amd64.deb`.

On Windows, verify the ZIP checksum in PowerShell with `Get-FileHash -Algorithm
SHA256 .\rhtop-v0.1.0-windows-amd64.zip`, compare it with `SHA256SUMS`, and extract
using `Expand-Archive`. Run `rhtop.exe --demo` from the extracted directory, or
use Chocolatey. Keep the notices with the binary.

## Use

```sh
rhtop --demo   # offline sample data, no account connection
rhtop login    # authorize your own Robinhood MCP connection
rhtop          # live dashboard
rhtop --help
```

Open the displayed authorization URL manually on the same machine. rhtop never
launches a browser. The callback listens on `127.0.0.1:8766`; use
`--oauth-port PORT` consistently to change it. Credentials are encrypted locally
with a secure native keyring, or a passphrase of at least 12 characters on
headless Linux. rhtop never accepts a broker password.

| Key | Action |
| --- | --- |
| `q` / `Ctrl+c` | Quit |
| `m` | Mask/reveal private values (masking starts on) |
| `a` | Select account |
| `r` / `p` | Refresh / pause |
| `/` | Filter |
| `l` | Change layout |
| `?` | Help |

Masking is a display control; public market data stays visible. `rhtop paths`
shows local storage locations. `rhtop auth-reset` removes local authorization
for the chosen callback port.

Report installation issues with version, OS, architecture, and sanitized error
text. Never attach tokens, authorization URLs, vault files, or unmasked account
screenshots. See [SECURITY.md](SECURITY.md) for private reporting.
For private support, purchase questions, or security reports, email
[contact@formaggio.software](mailto:contact@formaggio.software).
rhtop is independent of and not endorsed by Robinhood.

Binary use requires an active subscription under [LICENSE.txt](LICENSE.txt).
Read the same agreement at https://rhtop.dev/terms/ before subscribing.

## Binary-use license

Read [LICENSE.txt](LICENSE.txt) or the [published terms](https://rhtop.dev/terms/)
before subscribing or using rhtop. A paid subscription licenses one subscriber
on their devices for the paid period, including the remainder after cancellation.
Public downloads do not grant unpaid use or redistribution rights.
