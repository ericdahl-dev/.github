<!-- spelling: skip-file (this README quotes British spellings as examples) -->
# ericdahl-dev/.github

Organization-wide GitHub configuration.

## American spelling check

Every repo uses American spelling (color, center, canceled, analyze, gray...). The **American
spelling** workflow (`.github/workflows/american-spelling.yml`) runs the public
[spelling-dialect](https://github.com/ericdahl-dev/spelling-dialect) action on pull requests. The
org ruleset requires it, so a PR can't merge while its repo contains British spellings.

It reads every tracked text file word by word, including inside identifiers (`colour_edges`,
`AudioAnalyser`, `scanCancelled`), and prints `file:line: word -> fix`.

Run it locally on any repo:

```bash
pipx run --spec git+https://github.com/ericdahl-dev/spelling-dialect spelling-dialect .
```

### Exceptions

- **One line:** add `spelling: ok` to it (e.g. when quoting an external name).
- **One file:** put `spelling: skip-file` in its first five lines.
- **A repo:** add `.spelling-dialect` at its root (the older `.american-spelling-allow` also works):

  ```
  # a third-party API or a value stored in the database is spelled this way
  cancelled
  # vendored code
  path: lib/unity/
  ```

  Allowed words match case-insensitively, also inside identifiers. Use them for names you don't
  control: stored data values, external API fields, vendored code. Platform names that are British
  by definition (`AnalyserNode`, `CancelledError`, `isCancelled`, GitHub Actions' `cancelled`) are
  always allowed. See the [spelling-dialect README](https://github.com/ericdahl-dev/spelling-dialect#readme).
