# PRKN Treatment Diary — Investigation Charter

**Diary epoch:** 16 October 2026  
**Status:** Version 1, observational logging prototype  
**Interface:** Phone-first GitHub Pages (`index.html`)  
**Principle:** Record what happened; distinguish observations, hypotheses, and planned regimens.

## The neurologist question

> Can sustained anticholinergic treatment with procyclidine (Kemadrin) improve predominantly left lower-limb dystonia, movement and walking function sufficiently to support a clinician-supervised reduction in Half Sinemet CR? What do the different responses reveal about this person's PRKN-associated condition?

This is a question to investigate, **not an established pharmacological conclusion**. The diary never recommends, schedules automatically, or executes a dose change. A major levodopa reduction can worsen symptoms and should be discussed with the treating clinician.

## Purpose and commitments

- **Append-only:** Every saved event has an immutable ID, creation timestamp, and event timestamp. Corrections are additional entries referring to an earlier ID.
- **No forced baseline, ratings or interpretation:** Record only what the person chooses to report.
- **Separate medication and problem events:** Both appear in a single chronological diary.
- **Actual versus proposed:** A proposed schedule must never be mistaken for a dose actually taken.
- **Time-aware:** Dates and times default to the phone's current local time, but can be edited for retrospective entries.
- **Individual language:** Preserve the person's own terms, especially dystonic versus dyskinetic fatigue and walking power.
- **Portable:** Export all records as JSON or CSV, import JSON backups, and retain regimen history.
- **No automatic medical conclusions:** Pattern review is possible later, but correlations are not proof of causality.

## Medication inventory

| Medicine | Per unit | Available per 24 hours (reported) | Notes |
|---|---|---:|---|
| Madopar | Levodopa 50 mg / benserazide 12.5 mg | 2 | Unit/formulation to verify |
| Kemadrin (procyclidine) | 5 mg tablet | 2 | New second tablet available |
| Half Sinemet CR | Levodopa 100 mg / carbidopa 25 mg | 3 | **One full tablet** each time; “Half Sinemet” is the product name, not a direction to halve it |

These are user-reported supplies, not dosing recommendations.

## Historical regimen — as reported for 14 October 2026

| Time | Medication | Units |
|---|---|---:|
| 01:00 | Half Sinemet CR | 1 full tablet |
| 09:00 | Madopar | 1 |
| 12:00 | Half Sinemet CR | 1 full tablet |
| 15:30 | Half Sinemet CR | 1 full tablet |
| 21:00 | Madopar | 1 |
| 23:00 | Kemadrin | 1 tablet (5 mg) |

The 01:00 dose is treated as part of a repeating daily cycle. Times are reported schedule times, not verified administration records.

## Proposed starting schedule — not a record of doses taken

| Time | Medication | Units |
|---|---|---:|
| 01:00 | Half Sinemet CR | 1 full tablet |
| 09:00 | Madopar | 1 |
| 09:00 | Kemadrin | 1 tablet (5 mg) |
| 12:00 | Half Sinemet CR | 1 full tablet |
| 16:30 | Half Sinemet CR | 1 full tablet |
| 21:00 | Madopar | 1 |
| 21:00 | Kemadrin | 1 tablet (5 mg) |

Compared with the historical schedule, this adds 5 mg Kemadrin daily, moves the earlier Kemadrin from 23:00 to 21:00, and moves the afternoon CR from 15:30 to 16:30. Reported daily totals under the proposed schedule: 400 mg nominal levodopa and 10 mg procyclidine.

## Hypotheses and learning arc

1. **Starting observation:** PRKN-associated Parkinsonism with predominantly left lower-limb dystonia. Much of the day is spent sitting, with walking between sitting periods or walking the dog.
2. **Different phenomena:** Dystonic restriction, involuntary/dyskinetic movement, dystonic fatigue, dyskinetic fatigue and the subjective power of walking are distinct experiences and must not be collapsed into one score.
3. **Reported responses:** Madopar has sometimes relaxed dystonia enough for effective walking. Historically, Kemadrin—not Requip—has been associated with a notably strong, powerful walk.
4. **Current hypothesis:** More sustained antimuscarinic activity might improve symptoms enough to permit reassessment of levodopa exposure. This remains unproven; antimuscarinic activity does not replace dopamine.
5. **Potential later comparison:** A 5 mg twice-daily procyclidine schedule versus smaller divided doses (for example, 2.5 mg four times daily), while tracking actual regimens and experiences. These are **ideas for clinician review**, not instructions to change doses.
6. **Question for clinical review:** Does a different symptom profile emerge under different regimens, and could any Sinemet CR reduction be appropriate under supervision? Abrupt or large levodopa changes are not an app feature.
7. **Learning:** Compare timestamped entries across actual regimen periods; preserve confounders and uncertainty rather than asserting cause and effect.

## Problem vocabulary

- **Sitting:** Quadriceps tension, toe tapping, toe curling, knee flapping/wiggling, leg rocking, internal sense of movement.
- **Posture:** Sitting, standing, leaning forward with elbows on knees.
- **Walking:** Walking power/strength, dystonic restriction, relaxed walking, difficulty initiating walking, fatigue while walking.
- **Fatigue:** **Dystonic fatigue** and **dyskinetic fatigue** are separate labels.
- **Location:** Left lower limb, right lower limb, both, or unspecified.
- **Free text:** Always available; no compulsory severity scale or baseline.

## Data model

Each event includes `id`, `kind` (`medication`, `problem`, `note`, `correction`, or `regimen`), `occurredAt` (local ISO date-time string), `createdAt` (UTC ISO timestamp), and `payload` (the selected medication/quantity or problem labels and free text). A correction adds a new event with `correctsId`, never changes the original. Historical/proposed regimen records are explicitly marked as **reference** or **proposal**, not actual administrations.

## Version 1 delivery

- `index.html`: single-file mobile interface with Medication, Problems, Diary and Regimens.
- Saves entries to the browser's IndexedDB on the device, using an append-only object store.
- Includes JSON/CSV export, JSON import, and visible save confirmation.
- Uses the device clock and supports retrospective entry.
- Is installable to the phone's home screen through the browser's Add to Home Screen option.
- Works as a static GitHub Pages site without a server.

**Storage limitation:** GitHub Pages hosts the interface but does not save diary records to the GitHub repository. This version saves locally on the phone/browser. Clearing browser data, changing devices, or using a different browser can make the records inaccessible; export backups regularly. Cloud sync would be a separate later feature. The HTML contains no analytics or third-party scripts.

## Publishing

1. Create a GitHub repository, for example `prkn-diary`.
2. Upload `index.html` and `README.md` to the repository root.
3. In **Settings → Pages**, select **Deploy from a branch**, `main`, `/ (root)`, and save.
4. Open the published Pages URL on your phone and use **Add to Home Screen**.
5. Make a JSON backup regularly, especially before browser or phone changes.

## Future enhancements (not promised in v1)

Private cloud synchronization, charting, regimen comparison, reminders, offline app caching, and advanced reporting can be considered after the basic event logger is working reliably.


## Investigation milestone — 17 October 2026

**DILEMMA-001:** The first reported dilemma is a planned 16:30 Half Sinemet CR dose not taken as of the afternoon report, in the context of mild manageable seated dyskinesia, no reported dystonia and no dyskinetic fatigue. The patient hypothesizes that the added Kemadrin exposure may be altering the perceived levodopa requirement. See [17 October diary](diary/2026-10-17.md). The exact observation time and subsequent medication decision remain unknown. This is an observation and hypothesis, not confirmation of overmedication or a dose-change instruction.
