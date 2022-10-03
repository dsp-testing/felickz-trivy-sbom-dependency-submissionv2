# Universe 2022: What are SBOMs, and how do I make them useful? demo repo

This is a simple Maven project that builds a standalone JAR which contains a Jetty webserver and a simple bookstore servlet. The repository hosts a demo and resources to accompany SEC020: _What are SBOMs, and how do I make them useful?_, a talk presented at Universe 2022.

This project includes a workflow file ([`sbom-upload.yml`](.github/workflows/sbom-upload.yml)) that uses Anchore's [SBOM Action](https://github.com/anchore/sbom-action), which scans the JAR file and creates a software bill of materials using Syft. The action then transposes the SBOM to the required submission format for the (dependency submission API](https://docs.github.com/en/rest/dependency-graph/dependency-submission) and uploads it to the repository's [dependency graph](https://github.com/octodemo/sbom-demo/network/dependencies). This provides the repository with a more comprehensive dependency graph, including transitive Maven dependencies that are not parsed from the `pom.xml` by default using the dependency graph's static scanning capabilities. Dependabot Alerts for these new dependencies are synced automatically.

## About the dependency graph and the dependency submission API

GitHub builds a repository's dependency graph from static scans of checked-in manifest files by default, which limits the completeness of the graph in some ecosystems. The dependency submission API allows developers to upload dependency information directly to GitHub, for instance, from a build tool.

There are several [community-owned GitHub Actions in the Marketplace](https://github.com/marketplace?query=dependency+submission+) that will scan projects from different ecosystems and upload the dependencies to the repository's dependency graph. You can also write your own GitHub Action to submit dependencies with the [dependency submission toolkit](https://github.com/github/dependency-submission-toolkit/pkgs/npm/dependency-submission-toolkit).

Resources:
   * [Blog post: Creating a more comprehensive dependency graph with build time detection](https://github.blog/2022-06-17-creating-comprehensive-dependency-graph-build-time-detection/)
   * [Dependency submission API documentation](https://docs.github.com/en/rest/dependency-graph/dependency-submission)
   * [Dependency graph documentation](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/about-the-dependency-graph)

## About SBOMs

Software bills of materials are an inventory of everything that your software uses summed up in a specific format.

There are various tools that generate SBOMs:
   * [kubernetes-sigs/bom](https://github.com/kubernetes-sigs/bom)
   * [microsoft/sbom-tool](https://github.com/microsoft/sbom-tool)
   * [opensbom-generator/spdx-sbom-generator](https://github.com/opensbom-generator/spdx-sbom-generator)
   * [anchore/syft](https://github.com/anchore/syft)
   * [sbs2001/fatbom](https://github.com/sbs2001/fatbom)

There's also a community-owned GitHub Action that [submits SBOMs to the dependency submission API](https://github.com/evryfs/sbom-dependency-submission-action).

## Questions?

Add a discussion in [community/community](https://github.com/community/community/discussions/categories/code-security) with any questions about the dependency graph, dependency submission API, or how to integrate them with SBOMs.