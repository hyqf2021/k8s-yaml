# MySQL Helm Chart

This chart deploys a MySQL StatefulSet with one primary pod and replica pods using GTID replication.

## Install

```powershell
helm install mysql ./mysql
```

## Override Passwords

```powershell
helm install mysql ./mysql `
  --set auth.rootPassword='change-me' `
  --set auth.replicationPassword='change-me-too'
```

## Use Existing Secret

The secret must contain the keys configured by `auth.rootPasswordKey` and `auth.replicationPasswordKey`.

```powershell
helm install mysql ./mysql `
  --set auth.existingSecret='mysql-secret'
```

## Render Locally

```powershell
helm template mysql ./mysql
```

## Services

- `mysql-write`: routes writes to pod `mysql-0`.
- `mysql-read`: routes reads to all MySQL pods.
- `mysql`: headless service used by the StatefulSet.
