# HumRah Backend — Team aur Git Guide

Repository: https://github.com/Talal8t/backendcollab

HumRah aik carpooling / ride-sharing FYP hai. Frontend **Flutter / Dart** mein hai. Backend ke liye aik **ASP.NET Core Web API project**, aik **SQL Server database** aur **EF Core Database First** ka tareeqa istemal hoga.

## Abhi repository mein kya hai?

- **9 service modules, 30 subservices aur 60 khaali C# placeholder files** maujood hain.
- Architecture, team ownership, manual authentication aur Git workflow ki documentation shamil hai.
- `.gitkeep` sirf khaali folders ko Git mein rakhne ke liye hai; yeh application logic nahi hai.
- Login, signup, rides, matching, booking aur messaging ki feature logic abhi implement nahi hui.
- Asal Visual Studio solution, SQL schema aur ERD abhi supply nahi huay. Is liye restore/build verify nahi hua aur CI build workflow bhi configure nahi hua.

Asal project milne par pehle usay inspect karein. Sirf missing folders add karein; existing code, namespace, generated models aur DbContext ko preserve karein. Doosra C# project ya database migrations na banayein. Authentication manual hogi; ASP.NET Core Identity ya application Admin role shamil nahi hai.

## 1. Pehli dafa Git setup karein

Windows par Git install karein. Commands **PowerShell** ya **Visual Studio Terminal** mein chala sakte hain.

Neeche naam aur email ko apni details se replace karein. GitHub ki verified email ya GitHub Settings wali noreply email istemal kar sakte hain. Yeh commit ki pehchan set karta hai; GitHub login alag hota hai.

```powershell
git --version
git config --global user.name "Apna Naam"
git config --global user.email "apni-email@example.com"
```

Push ke liye apne GitHub account se sign in karein. GitHub Desktop, Visual Studio Git sign-in ya GitHub CLI ka `gh auth login` use kar sakte hain. Public repository clone karna push ki permission nahi deta; owner ko aapka confirmed GitHub username collaborator ke taur par add karna hoga. Token ya password chat, source code ya README mein na likhein.

## 2. Repository clone karein — sirf pehli dafa

```powershell
git clone https://github.com/Talal8t/backendcollab.git
cd backendcollab
git remote -v
git branch -a
```

- `clone` repository ki files aur history aapke computer par lata hai.
- `cd` repository ke folder mein le jata hai.
- `remote -v` mein fetch aur push ke liye backendcollab ka URL nazar aana chahiye.
- `branch -a` local aur remote branches dikhata hai.

Agli dafa dobara clone na karein; isi folder ko khol kar changes pull karein. Agar pehle se kisi aur folder mein clone ki hui hai to usi folder mein kaam karein.

## 3. Apna task aur feature branch chunain

`main` team ka combined code hai. Har developer apni feature branch par kaam karega.

| Developer | Shuruati feature branch |
|---|---|
| Hamid | `feature/hamid-profile-contacts` |
| Talal | `feature/talal-manual-auth` |
| Tayyab | `feature/tayyab-rides-matching` |
| Ehtisam | `feature/ehtisam-booking-groups` |

Yeh branches ka naming plan hai; table mein naam hone ka matlab yeh nahi ke branch pehle se bani hui hai. Branch ka naam GitHub permission bhi nahi deta. Baad mein har chhotay feature ke liye alag naam rakhein, jaise `feature/talal-login` ya `feature/hamid-preferences`.

Kaam shuru karne se pehle GitHub Issue claim karein aur team ownership document dekhein. Shared DTOs, Program.cs, DbContext, database schema aur package settings mein tabdeeli owner ke saath discuss karein.

## 4. Kaam shuru karne se pehle main update karein

```powershell
git status
git fetch origin --prune
git switch main
git pull --ff-only origin main
git switch -c feature/talal-login
```

`feature/talal-login` aik misaal hai; apne task ke mutabiq branch ka naam rakhein. Yeh commands Login implementation shuru karne ki approval nahi hain; feature coding alag task mein hogi.

- `status` aapki changed aur staged files dikhata hai. Branch badalne se pehle adhoora kaam apni current branch par commit karein ya samajh kar stash karein.
- `fetch` remote ki nayi history lata hai, lekin working files nahi badalta. `--prune` deleted remote branches ke purane tracking references hata deta hai.
- `switch main` local main branch par le jata hai.
- `pull --ff-only` main ko remote main ke saath update karta hai. Agar fail ho to divergence owner ke saath check karein; force push ya reset se kaam na mitayein.
- `switch -c` nayi branch banata hai aur us par le jata hai. Agar branch pehle se local hai to `git switch feature/talal-login` use karein.

## 5. Apni files commit aur push karein

Changes karne aur relevant checks chalane ke baad:

```powershell
git status
git diff
git add -- "fyp_humrah/Services/Authentication/Login/"
git diff --cached
git commit -m "feat(auth): implement manual login"
git push -u origin feature/talal-login
```

Upar ka path aur commit message sirf misaal hain. Apni asal changed files/folders ke paths add karein, jin mein zaroorat ke mutabiq repository, business rules, service, controller aur tests bhi shamil hon. Jis feature par kaam nahi hua uska implementation commit na banayein.

