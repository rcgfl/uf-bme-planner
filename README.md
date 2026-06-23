# UF BME Planner

A single-file curriculum planning tool for University of Florida Biomedical
Engineering (BME) students. Helps map out a four-year plan of study with
downstream-consequence visualization — surfacing prerequisite conflicts,
elective-credit gaps, and scheduling risk as students build their plan.

**This is not an official UF product.** It's an independent proof-of-concept
tool built and maintained outside of any official department system, currently
in an active feedback phase.

## Live site

`https://rcgfl.github.io/uf-bme-planner/`

## Structure

```
uf-bme-planner/
├── index.html      # the entire app — HTML, CSS, and JS inline, single file
├── data/           # live curriculum data, fetched at runtime by index.html
│   ├── core-courses.json
│   ├── approved-electives.json
│   ├── pathways.json
│   └── course-prefixes.json
└── README.md
```

## How data loading works

`index.html` fetches the four JSON files in `/data` at runtime via
`DATA_URLS` (pointed at this repo's raw GitHub content). If a fetch fails —
no network, GitHub unreachable, file moved — the app falls back to an
embedded snapshot of the same data baked into the JS (`FALLBACK_CORE`,
`FALLBACK_ELECTIVES`, etc.), so the planner still works offline or if GitHub
is briefly down. **The embedded fallback is a point-in-time snapshot and
will drift out of sync with the live JSON files over time** — it's a safety
net, not a substitute for keeping `/data` current.

## Editing curriculum data

Data files in `/data` are edited using the companion **UF BME Pathways
Editor** (a separate standalone tool, not in this repo) rather than by hand.

## Relationship to the old repo

This repo replaces `rcgfl/uf-bme-planner-data` as the live source going
forward. The old repo is left running, unmodified, so existing testers on
older builds aren't disrupted mid-test. All new development happens here.

## Versioning

Version and build date are tracked in `index.html` as `PLANNER_VERSION` and
`BUILD_DATE`, with a full changelog kept inline as comments near the top of
the script. Patch bumps (2.8.x → 2.8.y) are small fixes; minor bumps
(2.8.x → 2.9.0) mark structural or deployment changes.
