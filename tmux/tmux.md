# Introduction to tmux
## What is tmux?

tmux is short for "terminal multiplexer", and it’s a highly valuable tool for anyone who often works in a command-line environment. It allows users to switch effortlessly between several programs in one terminal, save sessions for later, or even split them into panes for simultaneous viewing.
Why use tmux?

Here are a few reasons why tmux is particularly helpful:

    Session Persistence: You can detach from a session and leave it running in the background, and then reattach to it later. This is useful if you're running long tasks or need to keep a session active even when you're not actively using it.

    Multiple Windows and Panes: Within a single tmux session, you can have multiple windows, each with its own command-line interface. Furthermore, each window can be split into multiple panes, making it easy to work on several things at once without the need for multiple terminal instances.

    Remote Work: When working on remote servers through SSH, network disruptions can be frustrating as they cause you to lose your active terminal session. With tmux, you can reattach to the session and pick up exactly where you left off.

    Customization and Scripting: tmux can be heavily customized to suit your workflow, and you can automate numerous tasks through scripts.

## Basic Commands

    tmux: Start a new tmux session.
    tmux new-session -s mysession: Start a new session with the name “mysession”.
    tmux attach -t mysession: Attach to an existing session named “mysession”.
    tmux ls: List all running tmux sessions.
    Ctrl-b followed by %: Split the window vertically into panes.
    Ctrl-b followed by ": Split the window horizontally into panes.
    Ctrl-b followed by d: Detach from the current session.
    Ctrl-b followed by c: Create a new window.
    Ctrl-b followed by n: Switch to the next window.
    Ctrl-b followed by p: Switch to the previous window.

## Configure tmux 

put the [.tmux.conf](./.tmux.conf) file in your home directory. If this doesn't automatically
install all plugins you will need to install the plugin manager manually: 

Install the Tmux Plugin Manager:

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```