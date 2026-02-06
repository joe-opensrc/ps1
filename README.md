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
  bash \
  You'll need a true-color $TERM + Symbols Nerd Font (or similar; untested)

#### USAGE

```bash
# generally: 
  ps1 -n <int> -e <int>

# to get usage:
> ps1 --help 

  ps1 [-CDPT] [-a <any_str>] [-c <caret_str>] [-d] [-e <index>] [-lm] [-n <index>] [-p <string>] [-z]

    -C          := print available carets
    -D          := sets a variable I use elsewhere (BASH_DEBUG_PRECLEAR), you can probs ignore this ;)
    -P          := print the available prompt stack
    -T          := modify PROMPT_DIRTRIM; there for convenience
    -a <string> := prefix arbitary string to the caret string
    -c <string> := specficy a caret directly / manually
    -d          := deac; deprecated (in the initial release ;D)
    -e <index>  := choose a predefined caret by index (int)
    -m          := set a minimal ascii prompt, namely: "> "
    -n <index>  := choose a predefined prompt by index (int)
    -p <string> := specficy a prompt directly / manually
    -z          := print the prompts in a way that fzf can display
    

```

There is autocompletion which uses fzf to present options with a preview

#### ENV VARS

You can use: PS1_COLOR_PRIMARY to set a color for the prompt \
Currently expects a 24-bit ansi-escaped color code: \
e.g., "\e[38;2;r;g;bm"

Bonus function:

```bash
hex_to_ansi () {
  rgb=${1:1}
  argb=$( for cpi in $(seq 0 2 $(( ${#rgb} - 1 ))); do printf '%d;' "0x${rgb:${cpi}:2}"; done);
  argb="${argb%;}"
  echo "\033[38;2;${argb}m"
}
```

So you can go:

```bash
export PS1_COLOR_PRIMARY="$( hex_to_ansi '#476c3d' )"
# which is the same as
export PS1_COLOR_PRIMARY="\033[38;2;71;108;61m"
```

Or, if you're feeling "ADHD", and have pastel installed, you can go:

```bash
export PROMPT_COMMAND+=( 'PS1_COLOR_PRIMARY="$(pastel random -n1 | pastel format ansi-24bit-escapecode)" ps1 -n7 -eR' )
```

more pastel + fzf related examples:

```bash
PS1_COLOR_PRIMARY="$(
  for x in $( pastel list | sort )
  do 
    echo -e "$( pastel format ansi-24bit-escapecode ${x} )${x}"
  done | fzf --ansi -s --cycle --reverse \
       | pastel format ansi-24bit-escapecode -)" \
         ps1 -n7 -eR
```

```bash
PS1_COLOR_PRIMARY="$(
  for x in $( pastel random -n 1000 | sort -V )
  do 
    echo -e "$( pastel format ansi-24bit-escapecode ${x} )${x}"
  done | fzf --ansi -s --cycle --reverse \
       | pastel format ansi-24bit-escapecode -)" \
         ps1
```
