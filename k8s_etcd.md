```markdown
# ETCDCTL CLI Tool

`ETCDCTL` is the CLI tool used to interact with **ETCD**. It can interact with the ETCD Server using two API versions: **Version 2** and **Version 3**. By default, it is set to use **Version 2**. Each version has a different set of commands.

## Commands by Version

### ETCDCTL Version 2 Commands:
- `etcdctl backup`
- `etcdctl cluster-health`
- `etcdctl mk`
- `etcdctl mkdir`
- `etcdctl set`

### ETCDCTL Version 3 Commands:
- `etcdctl snapshot save`
- `etcdctl endpoint health`
- `etcdctl get`
- `etcdctl put`

## Setting the API Version

To set the correct API version, use the environment variable `ETCDCTL_API`.

```bash
export ETCDCTL_API=3
```

- If the API version is not set, it defaults to **Version 2**, and the **Version 3** commands will not work.
- When the API version is set to **Version 3**, the **Version 2** commands will not work.

## Authentication with Certificates

To authenticate `ETCDCTL` with the ETCD API Server, you must specify the path to the certificate files. These files are typically located in the `etcd-master` at the following paths:

- `--cacert /etc/kubernetes/pki/etcd/ca.crt`
- `--cert /etc/kubernetes/pki/etcd/server.crt`
- `--key /etc/kubernetes/pki/etcd/server.key`

> **Note**: We discuss more about certificates in the security section of this course. Don't worry if this seems complex for now.

## Example Command

For the commands shown in the previous video to work, you must specify both the `ETCDCTL_API` version and the path to the certificate files. Below is an example command:

```bash
kubectl exec etcd-controlplane -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / \
  --prefix --keys-only --limit=10 / \
  --cacert /etc/kubernetes/pki/etcd/ca.crt \
  --cert /etc/kubernetes/pki/etcd/server.crt \
  --key /etc/kubernetes/pki/etcd/server.key"
```

This command retrieves keys from the ETCD server using **Version 3** of the API, with authentication provided via the specified certificate files.
```
