Yes, yes, I'm aware that this is a stupid name, but will you shut up man

**This does not work on windows, thanks to windows not being POSIX complaint**

## What is todo-me-daddy?
The whole idea of this plugin is that we as developers leave hundreds, and
hundreds of TODO comments in our code, and there is no way to find them, other

then grepping them.

Well this plugin makes the finding of to-do's easy.

What this plugin does is a few;, different options:
1. Output every to-do found to telescope (this can also include to do's found in markdown, by default that option is off)
2. Key bind to complete a to do in markdown
3. I have more plans for the future but in order to check them out, check out the [TODO.md](https://github.com/yonikosiner/todo-me-daddy/blob/master/TODO.md)

**Right now the plugin only outputs to telescope**

## Current bugs
You need to have ignore_folders added with at least one folder, check out why. [ignore_folders](#Options)
## Warning
Please refer to the ignore list, as of right now you need something in there otherwise the plugin will error
## Setup
Add this to your `init.vim` (change it depending on what package manger you use)

```vim
Plug 'yonikosiner/todo-me-daddy'
```

In your `telescope.lua` add:

```lua
require("telescope").load_extension('todo_me_daddy')
```

Then where you set your remaps add this
```vim
" We have to call the telescope exteion todo_me_daddy not todo-me-daddy, as lua goes mad at as if we use - in the string below
nnoremap <leader>td :lua require('telescope').extensions.todo_me_daddy.todos()<CR>
" This option will allow us to get to do's which are asigend to you (the to do will have your name in it such as TODO(bob), is a to do for Bob)
nnoremap <leader>tm :lua require('telescope').extensions.todo_me_daddy.your_todos()<CR>
" This will allow you to be on the line of a markdown to do and complete with a keybinding of your choice
nnoremap <leader>m :lua require("todo-me-daddy").complete_markdown_todo()<CR>
```

### Options
This plugin is configured 100% with lua. Wherever you want in your lua config add this

```lua
require("todo-me-daddy").setup{
    get_markdown_todo = false, -- The default for for this is false, what this does is as well as getting your to do comments this will also grab any to dos from a markdown file
    your_name = "", -- There is an option you can call to get all the to do's which are asigend to you, in order for this to work you must enter in your name (the name that is used when to do's in code are asgined to you).
    ignore_folders = { -- This allows you to tell todo-me-daddy to not search certin folders for to do's, there needs to be at least something in there or the plugin will glitch right now (I'm working on a fix for this), but you can add as many ignore folders as you want. There will be an option added to the telescope option to only ignore files on each call. This only works with one folder at the moment...
        node_modules = "node_modules",
    }
}
```
