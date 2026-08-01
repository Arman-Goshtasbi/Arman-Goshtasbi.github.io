# Portfolio site — setup notes

## Structure
- `index.html` — homepage: a gallery of project tiles (concept photo + title), one per project
- `project-gripper.html` — a full project page template (rename/duplicate per project)
- `project-bracket.html`, `project-thermal.html` — two more example project pages, built from the same template
- `research.html` — publication list, linked to your Google Scholar profile
- `about.html` — bio + contact links
- `style.css` — shared styling

## How a project page works
Each project page has:
1. A **hero** with the concept photo and short pitch
2. A **parts selector** (pill tabs: Overview / CAD / Code / Renders / Simulation) — clicking swaps which section is visible, all on one page, no reload
3. A **tools strip** at the bottom listing the software used (SolidWorks, Python, ANSYS, etc.)

This means each project is self-contained (all its files/media live on one page), but organized internally by file type — so a visitor can jump straight to "CAD" or "Code" without scrolling past everything else.

## To add a new project
1. Copy `project-gripper.html` → rename it (e.g. `project-drone.html`)
2. Edit: page `<title>`, the eyebrow label (e.g. "Course Project — Software", "Published — Robotics"), `<h1>`, hero description
3. Fill in each `.part-panel` section:
   - **Overview**: 2–3 sentence summary + a small gallery
   - **CAD**: one `.file-row` per file, linking to the file in your project's GitHub repo
   - **Code**: a short snippet in `.code-block` + a link to the full repo
   - **Renders**: `.gallery-item` divs — swap for `<img>` tags once you have images
   - **Simulation**: result files + images, same pattern as CAD/Renders
4. Update the `.tools-strip` tags at the bottom to match tools actually used
5. Add a matching tile to `index.html`'s project grid, linking to your new page

## Marking status (published / unpublished / course / hobby)
Each project's eyebrow label on both the homepage tile and the project hero does this —
e.g. `UNPUBLISHED — SOFT ROBOTICS`, `HOBBY — MECHANICAL`, `COURSE PROJECT — SIMULATION`.
No separate tagging system needed; it's just the label text.

## To use it
1. Create a GitHub repo named exactly `yourusername.github.io`
2. Put these files in the repo root (not a subfolder)
3. Settings → Pages → Source: Deploy from branch → `main` → `/root`
4. Site goes live at `https://yourusername.github.io`

## To customize
- **Hero photos**: add images to an `assets/` folder, then set `style="background-image:url('assets/yourimage.jpg'); background-size:cover; background-position:center;"` on the `<header>` tag
- **Colors/fonts**: CSS variables at the top of `style.css` — change `--accent` to switch the orange highlight
- **Research page**: replace the placeholder rows with your real papers (title, venue/year, link) — pull these straight from your Scholar profile
