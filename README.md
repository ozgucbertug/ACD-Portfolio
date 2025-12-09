# ACD-E25 Portfolio Template

Use this repo to publish your final portfolio submission as a GitHub Pages site. Each assignment folder (`A1`–`A4`) is pre-wired with the front matter Pages needs; you fill in the content.

## Publish with GitHub Pages
2. In GitHub: **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to “Deploy from a branch”, choose `main`, folder `/ (root)`, and save.
4. Wait for the build to finish; your site will appear at `https://<username>.github.io/<repo-name>/`.


## How to use the template
- Update each assignment folder’s content (code, images, write-up) following the structure above.
- Do **not** change the front matter in `A*/index.md`, `A*/README.md`, or `A*/BRIEF.md`; Pages depends on it for navigation.
- Remove all placeholder text in assignment `README.md` files. Document thoroughly: describe your approach, include diagrams/figures, show intermediary outputs, and present final results with explanations.
- Save visual assets in the `images/` folder with descriptive filenames (e.g., `heightmap-variation-1.png`, `agent-paths-final.png`) and embed them in the corresponding assignment `README.md`.
- This root `README.md` is your landing page. Replace this text with your final design and overview—structure and style are up to you.
- How Pages uses your files: each assignment `README.md` renders as the **Project Documentation** page; each `BRIEF.md` renders as the **Assignment Brief**. The `index.md` files handle nav/redirects—leave their front matter intact.

After each push, GitHub Pages will rebuild automatically (give it a few minutes). Your site will update once the build completes.

## Expected repo structure
```
README.md                  # This file
_config.yml
index.md
A1/
├── index.md               # Do not edit front matter or content
├── BRIEF.md               # Assignment brief; Do not edit front matter or content
├── README.md              # Project documentation; Keep front matter, replace the rest with your project documentation
├── images/                # Add diagram, intermediary, and final images here
└── ...                    # Assignment code/scripts; as defined in each assignment brief.
A2/
├── index.md
├── BRIEF.md
├── README.md
├── images/
└── ...
A3/
├── index.md
├── BRIEF.md
├── README.md
├── images/
└── ...
A4/
├── index.md
├── BRIEF.md
├── README.md
├── images/
└── ...
```
