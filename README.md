# Personal dotfiles

A small chezmoi setup for macOS and Linux, replacing the previous custom zsh
loader. Includes zsh shortcuts, Neovim, Herdr TUI, Starship and Ghostty.

## Another machine

Install chezmoi, zsh, Git, Neovim (0.11+), Starship, Herdr and Ghostty (1.2.3+).
Install BitstromWera Nerd Font for the configured font and prompt icons.
For Neovim, install ripgrep and a C compiler/make; language servers and project
runtimes must be installed separately. LazyGit needs the lazygit executable.

```sh
chezmoi init https://github.com/vicocamacho/dotfiles.git
chezmoi diff
chezmoi apply
```

Use zsh as your interactive shell. No OS defaults, apps or services are installed
automatically. This setup does not configure Bash.

## Shortcuts

- Git: gl, glog, gp, gd, gc, gca, gco, gb, gs, gac, gf, gcb, ge.
- c [project/subdirectory]: jump below $PROJECTS, default ~/src; supports Tab completion.
- e [files...]: open in $EDITOR, default nvim; no arguments opens the current directory.
- gcb copies the branch with pbcopy (macOS), wl-copy (Wayland), or xclip (X11).
- ge opens untracked files, including filenames with spaces.

Set machine-specific environment variables in ~/.localrc (not tracked), e.g.:

```sh
export PROJECTS="$HOME/code"
```

## Daily use

```sh
chezmoi edit --apply ~/.zshrc
chezmoi diff
chezmoi apply
chezmoi cd
# review, git add, git commit, git push
```

After direct edits to a plain managed file: `chezmoi add PATH`.
Ghostty and .zprofile use templates: use `chezmoi edit --apply PATH` to preserve
OS-specific logic. On another machine: `chezmoi update` pulls and applies.

## Scope

Preserves the current editor, terminal and prompt customization. Tests run in
Neovim's terminal; tmux/Vimux and old project-specific sessionizer mappings were
removed. Herdr bindings for missing worktree/sessionizer scripts were removed;
other Herdr bindings remain, including plugin actions requiring their plugins.
Neovim plugin revisions remain locked, except the removed Vimux plugin.

Excludes generated files, sessions, caches, credentials and machine-local settings.
The old bootstrap scripts, prompt, legacy Vim config, macOS defaults, package list,
Ruby/Node version-manager initialization and unused helper scripts are not carried
over. Add runtime initialization later if needed.

Adapted from https://github.com/vicocamacho/dotfiles; original license retained.
