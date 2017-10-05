---
title: Monitorare un cluster Azure Kubernetes con CoScale | Microsoft Docs
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
ms.openlocfilehash: f894191baced710fc0f5a8c8692df98033341a48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="a28a2-103">Monitorare un cluster Kubernetes del servizio contenitore di Azure con CoScale</span><span class="sxs-lookup"><span data-stu-id="a28a2-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="a28a2-104">Questo articolo illustra come distribuire l'agente [CoScale](https://www.coscale.com/) per monitorare tutti i nodi e tutti i contenitori del cluster Kubernetes nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="a28a2-104">In this article, we show you how to deploy the [CoScale](https://www.coscale.com/) agent to monitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="a28a2-105">Per questa configurazione, è necessario un account con CoScale.</span><span class="sxs-lookup"><span data-stu-id="a28a2-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="a28a2-106">Informazioni su CoScale</span><span class="sxs-lookup"><span data-stu-id="a28a2-106">About CoScale</span></span> 

<span data-ttu-id="a28a2-107">CoScale è una piattaforma di monitoraggio che raccoglie metriche ed eventi da tutti i contenitori in diverse piattaforme di orchestrazione.</span><span class="sxs-lookup"><span data-stu-id="a28a2-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="a28a2-108">CoScale offre il monitoraggio dello stack completo per gli ambienti Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a28a2-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="a28a2-109">Fornisce visualizzazioni e funzionalità di analisi per tutti i livelli dello stack, ovvero il sistema operativo, Kubernetes, Docker e le applicazioni in esecuzione all'interno dei contenitori.</span><span class="sxs-lookup"><span data-stu-id="a28a2-109">It provides visualizations and analytics for all layers in the stack: the OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="a28a2-110">CoScale offre alcuni dashboard di monitoraggio incorporati e include il rilevamento delle anomalie per consentire a operatori e sviluppatori di individuare rapidamente i problemi relativi all'infrastruttura e alle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="a28a2-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection to allow operators and developers to find infrastructure and application issues fast.</span></span>

![Interfaccia utente di CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="a28a2-112">Come illustrato in questo articolo, è possibile installare gli agenti in un cluster Kubernetes per eseguire CoScale come soluzione SaaS.</span><span class="sxs-lookup"><span data-stu-id="a28a2-112">As shown in this article, you can install agents on a Kubernetes cluster to run CoScale as a SaaS solution.</span></span> <span data-ttu-id="a28a2-113">Se si vogliono conservare i dati in sede, CoScale è disponibile anche per le installazioni locali.</span><span class="sxs-lookup"><span data-stu-id="a28a2-113">If you want to keep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a28a2-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a28a2-114">Prerequisites</span></span>

<span data-ttu-id="a28a2-115">È prima di tutto necessario [creare un account CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="a28a2-115">You first need to [create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="a28a2-116">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a28a2-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="a28a2-117">Si presume anche che gli strumenti dell'interfaccia della riga di comando di Azure `az` e `kubectl` siano installati.</span><span class="sxs-lookup"><span data-stu-id="a28a2-117">It also assumes that you have the `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="a28a2-118">È possibile verificare se lo strumento `az` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="a28a2-118">You can test if you have the `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="a28a2-119">Se lo strumento `az` non è installato, le istruzioni sono disponibili [qui](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a28a2-119">If you don't have the `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="a28a2-120">È possibile verificare se lo strumento `kubectl` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="a28a2-120">You can test if you have the `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="a28a2-121">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="a28a2-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a><span data-ttu-id="a28a2-122">Installazione dell'agente CoScale con DaemonSet</span><span class="sxs-lookup"><span data-stu-id="a28a2-122">Installing the CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="a28a2-123">Gli elementi [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) vengono usati da Kubernetes per eseguire una singola istanza di un contenitore in ogni host del cluster.</span><span class="sxs-lookup"><span data-stu-id="a28a2-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="a28a2-124">Sono ideali per l'esecuzione di agenti di monitoraggio, ad esempio l'agente CoScale.</span><span class="sxs-lookup"><span data-stu-id="a28a2-124">They're perfect for running monitoring agents such as the CoScale agent.</span></span>

<span data-ttu-id="a28a2-125">Dopo l'accesso a CoScale, passare alla [pagina degli agenti](https://app.coscale.com/) per installare gli agenti CoScale nel cluster tramite DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="a28a2-125">After you log in to CoScale, go to the [agent page](https://app.coscale.com/) to install CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="a28a2-126">L'interfaccia utente di CoScale fornisce una procedura guidata per la configurazione per creare un agente e iniziare a monitorare il cluster Kubernetes completo.</span><span class="sxs-lookup"><span data-stu-id="a28a2-126">The CoScale UI provides guided configuration steps to create an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Configurazione dell'agente CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="a28a2-128">Per avviare l'agente sul cluster, eseguire il comando specificato:</span><span class="sxs-lookup"><span data-stu-id="a28a2-128">To start the agent on the cluster, run the supplied command:</span></span>

![Avviare l'agente CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="a28a2-130">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="a28a2-130">That's it!</span></span> <span data-ttu-id="a28a2-131">Con gli agenti operativi, i dati verranno visualizzati nella console entro alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="a28a2-131">Once the agents are up and running, you should see data in the console in a few minutes.</span></span> <span data-ttu-id="a28a2-132">Visitare la [pagina degli agenti](https://app.coscale.com/) per visualizzare un riepilogo del cluster, eseguire procedure aggiuntive per la configurazione e visualizzare i dashboard, ad esempio la **panoramica del cluster Kubernetes**.</span><span class="sxs-lookup"><span data-stu-id="a28a2-132">Visit the [agent page](https://app.coscale.com/) to see a summary of your cluster, perform additional configuration steps, and see dashboards such as the **Kubernetes cluster overview**.</span></span>

![Panoramica del cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="a28a2-134">L'agente CoScale viene distribuito automaticamente nelle nuove macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="a28a2-134">The CoScale agent is automatically deployed on new machines in the cluster.</span></span> <span data-ttu-id="a28a2-135">L'agente viene aggiornato automaticamente al rilascio di una nuova versione.</span><span class="sxs-lookup"><span data-stu-id="a28a2-135">The agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a28a2-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a28a2-136">Next steps</span></span>

<span data-ttu-id="a28a2-137">Per altre informazioni sulle soluzioni di monitoraggio di CoScale, vedere la [documentazione di CoScale](http://docs.coscale.com/) e il [blog](https://www.coscale.com/blog).</span><span class="sxs-lookup"><span data-stu-id="a28a2-137">See the [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

