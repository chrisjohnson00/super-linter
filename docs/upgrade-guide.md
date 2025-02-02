# Super-linter upgrade guide

This document helps you upgrade from a super-linter version to newer ones:

- [Upgrade from v5 to v6](#upgrade-from-v5-to-v6)

## Upgrade from v5 to v6

This section helps you migrate from super-linter `v5` to `v6`.

### Dart

- super-linter doesn't include a default configuration file for `dart analyzer`
  because the Dart SDK doesn't support running `dart analyzer` against an
  arbitrary configuration file anymore. For more information about how to
  customize static analysis of Dart files, see
  [Customizing static analysis](https://dart.dev/tools/analysis) in the Dart SDK
  documentation.

### Experimental batch workers

- Experimental batch support is deprecated. You can safely remove the
  `EXPERIMENTAL_BATCH_WORKER` variable from your configuration.

### Gitleaks

- If you defined secret patterns in `.gitleaks.toml`, Gitleaks may report errors
  about that file. If this happens, you can
  [configure Gitleaks to ignore that file](https://github.com/gitleaks/gitleaks/tree/master?tab=readme-ov-file#gitleaksignore).
- Gitleaks doesn't consider the `FILTER_REGEX_EXCLUDE`, `FILTER_REGEX_INCLUDE`,
  `IGNORE_GENERATED_FILES`, `IGNORE_GITIGNORED_FILES` variables. For more
  information about how to ignore files with Gitleaks, see
  [the Gitleaks documentation](https://github.com/gitleaks/gitleaks/tree/master?tab=readme-ov-file#gitleaksignore).

### Jscpd

- The `VALIDATE_JSCPD_ALL_CODEBASE` variable is deprecated. Jscpd now lints the
  entire workspace instead of linting files one by one. You can safely remove
  the `VALIDATE_JSCPD_ALL_CODEBASE` variable from your configuration.
- Jscpd doesn't consider the `FILTER_REGEX_EXCLUDE`, `FILTER_REGEX_INCLUDE`,
  `IGNORE_GENERATED_FILES`, `IGNORE_GITIGNORED_FILES` variables. For more
  information about how to ignore files with Jscpd, see
  [the Jscpd documentation](https://github.com/kucherenko/jscpd/tree/master/packages/jscpd).

### textlint

- textlint doesn't consider the `FILTER_REGEX_EXCLUDE`, `FILTER_REGEX_INCLUDE`,
  `IGNORE_GENERATED_FILES`, `IGNORE_GITIGNORED_FILES` variables. For more
  information about how to ignore files with textlint, see
  [the textlint documentation](https://textlint.github.io/docs/ignore.html).

### USE_FIND_ALGORITHM and VALIDATE_ALL_CODEBASE used together

- Setting `USE_FIND_ALGORITHM` to `true` and `VALIDATE_ALL_CODEBASE` to `false`
  is an unsupported configuration. super-linter `v5` and earlier silently
  ignored `VALIDATE_ALL_CODEBASE` when `USE_FIND_ALGORITHM` is set to `true`,
  leading to potentially confusing behavior for users. super-linter `v6`
  explicitly fail in this case. Remove one of the two from your configuration,
  depending on the desired behavior.

### VALIDATE_KOTLIN_ANDROID

- The `VALIDATE_KOTLIN_ANDROID` variable has been deprecated because ktlint
  handles linting Kotlin files for Android using a configuration option, so
  super-linter doesn't need to account for this special case anymore. If you
  set `VALIDATE_KOTLIN_ANDROID` in your configuration, change it to
  `VALIDATE_KOTLIN` and configure ktlint to lint Android files.
