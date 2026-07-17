# Maven Interview Mind Map

An interactive, offline mind map for studying Maven — built for senior Java developers preparing for interviews. All content is stored in a plain JSON file, so you can add, edit, or extend topics without touching any HTML or JavaScript.

---

## Project Structure

```
maven-mindmap/
├── index.html          # The interactive mind map (open this in a browser)
├── build.py            # Build script — converts maven.json → maven-data.js
└── data/
    ├── maven.json      # All mind map content lives here — edit this file
    └── maven-data.js   # Auto-generated — DO NOT edit manually
```

---

## How to Use the Mind Map

1. Open `index.html` in any modern browser (Chrome, Edge, Firefox).
2. No server or internet connection is needed after the first load (fonts are from Google Fonts CDN).

### Navigation

| Action | How |
|---|---|
| Pan | Click and drag on the canvas |
| Zoom | Scroll wheel |
| Fit to screen | Click **Fit** button or press `F` |
| Expand one level | Click a node |
| Expand all | Click **+ Expand All** |
| Collapse all | Click **- Collapse All** |
| Zoom in / out | Click **+** / **-** buttons |
| Toggle dark mode | Click the moon/sun icon |

### Search

| Action | How |
|---|---|
| Search nodes | Type in the search box |
| Next match | `Enter` or click ↓ |
| Previous match | `Shift+Enter` or click ↑ |
| Clear search | `Escape` or click **✕ Clear** |

When you search, the matched node, all its children, and all ancestor nodes are highlighted. Everything else is dimmed.

### Detail Dialog (Info Panel)

Nodes that have a detailed explanation show a small **ⓘ** icon to the left of their label.

- Click the **ⓘ** icon to open a full-page detail panel.
- The panel contains a summary, section-by-section explanation, code examples, an interview tip, and an analogy.
- Close by clicking **✕**, pressing `Escape`, or clicking outside the panel.

### Quiz Dialog (Knowledge Check)

Nodes that have a quiz configured show a small green **t** icon (to the left of the **ⓘ** icon, if both exist).

- Click the **t** icon to start a quiz on that topic.
- Questions are picked **randomly** from the topic's question pool every time you open it, so no two attempts are identical.
- Answer one question at a time using **Previous** / **Next**, then click **Submit** (enabled once all questions are answered).
- The results screen shows:
  - Your score and a pass/fail verdict (pass is 60% or higher).
  - Two D3 charts — a score donut and a correct-vs-incorrect bar chart.
  - A full per-question review with your answer, the correct answer, and an explanation.
- Click **↻ Retake** to try a fresh random set, or **⬇ Download PDF** to export.

#### Downloading the PDF report

1. Click **⬇ Download PDF**.
2. Enter your **name** and **email** (email is validated).
3. Click **Generate PDF**. The report — stamped with your name, email, date, topic, and score — downloads as `Maven-Quiz-<Topic>-<Date>.pdf`.

### Text Selection vs Drag Mode

By default the canvas is in **Drag Mode** — you can pan freely without accidentally selecting text.

Click the **✦ Drag Mode** button in the toolbar to switch to **Select Mode** if you want to copy text from the map.

---

## How to Edit Content

All mind map content is in `data/maven.json`. After every edit, run the build script to regenerate `data/maven-data.js`, then refresh `index.html` in the browser.

### Step 1 — Edit `data/maven.json`

The file has two top-level keys: `meta` and `root`.

#### meta

```json
"meta": {
  "title": "Maven Interview Mind Map",
  "subtitle": "Interview Guide — 11 Years Experience",
  "source": "Durgasoft by Nagoor Babu",
  "version": "1.0",
  "lastUpdated": "2026-07-17"
}
```

Change any of these fields to update the header displayed in the mind map.

#### root — node structure

Every node follows this shape:

```json
{
  "text": "Node label shown on the map",
  "children": [ ...child nodes... ]
}
```

Nodes can be nested to any depth. The root node is always `"text": "Maven"`.

#### Adding a new topic

Find the `"children"` array of the parent where you want to add the topic, then append a new object:

```json
{
  "text": "🔌 Plugin System",
  "children": [
    { "text": "Plugins execute goals" },
    { "text": "Goals are bound to lifecycle phases" },
    { "text": "Example: maven-compiler-plugin" }
  ]
}
```

Leaf nodes (no children) are just `{ "text": "..." }`.

### Step 2 — Add an explanation (optional)

Any node can have an optional `"explanation"` object. This enables the **ⓘ** icon and fills the detail dialog when clicked.

```json
{
  "text": "🔌 Plugin System",
  "explanation": {
    "summary": "One or two sentences describing the concept.",
    "sections": [
      {
        "heading": "What it is",
        "body": "Detailed paragraph. Can be as long as needed."
      },
      {
        "heading": "Why it matters",
        "body": "Second section body."
      }
    ],
    "code": {
      "lang": "xml",
      "snippet": "<plugin>\n  <groupId>org.apache.maven.plugins</groupId>\n  <artifactId>maven-compiler-plugin</artifactId>\n</plugin>"
    },
    "tip": "What to say in an interview about this topic.",
    "analogy": "A plain-English comparison to something familiar."
  },
  "children": [ ... ]
}
```

