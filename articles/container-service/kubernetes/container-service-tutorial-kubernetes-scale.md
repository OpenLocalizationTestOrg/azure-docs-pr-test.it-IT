---
title: Esercitazione per il servizio contenitore di Azure - Scalare un'applicazione | Microsoft Docs
description: Esercitazione per il servizio contenitore di Azure - Scalare un'applicazione
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, microservizi, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 62e70e34d06f5220734ff85c70a0c9b475f9579b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="cadbc-104">Scalare i pod e l'infrastruttura Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cadbc-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="cadbc-105">Se sono state eseguite le esercitazioni, si ha un cluster Kubernetes in funzione nel servizio contenitore di Azure ed è stata distribuita l'app Azure Voting.</span><span class="sxs-lookup"><span data-stu-id="cadbc-105">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span></span> 

<span data-ttu-id="cadbc-106">In questa esercitazione, la quinta di sette, si aumenterà il numero di istanze dei pod nell'app e si proverà la scalabilità automatica dei pod.</span><span class="sxs-lookup"><span data-stu-id="cadbc-106">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="cadbc-107">Si apprenderà anche come ridimensionare il numero di nodi agente delle VM di Azure per modificare la capacità del cluster per l'hosting dei carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="cadbc-107">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="cadbc-108">Le attività completate comprendono:</span><span class="sxs-lookup"><span data-stu-id="cadbc-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cadbc-109">Scalabilità manuale di pod Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cadbc-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="cadbc-110">Configurazione della scalabilità automatica di pod che eseguono il front-end dell'app</span><span class="sxs-lookup"><span data-stu-id="cadbc-110">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="cadbc-111">Scalare i nodi agente Azure in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cadbc-111">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="cadbc-112">Nelle esercitazioni successive l'applicazione Azure Vote viene aggiornata e Operations Management Suite viene configurato per monitorare il cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cadbc-112">In subsequent tutorials, the Azure Vote application is updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cadbc-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cadbc-113">Before you begin</span></span>

<span data-ttu-id="cadbc-114">Nelle esercitazioni precedenti è stato creato un pacchetto di un'applicazione in un'immagine del contenitore, caricata poi nel Registro contenitori di Azure, ed è stato creato un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cadbc-114">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="cadbc-115">L'applicazione è stata quindi eseguita nel cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cadbc-115">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="cadbc-116">Se questi passaggi non sono stati ancora eseguiti e si vuole procedere, tornare a [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md) (Esercitazione 1: Creare immagini del contenitore).</span><span class="sxs-lookup"><span data-stu-id="cadbc-116">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="cadbc-117">Il requisito minimo per questa esercitazione è un cluster Kubernetes con un'applicazione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cadbc-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="cadbc-118">Scalare manualmente i pod</span><span class="sxs-lookup"><span data-stu-id="cadbc-118">Manually scale pods</span></span>

<span data-ttu-id="cadbc-119">Fino a questo momento sono stati distribuiti il front-end di Azure Vote e l'istanza di Redis, ognuno con una replica singola.</span><span class="sxs-lookup"><span data-stu-id="cadbc-119">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="cadbc-120">Per verificare, eseguire il comando [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="cadbc-120">To verify, run the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="cadbc-121">Output:</span><span class="sxs-lookup"><span data-stu-id="cadbc-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="cadbc-122">Modificare manualmente il numero di pod nella distribuzione `azure-vote-front` usando il comando [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale).</span><span class="sxs-lookup"><span data-stu-id="cadbc-122">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="cadbc-123">In questo esempio il numero aumenta a 5.</span><span class="sxs-lookup"><span data-stu-id="cadbc-123">This example increases the number to 5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="cadbc-124">Eseguire [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) per verificare che Kubernetes stia creando i pod.</span><span class="sxs-lookup"><span data-stu-id="cadbc-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) to verify that Kubernetes is creating the pods.</span></span> <span data-ttu-id="cadbc-125">Dopo circa un minuto i pod aggiuntivi sono in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="cadbc-125">After a minute or so, the additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="cadbc-126">Output:</span><span class="sxs-lookup"><span data-stu-id="cadbc-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="cadbc-127">Scalare automaticamente i pod</span><span class="sxs-lookup"><span data-stu-id="cadbc-127">Autoscale pods</span></span>

