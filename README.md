# speak-like-human for Microsoft Copilot

> Your uniqueness, makes you, you.

Copilot writes well, but it doesn't write like you. You can usually tell when it's had a hand in something: the em dashes, the word "delve", the cheerful sign-off nobody asked for.

This sorts that out. It's an interview that works out how you write, then gives Copilot a set of rules so it sounds like you from then on, whether it's drafting an email in Outlook or a document in Word.

This is the Microsoft Copilot branch. The Claude version is on `main`, and the GitHub Copilot version is on `github-copilot`.

## How it works

You start by giving it a few things you've written. It then asks you to write a couple of short bits on the spot ("turn down this meeting in your own words") and checks what you think about em dashes, hyphens, spelling, and how formal you like to be. It also shows you a list of common AI habits so you can ban the ones that annoy you.

After that it tests itself. It writes a few sentences in your voice and you tell it which sound right and which don't. It does this for five rounds at most, and you can stop it as soon as you're happy.

The full interview takes about 20 minutes. If you're short on time, type `quick` at any point and it takes about 5.

## Running it

There's nothing to install. The interview is a prompt that you hand to Copilot.

1. Open [prompts/voice-interview.md](prompts/voice-interview.md) and copy the whole thing. On GitHub, the copy button at the top right of the file does it in one click.
2. Start a new chat in Copilot, paste it in, and send it.
3. Answer the questions.

If Copilot says the message is too long, download the file, attach it to the chat, and type `follow the instructions in this file`.

## Saving your rules

When the interview ends, Copilot gives you your rules as a block of text. Copy it, then:

1. Open Copilot's Settings and choose Personalization.
2. Open Custom instructions.
3. Paste the rules in, replacing any old writing rules, and save.
4. Start a new chat.

From then on Copilot follows them. To check, ask it for a short email on anything and see whether it sounds like you.

If you can't find Custom instructions, or you can't edit it, your organisation's admin may have turned it off. You can still use your rules by pasting them in at the start of a chat.

## The other two prompts

[prompts/voice-tune.md](prompts/voice-tune.md) is for small fixes later. Paste it in, say what sounded wrong ("that email was too stiff", "I do use semicolons"), and it changes the one rule that caused it. You don't have to sit through the interview again.

[prompts/voice-check.md](prompts/voice-check.md) checks a draft. Paste it in with your text, and it points out anything that breaks your rules or sounds like a machine wrote it, with a suggested fix for each.

## Your writing stays with you

The samples you share go into your Copilot chat and nowhere else. This repo has no code in it and collects nothing. Your organisation's usual rules for Copilot chats still apply.

## A word of caution

I built this branch from Microsoft's documentation and haven't run it end to end in Copilot yet. I also couldn't find out how many characters the Custom instructions box accepts, so the interview keeps your rules short and tells you the count. If something doesn't behave the way this page says, please open an issue.
