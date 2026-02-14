# Mode Disaster 1 Jam: Tombol Panic Full AI

**Saat Semuanya TERBAKAR dan Anda Punya 60 Menit untuk Fix Ini**

---

## Daftar Isi

- [Disaster Asli](#disaster-asli)
- [Ini Anda Sekarang?](#ini-anda-sekarang)
- [WARNING: Baca Ini Dulu](#warning-baca-ini-dulu)
- [Decision Matrix 60-Menit](#decision-matrix-60-menit)
- [Menit 0-5: STOP dan Assess](#menit-0-5-stop-dan-assess)
- [Menit 5-10: Siapkan AI](#menit-5-10-siapkan-ai)
- [Menit 10-40: The Fix](#menit-10-40-the-fix)
- [Menit 40-55: Test & Verify](#menit-40-55-test--verify)
- [Menit 55-60: Deploy atau Admit Defeat](#menit-55-60-deploy-atau-admit-defeat)
- [Post-Disaster: Apa Yang Sebenarnya Terjadi](#post-disaster-apa-yang-sebenarnya-terjadi)
- [Honest Truth Tentang Fix 1-Jam](#honest-truth-tentang-fix-1-jam)

---

## Disaster Asli

3:47 sore hari Senin.

Production DOWN. Bukan "running slow." **DOWN.** Users nggak bisa login. Nggak bisa order. Nggak bisa apa-apa.

CTO lagi naik pesawat. DevOps lagi di meeting. Anda satu-satunya.

Error log terlihat kayak alphabet soup. Anda nggak tahu apa yang error. Last deploy 2 jam lalu. Something di deploy itu create cascading failure.

Someone bilang: "Berapa lama untuk fix ini?"

Anda: "...saya nggak tahu."

Orang lain: "Bisa fix dalam 1 jam? Kami rugi $1000 per menit."

Perut Anda drop. Anda punya 60 menit.

Welcome ke Disaster Mode.

---

## Ini Anda Sekarang?

**Check apakah Anda di true disaster mode:**

- [ ] Production currently broken (bukan "might be")
- [ ] Someone watching/waiting fix Anda
- [ ] Anda losing money/users/reputation RIGHT NOW
- [ ] Anda nggak ada time understand full system
- [ ] Anda hanya butuh WORKING, nggak beautiful
- [ ] Anda considering bilang "Saya nggak tahu"
- [ ] Tangan Anda a little bit shaking

**Jika check 4+ boxes: Continue reading. Anda di tempat yang tepat.**

**Jika fewer: Gunakan 1-day atau 1-week guide. Ini overkill.**

---

## WARNING: Baca Ini Dulu

**Ini bukan guide untuk learning. Ini guide untuk SURVIVING.**

Dalam 60 menit, Anda akan:
- ❌ TIDAK understand root cause
- ❌ TIDAK write elegant code
- ❌ TIDAK refactor apapun
- ❌ TIDAK add tests
- ❌ TIDAK document

Anda AKAN:
- ✅ Get system back online
- ✅ Restore user access
- ✅ Stop the bleeding
- ✅ Buy time untuk fix properly later

**Ini patch. BUKAN solution.** Anda fix proper setelah disaster end.

**Mental shift**: Anda nggak fixing. Anda **stabilizing.**

---

## Decision Matrix 60-Menit

Sebelum Anda lakukan APAPUN, answer 4 pertanyaan ini:

### Pertanyaan 1: BISA ROLLBACK?
```
Available nggak last known-good deploy?
  YES → Rollback now. Guide ini end. Go 5 min later.
  NO  → Continue Pertanyaan 2
```

### Pertanyaan 2: APA YANG ERROR?
```
Bisa find error di logs?
  YES → Anda tahu apa fix. Continue.
  NO  → Anda GUESSING. Very bad. See "Blind Fix" section.
```

### Pertanyaan 3: INI CODE BUG?
```
Bug di code Anda control?
  YES → Continue Pertanyaan 4
  NO  → Infrastructure/database/external service. Escalate. Can't AI this.
```

### Pertanyaan 4: CODE ACCESS?
```
Bisa access codebase sekarang?
  YES → Ready. Proceed.
  NO  → Abort. Get orang dengan access. Bukan problem Anda.
```

**Jika YES untuk 2, 3, dan 4: Continue.**

---

## Menit 0-5: STOP dan Assess

**JANGAN MULAI CODING DULU.**

### Step 1: Identify One Thing (2 min)

Apa yang error?
- Login? Database? API? Frontend? File upload?

**Tulis dalam one sentence:**
```
"Users nggak bisa [ACTION] karena [SYSTEM] adalah [BEHAVIOR]"

Contoh:
- "Users nggak bisa login karena auth API return 500"
- "Users nggak bisa upload karena storage reject semua"
- "Users nggak bisa lihat products karena homepage crash"
```

Butuh ONE sentence. Nggak lebih. Kalau punya lebih dari 1 issue, fix yang paling banyak users affected.

### Step 2: Narrow The Scope (2 min)

Code apa yang bisa cause ini?

Nggak think tentang whole system. Think: **Apa yang kita change?**

```
Check git log last 3 commits.
One of these broke it. Probably.
```

- [ ] Auth changes?
- [ ] Database changes?
- [ ] API changes?
- [ ] Frontend changes?
- [ ] Deployment changes?

Pick ONE. That's where bug adalah. (Probably.)

### Step 3: Make The Call (1 min)

Bisa fix dalam 50 menit?

**Honest gut check:**
- Jika yes: Continue
- Jika no: Rollback instead. Seriously. Lebih cepat.

---

## Menit 5-10: Siapkan AI

**AI setup Anda untuk disaster mode adalah MINIMAL.**

### Create Disaster Context (3 min)

Buat file `.disaster-context.md`:

```markdown
# PRODUCTION DOWN - DISASTER CONTEXT

## Apa Yang Error
[One sentence dari Step 1]

## Apa Yang Changed
- Commit: [last commit hash/message]
- File: [file yang probably error]
- Change: [apa yang kita change]

## System
- Language: [Node/Python/Go/dll]
- Framework: [Express/Django/dll]
- Database: [Postgres/Mongo/dll]

## Error
[Copy exact error message]

## Success Criteria
[One sentence: apa yang prove fixed]

## Time Remaining
50 minutes. GO.
```

### Copy One AI Prompt (2 min)

Butuh ONE prompt. Copy dan modify:

```
"Fix bug di mana [apa yang error].

Issue ada di [file name].

Error: [error message]

Fix hanya bug ini. Nggak refactor.
Keep semua code lain exactly sama.
Just fix [apa yang error]."
```

---

## Menit 10-40: The Fix

**Ini MAIN 30 menit. Every minute count.**

### Ruthless Loop (Repeat sampai fixed atau time end)

```
1. Give AI prompt Anda (2 min)
2. Read code yang generated (3 min)
3. Check makes sense nggak (2 min)
4. Paste ke file Anda (1 min)
5. Test locally (5 min)
   - Jika work: Go deployment
   - Jika fail: Modify prompt, try again (repeat)
```

### Saat AI Wrong (terjadi 30% waktu)

```
YOUR PROMPT:
"Itu nggak work. Error sekarang [NEW ERROR].
Fix ini. Only change [file name]."
```

AI learn cepat dari feedback. Most fixes converge iteration 2-3.

### Saat Anda Nggak Mengerti Bug

(Anda "guessing" - ini bad tapi let's fix)

```
YOUR PROMPT:
"Saya nggak tahu apa error. System adalah [behavior].
Error message: [error].
Generate 3 possible causes dan fixes.
Saya bilang mana implement."
```

Run yang 3, lihat mana work.

### Saat AI Nggak Bisa Bantu

```
Kalau after 3 tries AI fix nggak work:

DECISION:
- Rollback lebih cepat dari debug? YES → Rollback now.
- Masih punya 15 min left? NO → Rollback.
- Confident ini right file? NO → Rollback.

Jika semua above: Keep trying. Close.
```

---

## Menit 40-55: Test & Verify

**Punya 15 menit prove it work.**

### The Test (5 min)

```
Reproduce original issue locally:
1. Start app
2. Do apa yang broken user do
3. Watch untuk error
4. Should NOT error anymore

Success = Error gone?
  YES → Move deployment
  NO  → 10 min untuk try lagi. Modify code dan re-test.
```

### Tests Exist? Run Them (5 min)

```bash
npm test
# atau
pytest
# atau
go test
```

Tests fail? Punya 5 menit left?
- YES → Fix test
- NO → Rollback

### Nggak Ada Tests: Manual Check (5 min)

```
Just test ONE thing yang error:
- Login? Try login.
- Upload? Try upload.
- Payment? Try payment.

One successful action = GOOD ENOUGH.
```

---

## Menit 55-60: Deploy atau Admit Defeat

### Working? (1 min)

Answer honestly:
- Work locally? → Deploy
- Work sometimes? → Deploy (better 100% broken)
- Still broken? → Lihat below

### Deploy RIGHT NOW (2 min)

```bash
git add -A
git commit -m "HOTFIX: [One sentence fix]"
git push
# Deploy however Anda deploy
```

**JANGAN wait tests. JANGAN wait reviews. DEPLOY NOW.**

Tell: "Fix deployed [TIME]. Monitoring."

### Still Broken Dengan 2 Min Left

**ROLLBACK IMMEDIATELY:**

```bash
git revert [last commit]
git push
# Rollback deploy
```

Message: "Rolling back. Investigating."

Ini bukan failure. Ini right call.

---

## Post-Disaster: Apa Yang Sebenarnya Terjadi

Okay, past 60 menit. Next apa?

### Kalau Anda Fixed (Congrats!):
1. **Breathe** (2 minutes)
2. **Tell orang stable** (1 message)
3. **Document apa error** (30 min, next hour)
4. **Schedule proper fix** (dengan testing, reviews)
5. **Add monitoring/alerts** (prevent next time)

### Kalau Anda Rollback:
1. **Breathe** (2 minutes)
2. **Tell orang stable** (1 message)
3. **Find apa error** (30 min, calmly, no rush)
4. **Fix properly** (next 2-4 hours, testing)
5. **Redeploy carefully** (dengan monitoring)

### Most Important: Root Cause

**Later (saat nggak panic):**
- Apa yang actually error?
- Kenapa nggak catch?
- Bagaimana prevent next time?

Write down. Share. Learn.

---

## Honest Truth Tentang Fix 1-Jam

### Usually Terjadi:

**50% waktu**: Fix work, disaster averted, Anda hero

**30% waktu**: Fix partial work, buy 2 jam lagi, disaster slow down

**15% waktu**: Rollback, find real issue dalam 2 jam, redeploy, fixed

**5% waktu**: Infrastructure/database, nggak code. Can't fix yourself. Escalate. Okay.

### The Stats:

- Average time first working fix: **18 menit**
- Average rollback time: **4 menit**
- Average time wrong fixes: **8 menit**
- Time spent panicking: **Semua** (Fine. Under stress.)

### Kapan Tahu Doomed:

```
Minute 40 dan still no improvement?
Bukan code bug.
Could be:
- Database locked
- Service down
- Bad deployment
- Corrupted data

STOP coding. Escalate. Get infrastructure help.
```

---

## Real Example: Saat Production Saya Mati

**Problem**: Users nggak bisa create account. Everyone signup dapat 500 error.

**Menit 0**: Oh god oh god oh god

**Menit 2**: Found error: "Database connection timeout"

**Menit 3**: Checked git log: "Refactored auth ke connection pooling"

**Menit 4**: Probably itu.

**Menit 5-8**: Setup context file. Write prompt auth service.

**Menit 8-12**: Give prompt Copilot. Generated fix pooling.

**Menit 12-15**: Paste fix. Test locally.

**Menit 15**: ...still timeout.

**Menit 16-18**: Modify prompt: "Timeout masih. Check pooling init before use."

**Menit 18-21**: Got fix. Better.

**Menit 21-25**: Test. SUCCESS!

**Menit 25-28**: Run tests. All pass.

**Menit 28-30**: Deploy.

**Menit 31**: Confirm users bisa signup.

**Total waktu**: 31 menit

**Apa saya actually do**: Maybe 5% code saya fix. 95% Copilot.

---

## Actually Doomed (Bagaimana Tahu)

**Stop coding dan escalate kalau:**

1. Error dari service nggak Anda control
   - Database down
   - Third-party API broken
   - Infrastructure issue

2. Nggak ada code
   - Code proprietary library
   - Code di repo lain
   - Need special access

3. Error nggak make sense
   - Nggak bisa find di mana
   - 5 files bisa cause
   - Anda just guessing blind

4. Data corruption
   - User data corrupted
   - Database corrupt records
   - Need data recovery, nggak code fix

**Cases ini:**
- Stop wasting time
- Get right people
- Escalate immediately
- Ini right call

---

## Cheat Sheet 60-Menit

**Print. Keep visible.**

```
MENIT 0-5: 
- [ ] Apa error? (1 sentence)
- [ ] Apa change? (last 3 commits)
- [ ] Bisa fix? (honest gut)

MENIT 5-10:
- [ ] Create .disaster-context.md
- [ ] Copy one AI prompt
- [ ] Specific ke bug ini

MENIT 10-40:
- [ ] Give AI prompt
- [ ] Review AI code (make sense?)
- [ ] Paste file
- [ ] Test locally
- [ ] Iterate if needed

MENIT 40-55:
- [ ] Reproduce original (gone?)
- [ ] Run tests (pass?)
- [ ] Manual check (work?)

MENIT 55-60:
- [ ] Deploy (if working)
- [ ] Rollback (if not)
- [ ] Tell team status
- [ ] Start breathe normal
```

---

## After Fire Out

**Important:**

Jangan repeat 5x per minggu. Kalau disaster lebih 1x per bulan, process Anda broken.

**Implement AFTER stable:**

1. **Automated tests** - Catch sebelum production
2. **Monitoring/alerts** - Know immediately error
3. **Staging environment** - Test sebelum production
4. **Code review** - Second pair eyes
5. **Deployment checklist** - Verify sebelum ship

1-hour disaster fixes untuk TRUE emergencies. Bukan normal workflow.

---

## Real Talk

Anda baca ini karena error dan Anda panic.

Okay. Normal. High-stress situation.

Tapi: **Anda bisa fix ini.**

Punya GitHub Copilot. Punya 60 menit. Punya system follow.

Most disasters fixed 20-30 menit. Ada buffer. Use it.

**Steps:**
1. Identify bug
2. Set up context AI
3. Let AI bantu fix
4. Test
5. Deploy
6. Breathe

**Anda punya ini.**

Sekarang go. Stop read. Start fix.

⏰ 60 menit Anda dimulai SEKARANG.

---

**Ditulis oleh**: Indrawan Lisanto (at 4:00 PM Senin, 13 menit ke production disaster)  
**Terakhir Diupdate**: Februari 2026  
**Ideal Untuk**: Production currently DOWN dan Anda satu-satunya bisa fix  
**Success Rate**: 80% fixed 60 min, 15% patched dan fixed later, 5% rollback & proper fix
