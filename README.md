# speak-like-human for GitHub Copilot

> Your uniqueness, makes you, you.

Copilot writes well, but it doesn't write like you. You can usually tell when it's had a hand in something: the em dashes, the word "delve", the commit message that reads like a press release.

This sorts that out. It's an interview that works out how you write, then gives Copilot a set of rules so it sounds like you from then on. That covers chat replies, documentation, commit messages, pull request descriptions, and code comments.

This is the GitHub Copilot branch. The Claude version is on `main`, and the Microsoft Copilot version is on `ms-copilot`.

## How it works

You start by giving it a few things you've written. It then asks you to write a couple of short bits on the spot ("turn down this meeting in your own words") and checks what you think about em dashes, hyphens, spelling, and how formal you like to be. It also shows you a list of common AI habits so you can ban the ones that annoy you.

After that it tests itself. It writes a few sentences in your voice and you tell it which sound right and which don't. It does this for five rounds at most, and you can stop it as soon as you're happy.

The full interview takes about 20 minutes. There's a quick one that takes about 5.

## Setting it up

The interview is packaged as three agent skills, which Copilot picks up from the `.github/skills` folder. You'll need a version of VS Code or Copilot CLI that supports agent skills.

Clone this branch and open the folder:

```
git clone -b github-copilot https://github.com/sahilNaran/speak-like-human.git
cd speak-like-human
code .
```

Open Copilot Chat in agent mode and type `run the voice interview`. If you're short on time, type `run the quick voice interview`. In Copilot CLI, run `copilot` in the folder and ask for the same thing.

If you'd like the skills available in every project, copy the three folders from `.github/skills` into `~/.copilot/skills`.

## Where your rules end up

Copilot keeps its standing instructions in a few different places, so the interview asks which one you want.

- For Copilot CLI, it writes them to `~/.copilot/copilot-instructions.md` for you.
- For VS Code across all your projects, it gives you the rules as a block of text and walks you through saving them as a user-level instructions file.
- For Copilot Chat on github.com, it gives you the same block to paste into your personal instructions there.
- For a single repository, it can write them to `.github/copilot-instructions.md`. Bear in mind that everyone using Copilot in that repo gets them too.

Whenever it writes a file, it shows you the change first, waits for you to say yes, and saves a copy of the old file next to it.

One limit to know about: custom instructions shape what Copilot says in chat and agent mode. They don't affect the inline suggestions that appear as you type.

## What's in it

There are three skills.

`voice-interview` is the main one, described above.

`voice-tune` is for small fixes later. Tell it what sounded wrong ("that pull request description was too stiff", "I do use semicolons") and it changes the one rule that caused it. You don't have to sit through the interview again.

`voice-check` reads a draft and points out anything that breaks your rules or sounds like a machine wrote it, with a suggested fix for each. It never touches your settings.

## Your writing stays with you

The samples you paste in stay in the conversation. They don't get saved anywhere. The only things that end up in your instructions are the rules, plus a few example sentences that you've approved.

## A word of caution

I built this branch from the Copilot documentation and haven't run it end to end in Copilot yet. If something doesn't behave the way this page says, please open an issue.
