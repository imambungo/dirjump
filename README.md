# dirjump

Easily jump to recently used directories with
[oh-my-zsh's 'd'](https://superuser.com/a/664139/943615)-like directory history
that still saved after exiting the terminal.

## Installation

### Download the script

```bash
curl --create-dirs -o ~/.config/dirjump/dirjump https://raw.githubusercontent.com/imambungo/dirjump/master/dirjump
```

### Source the script to your shell

#### Bash

```bash
echo 'source ~/.config/dirjump/dirjump' >> ~/.bashrc
```

#### Zsh

```bash
echo 'source ~/.config/dirjump/dirjump' >> ~/.zshrc
```

## Uninstallation

### Delete the script and the directory history file

```bash
rm -rf ~/.config/dirjump
```

### Unsource the script from your shell

#### Bash

```bash
grep -v "source ~/.config/dirjump/dirjump" ~/.bashrc > temp; mv temp ~/.bashrc
```

#### Zsh

```bash
grep -v "source ~/.config/dirjump/dirjump" ~/.bashrc > temp; mv temp ~/.zshrc
```
