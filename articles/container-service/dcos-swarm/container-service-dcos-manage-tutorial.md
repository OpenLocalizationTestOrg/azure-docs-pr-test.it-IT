---
title: esercitazione per il servizio contenitore aaaAzure - controller di dominio di gestione del sistema operativo | Documenti Microsoft
description: Esercitazione sul servizio contenitore di Azure - Gestire DC/OS
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenitori, Micro-Service, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="18497-104">Esercitazione sul servizio contenitore di Azure - Gestire DC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="18497-105">DC/OS fornisce una piattaforma distribuita per l'esecuzione di applicazioni in contenitori e moderne.</span><span class="sxs-lookup"><span data-stu-id="18497-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="18497-106">Con il servizio contenitore di Azure, il provisioning di un cluster DC/OS pronto per la produzione è semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="18497-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="18497-107">Questo passaggi di base di informazioni di avvio rapido necessari toodeploy un cluster di controller di dominio o del sistema operativo e un carico di lavoro di base esecuzione.</span><span class="sxs-lookup"><span data-stu-id="18497-107">This quick start details basic steps needed toodeploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="18497-108">Creare un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="18497-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="18497-109">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="18497-109">Connect toohello cluster</span></span>
> * <span data-ttu-id="18497-110">Installare controller di dominio/OS CLI hello</span><span class="sxs-lookup"><span data-stu-id="18497-110">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="18497-111">Distribuire un cluster di toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="18497-111">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="18497-112">Scalabilità di un'applicazione in cluster hello</span><span class="sxs-lookup"><span data-stu-id="18497-112">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="18497-113">Ridimensionare i nodi del cluster hello controller di dominio o del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="18497-113">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="18497-114">Gestione di base di DC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="18497-115">Eliminare il cluster di controller di dominio/OS hello</span><span class="sxs-lookup"><span data-stu-id="18497-115">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="18497-116">Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="18497-116">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="18497-117">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="18497-117">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="18497-118">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="18497-118">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="18497-119">Creare un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-119">Create DC/OS cluster</span></span>

<span data-ttu-id="18497-120">Innanzitutto, creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="18497-120">First, create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="18497-121">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="18497-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="18497-122">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westeurope* percorso.</span><span class="sxs-lookup"><span data-stu-id="18497-122">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="18497-123">Successivamente, creare un cluster di controller di dominio o del sistema operativo con hello [az acs creare](/cli/azure/acs#create) comando.</span><span class="sxs-lookup"><span data-stu-id="18497-123">Next, create a DC/OS cluster with hello [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="18497-124">esempio Hello crea un cluster di controller di dominio o del sistema operativo denominato *myDCOSCluster* e crea le chiavi SSH se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="18497-124">hello following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="18497-125">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="18497-125">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="18497-126">Dopo alcuni minuti, comando hello completa e restituisce informazioni sulla distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="18497-126">After several minutes, hello command completes, and returns information about hello deployment.</span></span>

## <a name="connect-toodcos-cluster"></a><span data-ttu-id="18497-127">Connettere il cluster tooDC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-127">Connect tooDC/OS cluster</span></span>

<span data-ttu-id="18497-128">Dopo aver creato un cluster DC/OS, è possibile accedervi tramite un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="18497-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="18497-129">Comando che segue di esecuzione hello tooreturn hello indirizzo IP pubblico del database master di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="18497-129">Run hello following command tooreturn hello public IP address of hello DC/OS master.</span></span> <span data-ttu-id="18497-130">Questo indirizzo IP è archiviato in una variabile e usato nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="18497-130">This IP address is stored in a variable and used in hello next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="18497-131">toocreate hello tunnel SSH, eseguire hello comando seguente e istruzioni hello sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="18497-131">toocreate hello SSH tunnel, run hello following command and follow hello on-screen instructions.</span></span> <span data-ttu-id="18497-132">Se la porta 80 è già in uso, il comando hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="18497-132">If port 80 is already in use, hello command fails.</span></span> <span data-ttu-id="18497-133">Hello aggiornamento tunneled tooone porta non è in uso, ad esempio `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="18497-133">Update hello tunneled port tooone not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="18497-134">Installare l'interfaccia della riga di comando di DC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-134">Install DC/OS CLI</span></span>

