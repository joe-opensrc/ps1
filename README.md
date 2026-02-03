### PS1 -- set your bash terminal prompt with ease

A Hideously Functional⁽™⁾ script suite.

#### INSTALL

e.g.,

```bash
mkdir ~/apps/bash
cd ~/apps/bash
git clone https://github.com/joe-opensrc/ps1

# also (optionally) add the following to your profile
source ~/apps/bash/ps1/dotfiles/bashrc_ps1 
```

#### DEPENDENCIES
  bash
  you'll need a true-color $TERM + Symbols Nerd Font (or similar; untested)

#### USAGE

```bash
# to get usage:
ps1 --help 

# generally: 
ps1 -n <int> -e <int>
```

There is autocompletion which uses fzf to present options with a preview

#### ENV Vars

you can use: PS1_COLOR_PRIMARY to set a color for the prompt
Currently expects a 24-bit ansi (escaped) color code:
e.g., "\e[38;2;r;g;bm"
