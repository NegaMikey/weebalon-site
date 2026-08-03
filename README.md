# weebalon-site

The homepage for [weebalon.com](https://weebalon.com) — a modern fantasy tabletop
world. Static HTML, no build step, no dependencies.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole site. Styles are inline in a `<style>` block. |
| `perganum.png` | The city map. 1200×960, 26-colour indexed PNG, ~125 KB. |
| `netlify.toml` | Tells Netlify to publish the repo root, and sets cache headers. |

## Deploying

Netlify watches the `main` branch. Push to `main` and the site rebuilds
automatically — usually live in under a minute.

```bash
git add .
git commit -m "what changed"
git push
```

That's the whole deploy process. There's no build command because there's
nothing to build: Netlify copies these files to its CDN as-is.

## Updating the map

Export from Aseprite as an indexed PNG, then **give it a new filename**
(`perganum-v2.png`, `perganum-v3.png`) and update the `src` in `index.html`.

The reason: `netlify.toml` tells browsers to cache PNGs for a year. That makes
the site fast, but it also means a browser that already has `perganum.png` will
keep showing the old one. A new filename sidesteps the cache entirely.

If the new map isn't 1200×960, also update `width` and `height` on the `<img>`
tag so the page doesn't jump around while loading.

## Local preview

Open `index.html` in a browser. That's it.

To check it the way a server would serve it:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.
