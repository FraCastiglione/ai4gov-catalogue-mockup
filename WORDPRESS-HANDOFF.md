# WordPress developer handoff

## Objective

Implement the approved catalogue design from `index.html` on the existing AI4Gov-X WordPress website while keeping WordPress as the source of truth for activity data.

Reference implementation:

- Live page: https://fracastiglione.github.io/ai4gov-catalogue-mockup/
- Source: `index.html`
- Assets: `ai4gov-logo.png` and `ai4gov-hero.png`

## Recommended implementation

Use a child-theme template or an Elementor-compatible shortcode/template part. Do not maintain a second hard-coded production catalogue.

The official site currently uses:

- the `course` custom post type;
- the `course-language` taxonomy;
- the `course-tag` taxonomy for topics;
- Elementor/JetEngine catalogue and filtering components.

Query the existing `course` posts and map their current JetEngine/custom fields to the interface below. Confirm the exact custom-field keys in WordPress before implementing; the public page does not expose every internal field name.

## Data mapping

| Interface field | WordPress source |
| --- | --- |
| Course title | Course post title |
| Providing institution | Existing institution field or relationship |
| Provider URL | Existing institution URL |
| Topic | `course-tag` taxonomy |
| Language | `course-language` taxonomy |
| Teaching time | Existing teaching-hours field |
| Edition date | Existing start-date field; add an end date when available |
| Registration deadline | Existing deadline field or a new date field |
| Fee | Existing price field |
| Content notes | Existing Content Notes field/off-canvas content |
| Learning outcomes | Existing Learning Outcomes field/off-canvas content |
| Course information | Existing syllabus/document URL |
| Registration page | Existing Register URL |
| Multiple editions | Boolean field or edition relationship |
| Funding available | Boolean field maintained per current edition |
| Information checked | Last-verification date field |

All activity text and external URLs must be rendered from WordPress and escaped using the appropriate WordPress functions (`esc_html`, `esc_url`, `wp_kses_post`). External links should open in a new tab with `rel="noopener noreferrer"`.

## Required page structure

Keep the structure and wording shown in the reference implementation:

1. Two-level AI4Gov-X navigation with **Apply** highlighted.
2. Hero headed **AI4Gov-X extracurricular activities**, including the FSTP summary and Open Calls link.
3. Quality-assurance section headed **High-quality learning. Recognised credentials.**
4. FSTP information panel.
5. Search and filters.
6. Course cards.
7. Footer and Back to top action.

The standard page must open at the top. Direct links to a named section must still scroll to that section.

## Course-card requirements

Each card must support:

- automatic edition status;
- topic, multiple-edition and funding labels;
- title and provider;
- teaching time, edition date, fee and language;
- provider/registration action;
- Course information action when a syllabus or equivalent resource exists;
- FSTP action only for eligible current or future editions;
- expandable details containing Content Notes, Learning Outcomes and known editions.

Do not show funding as available for a past edition.

If there is no registration URL, render a disabled **Registration information unavailable** action rather than an empty or broken button.

## Status rules

Status should be derived from structured dates, with an optional manual override:

- **Registration open**: a registration page is available and the deadline has not passed.
- **Upcoming edition**: the edition is scheduled but registration is not yet open.
- **Registration closed**: the deadline has passed but the activity has not finished.
- **Schedule to be confirmed**: no reliable edition date is available.
- **Past edition**: the edition end date has passed.

Past editions remain visible and are placed after current and upcoming editions. They can still be found through the status filter.

## Filtering and accessibility

Retain the working behavior in `index.html`:

- keyword search;
- topic, provider and status filters;
- funding-only filter;
- sorting;
- page-size selection;
- removable active-filter chips;
- expandable details with `aria-expanded` and `aria-controls`;
- visible focus states and keyboard-accessible controls;
- query-string persistence for catalogue filters.

All activities should be present in the underlying result set. Pagination or page size may control how many are displayed at once.

## WordPress integration outline

1. Create a child-theme template or shortcode for the page.
2. Copy the approved page structure and styles from `index.html` into scoped theme files.
3. Query all published `course` posts with `WP_Query`.
4. Build the catalogue data from WordPress fields and taxonomies.
5. Render cards server-side or expose the escaped data to the existing catalogue script with `wp_json_encode`.
6. Enqueue the CSS and JavaScript only on the extracurricular-activities page.
7. Replace the static representative course array; do not use it as the production database.
8. Test in a staging environment before replacing the existing page.

## Pre-release QA checklist

- Every published course appears once.
- Course titles, providers, teaching hours, dates and prices match WordPress.
- Every provider, registration and Course information link reaches the intended resource.
- Content Notes and Learning Outcomes match the corresponding course.
- Missing URLs render a clear unavailable state.
- Past editions are last and do not show funding.
- Search, filters, sorting, page size and Reset all work together.
- The desktop title remains on one line; mobile text wraps without horizontal overflow.
- The page opens at the top on a normal visit or refresh.
- Direct section links still work.
- Desktop, tablet and mobile layouts have no horizontal overflow.
- Keyboard navigation and expandable details work.
- No JavaScript errors or mixed-content warnings appear.

## Important production note

The reference catalogue includes representative course data for demonstrating the interface. The production implementation must read the complete, maintained course set from WordPress rather than copying that sample array.
