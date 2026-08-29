<div align="center">
  <img width="180" height="180" src="logo.png" alt="Nullfin logo">
  <h1>Nullfin</h1>
  <p>A small community build made to play nicely with Strand.</p>
</div>

Nullfin takes your Stremio add-ons and puts their streams behind a Jellyfin-compatible server. Add it to Strand, connect the add-ons you already use, and that is pretty much the idea.

This build exists because the normal setup had a few annoying rough edges in Strand. We fixed the ones we kept running into and bundled them here so nobody else has to repeat the same tinkering.

## What is different

- Strand gets the complete source list instead of one `Remote - Unknown` entry.
- The source picker opens without waiting for every remote file to be probed first.
- File sizes can come straight from the add-on when they are available.
- Add-on scores show up in Strand's source list.
- Selecting a source still uses the normal playback checks, so the faster list does not skip the important part.
- The fixes work with standard Stremio streaming add-ons, not just one specific service.

Other Jellyfin clients keep their normal behavior. The Strand-specific shortcuts only turn on when the request identifies itself as Strand.

## Run it

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

Open `http://localhost:3000`, make the admin account, and add your Stremio manifest URLs from the Addons page. Then add Nullfin to Strand as a Jellyfin server.

That is enough for most setups. There is a slightly longer [Strand guide](docs/strand.md) if you want it.

## A couple of sensible notes

Keep the data folder persistent and back it up before updating. Pin `ghcr.io/nullstreamin/nullfin:v0.30.0` instead of `latest` if you would rather update manually.

Manifest URLs can contain API keys or personal tokens, so do not paste configured URLs into screenshots, bug reports, or public Compose files.

## Updates

The plan is to keep Nullfin close to the project it came from and bring over useful changes without turning maintenance into a second job. New builds will be tested before the `latest` tag moves.

## Credits and license

Nullfin is a community fork of [Remux by lostb1t](https://github.com/lostb1t/remux). It remains licensed under the [GNU Affero General Public License v3.0](LICENSE), and the original copyright and license notices are preserved.
