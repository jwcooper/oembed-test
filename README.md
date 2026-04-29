# Adafruit oEmbeds

Static, oEmbed-discoverable embeds for the Adafruit Learning System and adafruit-playground.com. Served via GitHub Pages.

## Layout

Each embed lives in its own folder at the repository root:

```
chart-temperature/
├── index.html
└── oembed.json
```

- `index.html` — the embeddable page. Also the iframe `src`. Declares discovery via `<link rel="alternate" type="application/json+oembed" href="oembed.json">`.
- `oembed.json` — the static oEmbed payload (`type: "rich"`).

## URLs

For an embed at `<embed-name>/`:

- Paste this into an editor: `https://adafruit.github.io/Adafruit_Learning_System_Embeds/<embed-name>/`
- oEmbed JSON: `https://adafruit.github.io/Adafruit_Learning_System_Embeds/<embed-name>/oembed.json`

The first URL hits `index.html`, which advertises the JSON via the discovery link. Consumers (Learn, Playground) follow the link and fetch the JSON.

## Adding a new embed

See [AGENTS.md](AGENTS.md).