<span data-ttu-id="18497-135">Installare hello cli di controller di dominio/OS utilizzando hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando.</span><span class="sxs-lookup"><span data-stu-id="18497-135">Install hello DC/OS cli using hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="18497-136">Se si utilizza Azure CloudShell, hello CLI di controller di dominio o del sistema operativo è già installato.</span><span class="sxs-lookup"><span data-stu-id="18497-136">If you are using Azure CloudShell, hello DC/OS CLI is already installed.</span></span> <span data-ttu-id="18497-137">Se si esegue hello CLI di Azure in macOS o Linux, potrebbe essere comando hello toorun con sudo.</span><span class="sxs-lookup"><span data-stu-id="18497-137">If you are running hello Azure CLI on macOS or Linux, you might need toorun hello command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="18497-138">Prima di hello che CLI può essere utilizzato con i cluster di hello, deve essere tunnel SSH di hello toouse configurato.</span><span class="sxs-lookup"><span data-stu-id="18497-138">Before hello CLI can be used with hello cluster, it must be configured toouse hello SSH tunnel.</span></span> <span data-ttu-id="18497-139">toodo in tal caso, eseguire hello comando seguente, modificare la porta hello se necessario.</span><span class="sxs-lookup"><span data-stu-id="18497-139">toodo so, run hello following command, adjusting hello port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="18497-140">Eseguire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="18497-140">Run an application</span></span>

<span data-ttu-id="18497-141">valore predefinito di Hello meccanismo per un cluster ACS controller di dominio o del sistema operativo di pianificazione è maratona.</span><span class="sxs-lookup"><span data-stu-id="18497-141">hello default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="18497-142">Maratona toostart utilizzata un'applicazione e gestire lo stato di hello di un'applicazione hello nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="18497-142">Marathon is used toostart an application and manage hello state of hello application on hello DC/OS cluster.</span></span> <span data-ttu-id="18497-143">tooschedule un'applicazione tramite maratona, creare un file denominato **maratona app.json**, e hello copia seguendo contenuto al suo interno.</span><span class="sxs-lookup"><span data-stu-id="18497-143">tooschedule an application through Marathon, create a file named **marathon-app.json**, and copy hello following contents into it.</span></span> 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="18497-144">Eseguire hello successivo comando tooschedule hello applicazione toorun nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="18497-144">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="18497-145">stato della distribuzione toosee hello per le app di hello, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="18497-145">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="18497-146">Quando hello **attività** passa il valore di colonna da *0/1* troppo*1/1*, la distribuzione di applicazioni è stata completata.</span><span class="sxs-lookup"><span data-stu-id="18497-146">When hello **TASKS** column value switches from *0/1* too*1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="18497-147">Ridimensionare l'applicazione Marathon</span><span class="sxs-lookup"><span data-stu-id="18497-147">Scale Marathon application</span></span>

<span data-ttu-id="18497-148">Nell'esempio precedente hello è stata creata un'applicazione a istanza singola.</span><span class="sxs-lookup"><span data-stu-id="18497-148">In hello previous example, a single instance application was created.</span></span> <span data-ttu-id="18497-149">Questa distribuzione in modo che siano disponibili, tre istanze di un'applicazione hello aprire hello tooupdate **maratona app.json** file e aggiornare hello istanza proprietà too3.</span><span class="sxs-lookup"><span data-stu-id="18497-149">tooupdate this deployment so that three instances of hello application are available, open up hello **marathon-app.json** file, and update hello instance property too3.</span></span>

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

<span data-ttu-id="18497-150">Aggiornare l'applicazione hello utilizzando hello `dcos marathon app update` comando.</span><span class="sxs-lookup"><span data-stu-id="18497-150">Update hello application using hello `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="18497-151">stato della distribuzione toosee hello per le app di hello, eseguire hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="18497-151">toosee hello deployment status for hello app, run hello following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="18497-152">Quando hello **attività** passa il valore di colonna da *1/3* troppo*3/1*, la distribuzione di applicazioni è stata completata.</span><span class="sxs-lookup"><span data-stu-id="18497-152">When hello **TASKS** column value switches from *1/3* too*3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="18497-153">Eseguire un'app accessibile su Internet</span><span class="sxs-lookup"><span data-stu-id="18497-153">Run internet accessible app</span></span>

<span data-ttu-id="18497-154">Hello ACS controller di dominio o del sistema operativo cluster include due set di nodi, una pubblica accessibile su internet di hello e una privata che non è accessibile su internet di hello.</span><span class="sxs-lookup"><span data-stu-id="18497-154">hello ACS DC/OS cluster consists of two node sets, one public which is accessible on hello internet, and one private which is not accessible on hello internet.</span></span> <span data-ttu-id="18497-155">set predefinito di Hello è nodi privata hello, che è stato usato nell'ultimo esempio hello.</span><span class="sxs-lookup"><span data-stu-id="18497-155">hello default set is hello private nodes, which was used in hello last example.</span></span>

