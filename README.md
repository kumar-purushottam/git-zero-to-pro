# Git Zero to Pro

A free course website that teaches Git and GitHub, from your first commit to handling
branches in a real team.

**Live site:** https://kumar-purushottam.github.io/git-zero-to-pro/

The site is also the practice project. Every lesson is written on its own branch, reviewed
in a pull request, and merged into `main`. GitHub Pages publishes only `main`, so a lesson
appears on the live site only after it is merged.

## Run it locally

No build step and no dependencies. Open `index.html` in a browser:

```bash
xdg-open index.html        # Linux
open index.html            # macOS
```

## Project structure

```
├── index.html               # home page: roadmap + how the site is built
├── CONTRIBUTING.md          # rules every contributor follows
├── CHANGELOG.md             # one line per merged PR
├── .github/
│   └── pull_request_template.md
├── assets/
│   ├── css/style.css        # shared styles (main only)
│   ├── js/modules.js        # module registry: titles, levels, status
│   ├── js/main.js           # shared behavior (main only)
│   └── img/                 # images, prefixed by module number
└── modules/
    ├── _template.html       # every module page starts from this
    └── NN-slug.html         # one file per module
```

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md). In short: branch off `main`, build one module,
open a pull request, and wait for review.