<span data-ttu-id="cadbc-128">Kubernetes supporta la [scalabilità automatica orizzontale dei pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) per modificare il numero dei pod in una distribuzione a seconda dell'utilizzo della CPU o delle altre metriche selezionate.</span><span class="sxs-lookup"><span data-stu-id="cadbc-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="cadbc-129">Per usare la scalabilità automatica, i pod devono avere richieste e limiti di CPU definiti.</span><span class="sxs-lookup"><span data-stu-id="cadbc-129">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="cadbc-130">Nella distribuzione di `azure-vote-front` il contenitore front-end richiede un valore di 0,25 della CPU, con un limite pari a 0,5 della CPU.</span><span class="sxs-lookup"><span data-stu-id="cadbc-130">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="cadbc-131">Le impostazioni sono simili:</span><span class="sxs-lookup"><span data-stu-id="cadbc-131">The settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="cadbc-132">L'esempio seguente usa il comando [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) per scalare automaticamente il numero di pod nella distribuzione `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="cadbc-132">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span></span> <span data-ttu-id="cadbc-133">In questo caso, se l'utilizzo della CPU supera il 50%, la scalabilità automatica aumenta il numero di pod fino al valore massimo di 10.</span><span class="sxs-lookup"><span data-stu-id="cadbc-133">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="cadbc-134">Per visualizzare lo stato della scalabilità automatica, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cadbc-134">To see the status of the autoscaler, run the following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="cadbc-135">Output:</span><span class="sxs-lookup"><span data-stu-id="cadbc-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="cadbc-136">Dopo pochi minuti con un carico minimo sull'app Azure Vote, il numero di repliche di pod si riduce automaticamente a 3.</span><span class="sxs-lookup"><span data-stu-id="cadbc-136">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span></span>

## <a name="scale-the-agents"></a><span data-ttu-id="cadbc-137">Scalare gli agenti</span><span class="sxs-lookup"><span data-stu-id="cadbc-137">Scale the agents</span></span>

<span data-ttu-id="cadbc-138">Se è stato creato usando i comandi predefiniti nell'esercitazione precedente, il cluster Kubernetes dispone di tre nodi agente.</span><span class="sxs-lookup"><span data-stu-id="cadbc-138">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="cadbc-139">Se si prevede un numero maggiore o minore di carichi di lavoro dei contenitori nel cluster, è possibile modificare manualmente il numero di agenti.</span><span class="sxs-lookup"><span data-stu-id="cadbc-139">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="cadbc-140">Usare il comando [az acs scale](/cli/azure/acs#scale) e specificare il numero di agenti con il parametro `--new-agent-count`.</span><span class="sxs-lookup"><span data-stu-id="cadbc-140">Use the [az acs scale](/cli/azure/acs#scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span></span>

<span data-ttu-id="cadbc-141">Nell'esempio seguente il numero di nodi agente viene aumentato a 4 nel cluster Kubernetes, denominato *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="cadbc-141">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="cadbc-142">Il completamento del comando richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="cadbc-142">The command takes a couple of minutes to complete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="cadbc-143">L'output del comando mostra il numero di nodi agente nel valore di `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="cadbc-143">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="cadbc-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cadbc-144">Next steps</span></span>

<span data-ttu-id="cadbc-145">In questa esercitazione sono state usate diverse funzionalità di scalabilità nel cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cadbc-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="cadbc-146">Le attività descritte includevano:</span><span class="sxs-lookup"><span data-stu-id="cadbc-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cadbc-147">Scalabilità manuale di pod Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cadbc-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="cadbc-148">Configurazione della scalabilità automatica di pod che eseguono il front-end dell'app</span><span class="sxs-lookup"><span data-stu-id="cadbc-148">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="cadbc-149">Scalare i nodi agente Azure in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cadbc-149">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="cadbc-150">Passare all'esercitazione successiva per apprendere come aggiornare l'applicazione in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cadbc-150">Advance to the next tutorial to learn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cadbc-151">Aggiornare un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cadbc-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

