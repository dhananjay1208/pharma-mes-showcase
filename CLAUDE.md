# pharma-mes-showcase — folder context

Deliverable #4 (hosting shell) of DK's **pharma / OSD MES training pack**, hosting the
static pages #2 (comparison), #5 (ISA-95) and #10 (glossary). Canon for every fact,
id, machine code and number: `..\PHARMA-MES-CONTEXT.md` (read it first). Donor
(read-only golden master): `MES Practitioner Training\Apps\tobacco-mes-showcase\`.
Port recipes: `C:\Users\DK\.claude\skills\mes-training-pack\assets\PORT_RECIPES.md`
(#2, #4, #10) and `PACK_CONVENTIONS.md`.

## What is here

| File | What | Content seam |
|---|---|---|
| `index.html` | Landing page, THREE cards (comparison / ISA-95 / glossary), grid `repeat(2, 1fr)` | card copy + `.card.<modifier>` colors: compare = chaos red (cross-pack law), isa = indigo `#312e81→#4f46e5`, gloss = teal `#0f766e→#14b8a6` |
| `pharma-mes-comparison.html` | Without-vs-With MES business case, red = chaos / cyan = precision toggle | ONE `const DATA` object (~line 430): stations, confusion scene, 11 pain cards, two 13-beat Monday timelines, whiteboards, modals (eBR / carton-UI trace / alerts), tables. Page chrome strings (header, banners, section h2s, callouts, the two `<h3>` strings inside `renderConfusion()`) are pharma-authored too. |
| `pharma-isa95-training.html` | ISA-95 standard page (built by a parallel agent — see its own notes in the pack context) | prose sections + `levelData` / `partData` / `quizQuestions` |
| `pharma-mes-glossary.html` | Participant glossary, 7 categories, search + chips + print CSS | `const CATEGORIES` + `const GLOSSARY` (`{c,t,f,d}` records) near the top of the page script. Engine untouched. |
| `favicon.svg` / `favicon.ico` | Pack glyph: white capsule on deep-indigo `#312e81` (from `Apps\_shared\`) | — |
| `netlify.toml` | `[build] publish = "."` | — |

## Login gate (all pages)

The 101-line `<style>+<script>` block before `</body>` is byte-identical on every
page. Keys: sessionStorage **`pharmaShowcaseAuth`**, localStorage
**`pharmaShowcasePass`**. Credentials: `mes` / `dec25`, instructor code `1208`.
Gate accent is pack indigo `#3730a3` (hover `#312e81`), logo 💊, brand "Helvion Pharma".
When editing the gate, edit it once and re-append to all pages (the block is the
single source; `md5sum` the block on each page to confirm).

## Rules

- **No dual-copy rule in this pack.** The tobacco kit kept standalone `Apps\`-root
  copies of the showcase pages in sync by hand; the pharma pack does NOT. This folder
  is the single source of every showcase page — do not create copies in `Apps\`.
- Content lives in the page's data constants; the render engine / CSS is shared
  family code — change it only deliberately and note it in the pack context.
- Canon-lock: state words 1=Running…6=Idle, `TabCountK` = kilo-tablets, `WeightTmg` =
  tenths of a mg, changeover ladder 20 min / 2 h / 3 h / 6 h + lab, unit hierarchy
  10 tablets/blister · 2 blisters/carton · 10 cartons/bundle · 20 bundles/case ·
  48 cases/pallet, packaging OEE 45.0 → 63.5, nightmare Monday €1,283,000 vs
  €21,400 (whiteboard items MUST add up — `scratchpad/verify.mjs` pattern: evaluate
  `DATA` in node and sum the amounts).
- Law 7: no tobacco vocabulary. Grep before finishing (`tobacco|Meridian|Plant 4|
  cigarette|menthol|tax stamp|TPD|OptiSeq|MK3|PK3`). "case-packer" (CP1) and the
  vignette's "consumed fiscal material" wording are canon, not leftovers.
- Real vendor names are fine; company, plant, products and people are fictional.
- Design grammar: family dark-teal gradient body + white cards + Segoe UI stay;
  pack palette indigo (business) / teal (MES) only through `:root`-level colors.

## Comparison page — story spine (for anyone extending it)

Cast: Ingrid (night supervisor), Rafael (production manager), Mei (Cartoner CR3),
Jonas (Press PR3), Amara (granulation), Petr (maintenance), Lucia (QC lab), Omar
(palletizer). Three villains: a sticky-note handover, the frozen FBD2 NIR probe
(LOD flat at 2.0%, true 3.4%), and IBC-0044 returned from Line 5 (ZTX-50) with a
hand-written CLEAN tag → batch B-CX-2417 cross-contaminated and written off.
Confusion scene = the tobacco "6 mm fiscal mark" analog: CDX-10 domestic vs
CDX-10-EXP export carton blanks differ only by the Italian AIC code + bollino
vignette window. With-MES mirror keeps every timestamp; the same batch B-CX-2417 is
released with QP-2417.

## Verify (no browser needed)

1. Extract each `<script>` and `node --check` it; evaluate `DATA` / `GLOSSARY` in a
   `vm` context and assert totals, counts, cast, canon ids (see the `verify.mjs`
   pattern described above — recreate it in the scratchpad if needed).
2. `python -m http.server 8081` in this folder → curl every page for HTTP 200.
3. Grep for tobacco vocabulary (Law 7).
4. Browser smoke (DK's orchestrator): gate login, both Mondays, 3 modals, glossary
   search narrows + highlights, chips filter, print preview.

## Publishing (DK's orchestrator, not this folder's agents)

`git init -b main` → `gh repo create dhananjay1208/pharma-mes-showcase --public
--source . --push` → Netlify site `pharma-mes-showcase` (publish root) → HUMAN step:
add the repo to the Netlify GitHub-App allowlist. Netlify pretty-URLs may rewrite
`.html` links — that is the optimizer, don't "fix" it.

## Status

2026-09-26: index, comparison, glossary, favicons, netlify.toml, README built and
gate-verified (node --check, totals, HTTP 200, vocabulary grep). ISA-95 page built by
the parallel #5 agent. Not yet: git, Netlify, browser smoke.

## pharma-isa95-training.html — structure (from its port, 2026-09-26)
1. Single-file dark-glass page, 8 tabs (Overview/Levels/Parts 1-5/Data Models/Segments/Sepasoft/Examples/Quiz); engine = showSection/selectLevel/selectPart/showModelTab/showSegmentTab/quiz — handlers pass `this`, never `event.currentTarget`.
2. Canon values live in `const WORLD` at the top of the main `<script>`; `levelData`/`partData`/`quizQuestions` read from it; HTML prose in the Data Models/Segments/Sepasoft/Examples sections repeats them (grep the canon when editing either).
3. Theme seam = `:root` (accent indigo #4338ca, teal companion #0f766e); Purdue level + Part colors are cross-pack frozen.
4. Quiz = 12 questions, never-block (wrong answer → explanation → auto-advance after 2.5 s); init order selectLevel(3)→selectPart(3)→renderQuiz() must stay throw-free. `Next` with no selection fires a blocking `alert()` (donor parity).
5. Gate block before `</body>`: keys `pharmaShowcaseAuth`/`pharmaShowcasePass`, `mes`/`dec25`, code `1208`; brand Helvion Pharma.
