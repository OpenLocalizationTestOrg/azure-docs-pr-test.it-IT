---
title: Guida introduttiva - Cluster Kubernetes Azure per Windows | Microsoft Docs
description: Informazioni per creare in modo rapido un cluster Kubernetes per contenitori Windows nel servizio contenitore di Azure con l'interfaccia della riga di comando di Azure.
documentationcenter: 
author: dlepow
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
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: f9bf4c4094addfa9654e3b99d91add03079ee045
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="974c1-103">Distribuire cluster Kubernetes per contenitori Windows</span><span class="sxs-lookup"><span data-stu-id="974c1-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="974c1-104">L'interfaccia della riga di comando di Azure viene usata per creare e gestire le risorse di Azure dalla riga di comando o negli script.</span><span class="sxs-lookup"><span data-stu-id="974c1-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="974c1-105">Questa guida illustra in modo dettagliato come usare l'interfaccia della riga di comando di Azure per distribuire un cluster [Kubernetes](https://kubernetes.io/docs/home/) nel [servizio contenitore di Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="974c1-105">This guide details using the Azure CLI to deploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="974c1-106">Dopo aver distribuito il cluster, è possibile connettersi a esso con lo strumento da riga di comando `kubectl` di Kubernetes e distribuire il primo contenitore Windows.</span><span class="sxs-lookup"><span data-stu-id="974c1-106">Once the cluster is deployed, you connect to it with the Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="974c1-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="974c1-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="974c1-108">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="974c1-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="974c1-109">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="974c1-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="974c1-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="974c1-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="974c1-111">Il supporto per i contenitori Windows in Kubernetes nel servizio contenitore di Azure è disponibile in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="974c1-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="974c1-112">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="974c1-112">Create a resource group</span></span>

<span data-ttu-id="974c1-113">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="974c1-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="974c1-114">Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="974c1-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="974c1-115">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="974c1-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="974c1-116">Creare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="974c1-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="974c1-117">Creare un cluster Kubernetes nel servizio contenitore di Azure con il comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="974c1-117">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="974c1-118">L'esempio seguente crea un cluster denominato *myK8sCluster* con un nodo master Linux e due nodi agente Windows.</span><span class="sxs-lookup"><span data-stu-id="974c1-118">The following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="974c1-119">Questo esempio crea le chiavi SSH necessarie per la connessione al nodo master Linux.</span><span class="sxs-lookup"><span data-stu-id="974c1-119">This example creates SSH keys needed to connect to the Linux master.</span></span> <span data-ttu-id="974c1-120">L'esempio usa *azureuser* come nome utente amministrativo e *myPassword12* come password nei nodi Windows.</span><span class="sxs-lookup"><span data-stu-id="974c1-120">This example uses *azureuser* for an administrative user name and *myPassword12* as the password on the Windows nodes.</span></span> <span data-ttu-id="974c1-121">Aggiornare i valori in modo che siano appropriati all'ambiente.</span><span class="sxs-lookup"><span data-stu-id="974c1-121">Update these values to something appropriate to your environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="974c1-122">Dopo alcuni minuti, il comando viene completato e mostra le informazioni sulla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="974c1-122">After several minutes, the command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="974c1-123">Installare kubectl</span><span class="sxs-lookup"><span data-stu-id="974c1-123">Install kubectl</span></span>

<span data-ttu-id="974c1-124">Per connettersi al cluster Kubernetes dal computer client, usare [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), il client da riga di comando di Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="974c1-124">To connect to the Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="974c1-125">Se si usa Azure CloudShell, `kubectl` è già installato.</span><span class="sxs-lookup"><span data-stu-id="974c1-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="974c1-126">Se lo si vuole installare in locale, è possibile usare il comando [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli).</span><span class="sxs-lookup"><span data-stu-id="974c1-126">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="974c1-127">L'interfaccia della riga di comando di Azure seguente installa `kubectl` nel sistema.</span><span class="sxs-lookup"><span data-stu-id="974c1-127">The following Azure CLI example installs `kubectl` to your system.</span></span> <span data-ttu-id="974c1-128">In Windows eseguire questo comando come amministratore.</span><span class="sxs-lookup"><span data-stu-id="974c1-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="974c1-129">Connettersi con kubectl</span><span class="sxs-lookup"><span data-stu-id="974c1-129">Connect with kubectl</span></span>

