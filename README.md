# Git Pairing Session

A mini set of shell scripts to enable you to take advantage of [commits with coauthors](https://github.com/blog/2496-commit-together-with-co-authors) in Github.

![github coauthored commit screenshot](https://i.imgur.com/2Yu1IdT.png)
## Why pair?

See my [blog post](https://tech.nested.com/) on the benefits of pair programming.

## Why record coauthors?

  * [Chris Beams](https://chris.beams.io/posts/git-commit/) does a great job of explaining why good git commits are important. Git coauthors extend all the points he makes.
  * Those sweet, sweet, contribution points. :green_heart:

## Installation

1. You'll need to install [jq](https://stedolan.github.io/jq/).

```
brew install jq
```

2. Clone this repo into your home directory. :house:

```
git clone https://github.com/sadir/git-pairing-session.git $HOME/
```

3. Add the `git-pairing-session` script to your bash config (e.g. in `~/.bash_profile` or `~/.bashrc`).

```
source $HOME/git-pairing-session/git-pairing-session
```

4. Setup your `$PAIRS_FILE` so `git-pairing-session` knows who you can :pear: with. By default this file should be in your `$HOME/git-pairing-session` directory where you cloned this repo.

```
cp .pairs.json.example .pairs.json
# add your colleagues
# optionally remove me :(
```

Note: [your colleagues email addresses must match their github email](https://help.github.com/articles/creating-a-commit-with-multiple-authors/).

## Usage

There are two options:

  1. Record your coauthor as you go.
  2. Retrospectively modify your branch to add your coauthor to every commit.

### Option 1

1. Set up your project to be ready for recording coauthors as you go, by running this command in the root of your project (where your `.git` directory is).

```
pairing_project # symlinks a git hook to append authors to your commit messages.
```

Note: this will ask your permission to override your current `prepare-commit-msg` git hook if you have one.

2. Get pairing with someone! :muscle:

```
pairing_with ms # hand it a set of initials you set up earlier
```

3. When you're done, stop recording your coauthor.

```
no_longer_pairing
```

4. Eat more fruit :pear: :grapes: :tangerine: :green_apple: :banana: :cherries:

### Option 2

1. Do your work, blissfully unaware that you've forgotten to record your coauthor.

2. Retrospectively amend your branch to add coauthors.

```
paired_with ms
```

3. Eat more fruit :pear: :grapes: :tangerine: :green_apple: :banana: :cherries:

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
