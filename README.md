# rhtop

A minimal, **read-only** Robinhood MCP terminal dashboard for macOS, Linux, and
Windows, inspired by [btop](https://github.com/aristocratos/btop),
[htop](https://htop.dev/), and [lazygit](https://github.com/jesseduffield/lazygit).
View accounts, positions, orders, assets, and watchlists. rhtop never submits,
previews, or cancels orders. Watchlists are read-only.

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
Keep the proprietary and third-party notices supplied with your download. See
[rhtop.dev](https://rhtop.dev) for product, subscription, and account information.

## Installation

Find versioned downloads, checksums, and platform support in
[Releases](https://github.com/formaggio-software/rhtop/releases).

```sh
pipx install rhtop
```

```sh
sudo apt install rhtop
```

```sh
brew install formaggio-software/tap/rhtop
```

```sh
choco install rhtop
```

```sh
npm install -g @formaggio-software/rhtop
```

More info: [INSTALLERS.md](INSTALLERS.md)

For Debian/Ubuntu, follow [signed APT setup](https://github.com/formaggio-software/apt-repo#install).
PyPI, npm, and Chocolatey install commands are documented in
[INSTALLERS.md](INSTALLERS.md). Windows assets use a native Windows build.
Linux release builds target Debian 12 Bookworm or newer (glibc 2.36+); Alpine/musl
is unsupported. Windows amd64 builds target a modern Windows console;
supported minimum Windows and macOS versions are recorded per release.
Python is bundled; no Python installation is needed.

For manual installation, choose the matching asset from Releases.

| System | Archive name (example version) |
| --- | --- |
| macOS Intel and Apple Silicon | `rhtop-v0.1.0-darwin-universal2.tar.gz` |
| Linux x86-64 | `rhtop-v0.1.0-linux-amd64.tar.gz` |
| Linux ARM64 | `rhtop-v0.1.0-linux-arm64.tar.gz` |
| Windows x86-64 | `rhtop-v0.1.0-windows-amd64.zip` |

Download `SHA256SUMS` from the same release and verify the downloaded archive
reports `OK` using `sha256sum --ignore-missing --check SHA256SUMS` on Linux or
`shasum -a 256 --check SHA256SUMS` on macOS (which may also report missing assets).
Then extract into a new directory and install. Substitute your asset name in the command below.

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

## Connect your own MCP account

```sh
rhtop --demo   # try sample data offline
rhtop login    # optional: authorize before launching the dashboard
rhtop          # connect and show live account data
rhtop --help
```

Authorize your own Robinhood MCP connection. The sole active **MCP / Agentic**
account is selected automatically. Use `a` to explicitly choose among the active
accounts the connection can read. If the MCP default is ambiguous or missing,
rhtop asks you to choose an account. rhtop encrypts your selection and restores
it on restart.

**OAuth uses a loopback callback.** Open the displayed authorization URL
manually on the same machine, authorize, and return to the terminal. By default
the callback listens on `127.0.0.1:8766`. Use `--oauth-port PORT` consistently
if you need a different port. rhtop leaves browser launch to you.

In the authorization dialog, click **Copy URL** or press **Ctrl+y** to copy the
entire URL. If your terminal cannot paste it, click **Show in terminal** or press
**Ctrl+t** to temporarily leave
the dashboard and copy the plain URL with your terminal's normal controls.
Press Enter to return. The OAuth callback continues listening while you copy.
Alternatively, run `rhtop login` to authorize from ordinary terminal output.

On a desktop with a secure native keyring, the vault encryption key lives there.
On headless Linux without a usable keyring, enter a vault passphrase of at least
12 characters before the UI starts. For unattended startup, supply
`RHTOP_PASSPHRASE` through your secret manager. rhtop does not load `.env` files or
accept broker passwords or access tokens as command-line arguments.

## Dashboard controls

| Key | Action |
| --- | --- |
| `Tab` / `Shift+Tab` | Move focus between panels and controls |
| Arrows / `j`, `k` | Navigate table rows (arrows also work in asset lists) |
| `Enter` | Inspect a row or select an asset |
| `m` / `Ctrl+h` | Toggle `***` for personal financial values and identifiers |
| `/` / `Esc` | Filter account tables / clear filter or close a dialog |
| `s` / `S` | Cycle sort column / reverse sort direction |
| Click table header | Sort that column |
| `a` | Select an active account (MCP / Agentic is the initial default) |
| `r` | Refresh / retry a failed connection |
| `p` | Pause / resume automatic account polling and crypto catalog refresh |
| `1`, `2`, `3`, `4`, `5` | Toggle Overview, Positions, Orders, Assets, Watchlists panels |
| `l` | Cycle classic, mirrored, and stacked layouts |
| `?` | Show keyboard help |
| `q` / `Ctrl+c` / `Ctrl+q` | Quit (`Ctrl+c` and `Ctrl+q` also work inside inputs and dialogs) |

Text inputs consume normal character keys while you type. Use Tab to leave an
input before using the single-character dashboard shortcuts. `Ctrl+h` toggles
privacy while an input has focus. At least one panel stays visible.
Click the `ACCOUNT` label in Overview to open the same account selector as `a`.
Click the green Account ID value to copy the full ID to the clipboard, including
when it is displayed as `***`.

Privacy starts **on at every launch**. Revealing values is session-only. Masking
covers balances, account numbers, quantities, cost basis, position value/P&L,
order prices and IDs, and IDs in asset detail dialogs. Public market symbols,
option contract descriptions (including strikes), names, sides, order states,
timestamps, row counts, and saved asset titles remain visible.

The classic layout puts the Overview column on the left, positions/orders in the
middle, and assets on the right. Press `l` once for the mirrored layout, with
Overview above Assets on the right and Positions above Orders on the left.
Press `l` again for the stacked layout, and again to return to classic.
Narrow terminals adapt the layout and allow scrolling. A terminal of at least
140×32 is recommended for the full five-panel view. Watchlists appears to the
right of Assets on wide terminals and below the other panels on narrow ones.
Press `5` to toggle it. Choose a watchlist to read its symbols and asset types.
`r` refreshes it along with the dashboard. Custom and followed curated lists are
supported. Options lists show single-leg contracts through the dedicated MCP
options watchlist reader. Watchlists cannot be edited in rhtop.

Hover over the connection status in the header for the last successful update
time and full notices.
A live clock with the machine's local timezone sits at the far right and continues
ticking while account polling is paused or disconnected.
On supported Unix terminals, rhtop uses the standard arrow pointer and restores
the previous pointer when you exit or show the authorization URL in the terminal.

## Asset browser

The right-hand picker **defaults to Crypto on every launch**. To change the
category with the keyboard, focus the dropdown, press Enter, choose with the
arrow keys, then press Enter again. Select an asset row to see its full details.

* **Crypto** shows supported pairs from all catalog pages. Halted pairs are
  retained and their titles end in
  `🚫` followed by space-separated regions, such as `🚫 NY TX` (`🚫 ALL` for a
  global halt, or just `🚫` when regions are unavailable). A regional halt can be one-sided.
  Enter a name or symbol in the search field to filter the catalog. The catalog
  refreshes alongside automatic polling and on `r`.
* For **equities**, enter a company name or ticker and press Enter. Select a result
  to inspect it and save it to recent selections.
* For **options**, search for a company or ticker, select an underlying, then
  select a contract to inspect and save it. To narrow a large chain, search
  directly using `AAPL 2026-12-18 call 250` (expiry, right, and strike are optional).
  rhtop displays up to 500 contracts per lookup and tells you when results are
  truncated.

The most recent **30 equities and 30 option contracts** are deduplicated and
restored on restart. Search again to refresh a saved contract's status. Live
recents are encrypted in the same vault as the saved account selection. Offline
demo recents use a private `demo-recents.json` file.

## Settings and data

`rhtop paths` prints the local paths. On Linux the defaults are
`~/.config/rhtop/settings.json` and `~/.local/share/rhtop/` for the vault.
The standard XDG directory variables are respected.

Non-secret settings (layout, panels, poll interval, sort direction) are saved
atomically. On Unix, settings use mode `0600` and new app directories use
`0700`. Polling defaults to 30 seconds, configurable with
`rhtop --poll-seconds 60` (10–3600).
The local vault encrypts credentials, your selected account, and recent assets
from live sessions.
No account snapshots, response bodies, or portfolio history are written to disk.

`rhtop auth-reset` removes the local vault for the selected callback port,
including its saved account and asset recents. It does not revoke Robinhood-side
authorization. Use Robinhood's connection controls for revocation.

Unknown values show `—`. Values and P&L are displayed only when supplied by the
broker. The status bar reports failures in optional sections. Paginated account positions
or orders are marked **partial (first page)**. A failed core refresh keeps the
last successful snapshot with a **STALE** notice. Retries back off to 60 seconds.
Crypto catalogs are never silently presented as complete after truncation or a
pagination failure.

## Support

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
