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
