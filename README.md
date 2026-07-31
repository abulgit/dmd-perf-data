# dmd-perf-data

Performance history for [dmd](https://github.com/dlang/dmd), written by its
`perf` workflow. One record per push to master:

```
data/<year>/<month>/<sha>.json
```

Each record holds the absolute metric values measured at that commit plus the
`-ftime-trace` phase breakdown. `push.commits` says how many commits arrived in
that push, since a rebase-merged PR lands several at once.

Pull request measurements are not stored here — they only appear as a comment
on the pull request itself.

## Setup

The publishing job authenticates with a deploy key:

1. `ssh-keygen -t ed25519 -N "" -f perf_data_key`
2. Add `perf_data_key.pub` here under Settings → Deploy keys, **with write
   access**.
3. Add the contents of `perf_data_key` to the dmd repo as the secret
   `PERF_DATA_KEY`.
4. Add the variable `PERF_DATA_REPO` there, set to `<owner>/dmd-perf-data`.

The publish step is skipped while `PERF_DATA_REPO` is unset, so the workflow can
be merged before any of this exists.