<span data-ttu-id="974c1-130">Per configurare `kubectl` per connettersi al cluster Kubernetes, eseguire il comando [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="974c1-130">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="974c1-131">L'esempio seguente scarica la configurazione del cluster per il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="974c1-131">The following example downloads the cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="974c1-132">Per verificare la connessione al cluster dal computer, provare a eseguire:</span><span class="sxs-lookup"><span data-stu-id="974c1-132">To verify the connection to your cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="974c1-133">`kubectl` elenca i nodi master e agente.</span><span class="sxs-lookup"><span data-stu-id="974c1-133">`kubectl` lists the master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="974c1-134">Distribuire un contenitore IIS Windows</span><span class="sxs-lookup"><span data-stu-id="974c1-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="974c1-135">È possibile eseguire un contenitore Docker all'interno di un *pod* Kubernetes, che contiene uno o più contenitori.</span><span class="sxs-lookup"><span data-stu-id="974c1-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="974c1-136">Questo esempio di base usa un file JSON per specificare un contenitore Microsoft Internet Information Server (IIS) e quindi crea il pod usando il comando `kubctl apply`.</span><span class="sxs-lookup"><span data-stu-id="974c1-136">This basic example uses a JSON file to specify a Microsoft Internet Information Server (IIS) container, and then creates the pod using the `kubctl apply` command.</span></span> 

<span data-ttu-id="974c1-137">Creare un file locale denominato `iis.json` e copiare il testo seguente.</span><span class="sxs-lookup"><span data-stu-id="974c1-137">Create a local file named `iis.json` and copy the following text.</span></span> <span data-ttu-id="974c1-138">Questo file indica a Kubernetes di eseguire IIS su Windows Server 2016 Nano Server usando un'immagine di contenitore pubblica dall'[hub Docker](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="974c1-138">This file tells Kubernetes to run IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="974c1-139">Il contenitore usa la porta 80, ma inizialmente è accessibile solo all'interno della rete di cluster.</span><span class="sxs-lookup"><span data-stu-id="974c1-139">The container uses port 80, but initially is only accessible within the cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="974c1-140">Per avviare il pod, digitare:</span><span class="sxs-lookup"><span data-stu-id="974c1-140">To start the pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="974c1-141">Per tenere traccia della distribuzione, digitare:</span><span class="sxs-lookup"><span data-stu-id="974c1-141">To track the deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="974c1-142">Durante la distribuzione del pod, lo stato è `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="974c1-142">While the pod is deploying, the status is `ContainerCreating`.</span></span> <span data-ttu-id="974c1-143">Per il passaggio del contenitore allo stato `Running`, possono essere necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="974c1-143">It can take a few minutes for the container to enter the `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="974c1-144">Visualizzare la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="974c1-144">View the IIS welcome page</span></span>

<span data-ttu-id="974c1-145">Per esporre il pod con un indirizzo IP pubblico, digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="974c1-145">To expose the pod to the world with a public IP address, type the following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="974c1-146">Con questo comando, Kubernetes crea un servizio e una [regola di Azure Load Balancer](container-service-kubernetes-load-balancing.md) con un indirizzo IP pubblico per il servizio.</span><span class="sxs-lookup"><span data-stu-id="974c1-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for the service.</span></span> 

<span data-ttu-id="974c1-147">Eseguire questo comando per visualizzare lo stato del servizio.</span><span class="sxs-lookup"><span data-stu-id="974c1-147">Run the following command to see the status of the service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="974c1-148">L'indirizzo IP viene inizialmente visualizzato come `pending`.</span><span class="sxs-lookup"><span data-stu-id="974c1-148">Initially the IP address appears as `pending`.</span></span> <span data-ttu-id="974c1-149">Dopo alcuni minuti, viene impostato l'indirizzo IP esterno del pod `iis`:</span><span class="sxs-lookup"><span data-stu-id="974c1-149">After a few minutes, the external IP address of the `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="974c1-150">È possibile usare il Web browser che si preferisce per vedere la pagina iniziale di IIS predefinita all'indirizzo IP esterno:</span><span class="sxs-lookup"><span data-stu-id="974c1-150">You can use a web browser of your choice to see the default IIS welcome page at the external IP address:</span></span>

![Immagine del passaggio a IIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="974c1-152">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="974c1-152">Delete cluster</span></span>
<span data-ttu-id="974c1-153">Quando il cluster non è più necessario, è possibile usare il comando [az group delete](/cli/azure/group#delete) per rimuovere il gruppo di risorse, il servizio contenitore e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="974c1-153">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="974c1-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="974c1-154">Next steps</span></span>

<span data-ttu-id="974c1-155">In questa guida introduttiva è stato distribuito un cluster Kubernetes, è stata eseguita la connessione con `kubectl` ed è stato distribuito un pod con un contenitore IIS.</span><span class="sxs-lookup"><span data-stu-id="974c1-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="974c1-156">Per altre informazioni sul servizio contenitore di Azure, continuare con l'esercitazione su Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="974c1-156">To learn more about Azure Container Service, continue to the Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="974c1-157">Gestire un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="974c1-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
