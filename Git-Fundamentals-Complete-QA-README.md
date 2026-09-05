# 🚀 Git Fundamentals — Complete Interview + Practical Q&A
## 👨‍💻 Senior DevOps Engineer Style | Hindi First → English → Commands → Production Mindset

> **🎯 Goal:** Git को सिर्फ commands की list की तरह नहीं, बल्कि एक **real DevOps Engineer** की तरह समझना।
>
> **Learning Flow:**  
> `Concept → आसान हिन्दी → English → Command → Output → Production Example → Interview Q&A → Common Confusion → Hands-on`

---

# 🧭 Git सीखने का Roadmap

```text
Git Basics
   ↓
Repository & Working Tree
   ↓
Add / Commit / Status / Log
   ↓
Branching
   ↓
Merge
   ↓
Rebase
   ↓
Remote Repository
   ↓
Fetch / Pull / Push
   ↓
Pull Request
   ↓
Conflict Resolution
   ↓
Undo / Reset / Revert
   ↓
Stash
   ↓
Tags
   ↓
Cherry-pick
   ↓
Git Ignore
   ↓
Git Hooks
   ↓
Git Security
   ↓
Git in CI/CD
   ↓
Production Git Workflow
```

---

# 🟢 1. Git क्या है?

### आसान हिन्दी

Git एक **Distributed Version Control System (DVCS)** है।

सरल भाषा में:

> Git आपके code की **history book** है। 📖

आपने आज code बदला, कल दूसरा change किया, फिर कुछ टूट गया — Git बता सकता है कि **क्या बदला, कब बदला और किस commit में बदला**।

### English

Git is a distributed version control system used to track changes in files and collaborate safely across teams.

### याद रखने की Trick

> **Git = Code + History + Collaboration + Recovery**

---

# 🟢 2. Git और GitHub में क्या difference है?

| Git | GitHub |
|---|---|
| Version control tool | Git hosting/collaboration platform |
| Local machine पर चलता है | Cloud platform है |
| Repository locally manage करता है | Remote repositories host करता है |
| CLI से काम कर सकते हैं | PR, Issues, Actions आदि देता है |

### 😂 DevOps याद रखने वाली लाइन

> **Git engine है, GitHub parking + collaboration space है. 🚗**

---

# 🟢 3. Git क्यों जरूरी है?

Git से आप:

- Code history maintain कर सकते हैं
- Multiple developers के साथ काम कर सकते हैं
- Branch बना सकते हैं
- Changes review कर सकते हैं
- गलती होने पर recovery कर सकते हैं
- CI/CD trigger कर सकते हैं
- Release/tag manage कर सकते हैं

---

# 🟢 4. Git install कैसे check करें?

```bash
git --version
```

Example:

```text
git version 2.x.x
```

> Exact version आपके installed Git version पर depend करेगी।

---

# 🟢 5. Git की basic configuration

```bash
git config --global user.name "Pradip Gavhankar"
git config --global user.email "your-email@example.com"
```

Check:

```bash
git config --global --list
```

### Production Tip

Commit identity सही configure करें। Shared machine पर blindly `--global` configuration बदलने से पहले scope समझें।

---

# 🟢 6. Git repository क्या है?

Repository यानी वह जगह जहाँ Git आपकी project history track करता है।

```text
my-project/
├── .git/
├── app/
├── README.md
└── main.tf
```

`.git` directory Git की internal database/history रखती है।

---

# 🟢 7. `git init` क्या करता है?

```bash
mkdir my-project
cd my-project
git init
```

यह current directory को Git repository बना देता है।

Expected output installation/version के अनुसार थोड़ा अलग हो सकता है।

---

# 🟢 8. Working Directory, Staging Area और Repository क्या हैं?

सबसे important Git concept:

```text
Working Directory
      ↓ git add
Staging Area
      ↓ git commit
Local Repository
      ↓ git push
Remote Repository
```

### आसान हिन्दी

- **Working Directory:** आपने अभी files बदली हैं
- **Staging Area:** commit के लिए changes चुने हैं
- **Local Repository:** commit history
- **Remote Repository:** GitHub/GitLab/Azure Repos जैसी remote location

### Golden Trick

> **Edit → Add → Commit → Push**

---

# 🟢 9. `git status` क्या करता है?

```bash
git status
```

यह बताता है:

- कौन-सी files modified हैं
- कौन-सी staged हैं
- कौन-सी untracked हैं
- current branch क्या है

### Daily DevOps Command

```bash
git status
```

इसे लगभग हर Git operation से पहले/बाद चलाना useful है।

---

# 🟢 10. `git add` क्या करता है?

```bash
git add main.tf
```

या:

```bash
git add .
```

यह changes को **staging area** में भेजता है।

> ⚠️ `git add` commit नहीं करता।

---

# 🟢 11. `git commit` क्या करता है?

```bash
git commit -m "Add Terraform resource"
```

यह staged changes को local Git history में save करता है।

### याद रखें

```text
git add     = क्या save करना है चुनो
git commit  = history में snapshot बनाओ
```

---

# 🟢 12. `git log` क्या करता है?

```bash
git log
```

Short version:

```bash
git log --oneline
```

Useful:

```bash
git log --oneline --graph --decorate --all
```

Example:

```text
a12bc34 Add AKS module
8de91fa Update README
42ab781 Initial commit
```

---

# 🟢 13. Commit क्या है?

Commit आपके project की एक **versioned snapshot** है।

हर commit का unique identifier होता है जिसे आमतौर पर commit hash कहते हैं।

```text
A → B → C → D
```

हर point एक commit हो सकता है।

---

# 🟢 14. Good commit message कैसी होनी चाहिए?

❌ Bad:

```bash
git commit -m "changes"
```

❌ Bad:

```bash
git commit -m "final"
```

✅ Better:

```bash
git commit -m "Add Azure resource group module"
```

✅ Better:

```bash
git commit -m "Fix GitHub Actions Terraform validation"
```

### Production Rule

Commit message ऐसा लिखें कि 3 महीने बाद भी आपको समझ आए कि change क्यों किया था।

---

# 🟢 15. Untracked, Modified और Staged क्या हैं?

| State | Meaning |
|---|---|
| Untracked | Git अभी file track नहीं कर रहा |
| Modified | Tracked file बदल गई |
| Staged | Next commit के लिए selected |
| Committed | Local history में save |

---

# 🟢 16. `.gitignore` क्या है?

`.gitignore` उन files को Git tracking से exclude करने के लिए है जिन्हें repository में नहीं रखना चाहिए।

Terraform example:

```gitignore
.terraform/
*.tfstate
*.tfstate.*
crash.log
```

Common examples:

```gitignore
.env
node_modules/
*.log
.vscode/
```

### 🚨 Security

`.gitignore` secret को **secret नहीं बनाता**। अगर secret पहले ही commit हो गया है, तो केवल `.gitignore` जोड़ना पर्याप्त नहीं है।

---

# 🟢 17. Git branch क्या है?

Branch development की अलग line है।

```text
main
 |
 A---B---C
          \
           D---E   feature/login
```

Example:

```bash
git branch feature/login
git switch feature/login
```

या:

```bash
git switch -c feature/login
```

---

# 🟢 18. `git switch` और `git checkout` में क्या difference है?

Modern Git में branch switching के लिए:

```bash
git switch feature/login
```

नई branch:

```bash
git switch -c feature/login
```

`git checkout` पुराना multi-purpose command है और files restore करने जैसे काम भी करता है।

