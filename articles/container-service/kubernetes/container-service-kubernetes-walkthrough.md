---
title: Guida introduttiva - Cluster Kubernetes Azure per Linux | Microsoft Docs
description: Informazioni per creare in modo rapido un cluster Kubernetes per contenitori Linux nel servizio contenitore di Azure con l'interfaccia della riga di comando di Azure.
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 5a2131659903e79b28f4d1b795d25a31d8d4ce8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="08c30-103">Distribuire cluster Kubernetes per contenitori Linux</span><span class="sxs-lookup"><span data-stu-id="08c30-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="08c30-104">In questa guida introduttiva viene distribuito un cluster Kubernetes usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="08c30-104">In this quick start, a Kubernetes cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="08c30-105">Un'applicazione multicontenitore costituita dal front-end Web e da un'istanza di Redis viene quindi distribuita ed eseguita nel cluster.</span><span class="sxs-lookup"><span data-stu-id="08c30-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="08c30-106">Al termine, l'applicazione è accessibile tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="08c30-106">Once completed, the application is accessible over the internet.</span></span> 

<span data-ttu-id="08c30-107">L'applicazione di esempio usata in questo documento è scritta in Python.</span><span class="sxs-lookup"><span data-stu-id="08c30-107">The example application used in this document is written in Python.</span></span> <span data-ttu-id="08c30-108">I concetti e i passaggi descritti possono essere usati per distribuire un'immagine del contenitore in un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="08c30-108">The concepts and steps detailed here can be used to deploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="08c30-109">Il codice, Dockerfile, e il file manifesto di Kubernetes creato in precedenza per questo progetto sono disponibili in [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="08c30-109">The code, Dockerfile, and pre-created Kubernetes manifest files related to this project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Immagine del passaggio ad Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="08c30-111">Questa guida introduttiva presuppone una conoscenza di base dei concetti relativi a Kubernetes. Per informazioni dettagliate su Kubernetes, vedere la [documentazione di Kubernetes]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="08c30-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="08c30-112">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="08c30-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="08c30-113">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="08c30-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="08c30-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="08c30-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="08c30-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="08c30-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="08c30-116">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="08c30-116">Create a resource group</span></span>

<span data-ttu-id="08c30-117">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="08c30-117">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="08c30-118">Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="08c30-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="08c30-119">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="08c30-119">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="08c30-120">Output:</span><span class="sxs-lookup"><span data-stu-id="08c30-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="08c30-121">Creare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="08c30-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="08c30-122">Creare un cluster Kubernetes nel servizio contenitore di Azure con il comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="08c30-122">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="08c30-123">L'esempio seguente crea un cluster denominato *myK8sCluster* con un nodo master Linux e tre nodi agente Linux.</span><span class="sxs-lookup"><span data-stu-id="08c30-123">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="08c30-124">Dopo alcuni minuti, il comando viene completato e restituisce le informazioni in formato json sul cluster.</span><span class="sxs-lookup"><span data-stu-id="08c30-124">After several minutes, the command completes and returns json formatted information about the cluster.</span></span> 

## <a name="connect-to-the-cluster"></a><span data-ttu-id="08c30-125">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="08c30-125">Connect to the cluster</span></span>

<span data-ttu-id="08c30-126">Per gestire un cluster Kubernetes, usare [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), il client da riga di comando di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="08c30-126">To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="08c30-127">Se si usa Azure CloudShell, kubectl è già installato.</span><span class="sxs-lookup"><span data-stu-id="08c30-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="08c30-128">Se lo si vuole installare in locale, è possibile usare il comando [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="08c30-128">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="08c30-129">Per configurare kubectl per connettersi al cluster Kubernetes, eseguire il comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="08c30-129">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="08c30-130">Con questo passaggio si scaricano le credenziali e si configura l'interfaccia della riga di comando di Kubernetes per il loro uso.</span><span class="sxs-lookup"><span data-stu-id="08c30-130">This step downloads credentials and configures the Kubernetes CLI to use them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="08c30-131">Per verificare la connessione al cluster, usare il comando [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) per restituire un elenco dei nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="08c30-131">To verify the connection to your cluster, use the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command to return a list of the cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="08c30-132">Output:</span><span class="sxs-lookup"><span data-stu-id="08c30-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-the-application"></a><span data-ttu-id="08c30-133">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="08c30-133">Run the application</span></span>

<span data-ttu-id="08c30-134">Un file manifesto di Kubernetes definisce uno stato desiderato per il cluster, incluse le immagini del contenitore da eseguire.</span><span class="sxs-lookup"><span data-stu-id="08c30-134">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span></span> <span data-ttu-id="08c30-135">Per questo esempio, viene usato un manifesto per creare tutti gli oggetti necessari per eseguire l'applicazione Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="08c30-135">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span></span> 

<span data-ttu-id="08c30-136">Creare un file denominato `azure-vote.yml` e copiarvi il codice YAML seguente.</span><span class="sxs-lookup"><span data-stu-id="08c30-136">Create a file named `azure-vote.yml` and copy into it the following YAML.</span></span> <span data-ttu-id="08c30-137">Se si usa Azure Cloud Shell, questo file può essere creato usando vi o Nano come se si usasse un sistema virtuale o fisico.</span><span class="sxs-lookup"><span data-stu-id="08c30-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="08c30-138">Usare il comando [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="08c30-138">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="08c30-139">Output:</span><span class="sxs-lookup"><span data-stu-id="08c30-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="08c30-140">Test dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="08c30-140">Test the application</span></span>

<span data-ttu-id="08c30-141">Mentre l'applicazione viene eseguita, viene creato un [servizio di Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) che espone il front-end dell'applicazione a Internet.</span><span class="sxs-lookup"><span data-stu-id="08c30-141">As the application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes the application front end to the internet.</span></span> <span data-ttu-id="08c30-142">Il processo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="08c30-142">This process can take a few minutes to complete.</span></span> 

<span data-ttu-id="08c30-143">Per monitorare lo stato, usare il comando [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) con l'argomento `--watch`.</span><span class="sxs-lookup"><span data-stu-id="08c30-143">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="08c30-144">**EXTERNAL-IP** per il servizio *azure-vote-front* inizialmente viene visualizzato come *pending*.</span><span class="sxs-lookup"><span data-stu-id="08c30-144">Initially the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="08c30-145">Dopo che l'indirizzo EXTERNAL-IP passa da *pending* a un *indirizzo IP*, usare `CTRL-C` per arrestare il processo kubectl watch.</span><span class="sxs-lookup"><span data-stu-id="08c30-145">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="08c30-146">È ora possibile passare all'indirizzo IP esterno per visualizzare l'app Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="08c30-146">You can now browse to the external IP address to see the Azure Vote App.</span></span>

![Immagine del passaggio ad Azure Vote](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="08c30-148">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="08c30-148">Delete cluster</span></span>
<span data-ttu-id="08c30-149">Quando il cluster non è più necessario, è possibile usare il comando [az group delete](/cli/azure/group#delete) per rimuovere il gruppo di risorse, il servizio contenitore e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="08c30-149">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="08c30-150">Ottenere il codice</span><span class="sxs-lookup"><span data-stu-id="08c30-150">Get the code</span></span>

<span data-ttu-id="08c30-151">In questa guida introduttiva sono state usate immagini del contenitore già creato per creare una distribuzione di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="08c30-151">In this quick start, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="08c30-152">Il codice dell'applicazione correlato, Dockerfile, e il file manifesto di Kubernetes sono disponibili su GitHub.</span><span class="sxs-lookup"><span data-stu-id="08c30-152">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="08c30-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="08c30-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="08c30-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08c30-154">Next steps</span></span>

<span data-ttu-id="08c30-155">In questa guida introduttiva è stato distribuito un cluster Kubernetes in cui è stata quindi distribuita un'applicazione multicontenitore.</span><span class="sxs-lookup"><span data-stu-id="08c30-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span> 

<span data-ttu-id="08c30-156">Per altre informazioni sul servizio contenitore di Azure e l'analisi di un codice completo per la distribuzione dell'esempio, passare all'esercitazione sul cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="08c30-156">To learn more about Azure Container Service, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="08c30-157">Gestire un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="08c30-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
