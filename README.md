## Issue description

`.bazelignore` of root repository should work on subdirectories added with `new_local_repository`, but it doesn't.

## How to reproduce

Note that we have `local_repo` and a folder `should_be_excluded` inside. 
It is excluded in the parent `.bazelignore`.

But, when you query targets from `@local_repo`, dirs `should_be_excluded` is NOT excluded:


```bash
$ bazel query @local_repo//...
@local_repo//should_be_excluded:run
@local_repo//:run
```

In cases when `local_repo` is not writeable, it is not possible to exclude dirs/targets from `local_repo`.

## Potential solutions

1. Add `bazelignore` argument to `new_local_repository`, similar to `build_file` or `build_file_content`.
2. Same as (1), but more generic: add `file_mapping` argument, which will copy/symlink files from root repository into new repository:
```
new_local_repository(
    name = 'local_repo',
    path = 'local_repo',
    build_file = 'BUILD.local',
    file_mapping = {
        '.bazelignore.local': '.bazelignore'
    }
)
```