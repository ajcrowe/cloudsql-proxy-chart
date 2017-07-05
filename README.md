Cloud SQL Proxy Chart
=====================

The [Cloud SQL Proxy](https://cloud.google.com/sql/docs/mysql/sql-proxy) provides secure access to your [Cloud SQL](https://cloud.google.com/sql/docs/) Second Generation instances without having to whitelist IP addresses or configure SSL.

### Introduction

This [Helm](https://helm.sh) chart provides a containerised cloud sql service within your [Kubernetes](https://kubernetes.io) cluster.

### Configuration


replicaCount: 1
image:
  name: b.gcr.io/cloudsql-docker/gce-proxy
  tag: latest
gcp:
  project: projectname
  region: europe-west2
  instance: cloudsql-instance
bind:
  addr: 0.0.0.0
  port: 3306
service:
  name: cloudsql-proxy
  type: ClusterIP
  internalPort: 3306
  externalPort: 3306
credentials: 
  path: /secrets/cloudsql
  file: credentials.json
  secret: cloudsql-credentials
  secret_enabled: true
  b64enc: 
ssl:
  path: /etc/ssl/certs
  hostpath: /etc/ssl/certs


### Install

```
$ helm install --name my-cloudsql-proxy \
    --set 