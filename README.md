# Hound JSHint

[JSHint] is a static code analysis tool for JavaScript

`hound-jshint` is a Node service that polls `JshintReviewJob`s from the
`jshint_review` queue, lints code with `JSHint`, then pushes the results to
the `high` queue, as `CompletedFileReviewJob`s.

[JSHint]: http://jshint.com/

## How fork update?

1. Add remote original upstream to your local repository

  ```
  git remote add upstream git@github.com:houndci/jshint.git
  ```

2. Fetch the branches and their respective commits from the upstream repository. Commits to `master` will be stored in a local branch, `upstream/master`.

  ```
  git fetch upstream
  ```

3. Check out your fork's local `master` branch.

  ```
  git checkout master
  ```

4. Merge the changes from `upstream/master` into your local `master` branch. This brings your fork's `master` branch into sync with the upstream repository, without losing your local changes.

  ```
  git merge upstream/master
  ```

  **If your local branch didn't have any unique commits, Git will instead perform a "fast-forward":**

  ```
  git merge upstream/master
  ```

## Testing locally

First, add the following to the bottom of `index.js`:

```js
var testQueue = require("./lib/test-queue");

testQueue(redis);
```

Next, start the Resque web interface:

```bash
$ cd node_modules/node-resque/resque-web
$ bundle install
$ bundle exec rackup
$ open http://localhost:9292
```

As you run the worker, monitor how jobs flow through the queues.
