---
title: User Guide
---

The checker walks you through three steps: scan your notebook for issues, review the results grouped by category, then apply fixes with guided interfaces.

## Scanning

1. Open the notebook you want to audit in JupyterLab.
2. Click the **Digital accessibility icon** in the right sidebar to open the extension panel.
3. Click **Analyze Notebook** to scan for issues.
4. Results appear grouped by issue type (image, heading, table, color, link).

## Fixing

### Image

- **Missing alt text:** Enter descriptive alt text in the text field. If the image contains text, the field is pre-filled with detected text. A vision model can generate a suggestion.

### Headings

- **No H1:** Type the notebook title in the text field — a new H1 cell is inserted at the top.
- **Multiple H1s:** Demote secondary H1s to H2 with one click.
- **Duplicate heading text:** Edit the highlighted heading to make it unique.
- **Wrong heading order:** Select the correct heading level from the dropdown.
- **Empty heading:** Type heading content in the text field.

### Tables

- **Missing headers:** Choose row, column, or row-and-column headers from the dropdown.
- **Missing caption:** Enter a table summary in the text field. A language model can generate a suggestion.
- **Missing scope:** Click **Apply** to inject `scope="col"` or `scope="row"` attributes.

### Color

- **Insufficient contrast:** Replace flagged images with versions that meet contrast guidelines.

### Links

- **Indiscernible link text:** Edit the link text or `aria-label` in the text field to make it descriptive.

## AI assistance

The extension can use language and vision-language models to suggest table captions and alt text. AI suggestions appear only when the AI option is enabled in the corresponding fix interface. Review suggestions and make edits before applying them.

### Configuration

- Open `Settings > Settings Editor > A11y Checker Settings` in JupyterLab.
- Provide the API endpoint, API key, and model name.

```{warning}
Do not include sensitive data in notebooks. API calls are configured per-user and go to your specified endpoint.
```
