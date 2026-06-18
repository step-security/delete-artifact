[![StepSecurity Maintained Action](https://raw.githubusercontent.com/step-security/maintained-actions-assets/main/assets/maintained-action-banner.png)](https://docs.stepsecurity.io/actions/stepsecurity-maintained-actions)

![CI](https://github.com/GeekyEggo/delete-artifact/workflows/CI/badge.svg)
![Example](https://github.com/GeekyEggo/delete-artifact/workflows/Example/badge.svg)

# Delete artifacts

A GitHub Action for deleting artifacts within the workflow run. This can be useful when artifacts are shared across jobs, but are no longer needed when the workflow is complete.

## ✅ Compatibility

| `step-security/delete-artifac` | `actions/upload-artifact` |
| --------------------------- | ------------------------- |
| `@v6`                       | `@v4`, `@v6`              |
| ~~@v4~~, `@v5`              | `@v4`                     |
| `@v1`, `@v2`                | `@v1`, `@v2`, `@v3`       |

<!-- prettier-ignore -->
> [!TIP]
> You can reference the immutable commit SHA, instead of a version, for example.
> ```yml
> - uses: step-security/delete-artifac@176a747ab7e287e3ff4787bf8a148716375ca118 # v6.0.0
> ```

<!-- prettier-ignore-end -->

## ⚡ Usage

See [action.yml](action.yml)

### Delete an individual artifact

```yml
steps:
    - name: Checkout
      uses: actions/checkout@v6

    - name: Create test file
      run: echo hello > test.txt

    - uses: actions/upload-artifact@v6
      with:
          name: my-artifact
          path: test.txt

    - uses: step-security/delete-artifac@v6
      with:
          name: my-artifact
```

### Specify multiple names

```yml
steps:
    - uses: step-security/delete-artifac@v6
      with:
          name: |
              artifact-*
              binary-file
              output
```

## 🚨 Error vs Fail

By default, the action will fail when it was not possible to delete an artifact (with the exception of name mismatches). When the deletion of an artifact is not integral to the success of a workflow, it is possible to error without failure. All errors are logged.

```yml
steps:
    - uses: step-security/delete-artifac@v6
      with:
          name: okay-to-keep
          failOnError: false
```
