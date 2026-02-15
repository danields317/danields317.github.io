# Configuration

Neovim is configured and customized by running a startup file each time Neovim is started.
The location of the startup file can be found by running the following command in Neovim:

```ps
:echo stdpath("config")
```

The file can either be called `init.vim` or `init.lua` depending on the preferred language.
Lua will be used in this guide since it is the modern standard.
Vim settings can be altered by finding the setting name and setting the correct value. All basic settings are found underneath the `vim.opt` namespace.

```lua
vim.opt.number = true
vim.opt.relativeNumber = true
```

## Plugin management

It is possible to manually install and manage each plugin you want to use in Neovim, but this is cumbersome and error prone. So using a plugin manager is recommended.
I will be using `Lazy.nvim` as plugin manager. Basic `Lazy.nvim` installation instructions are found on the website. One important feature of Lazy to mention is the way plugin configuration works.
A plugin is defined by specifying its name (usually mentioned on the GitHub repo of the plugin). Additional configuration for the plugin is done in the `config` field which always consists of a function call and inside of it all logic that needs to be tweaked. Usually the plugin documentation mentions the code that should be put inside of the function body.

```lua
{
        "rebelot/kanagawa.nvim",
        config = function () -- Simple config where the colorscheme is set
            vim.cmd.colorscheme("kanagawa-wave")
        end,
},
{
        "nvim-treesitter/nvim-treesitter",
        config = function () -- more complex config where the plugins own settings are changed. 
            require("nvim-treesitter.configs").setup({
                ensure_installed = { "c", "lua", "vim", "vimdoc", "query" },
                auto_install = true,
                highlight = {
                    enable = true
                },
                incremental_selection = {
                    enable = true,
                    keymaps = {
                        init_selection = "<Leader>ss",
                        node_incremental = "<Leader>si",
                        scope_incremental = "<Leader>ssi",
                        node_decremental = "<Leader>sd",
                    },
                },
            })
        end
      }

```

## Treesitter

Treesitter is a build-in tool in Neovim that is capable of scanning text and returns pattern information about the text. For Treesitter to work properly, modules for specific (programming) languages need to be installed. This can easily be done with the `nvim-treesitter` plugin. Although Treesitter is available by default, this plugin helps manage and configure the usage of Treesitter. The example at plugin management shows how to install it.

## LSP

The language server protocol (LSP) is a protocol that defines a standard way in which a server that gives programming language support should be written and how a client should be able to connect with it. Neovim contains an LSP client by default, but it is recommended to interact with it through the `nvim-lspconfig` plugin.

### Mason

It is possible to manually install the LSP servers, but this is cumbersome. Mason is a plugin that can install LSP servers for you.

### LSPConfig

LSPConfig is a plugin that contains sensible defaults for most LSP servers.

### MasonLspConfig

This plugin bridges the gap between Mason and LspConfig since sometimes there are some differences in which LSP Mason will install and the settings configured in LSPConfig.

## Buffers, Windows and Tabs

Buffers store text in memory, the content of a buffer can be displayed in a window. Tabs are containers for windows, having the ability to hold multiple windows.
A window reads a specified buffer (usually a file) and a window can be instructed to point to a different buffer to read other data. Multiple tabs can be created all containing their own windows. This allows you to have different layouts and workspaces stored per tab.
