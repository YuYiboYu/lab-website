# Adding a New Publication

The MINT Lab website uses a static HTML publication list. Publication records and their optional abstract and BibTeX panels are maintained directly in the page rather than generated from a database or a separate bibliography file.

## 1. Files to Edit

Edit [`publications/index.html`](../publications/index.html). It contains all of the following:

- year filter buttons;
- year sections;
- publication-type headings such as “Journal Articles,” “Conference Papers,” “Preprints,” and “Workshop Papers”;
- publication cards;
- inline abstracts and BibTeX records; and
- the JavaScript that controls the year filters and the ABS/BIB panels.

For a routine addition to an existing year, only the new publication entry in `publications/index.html` needs to change. Do not edit the inline filter/toggle JavaScript.

Publication PDFs currently exist in two locations:

- [`assets/pdfs/publications/<year>/`](../assets/pdfs/publications/) is the structured publication archive and the convention used by most entries. For example, a 2025 paper may use `assets/pdfs/publications/2025/paper-name.pdf`.
- [`assets/pdf/`](../assets/pdf/) is a legacy flat directory that is still referenced by some entries.

For a new PDF, prefer the structured `assets/pdfs/publications/<year>/` location unless there is a specific reason to follow a legacy entry.

There is no separate `.bib` directory: BibTeX is embedded in `publications/index.html`. Publication entries do not currently support thumbnail or cover images, and there is no publication-image directory used by this page.

## 2. Prepare Publication Information

Prepare the fields supported by the current implementation.

| Field | Current requirement | How it is represented |
| --- | --- | --- |
| Publication title | Required | `p.publication-title`, with the title inside `strong`. |
| Authors | Required | `p.publication-authors`. |
| Venue or status | Required | Full citation/status text in `p.publication-venue-line`. |
| Publication year | Required for published work | Used in the year section and citation. Forthcoming work instead belongs in the `data-year="forthcoming"` section. |
| Publication type | Required | Placement under the appropriate `h3`, such as Conference Papers, Journal Articles, Preprints, or Workshop Papers. |
| Short venue badge | Required | `publication-venue-short`, optionally linked to an official venue or preprint page. |
| PDF | Optional | A `PDF` link in `p.publication-actions`. |
| DOI | Optional | A `DOI` link in `p.publication-actions`. |
| Abstract | Optional | An `ABS` toggle plus a matching hidden `div.publication-abstract`. |
| BibTeX | Optional | A `BIB` toggle plus a matching hidden `div.publication-bibtex`. |

The page does not currently support publication images, project-page buttons, demo buttons, source-code buttons, or separate BibTeX files. Do not add those fields as part of a routine publication update.

Preserve the existing author emphasis convention described at the top of the Publications page: supervised students are underlined with `u`, and Bo Han is normally bolded with `strong`.

## 3. Copy an Existing Publication Entry

Copy a complete `<li class="publication-entry ...">` from the same publication type and, when possible, the same year. This is safer than assembling a card from individual fragments because the available buttons and panels vary between entries.

For example, this is the complete structure of an existing preprint entry:

```html
<li class="publication-entry publication-entry-2026">
  <div class="publication-entry-side">
    <a class="publication-venue-short publication-venue-link" href="https://arxiv.org/abs/2603.27960" target="_blank" rel="noopener noreferrer">arXiv</a>
    <p class="publication-actions">
      <a class="publication-button pdf" href="../assets/pdf/2603.27960v2.pdf">PDF</a>
      <button class="publication-button bib" type="button" aria-expanded="false" aria-controls="efficient-lvlm-inference-survey-bibtex" data-publication-toggle="efficient-lvlm-inference-survey-bibtex">BIB</button>
    </p>
  </div>
  <div class="publication-entry-main">
    <p class="publication-title"><strong>Towards Efficient Large Vision-Language Models: A Comprehensive Survey on Inference Strategies</strong></p>
    <p class="publication-authors"><u>Surendra Pathak</u> and <strong>Bo Han</strong></p>
    <p class="publication-venue-line">arXiv preprint arXiv:2603.27960, 2026.</p>
  </div>
  <div class="publication-bibtex" id="efficient-lvlm-inference-survey-bibtex" hidden aria-hidden="true">
    <pre><code>@article{pathak2026efficientlvlm,
  author = {Pathak, Surendra and Han, Bo},
  title = {Towards Efficient Large Vision-Language Models: A Comprehensive Survey on Inference Strategies},
  journal = {arXiv preprint arXiv:2603.27960},
  year = {2026},
  url = {https://arxiv.org/abs/2603.27960}
}</code></pre>
  </div>
</li>
```

