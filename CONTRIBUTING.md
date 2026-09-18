# How to make changes to this site (a guide for instructors)

This guide walks through the whole process of editing a help session notebook and getting your change published, assuming you've never used git or GitHub before. Follow the steps in order the first few times -- once it clicks, it takes about a minute of actual work per change.

**Before you start:** see the [README](README.md) for what belongs in this repo and how notebook execution works here.

## One-time setup

You only need to do this once, ever, on a given computer.

1. **Install git.**
   - Mac: open Terminal and type `git --version`. If it's not installed, it'll prompt you to install it -- follow the prompt.
   - Windows: download and install [Git for Windows](https://git-scm.com/download/win). This also gives you "Git Bash," a terminal you'll use for the commands below.
2. **Get a GitHub account** if you don't have one already, at [github.com](https://github.com).
3. **Ask to be added as a collaborator** on `BU-EK125/EK125-hw-help` (whoever manages the repo can add your GitHub username under the repo's Settings → Collaborators). Without this, you won't be able to push changes.
4. **Download ("clone") the repo to your computer.** Open Terminal (or Git Bash on Windows), navigate to wherever you'd like the folder to live (e.g., `cd Documents`), then run:
   ```
   git clone https://github.com/BU-EK125/EK125-hw-help.git
   ```
   This creates a folder called `EK125-hw-help` with a full copy of the repo. You only do this once -- from now on you'll just update this same folder.

## Every time you want to make a change

Think of this as a 5-step recipe: **update → branch → edit → commit/push → open a pull request.**

### 1. Make sure you're starting from the latest version

Open a terminal, move into the repo folder, and pull the latest changes:
```
cd EK125-hw-help
git checkout main
git pull
```

### 2. Create a new branch for your change

A "branch" is just an isolated workspace for one change, so your edits don't collide with anyone else's. Name it something short and descriptive:
```
git checkout -b add-hw3-help-session
```
(Replace `add-hw3-help-session` with whatever describes your change.)

### 3. Make your edit

Open the file in whatever editor you like (VS Code, Jupyter, Colab) and make your change. Notebooks live in `help-sessions/HomeworkN.ipynb`. If you're adding a brand-new page rather than editing an existing one, you'll also need to add one line to `_toc.yml` (see the [README](README.md)).

Just write real, working code in the code cells -- there's no separate "run it and save the outputs" step. The site executes every notebook itself, fresh, every time it builds, so whatever your code actually produces is exactly what gets published. All that matters is that it runs without erroring -- if it doesn't, step 6 below will catch it before your change can merge.

**Want a cell to intentionally raise an error** -- e.g. to show students what a common mistake looks like? Tag that cell `raises-exception`, otherwise the build treats the error as broken code and fails. In Jupyter/JupyterLab: View → Cell Toolbar → Tags, then type `raises-exception` in the tag box that appears at the top of the cell.

**Want a cell skipped entirely** -- e.g. it calls `input()`, or deliberately runs "forever" to demonstrate an infinite loop? Tag that cell `skip-execution` instead, and make sure you save it with the output you want students to see, since the build will leave it untouched rather than re-running it.

Save the file when you're done.

### 4. Save your change to git ("commit") and upload it ("push")

Back in the terminal:
```
git add .
git commit -m "Add Homework 3 help session"
git push -u origin add-hw3-help-session
```
- `git add .` stages every change you made.
- `git commit -m "..."` saves a snapshot with a short description -- replace the text in quotes with a plain-English summary of what you changed.
- `git push ...` uploads your branch to GitHub. The `-u origin add-hw3-help-session` part is only needed the very first time you push this branch; after that, plain `git push` works.

### 5. Open a pull request ("PR")

A pull request is a request to merge your branch into the live site. After you push, GitHub will print a URL in the terminal like:
```
remote: Create a pull request for 'add-hw3-help-session' on GitHub by visiting:
remote:      https://github.com/BU-EK125/EK125-hw-help/pull/new/add-hw3-help-session
```
Open that link in your browser (or go to the repo on github.com -- it'll show a yellow banner offering to create the PR for your recently-pushed branch). Give it a title, optionally a description, and click **Create pull request**.

### 6. Wait for the automatic check, then merge

Every PR automatically runs a check called `pr-check` that rebuilds the whole site -- since that build executes every notebook, this is also where a broken notebook gets caught. You'll see a status at the bottom of the PR page:
- 🟡 Yellow = still running, wait a few minutes.
- ✅ Green = passed. Click **Merge pull request**.
- ❌ Red = something's broken. Click "Details" next to the check to see what failed, fix it (edit the file, then repeat step 4 to push another commit to the same branch -- no need to open a new PR), and it'll re-run automatically.

Once merged, the live site rebuilds and republishes automatically within a few minutes -- no further action needed.

## Cheat sheet

Once you're comfortable, this is the whole thing:
```
git checkout main
git pull
git checkout -b my-branch-name
# ...edit files...
git add .
git commit -m "Describe the change"
git push -u origin my-branch-name
# ...open the PR link GitHub gives you, wait for the green check, click Merge...
```

## Common hiccups

- **"Permission denied" / "403" when pushing:** you're probably not yet added as a collaborator on the repo (see step 3 of setup), or you're not signed into git with the right GitHub account. Try `git config --global user.email` to check which email git thinks you are.
- **"Your branch is behind" or a merge conflict:** someone else's change landed on `main` before yours. Run `git checkout main && git pull`, then from your branch run `git merge main` and resolve any conflicts it flags (or just ask for help -- conflicts are the one part of git that's genuinely easier with a second pair of eyes).
- **You edited a notebook and the check failed:** the site executes the whole notebook when it builds, so this almost always means a cell errors out. Open the "Details" link on the failed check to see which cell and why, fix the code, and push again.
- **Not sure if your change is safe to make directly, or you'd like someone to look before it goes live:** that's exactly what the pull request is for -- it doesn't touch the live site until someone clicks "Merge." Feel free to open it and ask a question in the PR description rather than merging right away.

🤖 Generated with [Claude Code](https://claude.com/claude-code)
