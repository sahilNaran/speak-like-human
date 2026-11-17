---
name: voice-tune
description: Makes a small, targeted adjustment to the personal writing style profile in the person's Claude settings file. Use when they say Claude's writing sounded off, too formal, too stiff, or too much like an AI, or when they want to add, relax, or remove a single style rule (for example "allow semicolons" or "stop saying X") without redoing the whole interview.
argument-hint: "[what to change] [--target <path>]"
---

# Voice tune

Adjust an existing style profile with the smallest edit that fixes what the person raised. This is a two-minute job, not a second interview.

Arguments: `$ARGUMENTS`

The profile sits in `~/.claude/CLAUDE.md` unless `--target <path>` says otherwise, between the lines `<!-- voice-profile:start -->` and `<!-- voice-profile:end -->`.

## Steps

1. **Read the target file and find the profile.** If there are no markers but the file has writing style rules, work on those rules directly and leave the markers out. If there are no style rules at all, say so and suggest `/voice-interview`. Stop there.

2. **Understand the complaint.** It will be one of three kinds.
   - A direct instruction ("allow exclamation marks in chat"). Go to step 3.
   - A reaction to something Claude wrote ("that email was too stiff"). Find the text in the conversation, or ask for it. Work out which rule produced the problem, or which missing rule would have prevented it. If the person offers a rewrite, compare the two versions closely, because the difference is the answer.
   - A fresh writing sample to learn from. Compare it with the profile, using `../voice-interview/references/analysis-rubric.md`, and look for anything the profile gets wrong or leaves out.

   If no argument was given, ask what sounded off. Ask at most one clarifying question, and only when you can't tell which of two different edits they want.

3. **Propose the edit.** Change as little as possible: reword one rule, add one line, or remove one. Don't tidy the rest of the profile while you're there. Check that the edit doesn't contradict another rule, and if it does, resolve the conflict in the same edit and say so. For patterns to ban, `../voice-interview/references/ai-tells.md` has the catalogue and a caution about a banned pattern's nearest relative taking its place.

   Show the change as a before and after, with one sentence on what it will do to future writing.

4. **Confirm, back up, and write.** Once the person agrees, copy the target to `<filename>.bak-<YYYYMMDD-HHMMSS>` beside it, apply the edit, and leave everything else in the file untouched. Write the new text in the profile's own voice and by its own rules.

5. **Prove it.** Write two short sample sentences that show the adjusted rule at work, so the person can see the fix landed. If they're still not happy, adjust once more. After a second miss, suggest `/voice-interview` for a fuller recalibration and leave it there.

Finish by saying that the change applies to new Claude sessions, and where the backup is.
