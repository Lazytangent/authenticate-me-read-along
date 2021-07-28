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

## Phase 2: Setting up your Express + React application

When the instructions tell you to "[i]nitialize a `package.json` file at the
very root of your project directory...", it means that you should run `npm init
-y` at the root of your project. That command will generate a `package.json`
will some of the necessary information for Heroku to build your application and
then run it for you. Then, the instructions want you to paste over the `scripts`
that it's given you over the `scripts` key that was made from running the `npm
init -y` command.

When you commit and push this to your GitHub, make sure that you can see all the
files in the backend and frontend directories, only excluding the `node_modules`
directories and the `.env` file in your backend. The `package.json` file in the
root of your project should also be tracked on GitHub. If you are missing files
or have files that shouldn't be tracked, make sure to fix those issues, or your
deployment to Heroku might encounter more issues than it would normally.

## Phase 3: Deploy to Heroku

Since Heroku also supports a `main` branch now, you can push your `main` branch
if that's what your default branch is in your repository. This means that you
can use either

```sh
git push heroku main:master
```

to push your local `main` branch to a `master` branch on Heroku, but you'd have
to use this exact command every time you needed to push to Heroku,

```sh
git push heroku
```

or

```sh
git push heroku main
```

to just push your local `main` branch to a `main` branch on Heroku. Ideally, the
`git push heroku` command should work, as long as you are on your `main` branch
locally.

### Some common errors

Make sure that you have a database set up in your app on Heroku. You can use the
`Heroku Postgres` add-on that Heroku provides to add a database, and this should
also set the `DATABASE_URL` variable in your `Config Vars`.

If you run into some `invalid csrf token` errors on Heroku, but not locally,
check your `Config Vars` under `Settings` on Heroku to see if you have valid
values for `JWT_SECRET` and `JWT_EXPIRES_IN`.

As you deploy your application throughout the week, be sure to run the commands
necessary for migration and seeding if you've added those since the last
deployment to Heroku.
