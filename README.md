# gt - fast directory jumping

With `gt` (<u>g</u>o <u>t</u>o), fly in the terminal, with completion.

- [Example](#example)
- [Usage](#usage)
- [Tmux users](#tmux-users)
- [Installation](#installation)

## Example

![gt-gif](gt.gif)

```
> article % gt add belief
Alias 'belief' successfully added.
> article % gt
belief   ->  /Users/gsprd/Documents/phd/work/belief/article
des      ->  /Users/gsprd/Desktop
dot      ->  /Users/gsprd/.dotfiles
exam     ->  /Users/gsprd/Documents/phd/teaching/info/exam
gt       ->  /Users/gsprd/Documents/projects/gt
> article % gt remove exam
Alias 'exam' successfully removed.
```

## Usage

- List aliases with `gt` or `gt show`.
- Add alias to the current directory with `gt add ALIAS`.
- Jump to this directory with `gt ALIAS`.
- Remove an alias with `gt remove ALIAS`.
- Update an alias to the current directory with `gt update ALIAS`.
- Rename an alias with `gt rename ALIAS ALIAS`.
- Open your file browser to an alias with `gt open ALIAS`.
- Remove all broken aliases with `gt clean`.

```sh
> gt -h
Usage: gt [-h/--help]
Usage: gt show [ALIAS]

Usage: gt add ALIAS
Usage: gt remove ALIAS
Usage: gt update ALIAS
Usage: gt rename ALIAS ALIAS
Usage: gt open ALIAS
Usage: gt clean

Usage: gt [-t/--tmux] [-c/--current] ALIAS
Usage: gt config KEY [VALUE]
```

## Tmux users

Start, switch and attach tmux sessions seamlessly by switching `tmux on`
```sh
gt config tmux on
```

Now, `gt ALIAS` joins a named tmux session directly at the directory
pointed by `ALIAS`. It attaches if the session already exists!

You can force stay outside of tmux, or in the current tmux session, with the
`-c` flag
```sh
gt -c ALIAS
```
Similarly, when `tmux` is configured to `off`, you can force join a `tmux`
session with the `-t` flag
```sh
gt -t ALIAS
```

When you changed directory within tmux, you can go back to the base directory
with
```sh
gt .
```

## Installation

Download the executable with
```sh
mkdir -p ~/.config/gt
curl https://raw.githubusercontent.com/glambrechts/gt/main/gt > ~/.config/gt/.gt
```

Create the command by adding the following alias to your `~/.bashrc` /
`~/.zshrc`.
```sh
alias gt='source ~/.config/gt/.gt'
```

Setup completion in `zsh` with
```zsh
compdef '_files -W "/Users/gsprd/.config/gt"' .gt
```
or in `bash` with
```bash
_gt() {
    local cur files
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"
    files=$(ls ~/.config/gt)
    COMPREPLY=( $(compgen -W "${files}" -- ${cur}) )
}
complete -F _gt gt
```
