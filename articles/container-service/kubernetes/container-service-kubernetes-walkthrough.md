---
title: aaaQuickstart - cluster Kubernetes di Azure per Linux | Documenti Microsoft
description: Consente di capire velocemente toocreate un cluster Kubernetes per i contenitori di Linux nel servizio contenitore di Azure con hello CLI di Azure.
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
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="a9c3c-103">Distribuire cluster Kubernetes per contenitori Linux</span><span class="sxs-lookup"><span data-stu-id="a9c3c-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="a9c3c-104">In questa Guida introduttiva viene distribuito un cluster di Kubernetes utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="a9c3c-105">Un'applicazione multi-contenitore composta da front-end web e un'istanza di Redis viene quindi distribuita e in esecuzione nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="a9c3c-106">Una volta completato, un'applicazione hello è accessibile tramite internet hello.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="a9c3c-107">applicazione di esempio Hello utilizzata in questo documento viene scritto in Python.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="a9c3c-108">concetti Hello e i passaggi descritti in questa sezione possono essere utilizzati toodeploy qualsiasi contenitore di immagini in un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="a9c3c-109">Hello codice, Dockerfile e progetto toothis correlati di pre-creato Kubernetes file manifesto sono disponibili sul [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="a9c3c-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Immagine di esplorazione tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="a9c3c-111">Questa Guida introduttiva presuppone una conoscenza di base dei concetti Kubernetes, per informazioni dettagliate sul Kubernetes vedere hello [Kubernetes documentazione]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="a9c3c-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="a9c3c-112">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a9c3c-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a9c3c-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a9c3c-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a9c3c-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="a9c3c-116">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a9c3c-116">Create a resource group</span></span>

<span data-ttu-id="a9c3c-117">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a9c3c-118">Un gruppo di risorse di Azure è un gruppo logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="a9c3c-119">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="a9c3c-120">Output:</span><span class="sxs-lookup"><span data-stu-id="a9c3c-120">Output:</span></span>

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

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="a9c3c-121">Creare un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a9c3c-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="a9c3c-122">Creare un cluster di Kubernetes nel servizio contenitore di Azure con hello [az acs creare](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="a9c3c-123">esempio Hello crea un cluster denominato *myK8sCluster* con uno Linux master nodo e i tre nodi di agente di Linux.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="a9c3c-124">Dopo alcuni minuti, il comando hello completa e restituisce informazioni in formato json sul cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="a9c3c-125">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="a9c3c-125">Connect toohello cluster</span></span>

<span data-ttu-id="a9c3c-126">Utilizzare un cluster, Kubernetes toomanage [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client di hello Kubernetes della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="a9c3c-127">Se si usa Azure CloudShell, kubectl è già installato.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="a9c3c-128">Se si desidera tooinstall in locale, può utilizzare hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="a9c3c-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, eseguire hello [az acs kubernetes get-credenziali](/cli/azure/acs/kubernetes#get-credentials) comando.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="a9c3c-130">Questo passaggio Scarica le credenziali e configura hello toouse Kubernetes CLI li.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="a9c3c-131">tooverify hello connessione tooyour cluster utilizzare hello [kubectl ottenere](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando tooreturn un elenco di nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="a9c3c-132">Output:</span><span class="sxs-lookup"><span data-stu-id="a9c3c-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="a9c3c-133">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a9c3c-133">Run hello application</span></span>

<span data-ttu-id="a9c3c-134">Un file manifesto Kubernetes definisce uno stato desiderato per il cluster hello, incluse le immagini contenitore devono essere in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="a9c3c-135">Per questo esempio, un manifesto è toocreate utilizzati tutti gli oggetti necessari toorun hello applicazione Azure voto.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="a9c3c-136">Creare un file denominato `azure-vote.yml` copia al suo interno e hello seguenti YAML.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="a9c3c-137">Se si usa Azure Cloud Shell, questo file può essere creato usando vi o Nano come se si usasse un sistema virtuale o fisico.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

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

<span data-ttu-id="a9c3c-138">Hello utilizzare [kubectl creare](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) comando applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="a9c3c-139">Output:</span><span class="sxs-lookup"><span data-stu-id="a9c3c-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="a9c3c-140">Testare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="a9c3c-140">Test hello application</span></span>

<span data-ttu-id="a9c3c-141">Durante l'esecuzione di un'applicazione hello, un [Kubernetes servizio](https://kubernetes.io/docs/concepts/services-networking/service/) viene creato che espone hello applicazione front-end toohello internet.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="a9c3c-142">Questo processo può richiedere alcuni minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="a9c3c-143">lo stato di avanzamento toomonitor, utilizzare hello [kubectl ottenere servizio](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) con hello `--watch` argomento.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="a9c3c-144">Inizialmente hello **esterno IP** per hello *azure voto-anteriore* servizio viene visualizzato come *in sospeso*.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="a9c3c-145">Una volta che l'indirizzo IP esterno hello è stato modificato da *in sospeso* tooan *indirizzo IP*, utilizzare `CTRL-C` processo di controllo kubectl toostop hello.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="a9c3c-146">È ora possibile esplorare toohello esterno IP indirizzo toosee hello Azure voto App.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![Immagine di esplorazione tooAzure voto](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="a9c3c-148">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="a9c3c-148">Delete cluster</span></span>
<span data-ttu-id="a9c3c-149">Quando il cluster hello non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi gruppo di risorse hello tooremove, il servizio contenitore e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="a9c3c-150">Ottenere il codice hello</span><span class="sxs-lookup"><span data-stu-id="a9c3c-150">Get hello code</span></span>

<span data-ttu-id="a9c3c-151">In questa Guida introduttiva, le immagini contenitore creato in precedenza sono stati utilizzati toocreate una distribuzione Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="a9c3c-152">Hello correlati Dockerfile, codice dell'applicazione e file manifesto Kubernetes sono disponibili su GitHub.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="a9c3c-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="a9c3c-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="a9c3c-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9c3c-154">Next steps</span></span>

<span data-ttu-id="a9c3c-155">In questa Guida introduttiva è distribuito un cluster Kubernetes e distribuito tooit un'applicazione multi-contenitore.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="a9c3c-156">toolearn ulteriori informazioni su servizio di contenitore di Azure e procedura per un esempio di toodeployment di codice completo, continuare l'esercitazione di toohello Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="a9c3c-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9c3c-157">Gestire un cluster Kubernetes ACS</span><span class="sxs-lookup"><span data-stu-id="a9c3c-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
