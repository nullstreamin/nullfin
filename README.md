<div align="center">
  <img width="180" height="180" src="logo.png" alt="Nullfin logo">
  <h1>Nullfin</h1>
  <p>A community-maintained media server with a Jellyfin-compatible API.</p>
</div>

Nullfin brings Stremio add-ons, local files, WebDAV sources, IPTV, and music into one library. It works with Jellyfin clients such as Strand, Infuse, Swiftfin, and Jellyfin for Android, so the apps you already use do not need to change.

This fork stays close to the original Remux project. Community changes are kept small on purpose: setup should be easier, releases should be predictable, and bringing in new Remux work should not turn into a rewrite.

It also carries tested compatibility fixes for [Strand](docs/strand.md), including complete source lists, fast source-picker responses, and file sizes supplied by Stremio-style add-ons such as StreamNZB and AIOStreams.

## What it does

- Uses Stremio add-ons, local files, WebDAV, IPTV, and torrents as media sources.
- Serves the library through a Jellyfin-compatible API.
- Keeps playback progress and continue-watching data in sync.
- Supports multiple users, library filters, and per-user access.
- Provides a built-in admin dashboard for setup and maintenance.
- Reads stream details from RemuxDB so clients can show audio and subtitle tracks.

## Run it with Docker

```yaml
services:
  nullfin:
    image: ghcr.io/nullstreamin/nullfin:latest
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - ./data:/data
```

Open `http://localhost:3000`, create the admin account, and add your media sources from the Addons page.

If you use Strand, follow the short [Strand setup guide](docs/strand.md). No special image or patch is required; the compatibility work is included in this build.

The `latest` tag is the current stable community build. Back up the data directory before changing versions.

## Build it locally

You will need Rust, [cargo-make](https://github.com/sagiegurari/cargo-make), and the [Dioxus CLI](https://dioxuslabs.com/learn/0.6/getting_started/).

```sh
cargo install --force cargo-make
cargo install dioxus-cli
cp .env.example .env
cargo make jellyfin-web
cargo make dev
```

## Keeping the fork current

We bring in changes from the original Remux repository in reviewed batches. Each update is built and tested before a community image is published. The short maintainer checklist is in [docs/updates.md](docs/updates.md).

## Contributing

Bug reports and focused pull requests are welcome. Please explain what changed, why it helps, and how you tested it. Small changes are easier to review and easier to carry forward.

## Credits and license

Nullfin is based on [Remux by lostb1t](https://github.com/lostb1t/remux) and continues under the [GNU Affero General Public License v3.0](LICENSE). Existing copyright and license notices remain with their respective authors.
