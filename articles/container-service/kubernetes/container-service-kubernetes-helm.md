---
title: contenitori aaaDeploy con Helm in Azure Kubernetes | Documenti Microsoft
description: Usare i contenitori toodeploy hello Helm imballaggio strumento in un cluster Kubernetes contenitore nel servizio di Azure
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Usare contenitori toodeploy Helm in un cluster Kubernetes 

[Helm](https://github.com/kubernetes/helm/) è uno strumento di creazione di pacchetti open source che consente di installare e gestire hello del ciclo di vita delle applicazioni Kubernetes. Gestori di pacchetti tooLinux simili, ad esempio Apt get e Yum, Helm è usato toomanage Kubernetes grafici che sono pacchetti di risorse Kubernetes preconfigurati. Questo articolo illustra la modalità di distribuzione toowork con Helm in un cluster Kubernetes contenitore nel servizio di Azure.

Helm presenta due componenti: 
* Hello **Helm CLI** è un client in esecuzione nel computer in locale o cloud hello  

* **Barra** è un server in esecuzione nel cluster Kubernetes hello e gestisce hello del ciclo di vita delle applicazioni Kubernetes 
 
## <a name="prerequisites"></a>Prerequisiti

* [Creare un cluster Kubernetes](container-service-kubernetes-walkthrough.md) nel servizio contenitore di Azure

* [Installare e configurare `kubectl`](../container-service-connect.md) in un computer locale

* [Installare Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) in un computer locale

## <a name="helm-basics"></a>Nozioni di base di Helm 

tooview informazioni hello Kubernetes cluster che si installa barra e la distribuzione di applicazioni a digitare hello comando seguente:

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Dopo aver installato Helm, installare il cluster Kubernetes barra digitando hello comando seguente:

```bash
helm init --upgrade
```
Quando è stata completata correttamente, viene visualizzato l'output seguente hello:

![Installazione di Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview dei comandi di tutti i hello Helm grafici disponibili nel repository hello hello tipo seguente:

```bash 
helm search 
```

Viene visualizzato l'output seguente hello:

![Ricerca Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello grafici tooget hello versioni più recenti, digitare:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Distribuire un grafico controller in ingresso Nginx 
 
toodeploy un grafico di controller Nginx in ingresso, digitare un comando singolo:

```bash
helm install stable/nginx-ingress 
```
![Distribuire il controller in ingresso](./media/container-service-kubernetes-helm/nginx-ingress.png)

Se si digita `kubectl get svc` tooview tutti i servizi in esecuzione nel cluster hello, vedrai che viene assegnato un indirizzo IP controller in ingresso toohello. (Durante l'assegnazione di hello è in corso, vedere `<pending>`. Accetta un paio di minuti toocomplete). 

Una volta assegnato l'indirizzo IP hello, passare toohello valore hello esterno IP indirizzo toosee hello Nginx back-end in esecuzione. 
 
![Indirizzo IP in ingresso](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee un elenco di grafici installato nel cluster, tipo:

```bash
helm list 
```

È possibile abbreviare il comando di hello troppo`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Distribuire un client e un grafico di MariaDB

Distribuire ora un grafico MariaDB e un database di toohello MariaDB tooconnect client.

toodeploy hello MariaDB grafico hello tipo comando seguente:

```bash
helm install --name v1 stable/mariadb
```

dove `--name` è un tag usato per le versioni.

> [!TIP]
> Se la distribuzione di hello non riesce, eseguire `helm repo update` e riprovare.
>
 
 
tooview tutti i grafici di hello distribuito nel cluster, tipo:

```bash 
helm list
```
 
tooview tutte le distribuzioni in esecuzione nel cluster, digitare:

```bash
kubectl get deployments 
``` 
 
 
Infine, toorun un client di hello tooaccess pod, digitare:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
client toohello tooconnect, hello tipo comando seguente, sostituendo `v1-mariadb` con nome hello della distribuzione:

```bash
sudo mysql –h v1-mariadb
```
 
 
È ora possibile utilizzare i database toocreate comandi SQL standard, tabelle e così via. Ad esempio, `Create DATABASE testdb1;` crea un database vuoto. 
 
 
 
## <a name="next-steps"></a>Passaggi successivi

* Per ulteriori informazioni sulla gestione Kubernetes grafici, vedere hello [ad documentazione](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

