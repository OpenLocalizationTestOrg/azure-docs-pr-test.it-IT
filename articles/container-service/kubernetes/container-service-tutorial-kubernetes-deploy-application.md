---
title: esercitazione per il servizio contenitore aaaAzure - distribuire applicazioni | Documenti Microsoft
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
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="44b2f-104">Eseguire applicazioni in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44b2f-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="44b2f-105">In questa esercitazione, parte quattro di sette, verrà distribuita un'applicazione di esempio in un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="44b2f-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="44b2f-106">I passaggi completati comprendono:</span><span class="sxs-lookup"><span data-stu-id="44b2f-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44b2f-107">Scaricare i file manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44b2f-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="44b2f-108">Eseguire un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44b2f-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="44b2f-109">Testare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="44b2f-109">Test hello application</span></span>

<span data-ttu-id="44b2f-110">Nelle esercitazioni successive, questa applicazione viene ampliata, aggiornato, e Operations Management Suite sono configurati cluster di Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="44b2f-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="44b2f-111">In questa esercitazione si presuppone una conoscenza di base dei concetti Kubernetes, per informazioni dettagliate sul Kubernetes vedere hello [Kubernetes documentazione](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="44b2f-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="44b2f-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="44b2f-112">Before you begin</span></span>

<span data-ttu-id="44b2f-113">Nelle esercitazioni precedenti, un'applicazione è stata distribuita in un'immagine contenitore, questa immagine è stato caricato tooAzure contenitore del Registro di sistema e un cluster Kubernetes è stato creato.</span><span class="sxs-lookup"><span data-stu-id="44b2f-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="44b2f-114">Se si è già questi passaggi e si desidera toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="44b2f-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="44b2f-115">Il requisito minimo per questa esercitazione è un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="44b2f-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="44b2f-116">Ottenere il file manifesto</span><span class="sxs-lookup"><span data-stu-id="44b2f-116">Get manifest file</span></span>

<span data-ttu-id="44b2f-117">Per questa esercitazione, gli [oggetti Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) vengono distribuiti con un manifesto Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="44b2f-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="44b2f-118">Un manifesto Kubernetes è un file in formato YAML o JSON contenente le istruzioni sulla distribuzione e la configurazione degli oggetti.</span><span class="sxs-lookup"><span data-stu-id="44b2f-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="44b2f-119">file di manifesto dell'applicazione Hello per questa esercitazione è disponibile nel repository di applicazione di hello voto di Azure, è stato clonato in un'esercitazione precedente.</span><span class="sxs-lookup"><span data-stu-id="44b2f-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="44b2f-120">Se non è già stato fatto, è possibile clonare il repository di hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="44b2f-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="44b2f-121">file manifesto di Hello si trova nella seguente directory di repository clonato hello hello.</span><span class="sxs-lookup"><span data-stu-id="44b2f-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="44b2f-122">Aggiornare il file manifesto</span><span class="sxs-lookup"><span data-stu-id="44b2f-122">Update manifest file</span></span>

<span data-ttu-id="44b2f-123">Se si usa le immagini contenitore di Azure del Registro di sistema contenitore toostore hello, hello toobe esigenze manifesto aggiornato con hello ACR loginServer nome.</span><span class="sxs-lookup"><span data-stu-id="44b2f-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="44b2f-124">Ottenere il nome del server accesso ACR hello con hello [elenco acr az](/cli/azure/acr#list) comando.</span><span class="sxs-lookup"><span data-stu-id="44b2f-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="44b2f-125">Hello esempio manifesto è stato creato in precedenza con un nome di repository di *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="44b2f-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="44b2f-126">Aprire il file hello con qualsiasi editor di testo e sostituire hello *microsoft* valore con il nome di server hello account di accesso dell'istanza del record.</span><span class="sxs-lookup"><span data-stu-id="44b2f-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="44b2f-127">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="44b2f-127">Deploy application</span></span>

<span data-ttu-id="44b2f-128">Hello utilizzare [kubectl creare](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) comando applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="44b2f-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="44b2f-129">Questo comando analizza hello file manifesto e creare oggetti Kubernetes hello definito.</span><span class="sxs-lookup"><span data-stu-id="44b2f-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="44b2f-130">Output:</span><span class="sxs-lookup"><span data-stu-id="44b2f-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="44b2f-131">Testare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="44b2f-131">Test application</span></span>

<span data-ttu-id="44b2f-132">Oggetto [Kubernetes servizio](https://kubernetes.io/docs/concepts/services-networking/service/) viene creato che espone toohello applicazione hello internet.</span><span class="sxs-lookup"><span data-stu-id="44b2f-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="44b2f-133">Il processo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="44b2f-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="44b2f-134">lo stato di avanzamento toomonitor, utilizzare hello [kubectl ottenere servizio](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) con hello `--watch` argomento.</span><span class="sxs-lookup"><span data-stu-id="44b2f-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="44b2f-135">Inizialmente, hello **esterno IP** per hello *azure voto-anteriore* servizio viene visualizzato come *in sospeso*.</span><span class="sxs-lookup"><span data-stu-id="44b2f-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="44b2f-136">Una volta che l'indirizzo IP esterno hello è stato modificato da *in sospeso* tooan *indirizzo IP*, utilizzare `CTRL-C` processo di controllo kubectl toostop hello.</span><span class="sxs-lookup"><span data-stu-id="44b2f-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="44b2f-137">applicazione hello toosee, Sfoglia toohello l'indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="44b2f-137">toosee hello application, browse toohello external IP address.</span></span>

![Immagine del cluster Kubernetes in Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="44b2f-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="44b2f-139">Next steps</span></span>

<span data-ttu-id="44b2f-140">In questa esercitazione, hello applicazione voto Azure è stato distribuito tooan Kubernetes servizio contenitore di Azure cluster.</span><span class="sxs-lookup"><span data-stu-id="44b2f-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="44b2f-141">Le attività completate comprendono:</span><span class="sxs-lookup"><span data-stu-id="44b2f-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="44b2f-142">Scaricare i file manifesto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44b2f-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="44b2f-143">Eseguire un'applicazione hello in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44b2f-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="44b2f-144">Applicazione hello testata</span><span class="sxs-lookup"><span data-stu-id="44b2f-144">Tested hello application</span></span>

<span data-ttu-id="44b2f-145">Spostare toohello toolearn esercitazione successiva sulla scalabilità di un applicazione Kubernetes e hello Kubernetes infrastruttura sottostante.</span><span class="sxs-lookup"><span data-stu-id="44b2f-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="44b2f-146">Scalare l'applicazione e l'infrastruttura Kubernetes</span><span class="sxs-lookup"><span data-stu-id="44b2f-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)