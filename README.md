# Module name
<Description>

# Requirements

1. install dependencies:
   * [`poetry`](https://python-poetry.org/docs/)
2. Configure poetry: [poetry setup doc](https://docs.google.com/document/d/1oxNg-F3GwYUaj7jNCH_uvYzXfurqxB68ElsFreKNKzo/edit#heading=h.lnq3jg2l0j6j)
  
# Local development
1. Run `make setup-githooks` to symlink githooks we use.
<Steps required for local development>

# Setup

1. Make a copy of the .env.example and update the values
2. Run: `make setup` to setup your virtual environment with poetry and install dev dependencies
3. Run: `make start`

# Git Hooks (pre-push)
Before you push the code upstream a Git Hook will be triggered and run `make lint` and `make format` automatically. You can customize as needed and add additional steps if required by the new repository.

# GitHub actions & Workload Identity
This template contains basic CICD workflows but in order to allow the Google Service Account impersonation, you'll need an additional step and request the access by adding the new repository here (example): [https://github.com/EvolutionIQ/terraform/blob/main/GCP/foundation/shared_services.tf#L392](https://github.com/EvolutionIQ/terraform/blob/main/GCP/foundation/shared_services.tf#L392)

# Adding new dependencies
Suppose you want to add dagster 1.0.17 to the main group:
```
make setup
poetry add dagster==1.0.17
```
Note that the `poetry.lock` and `pyproject.toml` will now caintain a record of your changes and need to be committed.

See `poetry help add` and [online poetery documentation](https://python-poetry.org/docs/cli/#add) for more info.

## Dependencies best practice
Only add libraries to poetry that are imported or configured by your project. Let poetry manage the sub-dependencies.

# Docker integration

This app is deployed in the form of a docker image. Make sure your Dockerfile and docker-compose.yaml remain in working order:
```
make build
make up
```
This is also done in github when a new pull request is submitted.
