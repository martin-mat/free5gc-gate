# free5GC certification gate

[![CNTi cert](https://github.com/martin-mat/free5gc-gate/raw/badges/cnti-badge.svg)](https://github.com/martin-mat/free5gc-gate/actions/workflows/cnti.yml)

[free5GC](https://free5gc.org) — the CNTi Test Suite's reference CNF — certified by the
[CNTi Test Suite GitHub Action](https://github.com/lfn-cnti/testsuite-action) on a plain
GitHub-hosted runner: no private infrastructure, nothing pre-installed.

- [`free5gc-helm/`](free5gc-helm) — the upstream [free5gc-helm](https://github.com/free5gc/free5gc-helm)
  chart as a pinned submodule (Renovate proposes bumps).
- [`cnti-testsuite.yaml`](cnti-testsuite.yaml) — the CNF description, identical to the test
  suite's own nightly free5GC run.
- [`.github/workflows/cnti.yml`](.github/workflows/cnti.yml) — builds and loads the
  [gtp5g](https://github.com/free5gc/gtp5g) kernel module the UPF needs (kind nodes share the
  runner's kernel), creates a 3-node kind cluster with the sysctls the UPF needs, then runs
  `cnti-testsuite cert`. The job passes if the certification criterion is met, fails if not.

A full run takes about 1.5 hours, so it runs nightly and on demand rather than on every
push. The badge is published by the action to the [`badges`](https://github.com/martin-mat/free5gc-gate/tree/badges)
branch after each run on `main`.

Optional: set the `DOCKERHUB_USERNAME` / `DOCKERHUB_TOKEN` repository secrets so the ~16
image pulls are authenticated (avoids Docker Hub's anonymous rate limit).