```bash
git checkout feature/login
```

### Beginner Recommendation

> Branch work के लिए `git switch` और file restore के लिए `git restore` समझना cleaner approach है।

---

# 🟢 19. Branch क्यों बनाते हैं?

Production में developers आमतौर पर सीधे `main` पर experimental changes नहीं करते।

Typical flow:

```text
main
 ↓
feature branch
 ↓
commit
 ↓
push
 ↓
Pull Request
 ↓
Review
 ↓
CI
 ↓
Merge
```

---

# 🟢 20. Merge क्या है?

दो development histories को combine करना merge है।

```bash
git switch main
git merge feature/login
```

Graph:

```text
A---B---C main
     \
      D---E feature

After merge:

A---B---C---M
     \     /
      D---E
```

`M` merge commit हो सकता है, depending on history and merge strategy.

---

# 🟢 21. Fast-forward merge क्या है?

अगर target branch में कोई नया divergent commit नहीं है:

```text
A---B---C feature
         ^
        main
```

Main को सीधे आगे move किया जा सकता है।

```text
A---B---C
         ^
       main
       feature
```

इसमें अलग merge commit जरूरी नहीं होता।

---

# 🟢 22. Merge conflict क्या है?

जब Git automatically decide नहीं कर पाता कि same area में कौन-सा change रखना है।

Example:

```text
<<<<<<< HEAD
version = "1.0"
=======
version = "2.0"
>>>>>>> feature
```

आपको manually सही content चुनना होगा।

फिर:

```bash
git add <file>
git commit
```

---

# 🟢 23. Rebase क्या है?

Rebase आपकी branch के commits को नई base के ऊपर replay करता है।

```text
Before:

A---B---C main
     \
      D---E feature
```

Rebase के बाद conceptually:

```text
A---B---C---D'---E' feature
```

> Rebase commit history rewrite कर सकता है।

---

# 🟢 24. Merge vs Rebase

| Feature | Merge | Rebase |
|---|---|---|
| History | Preserve करता है | Rewrite कर सकता है |
| Merge commit | हो सकता है | सामान्यतः नहीं |
| Safe for shared history | Generally safer | सावधानी जरूरी |
| Linear history | जरूरी नहीं | अक्सर cleaner |
| Conflict | हो सकता है | हो सकता है |

### Production Rule

> Public/shared branch की history को बिना team agreement के rebase करके rewrite मत करो।

---

# 🟢 25. `git fetch` vs `git pull`

### `git fetch`

Remote से latest references/objects लाता है लेकिन आपकी current branch में automatically merge नहीं करता।

```bash
git fetch origin
```

### `git pull`

आमतौर पर fetch + integration operation करता है।

```bash
git pull origin main
```

### Safe mental model

```text
fetch = "पहले जानकारी ले आओ"
pull  = "जानकारी लाकर integrate भी करो"
```

---

# 🟢 26. `git push` क्या करता है?

Local commits को remote repository पर भेजता है।

```bash
git push origin feature/login
```

First push:

```bash
git push -u origin feature/login
```

---

# 🟢 27. Remote क्या है?

Remote किसी दूसरे repository location का नाम/reference है।

Check:

```bash
git remote -v
```

Typical remote:

```text
origin
```

Add:

```bash
git remote add origin <repository-url>
```

---

# 🟢 28. `origin` क्या है?

`origin` कोई magic Git command नहीं है।

यह सिर्फ remote का commonly used default name है।

```bash
git remote -v
```

आप technically दूसरा नाम भी रख सकते हैं।

---

# 🟢 29. Clone क्या करता है?

Remote repository की copy local machine पर लाता है।

```bash
git clone <repository-url>
```

Clone में सामान्यतः:

- Working files
- Git metadata
- Remote configuration
- Repository history

आ जाती है।

---

# 🟢 30. `git diff` क्या करता है?

Unstaged changes देखने के लिए:

```bash
git diff
```

Staged changes:

```bash
git diff --staged
```

दोनों का फर्क समझना debugging में बहुत useful है।

---

# 🟢 31. `git restore` क्या करता है?

Working tree changes को restore करने के लिए इस्तेमाल किया जा सकता है।

```bash
git restore main.tf
```

⚠️ इससे uncommitted changes खो सकते हैं।

Staged file को unstage करने के लिए:

```bash
git restore --staged main.tf
```

---

# 🟢 32. `git reset` क्या है?

Reset HEAD/index/working tree को अलग-अलग modes में move कर सकता है।

Common modes:

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
```

### सबसे important

`--hard` destructive हो सकता है।

> 🚨 Production/shared history पर blindly `git reset --hard` मत चलाओ।

---

# 🟢 33. `git revert` क्या है?

किसी existing commit के effect को reverse करने के लिए नया commit बनाता है।

```bash
git revert <commit-hash>
```

### Production में क्यों useful?

अगर commit पहले ही shared remote/main branch पर जा चुका है, तो `revert` अक्सर history rewrite करने से safer approach है।

---

# 🟢 34. Reset vs Revert

| Reset | Revert |
|---|---|
| History pointer बदल सकता है | नया reversing commit बनाता है |
| Local/private work में useful | Shared branch में useful |
| History rewrite कर सकता है | History preserve करता है |
| Dangerous हो सकता है | Generally safer |

### Golden Rule

> **Private history → reset can be useful**  
> **Shared history → revert is usually safer**

---

# 🟢 35. `git stash` क्या है?

Temporary uncommitted changes को side में रखता है।

```bash
git stash
```

बाद में:

```bash
git stash pop
```

List:

```bash
git stash list
```

Named stash:

```bash
git stash push -m "WIP Terraform changes"
```

### Use case

आप feature पर काम कर रहे हैं और अचानक production hotfix branch पर जाना है।

```text
Working changes
      ↓
git stash
      ↓
hotfix
      ↓
work complete
      ↓
git stash pop
```

---

# 🟢 36. Tag क्या है?

Tag किसी specific commit को meaningful name देता है।

Example:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Production releases में tags बहुत useful हैं।

```text
v1.0.0 → Release 1
v1.1.0 → Release 2
v2.0.0 → Major release
```

---

# 🟢 37. Annotated tag क्या है?

Annotated tag में metadata/message होता है।

```bash
git tag -a v1.0.0 -m "Production release 1.0.0"
```

Inspect:

```bash
git show v1.0.0
```

---

# 🟢 38. `git cherry-pick` क्या है?

किसी specific commit को दूसरी branch पर apply करना।

```bash
git cherry-pick <commit-hash>
```

### Real example

Production में urgent bug fix commit feature branch में बना।

आप वही exact fix release branch में भी चाहते हैं।

```text
feature
   |
   B ← required fix
   |
release ← cherry-pick B
```

### Warning

Cherry-pick duplicate history/commit situations पैदा कर सकता है। Use intentionally.

---

# 🟢 39. HEAD क्या है?

`HEAD` आपकी current checked-out location को refer करता है।

Example:

```text
A---B---C
        ^
       HEAD
```

अगर आप branch switch करते हैं, HEAD भी current branch/commit context बदल देता है।

---

# 🟢 40. HEAD~1 क्या है?

```text
A---B---C
        ^
       HEAD
