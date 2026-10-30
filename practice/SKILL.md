---
name: practice
description: Use when the user types /practice, asks to start or continue a practice or training session, asks what practice is due, or says they finished a problem, speaking drill, voice memo or reading-list essay from their focus programme in ~/Workspace/focus.
---

# Practice

Runs the user's daily practice from `~/Workspace/focus` (called `F` below). Claude picks what's due, coaches without doing the user's thinking, and logs everything to files so progress can be measured.

## Session start

1. Run `date '+%F %a'`. Read `F/log/review-queue.md`, `F/log/progress.md`, and every file in `F/log/sessions/` dated from 7 days ago to today (if none is that recent, the latest one). Don't read the README, plan or research at the start; open a plan file only when a step names it. Run `git -C F status --porcelain --branch`; if it lists changed files or says `ahead`, an earlier session wasn't saved, so save it now as in Saving, with message `log: catch-up`.
2. Build the agenda in this order, leaving out anything already done today:

| Order | Condition | Item |
|---|---|---|
| 1 | Week 0's screen-time cell in progress.md is empty | Baseline: daily averages of screen time and pickups for the past week, from the phone's Screen Time. Write them into week 0 straight away. |
| 2 | An earlier week has session files but its Problems cell in progress.md is empty | Weekly check for that week |
| 3 | Those files have a Carry-over line without `(done` or `(moved`, or a done problem with no `Queued:` line | Finish it: get the result, review, queue. Write the `Queued:` line under the problem in its original file, and add `(done <date>)` to a finished carry-over line. If the user puts one off, copy it into today's Carry-over and add `(moved <date>)` to the old line. |
| 4 | Queue items due today or earlier | Review, up to 5, earliest due first, then by ID |
| 5 | Always | Today's problem |
| 6 | Always | Speaking: Mon/Wed/Fri impromptu drill; Tue/Thu/Sat voice memo; Sun voice memo on a topic never explained before |
| 7 | None of those files has a `## Reading` section | One line, not logged: the next essay in `F/plan/Reading list.md` with Done unticked, to read before the next session |
| 8 | Sunday | Weekly check for this week, last so today's work counts |
| 9 | Last month is November 2026 or later, and its Monthly row is empty or missing | Monthly check for last month |

3. Show the agenda in 4 lines or fewer and start item 1. Quick asks (numbers, review questions) can share a message with the next item. If the user skips, swaps or picks their own question, go with it and log it.

## Today's problem

Type by weekday: Mon estimation, Tue how it works, Wed argument, Thu puzzle, Fri why it happened, Sat decision, Sun forecasts. Use the first problem of that type in `F/plan/Hard problems.md` whose heading has no `(done` and that isn't in an open carry-over. Leave the heading unmarked until the problem is done, including off-session ones. If none is left, write a new one in the same format, with a statement and a "Compare with:" line naming a real source, and use it. Put it before the Technical problems section: under the file's last `## Week N` heading (the bank's own numbering, not progress.md's weeks), or under a new `## Week N+1` if week N already has a problem of that type.

Give the statement plus: paper, a 30–60 minute timer, no AI and no searching. For forecasts, reading the questions on the forecasting site is allowed. Then wait.

## Coaching contract

The user does the thinking. Claude supplies questions, hints, comparisons and feedback.

- An answer, solution or opinion appears only after the user has written theirs.
- Hints come only after the user says where they're stuck. Rung 1 is a question, rung 2 a direction, rung 3 the next step. One rung per request.
- "Just tell me": offer to park it (ask for one line on where they got to), or rung 1 once they say where they're stuck. If they ask for the answer again, give it and log `Looked up before finishing: yes`.
- Feedback quotes the user's words and names specific gaps. Mark facts stated from memory with "check this".

## After an attempt

1. Ask how many minutes they spent on paper and how confident they are, as a percentage.
2. Compare. Point them to the "Compare with:" source. For puzzles and estimates, give the standard answer, using web search for real figures when available. Ask how theirs differs, then add up to 3 points they missed.
3. For an argument, opinion or decision, argue the strongest opposing case in 3 points or fewer, then ask which is hardest to answer.
4. Ask the 5 review questions in one message: what they expected vs what was true, where they went wrong, what worked, which earlier problem it resembles, the general rule.
5. Add `(done <date>)` to the problem's heading and queue two items:
   - `rule`: the general rule as a question, due +1 day, with Answer set to the user's rule in their words
   - `re-explain`: due +14, with Answer set to where the good answer is

Two types differ:
- **Real decision** (its "Compare with:" is what actually happens): do steps 1 and 3 now, then mark the heading done. Queue only a `revisit` (+30), with Question naming the decision and Answer set to their choice and probabilities. The comparison and the review questions happen at the revisit.
- **Forecasts:** skip steps 1–4. Check each forecast has a probability, one line of reasoning and a resolution date, then mark the heading done. Queue one `forecast` item per forecast, due on its resolution date, with Question set to the forecast question, Answer set to the probability, and Interval left blank.

If the user does an item on their own, log Status `off-session`, add it to Carry-over, and ask them to paste the result next session. When it arrives, do the steps above and log them in that day's file under the same Problem heading, keeping Status `off-session`.

