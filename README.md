# AI4Gov-X Extracurricular Activities Catalogue

Approved front-end reference for the redesigned AI4Gov-X extracurricular activities page.

Live reference: https://fracastiglione.github.io/ai4gov-catalogue-mockup/

## Files

- `index.html` - complete working page, including structure, styling, course-card data and interactions
- `ai4gov-logo.png` - AI4Gov-X logo asset
- `ai4gov-hero.png` - hero background image
- `WORDPRESS-HANDOFF.md` - implementation notes and QA checklist for the WordPress team

## For Developers

The complete reference implementation is in `index.html`. It can be opened directly in a browser without a build step or external dependency.

For the production WordPress implementation, read `WORDPRESS-HANDOFF.md`. The recommended approach is to retain WordPress/JetEngine as the source of course data and port this interface into a child-theme template or Elementor-compatible shortcode.

Clone the repository:

```bash
git clone https://github.com/FraCastiglione/ai4gov-catalogue-mockup.git
```

Alternatively, download the repository as a ZIP from GitHub.

## Viewing Locally

Open `index.html` in a browser.

## GitHub Pages

After pushing this repository to GitHub:

1. Open the repository settings.
2. Go to **Pages**.
3. Set source to **Deploy from a branch**.
4. Choose branch `main` and folder `/root`.
5. Save.

The current public version is available at the live reference URL above.
