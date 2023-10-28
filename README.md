<h1 align="center">Zellij Smart Sessionizer</h1>

<div align="center">
  <strong>Zellij sessionizer with layout selection capability</strong>
</div>

<div align="center">
    Instant Zellij session startup powered by Zoxide and fzf
</div>

## Table of Contents

- [Key Features](#key-features)
- [Installation](#installation)
- [Usage](#usage)
- [Inspirations](#inspirations)

## Key Features

- **Easy to use:** Run `zs` or `Ctrl+f` in your shell select your project from [`Zoxide`](https://github.com/ajeetdsouza/zoxide) list using [`fzf`](https://github.com/junegunn/fzf), select preferable layout;
- **Usage inside zellij session:** It will create a new tab with the selected layout;
- **Attach to the session:** Will not ask for layout when the session was previously created;
- **Layout config preview:** Layout config preview will be shown using [`bat`](https://github.com/sharkdp/bat) if installed or `cat` as a fallback

## Installation

1. Install all dependencies

   - [Zoxide](https://github.com/ajeetdsouza/zoxide)
   - [fzf](https://github.com/junegunn/fzf)
   - [bat](https://github.com/junegunn/fzf) - optional dependency

2. Clone the repo

```
git clone https://github.com/demestoss/zellij-smart-sessionizer
cd zellij-smart-sessionizer
```

3. Place [zellij-smart-sessionizer](https://github.com/demestoss/zellij-smart-sessionizer/blob/master/zellij-smart-sessionizer) script in your `PATH`. One of the ways:

```
sudo chmod +x ./zellij-smart-sessionizer
sudo ln -s $(echo "$(pwd)/zs") /usr/bin/zellij-smart-sessionizer
```

4. Populate your `Zoxide` database by simply going into the directories that you want to start the session from. Check [`Zoxide`](https://github.com/ajeetdsouza/zoxide) docs for more info.

_Quick tip_: If you want to remove some paths from your `Zoxide` DB you can use this simple command:

```sh
zoxide remove $(zoxide query -l | fzf -m)
```

Select options that you want to remove by pressing `Tab` and they will be deleted from DB

5. (Recommended) I like to create alias for the script to have an ability to easily execute it. Place it into your shell's `.rc` file:

```sh
alias zs="zellij-smart-sessionizer"
```

6. (Optional) Create an alias to call this script in your shells `.rs` config

```sh
bindkey -s ^f "zellij-smart-sessionizer^M"
```

## Usage

You just need to type this command in your shell to start a new session

```sh
zellij-smart-sessionizer

// or just this command if you have done (5) step of installation process

zs
```

Or `Ctrl+f` if you've set up an optional keybinding step

Next will be provided different types of scenarios of the script execution.

### Outside of Zellij (session doesn't exist)

You will be offered paths from `Zoxide`. After selection, it will give you a layout selection for the session if your layout directory is not empty. It uses the `LAYOUT DIR` path provided to `Zellij` setup.

After that, it will open a session with a zoxide path's `basename` and selected layout.

### Outside of Zellij (session exists)

You will be offered paths from `Zoxide`. After selecting a path, the layout step will be skipped and you will be attached to `Zellij` session.

### Inside Zellij

If you run this script inside `Zellij` you will be offered the same selection steps. But after selection, it will open a new tab with the selected session `basename` and Layout

_Feature_: Not all layouts will be provided in this case, It's kinda smart and will not provide layouts that contain `tabs` options inside it, because you cannot create tabs inside the tab.

## Passing session name argument

Also, you can provide optional arguments to the script

```sh
zellij-smart-sessionizer session-name

// or

zs session-name
```

It will pick up this argument and will init session with this name instead of the path's `basename`. It's very useful if you want to have several different sessions that were initialized from the same directory

## Next steps of this repo

Currently I'm working on Zellij plugin to integrate with Zellij in a better way and have ability to switch sessions inside Zellij

## Inspirations

Special thanks to this repos:

- [zellij-sessionizer](https://github.com/silicakes/zellij-sessionizer/tree/main)
- [t](https://github.com/joshmedeski/t-smart-tmux-session-manager)

## License

[MIT](https://tldrlegal.com/license/mit-license)
