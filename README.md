# node-publish-action

Uses [comfy-cli](https://github.com/Comfy-Org/comfy-cli) to publish the current version of your custom node to the [registry](https://comfyregistry.org). The goal is to create an easy way for developers to publish updates to their custom node to the registry.

## Getting Started

### Create a Publisher

You need to create a publisher on the registry before publishing. Follow the instructions [here](http://localhost:3000/custom-nodes/overview#publishing-to-the-registry).

### Initialize Custom Node

If you have never published to the registry before, [create](https://comfydocs.org/custom-nodes/overview#add-metadata) a pyproject.toml file for your custom node.

### Publish when pyproject.toml changes

Create a file in your custom node repository called: `.github/workflows/publish_custom_node.yml`

Copy this into the file:

```yaml
name: "Publish to Comfy registry"
on:
  push:
    branches:
      - main
    paths:
      - "pyproject.toml"

jobs:
  publish-node:
    name: Publish Custom Node to registry
    runs-on: ubuntu-latest
    steps:
      - name: Check out code
        uses: actions/checkout@v2
      - name: Publish Custom Node
        uses: comfy-org/node-publish-action@main # TODO replace when published.
        with:
          personal_access_token: ${{ secrets.GITHUB_TOKEN }} ## Add your own personal access token to your Github secrets and reference it here.
```

If you haven't yet, follow the instructions [here](https://comfydocs.org) to create a Publisher on the registry portal and a Personal Access Token. A personal access token is required to authenticate publishing node versions from Github Actions.

### Version Numbers

`comfy-cli` will publish the version written in `pyproject.toml`.

Make sure you update this before running the Github Action.

```toml

[project]
version = "1.0.1"
```
