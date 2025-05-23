# How to make a release

`jupyterhub-python-repo-template` is a package available on [PyPI] and
[conda-forge].

These are the instructions on how to make a release.

## Pre-requisites

- Push rights to this GitHub repository

## Steps to make a release

1. Create a PR updating `CHANGELOG.md` with [github-activity] and continue when
   its merged. For details about this, see the [team-compass documentation]
   about it.

   [team-compass documentation]: https://jupyterhub-team-compass.readthedocs.io/en/latest/practices/releases.html

2. Checkout main and make sure it is up to date.

   ```shell
   git checkout main
   git fetch origin main
   git reset --hard origin/main
   ```

3. Update the version, make commits, and push a git tag with `tbump`.

   ```shell
   pip install tbump
   ```

   `tbump` will ask for confirmation before doing anything.

   ```shell
   # Example versions to set: 1.0.0, 1.0.0b1
   VERSION=
   tbump ${VERSION}
   ```

   Following this, the [CI system] will build and publish a release.

4. Reset the version back to dev, e.g. `1.0.1.dev` after releasing `1.0.0`.

   ```shell
   # Example version to set: 1.0.1.dev
   NEXT_VERSION=
   tbump --no-tag ${NEXT_VERSION}.dev
   ```

5. Following the release to PyPI, an automated PR should arrive within 24 hours
   to [conda-forge/jupyterhub-python-repo-template-feedstock] with instructions
   on releasing to conda-forge. You are welcome to volunteer doing this, but
   aren't required as part of making this release to PyPI.

[github-activity]: https://github.com/executablebooks/github-activity
[pypi]: https://pypi.org/project/jupyterhub-python-repo-template/
[conda-forge]: https://anaconda.org/conda-forge/jupyterhub-python-repo-template
[conda-forge/jupyterhub-python-repo-template-feedstock]: https://github.com/conda-forge/jupyterhub-python-repo-template-feedstock
[ci system]: https://github.com/jupyterhub/jupyterhub-python-repo-template/actions/workflows/release.yaml
