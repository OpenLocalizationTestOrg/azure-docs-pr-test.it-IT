---
title: aaaMonitor Kubernetes Azure cluster con Datadog | Documenti Microsoft
description: Monitoraggio di un cluster Kubernetes nel servizio contenitore di Azure con Datadog
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="51a89-103">Monitorare un cluster del servizio contenitore di Azure con Datadog</span><span class="sxs-lookup"><span data-stu-id="51a89-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51a89-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="51a89-104">Prerequisites</span></span>
<span data-ttu-id="51a89-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="51a89-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="51a89-106">Inoltre, presuppone di aver hello `az` cli di Azure e `kubectl` installati gli strumenti.</span><span class="sxs-lookup"><span data-stu-id="51a89-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="51a89-107">È possibile verificare se si dispone di hello `az` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="51a89-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="51a89-108">Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="51a89-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="51a89-109">È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="51a89-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="51a89-110">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="51a89-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="51a89-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="51a89-111">DataDog</span></span>
<span data-ttu-id="51a89-112">Datadog è un servizio che raccoglie dati di monitoraggio dai contenitori all'interno del cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="51a89-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="51a89-113">Datadog è dotato di un dashboard di integrazione Docker in cui è possibile visualizzare metriche specifiche all'interno dei propri contenitori.</span><span class="sxs-lookup"><span data-stu-id="51a89-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="51a89-114">Le metriche raccolte dai contenitori sono organizzate per CPU, memoria, rete e I/O.</span><span class="sxs-lookup"><span data-stu-id="51a89-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="51a89-115">Datadog suddivide le metriche in contenitori e immagini.</span><span class="sxs-lookup"><span data-stu-id="51a89-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="51a89-116">È innanzitutto necessario troppo[creare un account](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="51a89-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="51a89-117">L'installazione di hello Datadog agente con un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="51a89-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="51a89-118">DaemonSets vengono utilizzati da Kubernetes toorun una singola istanza di un contenitore in ogni host in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="51a89-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="51a89-119">Sono ideali per l'esecuzione di agenti di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="51a89-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="51a89-120">Dopo aver eseguito l'accesso in Datadog, è possibile seguire hello [Datadog istruzioni](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agenti nel cluster utilizzando un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="51a89-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="51a89-121">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="51a89-121">Conclusion</span></span>
<span data-ttu-id="51a89-122">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="51a89-122">That's it!</span></span> <span data-ttu-id="51a89-123">Una volta agenti hello siano attivi e in esecuzione è verranno visualizzati i dati nella console di hello in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="51a89-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="51a89-124">È possibile visitare hello integrato [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee un riepilogo del cluster.</span><span class="sxs-lookup"><span data-stu-id="51a89-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
