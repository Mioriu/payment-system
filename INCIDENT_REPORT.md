# Incident Report: Payment Commission Bug

## Bug Discovery
- Found using: git bisec bad, git bisect good, git bisect run node /root/stepik/GIT/test-payment.js
- Problematic commit: 29b627ae08fb2df1dfd51337c486367d48106058
- Author: Miory

## Root Cause
The bug was introduced in the "Optimize commission calculation" commit where:
1. Commission calculation was changed to return rate instead of amount
2. Комиссия возвращала только процент комисси, а не сумму

## Fix Applied
- Reverted commit: 29b627ae08fb2df1dfd51337c486367d48106058
- Fix commit: ec471bfb2e8fd54eee9a07290c273f92f61a6a56
- Verification: Проверка тестовым скриптом node /root/stepik/GIT/test-payment.js вернула код 0

## Stash Usage
- Stashed work: в стэше было - modified:   src/commission.js и untracked src/analytics.js
- Stash command used: git stash pop
- Recovery successful: Yes

## Reflog Recovery
- Lost commit: ca44658 HEAD@{1}: commit: Add progressive comission
- Recovery command: git cherry-pick HEAD@{1}
- Restored SHA: 105fce30216d96aff062121fffa4f783c701c4e8

## Lessons Learned
Гит предоставляет множество удобных инструментов для восстановления потерянных изменений, поиска проблемных мест/багов и т.д.
Но необходимо их уметь применять и быть осторожным при работе с удаленной веткой, когда работаешь в команде
