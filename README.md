# Newest Sale!

Static full-screen announcement for a TV, hosted on GitHub Pages from the root of `main`.

The screen is dark, with fireworks along the left and right edges. Centered text reads **New Sale Just Landed**, then the rep name, then the sale amount. No invoice, account, or timestamp is shown.

## `data.json`

Another process overwrites this file through the GitHub Contents API when a sale lands. Do not rename it or change its shape:

```json
{
  "rep": "Aaron Moreland",
  "amount": "$1,500"
}
```

| Field | Type | Shown as |
| --- | --- | --- |
| `rep` | string | Rep name, large white text |
| `amount` | string | Amount, larger accent text. Include the `$` and any commas. |

The page requests `data.json?t=<timestamp>` on load and every 60 seconds with `cache: 'no-store'`. When `rep` or `amount` changes, the text swaps and an extra firework burst plays. A failed fetch, or a body that is not this shape, leaves the last values up. The page does a full reload every 30 minutes.

Name and amount stay blank until the first successful read. There is no placeholder name.

## GitHub Pages

`.nojekyll` is at the repo root so Pages serves the files directly. Publish the `main` branch from `/`.

## Local preview

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080`. Edit `data.json` and the screen updates within a minute.
