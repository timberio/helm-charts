# Vector Helm Charts

Official Helm charts for Vector. Currently supported:
- [Vector](charts/vector/README.md) (vector/vector)
- **DEPRECATED** [Vector Agents](charts/vector-agent/README.md) (vector/vector-agent)
- **DEPRECATED** [Vector Aggregators](charts/vector-aggregator/README.md) (vector/vector-aggregator)

# How to use the Vector Helm Repository

You need to add this repository to your Helm repositories:

```shell
helm repo add vector https://helm.vector.dev
helm repo update
```

# Releasing

Charts are packaged and released with [`cr`](https://github.com/helm/chart-releaser)
when the `develop` branch is merged into `master`.

To make releasing easier two scripts are utilized in the steps below.

1. `$ .github/release-vector-version.sh`
    - This queries [vectordotdev/vector](https://github.com/vectordotdev/vector)
for the latest release and updates the `vector` chart's default image.
    - This is convenient when updating the chart after a Vector release.

2. Commit the changes generated from step 1. This needs to be a
[conventional commit](https://www.conventionalcommits.org/).
    - E.g. "feat(vector): Bump Vector to v0.29.0"

3. `$ .github/release-changelog.sh`
    - This pulls the current `vector` chart version and uses `git-cliff` to update
the [CHANGELOG.md](CHANGELOG.md). Run this to generate the final commit merged into
`develop` before merging `develop` into `master`.
    - This script requires [`yq`](https://github.com/mikefarah/yq) and
[`git-cliff`](https://github.com/orhun/git-cliff) to be installed.

4. Commit the changes generated from step 1. This needs to be a
[conventional commit](https://www.conventionalcommits.org/).
    - E.g. "feat(vector): Regenerate CHANGELOG"
