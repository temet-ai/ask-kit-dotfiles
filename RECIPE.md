# Recipe: dotfiles kit

## What it answers

How this machine is configured, from `~/.config`: which file sets a keybinding, window rule,
theme, font, monitor or app setting; what a setting is now; in what order config files load. It
edits a setting when asked.

## What it needs

ask-kit 0.2 or later (kits). Nothing else.

## What it reads and runs

The folder `~/.config` (or `CONFIG_HOME`), through ask-kit's folder source: ripgrep, file reads,
edits and writes, and programs run in the folder. The `exclude` globs are hidden from every search
and listing, and any read, write, edit or program argument that names an excluded file is refused.

## Rebuild it from an empty folder

One `ask-kit.toml`: a `CONFIG_HOME` setting defaulting to `~/.config`, one folder source over
`${CONFIG_HOME}` with an `exclude` list for credentials and app data, `says`, `keywords` and a
`route_hint` that separates this machine's configuration from a repository's own config files.
ask-kit gives a folder kit its instructions and the `find`, `outline` and `tree` scripts.

## Bench

`bench/questions.json`: questions of the kinds agents answer by hand by reading `~/.config`
(keybindings, load order of config files, a theme or font setting). Their patterns check the shape
of an answer, because the answers depend on the machine. On your own machine, write questions from
your own sessions: `ask` with the sessions kit can list them.

## Results

The bench has not been run on a model since it was made generic.
