---
title: cluster di Azure Kubernetes aaaMonitor - Operations Manager | Documenti Microsoft
description: Monitoraggio di cluster Kubernetes nel servizio contenitore di Azure con Microsoft Operations Management Suite
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="52a32-103">Monitorare un cluster del servizio contenitore di Azure con Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="52a32-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52a32-104">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="52a32-104">Prerequisites</span></span>
<span data-ttu-id="52a32-105">Si presume che questa procedura dettagliata abbia [creato un cluster Kubernetes mediante il servizio contenitore di Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="52a32-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="52a32-106">Inoltre, presuppone di aver hello `az` cli di Azure e `kubectl` installati gli strumenti.</span><span class="sxs-lookup"><span data-stu-id="52a32-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="52a32-107">È possibile verificare se si dispone di hello `az` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="52a32-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="52a32-108">Se non si dispone di hello `az` strumento installato, non esistono istruzioni [qui](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="52a32-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="52a32-109">In alternativa, è possibile utilizzare [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), che dispone di hello `az` cli di Azure e `kubectl` strumenti già installati.</span><span class="sxs-lookup"><span data-stu-id="52a32-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="52a32-110">È possibile verificare se si dispone di hello `kubectl` strumento installato eseguendo:</span><span class="sxs-lookup"><span data-stu-id="52a32-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="52a32-111">Se `kubectl` non è installato, è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="52a32-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="52a32-112">tootest se si dispongono di chiavi kubernetes installate nello strumento di kubectl è possibile eseguire:</span><span class="sxs-lookup"><span data-stu-id="52a32-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="52a32-113">Se hello sopra errori comando, sono necessarie le chiavi di cluster di tooinstall kubernetes nello strumento di kubectl desiderato.</span><span class="sxs-lookup"><span data-stu-id="52a32-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="52a32-114">È possibile farlo con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="52a32-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="52a32-115">Monitoraggio dei contenitori con Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="52a32-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="52a32-116">Microsoft Operations Management (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.</span><span class="sxs-lookup"><span data-stu-id="52a32-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="52a32-117">Soluzione di contenitore è una soluzione Analitica di Log di OMS, che consente di visualizzare l'inventario contenitore hello, prestazioni e i log in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="52a32-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="52a32-118">È possibile audit, risoluzione dei contenitori di visualizzazione dei log di hello in posizione centralizzata e trovare rumore utilizzo in eccesso contenitore in un host.</span><span class="sxs-lookup"><span data-stu-id="52a32-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="52a32-119">Per ulteriori informazioni sulla soluzione di contenitore, vedere toothe [contenitore soluzione Log Analitica](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="52a32-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="52a32-120">Installazione di OMS in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="52a32-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="52a32-121">Ottenere l'ID e la chiave dell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="52a32-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="52a32-122">Per hello servizio toohello tootalk dell'agente OMS deve toobe configurato con un id area di lavoro e una chiave dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="52a32-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="52a32-123">id tooget hello e la chiave è necessario un OMS toocreate account in <https://mms.microsoft.com>. Seguire hello passaggi toocreate un account.</span><span class="sxs-lookup"><span data-stu-id="52a32-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="52a32-124">Dopo aver terminato la creazione di account di hello, è necessario tooobtain l'id e la chiave facendo **impostazioni**, quindi **Connected Sources**e quindi **server Linux**, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="52a32-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="52a32-125">Installare l'agente OMS hello utilizzando un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="52a32-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="52a32-126">DaemonSets vengono utilizzati da Kubernetes toorun una singola istanza di un contenitore in ogni host in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="52a32-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="52a32-127">Sono ideali per l'esecuzione di agenti di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="52a32-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="52a32-128">Ecco hello [file DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="52a32-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="52a32-129">Salvare il file tooa denominato `oms-daemonset.yaml` e sostituire i valori segnaposto hello per `WSID` e `KEY` con l'id area di lavoro e la chiave nel file hello.</span><span class="sxs-lookup"><span data-stu-id="52a32-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="52a32-130">Dopo aver aggiunto l'ID e la configurazione di DaemonSet toohello chiave, è possibile installare l'agente OMS hello in cluster con hello `kubectl` strumento da riga di comando:</span><span class="sxs-lookup"><span data-stu-id="52a32-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="52a32-131">Installazione agente OMS hello utilizzando un segreto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="52a32-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="52a32-132">tooprotect l'ID area di lavoro OMS e la chiave è possibile utilizzare Kubernetes segreto come parte del file DaemonSet YAML.</span><span class="sxs-lookup"><span data-stu-id="52a32-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="52a32-133">Copia script hello, file di modello segreta e hello file DaemonSet YAML (da [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) e assicurarsi che siano presenti hello stessa directory.</span><span class="sxs-lookup"><span data-stu-id="52a32-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="52a32-134">Script per la generazione di segreti: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="52a32-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="52a32-135">Modello di segreto: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="52a32-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="52a32-136">File DaemonSet YAML: omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="52a32-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="52a32-137">Eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="52a32-137">Run hello script.</span></span> <span data-ttu-id="52a32-138">script Hello verrà chiesta hello ID area di lavoro OMS e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="52a32-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="52a32-139">Inserire che e script hello creerà un file di secret yaml in modo da eseguire.</span><span class="sxs-lookup"><span data-stu-id="52a32-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="52a32-140">Creare pod segreti hello eseguendo hello:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="52a32-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="52a32-141">toocheck, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="52a32-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="52a32-142">Creare il DaemonSet dell'agente OMS eseguendo l'istruzione ``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="52a32-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="52a32-143">Conclusione</span><span class="sxs-lookup"><span data-stu-id="52a32-143">Conclusion</span></span>
<span data-ttu-id="52a32-144">L'operazione è terminata.</span><span class="sxs-lookup"><span data-stu-id="52a32-144">That's it!</span></span> <span data-ttu-id="52a32-145">Dopo alcuni minuti, si dovrebbe essere toosee in grado di dati che passano tooyour dashboard OMS.</span><span class="sxs-lookup"><span data-stu-id="52a32-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
