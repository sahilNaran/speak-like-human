# speak-like-human

> Your uniqueness, makes you, you.

Claude writes well, but it doesn't write like you. You can usually tell when it's had a hand in something: the em dashes, the word "delve", the cheerful sign-off nobody asked for.

This sorts that out. It's an interview that works out how you write, then gives Claude a set of rules so it sounds like you from then on. That covers emails, documents, chat replies, commit messages, and anything else it writes for you.

This is the Claude version. There's one for GitHub Copilot on the [`github-copilot`](https://github.com/sahilNaran/speak-like-human/tree/github-copilot) branch and one for Microsoft Copilot on the [`ms-copilot`](https://github.com/sahilNaran/speak-like-human/tree/ms-copilot) branch.

## How it works

You start by giving it a few things you've written. It then asks you to write a couple of short bits on the spot ("turn down this meeting in your own words") and checks what you think about em dashes, hyphens, spelling, and how formal you like to be. It also shows you a list of common AI habits so you can ban the ones that annoy you.

After that it tests itself. It writes a few sentences in your voice and you tell it which sound right and which don't. It does this for five rounds at most, and you can stop it as soon as you're happy.

The full interview takes about 20 minutes. There's a quick one that takes about 5.

## Setting it up in Cowork

All you need is the Claude desktop app and the link to this repo.

1. In Cowork, go to the Plugins page (it's under Customize, then Browse plugins) and pick Add marketplace. On some versions it's a + button on the Personal tab instead.
2. Paste in `https://github.com/sahilNaran/speak-like-human`.
3. Install speak-like-human from the list.
4. Start a new session and type `run the voice interview`. If you're short on time, type `run the quick voice interview`.

One thing to know: Claude can't change Cowork's settings for you. So when the interview finishes, it gives you your rules as a block of text. Copy it, open Settings, find Global instructions in the Cowork section, paste it in, and save. Every new session will use it.

If you've already got writing rules in that box, don't worry. The interview asks about them at the start and tells you what to swap out at the end.

This works in normal Claude chat too. The only difference is that the rules go into the personal preferences box in Settings.

## Setting it up in Claude Code

Clone the repo and open Claude Code inside it. There's nothing to install.

```
git clone https://github.com/sahilNaran/speak-like-human.git
cd speak-like-human
claude
```

Then type `/voice-interview`.

You only have to do this once. Your rules get saved to `~/.claude/CLAUDE.md`, which Claude reads in every project, so you can delete the folder afterwards.

If you'd like to keep it around, install it as a plugin:

```
/plugin marketplace add sahilNaran/speak-like-human
/plugin install speak-like-human@speak-like-human
```

The commands get a prefix when you do it this way, so it's `/speak-like-human:voice-interview`.

## What's in it

There are three skills.

`voice-interview` is the main one, described above. Add `quick` for the short version.

`voice-tune` is for small fixes later. Tell it what sounded wrong ("that email was too stiff", "I do use semicolons") and it changes the one rule that caused it. You don't have to sit through the interview again.

`voice-check` reads a draft and points out anything that breaks your rules or sounds like a machine wrote it, with a suggested fix for each. It never touches your settings.

## What it changes on your machine

In Cowork and Claude chat, nothing. You paste the rules in yourself.

In Claude Code, it adds one section to `~/.claude/CLAUDE.md` and leaves the rest of the file alone. It shows you exactly what it's going to change and waits for you to say yes. It also saves a copy of the old file next to it first, named something like `CLAUDE.md.bak-20261117-143000`, so if you don't like the result you can copy that back.

If you want to try it without touching your real settings, point it at a different file:

```
/voice-interview --target /tmp/test-profile.md
```

## Your writing stays with you

The samples you paste in stay in the conversation. They don't get saved anywhere. The only things that end up in your settings are the rules, plus a few example sentences that you've approved.
