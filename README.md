# Portfolio site — setup notes

## Folder structure
```
/
├── index.html          → Welcome (homepage, at yoursite.io/)
├── style.css
├── projects/
│   ├── index.html       → Projects gallery (yoursite.io/projects/)
│   ├── gripper.html      → individual project pages
│   ├── bracket.html
│   └── thermal.html
├── tools/
│   └── index.html       → Tools tab (yoursite.io/tools/)
├── research/
│   └── index.html       → Research tab (yoursite.io/research/)
├── about/
│   └── index.html       → About tab (yoursite.io/about/)
└── assets/               → put your photos, CV PDF, etc. here
```

Putting an `index.html` inside each folder gives clean URLs — e.g. `/projects/` instead of `/projects.html` — which is why every tab is a folder with its own `index.html`, except the individual project pages which sit directly inside `/projects/`.

## How links work — root-relative paths
Every internal link and the stylesheet use a **leading slash** (e.g. `/projects/`, `/style.css`), not a relative path. This matters because this repo is a **user site** (`yourusername.github.io`), which is served from the domain root — so `/style.css` always means "style.css at the very top of the site," no matter which folder the current page is in. This is what let us move files into folders without breaking any links.

If you ever rename the repo away from `yourusername.github.io` (making it a **project site** instead, served at `yourusername.github.io/reponame/`), these root-relative links would break — you'd need to switch to relative paths (`../style.css`) or add a base path. Not a concern as long as the repo keeps its current name.

## Nav (same on every page)
Welcome → Projects → Tools → Research → About

## How each project page works
1. **Hero** — concept photo + short pitch
2. **Tab selector** (Overview / CAD / Code / Renders / Simulation) — click to swap sections, no reload
3. **Tools strip** at the bottom — software used for that project

## How the Tools page works
All tool → file mappings live in one place: the `TOOL_FILES` object inside the `<script>` tag at the bottom of `tools/index.html`. Each tool maps to a list of files, each recording its project and a link.

**To add a file**: find the tool's array and add:
```js
{ project: "Project title", projectLink: "/projects/x.html",
  file: "filename.ext", fileLink: "https://github.com/...",
  type: "CAD" | "Code" | "Simulation" | "Render" }
```
**To add a new tool**: add a new key to `TOOL_FILES` — it appears automatically as a pill.

## To add a new project
1. Copy `projects/gripper.html` → rename it (e.g. `projects/drone.html`)
2. Edit: `<title>`, eyebrow label, `<h1>`, hero description
3. Fill in Overview / CAD / Code / Renders / Simulation — remove or note "not applicable" for sections that don't apply
4. Update the tools-strip tags
5. Add a matching tile to `projects/index.html`, linking to `/projects/drone.html`
6. Add its files to `tools/index.html`'s `TOOL_FILES`

## To use it
1. Repo must be named exactly `yourusername.github.io`
2. All these files/folders go in the repo root
3. Settings → Pages → Source: Deploy from branch → `main` → `/ (root)`
4. Site goes live at `https://yourusername.github.io`

## To customize
- **Welcome/About photo**: add to `/assets/`, swap the `.welcome-photo` div for `<img src="/assets/photo.jpg" alt="...">`
- **CV download**: add `/assets/CV_AGoshtasbi.pdf` — both Welcome and About already link to it
- **Colors/fonts**: CSS variables at the top of `style.css`
- **Research page**: swap the `#` placeholder links for real paper URLs as you get them
