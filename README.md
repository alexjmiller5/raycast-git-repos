# raycast-git-repos

My fork of the [Git Repos](https://raycast.com/moored/git-repos) Raycast
extension: list the git repositories under configured paths and open one in
an editor or any app.

Upstream lives in the `extensions/git-repos/` directory of the
`raycast/extensions` monorepo, so this is a snapshot fork rather than a GitHub
fork. The first commit is the pristine upstream copy; everything after it is
my delta. Updating from upstream means copying the newer directory over and
reapplying that delta.

## Use

Loaded into Raycast as a development import, not from the store:

```sh
pnpm install
pnpm run dev   # Ctrl-C once Raycast has loaded it; the import persists
```

Raycast registers the import by absolute path, so moving this directory
orphans it: run `pnpm run dev` again and delete the stale entry. Preferences
are the scan paths (`:`-separated, `~` expanded) and the maximum scan depth.
`AGENTS.md` carries the rest of the development notes.