<span data-ttu-id="18497-156">un'applicazione accessibile toomake in hello internet, distribuirle toohello set di nodi pubblici.</span><span class="sxs-lookup"><span data-stu-id="18497-156">toomake an application accessible on hello internet, deploy them toohello public node set.</span></span> <span data-ttu-id="18497-157">toodo, valutare hello `acceptedResourceRoles` il valore dell'oggetto `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="18497-157">toodo so, give hello `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="18497-158">Creare un file denominato **nginx public.json** e hello copia seguendo contenuto al suo interno.</span><span class="sxs-lookup"><span data-stu-id="18497-158">Create a file named **nginx-public.json** and copy hello following contents into it.</span></span>

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

<span data-ttu-id="18497-159">Eseguire hello successivo comando tooschedule hello applicazione toorun nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="18497-159">Run hello following command tooschedule hello application toorun on hello DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="18497-160">Ottenere l'indirizzo IP pubblico hello degli agenti di cluster pubblica hello controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="18497-160">Get hello public IP address of hello DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="18497-161">Esplorazione toothis indirizzo restituisce sito NGINX di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="18497-161">Browsing toothis address returns hello default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="18497-163">Ridimensionare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="18497-164">Negli esempi precedenti hello, un'applicazione è stato ridimensionato toomultiple istanza.</span><span class="sxs-lookup"><span data-stu-id="18497-164">In hello previous examples, an application was scaled toomultiple instance.</span></span> <span data-ttu-id="18497-165">infrastruttura di controller di dominio/OS Hello può anche essere scalato tooprovide più o meno capacità di calcolo.</span><span class="sxs-lookup"><span data-stu-id="18497-165">hello DC/OS infrastructure can also be scaled tooprovide more or less compute capacity.</span></span> <span data-ttu-id="18497-166">Questa operazione viene eseguita con hello [az acs scalare]() comando.</span><span class="sxs-lookup"><span data-stu-id="18497-166">This is done with hello [az acs scale]() command.</span></span> 

<span data-ttu-id="18497-167">numero corrente di hello toosee degli agenti di controller di dominio o del sistema operativo, utilizzare hello [az acs Mostra](/cli/azure/acs#show) comando.</span><span class="sxs-lookup"><span data-stu-id="18497-167">toosee hello current count of DC/OS agents, use hello [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="18497-168">tooincrease hello too5 count, utilizzare hello [az acs scalare](/cli/azure/acs#scale) comando.</span><span class="sxs-lookup"><span data-stu-id="18497-168">tooincrease hello count too5, use hello [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="18497-169">Eliminare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="18497-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="18497-170">Quando non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comandi tooremove gruppo di risorse hello, cluster/OS di controller di dominio e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="18497-170">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="18497-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="18497-171">Next steps</span></span>

<span data-ttu-id="18497-172">In questa esercitazione, si è appreso sulle attività di gestione di controller di dominio o del sistema operativo base inclusi hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="18497-172">In this tutorial, you have learned about basic DC/OS management task including hello following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="18497-173">Creare un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="18497-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="18497-174">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="18497-174">Connect toohello cluster</span></span>
> * <span data-ttu-id="18497-175">Installare controller di dominio/OS CLI hello</span><span class="sxs-lookup"><span data-stu-id="18497-175">Install hello DC/OS CLI</span></span>
> * <span data-ttu-id="18497-176">Distribuire un cluster di toohello applicazione</span><span class="sxs-lookup"><span data-stu-id="18497-176">Deploy an application toohello cluster</span></span>
> * <span data-ttu-id="18497-177">Scalabilità di un'applicazione in cluster hello</span><span class="sxs-lookup"><span data-stu-id="18497-177">Scale an application on hello cluster</span></span>
> * <span data-ttu-id="18497-178">Ridimensionare i nodi del cluster hello controller di dominio o del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="18497-178">Scale hello DC/OS cluster nodes</span></span>
> * <span data-ttu-id="18497-179">Eliminare il cluster di controller di dominio/OS hello</span><span class="sxs-lookup"><span data-stu-id="18497-179">Delete hello DC/OS cluster</span></span>

<span data-ttu-id="18497-180">Anticipo toohello successivo dell'esercitazione toolearn su caricare l'applicazione di bilanciamento del carico nel controller di dominio o sistema operativo in Azure.</span><span class="sxs-lookup"><span data-stu-id="18497-180">Advance toohello next tutorial toolearn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="18497-181">Bilanciare il carico delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="18497-181">Load balance applications</span></span>](container-service-load-balancing.md)