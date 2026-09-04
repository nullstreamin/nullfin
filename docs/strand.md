# Using Nullfin with Strand

Nullfin includes the compatibility behavior Strand needs when it asks for playable sources.

## Quick setup

1. Run Nullfin with persistent storage and finish the first-run admin setup.
2. In Nullfin, add the Stremio manifest URLs you already use. Keep provider credentials inside those services or their private manifest URLs; do not place them in Compose files you intend to share.
3. In Strand, add Nullfin as a Jellyfin-compatible media server using your Nullfin URL and account.
4. Open a movie or episode and check the source picker before removing any older Strand configuration.

StreamNZB, AIOStreams, and other Stremio-compatible add-ons remain separate services. Nullfin consumes their manifests; this image does not bundle them or alter their provider/indexer settings.

## Compatibility included here

- When Strand opens the source picker with the parent item as `MediaSourceId`, Nullfin returns the complete source list instead of one `Remote - Unknown` fallback.
- The initial Strand source list does not wait for remote media probing. Selecting an actual source still follows the normal probe and playback path.
- File size falls back to add-on metadata, including `behaviorHints.videoSize`, when no probe has run yet.
- When an add-on supplies a score, Strand receives it in the provider filename field its source picker renders.
- Add-on migrations no longer wait for every enabled add-on manifest to reload after each imported entry.
- Manifest discovery is capped at 10 seconds. If a Strand migration encounters an unavailable add-on, Nullfin preserves it as disabled so the remaining entries can finish importing.

These behaviors activate only for requests identifying the client as Strand. Existing Jellyfin client behavior is preserved.

## Updating safely

Keep the Nullfin data directory persistent and back it up before changing versions. Pin a numbered tag when you want repeatable deployments:

```yaml
services:
  nullfin:
    image: ghcr.io/nullstreamin/nullfin:v0.31.1
    restart: unless-stopped
    ports:
      - "3000:3000"
    volumes:
      - ./data:/data
```

Do not publish configured manifest URLs when they contain API keys or user-specific tokens.
