# speak-like-human for GitHub Copilot

> Your uniqueness, makes you, you.

An interview that works out how you write, then gives Copilot a set of rules so it sounds like you. The full story is on the [main branch](https://github.com/sahilNaran/speak-like-human). This page just covers your options for GitHub Copilot.

## Options for running it

**In VS Code.** Clone this branch, open the folder, and type `run the voice interview` in Copilot Chat (agent mode).

```
git clone -b github-copilot https://github.com/sahilNaran/speak-like-human.git
cd speak-like-human
code .
```

**In Copilot CLI.** Clone it the same way, run `copilot` in the folder, and type `run the voice interview`.

**In every project.** Copy the three folders from `.github/skills` into `~/.copilot/skills`. After that you can run the interview from anywhere.

Whichever you pick, say `run the quick voice interview` if you want the 5 minute version and not the 20 minute one.

## Options for where your rules go

The interview asks you to pick one.

- **Copilot CLI.** It writes them to `~/.copilot/copilot-instructions.md` for you.
- **VS Code, all projects.** It gives you the rules as text and walks you through saving them as a user-level instructions file.
- **Copilot Chat on github.com.** It gives you the rules to paste into your personal instructions.
- **One repository.** It writes them to `.github/copilot-instructions.md`. Everyone using Copilot in that repo gets them too.

Your rules apply to chat and agent mode. They don't change the inline suggestions that appear as you type.

## Options once you're set up

- `voice-tune` fixes one thing that sounds off, without redoing the interview.
- `voice-check` reads a draft and flags anything that breaks your rules or sounds machine-written.
