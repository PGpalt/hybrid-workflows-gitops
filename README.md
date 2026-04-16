# hybrid-workflows-gitops

GitOps source of truth for the Hybrid Workflows platform.

This repo holds the cluster roots, Argo CD `Application` definitions, platform
overlays, and the committed operator installer manifest consumed by Argo CD.

## Forking This Stack

If you fork the operator, GitOps, and infra repos together, review these kinds
of references in this repo so they point at your own repos and images:

- `repoURL` fields that still reference `https://github.com/PGpalt/hybrid-workflows-gitops.git`
- operator image names such as `ghcr.io/pgpalt/hybrid-workflows-operator`
- EKS demo values in `clusters/eks-dev/application-argo-workflows.yaml`, including the S3 region, bucket name, and the Argo service account names expected by the infra-managed EKS Pod Identity associations
- any other registry or organization-specific image references copied from the original repos

The operator release workflow can promote into a forked GitOps repo, but only if
the operator repo is configured with:

- a `GITOPS_REPO_TOKEN` secret that can push to the target GitOps repo
- an optional `GITOPS_REPO` variable if the target repo is not `<owner>/hybrid-workflows-gitops`
- an optional `GITOPS_REPO_BRANCH` variable if the target branch is not `main`
