# Logging standards for Kubernetes

Monitoring logs effectively in a Kubernetes environment requires tools that centralize and streamline log management.Logging in Kubernetes can be a challenge, especially when dealing with data across a distributed, containerized system. To keep your logs efficient and actionable, it’s essential to understand logging best practices, from handling diverse formats to structuring of logs.

## Tools used

We have used the following tools which help us match the logging standards defined below:

* Fluentbit
* Kubernetes exporter
* Cloudwatch log forwarder lambda - [lambda/logforwarder/log_forwarder_lambda.py](https://https://github.com/ONSdigital/dis-infra-cloudwatch-log-forwarder-module)

## What we should be logging

## Logging specification

We have defined the formatting and data structures, including field names and types, we use for logging.

This is important to allow the centralised logging service to properly index the data and make it searchable.  **Any logs not adhering to the specification may be lost.**

### Changes to the spec

Any changes, including the addition of new fields, must be agreed by the team as a whole before being added to this spec.  Any changes to this spec will require changes to all of the [tools used](#tools-used)  as well as the centralised logging service.

### Log structure

#### Common fields

The following are the only top level fields.

| Field name                  | Required | Type                                    | Example                                                              | Description                                                               |
|-----------------------------|----------|-----------------------------------------|----------------------------------------------------------------------|---------------------------------------------------------------------------|
| `kubernetes.annotations`    | No       | [`annotations`](#kubernetes-annotations)|                                                                      | [key-value pairs attached to Kubernetes objects](#kubernetes-annotations) |
| `kubernetes.container_hash` | Yes      | `text`                                  | `11771.dkr.ecr.eu-west-2.amanaws.com/dis/apps/dis-wagil-main@sha256` | Container hash information                                                |
| `kubernetes.container_image`| Yes      | `text`                                  | `11771.dkr.ecr.eu-west-2.amanaws.com/dis/apps/dis-wagil-main:12345`  | Container image information                                               |
| `kubernetes.container_name` | Yes      | `text`                                  | `sync-teams-cron`                                                    | Container name information                                                |
| `kubernetes.docker_id`      | Yes      | `text`                                  | `775cac02b25b9b0fd35bd86c5c0c2e4e226a6`                              | Docker id  information                                                    |
| `kubernetes.host`           | Yes      | `text`                                  | `ip-10-30-107-46.eu-west-2.compute.internal`                         | Ip address where the app has been deployed                                |
| `kubernetes.labels`         | Yes      | [`labels`](#kubernetes-labels)          |                                                                      | [`key-value pairs associated with Kubernetes object`](#kubernetes-labels) |
| `kubernetes.namespace_name` | Yes      | `text`                                  | `wagtail-main`                                                       | Represents a scope for the name of the resources                          |
| `kubernetes.pod_id`         | Yes      | `text`                                  | `6b9e7-1531-453-bfa-d1c2ff86d`                                       | Unique id across the whole cluster                                        |
| `kubernetes.pod_name`       | Yes      | `text`                                  | `main-sync-teams-cron`                                               | Pod name which is unique across the cluster                               |

#### Kubernetes annotations

Kubernetes annotations are key-value pairs attached to Kubernetes objects, providing a flexible way to extend the functionality of your Kubernetes resources without altering their internal specifications.

| Field name                                                          | Required | Type           | Example                      | Description                                                   |
|---------------------------------------------------------------------|----------|----------------|------------------------------|---------------------------------------------------------------|
| `checksum/config`                                                   | No      | `text`          | `236578`                     |                                                               |
| `checksum/configmap`                                                | No      | `text`          |                              |                                                               |
| `checksum/health`                                                   | No      | `text`          |                              |                                                               |
| `checksum/scripts`                                                  | No      | `text`          |                              |                                                               |
| `checksum/secret`                                                   | No      | `text`          |                              |                                                               |
| `container_apparmor_security_beta_kubernetes_io/aws-guardduty-agent`| No      | `text`          |                              |                                                               |
| `kubectl_kubernetes_io/default-container`                           | No      | `text`          |                              | Default container name                                        |
| `kubectl_kubernetes_io/restartedAt`                                 | No      | `text`          | `Apr 1, 2025 @ 11:26:03.000` | Date/time string of the request start time                    |
| `opentelemetry-operator-config/sha256`                              | No      | `text`          |                              | Opentelementry config sha.                                    |
| `started_at`                                                        | No      | `text`          | `2019-01-21T16:19:12.356Z`   | ISO8601 date string of the request start time                 |
| `prometheus_io/path`                                                | No      | `text`          |                              | The HTTP status code                                          |
| `prometheus_io/port`                                                | No      | `text`          | `10254`                      | Prometheus port                                               |
| `prometheus_io/scrape`                                              | No      | `text`          | `true`                       | Prometheus scrape enabled/disaled                             |

#### Kubernetes labels

| Field name                                                          | Required | Type           | Example                      | Description                                                   |
|---------------------------------------------------------------------|----------|----------------|------------------------------|---------------------------------------------------------------|
| `app`                                                               | Yes      | `text`         | `236578ebs-csi-controller`   | App name                                                      |
| `app_kubernetes_io/component`                                       | Yes      | `text`         | `mongodb`                    |                                                               |
| `app_kubernetes_io/instance`                                        | Yes      | `text`         | `sandbox`                    | The instance where the app is deployed                        |
| `app_kubernetes_io/managed-by`                                      | Yes      | `text`         | `Helm`                       | How the app is managed                                        |
| `app_kubernetes_io/name`                                            | Yes      | `text`         | `mongodb`                    | The name of the app                                           |
| `app_kubernetes_io/part-of`                                         | No       | `text`         | `ingress-nginx`              | The app which it belongs to                                   |
| `app_kubernetes_io/version`                                         | Yes      | `text`         | `8.0.4`                      | The version of Kubernetes app.                                |
| `apps_kubernetes_io/pod-index`                                      | No       | `text`         | `wagtail-main-sync-teams`    | The length of the response                                    |
| `batch_kubernetes_io/controller-uid`                                | No       | `text`         | `b8e7-452c-a73c-cb9c05b75e`  | The scheme or protocol from the URL                           |
| `batch_kubernetes_io/job-name`                                      | No       | `text`         | `wagtail-main-sync-cron`     |                                                               |
| `control-plane`                                                     | No       | `text`         |                              |                                                               |
| `controller-revision-hash`                                          | No       | `text`         |                              |                                                               |
| `controller-uid`                                                    | No       | `text`         | `1e4e6582-94ac-492d-95e8`    | The UUid of the controller                                    |
| `eks_amazonaws_com/component`                                       | No       | `text`         |                              |                                                               |
| `helm_sh/chart`                                                     | No       | `text`         | `wagtail-cms-0.0.0`          | Name of the helm chart                                        |
| `job-name`                                                          | No       | `text`         | `wagtail-teams-cron-29354924`| Job name which creates the pods for the application           |
| `k8s-app`                                                           | No       | `text`         | `kube-proxy`                 | Kubernetes app name                                           |
| `pod-template-generation`                                           | No       | `text`         | `45`                         |                                                               |
| `pod-template-hash`                                                 | No       | `text`         | `56c4c74bcc`                 | Pod template hash deployed                                    |
| `statefulset_kubernetes_io/pod-name`                                | No       | `text`         | `wagtail-main`               | Pod name deployed by the application                          |
| `ons_gov_uk/applogs`                                                | No       | `text`         | `true`                       | check if the application is our                               |
