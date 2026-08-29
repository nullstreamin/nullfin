# Updating Nullfin from the original Remux project

The goal is to keep Nullfin close enough to Remux that updates remain routine. Community changes should be small, focused, and easy to test on their own.

## Before starting

1. Make sure the current community build is healthy.
2. Back up any test data you care about.
3. Read the incoming Remux release notes and note database migrations or configuration changes.

## Bring in the changes

```sh
git fetch source
git switch main
git merge --no-ff source/main
```

The local remote named `source` should point to `https://github.com/lostb1t/remux.git`.

Resolve conflicts in favor of current Remux behavior first, then reapply the smallest community-specific change needed. Avoid copying whole files when a narrow edit will do.

## Check the result

```sh
cargo fmt --all -- --check
cargo test --workspace
```

Also build the container and check these by hand:

- A fresh setup can create an admin account.
- Existing data opens without a new setup prompt.
- Add-ons load and can return a playable stream.
- A Jellyfin client can sign in, browse, and start playback.
- Restarting the container keeps settings and users.

Publish a new image only after those checks pass. Keep the previous working tag available so a rollback is straightforward.
