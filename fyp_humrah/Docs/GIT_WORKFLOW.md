# Working together on HumRah

Repository: https://github.com/Talal8t/backendcollab

Owner and designated sole merger: **Talal8t**. Hamid, Talal, Tayyab and Ehtisam contribute through feature branches and pull requests (PRs). Their GitHub usernames must be confirmed before invitations or assignments.

## Repository setup and scope

The repository was verified public and empty before the initial scaffold upload.
`main` is the default branch. The connected Talal8t account has write/admin access.
The first scaffold upload is the initial-history exception; all later work uses
feature branches and PRs. Existing history must never be replaced or force-pushed.

The scaffold has 9 service modules, 30 subservices and 60 empty C# files. The
existing Visual Studio solution, SQL schema and ERD still need to be supplied and
inspected. No project, SDK or package versions were invented, and no backend
build has been verified. Keep `.github` at the repository root. Merge only missing
folders into the real single project, preserving existing source and models.

Main protection and owner-only merge enforcement remain unconfigured/unverified.
No collaborator invitations were sent. The owner setup section below explains
the required checks; documentation alone does not enforce permissions.

## Developers: clone once

Install Git for Windows. Use PowerShell or the Visual Studio terminal:

```powershell
git clone https://github.com/Talal8t/backendcollab.git
cd backendcollab
git remote -v
git branch -a
```

`clone` downloads files/history. `remote -v` should show the backendcollab URL for fetch and push. `branch -a` lists local and remote branches. Reading a public repo does not grant write access: the owner must invite each confirmed account with the minimum necessary permissions.

## Start a feature

Start with a clean working tree. Commit unfinished work on its current branch, or intentionally stash it, before switching.

```powershell
git status
git fetch origin --prune
git switch main
git pull --ff-only origin main
git switch -c feature/talal-login
```

`fetch` downloads history without changing working files; `--prune` removes obsolete remote-tracking refs. `pull --ff-only` advances main without a merge; if it fails, inspect the divergence with the owner. `switch -c` creates a feature branch from updated main.

| Developer | Initial ownership branch |
|---|---|
| Hamid | `feature/hamid-profile-contacts` |
| Talal | `feature/talal-manual-auth` |
| Tayyab | `feature/tayyab-rides-matching` |
| Ehtisam | `feature/ehtisam-booking-groups` |

Use narrower names such as `feature/talal-login` for later increments. Branch names identify work; they do not grant access. Claim an Issue and agree shared contracts before coding.

## Save and push changes

Stage only reviewed paths. This example assumes Login files were changed; substitute the paths you actually changed, including associated feature-layer files.

```powershell
git status
git diff
git add -- "fyp_humrah/Services/Authentication/Login/"
git diff --cached
git commit -m "feat(auth): implement manual login"
git push -u origin feature/talal-login
```

`add` stages selected changes; `diff --cached` shows the exact staged content. `commit` records it locally. `push -u` uploads the branch and remembers its upstream; later pushes can use `git push`. If nothing changed there is nothing to commit. Run the real project's checks when available; do not claim this skeleton builds.

Never commit `.vs/`, `bin/`, `obj/`, `.env`, secret-bearing appsettings, SQL credentials, local databases/backups, CNIC media or driver documents. Inspect the diff: `.gitignore` does not remove secrets already tracked.

## Open, review and merge a PR

1. Open https://github.com/Talal8t/backendcollab/pulls and select **New pull request**.
2. Set **base: main** and **compare: your feature branch**.
3. Describe the change and actual validation. Link an Issue using `Closes #123` only when it should close on merge.
4. Request Talal8t's review. Review **Files changed**, comments and **Checks**. Address requested changes on the same branch and push; the PR updates.
5. Talal8t merges after required reviews/checks pass. Other contributors do not merge, bypass checks or push directly to main.

This is team policy; technical enforcement requires the configuration below. There is no backend build check until the existing solution and matching SDK are integrated.

## Get merged work into your current feature

With a clean working tree:

```powershell
git switch feature/talal-login
git fetch origin
git merge origin/main
```

For conflicts: inspect `git status`, edit files to retain the intended work, remove conflict markers, stage resolved files and complete the merge with `git commit`. Run checks and `git push`. `git merge --abort` abandons an unresolved merge. Ask the relevant owner when resolution is unclear. The team merges main into shared feature branches; do not rebase and force-push shared history.

After the owner merges your PR:

```powershell
git switch main
git pull --ff-only origin main
git switch -c feature/talal-signup
```

To discover and follow an authorized remote branch:

```powershell
git fetch origin --prune
git branch -r
git switch --track origin/feature/talal-login
```

The last command requires that remote branch to exist and no local branch with the same name. For an existing local branch use `git switch feature/talal-login`.

## Owner: configure and verify main protection

Open **Settings → Rules → Rulesets**, or **Settings → Branches** for classic protection. Available controls depend on ownership and GitHub plan; inspect them before claiming enforcement.

- Target main; require PRs and a real successful build check once CI exists.
- Require eligible review where supported. The PR author cannot approve their own PR: owner-authored PRs need another eligible reviewer if approval is required.
- Block force pushes/deletion; avoid collaborator administrator or bypass access.
- Owner-only merging requires a supported restriction on updates to main that permits only the designated owner to merge. Requiring PRs or using CODEOWNERS alone does not restrict the merger. Broad bypass settings can also bypass reviews/CI; verify their scope.
- Inspect effective rules and test that a non-owner cannot merge/update main while still able to push feature branches and open PRs. Verify the owner's PR merge observes the intended checks and reviews.

If this repository configuration cannot enforce sole merge authority, record the gap and adopt a supported ownership/plan configuration or explicitly retain a manual policy. No enforcement is claimed here.

Official references:

- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets
- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets
- https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule

## Task tracking

Use one Issue per coherent feature, labels for feature areas and confirmed usernames as assignees. Report completed work, next step and blockers daily. Review changes to shared Program.cs, DbContext, schema, project/package settings, DTOs and cross-cutting contracts with the owner.
