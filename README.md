# Vertek Robotics website

Static HTML, CSS and JavaScript site. It has no package installation or build step. GitHub Actions publishes the repository to GitHub Pages when changes are pushed to `main`.

## Publish with GitHub Pages

1. Create a public GitHub repository and push this project to its `main` branch.
2. In the repository, open **Settings → Pages** and select **GitHub Actions** as the build and deployment source if it is not selected automatically.
3. The workflow in `.github/workflows/pages.yml` deploys the site. The public URL appears in the workflow run and in the Pages settings.

Keep `index.html`, the `assets`, `images`, and `data` directories together at the repository root. The GRIP catalog is fetched at runtime from `data/grip-products.json`, so it must be included in the deployment.

The contact form opens the visitor's email application with a message addressed to Jarno and Ganesh; it does not submit through a server.

## GRIP catalog data

The GRIP catalog is rendered from [`data/grip-products.json`](data/grip-products.json). Product prices are numeric EUR list prices excluding VAT; products marked `price_on_request` display “Price on request”. Source pages and sections are retained for traceability.

To update the catalog for a later price-list revision, replace the `products` array in that file with the updated rows and change `price_list_revision`. Keep prices as JSON numbers (or `null` when no reliable list price exists), and set `price_on_request` to `true` for inquiry-only rows. Keep family `slug` values stable because the website routes use them.

The optional global markup or discount is configured in `GRIP_CONFIG.markupPercent` in `index.html`; it defaults to `0` and is applied when prices are rendered. Family “from” prices are calculated from each family’s lowest priced, non-inquiry product.

Family images are local assets referenced by `image` in the JSON. Keep approved image files in the repository and use relative paths such as `assets/images/grip-families/example.webp`; the catalog does not hotlink product images.
