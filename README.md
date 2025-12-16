# Coolify Deploy Action

A reusable GitHub Action to trigger deployments on Coolify.

## Usage

### Basic Example

```yaml
name: Deploy to Coolify

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Trigger Coolify deployment
        uses: benbristow/coolify-deploy-action@v1
        with:
          token: ${{ secrets.COOLIFY_DEPLOY_TOKEN }}
          base_url: 'https://coolify.example.com'
          application_uuid: 'your-application-uuid-here'
          force: false
```

### Force Deployment

To force a deployment (useful for manual triggers or when you want to bypass certain checks):

```yaml
- name: Trigger Coolify deployment
  uses: benbristow/coolify-deploy-action@v1
  with:
    token: ${{ secrets.COOLIFY_DEPLOY_TOKEN }}
    base_url: 'https://coolify.example.com'
    application_uuid: 'your-application-uuid-here'
    force: true
```

### Using GitHub Actions Secrets

For better security, you can store all sensitive values as GitHub Actions secrets:

```yaml
name: Deploy to Coolify

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Trigger Coolify deployment
        uses: benbristow/coolify-deploy-action@v1
        with:
          token: ${{ secrets.COOLIFY_DEPLOY_TOKEN }}
          base_url: ${{ secrets.COOLIFY_BASE_URL }}
          application_uuid: ${{ secrets.COOLIFY_APPLICATION_UUID }}
          force: false
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `token` | Coolify API token (Bearer token) | Yes | - |
| `base_url` | Coolify base URL (e.g., `https://coolify.example.com`) | Yes | - |
| `application_uuid` | Application UUID to deploy (e.g., `{application-uuid}`) | Yes | - |
| `force` | Force deployment (boolean: `true`/`false`) | No | `false` |

## Config

### Secrets

You can store sensitive values as GitHub Actions secrets. At minimum, you need:

- `COOLIFY_DEPLOY_TOKEN`: Your Coolify API bearer token (required)

**Optional secrets** (for better security):
- `COOLIFY_BASE_URL`: Your Coolify instance URL (e.g., `https://coolify.example.com`)
- `COOLIFY_APPLICATION_UUID`: Your application UUID

### How to get your Coolify Deploy Token  

1. Navigate to the Keys & Tokens page, API tokens tab - https://your-coolify-instance.com/security/api-tokens
2. Check 'deploy' permission
3. Copy the token, store this somewhere safe.
4. Add it as a secret in your GitHub repository settings

### How to get your Application UUID

The Application UUID is a unique identifier for your application in Coolify.

1. Navigate to your application in Coolify
2. The Application UUID is visible in the URL: `https://your-coolify-instance.com/project/{project-uuid}/environment/{environment-uuid}/application/{application-uuid}`
3. Copy the application UUID part (the last segment after `/application/`, e.g., `{application-uuid}`)

## Contributing

Contributions are welcome! Please open an issue or pull request.

## License

This project is licensed under the terms of the GNU General Public License version 3 or later. See the [LICENSE](LICENSE) file for details.

