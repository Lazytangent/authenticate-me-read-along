# Authenticate Me Read-Along

This reading is meant to accompany the Authenticate Me project that's set for
the end of Week 15 in the Online Curriculum.

## Project Setup

The instructions advise you to create an `authenticate-me` folder as the root of
your project with a `backend` and `frontend` folder nested within the root
folder, like so:

```plaintext
authenticate-me
├── backend
└── frontend
```

You should initialize a git repository inside the `authenticate-me` directory,
so that when you push to GitHub, GitHub will show the `backend` and `frontend`
directories in the root of the project. When you first push to GitHub, if all
you've made is the `backend` and `frontend` directories, then nothing will show
up since git will not track empty folders.

## `.gitignore`

The `.gitignore` file is meant to be created at the root of your project.

## Dependencies

Make sure to grab the versions mentioned in the instructions. Using Sequelize v6
is not much different, but the models generated will be different from the code
examples in the instructions, so be wary.

## Sequelize Setup

While the instructions mention that you'll be setting up the
`backend/config/database.js` file, you'll do that after doing two other things
first.

The `.sequelizerc` file needs to go in your `backend` directory, and needs to be
created BEFORE you run the `npx sequelize init` command. If your
`backend/.sequelizerc` file is properly set up, then running the `npx sequelize
init` command should create the following files and folders:

* `backend/config/database.js` - this is the database config file
* `backend/db/migrations/` - this is the migrations folder
* `backend/db/models/` - this is the models folder
* `backend/db/models/index.js` - this is the file that sets up your Sequelize
    instance to interact with your database through your models
* `backend/db/seeders/` - this is the seeders folder

If you find a `backend/db/config.json`, `backend/db/config/config.json`, or
something similar, you'll run into issues with development in just a second when
testing the setup out. There are a few ways to solve this, but the fastest is
probably just to remove the files and folders that were generated by the
Sequelize initialization command, make sure that your `backend/.sequelizerc`
file is set up properly, and run the `npx sequelize init` command again. If this
error continues to occur, call in a TA for assistance.

## `.env` Gets Pushed to GitHub

You can remove the `.env` file from git tracking with `git rm --cached
backend/.env`, which is meant to be run from the root of your project. You
should then run `git status` to check for the removal of the `.env` file, add
and commit as appropriate before pushing again to GitHub. Then, check the GitHub
version of your repository to see if that has removed the `.env` file from
there.

## `req.csrfToken is not a function`

You might run into this error towards the end of `Phase 0`. Because this
application has a different setup than the group project from Module 4, you'll
be applying CSRF a little differently. In your `backend/app.js` file, where you
set up app-wide middleware, make sure that your `app.use(routes)` goes AFTER
your `app.use(csurf(...))` block, since we want the CSRF middleware to be
applied to our route handlers before our Express app has to handle any incoming
requests.

## `apiRouter`

Make sure that you're importing the `apiRouter` into the
`backend/routes/index.js` file and NOT into the `backend/routes/api/index.js`
file.

## ForbiddenError: invalid csrf token

If you're testing the `/api/test` route to test the api router, and getting the
`invalid csrf token` error message, check to see if you have the `XSRF-TOKEN`
header set in your `fetch` call, which you can get as a cookie when you go to
the `/hello/world` route.

## User model methods

Wondering where the instance and static methods should go in the User's model
file? Since they're all adding methods to the User model, they need to be in the
scope of the `User` variable created by the `sequelize.define()` method, so that
means, these methods will need to be defined within the anonymous function being
exported, above the `return User` statement, but outside the invocation of the
`sequelize.define` method. A good place to put them is right above the
`User.associate` method and right below the end of the `sequelize.define`
method.

## Removing user auth middleware routes

Once you are done with Phase 3, you can remove the three routes you created to
test the auth middleware, which are just the `/api/set-token-cookie`,
`/api/restore-user`, and `/api/require-auth` routes.

## `backend/routes/api/index.js`

When the instructions show you what the `backend/routes/api/index.js` file
should look like after you connect the routes, don't forget that you should have
the `/api/test` route in that file.

```js
// backend/routes/api/index.js
const router = require('express').Router();
const sessionRouter = require('./session');
const usersRouter = require('./users');

router.use('/session', sessionRouter);
router.use('/users', usersRouter);

router.post('/test', (req, res) => {
  res.json({ requestBody: req.body });
});

module.exports = router;
```

## Cleaning up the backend

The only route to remove at this point is the `/hello/world` route in the
`backend/routes/index.js` file. Make sure that you do NOT remove the `/api/test`
route in your `backend/routes/api/index.js` file.