- `diff` unstaged changes dikhata hai.
- `add` sirf chunay huay changes stage karta hai. Baghair review ke `git add .` na chalayein.
- `diff --cached` se check karein ke commit mein kya ja raha hai.
- `commit` changes ko local history mein save karta hai; yeh abhi GitHub par upload nahi karta.
- `push -u` branch GitHub par upload karta hai aur uska upstream set karta hai. Isi branch ki agli pushes ke liye `git push` kaafi hai.

Agar koi change nahi hai to commit ki zaroorat nahi. Asal backend project aane tak build pass hone ka dawa na karein.

## 6. GitHub par Pull Request (PR) banayein

1. [Pull requests](https://github.com/Talal8t/backendcollab/pulls) kholein aur **New pull request** par click karein.
2. **base: main** aur **compare: apni feature branch** select karein.
3. Title mein feature ka naam aur description mein changes, testing aur pending cheezen likhein.
4. Related Issue link karein. `Closes #123` sirf tab likhein jab PR merge hone par woh Issue close hona chahiye.
5. **Talal8t** se review mangain. Owner **Files changed**, comments aur available **Checks** dekhega.
6. Agar changes mangay jayein to usi feature branch mein edit, commit aur push karein. PR khud update ho jayega; naya PR banane ki zaroorat nahi.
7. Review aur zaroori checks ke baad **sirf owner Talal8t merge karega**. Baqi developers main par seedha push ya PR merge na karein.

**Pull aur Pull Request alag cheezen hain:** `git pull` remote changes aapke computer par lata hai. PR aapki feature branch ko main mein shamil karne ki review request hoti hai. `git push` apne aap main mein merge nahi karta.

## 7. Team ka naya kaam apni chalti feature branch mein laayein

Pehle working tree clean karein. Phir apni feature branch par:

```powershell
git switch feature/talal-login
git fetch origin
git merge origin/main
```

Is se main ka naya kaam aapki feature branch mein aa jayega. Agar merge theek ho jaye to relevant checks chala kar `git push` karein. Sirf local main update karne se feature branch update nahi hoti.

### Agar merge conflict aa jaye

1. `git status` se conflict wali files dekhein.
2. Files khol kar dono taraf ka kaam samjhein aur sahi changes rakhein. `<<<<<<<`, `=======` aur `>>>>>>>` markers hata dein.
3. Resolved files ko unke asal paths ke saath `git add -- "file-ka-path"` se stage karein. Is example path ko apni file se replace karein.
4. `git diff --cached` review karein aur `git commit` se merge complete karein.
5. Relevant checks chalayein, phir `git push` karein.

Agar unresolved merge radd karna ho to:

```powershell
git merge --abort
```

Agar sahi resolution samajh na aaye to feature owner se baat karein. Doosray developer ka code andazay se delete na karein. Shared branch ko rebase karke force push na karein.

## 8. Apna PR merge hone ke baad

```powershell
git switch main
git pull --ff-only origin main
git switch -c feature/talal-signup
```

Ab naya task updated main se shuru hoga. Apne aglay task ka branch name use karein. Pehle se merged feature branch ko naye unrelated kaam ke liye reuse na karein.

## 9. Pehle se bani remote branch kholna

```powershell
git fetch origin --prune
git branch -r
git switch --track origin/feature/talal-login
```

Aakhri command tab chalegi jab remote branch maujood ho aur isi naam ki local branch na ho. Agar local branch pehle se hai to `git switch feature/talal-login` karein. Doosray developer ki branch par changes karne se pehle us se coordinate karein.

## Team ke zaroori rules

- Main par seedha push ya force push na karein; har feature ki branch aur PR banayein.
- `.vs/`, `bin/`, `obj/`, `.env`, passwords, connection-string secrets, CNIC/driver documents aur local database backups commit na karein. `.gitignore` pehle se tracked secret ko nahi hatata; diff zaroor dekhein.
- Har shakhs apni assigned features par kaam kare aur shared contracts pehle agree kare.
- Daily chhoti update dein: kya complete hua, agla kaam kya hai aur blocker kya hai.
- Owner ka merge karna abhi team policy hai. Pichli API verification mein **main unprotected tha aur effective branch rules nahi thay**; owner-only merging technically enforce nahi thi. README likhne se permissions enforce nahi hoti. Owner GitHub **Settings → Rules → Rulesets / Branches** mein available protection controls configure aur verify kare. Tafseel Git workflow document mein hai.

## Mazeed documentation

- [Architecture aur project decisions](fyp_humrah/Docs/ARCHITECTURE.md)
- [Team ownership aur estimates](fyp_humrah/Docs/TEAM_OWNERSHIP.md)
- [Detailed Git workflow aur branch protection](fyp_humrah/Docs/GIT_WORKFLOW.md)
- [Manual authentication design](fyp_humrah/Docs/MANUAL_AUTH_DESIGN.md)
- [Database First, packages aur build handoff](fyp_humrah/Docs/DATABASE_FIRST_NOTES.md)

Agla backend qadam: asal project aur schema inspect/integrate karein, compatible SDK/packages verify karke restore/build chalayein, phir dbo.User aur manual-auth design review ke baad approved Login task shuru karein.
