---
title: Monitorare un cluster Azure Kubernetes con Datadog | Microsoft Docs
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
ms.openlocfilehash: 40b34457447a8f80d8cdf77579750e0c42df22d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="7cd33-103">Monitorare un cluster del servizio contenitore di Azure con Datadog</span><span class="sxs-lookup"><span data-stu-id="7cd33-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7cd33-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7cd33-104">Prerequisites</span></span>
<span data-ttu-id="7cd33-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="7cd33-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="7cd33-106">Si presume anche che gli strumenti dell'interfaccia della riga di comando di Azure `az` e `kubectl` siano installati.</span><span class="sxs-lookup"><span data-stu-id="7cd33-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="7cd33-107">È possibile verificare se lo strumento `az` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="7cd33-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="7cd33-108">Se lo strumento `az` non è installato, le istruzioni sono disponibili [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="7cd33-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="7cd33-109">È possibile verificare se lo strumento `kubectl` è installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="7cd33-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="7cd33-110">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="7cd33-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="7cd33-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="7cd33-111">DataDog</span></span>
<span data-ttu-id="7cd33-112">Datadog è un servizio che raccoglie dati di monitoraggio dai contenitori all'interno del cluster del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd33-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="7cd33-113">Datadog è dotato di un dashboard di integrazione Docker in cui è possibile visualizzare metriche specifiche all'interno dei propri contenitori.</span><span class="sxs-lookup"><span data-stu-id="7cd33-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="7cd33-114">Le metriche raccolte dai contenitori sono organizzate per CPU, memoria, rete e I/O.</span><span class="sxs-lookup"><span data-stu-id="7cd33-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="7cd33-115">Datadog suddivide le metriche in contenitori e immagini.</span><span class="sxs-lookup"><span data-stu-id="7cd33-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="7cd33-116">Prima è necessario [creare un account](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="7cd33-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="7cd33-117">Installazione dell'agente Datadog con DaemonSet</span><span class="sxs-lookup"><span data-stu-id="7cd33-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="7cd33-118">Gli elementi DaemonSet vengono usati da Kubernetes per eseguire una singola istanza di un contenitore in ogni host del cluster.</span><span class="sxs-lookup"><span data-stu-id="7cd33-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="7cd33-119">Sono ideali per l'esecuzione di agenti di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="7cd33-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="7cd33-120">Dopo l'accesso a Datadog, è possibile seguire le [istruzioni di Datadog](https://app.datadoghq.com/account/settings#agent/kubernetes) per installare gli agenti Datadog nel cluster usando DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="7cd33-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7cd33-121">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="7cd33-121">Conclusion</span></span>
<span data-ttu-id="7cd33-122">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="7cd33-122">That's it!</span></span> <span data-ttu-id="7cd33-123">Con gli agenti operativi, i dati verranno visualizzati nella console entro alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="7cd33-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="7cd33-124">È possibile visitare il [dashboard di Kubernetes](https://app.datadoghq.com/screen/integration/kubernetes) integrato per visualizzare un riepilogo del cluster.</span><span class="sxs-lookup"><span data-stu-id="7cd33-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