```

`HEAD~1` = previous commit यानी `B`.

`HEAD~2` = उससे पहले यानी `A`.

---

# 🟢 41. Detached HEAD क्या है?

जब HEAD किसी branch name की जगह सीधे commit पर point करता है।

```bash
git checkout <commit-hash>
```

Modern syntax:

```bash
git switch --detach <commit-hash>
```

आप code inspect/test कर सकते हैं।

अगर changes रखना है तो नई branch बनाना बेहतर है:

```bash
git switch -c experiment
```

---

# 🟢 42. `git show` क्या करता है?

Commit/tag की details देखने के लिए:

```bash
git show <commit-hash>
```

Latest commit:

```bash
git show HEAD
```

---

# 🟢 43. `git blame` क्या करता है?

किस line को किस commit/person ने last modify किया, यह trace करने में मदद करता है।

```bash
git blame main.tf
```

### Production debugging

यह **blame game** खेलने के लिए नहीं है 😂  
यह historical context खोजने के लिए है।

---

# 🟢 44. `git bisect` क्या है?

जब आपको पता है कि पहले code काम करता था और बाद में टूट गया, Git binary search से problematic commit खोजने में मदद कर सकता है।

```bash
git bisect start
git bisect bad
git bisect good <known-good-commit>
```

फिर Git commits के बीच search करवाता है।

### याद रखें

> `bisect = bug detective 🕵️`

---

# 🟢 45. Git aliases क्या हैं?

Frequently used commands को छोटा बना सकते हैं।

```bash
git config --global alias.st status
git config --global alias.co checkout
```

Then:

```bash
git st
git co main
```

Modern workflows में `switch`/`restore` commands भी prefer किए जा सकते हैं।

---

# 🟢 46. Git hooks क्या हैं?

Git hooks कुछ Git events पर scripts run कर सकते हैं।

Examples:

```text
pre-commit
commit-msg
pre-push
```

Use cases:

- Formatting
- Linting
- Secret scanning
- Commit message validation
- Tests

### Security

Hooks developer-side controls हैं; CI में server-side validation भी रखें क्योंकि local hooks bypass हो सकते हैं।

---

# 🟢 47. Git LFS क्या है?

Git LFS = Large File Storage.

Large binary files के लिए useful हो सकता है।

Examples:

- Large media
- ML model files
- Large design assets

हर large file को normal Git history में डालना repository को भारी कर सकता है।

---

# 🟢 48. Git में secret commit हो जाए तो क्या करें?

### 🚨 DO NOT USE IN PRODUCTION

सिर्फ:

```bash
echo secret >> .gitignore
```

करना पर्याप्त नहीं है।

### Correct response

1. Secret को तुरंत revoke/rotate करें
2. Affected system check करें
3. Git history exposure assess करें
4. Secret को secure secret manager में move करें
5. Repository history cleanup करें यदि आवश्यक हो
6. Secret scanning enable करें

### Terraform Example

Terraform state में sensitive values आ सकती हैं। इसलिए:

```gitignore
*.tfstate
*.tfstate.*
.terraform/
```

और remote encrypted backend/state management का उपयोग करें।

---

# 🏭 49. Production Git Repository Structure

Example:

```text
terraform-infrastructure/
├── .github/
│   └── workflows/
│       └── terraform.yml
├── environments/
│   ├── dev/
│   ├── stage/
│   └── prod/
├── modules/
│   ├── network/
│   ├── compute/
│   └── monitoring/
├── .gitignore
├── README.md
└── CODEOWNERS
```

### Production Principles

- Protected main branch
- Pull Request mandatory
- CI checks mandatory
- Secret scanning
- Code review
- CODEOWNERS
- Deployment approvals
- Meaningful commits
- Release tags

---

# 🔐 50. Git Security Checklist

```text
✅ Secrets Git में commit मत करो
✅ Secret scanning enable करो
✅ Branch protection लगाओ
✅ PR review mandatory रखो
✅ Least privilege access दो
✅ MFA/SSO use करो जहाँ available हो
✅ Deploy keys/tokens को safely manage करो
✅ CI credentials को secure रखो
✅ Logs में secrets print मत करो
✅ Compromised secrets तुरंत rotate करो
```

---

# 💰 51. Git का FinOps angle क्या है?

Git खुद usually major cloud cost driver नहीं है, लेकिन Git workflow infrastructure cost को indirectly control कर सकता है।

Examples:

```text
Git PR
 ↓
Terraform Plan
 ↓
Cost estimation/check
 ↓
Approval
 ↓
Apply
```

यह accidental expensive infrastructure deployment रोकने में मदद कर सकता है।

Example:

```text
Developer PR
   ↓
Terraform Plan
   ↓
Cost Check
   ↓
"Expected monthly cost +$2,000"
   ↓
Review
```

### FinOps Mindset

> **Merge करने से पहले cost देखो; bill आने के बाद shock मत लो. 😂**

---

# 🔄 52. Git + CI/CD Workflow

```text
Developer
   ↓
Feature Branch
   ↓
Commit
   ↓
Push
   ↓
Pull Request
   ↓
CI
   ├── Git validation
   ├── Secret scan
   ├── Lint
   ├── Unit tests
   ├── Terraform fmt
   ├── Terraform validate
   └── Terraform plan
   ↓
Code Review
   ↓
Approval
   ↓
Merge
   ↓
CD
   ↓
Deploy
   ↓
