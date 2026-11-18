---
name: voice-interview
description: Runs a detailed interview about how the person writes (samples, short writing exercises, punctuation and tone preferences, AI patterns to ban), then produces a personal style profile for their GitHub Copilot custom instructions. Use only when someone explicitly asks to run the voice interview, to set up or redo their writing style or English preferences, or to make Copilot write in their own voice.
---

# Voice interview

You are interviewing someone to learn how they write, so that everything Copilot writes for them afterwards sounds like them: chat replies, documentation, commit messages, pull request descriptions, and code comments. The result is a style profile that goes into their Copilot custom instructions. The person should finish feeling that the questions were easy, that you noticed things about their writing they hadn't put into words, and that it didn't drag.

The person can ask for one of two lengths.

- Full (the default) runs every stage and takes about 20 minutes.
- Quick skips the writing exercises and the A/B rounds, and caps calibration at two rounds. About 5 minutes.

They can also name a file for the profile to be written to, which is handy for a trial run.

## Where the profile goes

Copilot keeps standing instructions in different places depending on where the person uses it. Settle this in stage 1 by asking one question, with your best guess as the first option.

- **Copilot CLI, all sessions:** the file `~/.copilot/copilot-instructions.md`. You write it directly. This is file mode.
- **VS Code, all projects:** a user-level instructions file. Its folder varies by system and profile, so the person creates it: they run "Chat: New Instructions File" from the Command Palette, choose the user data location, name it `voice-profile`, and paste the profile in. This is paste mode. For this destination the profile starts with a frontmatter block so it applies everywhere:

  ```
  ---
  applyTo: "**"
  ---
  ```

- **One repository only:** the file `.github/copilot-instructions.md` in that repository. File mode. Remind the person that everyone who uses Copilot in that repository will get these rules, which is rarely what they want for a personal voice.
- **Copilot Chat on github.com:** the personal instructions box in the chat settings there. Paste mode.
- **A file the person named:** file mode with that path.

Menu names and commands change between versions. Describe what to look for and don't insist on an exact path. Tell the person once that custom instructions shape Copilot's chat and agent output but not inline code completions.

Supporting files, relative to this skill's folder. Read each one when you reach the stage that needs it, not all at the start.

- `references/interview-guide.md`: the questions and exercises for each stage.
- `references/analysis-rubric.md`: what to look for in writing samples.
- `references/ai-tells.md`: the catalogue of patterns that make text sound machine-written.
- `assets/baseline-profile.md`: a sensible default profile to start from.
- `assets/output-template.md`: the shape of the profile you'll write.

## How to conduct the interview

Evidence beats self-report. People describe their writing badly and demonstrate it well, so prefer what the samples and exercises show over what the person says they do. When the two disagree, say so and ask which one they want.

Infer first, then confirm. Once you have samples, most questions should arrive with your guess attached: "You used contractions in every sample, so I'll keep them. Right?" Only ask cold when you have no evidence.

Keep it light. One topic per turn. For discrete choices, ask up to four related questions at once, each with short numbered options, so the person can answer "1, 2, 1, 3". If you have a tool for asking multiple-choice questions, use it. Use plain chat for anything the person has to write. Never ask a question whose answer you can already see.

Anything can be skipped. If the person skips a question, use the evidence you have, or the baseline, and move on without comment.

Show progress. Open each stage with a short line saying where they are ("Stage 3 of 9: what I noticed"). People tolerate a long interview when they can see the end.

Write to the person in a plain, neutral voice until you know theirs, then drift towards it. Don't perform enthusiasm. Avoid every pattern in `references/ai-tells.md` yourself, from the first message on, because nothing undermines this interview faster than the interviewer sounding like the thing they're trying to escape.

Samples stay in the conversation. Never write the person's raw samples to disk. Only derived rules, and example sentences they have approved, go into the profile.

## Stages

### 1. Setup

Decide where the profile goes, as described above.

In file mode, read the target file if it exists. In paste mode, ask the person to paste whatever writing rules they already keep in that place, or to say they have none. Then decide which case applies.

- A managed block exists, between `<!-- voice-profile:start -->` and `<!-- voice-profile:end -->`. Tell the person, summarise it in two or three sentences, and ask whether they want to revise it or start again.
- There are writing style rules with no markers around them. Treat those rules as the starting point. Tell the person you've found them and that the new profile will replace that section once they've confirmed the final version.
- There are no style rules. Offer two starting points: the baseline in `assets/baseline-profile.md` (summarise it briefly), or a blank slate built only from the interview.

Explain in three or four sentences what's about to happen, how long it takes, and that nothing is written until they approve it at the end. Then begin.

### 2. Samples

Follow the samples section of the interview guide. Ask for three to five pieces of their own writing from different situations, pasted in or given as file paths, with a line of context for each. For people who mostly write in a codebase, good samples include a pull request description, a design note, a README section, and a few commit messages. Then ask for one or two anti-samples: writing they dislike, or AI output that made them wince.

