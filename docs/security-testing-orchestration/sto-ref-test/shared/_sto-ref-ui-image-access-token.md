The access token used to log in to the container registry. In most cases this is a password or an API key. You should [create a secret](/docs/platform/security/add-file-secrets) with your encrypted token and reference the secret using the format `<+secrets.getValue(project.container-access-id>`.  

| CI stage YAML key | SecurityTests stage YAML key |
| ------------ | ----------------------- |
| `container_access_token` | `access_token` |