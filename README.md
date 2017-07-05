Cloud SQL Proxy Chart
=====================

The [Cloud SQL Proxy](https://cloud.google.com/sql/docs/mysql/sql-proxy) provides secure access to your [Cloud SQL](https://cloud.google.com/sql/docs/) Second Generation instances without having to whitelist IP addresses or configure SSL.

### Introduction

This [Helm](https://helm.sh) chart provides a containerised cloud sql service within your [Kubernetes](https://kubernetes.io) cluster.

### Configuration

Below is a list of all configuration parameters available, items in **bold** are required settings

| Parameter                  | Description                            | Default                              |
|----------------------------|----------------------------------------|--------------------------------------|
**`gcp.project`**            | Google Cloud Platform project          |  `projectname`                       |
**`gcp.region`**             | Google Cloud Platford region           |  `europe-west2`                      |
**`gcp.instance`**           | Name of your Cloud SQL instance        | `cloudsql-instance`                  |
`image.name`                 | The image repository to pull           | `b.gcr.io/cloudsql-docker/gce-proxy` |
`image.tag`                  | The image tag to pull                  | `latest`                             |
`replicaCount`               | Number of pods to run in deployment    | `1`                                  |
`bind.addr`                  | Bind address for the container         | `0.0.0.0`                            |
`bind.port`                  | Bind port for the container            | `3306`                               |
`service.name`               | Service name                           | `cloudsql-proxy`                     |
`service.type`               | Service type                           | `ClusterIP`                          |
`service.externalPort`       | Service external port                  |  `3306`                              |
`credentials.path`           | Where to mount credentials             | `/secrets/cloudsql`                  |
`credentials.file`           | Where to look for a credentials file   | `credentials.json`                   |
`credentials.secret`         | The name for the credentials secret    | `cloudsql-credentials`               |
`credentials.secret_enabled` | Whether to create a credentials secret | `true`                               |
`credentials.b64enc`         | Base64 encoded credentials             | `nil`                                |
`ssl.path`                   | SSL mount path within container        | `/etc/ssl/certs`                     |
`ssl.hostpath`               | SSL certs host location                | `/etc/ssl/certs`                     |


### Install

```bash
$ git clone https://github.com/ajcrowe/cloudsql-proxy-chart.git cloudsql-proxy
$ helm install --name my-cloudsql-proxy \
    --set gcp.project=my-gcp-project \
    --set gcp.region=europe-west1 \
    --set gcp.instance=my-cloudsql-master \
    --set credentials.file=/path/to/credentials.json
    cloudsql-proxy
```

### Uninstall

```bash
$ helm delete my-cloud-proxy
```

