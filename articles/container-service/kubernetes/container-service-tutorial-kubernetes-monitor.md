---
title: Esercitazione sul servizio contenitore di Azure - Monitorare Kubernetes | Microsoft Docs
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
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="294b3-104">Monitorare un cluster Kubernetes con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="294b3-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="294b3-105">Il monitoraggio del cluster e dei contenitori Kubernetes è critico, soprattutto quando si gestisce un cluster di produzione su larga scala con più app.</span><span class="sxs-lookup"><span data-stu-id="294b3-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="294b3-106">È possibile sfruttare diverse soluzioni di monitoraggio di Kubernetes, da Microsoft o da altri provider.</span><span class="sxs-lookup"><span data-stu-id="294b3-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="294b3-107">In questa esercitazione si monitora il cluster Kubernetes con la soluzione dei contenitori in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), la soluzione di gestione IT di Microsoft basata sul cloud.</span><span class="sxs-lookup"><span data-stu-id="294b3-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="294b3-108">(la soluzione dei Contenitori di OMS è in anteprima).</span><span class="sxs-lookup"><span data-stu-id="294b3-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="294b3-109">Questa esercitazione, parte sette di sette, illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="294b3-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="294b3-110">Ottenere le impostazioni dell'area di lavoro di OMS</span><span class="sxs-lookup"><span data-stu-id="294b3-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="294b3-111">Configurare gli agenti OMS nei nodi Kubernetes</span><span class="sxs-lookup"><span data-stu-id="294b3-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="294b3-112">Accedere alle informazioni di monitoraggio nel portale di OMS o nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="294b3-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="294b3-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="294b3-113">Before you begin</span></span>

<span data-ttu-id="294b3-114">Nelle esercitazioni precedenti è stato creato un pacchetto di un'applicazione in immagini del contenitore, caricate poi nel Registro contenitori di Azure, ed è stato creato un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="294b3-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="294b3-115">Se questi passaggi non sono stati ancora eseguiti e si vuole procedere, tornare a [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md) (Esercitazione 1: Creare immagini del contenitore).</span><span class="sxs-lookup"><span data-stu-id="294b3-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="294b3-116">Come requisito minimo, questa esercitazione richiede un cluster Kubernetes con nodi di agente di Linux, e un account di Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="294b3-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="294b3-117">Se necessario, registrarsi per una [versione di valutazione gratuita di OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="294b3-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="294b3-118">Ottenere le impostazioni dell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="294b3-118">Get Workspace settings</span></span>

