# Git Commit Buildkite Plugin

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) to commit and push the results of a command to a git repository.  

## Example

With no options, commits all changed/added files to `$BUILDKITE_BRANCH` and pushes to `origin` with a commit message like `Build #4`:

```yml
steps:
  - command: make
    plugins:
      thedyrt/git-commit#v0.1.0: ~
```

With all options customized:

```yml
steps:
  - command: make
    plugins:
      thedyrt/git-commit#v0.1.0:
        add: app/
        branch: my-branch
        message: "Updated data [$BUILDKITE_BUILD_NUMBER]"
        remote: upstream
        user:
          name: Reid
          email: reid@example.com
```

## Configuration

- **add** (optional, defaults to `.`)

    A pathspec that will be passed to `git add -A` to add changed files.

- **branch** (optional, defaults to `$BUILDKITE_BRANCH`)

    The branch where changes will be committed. Since Buildkite runs builds in a detached HEAD state, this plugin will fetch and checkout the given branch prior to committing. 
    
- **message** (optional, defaults to `Build #${BUILDKITE_BUILD_NUMBER}`)

    The commit message

- **remote** (optional, defaults to `origin`)

    The git remote where changes will be pushed.
    
- **user.email** (optional)

    If given, will configure the git user email for the repo.

- **user.name** (optional)

    If given, will configure the git user name for the repo.


## Tests / Linting

To run the tests of this plugin, run

```sh
docker-compose run --rm tests
```

To run the [Buildkite Plugin Linter](https://github.com/buildkite-plugins/buildkite-plugin-linter), run

```sh
docker-compose run --rm lint
```

## License

MIT (see [LICENSE](LICENSE))