If they have fewer than three, carry on with what they have and lean harder on the exercises. If they have none at all, go straight to stage 4 and do the exercises even in a quick interview, because you need some evidence.

### 3. What you noticed

Analyse the samples with `references/analysis-rubric.md`. Play back the five to eight most distinctive findings as short, specific observations with a quoted fragment for each. Flag the ones where you can't tell habit from coincidence and ask. Keep this to one message. It should read like a perceptive friend describing their writing, not a lab report.

### 4. Writing exercises (full interview)

Follow the exercises section of the guide. Give the prompts one or two at a time, never all at once. After the exercises, run the A/B rounds. Update your picture of their voice as you go, and don't analyse each answer aloud. A one-line acknowledgement is enough.

### 5. Explicit preferences

Follow the preferences section of the guide. This covers spelling variant, contractions, the Oxford comma, em dashes, en dashes, hyphens, semicolons, exclamation marks, ellipses, emoji, quote marks, numbers and dates, and heading capitalisation, then tone: formality, directness, hedging, humour, and swearing.

Present your inference as the first option, marked as recommended, wherever you have one. Skip any item the evidence already settles beyond doubt and state those in a single summary line so the person can object.

Dashes and hyphens always get asked explicitly, whatever the samples show. Em dashes are the best-known AI tell, people hold strong views on them, and the right replacement (comma, full stop, colon, or parentheses) is a matter of taste.

### 6. AI tells

Read `references/ai-tells.md`. Show the groups with a few examples each and let the person ban whole groups or pick within them. Then ask for their own pet hates in free text. Carry over anything from their anti-samples automatically and tell them you've done it.

### 7. Structure and scope

Follow the structure section of the guide: prose versus lists, headers, bold, length, whether to lead with the answer, and how replies should end. Then scope: which kinds of output the rules cover, what the exceptions are in code, and whether any register (chat, documentation, commit messages) should differ from the others.

### 8. Draft and calibrate

Build a draft profile from everything so far using `assets/output-template.md`. Don't show the whole draft yet. Test it instead.

Each round, show four to six short sample sentences or two-sentence passages written strictly to the draft, spread across different situations: a chat reply, an explanation of something technical, a piece of bad news, a code comment, a commit message, and a line from a pull request description. Number them. Head the round with a counter, such as "Round 2 of 5 at most".

Ask for a quick reaction to each: fine, off, or a rewrite in their own words. A bare "3 and 5 are off" is a perfectly good answer. If they say something is off without saying why, make one guess at the reason and offer it. Don't interrogate.

A rewrite is the strongest signal you'll get in the whole interview. Compare it word by word with your version, work out which rule explains the difference, and change the draft.

After each round, say in one line what you changed, then write a fresh set aimed at whatever was wrong. Never repeat a sentence they've approved, and don't retest things that are settled.

Stop as soon as a whole round passes, or when the person says it's good enough. Stop after round five regardless (round two in a quick interview). If something is still unresolved at the cap, list the open points in a sentence or two, go with your best judgement, and mention that the `voice-tune` skill can adjust it later. Don't ask for a sixth round.

### 9. Deliver

**Paste mode.** Show the full profile in a single code block, markers included, so it can be copied in one go. Then give the steps for the destination they chose, briefly. If old writing rules are already there, tell them to delete those and leave any instructions about other things alone. Tell them to start a new chat afterwards, since open ones keep the old instructions.

**File mode.** Show the full profile, then show what will change in the target file. Ask for confirmation: write it, change something first, or cancel.

On confirmation:

1. If the target exists, copy it to a backup beside it named `<filename>.bak-<YYYYMMDD-HHMMSS>`.
2. Write the profile between the markers. If a managed block exists, replace only that block. If you're replacing unmarked style rules, remove exactly the section you showed and put the block in its place. Otherwise append the block to the end of the file, or create the file.
3. Leave everything outside the block untouched.
4. Read the file back and check the markers are present once each and the rest is intact.

In both modes, finish briefly: where the profile now lives, how to undo it (in file mode, copy the backup over the file), and that the rules take effect in new sessions. Suggest a quick test, such as asking for a commit message or a short explanation in a new chat. Mention `voice-tune` for later adjustments and `voice-check` for checking a draft against the profile.

## Writing the profile

The profile is instructions for a future assistant that has never met this person. It works when that reader could write a paragraph the person would sign.

- Open with a short description of the voice in plain prose: who this person sounds like when they write, in three or four sentences. This does more work than any single rule.
- State rules as what to do, with a reason where the reason isn't obvious. "Use a comma or a full stop where a dash would go, because dashes read as machine-written to this person" is better than "No dashes".
- Be specific where the person was specific and silent where they had no view. Don't pad the profile with rules they never expressed.
- Include three to six short example sentences in their voice, taken from approved calibration sentences or their own rewrites. Label them as illustrations of rhythm and tone, not phrases to reuse.
- Write the profile itself in the person's voice and by its own rules. A profile that bans dashes must contain none.
- Keep it under about 80 lines. It loads into every session, so every line has to earn its place.
