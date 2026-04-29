# AGENTS.md

How to add a new oEmbed to this repository.

## Steps

1. Create a folder named after the embed (kebab-case): `<embed-name>/`.
2. Add `index.html` with a discovery link in `<head>`:

   ```html
   <link rel="alternate"
         type="application/json+oembed"
         href="https://adafruit.github.io/Adafruit_Learning_System_Embeds/<embed-name>/oembed.json"
         title="<Title>">
   ```

3. Add `oembed.json` next to it:

   ```json
   {
     "version": "1.0",
     "type": "rich",
     "provider_name": "Adafruit",
     "provider_url": "https://adafruit.github.io/Adafruit_Learning_System_Embeds/",
     "title": "<Title>",
     "html": "<iframe src=\"https://adafruit.github.io/Adafruit_Learning_System_Embeds/<embed-name>/\" style=\"display:block;width:100%;aspect-ratio:16/9;border:0;\" loading=\"lazy\" title=\"<Title>\"></iframe>",
     "width": 1200,
     "height": 675
   }
   ```

## Requirements

- All URLs use `https://`. `http://`, `javascript:`, and `data:` schemes are rejected by the consumer's sanitizer.
- The `html` field's outermost element must be an `<iframe>`. Wrapper elements (`<div>`, `<section>`, etc.) are stripped.
- The iframe `src` must point to a page in this repository.
- The iframe is rendered with `sandbox="allow-scripts"` enforced by the consumer. Scripts run, but the iframe gets a unique opaque origin — no access to cookies or `localStorage` on its own host. Build self-contained content; load data inline or from public CDNs with permissive CORS.

## Allowed iframe attributes

`src`, `width`, `height`, `title`, `loading`, `allowfullscreen`, `allow`, `frameborder`, `style`. Anything else is stripped.

## Allowed inline CSS properties

`display`, `width`, `height`, `max-width`, `min-width`, `aspect-ratio`, `border`, `margin`. Other properties are dropped from the `style` attribute. Use `aspect-ratio` for responsive sizing.

## JSON requirements

- Must be valid JSON. The `html` value is a single-line string — no raw newlines inside string literals (escape as `\n` if you genuinely need one).
- `width` / `height` are advisory dimensions for consumers that ignore `aspect-ratio`. `1200 × 675` is a 16:9 default.

## Verify before committing

```sh
curl -sS https://adafruit.github.io/Adafruit_Learning_System_Embeds/<embed-name>/oembed.json | python3 -m json.tool
curl -sS https://adafruit.github.io/Adafruit_Learning_System_Embeds/<embed-name>/ | grep oembed
```

The JSON should print cleanly. The HTML page should show the discovery `<link>`.

