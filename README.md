# Dotfiles

This repository contains all of my personal dotfiles. such as **`.vimrc`** **`.zshrc`**, **`.Xresources`** and **`i3`**. They are published here on [GitHub](https://github.com/sayems/dotfiles) so I can easily clone them whenever I need them.



&nbsp;

## Table of contents
- [Clone the repository](#clone-the-repository)
- [Ignore The Untracked Files](#ignore-the-untracked-files)
- [Commit Your Changes](#commit-your-changes)
- [Start from scratch](#start-from-scratch)
- [References](#references)


&nbsp;


Clone the repository
--

This repository contains a `.zshrc` file, which you will want to override the
default file created by Zsh. If you need to retain your existing `.zshrc` file,
move it to a different spot:

```sh
mv ~/.zshrc ~/.zshrc.bk
```

Next, ensure that your `.dotfiles` directory will be ignored by Git (to eliminate
recursion issues) by adding to `.gitignore`:

```sh
touch .gitignore
echo ".dotfiles" >> .gitignore
```

Then, clone this repository into your home directory:

```sh
git clone --bare https://github.com/sayems/dotfiles.git $HOME/.dotfiles
```

Checkout the content of the repository into `$HOME`:

```sh
git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME checkout
```

If there are conflicts with existing files, Git will let you know like this:

```
error: The following untracked working tree files would be overwritten by checkout:
    .gitconfig
Please move or remove them before you can switch branches.
Aborting
```

Be sure to back those up first before moving forward.

Restart your shell session to pick up all the new aliases and configurations.

&nbsp;

Ignore The Untracked Files
--

You'll want to tell Git to ignore untracked files when running `git status`,
since this repository will only manage certain hand-picked files in your
home directory:

```sh
dot config --local status.showUntrackedFiles no
```

&nbsp;

Commit Your Changes
--

Suppose you just made a change to your `.zshrc` file and would like to commit it
to your dotfiles repo.

```sh
# See your proposed changes
dot status

# Stage up your changes
dot add .zshrc

# Commit it
dot commit -m "Message goes here"

# Push it up
dot push
```

You'll want to avoid running an "add all" command (like `dot add .` or `dot add -A`)
since only some of the files in the home directory are tracked by Git.

&nbsp;

## Start from scratch

To bring your existing home directory under version control, initialize a bare
git repository there and define an alias to help with managing it:

```sh
git init --bare $HOME/.dotfiles
alias dot='/usr/local/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dot config --local status.showUntrackedFiles no
```

Be sure to add the alias to `.zshrc`, either manually or like this:

```sh
echo "alias dot='/usr/local/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'" >> $HOME/.zshrc
```

Now, you can run ordinary git commands in your home directory using your newly
created `dotfiles` alias:

```sh
dot status
dot add .zshrc
dot commit -m "Add zshrc"
dot push
```

&nbsp;

References
--
- [Tracking dotfiles directly with Git](https://wiki.archlinux.org/index.php/Dotfiles#Tracking_dotfiles_directly_with_Git)
- [Hacker News: Dotfiles](https://news.ycombinator.com/item?id=11070797)
- [The best way to store your dotfiles](https://www.atlassian.com/git/tutorials/dotfiles)
