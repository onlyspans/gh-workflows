# gh-workflows

Shared GitHub Actions workflows for onlyspans services.

## release.yml

### Usage

```yaml
jobs:
  release:
    uses: onlyspans/gh-workflows/.github/workflows/release.yml@main
    permissions:
      contents: write
    with:
      image_name: my-service
      helm_release: my-service-staging
      kube_namespace: my-service
    secrets: inherit
```

### HELM_ENV

For services that require env vars in `helm/ci-values.yaml`, add a repository secret `HELM_ENV` with `KEY=VALUE` pairs (one per line):

```
MY_SERVICE_DATABASE_URL=postgresql://...
MY_SERVICE_S3_BUCKET=my-bucket
```

The workflow exports all variables from `HELM_ENV` into the environment before running `envsubst` on `helm/ci-values.yaml`. Services without `HELM_ENV` work as-is.
