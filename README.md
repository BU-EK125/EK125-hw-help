## For instructors: How to modify this jupyter book

This site is a public, permanent companion to the main [EK125 site](https://github.com/BU-EK125/EK125) -- it stays up and accessible indefinitely, not just for the current semester. It collects homework help session notebooks: worked walkthroughs of the problem-solving approach for that week's homework.

Every notebook is an executable Jupyter notebook (`.ipynb`). The site executes every notebook fresh every time it builds (`execute_notebooks: force` in `_config.yml`) -- you never need to run a notebook yourself or save it with outputs baked in. Whatever your code actually produces when it runs is exactly what gets published. This also means a notebook whose code no longer runs will fail the build outright, which is exactly what the `pr-check` below catches before a broken notebook can reach `main`.

**Want a cell to intentionally raise an error** (e.g. demonstrating a common mistake)? Tag that cell `raises-exception`, or the build will treat the error as broken code and fail. In Jupyter/JupyterLab: View → Cell Toolbar → Tags, then type `raises-exception` into the tag box for that cell.

**Want a cell skipped entirely at build time** (e.g. it calls `input()`, which can't run in an automated build, or it deliberately runs "forever" to demonstrate an infinite loop)? Tag that cell `skip-execution` instead -- the build will leave whatever output is already saved in that cell untouched rather than trying to re-run it, so make sure you save it with the output you want shown.

**Want the 🚀 "open in Colab" rocket icon on a page?** It's automatic for every notebook here -- `launch_buttons`/`repository` are already configured in `_config.yml` for the whole book. It only requires the file to actually be merged into `main` at its final path; the rocket button links straight to GitHub's `main` branch, so it 404s for anything still sitting in an unmerged PR.

**To add or modify a help session notebook:**

1. Create or edit the file at `help-sessions/HomeworkN.ipynb`. Just write real, working code -- there's nothing extra to do before saving; the site runs it for you at build time.
2. If you're adding a new page, add one line to `_toc.yml` following the existing pattern.
3. Open a pull request with your change rather than pushing directly to `main`. A GitHub Actions check (`pr-check`) runs automatically on every PR and builds the whole book -- since that build executes every notebook, any notebook whose code doesn't run cleanly will fail the check. Fix anything it flags before merging.
4. Once the PR is merged, GitHub Actions rebuilds and republishes the live site automatically -- no manual steps needed.

## https://BU-EK125.github.io/EK125-hw-help/intro.html
