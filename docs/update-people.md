# Adding or Updating a Person

The MINT Lab People page is maintained as static HTML. Additions and profile updates are made directly in the page; there is no separate people data file or content-management system.

## 1. Files to Edit

Edit [`people/index.html`](../people/index.html). It contains the People page sections, person cards, undergraduate list, profile links, timelines, research interests, and image references.

Member photos are stored in [`images/people/`](../images/people/). From `people/index.html`, those files are referenced with a relative path beginning `../images/people/`.

The shared People-card styling is already defined in `assets/css/styles_feeling_responsive.css`. Adding or updating a person should not require a CSS change.

## 2. Prepare Person Information

Only a full name is present on every current person card. All other profile information is optional and should be included only when it has been verified and provided.

| Field | Current requirement | How it is represented |
| --- | --- | --- |
| Full name | Required | The visible `h3` and the card's accessible ID. |
| Role or designation | Optional | A paragraph in the card body; the person's broader category is also conveyed by the section heading. |
| Department or affiliation | Optional | Additional lines in the role/affiliation paragraph, separated with `br` elements. |
| Timeline/date | Optional | A standalone paragraph containing only the date value. |
| Research interests | Optional | A paragraph beginning with `<strong>Research interests:</strong>`. |
| Personal website | Optional | Globe profile icon. |
| LinkedIn | Optional | LinkedIn profile icon. |
| Google Scholar | Optional | Google Scholar profile icon. |
| GitHub | Optional | GitHub profile icon. |
| Email | Optional | Mail profile icon using a `mailto:` URL. |
| Professional image | Optional | An `img.person-photo`; cards without an image use an empty visual placeholder. |

Also prepare a unique lowercase, hyphen-separated identifier derived from the person's name, such as `sthitadhi-sengupta`. The value must match between the card's `aria-labelledby` attribute and the person's `h3 id`.

Do not infer a full name, role, timeline, research interests, link, email address, or image from incomplete information.

## 3. Choose the Correct Section

The current page uses these sections:

1. **Faculty Director** — one featured card using `person-card-featured`.
2. **Research Scientist** — standard cards inside `people-grid people-grid-compact`.
3. **Ph.D. Students** — student cards inside `people-grid people-grid-students`.
4. **Alumni** — standard cards inside `people-grid people-grid-compact`.
5. **Undergraduate Researchers** — simple text entries inside `ul.undergraduate-list`, not cards.
6. **Collaborators** — narrative paragraphs describing collaboration areas; it is not currently a list of individual profiles.

Add a person under the appropriate existing section. Do not create a new category or move unrelated people unless that organizational change has been explicitly requested.

For an undergraduate researcher, copy an existing `li` and preserve its compact format:

```html
<li>Name, project or research topic, October 2021 &ndash;</li>
```

Do not convert the undergraduate list to cards. Likewise, do not introduce individual cards into the narrative Collaborators section as part of a routine profile update.

## 4. Copy an Existing Person Entry

For a card-based section, copy a complete `article.person-card` from the same category and update it. Choose a card with a similar set of optional fields.

For example, this is the current Ph.D. student card structure for a person with a timeline, research interests, and profile links:

```html
<article class="person-card" aria-labelledby="fahim-arsad-nafis">
  <div class="person-photo" aria-hidden="true"></div>
  <div class="person-card-body">
    <h3 id="fahim-arsad-nafis">Fahim Arsad Nafis</h3>

    <p>August 23 &ndash;</p>

    <p><strong>Research interests:</strong> collaborative immersive analytics, visualization, extended reality, human-centered systems, and open-source research ecosystems.</p>

    <div class="person-links" aria-label="Profile links for Fahim Arsad Nafis">
      <a class="person-profile-link" href="https://www.linkedin.com/in/fahim-arsad/" target="_blank" rel="noopener noreferrer" aria-label="Fahim Arsad Nafis LinkedIn"><span class="icon-linkedin" aria-hidden="true"></span></a>
      <a class="person-profile-link" href="https://scholar.google.com/citations?user=ntjZ270AAAAJ&amp;hl=en" target="_blank" rel="noopener noreferrer" aria-label="Fahim Arsad Nafis Google Scholar"><i class="ai ai-google-scholar" aria-hidden="true"></i></a>
      <a class="person-profile-link" href="https://github.com/Nafis2605/" target="_blank" rel="noopener noreferrer" aria-label="Fahim Arsad Nafis GitHub"><span class="icon-github" aria-hidden="true"></span></a>
      <a class="person-profile-link" href="mailto:fnafis2@gmu.edu" aria-label="Email Fahim Arsad Nafis"><span class="icon-mail" aria-hidden="true"></span></a>
    </div>
  </div>
</article>
```

Copy the complete card, including the photo or placeholder element and `person-card-body`. Its location within the surrounding grid determines its display order.

When updating an existing person, edit that person's current card in place. Do not replace verified information with a shorter or less complete value unless the update specifically requires it.

## 5. Update the Person Information

Review and update each applicable part of the copied card:

1. **Accessible identifier:** Change both `article[aria-labelledby]` and `h3[id]` to the same unique name-based identifier.
2. **Name:** Replace the visible `h3` text and update every person-specific `aria-label`.
3. **Role, designation, department, or affiliation:** Update the optional descriptive paragraph. The featured Faculty Director card currently separates its designation, department, and university with `br` elements.
4. **Timeline/date:** Replace the standalone timeline paragraph only when a value is provided.
5. **Research interests:** Replace the optional research-interest text without inventing missing topics.
6. **Profile links:** Update both each `href` and its accessible `aria-label`. Add only verified links.
7. **Email:** Use a `mailto:` URL and update the accessible label.
8. **Image:** Replace the photo path and alternative text, or keep the placeholder when no professional image is available.

