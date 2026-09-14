# [vrsn] Landing Pages — Higher-Load + Pregnancy

Two self-contained landing pages for the [vrsn] Pain Relief Sneaker, cloning the
Honex LP structure with [vrsn] branding. Built July 2026.

## Deploy

The two HTML files are fully self-contained (all generated imagery is embedded
as base64; real product photos load from the vrsn.co CDN; fonts from Google
Fonts). Host them anywhere as static files:

| File | Angle |
|---|---|
| `vrsn-higher-load.html` | Higher-load avatar ("Built for the load. All of it.") |
| `vrsn-pregnancy.html` | Pregnancy avatar ("Your feet changed. Your shoes didn't.") |

No build step is needed to deploy. Upload the HTML files and you are done.

## Rebuild (optional)

`build_pages.py` regenerates both HTML files from the assets:

```
python3 build_pages.py
```

Requires Python 3 + Pillow. Inputs:

- `out/` — 18 generated lifestyle/UGC images (embedded into the pages at build)
- `refs/` — shoe cutouts (white/navy/beige/black) + official [vrsn] wordmarks

## Image generation pipeline

Images were generated with Nano Banana Pro (gemini-3-pro-image), with the real
shoe cutout pinned as a reference for product fidelity. Scripts, in order of
creation (kept for reruns and future variants):

- `gen_scenes.py` — the 6 core lifestyle scenes (heroes, how-it-works, comfort)
- `gen_ugc.py` — 12 UGC-style review photos (majority adult women)
- `gen_fix.py` / `gen_fix2.py` — later regenerations: distinct reviewer faces,
  faces always visible, landscape 4:3 framing for the comfort card

Requires a Gemini API key at `~/.gemini_key`.

## Still pending before launch

- Checkout: the CTA currently forwards pairs/color/size + all UTM params to the
  vrsn.co product page. Swap in a real cart permalink when available.
- Two testimonial quotes per page are crafted marketing copy; replace with real
  verified reviews as they come in.
- Urgency claim (sale end date / stock) intentionally omitted until confirmed.

## Live pages (September 2026)

Two Skyvane advertorials built in this repo are deployed on get.vrsn.co from
the `vrsn-lp` repo (`client/public/adv/<slug>/index.html`, Vercel rewrite in
`vercel.json`). The files here are the source; the GitHub Pages copies are
previews only (the prize-draw pop-up is skipped on github.io because that
origin cannot hand the prize to /b).

| Source file | Live URL |
|---|---|
| `5-reasons-barefoot-shoes-doesnt-fixed-foot-pain.html` | https://get.vrsn.co/adv/barefoot |
| `i-bought-my-mom-6-pairs-caregiver.html` | https://get.vrsn.co/adv/caregiver |

Shipping copy on both follows the PDP (`/b`): "Ships by <order + 7 days> — free
shipping" and the FAQ line "US orders ship within 1-2 business days and
typically arrive in 4-6 business days." Both load `/adv/prize-draw.js` (same
rules as the PDP and the other /adv/ pages: 10%, code B9X2H71ZKXKY, 30-min TTL,
fires 5s after the offer block is reached).
