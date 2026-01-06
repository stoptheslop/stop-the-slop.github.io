# Production Ready Plan for "Stop the Slop"

This structure outlines the steps to make the site production-ready, focusing on automated signature collection, content management, and SEO/performance improvements.

## 1. Automated Signature Collection

**Goal:** Allow users to sign the manifesto easily, and automatically generate the signature in the code without manual intervention.

### Strategy: GitHub Issue Forms + GitHub Actions

Instead of asking users to create a file or edit YAML directly (which is error-prone), we will use GitHub Issue Forms.

1.  **Create an Issue Form (`.github/ISSUE_TEMPLATE/sign_manifesto.yml`)**:

    - Fields: Name (required), Affiliation (optional), GitHub Username (optional/auto-filled).
    - This provides a user-friendly UI for signing.

2.  **Create a GitHub Action Workflow (`.github/workflows/process_signature.yml`)**:
    - Trigger: When a generic issue with the "sign-manifesto" label is opened.
    - Job:
      - Parse the issue body to extract Name, Affiliation, and Username.
      - Validate the input (prevent spam/slop).
      - Append the new signature to `_data/signatures.yaml`.
      - Commit and push the change to the repository.
      - Close the issue automatically.

**Alternative (Current approach refinement):**
If you prefer the "PR based" approach, we can refine the "new file" link to ensure it targets a specific path and has stricter validation in a CI check. However, Issue Forms are significantly more "production ready" for end-users.

## 2. Configurable Content Management

**Goal:** Decouple content from layout. Move hardcoded text out of `index.html`.

### Strategy: Data Files & Configuration

1.  **Create `_data/content.yml`**:

    - Move the "Manifesto" text here.
    - Add the new "Backdrop" text here.
    - Structure:
      ```yaml
      backdrop:
        title: "The Backdrop"
        body: |
          Background story goes here...
      manifesto:
        title: "The Manifesto"
        items:
          - "We believe in craftsmanship..."
          - "We believe..."
      ```

2.  **Update `index.html`**:
    - Replace hardcoded text with Liquid tags: `{{ site.data.content.backdrop.body | markdownify }}`.
    - Iterate over manifesto items.

## 3. Production Readiness & SEO

**Goal:** Ensure the site is discoverable, fast, and accessible.

1.  **Meta Tags & SEO**:

    - Add `jekyll-seo-tag` plugin.
    - Configure `_config.yml` with title, description, url, twitter handle, etc.
    - Add Open Graph images (for social sharing).

2.  **Performance**:

    - Minify CSS (using Jekyll Sass or simple compression).
    - Ensure images (`assets/images/logo.png`) are optimized.

3.  **Analytics (Optional but recommended)**:
    - Add a privacy-friendly analytics script (e.g., Plausible or simple goatcounter) if metrics matter.

## 4. Implementation Steps (Plan of Action)

1.  **Refactor Content**:
    - Create `_data/content.yml`.
    - Update `index.html` to consume data.
2.  **Implement Backdrop**:
    - Add the new "Backdrop" section to `index.html` using the data source.
3.  **Setup Signature Automation**:
    - Add `.github/ISSUE_TEMPLATE/sign_manifesto.yml`.
    - Add `.github/workflows/process_signature.yml`.
    - Update the "Sign" button in `index.html` to point to the new Issue creation URL.
4.  **Final Polish**:
    - Check mobile responsiveness for new sections.
    - Verify SEO tags.

---

_Created by Antigravity_
