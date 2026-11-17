# Distribution maintainer checklist

Publish only these official release assets:

- `rhtop-vVERSION-darwin-universal2.tar.gz`, containing both Mac architectures.
- Two `rhtop-vVERSION-linux-{amd64,arm64}.tar.gz` archives.
- Two `rhtop_VERSION_{amd64,arm64}.deb` packages.
- `rhtop-vVERSION-windows-amd64.zip` when releasing Windows.
- `SHA256SUMS` covering all release assets (six when Windows is included).

Each binary archive includes `LICENSE.txt`, `NOTICE`, and `THIRD_PARTY_NOTICES`.

Verify that each executable matches its advertised platform and architecture,
including both Intel and Apple Silicon in the macOS universal2 archive.
Test version/help, the interactive demo, and OAuth/keyring behavior on each.
Review third-party license obligations and verify the bundled LICENSE.txt matches
the published terms at https://rhtop.dev/terms/.
Complete macOS signing,
notarization, and Gatekeeper verification before publishing macOS assets.

Inspect a draft release before publishing. Then generate the Homebrew formula
from those exact archives and publish signed APT metadata from those Debian
packages. Verify real Homebrew and APT installs before announcing availability.

Enable private vulnerability reporting here. Enable GitHub Pages on `apt-repo`
using the default branch's `/docs` directory. The documentation repository and tap need no Pages.
