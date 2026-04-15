# Advanced Git Tools Assignment Submission

## Repository Information
- Repository URL: https://github.com/Mioriu/payment-system.git
- Main branch: main
- Feature branch: feature/progressive-commission

## Bug Investigation Results
1. Bisect result - problematic commit:
```
running 'node' '/root/stepik/GIT/test-payment.js'
Bisecting: 0 revisions left to test after this (roughly 1 step)
[8e0073fa3c08fb3dfb3af5965e98dc0c594ae3c8] Extract commission calculation
running 'node' '/root/stepik/GIT/test-payment.js'
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[29b627ae08fb2df1dfd51337c486367d48106058] Optimize commission calculation
running 'node' '/root/stepik/GIT/test-payment.js'
29b627ae08fb2df1dfd51337c486367d48106058 is the first bad commit
commit 29b627ae08fb2df1dfd51337c486367d48106058
Author: Miory <matthew.gg.dk@gmail.com>
Date:   Wed Apr 15 21:17:24 2026 +0300

    Optimize commission calculation

 src/payment.js | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
bisect found first bad commit

```

2. Blame analysis - who introduced the bug:
```
29b627ae (Miory 2026-04-15 21:17:24 +0300  9)         commission: commission, // БАГ: теперь возвращаем rate, а не сумму

```

3. Search for commission changes:
```
1fc05aa Initial payment system setup
```

## Recovery Operations
1. Stash operations performed:
```
stash@{0}: On feature/progressive-commission: WIP: Progressive commission feature
```

2. Reflog recovery command:
```
git cherry-pick HEAD@{1}
```

## Verification Commands
Run these to verify the assignment completion:
```bash
# Check that bug is fixed
node test-payment.js && echo "Bug fixed!"

Bug fixed!

# Verify revert was used
git log --oneline | grep Revert

7995192 Revert "Optimize commission calculation"

# Check clean history in feature branch  
git log --oneline feature/progressive-commission ^main

7fed468 (feature/progressive-commission) add gitginore
105fce3 Add progressive comission

# Verify no sensitive files
git log --all --full-history -- config/secret-keys.json

Пустой вывод
```

## Self-Assessment Checklist
- [1] Used stash to save work in progress
- [1] Found bug using git bisect
- [1] Used blame to identify author
- [1] Fixed bug using revert (not reset)
- [1] Recovered lost commit using reflog
- [1] Cleaned up feature branch history
- [1] Removed sensitive file from history
- [1] All stashes cleaned up
- [1] Created comprehensive incident report
