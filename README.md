## 🚀 Release Process

This project follows a strict versioning and release workflow to ensure traceability and reproducibility.

Dockerhub repository : https://hub.docker.com/repository/docker/lordtibu/tp3-cicd

### 🔁 Continuous Integration (on push to `main`)

Every push to the `main` branch triggers the main CI pipeline.

This pipeline:

* checks out the source code
* installs dependencies
* runs automated tests
* builds the Docker image only if tests pass
* pushes the image to Docker Hub with:

  * the `latest` tag
  * the commit SHA tag

This ensures that the `main` branch always produces a tested and deployable container image.

### 🏷 Creating a Release (Versioned Product)

A product release is created from a validated state of `main`.

Release steps:

1. Develop changes on a feature branch
2. Open a Pull Request to `main`
3. Wait for the PR checks to pass
4. Merge the PR into `main`
5. Wait for the main CI pipeline to finish successfully
6. Create a Git tag for the version:
   `git tag v1.0.0`
   `git push origin v1.0.0`
7. The release workflow is triggered on that version tag
8. A Docker image is built and pushed with the matching version tag:

   * `v1.0.0`

This guarantees that released images are tied to a precise Git version.

### 📌 Versioning Rules

This project uses semantic versioning:

* **MAJOR**: incompatible or breaking changes
* **MINOR**: backward-compatible features
* **PATCH**: backward-compatible bug fixes

Examples:

* `v1.0.0`
* `v1.1.0`
* `v1.1.1`

Rules:

* version tags must follow the format `vX.Y.Z`
* a released version must always point to a single immutable Git commit
* a released version must never be rebuilt or overwritten
* `latest` is only a convenience tag and must not be used as a stable product version

### 🔎 Traceability

Traceability is ensured through multiple linked identifiers:

* **Git commit SHA** identifies the exact source state
* **Pull Requests** provide review history and validation before merge
* **Git tags** such as `v1.0.0` mark official product versions
* **Docker tags** such as `latest`, commit SHA, and version tags connect images to source history
* **Docker digest** uniquely identifies the exact built image content

With this workflow, it is always possible to:

* know which code produced an image
* know which tests were run before publication
* retrieve the exact released version
* distinguish rolling images (`latest`) from immutable releases (`vX.Y.Z`)
