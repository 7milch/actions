# slack-notify

Posts a colored status message to Slack through an Incoming Webhook.

```yaml
- uses: 7milch/actions/slack-notify@v1
  if: always()
  with:
    webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
    status: ${{ job.status == 'failure' && 'failure' || 'success' }}
    title: Deploy finished
    message: Optional mrkdwn body
    fields: |
      Image=nginx:latest
      Digest=sha256:...
```

## Inputs

| Name | Required | Description |
| --- | --- | --- |
| `webhook-url` | yes | Slack Incoming Webhook URL |
| `status` | yes | `success` (green), `skipped` (gray) or `failure` (red) |
| `title` | yes | Title line |
| `message` | no | Body text (mrkdwn) |
| `fields` | no | `Key=Value` lines rendered as a field grid |

A link to the workflow run is appended automatically.
