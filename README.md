# TextMapReady Terms: controlled-vocabulary term search for VOSviewer

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24557534.svg)](https://doi.org/10.5281/zenodo.24557534)

*Formerly PDFTerms.* Live app: https://textmining2.vercel.app

**A subject-neutral, directed text-mining tool: you define the terms, the app counts their occurrences and co-occurrences across your PDFs, shows the network in the app and generates a JSON file ready for VOSviewer.**

It complements [TextMapReady Words](https://text-umber-delta.vercel.app), which performs open extraction of every word. Here the logic is reversed: the vocabulary is controlled by you, which makes it well suited to evaluating reports and to systematic reviews in any field.

---

## Subject-neutral, with domain packs

The app is not tied to any topic. The term library is loaded at runtime as a **domain pack**, so the same app serves decarbonisation, the SDGs, ESG, or any other subject.

- A domain pack is a plain-text file in the term format: `[Category] Canonical label = variant1; variant2; wildcard*`
- Load one with **Load library (domain pack)**. Bare terms you type then expand to their variants automatically.
- Without a pack, terms are searched literally (still fully usable).
- Build a pack by writing terms in area A and clicking **Save terms (.txt)**; that file can be reloaded later as a library.
- A thesaurus in CSV (columns `term, category, variants`, variants separated by `;`) can be loaded as a library too. In that case only the variants are searched, not the label, which reproduces a coding pipeline where the label is just the name of the measure.
- The option **Also search the label itself** decides whether the text before `=` counts as a search term. Untick it when the label is only a name (for example `Wind = wind power; wind energy`).
- An example pack for maritime/port decarbonisation, aligned to Fadiga et al. (2024), is included: `decarbonisation-keywords-fadiga.txt`.

---

## Two ways to form clusters

| | Free terms | Defined clusters (up to 6) |
|---|---|---|
| Logic | Inductive: clusters emerge from the data | Deductive: clusters come from your theory or framework |
| Who forms the clusters | The app (Louvain modularity) or VOSviewer | You, one box per cluster |
| Typical use | Exploration, bibliometric review | Testing a framework (SDGs, ESG pillars, GRI topics) |

Running the same terms in both modes shows whether the theoretical groups actually appear in the texts. In Free terms mode the JSON carries no clusters by default, so VOSviewer forms its own; an option in the Export tab sends the app's clusters instead.

## Two ways to see the result

- **View in the app**: interactive network (node size = occurrences, line thickness = co-occurrence, colour = cluster), cluster legend, bar chart of occurrences and a high-resolution PNG download (3000 px).
- **Export to VOSviewer**: JSON for VOSviewer Online plus the CSV files.

---

## Difference from TextMapReady Words

| | TextMapReady Words | TextMapReady Terms |
|---|---|---|
| Approach | Open, data-driven | Directed, theory-driven |
| Who chooses the terms | The algorithm | You |
| Typical use | Initial exploration | Report evaluation, systematic review |

---

## Features

- Two clearly separated areas: **A**, where you type the keywords you want, and **B**, where the app shows the synonyms it generated for each one (your study's thesaurus)
- Upload of multiple PDFs by drag & drop (text extraction is 100% local)
- Loadable domain packs (libraries) for any subject; bilingual variants supported (e.g. English + Portuguese)
- Manual synonym grouping with `=` (always takes priority over the library)
- Free terms mode (clusters detected with Louvain) or Defined clusters mode (up to 6 named boxes)
- Warnings for terms placed in more than one cluster, duplicate cluster names and empty boxes
- In-app interactive network (node area proportional to occurrences, strongest 100/300/1000/all links shown) with high-resolution PNG export, and a bar chart of occurrences
- Cluster names and colours carried into the VOSviewer JSON, so VOSviewer shows the same legend as the app
- Compound-term search (e.g. `shore power`) and wildcards (`emission*`)
- Case-insensitive and accent-insensitive matching
- Binary counting per document or co-occurrence per sentence (sentences end at . ! ? or a blank line, not at PDF line breaks)
- Overlapping variants of the same term count once (`green hydrogen` is one mention, not two)
- Compounds broken at the end of a line (`just-in-` / `time`) and hyphen or space variants (`shore-power`, `shore power`) are matched
- Each file shows pages and words, with a warning when a PDF has little text (scanned or image-only)
- Coverage diagnostics: lists the terms with zero occurrences
- Exports: VOSviewer JSON, thesaurus mapping (CSV), term × document matrix (CSV), frequencies (CSV), documents (CSV: pages, words, terms found)
- Save and load term lists / libraries (.txt)
- CSV files with UTF-8 marker, so accents open correctly in Excel
- Accessibility checked against WCAG 2 AA (axe-core)

---

## How to use

1. Upload one or more PDFs
2. (Optional) Load a domain pack for your topic with **Load library**
3. Choose **Free terms** or **Defined clusters (up to 6)**
4. Type your search terms in area A (or in the cluster boxes), one per line; check area B to confirm the synonyms
5. Adjust the co-occurrence scope and the minimum thresholds
6. Click **Count terms and build network**
7. Explore the network in **View in the app**, or go to **Export to VOSviewer**, download the JSON and open it at [app.vosviewer.com](https://app.vosviewer.com) → Open → VOSviewer JSON file

> Scanned PDFs (image only) require OCR before processing.

---

## Term and pack format

```
CO2                              # bare term, expands if the loaded pack knows it
ballast water                    # compound term
[Energy] hydrogen = H2; green hydrogen   # category: loads into the "Energy" box in Defined clusters mode
govern*                          # wildcard
```

---

## Technologies

| Technology | Use |
|---|---|
| HTML / CSS / JavaScript | Interface and logic |
| PDF.js (v3.11) | Text extraction from PDFs |
| vis-network (v9.1) | In-app network visualisation |
| VOSviewer | Network visualisation (export) |
| Vercel | Hosting |

---

## Privacy

All processing happens in the browser. No file is sent to any server.

---

## How to cite

> Cunha, D. R. (2026). TextMapReady Terms: directed text mining of PDF reports for VOSviewer [Software]. Zenodo. https://doi.org/10.5281/zenodo.24557534

## Author

**Darliane Ribeiro Cunha, PhD**
Researcher in sustainability governance, environmental analytics and the SDGs
[ORCID: 0000-0003-2548-1237](https://orcid.org/0000-0003-2548-1237)
