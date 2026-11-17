---
name: voice-check
description: Checks a piece of writing against the person's saved writing style profile and flags anything that breaks their rules or sounds machine-written, with a suggested fix for each. Use when they ask whether a draft sounds like them, sounds like AI, or follows their style rules, or ask for a draft to be checked or cleaned up against their voice.
argument-hint: "[text or file path] [--target <path>]"
---

# Voice check

Review a draft against the person's style profile and report what breaks it. This skill never edits the settings file.

Arguments: `$ARGUMENTS`

## Steps

1. **Get the draft.** It's the pasted text, the file at the given path, or the piece of writing most recently discussed in the conversation. If none of those is clear, ask.

2. **Load the profile.** It's the block between `<!-- voice-profile:start -->` and `<!-- voice-profile:end -->`. In Claude Code, read `~/.claude/CLAUDE.md`, or the file given by `--target <path>`. In Cowork or Claude chat, the profile lives in a settings box, so look for it in the instructions you were given for this session, and ask the person to paste it if it isn't there. If there are no markers, use whatever writing style rules you find. If there are none, say so, check the draft against `../voice-interview/references/ai-tells.md` alone, and mention that `/voice-interview` would create a profile.

3. **Check the draft.** Read it twice, with a different question each time.
   - First, against the rules: spelling variant, punctuation, banned words and phrases, structure, and formatting. These are mechanical, so be exhaustive. For punctuation rules such as a dash ban, search the text for the characters instead of relying on a read-through.
   - Second, against the voice: read the profile's description and example sentences, then ask whether this person would have written each paragraph. Look for patterns from `../voice-interview/references/ai-tells.md` that the profile doesn't name, and for rhythm, formality, or warmth that doesn't match.

   Respect the profile's exceptions: code identifiers, technical terms, and direct quotes.

4. **Report.** Start with a one-sentence verdict. Then list the findings in the order they appear in the draft, each with:
   - the offending text, quoted
   - the rule it breaks, or the reason it sounds off, in a few words
   - a suggested rewrite

   Put rule breaches before judgement calls and keep the two visibly apart, since the first are facts and the second are opinions. If the same breach recurs many times, report it once with a count. If the draft is clean, say so in a line and stop. Don't invent findings to look thorough.

5. **Offer a rewrite.** Ask whether they'd like a corrected version. If they would, change only what the findings cover and keep their content, order, and meaning. When the draft is a file, show the rewrite first and edit the file only if asked.

Write the report itself by the profile's rules.
