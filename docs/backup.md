# Backing Up MinIO Data

Scenario:

- You have the "dev" instance of MinIO running in the `uds-dev-stack` namespace
- You have provisioned a new bucket called "zarf-registry" and wired up the Zarf init package to leverage it as its container registry backend
- Using the minio operator, you deployed a second MinIO tenant

Use the mc cli tool found within your MinIO container to back up data from the "dev" MinIO instance to the new MinIO tenant.

- netpol needed to be created to allow egress from the minio operator tenant
  - just egress 9000 was needed, hbone/ztunnel was already allowed, uds-dev-stack is not protected by uds operator
  - the root of this repo contains an example netpol that is outputted by the ADDITIONAL_NETWORK_ALLOW config override during bundle deployment

```bash
mc mb new/zarf-registry

mc mirror --overwrite --preserve old/zarf-registry new/zarf-registry
```
