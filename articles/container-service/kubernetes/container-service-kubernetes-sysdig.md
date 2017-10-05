---
title: Monitorare un cluster Azure Kubernetes - Sysdig | Documentazione Microsoft
description: Monitoraggio di cluster Kubernetes nel servizio contenitore di Azure con Sysdig
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: afe22b84015526f901111238e36baaa94694ccbf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="5e454-103">Monitorare un cluster Kubernetes del servizio contenitore di Azure con Sysdig</span><span class="sxs-lookup"><span data-stu-id="5e454-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e454-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5e454-104">Prerequisites</span></span>
<span data-ttu-id="5e454-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5e454-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="5e454-106">Si presume inoltre che gli strumenti azure cli e kubectl siano installati.</span><span class="sxs-lookup"><span data-stu-id="5e454-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="5e454-107">È possibile verificare se lo strumento `az` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="5e454-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="5e454-108">Se lo strumento `az` non è installato, le istruzioni sono disponibili [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="5e454-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="5e454-109">È possibile verificare se lo strumento `kubectl` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="5e454-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="5e454-110">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="5e454-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="5e454-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="5e454-111">Sysdig</span></span>
<span data-ttu-id="5e454-112">Sysdig è una società che offre uno strumento di monitoraggio esterno come servizio, che consente di monitorare i contenuti nel cluster Kubernetes in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e454-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="5e454-113">L'uso di Sysdig richiede un account Sysdig attivo.</span><span class="sxs-lookup"><span data-stu-id="5e454-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="5e454-114">È possibile iscriversi per creare un account nel rispettivo [sito](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="5e454-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="5e454-115">Una volta connessi al sito Web del cloud di Sysdig, fare clic sul nome utente. Nella pagina verrà visualizzata la chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="5e454-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Chiave API di Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="5e454-117">Installazione degli agenti Sysdig in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5e454-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="5e454-118">Per monitorare i contenitori, Sysdig esegue un processo in ogni computer usando un oggetto `DaemonSet` di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5e454-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="5e454-119">Gli oggetti DaemonSet sono oggetti API di Kubernetes che eseguono una singola istanza del contenitore per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e454-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="5e454-120">Sono ottimali per l'installazione di strumenti quale l'agente di monitoraggio di Sysdig.</span><span class="sxs-lookup"><span data-stu-id="5e454-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="5e454-121">Per installare gli oggetti DaemonSet di Sysdig, è necessario scaricare il [modello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) da sysdig.</span><span class="sxs-lookup"><span data-stu-id="5e454-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="5e454-122">Salvare il file come `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="5e454-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="5e454-123">In Linux e OS X è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="5e454-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="5e454-124">In PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5e454-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="5e454-125">Modificare quindi il file per inserire la chiave di accesso ottenuta dall'account Sysdig.</span><span class="sxs-lookup"><span data-stu-id="5e454-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="5e454-126">Al termine, creare l'oggetto DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="5e454-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="5e454-127">Visualizzare il monitoraggio</span><span class="sxs-lookup"><span data-stu-id="5e454-127">View your monitoring</span></span>
<span data-ttu-id="5e454-128">Dopo l'installazione e l'esecuzione, gli agenti dovrebbero restituire dati a Sysdig.</span><span class="sxs-lookup"><span data-stu-id="5e454-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="5e454-129">Tornare al [dashboard sysdig](https://app.sysdigcloud.com) per visualizzare le informazioni sui contenitori.</span><span class="sxs-lookup"><span data-stu-id="5e454-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="5e454-130">È anche possibile installare dashboard specifici di Kubernetes tramite la [creazione guidata di un nuovo dashboard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="5e454-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
