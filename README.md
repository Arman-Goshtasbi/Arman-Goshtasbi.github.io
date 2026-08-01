# Portfolio site — setup notes

## Structure
- `index.html` — **Welcome** tab: photo, short bio, quick links (email/GitHub/Scholar/CV)
- `projects.html` — **Projects** tab: gallery of project tiles, each linking to its own page
- `project-gripper.html`, `project-bracket.html`, `project-thermal.html` — individual project pages, each with a description + CAD/Code/Renders/Simulation tabs
- `tools.html` — **Tools** tab: click a software name, see every file across all projects made with it
- `research.html` — **Research** tab: publication list, pulled from your CV, linked to Google Scholar
- `style.css` — shared styling

## How each project page works
1. **Hero** — concept photo + short pitch
2. **Tab selector** (Overview / CAD / Code / Renders / Simulation) — click to swap sections, no page reload
3. **Tools strip** at the bottom — software used for that project

## How the Tools page works
All the tool → file mappings live in one place: the `TOOL_FILES` object inside the `<script>` tag at the bottom of `tools.html`. Each tool (e.g. "SolidWorks") maps to a list of files, and each file records which project it belongs to and a link to it.

**To add a new file to a tool**: open `tools.html`, find the tool's array in `TOOL_FILES`, and add an entry:
```js
{ project: "Project title", projectLink: "project-x.html",
  file: "filename.ext", fileLink: "https://github.com/...",
  type: "CAD" | "Code" | "Simulation" | "Render" }
```
**To add a brand-new tool**: add a new key to `TOOL_FILES`, e.g. `"Fusion 360": [ ... ]` — it will automatically appear as a clickable pill.

This is the one file you'll touch most often as you add projects, since it's the cross-reference between "what software" and "which files."

## To add a new project
1. Copy `project-gripper.html` → rename it (e.g. `project-drone.html`)
2. Edit: page `<title>`, eyebrow label (e.g. "Course Project — Software", "Published — Robotics"), `<h1>`, hero description
3. Fill in each tab section (Overview / CAD / Code / Renders / Simulation) — delete or leave a "not applicable" note for any that don't apply to that project
4. Update the tools-strip tags at the bottom
5. Add a matching tile to `projects.html`'s grid
6. Add the new files to `tools.html`'s `TOOL_FILES` object so they show up under the right software

## To use it
1. Create a GitHub repo named exactly `yourusername.github.io`
2. Put these files in the repo root (not a subfolder)
3. Settings → Pages → Source: Deploy from branch → `main` → `/root`
4. Site goes live at `https://yourusername.github.io`

## To customize
- **Welcome photo**: add an image to `assets/`, then swap the `.welcome-photo` div in `index.html` for `<img src="assets/photo.jpg" alt="...">`
- **CV download**: add your CV PDF to `assets/CV_AGoshtasbi.pdf` (the link on the Welcome page already points there)
- **Colors/fonts**: CSS variables at the top of `style.css`
- **Research page**: swap the "#" placeholder links for real paper URLs (DOI or publisher page) as you get them
