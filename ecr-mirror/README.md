# ecr-mirror

Copies an image from any registry into Amazon ECR using [crane](https://github.com/google/go-containerregistry/tree/main/cmd/crane).
Authentication goes through `aws-actions/configure-aws-credentials`: pass `role-to-assume` for OIDC, or `aws-access-key-id` + `aws-secret-access-key` for static keys.

## Inputs

| Name | Required | Default | Description |
| --- | --- | --- | --- |
| `source-image` | yes | | Source image reference, e.g. `docker.io/library/nginx:1.27` |
| `destination-repository` | yes | | ECR repository name |
| `destination-tag` | no | source tag (or `latest`) | Tag in ECR |
| `aws-region` | yes | | ECR region |
| `aws-account-id` | no | from `sts get-caller-identity` | Account ID of the registry |
| `role-to-assume` | no | | IAM role ARN for OIDC. Needs `permissions: id-token: write` |
| `aws-access-key-id` | no | | Static credentials (when no role) |
| `aws-secret-access-key` | no | | Static credentials (when no role) |
| `crane-version` | no | `latest` | crane version |

## Outputs

| Name | Description |
| --- | --- |
| `destination-image` | Full image reference pushed to ECR |

## Required IAM permissions

- `ecr:GetAuthorizationToken` on `*`
- `ecr:BatchCheckLayerAvailability`, `ecr:BatchGetImage`, `ecr:GetDownloadUrlForLayer`, `ecr:InitiateLayerUpload`, `ecr:UploadLayerPart`, `ecr:CompleteLayerUpload`, `ecr:PutImage` on the repository
- `sts:GetCallerIdentity` (only if `aws-account-id` is omitted)