<span data-ttu-id="294b3-119">Quando è possibile accedere al [portale OMS](https://mms.microsoft.com), passare a **Impostazioni** > **Origini connesse** > **Server Linux**.</span><span class="sxs-lookup"><span data-stu-id="294b3-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="294b3-120">Qui è possibile trovare l'*ID area di lavoro* e una *Chiave dell'area di lavoro* primaria o secondaria.</span><span class="sxs-lookup"><span data-stu-id="294b3-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="294b3-121">Prendere nota di questi valori, per cui è necessario configurare gli agenti OMS nel cluster.</span><span class="sxs-lookup"><span data-stu-id="294b3-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="294b3-122">Configurare gli agenti OMS</span><span class="sxs-lookup"><span data-stu-id="294b3-122">Set up OMS agents</span></span>

<span data-ttu-id="294b3-123">Di seguito è riportato un file con estensione YAML per configurare gli agenti OMS nei nodi del cluster di Linux.</span><span class="sxs-lookup"><span data-stu-id="294b3-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="294b3-124">Questa operazione crea un [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) di Kubernetes, che esegue un singolo pod identico in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="294b3-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="294b3-125">La risorsa DaemonSet è ideale per la distribuzione di un agente di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="294b3-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="294b3-126">Salvare il testo seguente in un file denominato `oms-daemonset.yaml` e sostituire i valori del segnaposto *myWorkspaceID* e *myWorkspaceKey* con l'ID e la chiave dell'area di lavoro OMS</span><span class="sxs-lookup"><span data-stu-id="294b3-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="294b3-127">(nell'ambiente di produzione, è possibile codificare questi valori come segreti).</span><span class="sxs-lookup"><span data-stu-id="294b3-127">(In production, you can encode these values as secrets.)</span></span>

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

<span data-ttu-id="294b3-128">Creare il DaemonSet con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="294b3-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="294b3-129">Per verificare che sia stato creato il DaemonSet, eseguire:</span><span class="sxs-lookup"><span data-stu-id="294b3-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="294b3-130">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="294b3-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="294b3-131">Con gli agenti in esecuzione, OMS richiede diversi minuti per inserire ed elaborare i dati.</span><span class="sxs-lookup"><span data-stu-id="294b3-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="294b3-132">Accesso ai dati di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="294b3-132">Access monitoring data</span></span>

<span data-ttu-id="294b3-133">Visualizzare e analizzare i dati di monitoraggio del contenitore OMS con la [Soluzione Contenitore](../../log-analytics/log-analytics-containers.md) nel portale di OMS o nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="294b3-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="294b3-134">Per installare la Soluzione Contenitore tramite il [portale di OMS](https://mms.microsoft.com), passare a **Raccolta soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="294b3-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="294b3-135">Aggiungere quindi la **Soluzione Contenitore**.</span><span class="sxs-lookup"><span data-stu-id="294b3-135">Then add **Container Solution**.</span></span> <span data-ttu-id="294b3-136">In alternativa, aggiungere la Soluzione Contenitore da [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="294b3-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="294b3-137">Nel portale di OMS cercare un riquadro di riepilogo dei **Contenitori** nel dashboard di OMS.</span><span class="sxs-lookup"><span data-stu-id="294b3-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="294b3-138">Fare clic sul riquadro per i dettagli, tra cui: eventi del contenitore, errori, stato, inventario dell'immagine e uso di CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="294b3-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="294b3-139">Per informazioni più granulari, fare clic su una riga in qualsiasi riquadro o eseguire una [ricerca log](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="294b3-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Dashboard dei contenitori nel portale OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="294b3-141">Analogamente, nel portale di Azure passare a **Log Analytics** e selezionare il nome della propria area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="294b3-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="294b3-142">Per visualizzare il riquadro di riepilogo dei **Contenitori**, fare clic su **Soluzioni** > **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="294b3-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="294b3-143">Per visualizzare i dettagli, fare clic sul riquadro.</span><span class="sxs-lookup"><span data-stu-id="294b3-143">To see details, click the tile.</span></span>

<span data-ttu-id="294b3-144">Vedere la [Documentazione su Log Analytics](../../log-analytics/index.md) per istruzioni dettagliate sulla creazione di query e sull'analisi dei dati di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="294b3-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="294b3-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="294b3-145">Next steps</span></span>

<span data-ttu-id="294b3-146">In questa esercitazione è stato monitorato il cluster di Kubernetes con OMS.</span><span class="sxs-lookup"><span data-stu-id="294b3-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="294b3-147">Le attività descritte includevano:</span><span class="sxs-lookup"><span data-stu-id="294b3-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="294b3-148">Ottenere le impostazioni dell'area di lavoro di OMS</span><span class="sxs-lookup"><span data-stu-id="294b3-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="294b3-149">Configurare gli agenti OMS nei nodi Kubernetes</span><span class="sxs-lookup"><span data-stu-id="294b3-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="294b3-150">Accedere alle informazioni di monitoraggio nel portale di OMS o nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="294b3-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="294b3-151">Seguire questo collegamento per vedere esempi di script predefiniti per il servizio contenitore.</span><span class="sxs-lookup"><span data-stu-id="294b3-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="294b3-152">Esempi di script del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="294b3-152">Azure Container Service script samples</span></span>](cli-samples.md)
