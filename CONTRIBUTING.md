# Contributing

Thanks for taking the time to help. This fork works best when changes stay focused and easy to carry forward.

## Before opening a change

- Search the existing issues first.
- Explain the problem in everyday terms.
- Keep unrelated cleanup in a separate change.
- Do not include credentials, private URLs, or personal server data.

## Testing

Run these checks when your environment supports them:

```sh
cargo fmt --all -- --check
cargo test -p remux-server
```

For dashboard changes, also open the setup and admin pages in a browser and check the mobile layout.

## Pull requests

Explain what changed, why it matters, and how you tested it. Screenshots are helpful for visible changes. A small pull request with a clear purpose is easier to review and easier to keep compatible with future Remux updates.
