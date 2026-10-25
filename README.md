# renovate-config

The shared [Renovate](https://docs.renovatebot.com/) preset for the `slafhas` and `Grundkoll`
repositories. Each repository's `renovate.json` extends it and adds the groups that belong to
its own stack:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>pRob3/renovate-config"]
}
```

## What it does

- **Once a week**, Monday between 02:00 and 06:00 Stockholm time, the version updates arrive.
  A human merges them. Majors arrive as their own pull request unless the repository holds
  them back in its own `renovate.json`.
- **Security fixes** arrive outside the schedule, labelled `security`, once the fixed version
  is two days old -- the same wait as every other update -- and merge themselves once every
  check is green, at night, inside the same window as every automerge. A fix that is wanted
  before then is listed under *Pending Status Checks* on the Dependency Dashboard: tick it to
  get the pull request now and merge it by hand. Renovate reads the repository's Dependabot
  alerts and the OSV database for them. Dependabot's version updates are off; its security
  updates stay on for transitive dependencies, which Renovate does not fix, and a human merges
  those.
- **At night.** Open branches are rebased only inside the window, so a day of pushes does not
  start a CI run for every open dependency pull request.
- **Merging deploys nothing.** A published GitHub release does.

Every rule carries its reason in its `description`. Change a rule here and every repository
follows on its next run.

## License

MIT, see [LICENSE](LICENSE).
