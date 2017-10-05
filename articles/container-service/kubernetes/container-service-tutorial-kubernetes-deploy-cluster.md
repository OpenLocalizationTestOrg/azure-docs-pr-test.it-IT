---
title: Esercitazione sul servizio contenitore di Azure - Distribuire un cluster | Microsoft Docs
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
ms.openlocfilehash: 472697c1f0c18859087d7b448e1786d85c27aca0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="6b8d8-104">Distribuire un cluster Kubernetes nel servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6b8d8-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="6b8d8-105">Kubernetes fornisce una piattaforma distribuita per applicazioni in contenitori.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="6b8d8-106">Con il servizio contenitore di Azure, il provisioning di un cluster Kubernetes pronto per la produzione è semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="6b8d8-107">In questa esercitazione, parte 3 di 7, viene distribuito un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="6b8d8-108">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="6b8d8-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b8d8-109">Distribuzione di un cluster del servizio contenitore di Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6b8d8-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="6b8d8-110">Installazione dell'interfaccia della riga di comando Kubernetes (kubectl)</span><span class="sxs-lookup"><span data-stu-id="6b8d8-110">Installation of the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="6b8d8-111">Configurazione di kubectl</span><span class="sxs-lookup"><span data-stu-id="6b8d8-111">Configuration of kubectl</span></span>

<span data-ttu-id="6b8d8-112">Nelle esercitazioni successive, l'applicazione Azure Vote viene distribuita nel cluster, ridimensionata, aggiornata e Operations Management Suite viene configurato per monitorare il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-112">In subsequent tutorials, the Azure Vote application is deployed to the cluster, scaled, updated, and Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6b8d8-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="6b8d8-113">Before you begin</span></span>

<span data-ttu-id="6b8d8-114">Nelle esercitazioni precedenti, un'immagine del contenitore è stata creata e caricata in un'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-114">In previous tutorials, a container image was created and uploaded to an Azure Container Registry instance.</span></span> <span data-ttu-id="6b8d8-115">Se questi passaggi non sono stati ancora eseguiti e si vuole procedere, tornare a [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md) (Esercitazione 1: Creare immagini del contenitore).</span><span class="sxs-lookup"><span data-stu-id="6b8d8-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="6b8d8-116">Creare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6b8d8-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="6b8d8-117">Nell'[esercitazione precedente](./container-service-tutorial-kubernetes-prepare-acr.md) è stato creato un gruppo di risorse denominato *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-117">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="6b8d8-118">Se questa operazione non è stata ancora eseguita, creare ora il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="6b8d8-119">Creare un cluster Kubernetes nel servizio contenitore di Azure con il comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="6b8d8-119">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="6b8d8-120">L'esempio seguente crea un cluster denominato *myK8sCluster* con un nodo master Linux e tre nodi agente Linux.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-120">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="6b8d8-121">Dopo alcuni minuti, il comando viene completato e restituisce le informazioni in formato JSON sulla distribuzione del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-121">After several minutes, the command completes, and returns json formatted information about the ACS deployment.</span></span>

## <a name="install-the-kubectl-cli"></a><span data-ttu-id="6b8d8-122">Installare l'interfaccia della riga di comando di kubectl</span><span class="sxs-lookup"><span data-stu-id="6b8d8-122">Install the kubectl CLI</span></span>

<span data-ttu-id="6b8d8-123">Per connettersi al cluster Kubernetes dal computer client, usare [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), il client da riga di comando di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-123">To connect to the Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="6b8d8-124">Se si usa Azure CloudShell, `kubectl` è già installato.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="6b8d8-125">Se lo si vuole installare in locale, usare il comando [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="6b8d8-125">If you want to install it locally, use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="6b8d8-126">Se è in esecuzione in Linux o MacOS, potrebbe essere necessario procedere all'esecuzione con sudo.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-126">If running in Linux or macOS, you may need to run with sudo.</span></span> <span data-ttu-id="6b8d8-127">In Windows accertarsi che la shell sia stata eseguita come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="6b8d8-128">In Windows l'installazione predefinita è *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-128">On Windows, the default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="6b8d8-129">Potrebbe essere necessario aggiungere questo file al percorso di Windows.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-129">You may need to add this file to the Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="6b8d8-130">Connettersi con kubectl</span><span class="sxs-lookup"><span data-stu-id="6b8d8-130">Connect with kubectl</span></span>

<span data-ttu-id="6b8d8-131">Per configurare `kubectl` per connettersi al cluster Kubernetes, eseguire il comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="6b8d8-131">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="6b8d8-132">Per verificare la connessione al cluster, eseguire il comando [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="6b8d8-132">To verify the connection to your cluster, run the [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="6b8d8-133">Output:</span><span class="sxs-lookup"><span data-stu-id="6b8d8-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="6b8d8-134">Al termine dell'esercitazione, sarà disponibile un cluster Kubernetes del servizio contenitore di Azure pronto per i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="6b8d8-135">Nelle esercitazioni successive, in questo cluster viene distribuita un'applicazione multi-contenitore, quindi viene scalata orizzontalmente, aggiornata e monitorata.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-135">In subsequent tutorials, a multi-container application is deployed to this cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b8d8-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b8d8-136">Next steps</span></span>

<span data-ttu-id="6b8d8-137">In questa esercitazione è stato distribuito un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="6b8d8-138">Sono stati completati i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6b8d8-138">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b8d8-139">Distribuzione di un cluster Kubernets del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="6b8d8-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="6b8d8-140">Installazione dell'interfaccia della riga di comando di Kubernetes (kubectl)</span><span class="sxs-lookup"><span data-stu-id="6b8d8-140">Installed the Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="6b8d8-141">Configurazione di kubectl</span><span class="sxs-lookup"><span data-stu-id="6b8d8-141">Configured kubectl</span></span>

<span data-ttu-id="6b8d8-142">Passare all'esercitazione successiva per apprendere come eseguire l'applicazione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="6b8d8-142">Advance to the next tutorial to learn about running application on the cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b8d8-143">Distribuire un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6b8d8-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
