# ask-kit-dotfiles

An [ask-kit](https://github.com/temet-ai/ask-kit) kit that lets your coding agent's `ask` tool
answer questions about how your machine is configured: which file in `~/.config` sets a
keybinding, a window rule, a theme, a monitor or an app setting, and what it is now. A cheap model
searches the folder outside your agent's context, answers with `path:line`, and changes a setting
when asked.

Kinds of question it is built for, which agents otherwise answer by reading `~/.config` by hand:

- Which key combination is bound to a given action in my terminal or window manager, and in which
  file and line?
- Which file sets my monitor layout, and which of two files that set it is loaded last?
- Which font and theme does my terminal use right now, and where are they set?

## Install

You need [ask-kit](https://github.com/temet-ai/ask-kit#set-it-up). Nothing else: the kit is one
manifest with no code.

Paste this into your agent:

```
Read ~/.config/ask-kit/AGENTS.md, then add this kit: github.com/temet-ai/ask-kit-dotfiles
```

Or run it yourself:

```sh
ask-kit kit install temet-ai/ask-kit-dotfiles        # shows what it reads, changes and runs
ask-kit kit install temet-ai/ask-kit-dotfiles --yes  # installs and enables it
```

Restart your agents so `ask` lists `dotfiles`.

## Settings

| Setting | Default | What it is |
|---|---|---|
| `CONFIG_HOME` | `~/.config` | the configuration folder to search |

Set it in the environment or in ask-kit's config as `domains.dotfiles.settings.CONFIG_HOME`.

## What stays out

`~/.config` holds tokens and app data, and what the investigator reads goes to a model. The
manifest's `exclude` list leaves out env files; anything named token, secret, credential or
password; keys, cookies, databases and logs; and the folders of password managers, cloud CLIs,
browsers, chat apps and editors. Excluded files never appear in a search or listing, and reading,
writing or running a program on one is refused.

The list is `exclude` in [`ask-kit.toml`](ask-kit.toml), and the install preview shows it. Once
installed, the manifest is at `~/.config/ask-kit/kits/dotfiles/ask-kit.toml`: add the folders on
your machine that hold credentials or private data before your agents use the kit.

## What it can change

When asked, it edits and writes configuration files and runs programs in the folder (for example
to reload an app). Files on the exclude list are refused.

## How well it works

The bench, `bench/questions.json`, holds questions of those kinds, each with patterns that check
the shape of an answer (a `path:line` citation and a mention of the setting). Their answers depend
on your files, so the bench has not been run against a model; write your own questions from ones
your agents have asked about your machine.

## What is in it

`ask-kit.toml`: a folder source over `CONFIG_HOME` with the exclude list. ask-kit gives a folder
source search, reads, edits and programs, and its `find`, `outline` and `tree` scripts.
[RECIPE.md](RECIPE.md) says what it reads and runs, and how to rebuild it.

MIT licence.
