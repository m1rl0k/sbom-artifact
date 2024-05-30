# SBOM Generation Action
[![SBOM Generation](https://github.com/m1rl0k/sbom-artifact/actions/workflows/sbom.yml/badge.svg)](https://github.com/m1rl0k/sbom-artifact/actions/workflows/sbom.yml)

This GitHub Action generates an SBOM (Software Bill of Materials) for your repository using the [Anchore SBOM Action](https://github.com/anchore/sbom-action). The SBOM file provides a comprehensive inventory of the software components and dependencies present in your repository.

## Usage

To use the SBOM Generation Action in your workflow, follow these steps:

1. Make sure your workflow file (e.g., `.github/workflows/main.yml`) has the necessary permissions:

   ```yaml
   permissions:
     id-token: write
     contents: read
   ```

2. Add the following steps to your workflow:

   ```yaml
   steps:
     - uses: actions/checkout@v4
     - name: Generate SBOM
       uses: m1rl0k/sbom-artifact@main
       with:
         repository-name: ${{ github.event.repository.name }}
   ```

   Replace `goodyear` with your actual GitHub organization or username if you've published the action under a different organization or personal account.

3. Commit and push the changes to your repository.

Now, whenever the workflow containing these steps is triggered, it will:
1. Check out the code from your repository using `actions/checkout@v4`.
2. Run the SBOM Generation Action using `m1rl0k/sbom-artifact@main`.
   - The `repository-name` input is set to `${{ github.event.repository.name }}`, which represents the name of the repository.

The action will generate an SBOM file in the SPDX-JSON format and upload it as an artifact named `sbom-files`.

## Inputs

The SBOM Generation Action supports the following input parameters:

- `repository-name` (required): The name of the repository for which the SBOM is generated.
- `path` (optional): The path to scan for generating the SBOM. Default is the current directory (`.`).
- `format` (optional): The format of the SBOM file. Default is `spdx-json`.

## Outputs

The SBOM Generation Action generates the following output:

- `sbom-files`: An artifact containing the generated SBOM file in the specified format.

## Example Workflow

Here's an example workflow that demonstrates how to use the SBOM Generation Action:

```yaml
name: Generate SBOM

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

permissions:
  id-token: write
  contents: read

jobs:
  generate-sbom:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Generate SBOM
        uses: m1rl0k/sbom-artifact@main
        with:
          repository-name: ${{ github.event.repository.name }}
```
