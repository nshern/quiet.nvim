# quiet.nvim

A Lua port of Neovim runtime's [`quiet.vim`](https://github.com/neovim/neovim/blob/master/runtime/colors/quiet.vim) colorscheme by Maxence Weynans, intended as a base for Neovim-focused tweaks.

The base palette and highlight groups match `quiet.vim` exactly. The structure splits the palette into its own Lua module so highlight groups can be remapped without touching color values.

## Usage

```vim
colorscheme quiet-nvim
```

Toggle background:

```vim
set background=dark   " default
set background=light
```

The palette is available as Lua data:

```lua
local palette = require("quiet-nvim.palette")
print(palette.dark.fg)
```

## Structure

- `colors/quiet-nvim.lua` — entry point; applies links, then dark or light highlights.
- `lua/quiet-nvim/palette.lua` — `dark` and `light` color tables plus terminal palettes.
- `extra/ghostty/` — matching Ghostty themes (`quiet-nvim-dark`, `quiet-nvim-light`).

## Deviations from `quiet.vim`

Faithful for truecolor and 256-color terminals. The following were intentionally dropped:

- The `t_Co >= 16` and `t_Co >= 8` fallback blocks (16/8-color terminals).
- Vim-only `term=` attributes (Neovim ignores them).

`colors/quiet-nvim.lua` still `source`s `$VIMRUNTIME/colors/vim.lua` before applying overrides, matching `quiet.vim`'s behavior of reverting to the Vim default base before painting.
