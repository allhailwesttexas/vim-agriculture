# Vim Agriculture 🚜

A vim plugin to improve the project search experience when using tools like [ag](https://github.com/ggreer/the_silver_searcher) and [rg](https://github.com/BurntSushi/ripgrep).

# Rationale

I was inspired by [Fzf.vim](https://github.com/junegunn/fzf.vim)'s ability to quickly `:Ag` search multiple words without quotes, narrow down multiple results in realtime with [extended search syntax](https://github.com/junegunn/fzf#search-syntax), then populate quickfix for a large refactor 👌

```
:Ag function index
```

But I found myself missing the ability to pass options to like I could with [Ack.vim](https://github.com/mileszs/ack.vim)'s `:Ack` 😢

```
:Ack -Q -i 'function index' vendor
```

Furthermore, switching between both tools was frustrating because Ack.vim always required quotes for multi word searches, but Fzf.vim treated quotes as a literal part of the search query.

Thus, the intention of this plugin is to bring the best of both worlds to your favourite search wrapper.  Perform multi-word searches with or without quotes, pass options, and do it all from one command! ❤️

# Installation

Install using [vim-plug](https://github.com/junegunn/vim-plug) or similar:

```
Plug 'jesseleite/vim-agriculture'
```

# Usage

If you are already using [Fzf.vim](https://github.com/junegunn/fzf.vim), you can use the provided `:AgRaw` / `:RgRaw` commands.

```
:AgRaw func.*index
:AgRaw 'func.*index'
:AgRaw -Q 'function index()' app/Http/Controllers
```

If you are using another search wrapper, you'll need to wrap your input with `agriculture#smart_quote_input()`.

# Mappings

If you are using one of the above mentioned commands, you can also hook into the provided `<Plug>` mappings in your `.vimrc`:

```
" Ag search project
nmap <Leader>/ <Plug>AgRawSearch
vmap <Leader>/ <Plug>AgRawVisualSelection
nmap <Leader>* <Plug>AgRawWordUnderCursor
```

And likewise for `:RgRaw`, just substitute `AgRaw` for `RgRaw` in the above examples.

# How It Works

Your input will be automatically quoted _unless_ the following conditions are met:
   - Quotes in your query, signifying you might want to handle your own quoting/escaping, ie.
      ```
      :Ag -Q "Already quoted this pattern."
      :Ag Why you "scruffy looking nerf herder"!
      :Ag Who's scruffy looking?
      ```
   - A space followed by a dash in your query, signifying you might be passing an option, ie.
      ```
      :Ag -Q function index
      :Ag Which way to the beach? -> that way!
      ```
   - An escaped pattern followed by an unescaped space, signifying you might be passing a path, ie.
      ```
      :Ag an\ escaped\ pattern vendor/folder
      ```

TL;DR: If you use quotes, dashes, or need to pass a path, it's recommended you quote/escape your own pattern and vim-agriculture will stay out of your way 👍

# Who am I?

Just a hack 🔨

- [jesseleite.com](https://jesseleite.com)
- [@jesseleite85](https://twitter.com/jesseleite85)