This example has PDF and BibTeX resources but no DOI or abstract. For a formal paper with a DOI and abstract, copy an existing conference or journal entry that already includes the `DOI` and `ABS` controls. For a publication with no optional resources, copy a short entry such as one of the forthcoming or journal records that contains only the badge and main citation content.

Insert the copied entry into the correct year section and under the correct publication-type heading. The order of the `<li>` elements is the display order; there is no automatic citation sorting.

## 4. Update the Publication Content

Update every publication-specific value in the copied entry:

1. **Year grouping:** Place the entry inside the matching `section.publication-year-section`. When the copied entry has a year class such as `publication-entry-2026`, change it to match the new publication year.
2. **Publication label:** Update the short venue label and its optional link. Formal conference and journal badges retain their year, such as `CHI 2026`. Preprint badges contain only the platform name, such as `arXiv`; the year remains in the citation line.
3. **Title:** Replace the text inside `p.publication-title > strong`.
4. **Authors:** Replace the complete author list while preserving the page's `u` and `strong` conventions.
5. **Venue and year:** Replace the full text in `p.publication-venue-line`, including the correct venue name, volume/pages when applicable, and year.
6. **PDF:** Update the `href` on the `publication-button pdf` link after adding the file. Remove the PDF link if no local PDF is available.
7. **DOI:** Update the `href` on the `publication-button doi` link. Remove it if the publication has no DOI.
8. **Abstract:** Replace the text in `div.publication-abstract`. Give the block a unique ID, then use exactly that ID in both `aria-controls` and `data-publication-toggle` on its ABS button.
9. **BibTeX:** Replace the complete record inside `div.publication-bibtex pre code`. Give the block a unique ID and use that same ID in the BIB button's `aria-controls` and `data-publication-toggle` attributes.

Use a unique, lowercase, hyphen-separated stem for panel IDs, for example:

```text
new-paper-title-abstract
new-paper-title-bibtex
```

The ABS and BIB panels must retain `hidden aria-hidden="true"`; the existing page script manages those attributes when a visitor opens a panel.

If an optional resource is unavailable, remove its complete link or button. If an actions row would otherwise be empty, remove the complete `p.publication-actions` element. If an ABS or BIB button is removed, also remove its corresponding hidden content block. Never link to `#`, an empty URL, a nonexistent file, or `404.html`.

The current implementation has no project or demo links for publication cards, so do not invent them.

## 5. Add Supporting Files

### PDF files

For a new paper, use the structured archive:

```text
assets/pdfs/publications/<year>/<descriptive-paper-name>.pdf
```

The structured archive uses four-digit year directories and mostly lowercase, hyphen-separated filenames, for example:

```text
assets/pdfs/publications/2025/centralization-in-the-decentralized-web.pdf
assets/pdfs/publications/2026/view-synthesis-6dof-pose-estimation-mmwave-radar-nerf.pdf
```

From `publications/index.html`, reference a new file with a path such as:

```html
<a class="publication-button pdf" href="../assets/pdfs/publications/2026/descriptive-paper-name.pdf">PDF</a>
```

Confirm that the filename, capitalization, extension, year directory, and HTML path match exactly. Do not add a PDF link until the file exists in the repository.

The older `assets/pdf/` directory contains mixed filename styles, including arXiv identifiers and publisher-generated names. Existing links to that directory should remain unchanged, but new files should normally use the structured year-based archive.

### BibTeX and images

Keep BibTeX inline in the publication entry; do not create a separate `.bib` file unless the site architecture changes in a separate task.

Publication images are not supported by the current card structure. Do not add an image or create an image directory for a routine publication entry.

## 6. Preserve Existing Formatting

Reuse the markup and classes from the copied entry, including:

- `publication-entry` and any matching year class;
- `publication-entry-side` and `publication-entry-main`;
- `publication-venue-short` and, when linked, `publication-venue-link`;
- `publication-actions` and the existing `publication-button` variants;
- `publication-title`, `publication-authors`, and `publication-venue-line`;
- `publication-abstract` and `publication-bibtex`, when applicable.

Do not modify the publication layout, filters, sorting/order of unrelated entries, colors, fonts, button styles, CSS, navigation, footer, or unrelated publication records. A routine addition should match an existing entry without introducing new classes or inline styles.

If the publication belongs to a year that does not yet have a section and filter button, treat that as a separate coordinated maintenance change. Do not casually alter the filter structure while adding an entry to an existing year.

After editing, preview the Publications page and verify that:

- the entry appears under the correct year and publication type;
- its short badge follows the formal-publication or preprint convention;
- the title, authors, venue, and year are accurate;
- every included PDF and DOI link works;
- ABS and BIB buttons open only their matching panels;
- the relevant year filter shows the entry; and
- no empty action rows, broken links, duplicate IDs, or placeholder content remain.
