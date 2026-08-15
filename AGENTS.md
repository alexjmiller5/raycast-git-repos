# raycast-git-repos

Fork of the [Git Repos Raycast extension](https://raycast.com/moored/git-repos).
Upstream is the `extensions/git-repos/` subdir of the `raycast/extensions`
monorepo (no standalone upstream repo exists — that's why this is a snapshot
fork, not a GitHub fork). The initial commit is the pristine upstream copy;
`git diff <initial-commit>..HEAD` is Alex's whole delta. Updating from
upstream = copy the newer subdir over, re-apply that delta.

## Dev workflow

- Loaded into Raycast as a **dev import**, not from the store: run
  `pnpm run dev`, Ctrl-C once it loads — the import persists without the
  watcher. Raycast registers the import by ABSOLUTE PATH
  (`~/Desktop/coding/active-projects/raycast-git-repos`); renaming or moving
  this dir orphans it — re-run `pnpm run dev` and delete the stale entry.
- `npx ray develop` ALWAYS fails ("could not determine executable to run"):
  the `ray` CLI ships inside `@raycast/api`, there is no npm package named
  `ray`. Use `pnpm run dev` or `pnpm exec ray develop`.
- `pnpm-workspace.yaml`'s `allowBuilds: esbuild: true` is load-bearing:
  pnpm 10+ blocks dependency postinstall scripts, and without the approval
  `ray develop`'s internal `pnpm install` exits 1.
- Verify a change builds with `pnpm exec ray build -e dist`. That does NOT
  refresh what Raycast runs (`-e` is environment, not output path): the live
  bundle is `~/.config/raycast/extensions/git-repos/`, only rewritten by
  `pnpm run dev` or `pnpm exec ray build -e dev -o ~/.config/raycast/extensions/git-repos`.

## Registration reality (why this repo isn't nix-managed)

Raycast records installed/imported extensions in an encrypted local DB
(`raycast-enc.sqlite`) with no CLI/API to write to it — extensions can't be
declared in nix-config. The inventory + restore procedure lives in
nix-config `MANUAL-macbook-air.md` §"Raycast extensions".
