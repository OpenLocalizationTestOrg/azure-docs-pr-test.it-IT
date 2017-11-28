---
title: aaaQuickstart - cluster Kubernetes di Azure per Windows | Documenti Microsoft
description: Consente di capire velocemente toocreate un cluster Kubernetes per i contenitori di Windows nel servizio contenitore di Azure con hello CLI di Azure.
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
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="826d0-103">Distribuire cluster Kubernetes per contenitori Windows</span><span class="sxs-lookup"><span data-stu-id="826d0-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="826d0-104">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="826d0-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="826d0-105">Questa guida descrive con hello Azure CLI toodeploy un [Kubernetes](https://kubernetes.io/docs/home/) cluster nel [servizio contenitore di Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="826d0-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="826d0-106">Dopo aver distribuito il cluster hello, ci si connette tooit con hello Kubernetes `kubectl` strumento da riga di comando e distribuire il primo contenitore di Windows.</span><span class="sxs-lookup"><span data-stu-id="826d0-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="826d0-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="826d0-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="826d0-108">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="826d0-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="826d0-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="826d0-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="826d0-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="826d0-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="826d0-111">Il supporto per i contenitori Windows in Kubernetes nel servizio contenitore di Azure è disponibile in versione di anteprima.</span><span class="sxs-lookup"><span data-stu-id="826d0-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="826d0-112">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="826d0-112">Create a resource group</span></span>

<span data-ttu-id="826d0-113">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="826d0-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="826d0-114">Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="826d0-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="826d0-115">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="826d0-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="826d0-116">Creare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="826d0-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="826d0-117">Creare un cluster di Kubernetes nel servizio contenitore di Azure con hello [az acs creare](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="826d0-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="826d0-118">esempio Hello crea un cluster denominato *myK8sCluster* con uno Linux master nodo e due nodi di agente di Windows.</span><span class="sxs-lookup"><span data-stu-id="826d0-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="826d0-119">Questo esempio crea SSH master Linux toohello tooconnect necessari di chiavi.</span><span class="sxs-lookup"><span data-stu-id="826d0-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="826d0-120">Questo esempio viene utilizzato *azureuser* per un nome utente amministrativo e *myPassword12* come password hello nei nodi di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="826d0-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="826d0-121">Aggiornare questi ambiente appropriato tooyour toosomething di valori.</span><span class="sxs-lookup"><span data-stu-id="826d0-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="826d0-122">Dopo alcuni minuti, hello comando viene completato e vengono visualizzate informazioni sulla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="826d0-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="826d0-123">Installare kubectl</span><span class="sxs-lookup"><span data-stu-id="826d0-123">Install kubectl</span></span>

<span data-ttu-id="826d0-124">tooconnect toohello Kubernetes cluster da computer client, utilizzare [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), client di hello Kubernetes della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="826d0-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="826d0-125">Se si usa Azure CloudShell, `kubectl` è già installato.</span><span class="sxs-lookup"><span data-stu-id="826d0-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="826d0-126">Se si desidera tooinstall in locale, può utilizzare hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="826d0-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="826d0-127">Hello seguente installa esempio CLI di Azure `kubectl` tooyour sistema.</span><span class="sxs-lookup"><span data-stu-id="826d0-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="826d0-128">In Windows eseguire questo comando come amministratore.</span><span class="sxs-lookup"><span data-stu-id="826d0-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="826d0-129">Connettersi con kubectl</span><span class="sxs-lookup"><span data-stu-id="826d0-129">Connect with kubectl</span></span>

<span data-ttu-id="826d0-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, eseguire hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="826d0-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="826d0-131">Hello esempio download di configurazione del cluster per il cluster Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="826d0-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="826d0-132">tooverify cluster tooyour hello connessione dal computer, provare a eseguire:</span><span class="sxs-lookup"><span data-stu-id="826d0-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="826d0-133">`kubectl`Elenca i nodi master e l'agente di hello.</span><span class="sxs-lookup"><span data-stu-id="826d0-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="826d0-134">Distribuire un contenitore IIS Windows</span><span class="sxs-lookup"><span data-stu-id="826d0-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="826d0-135">È possibile eseguire un contenitore Docker all'interno di un *pod* Kubernetes, che contiene uno o più contenitori.</span><span class="sxs-lookup"><span data-stu-id="826d0-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="826d0-136">Questo esempio di base viene utilizzato un toospecify file JSON un contenitore di Microsoft Internet Information Server (IIS) e quindi crea pod hello utilizzando hello `kubctl apply` comando.</span><span class="sxs-lookup"><span data-stu-id="826d0-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="826d0-137">Creare un file locale denominato `iis.json` e hello copia seguendo il testo.</span><span class="sxs-lookup"><span data-stu-id="826d0-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="826d0-138">Questo file indica Kubernetes toorun IIS in Windows Server 2016 Nano Server, usando un'immagine di contenitore pubblico da [Hub Docker](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="826d0-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="826d0-139">contenitore di Hello Usa la porta 80, ma inizialmente è accessibile solo all'interno di rete di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="826d0-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

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

<span data-ttu-id="826d0-140">pod hello toostart, di tipo:</span><span class="sxs-lookup"><span data-stu-id="826d0-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="826d0-141">distribuzione di hello tootrack, tipo:</span><span class="sxs-lookup"><span data-stu-id="826d0-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="826d0-142">Durante la distribuzione di pod hello, lo stato di hello è `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="826d0-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="826d0-143">Può richiedere alcuni minuti per hello di hello contenitore tooenter `Running` stato.</span><span class="sxs-lookup"><span data-stu-id="826d0-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="826d0-144">Hello Visualizza la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="826d0-144">View hello IIS welcome page</span></span>

<span data-ttu-id="826d0-145">tooexpose pod toohello HelloWorld con un indirizzo IP pubblico, hello tipo comando seguente:</span><span class="sxs-lookup"><span data-stu-id="826d0-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="826d0-146">Con questo comando, Kubernetes crea un servizio e un [regola di bilanciamento del carico di Azure](container-service-kubernetes-load-balancing.md) con un indirizzo IP pubblico per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="826d0-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="826d0-147">Eseguire hello seguente lo stato del comando toosee hello del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="826d0-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="826d0-148">Indirizzo IP hello viene inizialmente visualizzato come `pending`.</span><span class="sxs-lookup"><span data-stu-id="826d0-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="826d0-149">Dopo alcuni minuti, hello indirizzo IP esterno di hello `iis` pod è impostato:</span><span class="sxs-lookup"><span data-stu-id="826d0-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="826d0-150">È possibile utilizzare le scelte toosee hello IIS pagina iniziale predefinita di un browser web all'indirizzo IP esterno hello:</span><span class="sxs-lookup"><span data-stu-id="826d0-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Immagine di esplorazione tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="826d0-152">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="826d0-152">Delete cluster</span></span>
<span data-ttu-id="826d0-153">Quando il cluster hello non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi gruppo di risorse hello tooremove, il servizio contenitore e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="826d0-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="826d0-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="826d0-154">Next steps</span></span>

<span data-ttu-id="826d0-155">In questa guida introduttiva è stato distribuito un cluster Kubernetes, è stata eseguita la connessione con `kubectl` ed è stato distribuito un pod con un contenitore IIS.</span><span class="sxs-lookup"><span data-stu-id="826d0-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="826d0-156">toolearn ulteriori informazioni su servizio di contenitore di Azure, continuare toohello Kubernetes esercitazione.</span><span class="sxs-lookup"><span data-stu-id="826d0-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="826d0-157">Gestire un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="826d0-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
