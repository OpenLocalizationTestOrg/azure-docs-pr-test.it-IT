---
title: esercitazione per il servizio contenitore aaaAzure - monitoraggio Kubernetes | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Monitorare Kubernetes con Microsoft Operations Management Suite (OMS)
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="404e4-104">Monitorare un cluster Kubernetes con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="404e4-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="404e4-105">Il monitoraggio del cluster e dei contenitori Kubernetes è critico, soprattutto quando si gestisce un cluster di produzione su larga scala con più app.</span><span class="sxs-lookup"><span data-stu-id="404e4-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="404e4-106">È possibile sfruttare diverse soluzioni di monitoraggio di Kubernetes, da Microsoft o da altri provider.</span><span class="sxs-lookup"><span data-stu-id="404e4-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="404e4-107">In questa esercitazione, monitorare il cluster Kubernetes utilizzando hello contenitori soluzione in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), soluzione di gestione IT Microsoft basata sul cloud.</span><span class="sxs-lookup"><span data-stu-id="404e4-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="404e4-108">(hello soluzione contenitori OMS è in anteprima).</span><span class="sxs-lookup"><span data-stu-id="404e4-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="404e4-109">In questa esercitazione, parte 7 di sette, copre hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="404e4-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="404e4-110">Ottenere le impostazioni dell'area di lavoro di OMS</span><span class="sxs-lookup"><span data-stu-id="404e4-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="404e4-111">Configurare gli agenti OMS nei nodi Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="404e4-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="404e4-112">Accedere a informazioni di monitoraggio nel portale di OMS hello o il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="404e4-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="404e4-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="404e4-113">Before you begin</span></span>

<span data-ttu-id="404e4-114">Nelle esercitazioni precedenti, un'applicazione è stata assemblata in immagini contenitore, queste immagini caricate tooAzure contenitore del Registro di sistema e un cluster Kubernetes creato.</span><span class="sxs-lookup"><span data-stu-id="404e4-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="404e4-115">Se si è già questi passaggi e si desidera toofollow lungo, restituire troppo[esercitazione 1: creare le immagini contenitore](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="404e4-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="404e4-116">Come requisito minimo, questa esercitazione richiede un cluster Kubernetes con nodi di agente di Linux, e un account di Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="404e4-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="404e4-117">Se necessario, registrarsi per una [versione di valutazione gratuita di OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="404e4-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="404e4-118">Ottenere le impostazioni dell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="404e4-118">Get Workspace settings</span></span>

<span data-ttu-id="404e4-119">Quando è possibile accedere a hello [portale OMS](https://mms.microsoft.com), andare troppo**impostazioni** > **Connected Sources** > **server Linux**.</span><span class="sxs-lookup"><span data-stu-id="404e4-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="404e4-120">Non esiste, è possibile trovare hello *ID area di lavoro* e un database primario o secondario *chiave dell'area di lavoro*.</span><span class="sxs-lookup"><span data-stu-id="404e4-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="404e4-121">Prendere nota di questi valori, che è necessario tooset installare gli agenti OMS in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="404e4-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="404e4-122">Configurare gli agenti OMS</span><span class="sxs-lookup"><span data-stu-id="404e4-122">Set up OMS agents</span></span>

<span data-ttu-id="404e4-123">Di seguito è riportato un tooset file YAML installare gli agenti OMS nei nodi del cluster Linux hello.</span><span class="sxs-lookup"><span data-stu-id="404e4-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="404e4-124">Questa operazione crea un [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) di Kubernetes, che esegue un singolo pod identico in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="404e4-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="404e4-125">risorsa DaemonSet Hello è ideale per la distribuzione di un agente di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="404e4-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="404e4-126">Salvare i seguenti file di testo tooa denominato hello `oms-daemonset.yaml`e sostituire i valori segnaposto hello per *myWorkspaceID* e *myWorkspaceKey* con l'ID area di lavoro OMS e la chiave.</span><span class="sxs-lookup"><span data-stu-id="404e4-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="404e4-127">(nell'ambiente di produzione, è possibile codificare questi valori come segreti).</span><span class="sxs-lookup"><span data-stu-id="404e4-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="404e4-128">Creare hello DaemonSet con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="404e4-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="404e4-129">toosee tale hello DaemonSet viene creato, eseguire:</span><span class="sxs-lookup"><span data-stu-id="404e4-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="404e4-130">L'output è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="404e4-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="404e4-131">Dopo che sono in esecuzione gli agenti di hello, sono necessari diversi minuti per OMS tooingest ed elaborare hello i dati.</span><span class="sxs-lookup"><span data-stu-id="404e4-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="404e4-132">Accesso ai dati di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="404e4-132">Access monitoring data</span></span>

<span data-ttu-id="404e4-133">Visualizzare e analizzare i dati con hello di monitoraggio tipo contenitore hello OMS [soluzione contenitore](../../log-analytics/log-analytics-containers.md) nel portale di OMS hello o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="404e4-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="404e4-134">soluzione di contenitore hello tooinstall hello [portale OMS](https://mms.microsoft.com), andare troppo**Solutions Gallery**.</span><span class="sxs-lookup"><span data-stu-id="404e4-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="404e4-135">Aggiungere quindi la **Soluzione Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="404e4-135">Then add **Container Solution**.</span></span> <span data-ttu-id="404e4-136">In alternativa, aggiungere soluzioni contenitori hello da hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="404e4-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="404e4-137">Nel portale OMS hello, cercare un **contenitori** riquadro Riepilogo del dashboard OMS hello.</span><span class="sxs-lookup"><span data-stu-id="404e4-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="404e4-138">Fare clic sul riquadro hello per dettagli, tra cui: utilizzo della CPU e memoria, errori, lo stato, inventario immagine ed eventi di contenitore.</span><span class="sxs-lookup"><span data-stu-id="404e4-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="404e4-139">Per informazioni più granulari, fare clic su una riga in qualsiasi riquadro o eseguire una [ricerca log](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="404e4-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Dashboard dei contenitori nel portale OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="404e4-141">Analogamente, nel portale di Azure hello, andare troppo**Analitica Log** e selezionare il nome dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="404e4-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="404e4-142">hello toosee **contenitori** sezione di riepilogo, fare clic su **soluzioni** > **contenitori**.</span><span class="sxs-lookup"><span data-stu-id="404e4-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="404e4-143">toosee dettagli, fare clic su riquadro hello.</span><span class="sxs-lookup"><span data-stu-id="404e4-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="404e4-144">Vedere hello [documentazione di Azure Log Analitica](../../log-analytics/index.md) per istruzioni dettagliate sulla query e analisi dei dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="404e4-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="404e4-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="404e4-145">Next steps</span></span>

<span data-ttu-id="404e4-146">In questa esercitazione è stato monitorato il cluster di Kubernetes con OMS.</span><span class="sxs-lookup"><span data-stu-id="404e4-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="404e4-147">Le attività descritte includevano:</span><span class="sxs-lookup"><span data-stu-id="404e4-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="404e4-148">Ottenere le impostazioni dell'area di lavoro di OMS</span><span class="sxs-lookup"><span data-stu-id="404e4-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="404e4-149">Configurare gli agenti OMS nei nodi Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="404e4-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="404e4-150">Accedere a informazioni di monitoraggio nel portale di OMS hello o il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="404e4-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="404e4-151">Seguire questo toosee di collegamento incorporati gli esempi di script per il servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="404e4-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="404e4-152">Esempi di script del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="404e4-152">Azure Container Service script samples</span></span>](cli-samples.md)
