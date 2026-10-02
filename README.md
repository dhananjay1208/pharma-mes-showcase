# Helvion Pharma MES Showcase

Static training pages for the MES Practitioner programme, pharma / oral-solid-dose
edition (fictional Helvion Pharma, Plant 2 Lakeworth). No build step — plain HTML,
deployable anywhere.

| Page | Purpose |
|---|---|
| `index.html` | Landing page (three cards) |
| `pharma-mes-comparison.html` | "Without MES vs With MES" — the €1,283,000 nightmare Monday vs the same Monday with MES (€21,400) |
| `pharma-isa95-training.html` | ISA-95 for pharma OSD manufacturing — levels, Parts 1–5, models, segments, knowledge check |
| `pharma-mes-glossary.html` | MES & Pharma glossary — searchable, category-filtered, printable handout |

Deploys on Netlify (publish root, per `netlify.toml`). Every page carries the family
login gate (username `mes`, password `dec25`; instructor code `1208` sets a new
password) — a training-room convenience, not security.

Sibling app: [mesfunctionspharma.netlify.app](https://mesfunctionspharma.netlify.app)
(the pharma MES Functions app).

All plant data, company, product names and figures are fictional or representative
industry ranges for training purposes. No real drug names.
