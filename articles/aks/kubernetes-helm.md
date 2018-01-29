---
title: Distribuire contenitori con Helm in Kubernetes in Azure
description: Usare lo strumento per la creazione di pacchetti Helm per distribuire contenitori in un cluster Kubernetes nel servizio contenitore di Azure
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 10/24/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 39c6de1ce2443cf027d7cde067281355ea0b7207
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2017
---
# <a name="use-helm-with-azure-container-service-aks"></a>Usare Helm con il servizio contenitore di Azure

[Helm] [ helm] è uno strumento di creazione di pacchetti open source che consente di installare e gestire il ciclo di vita delle applicazioni Kubernetes. Analogamente agli strumenti di gestione pacchetti Linux, come *APT* e *Yum*, Helm viene usato per gestire i grafici per Kubernetes, che sono pacchetti di risorse Kubernetes preconfigurate.

Questo documento illustra la configurazione e l'uso di Helm in un cluster Kubernetes nel servizio contenitore di Azure.

## <a name="before-you-begin"></a>Prima di iniziare

I passaggi dettagliati contenuti in questo documento presuppongono che sia stato creato un cluster del servizio contenitore di Azure e che sia stata stabilita una connessione kubectl al cluster. Se è necessario di questi elementi, vedere il [delle Guide rapide AKS][aks-quickstart].

## <a name="install-helm-cli"></a>Installare l'interfaccia della riga di comando di Helm

L'interfaccia della riga di comando di Helm è un client eseguito nel sistema di sviluppo che consente di avviare, arrestare e gestire applicazioni con grafici Helm.

Se si usa Azure Cloud Shell, l'interfaccia della riga di comando di Helm è già installata. Per installare l'interfaccia della riga di comando di Helm in un computer Mac, usare `brew`. Per altre informazioni, vedere Opzioni [installazione Helm][helm-install-options].

```console
brew install kubernetes-helm
```

Output:

```
==> Downloading https://homebrew.bintray.com/bottles/kubernetes-helm-2.6.2.sierra.bottle.1.tar.gz
######################################################################## 100.0%
==> Pouring kubernetes-helm-2.6.2.sierra.bottle.1.tar.gz
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
==> Summary
🍺  /usr/local/Cellar/kubernetes-helm/2.6.2: 50 files, 132.4MB
```

## <a name="configure-helm"></a>Configurare Helm

Il [helm init] [ helm-init] comando viene utilizzato per installare i componenti di Helm in un cluster Kubernetes e apportare le configurazioni sul lato client. Eseguire il comando seguente per installare Helm sul cluster AKS e configurare il client Helm.

```azurecli-interactive
helm init
```

Output:

```
$HELM_HOME has been configured at /home/user/.helm.

Tiller (the Helm server-side component) has been installed into your Kubernetes Cluster.
Happy Helming!
```

## <a name="find-helm-charts"></a>Trovare i grafici Helm

I grafici Helm vengono usati per distribuire applicazioni in un cluster Kubernetes. Per eseguire una ricerca per i grafici Helm creati in precedenza, utilizzare il [ricerca helm] [ helm-search] comando.

```azurecli-interactive
helm search
```

L'output sarà simile al seguente, ma con molti più grafici.

```
NAME                            VERSION DESCRIPTION
stable/acs-engine-autoscaler    2.0.0   Scales worker nodes within agent pools
stable/artifactory              6.1.0   Universal Repository Manager supporting all maj...
stable/aws-cluster-autoscaler   0.3.1   Scales worker nodes within autoscaling groups.
stable/buildkite                0.2.0   Agent for Buildkite
stable/centrifugo               2.0.0   Centrifugo is a real-time messaging server.
stable/chaoskube                0.5.0   Chaoskube periodically kills random pods in you...
stable/chronograf               0.3.0   Open-source web application written in Go and R...
stable/cluster-autoscaler       0.2.0   Scales worker nodes within autoscaling groups.
stable/cockroachdb              0.5.0   CockroachDB is a scalable, survivable, strongly...
stable/concourse                0.7.0   Concourse is a simple and scalable CI system.
stable/consul                   0.4.1   Highly available and distributed service discov...
stable/coredns                  0.5.0   CoreDNS is a DNS server that chains middleware ...
stable/coscale                  0.2.0   CoScale Agent
stable/dask-distributed         2.0.0   Distributed computation in Python
stable/datadog                  0.8.0   DataDog Agent
...
```

Per aggiornare l'elenco dei grafici, utilizzare il [aggiornamento repository helm] [ helm-repo-update] comando.

```azurecli-interactive
helm repo update
```

Output:

```
Hang tight while we grab the latest from your chart repositories...
...Skip local chart repository
...Successfully got an update from the "stable" chart repository
Update Complete. ⎈ Happy Helming!⎈
```

## <a name="run-helm-charts"></a>Eseguire i grafici Helm

Per distribuire un controller di ingresso NGINX, utilizzare il [helm installazione] [ helm-install] comando.

```azurecli-interactive
helm install stable/nginx-ingress
```

L'output sarà simile al seguente, ma includerà informazioni aggiuntive, ad esempio istruzioni su come usare la distribuzione di Kubernetes.

```
NAME:   tufted-ocelot
LAST DEPLOYED: Thu Oct  5 00:48:04 2017
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/ConfigMap
NAME                                    DATA  AGE
tufted-ocelot-nginx-ingress-controller  1     5s

==> v1/Service
NAME                                         CLUSTER-IP   EXTERNAL-IP  PORT(S)                     AGE
tufted-ocelot-nginx-ingress-controller       10.0.140.10  <pending>    80:30486/TCP,443:31358/TCP  5s
tufted-ocelot-nginx-ingress-default-backend  10.0.34.132  <none>       80/TCP                      5s

==> v1beta1/Deployment
NAME                                         DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
tufted-ocelot-nginx-ingress-controller       1        1        1           0          5s
tufted-ocelot-nginx-ingress-default-backend  1        1        1           1          5s
...
```

Per ulteriori informazioni sull'uso di un controller di ingresso NGINX con Kubernetes, vedere [NGINX in ingresso Controller][nginx-ingress].

## <a name="list-helm-charts"></a>Visualizzare un elenco dei grafici Helm

Per visualizzare un elenco di grafici installato nel cluster, utilizzare il [elenco helm] [ helm-list] comando.

```azurecli-interactive
helm list
```

Output:

```
NAME            REVISION    UPDATED                     STATUS      CHART               NAMESPACE
bilging-ant     1           Thu Oct  5 00:11:11 2017    DEPLOYED    nginx-ingress-0.8.7 default
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla gestione dei grafici per Kubernetes, vedere la documentazione di Helm.

> [!div class="nextstepaction"]
> [Documentazione Helm][helm-documentation]

<!-- LINKS - external -->
[helm]: https://github.com/kubernetes/helm/
[helm-documentation]: https://github.com/kubernetes/helm/blob/master/docs/index.md
[helm-init]: https://docs.helm.sh/helm/#helm-init
[helm-install]: https://docs.helm.sh/helm/#helm-install
[helm-install-options]: https://github.com/kubernetes/helm/blob/master/docs/install.md
[helm-list]: https://docs.helm.sh/helm/#helm-list
[helm-repo-update]: https://docs.helm.sh/helm/#helm-repo-update
[helm-search]: https://docs.helm.sh/helm/#helm-search
[nginx-ingress]: https://github.com/kubernetes/ingress-nginx

<!-- LINKS - internal -->
[aks-quickstart]: ./kubernetes-walkthrough.md