# Frontier AI Lineage Network — Graph-Ready v1.1

Interactive network visualization + corrected/merged dataset (August 2026).

## What's in here

```
index.html            interactive dashboard: Network / Timeline / Heatmap / Rankings /
                      Concentration tabs (D3, one file, loads the CSVs beside it (or in data/),
                      embedded offline fallback)
nodes.csv        66 nodes  (v1 corrected + 36 new from the Aug 2026 research pass)
edges.csv        117 edges (v1 corrected + 79 new)
sources.csv      53 sources (S001–S014 original + S015–S054 research pass)
uncertainty.csv  20 logged claims (U001–U010 original + U011–U020 new)
events.csv       v1 event timeline (unchanged)
CHANGELOG.md          every v1 → v1.1 change, itemized
```

## Publish it (GitHub → Ghost), five steps

1. Create a new GitHub repository (public), e.g. `ai-lineage-network`.
2. Upload **everything in this folder** — all eight files can sit flat at the repo root.
   (GitHub web UI: "Add file → Upload files" → "choose your files" → select all → Commit.)
3. Repo **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
   After a minute your page is live at `https://YOURUSER.github.io/ai-lineage-network/`.
4. In Ghost, edit your page/post, add an **HTML card**, and paste:

   ```html
   <iframe src="https://YOURUSER.github.io/ai-lineage-network/"
           width="100%" height="820" style="border:none;border-radius:10px;"
           loading="lazy" title="Frontier AI Lineage Network"></iframe>
   ```

5. Publish. Updating the map later = just replacing the CSVs in the repo; the
   embed picks up changes automatically.

Note: opening `index.html` by double-clicking (file://) will show a load error —
browsers block CSV fetching from local files. Use GitHub Pages, or locally run
`python3 -m http.server` in this folder and open http://localhost:8000.

## Using the map

- **Channels** toggle edge classes: People / Founder lineage (derived) / Institutional /
  Money / Machines / Methods & models / Academic — matching the five-channel
  inheritance framing plus governance and academic training.
- **Entities** toggle node types (people, labs, parents, universities, funders, compute).
- **Force / Radial**: force-directed by default; radial places older institutions toward
  the center (radius = founding year) grouped by community sector.
- Click a node to isolate its relationships; the panel lists each edge with dates,
  description, and flags (derived / reported). Dashed lines = derived or reported-only.
- Logos load from each organization's favicon; people render as initials.

## Data rules preserved

Primitive vs derived edges are kept distinct (derived FOUNDER_LINEAGE edges carry their
primitive edge IDs and derivation rule). Evidence levels, date precision, and the
uncertainty log carry through. Baidu is intentionally edge-less pending lab-level
personnel documentation (U016). Three items remain flagged for re-verification before
freezing: DNNresearch terms (U011), Google's initial Anthropic date (U015), and the
NVIDIA–OpenAI LOI status (U017).
