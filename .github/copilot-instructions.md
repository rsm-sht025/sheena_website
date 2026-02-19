# AI Coding Instructions for Sheena Website

## Project Overview
This is a **Quarto-based portfolio website** showcasing data analytics projects, built with:
- **Quarto** (`.qmd` files for content/projects)
- **HTML/CSS** for styling
- **R Project** configuration (RStudio-based workflow)
- Custom Lua extension for PDF embedding

The site generates static HTML in the `docs/` folder for GitHub Pages hosting.

## Architecture & Key Patterns

### Directory Structure
- **Root `.qmd` files** (`index.qmd`, `about.qmd`, `projects.qmd`, `resume.qmd`): Main site pages
- **`projects/` folder**: Each project has its own folder (e.g., `project1/`, `Project5/`) with:
  - `index.qmd`: Project narrative, findings, code explanations
  - Data files (`.csv`, `.dta`, etc.)
- **`docs/` folder**: Generated HTML output (auto-built by Quarto)
- **`_extensions/jmgirard/embedpdf/`**: Custom Quarto extension for embedding PDF files via `embedpdf.lua`

### Build System
- **Config**: `_quarto.yml` defines:
  - `type: website` (static site generator)
  - Output directory: `docs/` (for GitHub Pages)
  - Theme: "lux" (Bootswatch)
  - Navigation bar with Home, About, Projects links
  - Global CSS: `styles.css`
- **Build command**: `quarto render` (standard Quarto)
  - Renders all `.qmd` files to HTML
  - Copies assets to `docs/` with proper directory structure

### Content Patterns
1. **Project pages** (`projects/*/index.qmd`):
   - Lead with executive summary and key findings
   - Include data descriptions and source file paths
   - Document analysis workflow (data loading → EDA → testing/modeling → conclusions)
   - Use code blocks to show logic (Python/R analysis scripts)
   - Reference local data files in same folder

2. **Home page** (`index.qmd`):
   - Uses "trestles" about template for profile display
   - Includes `files/profile.jpg` image reference
   - Contact links (email, LinkedIn)

3. **Styling**:
   - Custom `styles.css` overrides Quarto defaults
   - Colors: Primary blue (`#0056b3`), subtle background (`#e6dfdff6`)
   - Responsive design with media queries for mobile

## Developer Workflows

### Building/Previewing
```bash
quarto render              # Full build to docs/
quarto preview            # Local dev server + live reload
```

### Common Tasks
- **Adding a new project**: Create `projects/projectN/index.qmd` with data files in same folder
- **Updating styling**: Edit `styles.css` (plain CSS, no preprocessor)
- **Publishing**: Push to GitHub; site auto-deploys from `docs/` branch

### Project-Specific Conventions
1. **Project folder naming**: Lowercase with numbers (e.g., `project1`), except `Project5` (maintain existing case)
2. **Data files**: Store in project folders, reference via relative paths (`data.csv`, not absolute paths)
3. **Code documentation**: Project `.qmd` files explain the "why" behind analysis steps, not just results
4. **R project context**: `sheena_website.Rproj` configured for 2-space indentation

## Critical Integration Points

### Quarto Extensions
- **embedpdf extension** (`_extensions/jmgirard/embedpdf/embedpdf.lua`):
  - Allows embedding PDF documents in `.qmd` files
  - Custom filter for rendering PDFs in HTML output
  - Use in page YAML if embedding PDFs: `embed-pdf: true`

### External Dependencies
- No npm/Python dependencies required for site generation
- Data analysis code (in projects) may use Python (pandas, scipy, statsmodels) or R
- Rendering requires Quarto CLI installation

## Common Pitfalls to Avoid
1. **Path references**: Use relative paths in project `.qmd` files; Quarto auto-resolves from output context
2. **Output directory**: Don't manually edit files in `docs/`; always regenerate via `quarto render`
3. **Case sensitivity**: Respect existing folder case (e.g., `Project5`, not `project5`)
4. **CSS specificity**: Keep custom CSS minimal; leverage Quarto theme (lux) variables when possible
