# Vertek Robotics website

Static HTML, CSS and JavaScript site. It has no package installation or build step. GitHub Actions publishes the repository to GitHub Pages when changes are pushed to `main`.

## Publish with GitHub Pages

1. Create a public GitHub repository and push this project to its `main` branch.
2. In the repository, open **Settings → Pages** and select **GitHub Actions** as the build and deployment source if it is not selected automatically.
3. The workflow in `.github/workflows/pages.yml` deploys the site. The public URL appears in the workflow run and in the Pages settings.

Keep `index.html`, the `assets`, `images`, and `data` directories together at the repository root. The GRIP catalog is fetched at runtime from `data/grip-products.json`, so it must be included in the deployment.

The contact form opens the visitor's email application with a message addressed to Jarno and Ganesh; it does not submit through a server.

## Quick edits

The product information shown on the website is kept in two data files. You can edit these files without changing the page layout or JavaScript:

- **ROKAE robots, cobots and DH-Robotics grippers:** [data/website-products.json](data/website-products.json)
- **GRIP families, tool changers, kits and prices:** [data/grip-products.json](data/grip-products.json)

### Change a product price

1. Open the relevant JSON file and search for the model name or SKU (for example, `CR7-7/0.98C` or `G-CON-SHW`).
2. Change only its `price_eur` value. Enter a number without a currency sign or thousands separator, such as `1990` or `1990.50`.
3. Save the file. To hide a price, set `price_eur` to `null`. The website formats the number as EUR automatically.

The prices in `website-products.json` are displayed with VAT, matching the existing robot/cobot price note. GRIP list prices in `grip-products.json` are in EUR excluding VAT. The GRIP markup/discount is controlled by `GRIP_CONFIG.markupPercent` in `index.html` (0 means list price).

### Update the live website

After saving your edits, commit and push them to the repository's `main` branch. GitHub Actions will publish them automatically; usually the site updates within a minute or two. If you use GitHub Desktop, the basic steps are **Commit to main** and **Push origin**. The repository is [github.com/vertekwebsite/vertek-robotics-website](https://github.com/vertekwebsite/vertek-robotics-website).

### Edit other content

Most page text, translations, contact details, and visual styling are currently in [index.html](index.html). Search for the text you want to change. The Finnish translations are in the `FI` dictionary in the same file. Product images are referenced by each product's `img` value; keep local images inside `assets/images` and use a relative path.

### GRIP catalog data

GRIP family cards and product tables are generated from `data/grip-products.json`. To update the price list revision, change `price_list_revision`. Keep family `slug` values stable because the website routes use them. A family's “from” price is calculated from the matching products, so it should not be typed into the family description.

The optional global markup or discount is configured in `GRIP_CONFIG.markupPercent` in `index.html`; it defaults to `0` and is applied when GRIP prices are rendered. Family images are local assets referenced by `image` in the JSON. Keep approved image files in the repository and use relative paths such as `assets/images/grip-families/example.webp`; the catalog does not hotlink GRIP product images.
