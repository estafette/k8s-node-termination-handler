
# Purpose

The [k8s-node-termination-handler](https://github.com/GoogleCloudPlatform/k8s-node-termination-handler) application is a way to ensure a preemptible node receives a signal when it's going to be preempted in order for Kubernetes to update it's administration. Without a node just gets lost and it takes a while for Kubernetes to realize that it's gone and update it's administration. In the mean time request can continue to be sent to pods that are no longer there. This is especially harmful for applications like kube-dns.

This repository packages the applications as a Helm chart.

# Installation

To install the application using Helm run the following steps:

```bash
helm repo add estafette https://helm.estafette.io
helm upgrade --install estafette-gke-preemptible-killer --namespace estafette estafette/estafette-gke-preemptible-killer
```

# Miscellaneous

To prevent preemptibles in your GKE cluster from getting mass replaced after their max lifetime of 24 hours you can run [estafette-gke-preemptible-killer](https://github.com/estafette/estafette-gke-preemptible-killer), which tries to spread their termination - when not preempted before their max lifetime - so they do not mass terminate at the same time.