# Contributing to Git Zero to Pro

This project is built the way a real team builds software. There is one **main model**
(the maintainer) and several **contributor models**. Each contributor builds one module on
its own branch and opens a pull request. The main model reviews and merges it.

Read this whole file before you write anything.

---

## 1. Roles

| Role | Can do | Cannot do |
|------|--------|-----------|
| **Main model** (maintainer) | Owns shared files, reviews PRs, merges into `main` | Merge a PR that breaks these rules |
| **Contributor model** | Builds one module on its own branch, opens a PR | Push to `main`, edit shared files |

## 2. File ownership

| File / folder | Owner | Contributors may… |
|---------------|-------|-------------------|
| `index.html` | main | not edit |
| `assets/css/style.css` | main | not edit |
| `assets/js/main.js` | main | not edit |
| `modules/_template.html` | main | copy it, never edit it |
| `README.md`, `CONTRIBUTING.md` | main | not edit |
| `assets/js/modules.js` | main | flip **only their own** `status` line from `"soon"` to `"ready"` |
| `CHANGELOG.md` | shared | add **one** line for their PR |
| `modules/NN-slug.html` | contributor | create and edit freely |
| `assets/img/NN-*` | contributor | create and edit freely |

Need a change to a shared file (a new CSS style, for example)? **Do not make it yourself.**
Ask for it under "Requests for main" in your PR description. The main model will make it
on its own `style/...` or `fix/...` branch.

## 3. Branches

- `main` must always work. **Nobody pushes to `main` directly.** Everything arrives through a PR.
- One module = one branch = one PR.
- Branch names:

| Prefix | Use for | Example |
|--------|---------|---------|
| `module/` | a new module page | `module/06-branching` |
| `fix/` | fixing a bug or a typo | `fix/07-broken-link` |
| `style/` | shared CSS/JS changes (main only) | `style/table-styles` |
| `docs/` | README / CONTRIBUTING changes | `docs/pr-checklist` |

The exact branch name for every module is listed in `assets/js/modules.js`
(`module/` + the module's `slug`).

## 4. Commit messages

Use [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <what changed, in the imperative>

feat(module-06): add branching basics page
fix(module-06): correct switch command in lab step 3
docs(changelog): add module 06 entry
style(css): add table styles
```

Types: `feat`, `fix`, `docs`, `style`, `chore`. Keep commits small. One logical change per commit.

## 5. Contributor workflow, step by step

```bash
# 1. Start from an up-to-date main
git switch main
git pull origin main

# 2. Create your branch
git switch -c module/NN-slug

# 3. Create your page from the template
cp modules/_template.html modules/NN-slug.html
#    ...write the module...

# 4. Commit as you go
git add modules/NN-slug.html
git commit -m "feat(module-NN): add <topic> page"

# 5. Mark it ready + add a changelog line
#    - modules.js: status "soon" -> "ready" (your entry only)
#    - CHANGELOG.md: add one line at the TOP of the "Unreleased" list
git add assets/js/modules.js CHANGELOG.md
git commit -m "docs(module-NN): mark ready and update changelog"

# 6. Before opening the PR, bring in anything new from main
git fetch origin
git merge origin/main          # resolve conflicts if any, then commit

# 7. Push and open the PR
git push -u origin module/NN-slug
gh pr create --base main --fill
```

## 6. Module page rules

Every module page **must** have these sections, in this order, using the ids and classes from
`modules/_template.html`:

1. Header: `.eyebrow[data-auto]` (auto-filled), `h1`, `.lead`
2. `#goals`: 3–5 learning goals
3. `#concept`: plain-language explanation and at least one `pre.graph` or diagram
4. `#commands`: every command in a `pre.cmd`, each with a one-line explanation
5. `#lab`: numbered steps in `ol.steps`, run in `~/git-playground` (never in a real project)
6. `#scenario`: an "At work" story from a real team
7. `#mistakes`: 2–4 `.mistake` blocks, each with a `.bad` and a `.fix`
8. `#quiz`: exactly 3 `<details>` questions
9. `#summary`: 3–5 bullets

Also:
- Use **simple English**. Short sentences. Explain every new word the first time.
- No `<style>` tags, no inline `style=""`, no extra CSS or JS files.
- No external libraries, fonts or images from other sites.
- `body` must have `data-root=".."` and `data-module="NN"`.
- Commands must be copy-paste safe: no `$ ` prompt prefix in `pre.cmd`.

## 7. Pull request checklist

Your PR description must tick every box (the PR template includes it):

- [ ] Branch is named `module/NN-slug`
- [ ] Only my own files changed (plus my `modules.js` status line and one `CHANGELOG.md` line)
- [ ] All 9 sections are present and in order
- [ ] Every command was checked to be correct
- [ ] Page opened in a browser in light **and** dark mode
- [ ] Prev / next links and the sidebar work
- [ ] Branch is up to date with `main` (no conflicts)

## 8. Review and merge (main model)

1. Read the diff: `gh pr diff <number>`
2. Check the rules above. If something is wrong: `gh pr review <number> --request-changes -b "..."`
3. When it's right: `gh pr merge <number> --merge --delete-branch`
4. GitHub Pages redeploys `main` automatically. The module is now live.

We use **merge commits** (not squash) on purpose, so the branch history stays visible in
`git log --graph`. That's useful while you're learning.
