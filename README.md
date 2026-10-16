# study

My personal sandbox for learning **Git** and **GitHub** — the place where I break things on purpose, so I don't break them by accident in real projects.

---

## Why this repo exists

I'm new to Git and GitHub. Instead of reading docs and hoping it sticks, I use this repo to actually practice:

- Make commits, branches, and merges until they feel boring.
- Open pull requests against my own `main` branch.
- Get comfortable being lost — then use `git reflog` to find my way back.
- Learn what each command really does, not just what to type.

Rule for this repo: **nothing here is precious.** If I need to test `git reset --hard`, this is where I test it.

---

## Learning roadmap

Basics first, then the parts that scare people.

**Level 1 — The everyday loop**

- [x] Create a repository, write a README
- [x] `git add` / `git commit` / `git status` / `git log`
- [x] Connect a local repo to GitHub with `git remote`
- [ ] Understand the three areas: working directory → staging area → repository
- [ ] Write a proper `.gitignore`
- [ ] Commit with a message that future-me will understand

**Level 2 — Branching**

- [ ] Create and switch branches (`git switch -c`)
- [ ] Merge a branch into `main`
- [ ] Resolve a merge conflict on purpose
- [ ] Delete merged branches
- [ ] Know when to rebase instead of merge (and when not to)

**Level 3 — Working with GitHub**

- [ ] Push a branch and open a pull request
- [ ] Review my own PR and merge it on GitHub
- [ ] Keep a fork in sync with the upstream repo
- [ ] Open an issue, close it with a commit message (`Closes #1`)
- [ ] Read a PR diff and leave a comment

**Level 4 — Fixing mistakes**

- [ ] Unstage a file without losing changes (`git restore --staged`)
- [ ] Amend the last commit
- [ ] Undo a commit three ways: `reset --soft`, `revert`, `reset --hard`
- [ ] Recover a "lost" commit with `git reflog`
- [ ] Stash work, switch branches, come back (`git stash pop`)
- [ ] Find the commit that broke something (`git bisect`)

**Level 5 — Habits of people who aren't scared of Git**

- [ ] Keep commits small and focused
- [ ] Pull with `--rebase` to keep history readable
- [ ] Never commit secrets (and know how to clean up if I do)
- [ ] Tag releases

---

## Cheat sheet

The commands I actually reach for, in the order I learned them.

### One-time setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global pull.rebase true      # rebase instead of merge on pull
git config --global core.editor "vim"     # or nano, or code --wait
```

### The everyday loop

```bash
git status                     # what changed, what's staged
git diff                       # unstaged changes
git diff --staged              # staged changes (what will be committed)
git add <file>                 # stage one file
git add -p                     # stage part of a file, hunk by hunk — very useful
git commit -m "message"        # commit
git log --oneline --graph --decorate --all
```

### Undo (safe → dangerous)

```bash
git restore <file>             # discard changes in the working directory  ⚠️ permanent
git restore --staged <file>    # unstage, keep the changes
git commit --amend             # fix the last commit message or contents
git reset --soft HEAD~1        # undo last commit, keep changes staged
git reset --hard HEAD~1        # undo last commit AND delete the changes  ⚠️⚠️ permanent
git revert <sha>               # make a new commit that undoes an old one (safe on shared branches)
git reflog                     # the escape hatch — shows every place HEAD has been
```

> If I lost something, `git reflog` first. Almost nothing is truly gone until it's garbage-collected.

### Branches and merges

```bash
git switch -c feature/name     # create and switch
git switch main                # switch back
git branch -a                  # list local + remote branches
git merge feature/name         # merge into the current branch
git rebase main                # replay my commits on top of main (cleaner history)
git branch -d feature/name     # delete a merged branch
```

### Working with GitHub

```bash
git remote -v                          # where does this repo point
git remote add origin <url>            # connect to a remote
git push -u origin <branch>            # push and remember the upstream
git fetch --prune                      # see what changed on the remote, clean stale refs
git pull --rebase                      # get remote changes without a merge commit
```

GitHub CLI (`gh`) — faster than clicking around:

```bash
gh auth login
gh repo create
gh pr create --fill --base main
gh pr list
gh issue list
gh pr checkout 3
```

### Stashing

```bash
git stash                      # set work aside
git stash list                 # see what's stashed
git stash pop                  # bring it back (and drop the stash entry)
git stash apply                # bring it back (keep the stash entry)
git stash push -m "wip: X"     # stash with a name, easier to find later
```

---

## Conventions I'm trying to build

- **Commit messages:** start with a verb, imperative mood — `Add`, `Fix`, `Update`, `Remove`. Not `Added` or `Adds`.
- **One idea per commit.** If I need the word "and" in the subject, it's probably two commits.
- **Branch names:** `type/short-description` — e.g. `docs/readme`, `practice/merge-conflict`.
- **`main` stays working.** Experiments happen on branches, and they get merged only when they make sense.
- **Never commit** credentials, API keys, `.env` files, or anything I'd be embarrassed to see public.

---

## Journal

What I did, and what surprised me.

| Date       | What I practiced                                    | Notes                                                               |
| ---------- | --------------------------------------------------- | ------------------------------------------------------------------- |
| 2026-10-16 | Created the repo, first commit, wrote a real README | Pushing the first time was the hard part — the rest was just typing |

---

## Resources worth the time

- [Pro Git book](https://git-scm.com/book/en/v2) — free, and the branching chapter is the best explanation anywhere
- [GitHub Docs](https://docs.github.com/en) — the actual reference
- [Learn Git Branching](https://learngitbranching.js.org/) — interactive, and the only thing that made rebase click for me
- [Oh Shit, Git!?!](https://ohshitgit.com/) — what to do when it goes wrong
- [Conventional Commits](https://www.conventionalcommits.org/) — a stricter message convention, for later

---

## License

This is a personal learning repo. There's no code worth reusing here — take the README structure if it helps.
