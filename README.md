# 7milch/actions

Reusable GitHub Actions.

| Action | Description |
| --- | --- |
| [`ecr-mirror`](./ecr-mirror) | Copy a container image into Amazon ECR with crane (OIDC or access key) |
| [`slack-notify`](./slack-notify) | Post a success / skipped / failure message to Slack via Incoming Webhook |

## Usage

```yaml
# OIDC
permissions:
  id-token: write
  contents: read
steps:
  - uses: 7milch/actions/ecr-mirror@v1
    with:
      source-image: docker.io/library/nginx:1.27
      destination-repository: nginx
      aws-region: ap-northeast-1
      role-to-assume: arn:aws:iam::123456789012:role/github-actions-ecr
```

```yaml
# Access key
steps:
  - uses: 7milch/actions/ecr-mirror@v1
    with:
      source-image: docker.io/library/nginx:1.27
      destination-repository: nginx
      aws-region: ap-northeast-1
      aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

See [`ecr-mirror/README.md`](./ecr-mirror/README.md) for all inputs.

## Versioning

Use the major tag `v1`; it is moved forward on each compatible release (`v1.x.y`).
