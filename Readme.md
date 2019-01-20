<img src="design/logo.svg" height="150" />

# GITSI
## Git Status Interactive

### Usage

```bash
# Run with a rspecific repository
gitsi ~/Development/Code

# The current directory is a repository
gitsi
```

### What is it
Gitsi  is  a  simple  wrapper around git status and git add It provides an easy terminal UI that is optimized for staging, unstaging, and deleting files and changes between the git index, workspace and untracked files.

There are many useful features such as quick jumping to sections, filtering, running `git add -p` diffing, and quick navigation.

Gitsi displays all your changes and untracked files in a list with the index, workspace, and untracked sections. Just like git status However, you can navigate this this interactively much like vi / vim.  Which makes it much easier to quickly jump to the one file you'd like to add or the one file you'd like to move back from the index to the workspace.

### See it in action

FIXME

### Shortcuts

The following shortcuts are also explained within `gitsi` in a help section at the bottom.

#### NAVIGATION

- `j`      move one line down
- `k`      move one like up
- `C-d`    Jump half a page down
- `C-u`    Jump half a page up
- `!`      [Shift 1] Jump straight to the index section of the git status output.
- `@`      [Shift 2] Jump straight to the workspace section of the git status output.
- `#`      [Shift 3] Jump straeight to the untracked files section of the git status output.
- `G`      Jump to the bottom of the list.
- `g`      Jump to the top of the list.
- `q`      Quit

#### SEARCHING

- `/`      Enter the search / filter mode. Hit return to apply the filter and ESC to cancel the filter.  If a filter has been applied, hit `/` again to edit it again.
- `ESC`    Cancel the current search or visual mark mode.
- `Enter`  Apply the current search.

#### ACTIONS

- `s`      Add file or stage (depending on context).
- `u`      Unstage file or delete file (depending on context).
- `m`      Mark selected file.
- `V`      Toggle visual mark mode. Moving around will mark files
- `S`      Stage / Add all marked files.  This will also unmark all marked files.
- `U`      Unstage / delete all marked files.  This will also unmark all marked files.
- `d`      Switch to a git diff of the selected file
- `i`      Run a interactive add `git add -p1
- `c`      Run `git commit`
- `C`      Run `git commit --amend`
- `x`      Delete all changes to this file. The same as `git checkout -- name-of-file`

The `j/k/C-d/C-u` commands can be repeated by entering numbers before the actual command, like vim. i.e. `12j` would jump down 12 lines.

## Installation

### macOS

### Ubuntu
apt-get install make
apt-get install libgit2-dev
apt-get install libncurses-dev

## Development

This is the first pure C project I finished since around 2004. I'm sure there're tons of bugs. If you find an issue, feel free to point it out.

If you build it in debug mode, it will create `/tmp/gitsi.log` and you can use the `gitsi_debug_str` function to write to this log.

For testing on Linux, if you're on a Mac, there's `res/Dockerfile` that adds clang, valgrind, etc. It can be run via:

``` bash
# assuming you build the docker image via `docker build . --tag=gitsi:dev`
docker run -it --mount type=bind,source="$(pwd)"/gitsi,target=/code gitsi:dev bash
```

### Valgrind

Valgrind is a good way of detecting memory leaks. Running it looks like this:
``` bash
valgrind --leak-check=full \
         --show-leak-kinds=all \
         --track-origins=yes \
         --verbose \
         --log-file=valgrind-out.txt \
         ./gitsi REPO-DIR
```

## Open Issues

- [Maybe] Split up into multiple files
- Add git stash support, especially for stashing individual files
- Mark all
- Clear all marks
- git commit -a
- [Maybe] add to homebrew
- [Maybe] a config file (line numbers on off, color on off, etc)
- Better error handling (calloc fail, git fail, etc)