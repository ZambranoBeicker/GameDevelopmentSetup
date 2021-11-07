# Game Development Setup: Linux, NeoVim & Unity


This setup isn't so difficult but you can spend a lot of time figuring out what to do and where to find the info so first of all let's list the things we need:

* [MonoDevelop](#MonoDevelop)
* [Omnisharp server (Roslyn)](#OmniSharp Server)
* [Neovim Plugins for LSP](#Neovim Plugins for LSP)
* [Considerations](#Considerations)

That will be all for now and it'll work

# MonoDevelop

Just go to the [download page](https://www.mono-project.com/download/stable/#download-lin) and follow the steps to install Mono

# Omnisharp server

This is the server you will need to enable autocompletion. You need to have it installed, and there are some ways but the one that worked for me was just going to the repo and download a [ release file ](https://github.com/OmniSharp/omnisharp-roslyn/releases)

Then extract it into the folder of your preference and you will get some files and directories. The one you need is called "run". So now we'll use the full path to this file to setup our LSP and NeoVim autocompletion

# NeoVim Plugins for LSP

In NeoVim there are many ways to use autocompletion. I liked to use LSP because of its velocity. To use LSP autocompletion for Unity
you will install these two plugins:

- `Plug 'neovim/nvim-lspconfig'`
- `Plug 'hrsh7th/nvim-compe'` 

You can read those repos to find more info about how to use LSP.

Now that we have our plugins and have installed the OmniSharp server we need to copy a [ configuration for OmniSharp completion ](https://github.com/neovim/nvim-lspconfig/blob/master/CONFIG.md#omnisharp).

We have a step done that is the server installed, so now you just need to change the line that says: `local omnisharp_bin = "/path/to/omnisharp-repo/run"` for the current path of the file I told you before (the "run" file). And that will be all

You may have an error with the assembly references, if so you can try the solution in [ this reddit thread ](https://www.reddit.com/r/neovim/comments/jq1cbr/neovimlsp_omnisharpvim_c_what_am_i_doing_wrong/). It consist in just changing a line in that file:

>TL;DR: in the starter script of Omnisharp change the line bin_dir=${base_dir}/bin to bin_dir=/usr/bin (or whatever the location on your system might be).


# Considerations

Sometimes you will need to recreate the packages for Unity. One error I experimented was when I renamed a file, Neovim just couldn't find Assembly References and the autocompletion stopped only for Unity classes. So I needed to go to `Edit > Preferences > External Tools` and regenerate all the `.csproj` for Unity and then everything started to work properly
