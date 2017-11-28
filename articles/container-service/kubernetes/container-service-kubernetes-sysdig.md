---
title: cluster di Azure Kubernetes aaaMonitor - Sysdig | Documenti Microsoft
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="acf24-103">Monitorare un cluster Kubernetes del servizio contenitore di Azure con Sysdig</span><span class="sxs-lookup"><span data-stu-id="acf24-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acf24-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="acf24-104">Prerequisites</span></span>
<span data-ttu-id="acf24-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="acf24-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="acf24-106">Inoltre, si presuppone di aver hello azure cli e kubectl installati gli strumenti.</span><span class="sxs-lookup"><span data-stu-id="acf24-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="acf24-107">È possibile verificare se si dispone di hello `az` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="acf24-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="acf24-108">Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="acf24-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="acf24-109">È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="acf24-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="acf24-110">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="acf24-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="acf24-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="acf24-111">Sysdig</span></span>
<span data-ttu-id="acf24-112">Sysdig è una società che offre uno strumento di monitoraggio esterno come servizio, che consente di monitorare i contenuti nel cluster Kubernetes in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="acf24-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="acf24-113">L'uso di Sysdig richiede un account Sysdig attivo.</span><span class="sxs-lookup"><span data-stu-id="acf24-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="acf24-114">È possibile iscriversi per creare un account nel rispettivo [sito](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="acf24-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="acf24-115">Dopo aver eseguito il nel sito Web di toohello Sysdig cloud, fare clic sul nome utente e nella pagina di hello si dovrebbe visualizzare la "chiave di accesso".</span><span class="sxs-lookup"><span data-stu-id="acf24-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Chiave API di Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="acf24-117">L'installazione di hello Sysdig agenti tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="acf24-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="acf24-118">i contenitori, Sysdig viene eseguito un processo in ogni computer utilizzando un Kubernetes toomonitor `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="acf24-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="acf24-119">Gli oggetti DaemonSet sono oggetti API di Kubernetes che eseguono una singola istanza del contenitore per ogni macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="acf24-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="acf24-120">Sono ideali per l'installazione di strumenti quali l'agente di monitoraggio del Sysdig hello.</span><span class="sxs-lookup"><span data-stu-id="acf24-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="acf24-121">tooinstall hello Sysdig daemonset, è necessario innanzitutto scaricare [modello hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) da sysdig.</span><span class="sxs-lookup"><span data-stu-id="acf24-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="acf24-122">Salvare il file come `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="acf24-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="acf24-123">In Linux e OS X è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="acf24-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="acf24-124">In PowerShell:</span><span class="sxs-lookup"><span data-stu-id="acf24-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="acf24-125">Modificare quindi tooinsert tale file la chiave di accesso, che è stato ottenuto da account Sysdig.</span><span class="sxs-lookup"><span data-stu-id="acf24-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="acf24-126">Creare infine hello DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="acf24-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="acf24-127">Visualizzare il monitoraggio</span><span class="sxs-lookup"><span data-stu-id="acf24-127">View your monitoring</span></span>
<span data-ttu-id="acf24-128">Una volta installato e in esecuzione, gli agenti di hello devono pump tooSysdig indietro di dati.</span><span class="sxs-lookup"><span data-stu-id="acf24-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="acf24-129">Tornare indietro toothe [sysdig dashboard](https://app.sysdigcloud.com) dovrebbe essere possibile visualizzare informazioni ai contenitori.</span><span class="sxs-lookup"><span data-stu-id="acf24-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="acf24-130">È anche possibile installare dashboard specifici di Kubernetes tramite la [creazione guidata di un nuovo dashboard](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="acf24-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
