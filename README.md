## Issue description

`.bazelignore` of root repository should work on subdirectories added with `new_local_repository`, but it doesn't.

## How to reproduce

Note that we have `local_repo` and a folder `should_be_excluded` inside. It is excluded in the parent `.bazelignore`