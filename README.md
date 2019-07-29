# dirjump

Easily jump to recently used directories with
[oh-my-zsh's 'd'](https://superuser.com/a/664139/943615)-like directory history
that still saved whenever you exit the terminal.

## Usage

### Main Feature

- Show the list of 10 most recent used directory with [`d`](#change-the-main-command).
 
- Jump to any directory in the list by [typing the number](#alternative-command-to-jump) of the directory in the list. You need to use 0 instead of 10 to jump to the 10th and last directory.

- A directory path will be put to the top of the list every time you use [`v`](#i-dont-use-vim)([vim](https://www.vim.org/about.php))  to edit files or `o`([xdg-open](https://linux.die.net/man/1/xdg-open)) to open a file from that directory. Or if you like, [every time you visit a directory](#always-put-visited-directory-to-the-history).

### Additional Feature

- Automatically list all files in the directory you jumped to if it contains 30 or fewer files. You can [turn it off](#dont-list-files-after-jump) if you like.
        
## Personal Preference

You can modify the code to suit your needs. If you follow the [installation guide](#installation), it is located in `~/.config/dirjump/dirjump`.

### Change the main command

You can change the main command from `d` to another by modifying [the code](https://github.com/imambungo/dirjump/blob/master/dirjump#L3) below:

```bash
dirjump_command="d"
```

### Alternative command to jump

By default, you can also jump with `<main command> <directory number>`:
```
d 8
```
If you already used any number as aliases, just delete or comment out the code from [line 12 to 22](https://github.com/imambungo/dirjump/blob/3ea9b91485a8b2b217d411b0c7eb3cad1821a483/dirjump#L12).

### I don't use Vim

You can make a spesific command trigger dirjump to put your current directory to the directory history by adding the following line to the end of the script:

```
alias <yourcommand alias>="propose_dir_path && <yourcommand> " # make sure you put a space before the closing double quote
```

Here's an example to make `vsc` an alias of [`code`](https://askubuntu.com/a/852086/356625)(Visual Studio Code):

```bash
alias vsc="propose_dir_path && code "
```

### Always put visited directory to the history

If you want dirjump to always put visited directory to the history, add the following snippet to the end of the script:

```bash

# If using Zsh
if [ -n "$ZSH_VERSION" ]
then
	# Source: https://stackoverflow.com/a/3964198/9157799
	chpwd_functions=(${chpwd_functions[@]} propose_dir_path)
else
	cd()
	{
		builtin cd "$@" # https://unix.stackexchange.com/a/366974/307359
		propose_dir_path
	}
fi
```

### Don't list files after jump

[Here](https://github.com/imambungo/dirjump/blob/3ea9b91485a8b2b217d411b0c7eb3cad1821a483/dirjump#L99), just delete it.

## Installation

1. Download the script

        curl --create-dirs -o ~/.config/dirjump/dirjump https://raw.githubusercontent.com/imambungo/dirjump/master/dirjump

2. Source the script to your shell

        echo 'source ~/.config/dirjump/dirjump' >> ~/.bashrc

   If you use Zsh:

        echo 'source ~/.config/dirjump/dirjump' >> ~/.zshrc

## Uninstallation

1. Delete the script and the directory history file

        rm -rf ~/.config/dirjump

2. [Unsource](https://stackoverflow.com/a/5413132/9157799
) the script from your shell

        grep -Fxv "source ~/.config/dirjump/dirjump" ~/.bashrc > temp; mv temp ~/.bashrc

   If you use Zsh:
   
        grep -Fxv "source ~/.config/dirjump/dirjump" ~/.bashrc > temp; mv temp ~/.zshrc