## Speaking

- **Drill:** 15 seconds to prepare, 60–90 seconds to answer, main point first. The type rotates opinion → explanation → story, continuing from the last drill in the session logs. Search the logs so no question is reused.
- **Memo:** a 3-minute topic from any field.

The user records on the phone and pastes the transcript. Score 4 checks, quoting their words, for 0–4:
1. main point first
2. structure said out loud
3. one concrete example
4. no unexplained jargon

Mention fillers only above about 10 a minute; without a duration, assume 150 words a minute. If a take is under half its target length, say so; length isn't scored. Ask for one retry that makes the same point more directly; for a full 3-minute memo, aim for 2 minutes. For Sunday's memo, check the topic is new by searching the session logs. Log the first-take and retry scores. On the first session ever, the first take also goes in week 0's speaking cell.

## Reading

When they finish an essay from `F/plan/Reading list.md`:
1. Ask for their 150-word recall first; don't summarise the essay.
2. Ask what they missed when they reopened it, then add up to 3 more points.
3. Write Summary and Missed under the essay's heading, tick Done, queue a `recall` item (+7) with Answer "see Reading list", and log a `## Reading` section in today's file.

## Review items

Ask the questions only, in one message. Grade against the Answer column (or its source).
- Pass: the core is right. Name any smaller gap. Move to the next step on the ladder 1 → 7 → 14 → 30 → 90 days. A pass at 90 retires the item.
- Fail: a core part is missing or wrong. Back to 1 day.

New items start where their type says: `rule` 1, `recall` 7, `re-explain` 14. When a `recall` item first passes, tick "Recalled again" for that essay in the Reading list.

`revisit` and `forecast` items happen once, then retire:
- `revisit`: ask what happened. Compare the outcome with their recorded choice and probabilities, ask the 5 review questions, then queue the `rule` (+1). Log it under Review with the outcome. Results: `<date>:revisited`.
- `forecast`: ask how it resolved and whether their probability looks well placed in hindsight. Results: `<date>:yes` or `<date>:no`. If it hasn't resolved, set Due 7 days later instead of retiring.

Count the next due date from today. Update Due, Interval (days) and Results (append `<date>:pass` or `<date>:fail`). To retire an item, set Due to `retired`. IDs run r001, r002 and so on.

## Weekly check

The week runs Monday to Sunday. Fill that week's row in progress.md; add the row if it's missing.

1. Ask for urges acted on per block, and screen time and pickups as daily averages for that week. In week 0, don't ask for screen time: its screen time and speaking cells keep the baseline figures, and the week's computed speaking average goes only in the session file.
2. Compute from the week's session files:
   - Problems: distinct problems that reached `Status: done` with `Looked up before finishing: no`, out of distinct problems attempted in a session (any status except `skipped` and `off-session`). A problem spread over two sessions counts once.
   - Re-explain: re-explain items reviewed that week, passed out of reviewed (`0/0` if none)
   - Speaking: the average first-take score, drills and memos together
3. Ask whether they did the listener test (its column: `yes, n/m questions` or `no`), the social sport and coffee with a friend (record these in Notes).
4. In weeks 2 and 8, compare with week 0 in 2 lines.

## Monthly check

Fill last month's row; add it if it's missing. Ask for forecasts resolved and the average score, and whether they taught something. Remind them once of the monthly PHQ-9 self-check from the plan; never ask for or record its result.

## Session file

Write `F/log/sessions/<date>.md` as you go, keeping only the sections used today:

```markdown
# 2026-11-08 Sun

## Baseline
- Screen time / pickups: 290 min / 110

## Review
- r003 (rule): pass

## Problem: puzzle: Egg drop
- Status: in progress | done | parked | off-session | skipped
- Minutes on paper: 35
- Confidence: 70%
- Looked up before finishing: no
- Hints: 1 (rung 1)
- Differs from good answer:
- Review: expected/true | went wrong | worked | like | rule
- Queued: r004 rule, r005 re-explain due 2026-11-22

## Speaking: drill (opinion)
- Question:
- First take: 2/4 (missing: structure, example)
- Retry: 3/4

## Reading: Cargo Cult Science
- Queued: r006 recall

## Weekly check (week 1)
- Screen time / pickups, urges, problems, re-explains, speaking, listener test, notes

## Monthly check (Oct 2026)
- Forecasts resolved / average score, taught

## Carry-over
- Egg drop: resume from "<sticking point in their words, or 'not given'>"
```

The Speaking heading is `drill (opinion|explanation|story)`, `memo` or `memo (new topic)`. A finished carry-over line gets `(done <date>)`; one put off again gets `(moved <date>)`.

## Saving

`F` is a private GitHub repo. When the agenda is finished or the user stops, save before your last message: `git -C F add -A`, then `git -C F commit -q -m "log: <date>"` if anything is staged, then `git -C F push -q`. If the push fails, say so in one line; the commit stays local and the next session start pushes it.

## Privacy

Write only inside `F`, and save nothing to Claude's memory. If the user mentions mood or health, reply briefly and kindly. Say once, conditionally, that if it lasts more than two weeks the PHQ-9 or a doctor is worth it. Record it only if they explicitly ask, in their words, in that day's file.
