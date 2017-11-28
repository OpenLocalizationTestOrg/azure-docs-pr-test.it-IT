---
title: esercitazione per il servizio contenitore aaaAzure - applicazioni su larga scala | Documenti Microsoft
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="75053-104">Scalare i pod e l'infrastruttura Kubernetes</span><span class="sxs-lookup"><span data-stu-id="75053-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="75053-105">Se ci ha seguito esercitazioni hello, si dispone di un lavoro Kubernetes cluster nel servizio contenitore di Azure e hello Azure voto app è stata distribuita.</span><span class="sxs-lookup"><span data-stu-id="75053-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="75053-106">In questa esercitazione, parte 5, 7, scalabilità POD hello in app hello si cerca la scalabilità automatica pod.</span><span class="sxs-lookup"><span data-stu-id="75053-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="75053-107">Verrà inoltre descritto come numero di hello tooscale di macchina virtuale di Azure agente nodi toochange hello capacità del cluster per ospitare i carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="75053-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="75053-108">Le attività completate comprendono:</span><span class="sxs-lookup"><span data-stu-id="75053-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75053-109">Scalabilità manuale di pod Kubernetes</span><span class="sxs-lookup"><span data-stu-id="75053-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="75053-110">Configurazione di scalabilità automatica POD esecuzione front-end di hello app</span><span class="sxs-lookup"><span data-stu-id="75053-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="75053-111">Ridimensionare i nodi di hello Kubernetes agente di Azure</span><span class="sxs-lookup"><span data-stu-id="75053-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="75053-112">Nelle esercitazioni successive, viene aggiornato l'applicazione Azure voto hello e Operations Management Suite sono configurati cluster di Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="75053-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="75053-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="75053-113">Before you begin</span></span>

<span data-ttu-id="75053-114">Nelle esercitazioni precedenti, un'applicazione è stata distribuita in un'immagine contenitore, questa immagine caricata tooAzure contenitore del Registro di sistema e un cluster Kubernetes creato.</span><span class="sxs-lookup"><span data-stu-id="75053-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="75053-115">un'applicazione Hello quindi è stata eseguita nel cluster Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="75053-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="75053-116">Se si è già questi passaggi e si desidera toofollow lungo, restituire toohello [esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="75053-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="75053-117">Il requisito minimo per questa esercitazione è un cluster Kubernetes con un'applicazione in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="75053-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="75053-118">Scalare manualmente i pod</span><span class="sxs-lookup"><span data-stu-id="75053-118">Manually scale pods</span></span>

<span data-ttu-id="75053-119">Finora, hello Azure voto front-end e l'istanza di Redis sono stati distribuiti, ognuno con una singola replica.</span><span class="sxs-lookup"><span data-stu-id="75053-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="75053-120">tooverify, eseguire hello [kubectl ottenere](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) comando.</span><span class="sxs-lookup"><span data-stu-id="75053-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="75053-121">Output:</span><span class="sxs-lookup"><span data-stu-id="75053-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="75053-122">Modificare manualmente il numero di hello di POD in hello `azure-vote-front` distribuzione utilizzando hello [scala kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) comando.</span><span class="sxs-lookup"><span data-stu-id="75053-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="75053-123">Questo esempio si aumentano too5 numero hello.</span><span class="sxs-lookup"><span data-stu-id="75053-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="75053-124">Eseguire [kubectl ottenere POD](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify che Kubernetes crea POD hello.</span><span class="sxs-lookup"><span data-stu-id="75053-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="75053-125">Dopo un minuto, eseguono POD aggiuntive hello:</span><span class="sxs-lookup"><span data-stu-id="75053-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="75053-126">Output:</span><span class="sxs-lookup"><span data-stu-id="75053-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="75053-127">Scalare automaticamente i pod</span><span class="sxs-lookup"><span data-stu-id="75053-127">Autoscale pods</span></span>

<span data-ttu-id="75053-128">Supporta Kubernetes [il ridimensionamento orizzontale pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) POD in una distribuzione a seconda della CPU o altri numerosi hello tooadjust selezionare metriche.</span><span class="sxs-lookup"><span data-stu-id="75053-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="75053-129">toouse hello autoscaler, l'unità deve avere le richieste di CPU e i limiti definiti.</span><span class="sxs-lookup"><span data-stu-id="75053-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="75053-130">In hello `azure-vote-front` distribuzione, hello CPU richieste 0,25 contenitore front-end, con un limite pari a 0,5 della CPU.</span><span class="sxs-lookup"><span data-stu-id="75053-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="75053-131">le impostazioni di Hello è simile:</span><span class="sxs-lookup"><span data-stu-id="75053-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="75053-132">esempio Hello utilizza hello [scalabilità automatica kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) comando tooautoscale hello numero di unità in hello `azure-vote-front` distribuzione.</span><span class="sxs-lookup"><span data-stu-id="75053-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="75053-133">In questo caso, se l'utilizzo della CPU superiore al 50%, hello autoscaler aumenta hello POD tooa massimo 10.</span><span class="sxs-lookup"><span data-stu-id="75053-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="75053-134">stato di hello toosee di autoscaler hello, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="75053-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="75053-135">Output:</span><span class="sxs-lookup"><span data-stu-id="75053-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="75053-136">Dopo alcuni minuti, con un carico minimo sull'app Azure voto hello, numero di hello di repliche pod riduce automaticamente too3.</span><span class="sxs-lookup"><span data-stu-id="75053-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="75053-137">Agenti di hello scala</span><span class="sxs-lookup"><span data-stu-id="75053-137">Scale hello agents</span></span>

<span data-ttu-id="75053-138">Se è stato creato il cluster Kubernetes utilizzando i comandi predefiniti nell'esercitazione precedente hello, dispone di tre nodi di agente.</span><span class="sxs-lookup"><span data-stu-id="75053-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="75053-139">Se si prevede più o meno contenitore i carichi di lavoro nel cluster, è possibile modificare manualmente il numero di hello degli agenti.</span><span class="sxs-lookup"><span data-stu-id="75053-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="75053-140">Hello utilizzare [az acs scalare](/cli/azure/acs#scale) comando e specificare il numero di hello di agenti con hello `--new-agent-count` parametro.</span><span class="sxs-lookup"><span data-stu-id="75053-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="75053-141">esempio Hello aumenta il numero di hello di agente too4 di nodi nel cluster Kubernetes hello denominato *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="75053-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="75053-142">comando Hello accetta un paio di minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="75053-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="75053-143">Hello output del comando Mostra il numero di hello dell'agente nodi valore hello `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="75053-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="75053-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75053-144">Next steps</span></span>

<span data-ttu-id="75053-145">In questa esercitazione sono state usate diverse funzionalità di scalabilità nel cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="75053-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="75053-146">Le attività descritte includevano:</span><span class="sxs-lookup"><span data-stu-id="75053-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="75053-147">Scalabilità manuale di pod Kubernetes</span><span class="sxs-lookup"><span data-stu-id="75053-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="75053-148">Configurazione di scalabilità automatica POD esecuzione front-end di hello app</span><span class="sxs-lookup"><span data-stu-id="75053-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="75053-149">Ridimensionare i nodi di hello Kubernetes agente di Azure</span><span class="sxs-lookup"><span data-stu-id="75053-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="75053-150">Spostare toohello Avanti toolearn esercitazione sull'aggiornamento dell'applicazione in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="75053-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75053-151">Aggiornare un'applicazione in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="75053-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