All `explanation` fields are optional except `summary` — you can include any combination of `sections`, `code`, `tip`, and `analogy`.

| Field | Type | Purpose |
|---|---|---|
| `summary` | string | Bold card shown at the top of the dialog |
| `sections` | array | Heading + body pairs — unlimited |
| `code.lang` | string | Language label shown above the code block (e.g. `xml`, `bash`) |
| `code.snippet` | string | Raw code text — use `\n` for line breaks |
| `tip` | string | Amber callout box — interview angle |
| `analogy` | string | Green callout box — plain-English comparison |

### Step 2b — Add a quiz (optional)

Any node can have an optional `"quiz"` object. This enables the green **t** icon and powers the quiz dialog.

```json
{
  "text": "What is Maven?",
  "explanation": { ... },
  "quiz": {
    "count": 5,
    "questions": [
      {
        "q": "What is Maven primarily used for?",
        "options": ["Memory management", "Project management and build automation", "Thread scheduling", "Database indexing"],
        "answer": 1,
        "explain": "Maven is a project management and build automation tool."
      }
    ]
  },
  "children": [ ... ]
}
```

| Field | Type | Purpose |
|---|---|---|
| `count` | number | (Optional) How many questions to show per attempt. Falls back to `meta.quizDefaultCount` if omitted. |
| `questions` | array | The question pool. Questions are picked randomly each attempt. |
| `questions[].q` | string | The question text |
| `questions[].options` | array | 2–6 answer choices |
| `questions[].answer` | number | **0-based** index of the correct option (`0` = first option) |
| `questions[].explain` | string | (Optional) Explanation shown in the results review |

Notes:
- `answer` is **zero-based**: for `["A", "B", "C"]`, the correct answer `B` is `1`.
- Put **more** questions in the pool than `count` so each attempt shows a different random subset.
- Set a global default for all quizzes with `"quizDefaultCount"` in the `meta` block.

### Step 3 — Run the build script

Requires Python 3 (no extra packages needed).

```bash
# From inside the maven-mindmap/ folder:
py build.py
```

Expected output:

```
Done! Built data\maven-data.js  (10 top-level topics, 27 explanations, 5 quizzes)
```

### Step 4 — Refresh the browser

Press `Ctrl+R` (or `Cmd+R`) in the browser tab showing `index.html`. Your changes appear immediately.

---

## Common Workflows

### Add a new leaf bullet point

1. Open `data/maven.json`.
2. Find the parent node by its `"text"` value.
3. Add `{ "text": "Your new bullet" }` to its `"children"` array.
4. Run `py build.py` and refresh.

### Add a new section with sub-topics

1. Add a new object with `"text"` and `"children"` inside the relevant parent's `"children"` array.
2. Optionally add an `"explanation"` to enable the detail panel.
3. Run `py build.py` and refresh.

### Extend an existing explanation

1. Find the node by its `"text"` in `data/maven.json`.
2. Edit or add fields inside its `"explanation"` object.
3. Run `py build.py` and refresh.

### Change the topic covered entirely

Replace the content of `data/maven.json` with a new structure following the same schema. Update `meta.title` and `meta.subtitle` to match. Run `py build.py` and refresh.

---

## Requirements

| Requirement | Details |
|---|---|
| Python | 3.7 or later (standard library only) |
| Browser | Chrome 90+, Edge 90+, Firefox 88+ |
| Internet | Only for Google Fonts on first load |

---

## File Reference

### `data/maven.json` — content source

The single file you need to edit. Controls every node label, every child relationship, and every detail dialog. The build script reads nothing else.

### `build.py` — build script

Reads `data/maven.json` and writes `data/maven-data.js`. It:
- Converts the `{text, children}` tree into markmap's `{content, children, payload}` format.
- Sets all nodes beyond depth 0 to start folded (`payload.fold = 1`).
- Collects all `explanation` objects into a flat `MAVEN_EXPLANATIONS` lookup keyed by node text.
- Collects all `quiz` objects into a flat `MAVEN_QUIZZES` lookup keyed by node text.

Run it every time you change `maven.json`.

### `data/maven-data.js` — auto-generated

Do not edit this file directly. It is overwritten every time `build.py` runs. Contains four JavaScript globals used by `index.html`:

- `MAVEN_META` — header metadata (including `quizDefaultCount`)
- `MAVEN_ROOT` — the full node tree in markmap format
- `MAVEN_EXPLANATIONS` — flat lookup of node text → explanation object
- `MAVEN_QUIZZES` — flat lookup of node text → quiz object

### `index.html` — the application

Self-contained HTML file. Loads D3, markmap-view, jsPDF, and html2canvas from CDN, then loads `data/maven-data.js` as a local script. All styling, search logic, dialog rendering, info/quiz icon injection, the quiz engine, D3 charts, and PDF export live here. Only edit this file if you need to change the UI, color theme, or application behavior.
