# actions-test (changed by hotfix D)

Sandbox to exercise the `create-version-branch.yml` + `finish-version-branch.yml` flow end-to-end before touching the real repo.

## Branches
- `main` — production mirror
- `develop` — integration

## Flow to exercise
1. Create a fix branch from `main`
2. Merge it to `develop` (simulates "tested in dev")
3. Dispatch `Create Version Branch` with type `hotfix` → creates `hotfix/vX.Y.Z` from main, opens PR to main
4. Merge fix branch into `hotfix/vX.Y.Z` (PR)
5. Merge hotfix PR to main
6. `finish-version-branch.yml` fires → tag created + merge-back PR to develop

## Conflict scenarios to test
- A) Clean merge-back
- B) Only `package.json` `version` field diverges (auto-resolve)
- C) `package.json` with deps divergence (should open `[CONFLICT]` PR)
- D) Another file conflicts (should open `[CONFLICT]` PR)