Current card timelines display only the date value, for example:

```html
<p>August 23 &ndash;</p>
```

Do not add the visible label `Timeline:`. Use `&ndash;` for the en dash to match the existing HTML. Preserve an existing person's timeline exactly unless a new value has been provided. If there is no timeline, omit the complete paragraph rather than adding an empty value.

Unavailable profile links must be omitted. Never point an icon to `#`, an empty URL, `404.html`, another person's profile, or a guessed destination. If a person has no profile links, omit the complete `div.person-links`, as the current Nan Wu and Elizabeth cards do.

## 6. Profile Icons and Links

Place available profile icons inside:

```html
<div class="person-links" aria-label="Profile links for Full Name">
  ...
</div>
```

Use this order, skipping any unavailable link without leaving a gap or placeholder:

1. Personal Website
2. LinkedIn
3. Google Scholar
4. GitHub
5. Email

The current icon markup is:

```html
<!-- Personal Website -->
<a class="person-profile-link" href="https://example.com/" target="_blank" rel="noopener noreferrer" aria-label="Full Name personal website"><span class="icon-globe" aria-hidden="true"></span></a>

<!-- LinkedIn -->
<a class="person-profile-link" href="https://www.linkedin.com/in/example/" target="_blank" rel="noopener noreferrer" aria-label="Full Name LinkedIn"><span class="icon-linkedin" aria-hidden="true"></span></a>

<!-- Google Scholar -->
<a class="person-profile-link" href="https://scholar.google.com/citations?user=EXAMPLE&amp;hl=en" target="_blank" rel="noopener noreferrer" aria-label="Full Name Google Scholar"><i class="ai ai-google-scholar" aria-hidden="true"></i></a>

<!-- GitHub -->
<a class="person-profile-link" href="https://github.com/example" target="_blank" rel="noopener noreferrer" aria-label="Full Name GitHub"><span class="icon-github" aria-hidden="true"></span></a>

<!-- Email -->
<a class="person-profile-link" href="mailto:name@gmu.edu" aria-label="Email Full Name"><span class="icon-mail" aria-hidden="true"></span></a>
```

These examples use the exact classes and element types used by the current People page. Replace the example values only with verified information. In HTML attributes, encode ampersands in query strings as `&amp;`.

External Website, LinkedIn, Google Scholar, and GitHub links must retain `target="_blank"` and `rel="noopener noreferrer"`. Email links use `mailto:` and do not need a new-tab attribute.

Do not add text labels inside the circular icon links. The `aria-label` supplies an accessible name, while the icon itself retains `aria-hidden="true"`.

## 7. Add or Update a Profile Image

Store member images in:

```text
images/people/
```

The current files are `BoHan.jpg` and `ruizhi.png`. They use person-based filenames but do not follow one consistent capitalization or extension convention. For a new file, use a clear name based on the person's full name, avoid spaces, and keep the filename and extension exactly consistent with the HTML path. For example, a lowercase hyphen-separated filename such as `first-last.jpg` is easy to maintain.

Replace the no-image placeholder:

```html
<div class="person-photo" aria-hidden="true"></div>
```

with an image element:

```html
<img class="person-photo" src="../images/people/first-last.jpg" alt="First Last" />
```

When updating a photo, retain `class="person-photo"` and provide the person's name as concise alternative text. The existing CSS gives photos a responsive 4:3 frame and uses `object-fit: contain` with centered positioning. Use a clear professional image that works within that frame.

Do not add inline sizing or change global image CSS for one person. If no image is provided, retain the existing placeholder rather than using a broken, guessed, or unrelated image.

## 8. Research Interests and Other Text

Research interests use a normal paragraph with a bold inline label followed by a comma-separated list:

```html
<p><strong>Research interests:</strong> Immersive Systems, Human-Robot Interaction, Systems and Networks</p>
```

Keep the exact `Research interests:` label and follow the capitalization and punctuation style of the verified text supplied for that person. Do not convert the interests to tags, bullets, or a separate card section.

Role and affiliation text also remains in normal paragraphs. Use `br` only when separate lines are appropriate, as in the existing Faculty Director entry:

```html
<p>Associate Professor<br />
Department of Computer Science<br />
George Mason University</p>
```

Do not invent research interests, titles, departments, affiliations, timelines, full names, or other biography text. Preserve existing verified information when an update does not replace it.

## 9. Preserve Existing Formatting

Reuse the structure and classes from the appropriate existing entry, including:

- `people-section` and the existing grid class for the category;
- `person-card` and, only for the Faculty Director, `person-card-featured`;
- `person-photo`;
- `person-card-body`;
- `person-links` and `person-profile-link`; and
- `undergraduate-list` for undergraduate researchers.

Do not unnecessarily modify the People page layout, card sizes, image sizing, fonts, colors, icon styles, navigation, footer, or unrelated people entries. Do not add inline styles or new CSS classes for a routine profile update.

After editing, preview the People page and verify that:

- the person appears in the correct section and order;
- the card ID and `aria-labelledby` value match;
- the timeline displays only its value, without `Timeline:`;
- research interests and other text match the supplied information;
- profile icons appear in the correct order and only for available links;
- external links open in a new tab and email uses `mailto:`;
- any image loads from `images/people/` and fits the existing frame; and
- no unrelated profile information has changed or shifted between people.
