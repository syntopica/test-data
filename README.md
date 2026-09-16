# syntopica/test-data

A synthetic, self-contained Syntopica data instance for exercising the engines
against a configuration that holds no real data: one example page, an empty
capture archive, stub engine checkouts and a `syntopica.config.json` that
declares every section the schema knows about.

Nothing here is personal. The brain page is a placeholder, the clip archive
and the newsletter lists are empty, and the engine stubs hold only the
configuration schema the doctors validate against.

## Use

```bash
git clone https://github.com/syntopica/test-data.git
cd test-data
bin/mark-repository-boundaries
```

The script recreates the `.git` markers in `clips/`, `engines/brain/` and
`engines/clips/` that git cannot carry in a clone (git refuses to track a path
with a `.git` component); the engines stop their upward instance search at
those boundaries. Then point either engine at the directory:

```bash
SYNTOPICA_DATA=$PWD ~/p/brain/bin/brain doctor
SYNTOPICA_DATA=$PWD clips doctor
```

`verification/` keeps the last recorded doctor output from both engines.

## Layout

- `syntopica.config.json` declares `brain`, `clips`, `atrium`, `conversations`
  and `engines`; `atrium/` and `conversations/` are state directories the
  engines create and are ignored.
- `engines/brain/schema/` is a snapshot of the engine's configuration schema;
  refresh it from `syntopica/brain` when the schema changes.
- `.config/` holds the empty project-alias and newsletter lists.
- `brain-only/` is a second instance that declares only the brain engine, for
  the onboarding hub's brain-only path; `bin/mark-repository-boundaries` makes
  it a repository too, and `SYNTOPICA_DATA=$PWD/brain-only` selects it.

MIT, see `LICENSE`.
