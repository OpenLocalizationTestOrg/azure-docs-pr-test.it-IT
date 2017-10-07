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
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="87208-103">Usare contenitori toodeploy Helm in un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="87208-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="87208-104">[Helm](https://github.com/kubernetes/helm/) è uno strumento di creazione di pacchetti open source che consente di installare e gestire hello del ciclo di vita delle applicazioni Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="87208-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="87208-105">Gestori di pacchetti tooLinux simili, ad esempio Apt get e Yum, Helm è usato toomanage Kubernetes grafici che sono pacchetti di risorse Kubernetes preconfigurati.</span><span class="sxs-lookup"><span data-stu-id="87208-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="87208-106">Questo articolo illustra la modalità di distribuzione toowork con Helm in un cluster Kubernetes contenitore nel servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="87208-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="87208-107">Helm presenta due componenti:</span><span class="sxs-lookup"><span data-stu-id="87208-107">Helm has two components:</span></span> 
* <span data-ttu-id="87208-108">Hello **Helm CLI** è un client in esecuzione nel computer in locale o cloud hello</span><span class="sxs-lookup"><span data-stu-id="87208-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="87208-109">**Barra** è un server in esecuzione nel cluster Kubernetes hello e gestisce hello del ciclo di vita delle applicazioni Kubernetes</span><span class="sxs-lookup"><span data-stu-id="87208-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="87208-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="87208-110">Prerequisites</span></span>

* <span data-ttu-id="87208-111">[Creare un cluster Kubernetes](container-service-kubernetes-walkthrough.md) nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="87208-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="87208-112">[Installare e configurare `kubectl`](../container-service-connect.md) in un computer locale</span><span class="sxs-lookup"><span data-stu-id="87208-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="87208-113">[Installare Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) in un computer locale</span><span class="sxs-lookup"><span data-stu-id="87208-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="87208-114">Nozioni di base di Helm</span><span class="sxs-lookup"><span data-stu-id="87208-114">Helm basics</span></span> 

<span data-ttu-id="87208-115">tooview informazioni hello Kubernetes cluster che si installa barra e la distribuzione di applicazioni a digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="87208-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="87208-117">Dopo aver installato Helm, installare il cluster Kubernetes barra digitando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="87208-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="87208-118">Quando è stata completata correttamente, viene visualizzato l'output seguente hello:</span><span class="sxs-lookup"><span data-stu-id="87208-118">When it completes successfully, you see output like hello following:</span></span>

![Installazione di Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="87208-120">tooview dei comandi di tutti i hello Helm grafici disponibili nel repository hello hello tipo seguente:</span><span class="sxs-lookup"><span data-stu-id="87208-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="87208-121">Viene visualizzato l'output seguente hello:</span><span class="sxs-lookup"><span data-stu-id="87208-121">You see output like hello following:</span></span>

![Ricerca Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="87208-123">tooupdate hello grafici tooget hello versioni più recenti, digitare:</span><span class="sxs-lookup"><span data-stu-id="87208-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="87208-124">Distribuire un grafico controller in ingresso Nginx</span><span class="sxs-lookup"><span data-stu-id="87208-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="87208-125">toodeploy un grafico di controller Nginx in ingresso, digitare un comando singolo:</span><span class="sxs-lookup"><span data-stu-id="87208-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Distribuire il controller in ingresso](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="87208-127">Se si digita `kubectl get svc` tooview tutti i servizi in esecuzione nel cluster hello, vedrai che viene assegnato un indirizzo IP controller in ingresso toohello.</span><span class="sxs-lookup"><span data-stu-id="87208-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="87208-128">(Durante l'assegnazione di hello è in corso, vedere `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="87208-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="87208-129">Accetta un paio di minuti toocomplete).</span><span class="sxs-lookup"><span data-stu-id="87208-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="87208-130">Una volta assegnato l'indirizzo IP hello, passare toohello valore hello esterno IP indirizzo toosee hello Nginx back-end in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="87208-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Indirizzo IP in ingresso](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="87208-132">toosee un elenco di grafici installato nel cluster, tipo:</span><span class="sxs-lookup"><span data-stu-id="87208-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="87208-133">È possibile abbreviare il comando di hello troppo`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="87208-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="87208-134">Distribuire un client e un grafico di MariaDB</span><span class="sxs-lookup"><span data-stu-id="87208-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="87208-135">Distribuire ora un grafico MariaDB e un database di toohello MariaDB tooconnect client.</span><span class="sxs-lookup"><span data-stu-id="87208-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="87208-136">toodeploy hello MariaDB grafico hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="87208-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="87208-137">dove `--name` è un tag usato per le versioni.</span><span class="sxs-lookup"><span data-stu-id="87208-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="87208-138">Se la distribuzione di hello non riesce, eseguire `helm repo update` e riprovare.</span><span class="sxs-lookup"><span data-stu-id="87208-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="87208-139">tooview tutti i grafici di hello distribuito nel cluster, tipo:</span><span class="sxs-lookup"><span data-stu-id="87208-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="87208-140">tooview tutte le distribuzioni in esecuzione nel cluster, digitare:</span><span class="sxs-lookup"><span data-stu-id="87208-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="87208-141">Infine, toorun un client di hello tooaccess pod, digitare:</span><span class="sxs-lookup"><span data-stu-id="87208-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="87208-142">client toohello tooconnect, hello tipo comando seguente, sostituendo `v1-mariadb` con nome hello della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="87208-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="87208-143">È ora possibile utilizzare i database toocreate comandi SQL standard, tabelle e così via. Ad esempio, `Create DATABASE testdb1;` crea un database vuoto.</span><span class="sxs-lookup"><span data-stu-id="87208-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="87208-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87208-144">Next steps</span></span>

* <span data-ttu-id="87208-145">Per ulteriori informazioni sulla gestione Kubernetes grafici, vedere hello [ad documentazione](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="87208-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

