---
title: aaaDeploy un cluster di contenitore Docker - CLI di Azure | Documenti Microsoft
description: Distribuire una soluzione Kubernetes, DC/OS o Docker Swarm nel servizio contenitore di Azure usando l'interfaccia della riga di comando di Azure 2.0
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="77260-103">Distribuire un contenitore Docker mediante Azure CLI 2.0 hello soluzione di hosting</span><span class="sxs-lookup"><span data-stu-id="77260-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="77260-104">Hello utilizzare `az acs` comandi in toocreate hello 2.0 CLI di Azure e gestire i cluster nel servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="77260-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="77260-105">È inoltre possibile distribuire un cluster il servizio contenitore di Azure tramite hello [portale di Azure](container-service-deployment.md) o hello API del servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="77260-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="77260-106">Per informazioni su `az acs` comandi, passare hello `-h` comando tooany di parametro.</span><span class="sxs-lookup"><span data-stu-id="77260-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="77260-107">Ad esempio: `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="77260-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="77260-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77260-108">Prerequisites</span></span>
<span data-ttu-id="77260-109">un cluster il servizio contenitore di Azure mediante toocreate hello CLI di Azure 2.0, è necessario:</span><span class="sxs-lookup"><span data-stu-id="77260-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="77260-110">Avere un account Azure ([versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/))</span><span class="sxs-lookup"><span data-stu-id="77260-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="77260-111">aver installato e configurato hello [CLI di Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="77260-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="77260-112">Attività iniziali</span><span class="sxs-lookup"><span data-stu-id="77260-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="77260-113">Accedi tooyour account</span><span class="sxs-lookup"><span data-stu-id="77260-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="77260-114">Seguire toolog prompt hello in modo interattivo.</span><span class="sxs-lookup"><span data-stu-id="77260-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="77260-115">Per altri metodi toolog in, vedere [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="77260-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="77260-116">Configurare la sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="77260-116">Set your Azure subscription</span></span>

<span data-ttu-id="77260-117">Se si dispone di più di una sottoscrizione di Azure, impostare la sottoscrizione predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="77260-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="77260-118">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="77260-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="77260-119">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="77260-119">Create a resource group</span></span>
<span data-ttu-id="77260-120">È consigliabile creare un gruppo di risorse per ogni cluster.</span><span class="sxs-lookup"><span data-stu-id="77260-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="77260-121">Specificare un'area di Azure in cui sia [disponibile](https://azure.microsoft.com/en-us/regions/services/) il servizio contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="77260-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="77260-122">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="77260-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="77260-123">L'output è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="77260-123">Output is similar toohello following:</span></span>

![Creare un gruppo di risorse](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="77260-125">Creare un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="77260-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="77260-126">Utilizzare un cluster, toocreate `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="77260-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="77260-127">Un nome per il cluster hello e hello hello del gruppo di risorse creato nel passaggio precedente hello sono parametri obbligatori.</span><span class="sxs-lookup"><span data-stu-id="77260-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="77260-128">Gli altri input sono valori toodefault set (vedere la seguente schermata hello) a meno che non sovrascritto con le rispettive opzioni.</span><span class="sxs-lookup"><span data-stu-id="77260-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="77260-129">Ad esempio, orchestrator hello è impostata per operazioni di tooDC predefinita del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="77260-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="77260-130">E se non si specifica un prefisso del nome DNS viene creato in base a nome del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="77260-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![az acs create usage](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="77260-132">Operazione rapida con i valori predefiniti per `acs create`</span><span class="sxs-lookup"><span data-stu-id="77260-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="77260-133">Se si dispone di un file di chiave pubblica SSH RSA `id_rsa.pub` nel percorso predefinito di hello (o è stato creato uno per [OS X e Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) o [Windows](../../virtual-machines/linux/ssh-from-windows.md)), utilizzare un comando simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="77260-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="77260-134">Se non è disponibile alcuna chiave pubblica SSH, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="77260-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="77260-135">Questo comando con hello `--generate-ssh-keys` viene creato uno automaticamente.</span><span class="sxs-lookup"><span data-stu-id="77260-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="77260-136">Dopo aver immesso il comando hello, attendere circa 10 minuti per hello cluster toobe creato.</span><span class="sxs-lookup"><span data-stu-id="77260-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="77260-137">output del comando Hello include nomi di dominio completo (FQDN) del master hello e nodi di agente e un master prima SSH comando tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="77260-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="77260-138">Ecco un output abbreviato:</span><span class="sxs-lookup"><span data-stu-id="77260-138">Here is abbreviated output:</span></span>

![Immagine del comando create del servizio contenitore di Azure](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="77260-140">Hello [procedura dettagliata Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md) viene illustrato come toouse `az acs create` con toocreate di valori predefinito un Kubernetes del cluster.</span><span class="sxs-lookup"><span data-stu-id="77260-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="77260-141">Gestire i cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="77260-141">Manage ACS clusters</span></span>

<span data-ttu-id="77260-142">Utilizzare aggiuntive `az acs` comandi toomanage del cluster.</span><span class="sxs-lookup"><span data-stu-id="77260-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="77260-143">Di seguito sono riportati alcuni esempi.</span><span class="sxs-lookup"><span data-stu-id="77260-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="77260-144">Elencare i cluster in una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="77260-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="77260-145">Elencare i cluster in un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="77260-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="77260-147">Visualizzare i dettagli di un cluster del servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="77260-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="77260-149">Cluster hello scala</span><span class="sxs-lookup"><span data-stu-id="77260-149">Scale hello cluster</span></span>
<span data-ttu-id="77260-150">È consentito sia ridurre che aumentare il numero di istanze dei nodi agente.</span><span class="sxs-lookup"><span data-stu-id="77260-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="77260-151">parametro Hello `new-agent-count` è nuovo numero di agenti in cluster hello ACS di hello.</span><span class="sxs-lookup"><span data-stu-id="77260-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="77260-153">Eliminare un cluster del servizio contenitore</span><span class="sxs-lookup"><span data-stu-id="77260-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="77260-154">Questo comando Elimina tutte le risorse (rete e archiviazione) create durante la creazione del servizio contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="77260-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="77260-155">toodelete tutte le risorse facilmente, è consigliabile implementare ogni cluster in un gruppo di risorse distinto.</span><span class="sxs-lookup"><span data-stu-id="77260-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="77260-156">Eliminare quindi il gruppo di risorse hello quando cluster hello non è più necessario.</span><span class="sxs-lookup"><span data-stu-id="77260-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77260-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77260-157">Next steps</span></span>
<span data-ttu-id="77260-158">Ora che si ha a disposizione un cluster funzionante, vedere i documenti seguenti per informazioni dettagliate sulla connessione e la gestione:</span><span class="sxs-lookup"><span data-stu-id="77260-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="77260-159">Connettersi tooan cluster del servizio di contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="77260-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="77260-160">Gestione di contenitori tramite l'API REST</span><span class="sxs-lookup"><span data-stu-id="77260-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="77260-161">Gestione dei contenitori con Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="77260-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="77260-162">Uso del servizio contenitore di Azure e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="77260-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)