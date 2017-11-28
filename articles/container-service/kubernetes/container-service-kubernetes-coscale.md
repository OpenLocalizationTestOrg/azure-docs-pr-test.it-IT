---
title: aaaMonitor un Kubernetes Azure cluster con CoScale | Documenti Microsoft
description: Monitorare un cluster Kubernetes nel servizio contenitore di Azure tramite CoScale
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="82e63-103">Monitorare un cluster Kubernetes del servizio contenitore di Azure con CoScale</span><span class="sxs-lookup"><span data-stu-id="82e63-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="82e63-104">In questo articolo verrà illustrato come hello toodeploy [CoScale](https://www.coscale.com/) toomonitor agente tutti i nodi e i contenitori il Kubernetes cluster nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="82e63-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="82e63-105">Per questa configurazione, è necessario un account con CoScale.</span><span class="sxs-lookup"><span data-stu-id="82e63-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="82e63-106">Informazioni su CoScale</span><span class="sxs-lookup"><span data-stu-id="82e63-106">About CoScale</span></span> 

<span data-ttu-id="82e63-107">CoScale è una piattaforma di monitoraggio che raccoglie metriche ed eventi da tutti i contenitori in diverse piattaforme di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="82e63-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="82e63-108">CoScale offre il monitoraggio dello stack completo per gli ambienti Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="82e63-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="82e63-109">Fornisce visualizzazioni e analitica per tutti i livelli dello stack hello: hello OS, Kubernetes, Docker e applicazioni eseguiti all'interno di ai contenitori.</span><span class="sxs-lookup"><span data-stu-id="82e63-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="82e63-110">CoScale offre diversi dashboard di monitoraggio predefinite e ha operatori tooallow rilevamento di anomalie predefiniti e problemi di infrastruttura e applicazione toofind sviluppatori veloci.</span><span class="sxs-lookup"><span data-stu-id="82e63-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![Interfaccia utente di CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="82e63-112">Come illustrato in questo articolo, è possibile installare gli agenti in un toorun cluster Kubernetes CoScale come una soluzione SaaS.</span><span class="sxs-lookup"><span data-stu-id="82e63-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="82e63-113">Se si desidera tookeep i dati localmente, CoScale è anche disponibile per l'installazione locale.</span><span class="sxs-lookup"><span data-stu-id="82e63-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="82e63-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="82e63-114">Prerequisites</span></span>

<span data-ttu-id="82e63-115">È innanzitutto necessario troppo[creare un account CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="82e63-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="82e63-116">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="82e63-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="82e63-117">Inoltre, presuppone di aver hello `az` CLI di Azure e `kubectl` installati gli strumenti.</span><span class="sxs-lookup"><span data-stu-id="82e63-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="82e63-118">È possibile verificare se si dispone di hello `az` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="82e63-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="82e63-119">Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="82e63-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="82e63-120">È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="82e63-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="82e63-121">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="82e63-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="82e63-122">L'installazione dell'agente CoScale hello con un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="82e63-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="82e63-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) sono utilizzato da Kubernetes toorun una singola istanza di un contenitore in ogni host in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="82e63-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="82e63-124">Sono ideali per l'esecuzione di agenti di monitoraggio, ad esempio agente CoScale hello.</span><span class="sxs-lookup"><span data-stu-id="82e63-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="82e63-125">Dopo l'accesso tooCoScale, visitare toohello [pagina agente](https://app.coscale.com/) agenti CoScale tooinstall nel cluster utilizzando un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="82e63-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="82e63-126">Hello dell'interfaccia utente CoScale fornisce toocreate passaggi di configurazione guidata un agente e avvia il monitoraggio dei cluster Kubernetes completo.</span><span class="sxs-lookup"><span data-stu-id="82e63-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configurazione dell'agente CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="82e63-128">agente di hello toostart nel cluster hello, eseguire il comando hello fornito:</span><span class="sxs-lookup"><span data-stu-id="82e63-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Avviare l'agente CoScale hello](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="82e63-130">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="82e63-130">That's it!</span></span> <span data-ttu-id="82e63-131">Una volta agenti hello siano in esecuzione, verranno visualizzati i dati nella console di hello in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="82e63-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="82e63-132">Visitare hello [pagina agente](https://app.coscale.com/) toosee un riepilogo del cluster, eseguire ulteriori passaggi di configurazione e visualizzare i dashboard, ad esempio hello **Kubernetes cluster Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="82e63-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Panoramica del cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="82e63-134">agente CoScale Hello viene distribuito automaticamente in nuovi computer nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="82e63-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="82e63-135">Aggiornamenti agente Hello automaticamente quando viene rilasciata una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="82e63-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82e63-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82e63-136">Next steps</span></span>

<span data-ttu-id="82e63-137">Vedere hello [CoScale documentazione](http://docs.coscale.com/) e [blog](https://www.coscale.com/blog) per ulteriori informazioni sulle soluzioni di monitoraggio CoScale.</span><span class="sxs-lookup"><span data-stu-id="82e63-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

