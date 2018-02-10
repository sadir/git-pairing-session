# Git Pairing Session

A mini set of shell scripts to enable you to take advantage of [commits with coauthors](https://github.com/blog/2496-commit-together-with-co-authors).

## Why pair?

See my [blog post](https://tech.nested.com/) on the benefits of pair programming.

## Installation

1. Clone this repo into your home directory.

```
git clone https://github.com/sadir/git-pairing-session.git $HOME/
```

2. Add the `git-pairing-session` script to your bash config (e.g. in `~/.bash_profile` or `~/.bashrc`).

```
source $HOME/git-pairing-session/git-pairing-session
```

3. Set up your project to be ready for pairing sessions, by running this command in the root of your project (where your `.git` directory is).

```
pairing_project # symlinks a git hook to append authors to your commit messages.
```

Note: this will ask your permission to override your current `prepare-commit-msg` git hook if you have one.

4. Setup your `$PAIRS_FILE` so `git-pairing-session` knows who you can pair with. By default this file should be in the directory you cloned this repo into.

```
cp .pairs.json.example .pairs.json
# add your colleagues
# optionally remove me :(
```

Note: [your colleagues email addresses must match their github email](https://help.github.com/articles/creating-a-commit-with-multiple-authors/).

5. Get pairing with someone!

```
pairing_with ms # hand it a set of initials you set up earlier
```

6. When you're done, stop pairing.

```
no_longer_pairing # the lone wolf returns
```

## Customisation

Set these variables after you `source` this repo to override and configure where things live:

```
export GIT_PAIR_SESSION_DIR=$HOME/git-pairing-session
export COAUTHOR_FILE=$GIT_PAIR_SESSION_DIR/.coauthor.json
export PAIRS_FILE=$GIT_PAIR_SESSION_DIR/.pairs.json
```

## Why this repo? Why not `other-repo`?

I had a look at a few of these:

* [pivotal/git-scripts](https://github.com/pivotal/git_scripts)

This one randomly attributes the commit to one member of the pair. I wanted each commit to be attributed to both.

* [chrisk/git-pair](https://github.com/chrisk/git-pair)

This one put both co-authors in as the commiter but that broke the way that github represented commiters. Git the vcs wasn't set up for that.

* [peterjwest/git-pair](https://github.com/peterjwest/git-pair)

Similar to git-pair, with added downsides of not being maintained and I quite wanted something in shell script rather than JS.
