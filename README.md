# Bird Orders

A single-page reference site covering all 44 extant bird orders, organized by phylogenetic taxonomy.

**Live site:** [sveppalicious.github.io](https://sveppalicious.github.io)

## What's included

Each order card shows:

- **Common names** and taxonomic placement within the avian phylogeny
- **Info callout** with distribution, habitat, recognition, feeding ecology, and breeding behavior
- **Species count** badge sourced from the eBird/Clements Taxonomy (v2025)
- **Foot type** and **chick development** icons
- **Fun facts** and notable observations
- **Etymology** of the Latin/Greek order name, with confidence indicators and source links
- **Phylogeny images** from the Birds of the World Phylogeny Explorer

## How it works

The site is a static HTML page that renders Obsidian-flavored Markdown client-side:

1. `Orders.md` contains all the content, written using Obsidian callout syntax (`> [!Info]`, `> [!Tip]`, etc.)
2. `index.html` fetches and processes the Markdown at load time using [marked.js](https://marked.js.org/)
3. A custom `preprocessObsidian()` function converts Obsidian-specific syntax (callouts, image embeds, heading hierarchy) into HTML
4. Additional data files (`SpeciesNumbers.md`, `Etymology.md`) are fetched in parallel and injected into the rendered page

No build step, no framework — just open `index.html` in a browser or deploy to any static host.

## Data sources

1. Order descriptions adapted from: Lovette, I. J. & Fitzpatrick, J. W. (Eds.). *Handbook of Bird Biology*, 3rd ed.
2. Taxonomic text from: Hosner, P. *A Higher-Level Classification of Birds*. University of Copenhagen.
3. Phylogeny images from the [Birds of the World Phylogeny Explorer](https://birdsoftheworld.org/bow/phylogeny) (Miller et al., 2025).
4. Foot type icons adapted from Carril et al. (2024), *Nature Communications* 15, 9888.
5. Species counts from the eBird/Clements checklist (Clements et al., 2025).
6. Order name etymologies researched with AI assistance.

## Local development

```bash
# Serve locally (any static server works)
python3 -m http.server 8000
# Then open http://localhost:8000
```

## File structure

```
Orders/
  index.html          # The entire app (HTML + CSS + JS)
  Orders.md           # Main content (Obsidian Markdown)
  SpeciesNumbers.md   # Species count data table
  Etymology.md        # Order name etymology data table
  photos/             # Bird and phylogeny images
  icons/              # Foot type and chick development icons
```
