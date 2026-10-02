# ericdahl-dev/.github

Organization-wide GitHub configuration.

## American spelling check

Every repo uses American spelling (color, center, canceled, analyze, gray...). The
**American spelling** workflow (`.github/workflows/american-spelling.yml`) runs
`scripts/american_spelling.py` on pull requests. The org ruleset requires it, so a PR can't
merge while its repo contains British spellings.

The checker reads every tracked text file word by word, including inside identifiers
(`colour_edges`, `AudioAnalyser`, `scanCancelled`), and prints `file:line: word -> fix`.

Run it locally on any repo:

```bash
python scripts/american_spelling.py path/to/repo
```

### Exceptions

- **One line:** add `spelling: ok` to the line (e.g. when quoting an external name).
- **One file:** put `spelling: skip-file` in its first five lines.
- **A repo:** add `.american-spelling-allow` at its root:

  ```
  # a third-party API or a value stored in the database is spelled this way
  cancelled
  Colour
  # vendored code
  path: lib/unity/
  ```

  Allowed words match case-insensitively, also inside identifiers. Use them for names you
  don't control: stored data values, external API fields, vendored code. Web API names that are
  British by definition (`AnalyserNode`, `createAnalyser`) are always allowed.
