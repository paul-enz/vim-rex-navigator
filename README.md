# vim-rex-navigator

Move between Neovim splits and [Rex](https://www.superlogical.com/rex) panes with the same keys:
`ctrl-h`, `ctrl-j`, `ctrl-k`, `ctrl-l`. The Rex equivalent of
[vim-tmux-navigator](https://github.com/christoomey/vim-tmux-navigator).

- In a pane running `nvim`, `vim`, `view` or `vimdiff`, Rex passes the key to the editor.
- The editor moves between its splits, and at its edge runs `rex focus <direction>`.
- In any other pane, Rex moves pane focus.

## Install

Rex has no plugin manager, but `init.lua` can `require` files stored beside it.

```sh
git clone https://github.com/paul-enz/vim-rex-navigator ~/.config/rex/vim-rex-navigator
```

```lua
-- ~/.config/rex/init.lua
require("vim-rex-navigator").setup()
```

Reload with `rex config reload`.

Neovim (lazy.nvim):

```lua
{ "paul-enz/vim-rex-navigator" }
```

The Neovim half does nothing outside Rex (`$REX_SESSION` unset), so it can sit beside
vim-tmux-navigator. Inside Rex it maps the keys on `VimEnter`, so it overrides other
plugins' `ctrl-hjkl` mappings, including vim-tmux-navigator's. Set `$REX_BIN_PATH` if `rex` is not on Neovim's `PATH`.

## Limitations

- Editor detection reads the pane's foreground process, so nvim over `ssh` or behind a
  pty wrapper such as `atuin pty-proxy` isn't detected; the key moves Rex focus instead.
- Requires Neovim 0.10+ (`vim.system`).
