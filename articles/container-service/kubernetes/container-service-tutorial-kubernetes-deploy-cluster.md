---
title: esercitazione per il servizio contenitore aaaAzure - distribuire Cluster | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Distribuire un cluster
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="1382f-104">Distribuire un cluster Kubernetes nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="1382f-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="1382f-105">Kubernetes fornisce una piattaforma distribuita per applicazioni in contenitori.</span><span class="sxs-lookup"><span data-stu-id="1382f-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="1382f-106">Con il servizio contenitore di Azure, il provisioning di un cluster Kubernetes pronto per la produzione è semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="1382f-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="1382f-107">In questa esercitazione, parte 3 di 7, viene distribuito un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="1382f-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="1382f-108">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="1382f-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1382f-109">Distribuzione di un cluster del servizio contenitore di Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1382f-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="1382f-110">Installazione di hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="1382f-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="1382f-111">Configurazione di kubectl</span><span class="sxs-lookup"><span data-stu-id="1382f-111">Configuration of kubectl</span></span>

<span data-ttu-id="1382f-112">Nelle esercitazioni successive, hello Azure voto applicazione viene distribuita cluster toohello, scalato, aggiornate e Operations Management Suite è cluster Kubernetes di hello toomonitor configurato.</span><span class="sxs-lookup"><span data-stu-id="1382f-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1382f-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="1382f-113">Before you begin</span></span>

<span data-ttu-id="1382f-114">Nelle esercitazioni precedenti, un'immagine contenitore è stata creata e caricato l'istanza del Registro di sistema di Azure contenitore tooan.</span><span class="sxs-lookup"><span data-stu-id="1382f-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="1382f-115">Se si è già questi passaggi e si desidera toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="1382f-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="1382f-116">Creare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1382f-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="1382f-117">In hello [esercitazione precedente](./container-service-tutorial-kubernetes-prepare-acr.md), un gruppo di risorse denominato *myResourceGroup* è stato creato.</span><span class="sxs-lookup"><span data-stu-id="1382f-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="1382f-118">Se questa operazione non è stata ancora eseguita, creare ora il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1382f-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="1382f-119">Creare un cluster di Kubernetes nel servizio contenitore di Azure con hello [az acs creare](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1382f-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="1382f-120">esempio Hello crea un cluster denominato *myK8sCluster* con uno Linux master nodo e i tre nodi di agente di Linux.</span><span class="sxs-lookup"><span data-stu-id="1382f-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="1382f-121">Dopo alcuni minuti, completamento del comando hello e restituisce json formattato informazioni sulla distribuzione di hello ACS.</span><span class="sxs-lookup"><span data-stu-id="1382f-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="1382f-122">Installare hello kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="1382f-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="1382f-123">tooconnect toohello Kubernetes cluster da computer client, utilizzare [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client di hello Kubernetes della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1382f-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="1382f-124">Se si usa Azure CloudShell, `kubectl` è già installato.</span><span class="sxs-lookup"><span data-stu-id="1382f-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="1382f-125">Se si desidera tooinstall utilizzi localmente, hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="1382f-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="1382f-126">Se in esecuzione Linux o Mac OS, potrebbe essere toorun con sudo.</span><span class="sxs-lookup"><span data-stu-id="1382f-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="1382f-127">In Windows accertarsi che la shell sia stata eseguita come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1382f-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="1382f-128">In Windows, è l'installazione predefinita di hello *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="1382f-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="1382f-129">Potrebbe essere necessario tooadd questo percorso di file toohello Windows.</span><span class="sxs-lookup"><span data-stu-id="1382f-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="1382f-130">Connettersi con kubectl</span><span class="sxs-lookup"><span data-stu-id="1382f-130">Connect with kubectl</span></span>

<span data-ttu-id="1382f-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, eseguire hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="1382f-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="1382f-132">tooverify hello connessione tooyour cluster esegue hello [kubectl ottenere nodi](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="1382f-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="1382f-133">Output:</span><span class="sxs-lookup"><span data-stu-id="1382f-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="1382f-134">Al termine dell'esercitazione, sarà disponibile un cluster Kubernetes del servizio contenitore di Azure pronto per i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1382f-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="1382f-135">Nelle esercitazioni successive, un'applicazione multi-contenitore è distribuito toothis cluster, la scalabilità, aggiornate e monitorati.</span><span class="sxs-lookup"><span data-stu-id="1382f-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1382f-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1382f-136">Next steps</span></span>

<span data-ttu-id="1382f-137">In questa esercitazione è stato distribuito un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="1382f-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="1382f-138">sono stata completata Hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1382f-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1382f-139">Distribuzione di un cluster Kubernets del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="1382f-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="1382f-140">Hello installato Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="1382f-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="1382f-141">Configurazione di kubectl</span><span class="sxs-lookup"><span data-stu-id="1382f-141">Configured kubectl</span></span>

<span data-ttu-id="1382f-142">Spostare toohello Avanti toolearn esercitazione sull'esecuzione dell'applicazione in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1382f-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1382f-143">Distribuire un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="1382f-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
