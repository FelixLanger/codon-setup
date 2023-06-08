# Introduction to Zsh
## What is Zsh?

Zsh, or Z Shell, is an extended version of the Bourne Shell (sh), with many new features, and support for plugins and themes. Since it's based on the same scripting syntax as the older shell, bash, it's usually easy to switch. Zsh is highly popular among developers and system administrators due to its powerful features such as better auto-completions, spell correction, and improved globbing.
Why use Zsh?

-   Auto-suggestions: Zsh can suggest commands as you type based on your history and the existing commands which are very helpful.

-    Theme Support: Zsh supports themes which can make your terminal much more visually appealing.

-    Plugin Support: You can add plugins for popular tools like git, Docker, and many others that can greatly speed up your workflow.

-    Improved array handling and path expansion: This is especially useful for scripting.

## Installing Zsh

zsh is installed on codon under 
```
/usr/bin/zsh
```

## Oh My Zsh

Oh My Zsh is an open-source, community-driven framework for managing your Zsh configuration. It comes with a ton of helpful functions, plugins, helpers, themes, and a few things that make your terminal look fantastic.
Installing Oh My Zsh

Via curl: 
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" 
```

Via wget:
```bash
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

This will automatically set up Oh My Zsh and change your default shell to Zsh.
It is not recommended to use zsh as the default shell, therefore we will just revert this by using
```bash
chsh -s /bin/bash
```
and just set our default shell inside tmux to be zsh. This way we use zsh for all interactive sessions but don't run into troubles which could occur when bash is expected to be the default shell.

## Powerlevel10k Theme

Powerlevel10k is a theme for Zsh that’s an extension of another popular theme, powerlevel9k, and it's highly customizable and really fast.
### Installing Powerlevel10k Theme

First, make sure you have Oh My Zsh installed.

Clone the repository:
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
Set the theme in your ~/.zshrc. :
```
ZSH_THEME="powerlevel10k/powerlevel10k" 
```
Restart Zsh by just typing zsh in the terminal.

The first time you do this, you'll be prompted to go through the configuration wizard which will allow you to customize your prompt.