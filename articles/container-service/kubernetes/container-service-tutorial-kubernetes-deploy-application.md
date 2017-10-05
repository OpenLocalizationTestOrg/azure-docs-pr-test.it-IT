---
title: Esercitazione sul servizio contenitore di Azure - Distribuire un'applicazione | Microsoft Docs
description: Esercitazione sul servizio contenitore di Azure - Distribuire un'applicazione
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="8cb40-104">Eseguire applicazioni in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8cb40-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="8cb40-105">In questa esercitazione, parte quattro di sette, verrà distribuita un'applicazione di esempio in un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8cb40-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="8cb40-106">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="8cb40-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8cb40-107">Scaricare i file manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8cb40-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="8cb40-108">Eseguire un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8cb40-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="8cb40-109">Test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="8cb40-109">Test the application</span></span>

<span data-ttu-id="8cb40-110">Nelle esercitazioni successive, l'applicazione viene aggiornata e ne vengono aumentate le istanze e Operations Management Suite viene configurato per monitorare il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8cb40-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="8cb40-111">Questa esercitazione presuppone una conoscenza di base dei concetti relativi a Kubernetes. Per informazioni dettagliate su Kubernetes, vedere la [documentazione di Kubernetes](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="8cb40-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8cb40-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8cb40-112">Before you begin</span></span>

<span data-ttu-id="8cb40-113">Nelle esercitazioni precedenti è stato creato un pacchetto di un'applicazione in un'immagine del contenitore, caricata poi nel Registro contenitori di Azure, ed è stato creato un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8cb40-113">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="8cb40-114">Se questi passaggi non sono stati ancora eseguiti e si vuole procedere, tornare a [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md) (Esercitazione 1: Creare immagini del contenitore).</span><span class="sxs-lookup"><span data-stu-id="8cb40-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="8cb40-115">Il requisito minimo per questa esercitazione è un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8cb40-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="8cb40-116">Ottenere il file manifesto</span><span class="sxs-lookup"><span data-stu-id="8cb40-116">Get manifest file</span></span>

<span data-ttu-id="8cb40-117">Per questa esercitazione, gli [oggetti Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) vengono distribuiti con un manifesto Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8cb40-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="8cb40-118">Un manifesto Kubernetes è un file in formato YAML o JSON contenente le istruzioni sulla distribuzione e la configurazione degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="8cb40-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="8cb40-119">Il file manifesto dell'applicazione per questa esercitazione è disponibile nell'archivio dell'applicazione Azure Vote, che è stato clonato in un'esercitazione precedente.</span><span class="sxs-lookup"><span data-stu-id="8cb40-119">The application manifest file for this tutorial is available in the Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="8cb40-120">Se questa operazione non è già stata eseguita, clonare l'archivio con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8cb40-120">If you have not already done so, clone the repo with the following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="8cb40-121">Il file manifesto si trova nella directory seguente dell'archivio clonato.</span><span class="sxs-lookup"><span data-stu-id="8cb40-121">The manifest file is found in the following directory of the cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="8cb40-122">Aggiornare il file manifesto</span><span class="sxs-lookup"><span data-stu-id="8cb40-122">Update manifest file</span></span>

<span data-ttu-id="8cb40-123">Se si usa Registro contenitori di Azure per archiviare le immagini del contenitore, è necessario aggiornare il manifesto con il nome del server di accesso di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cb40-123">If using Azure Container Registry to store the container images, the manifest needs to be updated with the ACR loginServer name.</span></span>

<span data-ttu-id="8cb40-124">Ottenere il nome del server di accesso del Registro contenitori di Azure con il comando [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="8cb40-124">Get the ACR login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="8cb40-125">Il manifesto di esempio è stato creato in precedenza con il nome di repository *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="8cb40-125">The sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="8cb40-126">Aprire il file con qualsiasi editor di testo e sostituire il valore *microsoft* con il nome del server di accesso dell'istanza di Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cb40-126">Open the file with any text editor, and replace the *microsoft* value with the login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="8cb40-127">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="8cb40-127">Deploy application</span></span>

<span data-ttu-id="8cb40-128">Usare il comando [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8cb40-128">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span> <span data-ttu-id="8cb40-129">Questo comando analizza il file manifesto e creare gli oggetti Kubernetes definiti.</span><span class="sxs-lookup"><span data-stu-id="8cb40-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="8cb40-130">Output:</span><span class="sxs-lookup"><span data-stu-id="8cb40-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="8cb40-131">Testare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8cb40-131">Test application</span></span>

<span data-ttu-id="8cb40-132">Viene creato un [servizio di Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) che espone l'applicazione a Internet.</span><span class="sxs-lookup"><span data-stu-id="8cb40-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="8cb40-133">Il processo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="8cb40-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="8cb40-134">Per monitorare lo stato, usare il comando [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) con l'argomento `--watch`.</span><span class="sxs-lookup"><span data-stu-id="8cb40-134">To monitor progress, use the [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="8cb40-135">**EXTERNAL-IP** per il servizio *azure-vote-front* inizialmente viene visualizzato come *pending*.</span><span class="sxs-lookup"><span data-stu-id="8cb40-135">Initially, the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="8cb40-136">Dopo che l'indirizzo EXTERNAL-IP passa da *pending* a un *indirizzo IP*, usare `CTRL-C` per arrestare il processo kubectl watch.</span><span class="sxs-lookup"><span data-stu-id="8cb40-136">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="8cb40-137">Per vedere l'applicazione, passare all'indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="8cb40-137">To see the application, browse to the external IP address.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="8cb40-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8cb40-139">Next steps</span></span>

<span data-ttu-id="8cb40-140">In questa esercitazione è stata distribuita un'applicazione Azure Vote in un cluster Kubernetes del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="8cb40-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="8cb40-141">Le attività completate comprendono:</span><span class="sxs-lookup"><span data-stu-id="8cb40-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="8cb40-142">Scaricare i file manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8cb40-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="8cb40-143">Eseguire l'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8cb40-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="8cb40-144">Testare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="8cb40-144">Tested the application</span></span>

<span data-ttu-id="8cb40-145">Passare all'esercitazione successiva per informazioni sulla scalabilità sia di un'applicazione Kubernetes sia dell'infrastruttura Kubernetes sottostante.</span><span class="sxs-lookup"><span data-stu-id="8cb40-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cb40-146">Scalare l'applicazione e l'infrastruttura Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8cb40-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)