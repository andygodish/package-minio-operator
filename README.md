# Package: Minio Operator

Deploy the [Core Minio Operator](https://github.com/defenseunicorns/uds-package-minio-operator) package configured to your environment.

- Tenant mode always enables erasure coding.

Even with a single server, MinIO requires multiple volumes:
  
- MinIO treats each PVC as a “drive.”
- Erasure coding stripes and shards objects across them.
- This is why your single-node tenant creates four PVCs by default.

- There is no “single filesystem bucket mode” when deployed via operator.

If you want a single volume, you must:

```yaml
volumesPerServer: 1
```

but it remains a Tenant—just a 1-drive EC cluster (no redundancy).
