# Adding a New Project

The MINT Lab website is a mostly static HTML site. Project cards are maintained directly in the HTML, so adding a project does not require a build script or a data file.

## 1. Files to Edit

Edit [`research/index.html`](../research/index.html). The live project cards are inside:

```html
<section class="projects-section" id="projects" aria-labelledby="projects-heading">
  ...
  <div class="projects-grid">
    <!-- Project cards are here. -->
  </div>
</section>
```

Do **not** add the card to [`projects/index.html`](../projects/index.html). That file only redirects visitors to `research/#projects` and does not contain the live project list.

The repository's existing general-purpose image directory is [`images/`](../images/). However, the current project cards do not reference image files: each one displays an `Image Placeholder`. There is no dedicated project-image directory in the current implementation.

The project styling already exists in `assets/css/styles_feeling_responsive.css`. A routine project addition should not require editing that stylesheet.

## 2. Prepare Project Information

Prepare the fields that the current cards actually use:

| Field | Current requirement | Notes |
| --- | --- | --- |
| Project title | Required | Displayed in `.project-title`. |
| Short description | Required | Displayed in `.project-description`. Keep it concise. |
| Research-area tag | Required by the current pattern | Every existing card has at least one `.project-tag`; some have more than one. |
| Project image | Optional | Existing cards use a placeholder. A real image can replace it. |
| Related publication | Optional | Cards with publications use a “Selected Publications” list; cards without publications omit the entire block. |

You may also collect a project website, GitHub repository, demo link, or documentation link if the project has them. These are optional and the current Projects page has **no dedicated fields or action buttons for them**. Do not invent button markup or add placeholder links during a routine project update. Adding a new type of project link would be a separate design change and should follow an approved site-wide pattern.

## 3. Copy an Existing Project Entry

The safest workflow is to copy an existing `<article class="project-card">` from the `projects-grid` that has the same structure as the new project.

For example, this is the current card structure for a project with tags and selected publications:

```html
<article class="project-card">
  <div class="project-media">
    <div class="project-image-placeholder">Image Placeholder</div>
  </div>
  <div class="project-content">
    <h3 class="project-title">Multi-user Research Infrastructure for XR</h3>
    <p class="project-description">Development of reusable infrastructure for conducting and supporting collaborative multi-user XR research and experiments.</p>
    <div class="project-tags" aria-label="Research-area tags">
      <span class="project-tag">XR Systems</span>
    </div>
    <div class="project-publications">
      <h4>Selected Publications</h4>
      <ul>
        <li><a class="project-publication-link" href="https://doi.org/10.1109/mnet.126.2200385" target="_blank" rel="noopener noreferrer">CoMIC: A Collaborative Mobile Immersive Computing Infrastructure for Conducting Multi-user XR Research</a></li>
        <li><a class="project-publication-link" href="https://doi.org/10.1109/tvcg.2022.3150467" target="_blank" rel="noopener noreferrer">SEAR: Scaling Experiences in Multi-user Augmented Reality</a></li>
      </ul>
    </div>
  </div>
</article>
```

Copy the complete `article`, including both `project-media` and `project-content`, and paste it inside `div.projects-grid`. Its position in that container determines its display order.

For a project without publications, copy an existing shorter card such as “Neural Immersive Content Delivery,” which omits the complete `project-publications` block.

## 4. Update the Content

In the copied card:

1. Replace the text inside `h3.project-title` with the new title.
2. Replace the text inside `p.project-description` with the new description.
3. Update each `span.project-tag`. Add or remove complete tag spans as needed, while keeping at least one tag to match the current pattern.
4. Update the media block as described below. Keep the placeholder if no image is available.
5. If there are related publications, update both the link destination and visible paper title in each list item. External publication links should retain `target="_blank"` and `rel="noopener noreferrer"`.
6. If there are no related publications, remove the entire `div.project-publications` block. Do not leave an empty heading or list.

The current cards have no project website, GitHub, demo, documentation, or download buttons. Do not point unused links to `#`, an empty URL, or `404.html`. Remove unused publication list items or optional blocks completely.

## 5. Add the Project Image

Current project entries use this placeholder:

```html
<div class="project-image-placeholder">Image Placeholder</div>
```

If a real image is available:

1. Store it in the existing [`images/`](../images/) directory.
2. Use a descriptive lowercase, hyphen-separated filename, such as `multi-user-xr-infrastructure.jpg`.
3. Prefer a 3:2 image. The existing CSS displays project media at `180 × 120` pixels and uses `object-fit: cover`, so other aspect ratios may be cropped.
4. Replace the placeholder inside `div.project-media` with an image element:

```html
<div class="project-media">
  <img src="../images/multi-user-xr-infrastructure.jpg" alt="Multi-user XR research infrastructure">
</div>
```

The `../images/...` path is relative to `research/index.html`. Always provide concise, meaningful alternative text. Do not use an empty `alt` value unless the image is purely decorative.

If no image is available, keep the existing placeholder rather than using a broken or unrelated image.

## 6. Preserve Existing Styling

Reuse the existing classes and nesting exactly:

- `project-card`
- `project-media`
- `project-content`
- `project-title`
- `project-description`
- `project-tags` and `project-tag`
- `project-publications` and `project-publication-link`, when applicable

Do not modify global CSS, fonts, colors, navigation, footer, or unrelated cards just to add a project. Do not add inline styles to the new card.

After editing, preview `research/index.html` and verify that:

- the card appears under the Projects heading;
- its title, description, and tags are correct;
- any image loads and is cropped acceptably;
- every included publication link works;
- no empty optional blocks or placeholder links remain; and
- neighboring cards retain their existing layout and content.
