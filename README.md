# speak-like-human

Three Claude Code skills that teach Claude to write the way you do. An interview learns your voice from samples, short exercises, and your answers about punctuation and tone, then saves a style profile to your Claude settings. After that, everything Claude writes for you follows it: emails, documents, chat replies, commit messages, and code comments.

## Running it in Cowork

You need the Claude desktop app and this repo's address. Nothing else.

1. In Cowork, open the Plugins page (under Customize, then Browse plugins) and choose Add marketplace. In some versions it's a + button on the Personal tab, labelled Add marketplace from GitHub.
2. Paste `https://github.com/sahilNaran/speak-like-human` and confirm.
3. Install the speak-like-human plugin from the list that appears.
4. Start a new Cowork session and type: `run the voice interview`. For the short version, say `run the quick voice interview`.

Claude can't change Cowork's settings itself, so the interview ends by handing you your profile as a block of text. Copy it, open Settings, find Global instructions in the Cowork section, paste it in, and save. New sessions will follow it from then on. If you already keep writing rules in that box, the interview will ask for them at the start and tell you what to replace at the end.

The same approach works in ordinary Claude chat, where the profile goes into the personal preferences box in Settings.

## Running it in Claude Code

The quickest way is to clone the repo and start Claude Code inside it. The skills are picked up from the folder, with nothing to install.

```
git clone https://github.com/sahilNaran/speak-like-human.git
cd speak-like-human
claude
```

Then type `/voice-interview`.

You only need to do this once. The profile lives in `~/.claude/CLAUDE.md`, which Claude reads in every project, so you can delete the clone afterwards if you like.

If you'd prefer to keep the skills available everywhere, install the repo as a plugin instead:

```
/plugin marketplace add sahilNaran/speak-like-human
/plugin install speak-like-human@speak-like-human
```

As a plugin, the commands carry a prefix, for example `/speak-like-human:voice-interview`.

## The skills

`/voice-interview` runs the full interview. It takes about 20 minutes, or about 5 with `/voice-interview quick`. It asks for a few pieces of your own writing, sets some short exercises ("decline this meeting in your own words"), asks about em dashes, hyphens, spelling, and tone, and shows you a catalogue of AI habits to ban. It then tests its understanding on you with sample sentences, for five rounds at most, and writes the profile once you've approved it.

`/voice-tune` makes one small change later on. Tell it what sounded off ("that email was too stiff", "allow semicolons") and it edits the one rule responsible.

`/voice-check` reviews a draft against your profile and lists anything that breaks your rules or sounds machine-written, with a suggested fix for each. It never changes your settings.

## What gets written

In Cowork and Claude chat, nothing is written for you: the interview gives you the profile and you paste it into your settings. The rest of this section is about Claude Code.

In Claude Code, the interview writes one block to `~/.claude/CLAUDE.md`, between two marker comments, and leaves the rest of the file alone. It shows you the exact change and waits for your approval first. Every write makes a timestamped backup beside the file, such as `CLAUDE.md.bak-20261117-143000`. To undo a change, copy the backup over `CLAUDE.md`.

To try the interview without touching your real settings, point it at another file:

```
/voice-interview --target /tmp/test-profile.md
```

The same option works with the other two skills.

## Privacy

Your writing samples stay in the conversation and are never saved to disk. The profile holds only the rules derived from them, plus a few example sentences you approve. The skills read nothing except the text you paste, the files you name, and the settings file.