Monitor
```

---

# 🏆 53. Production Git Branching Strategy

A practical model:

```text
main
 |
 +-- feature/*
 |
 +-- bugfix/*
 |
 +-- hotfix/*
 |
 +-- release/*
```

Typical flow:

```text
feature/login
      ↓
Pull Request
      ↓
CI checks
      ↓
Review
      ↓
main
      ↓
Release Tag
      ↓
Production
```

Exact branching model should match team/release requirements. Avoid creating branches just because a diagram looks impressive.

---

# 🟢 54. `git clean` क्या है?

Untracked files/directories clean करने के लिए।

Preview:

```bash
git clean -n
```

Actually remove:

```bash
git clean -f
```

Directories:

```bash
git clean -fd
```

### 🚨 Danger

यह untracked data permanently delete कर सकता है।

> पहले `-n` से preview करो।

---

# 🟢 55. `git rm` क्या करता है?

Tracked file को remove करके deletion stage करता है।

```bash
git rm old-config.yaml
```

फिर commit:

```bash
git commit -m "Remove deprecated configuration"
```

---

# 🟢 56. File rename कैसे track करें?

```bash
git mv old-name.txt new-name.txt
```

फिर:

```bash
git commit -m "Rename configuration file"
```

Git similarity के आधार पर rename detect कर सकता है।

---

# 🟢 57. Remote branch क्या है?

Remote repository की branch का local reference हो सकता है:

```bash
origin/main
```

देखने के लिए:

```bash
git branch -r
```

सभी branches:

```bash
git branch -a
```

---

# 🟢 58. Local branch और remote branch में difference?

```text
Local:
main

Remote-tracking:
origin/main
```

Local `main` और `origin/main` अलग refs हैं और sync state अलग हो सकती है।

---

# 🟢 59. Pull Request क्या है?

Pull Request (PR) एक collaboration/review mechanism है जिसमें आप propose करते हैं:

> "मेरी branch के changes को target branch में merge करना है।"

PR में सामान्यतः:

- Code review
- CI checks
- Security checks
- Discussions
- Approvals
- Change history

हो सकती है।

---

# 🟢 60. PR में क्या check करना चाहिए?

```text
✅ Correct branch?
✅ Correct files?
✅ No secrets?
✅ Tests pass?
✅ CI green?
✅ Terraform plan reviewed?
✅ Breaking change?
✅ Security impact?
✅ Cost impact?
✅ Rollback strategy?
```

---

# 🟢 COMPLETE BEGINNER GIT Q&A — NO BASIC QUESTION MISSED

> **यह section आपकी दी हुई पूरी question-list को 1:1 cover करता है।**
> इसके बाद extra beginner questions भी जोड़े गए हैं ताकि Git fundamentals में कोई major gap न रहे।

---

## Q1. What is Git?

**हिन्दी:** Git एक Distributed Version Control System (DVCS) है, जो files/code में हुए changes की history track करता है और teams को safely collaborate करने देता है।

**English:** Git is a distributed version control system used to track changes, maintain history, create branches, and collaborate on software projects.

---

## Q2. Why do we use Git?

Git का उपयोग:

- Code history maintain करने के लिए
- Multiple developers के collaboration के लिए
- Branching और merging के लिए
- Changes review करने के लिए
- पुराने version पर वापस जाने के लिए
- CI/CD workflows integrate करने के लिए

**Interview line:**  
> "We use Git to manage source-code history, collaboration, branching, review, and controlled delivery."

---

## Q3. What is version control?

Version control एक system है जो files में होने वाले changes को समय के साथ record करता है।

```text
Version 1
   ↓
Version 2
   ↓
Version 3
   ↓
Version 4
```

आप देख सकते हैं कि **क्या बदला, कब बदला और किस commit में बदला।**

---

## Q4. What problem does Git solve?

Git मुख्यतः इन problems को solve करता है:

```text
❌ कौन-सा code latest है?
❌ किसने change किया?
❌ पुराना working version कहाँ है?
❌ दो developers के changes कैसे combine करें?
❌ गलत change को कैसे reverse करें?
```

Git इन्हें history, commits, branches, merge और collaboration workflow से solve करता है।

---

## Q5. What is a Git repository?

Git repository वह project location है जहाँ Git source files और उनकी version-control information manage करता है।

```text
project/
├── .git/
├── app/
├── README.md
└── main.tf
```

`.git` directory Git की repository metadata/history के लिए महत्वपूर्ण है।

---

## Q6. How do you create a Git repository?

Existing project में:

```bash
git init
```

फिर:

```bash
git status
```

से verify कर सकते हैं।

Remote repository की existing copy लेने के लिए:

```bash
git clone <repository-url>
```

---

## Q7. What is the working directory?

Working directory वह actual filesystem area है जहाँ आपकी checked-out project files रहती हैं और जहाँ आप code edit करते हैं।

```text
Working Directory
       ↓
     edit
       ↓
changes
```

---

## Q8. Where do changes exist when you first modify a file?

जब आप tracked file modify करते हैं, change initially **working directory/working tree** में होता है।

```text
Edit file
   ↓
Working Tree
   ↓ git add
Staging Area
   ↓ git commit
Repository
```

---

## Q9. What is the staging area?

Staging area वह intermediate area है जहाँ आप अगले commit में शामिल होने वाले changes select करते हैं।

```bash
git add main.tf
```

के बाद `main.tf` staged हो जाता है।

---

## Q10. Why do we need a staging area?

Staging area आपको यह control देता है कि **कौन-से changes अगले commit में जाएँगे।**

मान लो आपने एक साथ 3 files बदलीं:

```text
main.tf
variables.tf
README.md
```

लेकिन अभी सिर्फ `main.tf` commit करना है:

```bash
git add main.tf
git commit -m "Add resource configuration"
```

यही staging area का बड़ा फायदा है।

---

## Q11. What does `git add` do?

`git add` selected working-tree changes को staging area/index में रखता है।

```bash
git add main.tf
```

Multiple files:

```bash
git add main.tf variables.tf
```

All relevant changes:

```bash
git add .
```

> ⚠️ `git add` commit नहीं बनाता।

---

## Q12. What is a commit?

Commit Git history में changes का एक recorded snapshot है।

```text
A → B → C → D
```

हर commit एक logical point-in-time state represent करता है।

---

## Q13. Why do we create commits?

Commits से:

- History maintain होती है
- Changes trace किए जा सकते हैं
- Review आसान होता है
- Recovery possible होती है
- Release points identify किए जा सकते हैं

**Golden idea:**

> **Commit = "मेरे changes का meaningful checkpoint."**

---

## Q14. What does `git commit` do?

Staged changes को local Git repository history में commit के रूप में record करता है।

```bash
git commit -m "Add Azure network configuration"
```

Flow:

```text
Working Tree
    ↓
git add
    ↓
Staging Area
    ↓
git commit
    ↓
Local Repository
```

---

## Q15. Why is a commit message important?

Commit message बताता है कि change किस purpose से किया गया।

❌ Bad:

```bash
git commit -m "update"
```

❌ Bad:

```bash
git commit -m "final"
```

✅ Better:

```bash
git commit -m "Fix Terraform validation workflow"
```

Production में meaningful commit messages debugging, auditing और history understanding में मदद करते हैं।

---

## Q16. What does `git status` show?

```bash
git status
```

यह सामान्यतः बताता है:

- Current branch
- Modified files
- Untracked files
- Staged changes
- Unstaged changes
- Branch synchronization information, जहाँ उपलब्ध हो

### Daily habit

> **Git में confusion हो → पहले `git status`.**

---

## Q17. What is Git history?

Git history repository में recorded commits की chronological/graph-like history है।

```text
Initial
  ↓
Feature
  ↓
Bug Fix
  ↓
Release
```

History से पता चलता है कि project कैसे evolve हुआ।

---

## Q18. How can you view Git history?

Basic:

```bash
git log
```

Compact:

```bash
git log --oneline
```

Graph:

```bash
git log --oneline --graph --decorate --all
```

Specific commit:

```bash
git show <commit-hash>
```

---

## Q19. What is a branch?

Branch development की एक independent line/reference है जो अलग work को isolate करने में मदद करती है।

```text
main
 |
 A---B---C
      \
       D---E feature/login
```

---

## Q20. Why do we use branches?

Branches से:

- Features isolate होते हैं
- Experiments safe रहते हैं
- Multiple developers parallel काम कर सकते हैं
- Production/main branch protect की जा सकती है
- PR-based workflow possible होता है

---

## Q21. What is the main branch?

`main` आमतौर पर repository की primary/default branch होती है।

Historically कुछ repositories में `master` भी इस्तेमाल हुआ है।

> Important: `main` कोई Git requirement नहीं; repository/team इसे अलग नाम दे सकती है।

---

## Q22. How do you create a new branch?

Modern Git:

```bash
git switch -c feature/login
```

Check:

```bash
git branch
```

Older/common alternative:

```bash
git checkout -b feature/login
```

---

## Q23. What does it mean to switch branches?

Branch switch करने का मतलब current working context को दूसरी branch पर move करना है।

```bash
git switch feature/login
```

Git उस branch की tracked file state को working tree में checkout करता है, subject to uncommitted-change constraints।

---

## Q24. What is merging?

Merge दो development histories को combine करता है।

```bash
git switch main
git merge feature/login
```

Concept:

```text
main
 A---B---C
      \
       D---E feature

          ↓ merge

A---B---C---M
     \     /
      D---E
```

---

## Q25. Why do we merge branches?

जब feature/bugfix branch का काम target branch में integrate करना हो।

Typical:

```text
feature
   ↓
PR
   ↓
review
   ↓
merge
   ↓
main
```

---

## Q26. What is a merge conflict?

जब Git के पास conflicting changes को automatically combine करने के लिए enough information नहीं होती, conflict आ सकता है।

Example:

```text
<<<<<<< HEAD
version = "1.0"
=======
version = "2.0"
>>>>>>> feature
```

Developer को correct result choose करके conflict resolve करना पड़ता है।

---

## Q27. What is a remote repository?

Remote repository Git repository की दूसरे location/server पर उपलब्ध copy है।

Examples:

```text
origin
upstream
```

Remote inspect करें:

```bash
git remote -v
```

---

## Q28. What is GitHub?

GitHub एक platform है जो Git repositories को host करता है और collaboration सुविधाएँ देता है, जैसे:

- Pull Requests
- Code review
- Issues
- Actions/CI
- Repository permissions
- Branch protection

---

## Q29. What is the difference between Git and GitHub?

```text
Git
 ↓
Version Control System

GitHub
 ↓
Git repository hosting + collaboration platform
```

**Interview answer:**

> "Git is the version control technology; GitHub is a platform that hosts Git repositories and provides collaboration, review, automation, and governance features."

---

## Q30. What does `git push` do?

Local commits/refs को remote repository में भेजने के लिए use होता है।

```bash
git push origin feature/login
```

First upstream setup:

```bash
git push -u origin feature/login
```

---

## Q31. What does `git pull` do?

`git pull` सामान्यतः remote changes fetch करके उन्हें current branch में integrate करने की workflow perform करता है।

```bash
git pull origin main
```

Exact integration behavior configuration/command options पर depend कर सकता है; rebase workflow के लिए:

```bash
git pull --rebase
```

---

## Q32. What does `git clone` do?

Remote repository की working copy local machine पर create करता है।

```bash
git clone <repository-url>
```

Clone के बाद आप repository में काम कर सकते हैं और configured remote से sync कर सकते हैं।

---

## Q33. What is the difference between `git push` and `git pull`?

| `git push` | `git pull` |
|---|---|
| Local → Remote | Remote → Local integration |
| Local commits भेजता है | Remote changes लाता/integrate करता है |
| Upload direction | Download + integration direction |
| Example: `git push origin main` | Example: `git pull origin main` |

### Memory Trick

> **Push = भेजो 📤**  
> **Pull = लाओ 📥**

---

## Q34. What is the difference between `git clone` and `git pull`?

| `git clone` | `git pull` |
|---|---|
| Repository की initial local copy बनाता है | Existing local repository को update करता है |
| Usually first setup में | Day-to-day sync में |
| Remote repository से नया local repo | Existing repo में remote changes |
| Example: `git clone <url>` | Example: `git pull origin main` |

### Memory Trick

> **Clone = पहली बार घर लाना 🏠**  
> **Pull = घर में latest सामान लाना 📦**

---

## Q35. What is the difference between `git add` and `git commit`?

| `git add` | `git commit` |
|---|---|
| Changes stage करता है | Staged changes record करता है |
| Working Tree → Index | Index → Local Repository |
| Commit नहीं बनाता | Commit बनाता है |
| Example: `git add main.tf` | Example: `git commit -m "Add resource"` |

---

## Q36. Can you explain the Git workflow from making a change to creating a commit?

Complete flow:

```text
1. Edit file
      ↓
2. git status
      ↓
3. git diff
      ↓
4. git add
      ↓
5. git diff --staged
      ↓
6. git commit -m "meaningful message"
      ↓
7. git log
```

Example:

```bash
vim main.tf

git status
git diff

git add main.tf
git diff --staged

git commit -m "Add resource group"

git log --oneline -1
```

---

## Q37. Can you explain how a local repository communicates with a remote repository?

Typical flow:

```text
                 Remote Repository
                    GitHub
                       ↑
                    git push
                       |
Local Repository ←→ Remote-tracking refs
       ↑
   git fetch
       |
       ↓
Remote updates
```

Day-to-day example:

```text
git fetch
   ↓
Inspect
   ↓
merge/rebase
   ↓
local commit
   ↓
git push
```

Remote का address देखने के लिए:

```bash
git remote -v
```

---

## Q38. Can you explain Git to someone who has never used it before?

### सबसे आसान explanation

मान लो आप एक document लिख रहे हो और हर बार अलग copy बनाते हो:

```text
project-final
project-final-new
project-final-new2
project-final-REAL
project-final-REAL-LAST
😂
```

Git इस chaos को organized history में बदल देता है:

```text
Version A
   ↓
Version B
   ↓
Version C
   ↓
Version D
```

आप:

- Change कर सकते हो
- Snapshot बना सकते हो
- अलग branch पर experiment कर सकते हो
- Team के साथ collaborate कर सकते हो
- जरूरत पड़ने पर पुरानी state investigate/recover कर सकते हो

### One-line definition

> **Git is a tool that helps you safely track, manage, review, and collaborate on changes to your project.**

---

# 🟢 EXTRA BEGINNER QUESTIONS — FUNDAMENTALS को COMPLETE करने के लिए

## Q39. What is `.git`?

`.git` repository की internal metadata/database directory है।

इसे manually delete करना repository की Git history/metadata को नुकसान पहुँचा सकता है।

---

## Q40. What is an untracked file?

ऐसी file जिसे Git अभी track नहीं कर रहा।

```text
?? newfile.txt
```

Track करने के लिए:

```bash
git add newfile.txt
```

---

## Q41. What is a modified file?

Tracked file जिसकी content last committed version से बदल गई है।

Check:

```bash
git status
```

---

## Q42. What is a staged file?

ऐसी change जिसे next commit में शामिल करने के लिए index/staging area में रखा गया है।

```bash
git add file.txt
```

---

## Q43. What is the difference between tracked and untracked files?

| Tracked | Untracked |
|---|---|
| Git already knows the file | Git अभी file track नहीं कर रहा |
| Changes detect कर सकता है | New file के रूप में दिखाई देती है |
| Modify → status में modified | `??` के रूप में दिख सकती है |

---

## Q44. What is `HEAD`?

`HEAD` current checked-out commit/branch context को refer करता है।

Typical:

```text
A---B---C
        ^
       HEAD
```

---

## Q45. What is a commit hash?

Commit का unique identifier hash होता है।

Example:

```text
a12bc34
```

Full hash इससे लंबा हो सकता है।

---

## Q46. How do you see the current branch?

```bash
git branch --show-current
```

Alternative:

```bash
git status
```

---

## Q47. How do you list branches?

Local:

```bash
git branch
```

Remote:

```bash
git branch -r
```

All:

```bash
git branch -a
```

---

## Q48. How do you delete a local branch?

Merged branch:

```bash
git branch -d feature/login
```

Force delete:

```bash
git branch -D feature/login
```

> ⚠️ `-D` carefully use करें; unmerged work खोने का risk हो सकता है।

---

## Q49. What is `.gitignore`?

`.gitignore` Git को बताता है कि कौन-सी untracked files/patterns सामान्यतः track नहीं करनी हैं।

Example:

```gitignore
.terraform/
*.tfstate
.env
*.log
```

> `.gitignore` already committed secret को history से remove नहीं करता।

---

## Q50. What is the difference between local and remote repository?

```text
Local Repository
→ आपकी machine पर Git history

Remote Repository
→ Shared/server-side Git repository
```

Typical:

```text
Local
  ↓ push
Remote

Remote
  ↓ fetch/pull
Local
```

---

## Q51. What is `origin`?

`origin` remote repository का commonly used default name है।

Check:

```bash
git remote -v
```

यह Git की mandatory keyword नहीं है; remote का नाम बदला जा सकता है।

---

## Q52. What is a Pull Request?

Pull Request एक proposed change/integration request है।

```text
Feature Branch
      ↓
     PR
      ↓
Review + CI
      ↓
Approval
      ↓
Merge
```

---

## Q53. Why should production teams use Pull Requests?

क्योंकि PR:

- Code review देता है
- CI checks trigger कर सकता है
- Security validation जोड़ सकता है
- Audit trail देता है
- Approval workflow support करता है

---

## Q54. What is a remote-tracking branch?

Remote branch की local reference को remote-tracking branch कहा जाता है।

Example:

```text
origin/main
```

यह आपके local repository में remote की known state represent करती है और `git fetch` से update हो सकती है।

---

## Q55. What is `git diff`?

Changes inspect करने के लिए:

```bash
git diff
```

Staged changes:

```bash
git diff --staged
```

---

## Q56. What is `git show`?

Commit/tag की details देखने के लिए:

```bash
git show <commit-hash>
```

---

## Q57. What is `git restore`?

Working tree या staging state को restore करने के लिए उपयोग किया जा सकता है।

```bash
git restore file.txt
```

Staged change unstage करने के लिए:

```bash
git restore --staged file.txt
```

---

## Q58. What is `git fetch`?

Remote repository से latest remote objects/references लाता है लेकिन आपकी current branch को automatically integrate नहीं करता।

```bash
git fetch origin
```

---

## Q59. What is the difference between fetch and pull?

```text
fetch
  ↓
Remote updates लाओ
  ↓
लेकिन current branch को automatically integrate मत करो

pull
  ↓
Fetch
  ↓
Integration workflow
```

---

## Q60. What is a Git conflict resolution mindset?

Conflict को "Git की गलती" नहीं समझना चाहिए।

Git कह रहा है:

> "भाई, दोनों changes valid दिख रहे हैं; final decision इंसान करे." 😂

Process:

```text
Identify
 ↓
Understand
 ↓
Resolve
 ↓
Test
 ↓
Stage
 ↓
Continue/Commit
```

---

# 🟡 INTERMEDIATE INTERVIEW QUESTIONS

## Q61. Git distributed क्यों कहलाता है?

**Answer:**  
हर clone में repository history का substantial हिस्सा locally उपलब्ध रहता है। इसलिए developers कई operations बिना central server के भी कर सकते हैं।

---

## Q62. Git working tree क्या है?

**Answer:**  
Working tree वह filesystem state है जहाँ आपकी checked-out files मौजूद हैं और जहाँ आप changes करते हैं।

---

## Q63. Index क्या है?

**Answer:**  
Git का index staging area है। `git add` के बाद selected changes index में रखे जाते हैं और अगला commit इसी staged snapshot से बनता है।

---

## Q64. `git diff` और `git diff --staged` में difference?

**Answer:**

```text
git diff
→ Working tree vs staged/index

git diff --staged
→ Staged/index vs last commit
```

---

## Q65. `git merge --no-ff` क्यों use करते हैं?

**Answer:**  
यह merge commit force कर सकता है, जिससे feature branch integration history explicitly दिखाई दे सकती है। Team की branching/release policy के अनुसार इसका उपयोग करें।

---

## Q66. Rebase कब avoid करना चाहिए?

**Answer:**  
जब commits पहले से shared/public history का हिस्सा हों और rewriting से दूसरे developers की history प्रभावित हो सकती हो।

---

## Q67. `git pull --rebase` क्या करता है?

**Answer:**  
यह remote changes fetch करके local unpushed commits को नई base के ऊपर replay करने की workflow अपनाता है। इससे कई workflows में unnecessary merge commits कम हो सकते हैं।

---

## Q68. `git fetch` क्यों safer माना जा सकता है?

**Answer:**  
क्योंकि fetch remote updates लाता है लेकिन आपकी current branch को automatically integrate नहीं करता। आप changes inspect करके फिर merge/rebase decide कर सकते हैं।

---

## Q69. `git reset --soft` क्या करता है?

**Answer:**  
HEAD को पीछे move करता है लेकिन working tree और index में changes रखता है। इसलिए commit को edit/squash करने जैसी local-history operations में useful हो सकता है।

---

## Q70. `git reset --mixed` क्या करता है?

**Answer:**  
HEAD move करता है और index reset करता है, लेकिन working tree changes सामान्यतः रखता है। यह default reset mode है।

---

## Q71. `git reset --hard` का risk क्या है?

**Answer:**  
यह working tree और index को target commit के अनुसार बदल सकता है और uncommitted changes खो सकते हैं।

---

## Q72. `git revert` production में क्यों useful है?

**Answer:**  
क्योंकि यह पुराने commit को मिटाने के बजाय उसके effect को reverse करने वाला नया commit बनाता है। Shared history के लिए यह अक्सर safer होता है।

---

## Q73. Cherry-pick कब use करेंगे?

**Answer:**  
जब किसी specific commit का change दूसरी branch पर चाहिए और पूरी branch merge नहीं करनी।

---

## Q74. Squash commit क्या है?

**Answer:**  
Multiple commits को एक logical commit में combine करना। इससे final history cleaner हो सकती है।

Example:

```text
WIP
fix
fix again
final
```

↓

```text
Add login feature
```

---

## Q75. Git conflict resolve करने का सही process?

**Answer:**

```text
1. Conflict files identify
2. Conflict markers समझें
3. Correct content चुनें
4. Markers remove करें
5. Test करें
6. git add
7. Merge/rebase continue या commit
```

---

# 🔴 PRODUCTION / SCENARIO-BASED INTERVIEW QUESTIONS

## Q76. Developer ने production branch पर secret push कर दिया। क्या करेंगे?

**Interview-ready answer:**

> First, I would assume the secret is compromised. I would immediately revoke/rotate it, assess where it was exposed, inspect logs/access, remove it from the repository/history where appropriate, and enable/verify secret scanning. I would also move the credential to an approved secret-management solution and identify how the control failed.

---

## Q77. Production में गलत commit merge हो गया। Reset या revert?

**Answer:**

> If the commit is already part of a shared production branch, I would normally prefer `git revert` because it preserves shared history. I would use reset mainly for private/local history when rewriting is safe.

---

## Q78. `main` branch पर कोई direct push कर रहा है। क्या करेंगे?

**Answer:**

> Protect the branch and require Pull Requests, mandatory CI checks, appropriate approvals, and restricted write permissions. Then audit who has direct access and remove unnecessary permissions.

---

## Q79. Developer कहता है "मैंने code change किया लेकिन GitHub पर नहीं दिख रहा।"

Check:

```bash
git status
git log --oneline -5
git remote -v
git branch --show-current
git fetch origin
git status
```

फिर verify करें कि commit local है और सही remote/branch पर push हुआ है।

---

## Q80. `git push` rejected हो रहा है क्योंकि remote में नए commits हैं। क्या करेंगे?

पहले remote changes inspect करें:

```bash
git fetch origin
```

फिर team policy के अनुसार:

```bash
git pull --rebase origin main
```

या merge strategy अपनाएँ।

फिर tests चलाकर push करें।

> Blind `git push --force` नहीं।

---

## Q81. Developer ने `git push --force` किया और shared branch history बदल गई। क्या करेंगे?

**Answer:**

1. Stop further destructive changes
2. Identify previous known-good ref
3. Check reflog/remote history where available
4. Coordinate with team
5. Restore branch carefully
6. Protect branch
7. Investigate why force push was allowed

---

## Q82. Terraform project में `.terraform` और `.tfstate` GitHub में चले गए। Risk?

**Answer:**

`.terraform/` generated/provider data रख सकता है और state में infrastructure information तथा sensitive values हो सकती हैं। Repository exposure होने पर state/credentials को compromised मानकर appropriate rotation and cleanup करना चाहिए।

---

## Q83. Production deployment Git से कैसे secure करेंगे?

```text
PR
 ↓
Code Review
 ↓
Secret Scan
 ↓
Security Scan
 ↓
Tests
 ↓
Terraform Plan
 ↓
Cost Check
 ↓
Approval
 ↓
Apply/Deploy
 ↓
Monitoring
```

---

## Q84. Team में merge conflicts बहुत ज्यादा हैं। क्या करेंगे?

**Answer:**

- Smaller PRs
- Short-lived feature branches
- Frequent synchronization with target branch
- Clear ownership
- Better modularization
- Avoid unrelated changes in same PR
- Good communication
- Consistent formatting

---

## Q85. Git repository बहुत बड़ा हो गया है। क्या investigate करेंगे?

Check:

```text
Large binaries
Large historical files
Generated artifacts
Build outputs
Logs
Unnecessary vendor directories
Git LFS suitability
History cleanup requirement
```

पहले root cause identify करें; blindly history rewrite न करें।

---

# 🧠 COMMON CONFUSIONS

| Confusion | सही समझ |
|---|---|
| Git = GitHub | नहीं; Git VCS है, GitHub hosting/collaboration platform है |
| `git add` = commit | नहीं; add staging करता है |
| `git commit` = GitHub पर upload | नहीं; commit local होता है |
| `git push` = commit | नहीं; local commits remote पर भेजता है |
| `git pull` = fetch only | नहीं; सामान्यतः fetch + integration करता है |
| `git fetch` changes merge करता है | नहीं; fetch integration नहीं करता |
| `.gitignore` secret को secure करता है | नहीं |
| reset और revert same हैं | नहीं |
| branch copy = अलग repository | नहीं |
| rebase हमेशा better है | नहीं |
| force push हमेशा गलत है | Shared protected branches में dangerous; controlled private workflows में valid हो सकता है |
| `git clean` safe delete है | नहीं; untracked data delete कर सकता है |
| commit message कोई भी हो सकता है | technically हाँ, production quality के लिए meaningful होना चाहिए |
| PR सिर्फ code upload है | नहीं; review, CI, discussion और approval workflow भी है |
| Git backup है | Git version history है; backup strategy अलग हो सकती है |

---

# 🆚 IMPORTANT COMMAND COMPARISON

## `fetch` vs `pull` vs `push`

| Command | Main Purpose |
|---|---|
| `git fetch` | Remote updates download/reference करना |
| `git pull` | Fetch + integrate |
| `git push` | Local commits remote पर भेजना |

## `reset` vs `restore` vs `revert`

| Command | Main Use |
|---|---|
| `restore` | Working tree/index changes restore करना |
| `reset` | HEAD/index/working tree state move करना |
| `revert` | Existing commit का effect reverse करने वाला नया commit |

## `merge` vs `rebase`

| Feature | Merge | Rebase |
|---|---|---|
| History rewrite | No | Can |
| Merge commit | Possible | Normally no |
| Shared history | Safer default | Caution |
| Linear history | Not guaranteed | Often cleaner |

---

# 🧱 COMPLETE BEGINNER HANDS-ON LAB

## Step 1 — Create project

```bash
mkdir git-fundamentals-lab
cd git-fundamentals-lab
```

## Step 2 — Initialize

```bash
git init
```

## Step 3 — Create file

```bash
echo "# Git Fundamentals Lab" > README.md
```

## Step 4 — Check status

```bash
git status
```

## Step 5 — Stage

```bash
git add README.md
```

## Step 6 — Commit

```bash
git commit -m "Initial Git lab setup"
```

## Step 7 — Create branch

```bash
git switch -c feature/demo
```

## Step 8 — Change file

Add:

```text
This repository is for Git practice.
```

## Step 9 — Commit

```bash
git add README.md
git commit -m "Add Git practice description"
```

## Step 10 — View history

```bash
git log --oneline --graph --decorate --all
```

## Step 11 — Return to main

```bash
git switch main
```

## Step 12 — Merge

```bash
git merge feature/demo
```

---

# 🧪 ADVANCED HANDS-ON LAB

Practice this workflow:

```text
main
 ↓
feature/network
 ↓
3 commits
 ↓
interactive cleanup
 ↓
Pull Request simulation
 ↓
merge
 ↓
tag release
 ↓
revert one commit
```

Useful commands:

```bash
git switch -c feature/network

git add .
git commit -m "Add network configuration"

git log --oneline

git switch main
git merge feature/network

git tag -a v1.0.0 -m "Production release 1.0.0"

git show v1.0.0
```

---

# 🏭 REAL PRODUCTION GIT WORKFLOW

```text
Developer
   |
   v
feature/*
   |
   v
Commit
   |
   v
Push
   |
   v
Pull Request
   |
   +---- Secret Scan
   |
   +---- SAST
   |
   +---- Tests
   |
   +---- Terraform Validate
   |
   +---- Terraform Plan
   |
   +---- Cost Check
   |
   v
Code Review
   |
   v
Approval
   |
   v
Merge
   |
   v
main
   |
   v
Release Tag
   |
   v
Deployment
   |
   v
Monitoring
```

---

# 🔐 Git + DevSecOps

Production pipeline में:

```text
Git Push
   ↓
Secret Scanning
   ↓
SAST
   ↓
Dependency Scan
   ↓
IaC Scan
   ↓
Tests
   ↓
Build
   ↓
Artifact Scan
   ↓
Approval
   ↓
Deploy
```

### Important

Git repository में कभी भी casually commit न करें:

```text
❌ Passwords
❌ API keys
❌ Cloud access keys
❌ Private keys
❌ Tokens
❌ Production secrets
❌ Terraform state containing sensitive information
```

Use approved secret management:

```text
Azure Key Vault
AWS Secrets Manager
GitHub/Azure DevOps secret mechanisms
OIDC / workload identity
Managed Identity where applicable
```

---

# 💰 Git + FinOps

Git workflow में FinOps controls:

```text
PR
 ↓
Infrastructure Plan
 ↓
Estimated Cost
 ↓
Budget Check
 ↓
Approval
 ↓
Deploy
```

Good practices:

```text
✅ Environment tags
✅ Owner tags
✅ Cost-center tags
✅ Budget alerts
✅ PR-based infrastructure changes
✅ Right-sizing review
```

---

# 😂 DEVOPS COMEDY CORNER

### Joke 1

> Developer: "भाई सिर्फ एक छोटी सी change है।"

> DevOps: "PR बनाई?"

> Developer: "नहीं, production में कर दी।"

> DevOps: "आज से तुम change नहीं, incident हो।" 😂

---

### Joke 2

> `git push --force` production पर करना ऐसा है जैसे  
> शादी के album से पुराने photos delete करके बोलना —  
> "History clean कर दी भाई!" 😂

---

### Joke 3

> Developer: "मेरे laptop पर तो काम कर रहा था!"

> DevOps: "Production तुम्हारा laptop नहीं है भाई!" 😂

---

# 🚨 DANGER ZONE — 10 बातें Production में मत भूलना

```text
❌ Secret commit मत करो
❌ Shared main पर blind force push मत करो
❌ Production में बिना review change मत डालो
❌ Unreviewed direct push avoid करो
❌ git reset --hard blindly मत चलाओ
❌ git clean -f blindly मत चलाओ
❌ Huge binary files casually commit मत करो
❌ Meaningless commit messages मत लिखो
❌ CI/security checks bypass मत करो
❌ "बस जल्दी से production में कर देता हूँ" mindset मत रखो 😂
```

---

# ✅ GOOD PRODUCTION PRACTICES

## Practice 1 — Small, meaningful commits

### ❌ Bad

```bash
git commit -m "changes"
```

### ✅ Good

```bash
git commit -m "Fix AKS ingress health probe"
```

**Why?**

Debugging, review और rollback आसान होते हैं।

---

## Practice 2 — PR + Code Review

### ❌ Bad

```text
Developer → main → Production
```

### ✅ Good

```text
Developer
   ↓
Feature Branch
   ↓
PR
   ↓
CI
   ↓
Review
   ↓
Merge
```

**Why?**

Human review + automated validation risk कम करते हैं।

---

## Practice 3 — Secrets को Git से बाहर रखें

### ❌ Bad

```hcl
client_secret = "my-super-secret"
```

### ✅ Good

```text
Application
   ↓
Managed Identity / Secret Manager
   ↓
Secret
```

**Why?**

Source code और Git history में credentials exposure कम होता है।

---

# ❌ BAD PRODUCTION PRACTICES

## Bad Practice 1 — Force push to shared branch

```bash
git push --force origin main
```

🚨 **DO NOT USE BLINDLY IN PRODUCTION**

Risk:

- History rewrite
- Other developers' work affected
- Recovery complexity

---

## Bad Practice 2 — Secrets in repository

```text
AWS_ACCESS_KEY=...
AZURE_CLIENT_SECRET=...
PASSWORD=...
```

Risk:

- Credential theft
- Security incident
- Compliance issue

Fix:

- Rotate
- Revoke
- Remove
- Secret manager
- Secret scanning

---

## Bad Practice 3 — Direct production changes

```text
Developer
   ↓
git push main
   ↓
Production
```

Risk:

- No review
- No CI
- No approval
- No audit workflow

Better:

```text
PR → CI → Review → Approval → Deploy
```

---

# 🎯 50 MOST IMPORTANT GIT COMMANDS

```bash
git --version
git config --global user.name "Name"
git config --global user.email "email"
git init
git clone <url>
git status
git add <file>
git add .
git commit -m "message"
git log
git log --oneline
git log --graph --oneline --all
git diff
git diff --staged
git branch
git branch -a
git switch main
git switch -c feature/name
git merge branch
git rebase branch
git remote -v
git remote add origin <url>
git fetch origin
git pull
git pull --rebase
git push
git push -u origin branch
git restore <file>
git restore --staged <file>
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git revert <hash>
git stash
git stash list
git stash pop
git tag
git tag -a v1.0.0 -m "Release"
git push origin v1.0.0
git cherry-pick <hash>
git show <hash>
git blame <file>
git bisect
git clean -n
git clean -f
git rm <file>
git mv old new
```

---

# 🎯 INTERVIEW RAPID-FIRE — 20 QUESTIONS

1. Git क्या है?
2. Git और GitHub में difference?
3. Repository क्या है?
4. `.git` directory क्या रखती है?
5. Working tree क्या है?
6. Staging area क्या है?
7. `git add` क्या करता है?
8. `git commit` क्या करता है?
9. `git push` क्या करता है?
10. `git pull` क्या करता है?
11. `git fetch` क्या करता है?
12. Branch क्यों बनाते हैं?
13. Merge क्या है?
14. Rebase क्या है?
15. Conflict क्यों आता है?
16. Reset vs revert?
17. Stash क्यों?
18. Cherry-pick क्यों?
19. Tag क्यों?
20. Production branch को कैसे protect करेंगे?

---

# 🧠 INTERVIEW CLOSING LINES

Interview में सिर्फ command बोलने के बजाय production thinking दिखाएँ:

> **"I prefer Git workflows that protect shared history, enforce Pull Request reviews, automate validation and security checks in CI, keep secrets outside source control, and make production changes auditable and reversible."**

एक और strong line:

> **"For shared production branches, I avoid unnecessary history rewriting and prefer controlled PR-based changes with CI, approval, and a documented rollback strategy."**

---

# 🏆 10 GOLDEN RULES

```text
1. Git को सिर्फ commands नहीं, history system समझो.

2. Edit → Add → Commit → Push याद रखो.

3. Meaningful commit messages लिखो.

4. Feature branch + PR workflow अपनाओ.

5. Shared history को बिना जरूरत rewrite मत करो.

6. Production में revert अक्सर reset से safer होता है.

7. Secrets Git में कभी commit मत करो.

8. .gitignore protection है, secret management नहीं.

9. CI + security + review को Git workflow का हिस्सा बनाओ.

10. Production को experiment lab मत बनाओ. 😂
```

---

# 🧠 ONE-PAGE MEMORY MAP

```text
                    GIT
                     |
       +-------------+-------------+
       |             |             |
    LOCAL          BRANCH        REMOTE
       |             |             |
   status         switch         fetch
   add            merge          pull
   commit         rebase         push
   diff           stash          clone
   log            cherry-pick
   reset          tag
   revert
       |
       v
   PRODUCTION
       |
       +-- PR
       +-- Review
       +-- CI
       +-- Security
       +-- Approval
       +-- Deploy
       +-- Monitor
```

---

# 🚀 FINAL PRODUCTION CHECKLIST

```text
Repository
✅ README exists
✅ .gitignore configured
✅ Branch protection enabled

Development
✅ Feature branch
✅ Small commits
✅ Meaningful commit messages

Security
✅ Secret scanning
✅ No credentials in Git
✅ Least privilege
✅ CI security checks

Review
✅ Pull Request
✅ Code review
✅ Automated tests
✅ IaC validation

Deployment
✅ Plan reviewed
✅ Approval
✅ CI/CD deployment
✅ Monitoring
✅ Rollback strategy

Recovery
✅ Tags/releases
✅ Revert strategy
✅ Backup/recovery process
```

---

# 🎓 Git Mastery Level

```text
LEVEL 1 🟢
init → status → add → commit → log

LEVEL 2 🟡
branch → switch → merge → remote → push/pull

LEVEL 3 🔵
rebase → stash → reset → revert → cherry-pick

LEVEL 4 🟠
tags → hooks → bisect → LFS → advanced history

LEVEL 5 🔴
PR → Branch Protection → CI/CD → Security → Release

LEVEL 6 🏆
Production Git Strategy
+ DevSecOps
+ FinOps
+ Governance
+ Incident Recovery
```

---

# 👑 FINAL MESSAGE

> **Git expert बनने का मतलब 50 commands याद करना नहीं है।**
>
> असली Git maturity तब आती है जब आप जानते हैं:
>
> **कौन-सा command कब use करना है, कब नहीं करना है, production risk क्या है, shared history कैसे protect करनी है, और गलती होने पर safely recover कैसे करना है।**

### ❤️ याद रखो:

```text
Code लिखना Developer का काम है.
Code को safely version करना Git का काम है.
Code को safely deliver करना DevOps का काम है.
और Production को बचाना... पूरे team का काम है. 😎
```

---

## 📌 Author

**Pradip Gavhankar**

*DevOps | Cloud | DevSecOps | FinOps Learning Journey*
