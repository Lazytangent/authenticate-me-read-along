# Authenticate Me Read-Along Part 2: Frontend

This reading is meant to accompany Part 2 of the Authenticate Me project that's
set for the end of Week 15 in the Online Curriculum.

## Phase 0: Set Up

After running the `npx create-react-app` command to bootstrap your React app,
check in your `frontend` directory for a `.git` directory. If you don't find
one, that's great! If you do happen to find one there, go ahead and remove it.
You can use `rm -r frontend/.git` from the root of your Authenticate Me project
to remove the `.git` directory in your `frontend` directory with your terminal.
If you make a commit where that nested `.git` folder still exists, git will stop
tracking your `frontend` directory since it will think that your `frontend`
directory is another repository and GitHub will not show the files nested
within the `frontend` directory.


### Method 2: Use Redux template

If you intend on using the `react-redux` template, make sure that you also
install `js-cookie` after the app is bootstrapped since the template does not
come with that package.

Install the `js-cookie` package with

```sh
npm install js-cookie
```

### Restore the XSRF-TOKEN Cookie

Make sure that the two code blocks in this section are placed in your
`backend/routes/index.js` and not somewhere else. The code blocks should also
not be nested within each other since they are conditionals to give your
frontend application the `XSRF-TOKEN` cookie differently depending on whether
your application is in production or not.

## From here...

From here, the instructions are fairly straightforward for the rest of this
section.

## Things of note

### `csrfFetch`

Because of how the `csrfFetch` is designed, (see the
`frontend/src/store/csrf.js` file), the `Content-Type` header is automatically
set to `application/json` so you will almost never have to set that header
yourself when using the `csrfFetch` in your thunk.

Also, the `csrfFetch` function throws the `response` object that is
returned from the `fetch` call if the status code on the response is 400 or
greater.

Possible status codes:

1. `404` - Route doesn't exist
2. `500` - Sequelize encountered an error when making a query
3. `401` - No authorized user

Because the response is thrown, you will have to `catch` it somewhere
in your code to parse those errors.

Two possibilities for catching include:

* Using a `try { ... } catch (err) { ... }` block
* Using `.catch()` Promise methods.

You can follow the example in the instructions on how to do it with a `.catch()`
method in Phase 1 with the `LoginFormPage` and in Phase 2 with the
`SignupFormPage` components, it their `handleSubmit` functions.
