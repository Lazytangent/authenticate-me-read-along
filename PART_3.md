# Authenticate Me Read-Along Part 3: Heroku Deployment

This reading is meant to accompany Part 3 of the Authenticate Me project that's
set for the end of Week 15 in the Online Curriculum.

## Phase 1: Heroku Connection

If you're on WSL or can't install Heroku on your Mac with Homebrew, use the
`Standalone installation` method, which is just the `curl` command to run an
install script. At the time of writing this reading, the current command for the
standalone installation is

```sh
curl https://cli-assets.heroku.com/install.sh | sh
```

If you're on a Mac, try using the Homebrew method first:

```sh
brew tap heroku/brew && brew install heroku
```

Homebrew might take a moment to update its package list first, which might take
a bit of time.
