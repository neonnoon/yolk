![image](./img/yolk.png)

A simple dotfile manager, no magic, just `yolk`.


### Install

The easiest way to install `yolk` is with [Homebrew](http://brew.sh):
```
brew tap neonnoon/brew https://github.com/neonnoon/brew
brew install yolk
```

But of course, you can also clone this repo or download the `yolk` script and put it somewhere in your path.


### Getting Started

Clone a repo and initialise `yolk`:
```
yolk init <YOUR_DOTFILE_REMOTE_REPO>
```

`yolk` does not do any changes to your local files yet, but shows you missing or changed files:
```
$ yolk status
CHANGED .changed-file
MISSING .missing-file
```

You can now edit as much as you want and `yolk save` or `yolk restore` your files, to save and restore, exactly.

If you want to start tracking your changes with `yolk`, just do so:
```
yolk track .new-file
```

You can, of course, also stop tracking a file. This will keep the file in your home, but will not track it anymore in your git repo.
```
yolk untrack .a-file
```


### How it Works

`yolk` doesn't do any magic, it uses a bare git repository in `~/.dotfiles`  (or where ever you like) to store and version your configuration files. It basically treats your whole home directory as a git repository -- but only when you want to (by using `yolk`), and only for what you want to (by using a `.gitignore` file that ignores everything).

### Encrypted Files

Sometimes you might want to track files that contain sensitive information like a password, but clearly you wouldn't want this information to end up in clear text in your git repo. `yolk` can use [git-crypt](https://github.com/AGWA/git-crypt) to encrypt files (optional). Run `yolk crypt` to prepare your repo and `yolk track -e <FILE>` to track files without exposing sensitive information.

### Advanced Stuff

If you have added something to your repo that you didn't want to, let's say a file containing sensitive information, `yolk untrack` is not enough as it will keep the file's history. You will have to completely delete the history with:
```
yolk forget .file-that-should-not-be-in-your-repo
```

Not enough? You can always use `yolk git` to perform any git command you like.
