```
#AGENTS.md

## Git Policy — No History Rewriting

- **NEVER** delete or revert commits. Committed history is immutable.
- **NEVER** force-push (`git push --force`, `git push --force-with-lease`, or any variant that rewrites remote history).
- The only push allowed is a fast-forward `git push`.
- If a mistake has been committed, fix it with a **new** commit on top — do not amend, rebase, or reset published commits.
- If you need to undo something, use `git revert` to create a new commit that reverses the change.
- If you accidentally commit something sensitive (secrets, keys), ask the user how to handle it — do not attempt to rewrite history.
- **`git clean` is TOTALLY PROHIBITED in any form** (`git clean`, `git clean -f`, `git clean -fd`, `git clean -fdx`, `git clean -n`). It deletes untracked files permanently and irrecoverably. If you ever type or think of `git clean`, STOP and use a non-destructive alternative below.
- **`git reset --hard` is PROHIBITED against any working tree that contains uncommitted work or untracked files** (see Working-Tree Safety below). If you must reset, first verify there is nothing to lose, and prefer `git checkout -- <path>` or `git restore` scoped to specific files.

## Working-Tree & Untracked-File Safety (CRITICAL)

Untracked files are frequently the ONLY copy of real work in this repo (new packages, new features, docs, refactors may never have been committed). Treat untracked files as **valuable, unrecoverable data** until proven otherwise.

- **Before ANY destructive git operation** (`reset --hard`, `clean`, `checkout .`, `restore --staged`, deleting files), run `git status --short` and:
  - List every untracked file (`??`) and every modified tracked file (`M`).
  - **Assume untracked files are valuable source unless you can prove otherwise.**
  - Confirm none of them are source code, documentation, or work you must keep.
- **Never run `git clean`** (see Git Policy). There is NO safe use case for it in this repo.
- **Never run `git reset --hard` or `git checkout .` while there are untracked files or uncommitted modifications you care about.** These reset working-tree content without warning.
- **Commit work-in-progress BEFORE any cleanup/reset.** If you're about to discard or reset, first `git add` + `git commit` (or `git stash push -u` to include untracked) so work is recoverable. Prefer creating a commit or a stash over permanently destroying files.
- **To safely remove only files you KNOW are junk** (e.g. stray build artifacts, editor temp files), delete them one-by-one with `rm` after a `git status` shows they are the specific files you intend to remove — never a bulk glob over unknown untracked files.
- **Verify with `git status` that the working tree is clean and you actually removed what you intended** after any cleanup, and that you removed nothing you depended on.
- If you are unsure whether a file is needed, **keep it** and ask the user, rather than risk losing it.

## Never Let an Autonomous Agent Run Unconstrained

- ANY long-running/autonomous agent (e.g. `opencode run`, GH Actions self-hosted builder, a tramp process) MUST be given a **strictly scoped, single-purpose change** with explicit boundary files. NEVER let it "investigate and implement broadly" across a large repo.
- Before launching an autonomous build, define and record: the exact package/file scope, the tests allowed to run, and a hard "abort if touching anything outside scope" guard.
- If an agent produces sweeping, out-of-scope, or unrequested changes, **do NOT try to clean them by discarding files while untracked work exists**. Instead: commit the in-scope work first, then handle the out-of-scope residue separately and non-destructively.
- For validating an end-to-end pipeline that does real external side effects (opening PRs, pushing branches), prefer a **controlled, deterministic smoke diff** over an uncontrolled generative edit, so the pipeline can be verified without risking large unwanted diffs.
- Always diff/review what an autonomous agent changed (`git diff --stat`) BEFORE committing or pushing anything it produced.

```
