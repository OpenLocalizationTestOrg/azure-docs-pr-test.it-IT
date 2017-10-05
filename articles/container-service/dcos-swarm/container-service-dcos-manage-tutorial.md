---
title: Esercitazione sul servizio contenitore di Azure - Gestire DC/OS | Microsoft Docs
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
ms.openlocfilehash: e93f782c26c32f97749e817ec59ee3c2ecb7e119
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a><span data-ttu-id="5fbbf-104">Esercitazione sul servizio contenitore di Azure - Gestire DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-104">Azure Container Service tutorial - Manage DC/OS</span></span>

<span data-ttu-id="5fbbf-105">DC/OS fornisce una piattaforma distribuita per l'esecuzione di applicazioni in contenitori e moderne.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="5fbbf-106">Con il servizio contenitore di Azure, il provisioning di un cluster DC/OS pronto per la produzione è semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="5fbbf-107">Questa guida rapida illustra in dettaglio i passaggi di base necessari per distribuire un cluster DC/OS ed eseguire un carico di lavoro di base.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-107">This quick start details basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5fbbf-108">Creare un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="5fbbf-108">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="5fbbf-109">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="5fbbf-109">Connect to the cluster</span></span>
> * <span data-ttu-id="5fbbf-110">Installare l'interfaccia della riga di comando di DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-110">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="5fbbf-111">Distribuire un'applicazione nel cluster</span><span class="sxs-lookup"><span data-stu-id="5fbbf-111">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="5fbbf-112">Ridimensionare un'applicazione nel cluster</span><span class="sxs-lookup"><span data-stu-id="5fbbf-112">Scale an application on the cluster</span></span>
> * <span data-ttu-id="5fbbf-113">Ridimensionare i nodi del cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-113">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="5fbbf-114">Gestione di base di DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-114">Basic DC/OS management</span></span>
> * <span data-ttu-id="5fbbf-115">Eliminare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-115">Delete the DC/OS cluster</span></span>

<span data-ttu-id="5fbbf-116">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-116">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5fbbf-117">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-117">Run `az --version` to find the version.</span></span> <span data-ttu-id="5fbbf-118">Se è necessario eseguire l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-118">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-dcos-cluster"></a><span data-ttu-id="5fbbf-119">Creare un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-119">Create DC/OS cluster</span></span>

<span data-ttu-id="5fbbf-120">Creare prima di tutto un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-120">First, create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5fbbf-121">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-121">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5fbbf-122">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-122">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="5fbbf-123">Creare prima di tutto un cluster DC/OS con il comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-123">Next, create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="5fbbf-124">L'esempio seguente crea un cluster DC/OS denominato *myDCOSCluster* e crea le chiavi SSH se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-124">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="5fbbf-125">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-125">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="5fbbf-126">Dopo alcuni minuti, il comando viene completato e restituisce le informazioni sulla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-126">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="5fbbf-127">Connettersi al cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-127">Connect to DC/OS cluster</span></span>

<span data-ttu-id="5fbbf-128">Dopo aver creato un cluster DC/OS, è possibile accedervi tramite un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-128">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="5fbbf-129">Eseguire il comando seguente per restituire l'indirizzo IP pubblico del master DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-129">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="5fbbf-130">L'indirizzo IP viene archiviato in una variabile e usato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-130">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="5fbbf-131">Per creare il tunnel SSH, eseguire il comando seguente e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-131">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="5fbbf-132">Se la porta 80 è già in uso, il comando non riesce.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-132">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="5fbbf-133">Aggiornare la porta di tunneling selezionandone una non in uso, come `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-133">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a><span data-ttu-id="5fbbf-134">Installare l'interfaccia della riga di comando di DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-134">Install DC/OS CLI</span></span>

<span data-ttu-id="5fbbf-135">Installare l'interfaccia della riga di comando di DC/OS con il comando [az acs dcos install-cli](/azure/acs/dcos#install-cli).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-135">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="5fbbf-136">Se si usa Azure CloudShell, l'interfaccia della riga di comando di DC/OS è già installata.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-136">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> <span data-ttu-id="5fbbf-137">Se si esegue l'interfaccia della riga di comando di Azure in macOS o Linux, potrebbe essere necessario eseguire il comando con sudo.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-137">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="5fbbf-138">Prima di poter usare l'interfaccia della riga di comando con il cluster, deve essere configurato per usare il tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-138">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="5fbbf-139">A tale scopo, eseguire il comando seguente, modificando la porta se necessario.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-139">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="5fbbf-140">Eseguire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="5fbbf-140">Run an application</span></span>

<span data-ttu-id="5fbbf-141">Il meccanismo di pianificazione predefinito per un cluster DC/OS del servizio contenitore di Azure è Marathon.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-141">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="5fbbf-142">Marathon viene usato per avviare un'applicazione e gestire lo stato dell'applicazione nel cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-142">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="5fbbf-143">Per pianificare un'applicazione tramite Marathon, creare un file denominato **marathon-app.json** e copiarvi il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-143">To schedule an application through Marathon, create a file named **marathon-app.json**, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="5fbbf-144">Eseguire il comando seguente per pianificare l'esecuzione dell'applicazione nel cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-144">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="5fbbf-145">Per visualizzare lo stato di distribuzione per l'app, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-145">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="5fbbf-146">Quando il valore della colonna **TASKS** (Attività) passa da *0/1* a *1/1*, la distribuzione dell'applicazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-146">When the **TASKS** column value switches from *0/1* to *1/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a><span data-ttu-id="5fbbf-147">Ridimensionare l'applicazione Marathon</span><span class="sxs-lookup"><span data-stu-id="5fbbf-147">Scale Marathon application</span></span>

<span data-ttu-id="5fbbf-148">Nell'esempio precedente è stata creata un'applicazione a istanza singola.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-148">In the previous example, a single instance application was created.</span></span> <span data-ttu-id="5fbbf-149">Per aggiornare la distribuzione in modo che siano disponibili tre istanze dell'applicazione, aprire il file **marathon-app.json** e impostare la proprietà per le istanze su 3.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-149">To update this deployment so that three instances of the application are available, open up the **marathon-app.json** file, and update the instance property to 3.</span></span>

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

<span data-ttu-id="5fbbf-150">Aggiornare l'applicazione con il comando `dcos marathon app update`.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-150">Update the application using the `dcos marathon app update` command.</span></span>

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

<span data-ttu-id="5fbbf-151">Per visualizzare lo stato di distribuzione per l'app, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-151">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="5fbbf-152">Quando il valore della colonna **TASKS** (Attività) passa da *1/3* a *3/1*, la distribuzione dell'applicazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-152">When the **TASKS** column value switches from *1/3* to *3/1*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a><span data-ttu-id="5fbbf-153">Eseguire un'app accessibile su Internet</span><span class="sxs-lookup"><span data-stu-id="5fbbf-153">Run internet accessible app</span></span>

<span data-ttu-id="5fbbf-154">Il cluster DC/OS del servizio contenitore di Azure è costituito da due set di nodi, uno pubblico accessibile su Internet e uno privato non accessibile su Internet.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-154">The ACS DC/OS cluster consists of two node sets, one public which is accessible on the internet, and one private which is not accessible on the internet.</span></span> <span data-ttu-id="5fbbf-155">Il set predefinito è quello dei nodi privati, usato nell'ultimo esempio.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-155">The default set is the private nodes, which was used in the last example.</span></span>

<span data-ttu-id="5fbbf-156">Per rendere un'applicazione accessibile su Internet, distribuirla nel set di nodi pubblico.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-156">To make an application accessible on the internet, deploy them to the public node set.</span></span> <span data-ttu-id="5fbbf-157">A tale scopo, assegnare all'oggetto `acceptedResourceRoles` il valore `slave_public`.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-157">To do so, give the `acceptedResourceRoles` object a value of `slave_public`.</span></span>

<span data-ttu-id="5fbbf-158">Creare un file denominato **nginx-public.json** e copiare il contenuto seguente nel file.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-158">Create a file named **nginx-public.json** and copy the following contents into it.</span></span>

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

<span data-ttu-id="5fbbf-159">Eseguire il comando seguente per pianificare l'esecuzione dell'applicazione nel cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-159">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli 
dcos marathon app add nginx-public.json
```

<span data-ttu-id="5fbbf-160">Ottenere l'indirizzo IP pubblico degli agenti del cluster pubblico DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-160">Get the public IP address of the DC/OS public cluster agents.</span></span>

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="5fbbf-161">Passando a questo indirizzo viene restituito il sito NGINX predefinito.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-161">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a><span data-ttu-id="5fbbf-163">Ridimensionare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-163">Scale DC/OS cluster</span></span>

<span data-ttu-id="5fbbf-164">Negli esempi precedenti, un'applicazione è stata ridimensionata per più istanze.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-164">In the previous examples, an application was scaled to multiple instance.</span></span> <span data-ttu-id="5fbbf-165">Anche l'infrastruttura di DC/OS può essere ridimensionata per offrire maggiore o minore capacità di calcolo.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-165">The DC/OS infrastructure can also be scaled to provide more or less compute capacity.</span></span> <span data-ttu-id="5fbbf-166">Questa operazione viene eseguita con il comando [az acs scale]().</span><span class="sxs-lookup"><span data-stu-id="5fbbf-166">This is done with the [az acs scale]() command.</span></span> 

<span data-ttu-id="5fbbf-167">Per visualizzare il numero corrente di agenti di DC/OS, usare il comando [az acs show](/cli/azure/acs#show).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-167">To see the current count of DC/OS agents, use the [az acs show](/cli/azure/acs#show) command.</span></span>

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

<span data-ttu-id="5fbbf-168">Per aumentare il conteggio a 5, usare il comando [az acs scale](/cli/azure/acs#scale).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-168">To increase the count to 5, use the [az acs scale](/cli/azure/acs#scale) command.</span></span> 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a><span data-ttu-id="5fbbf-169">Eliminare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-169">Delete DC/OS cluster</span></span>

<span data-ttu-id="5fbbf-170">Quando non serve più, è possibile rimuovere il gruppo di risorse, il cluster DC/OS e tutte le risorse correlate tramite il comando [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="5fbbf-170">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="5fbbf-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fbbf-171">Next steps</span></span>

<span data-ttu-id="5fbbf-172">In questa esercitazione sono state descritte le attività di gestione di base di DC/OS, incluse le seguenti.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-172">In this tutorial, you have learned about basic DC/OS management task including the following.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5fbbf-173">Creare un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="5fbbf-173">Create an ACS DC/OS cluster</span></span>
> * <span data-ttu-id="5fbbf-174">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="5fbbf-174">Connect to the cluster</span></span>
> * <span data-ttu-id="5fbbf-175">Installare l'interfaccia della riga di comando di DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-175">Install the DC/OS CLI</span></span>
> * <span data-ttu-id="5fbbf-176">Distribuire un'applicazione nel cluster</span><span class="sxs-lookup"><span data-stu-id="5fbbf-176">Deploy an application to the cluster</span></span>
> * <span data-ttu-id="5fbbf-177">Ridimensionare un'applicazione nel cluster</span><span class="sxs-lookup"><span data-stu-id="5fbbf-177">Scale an application on the cluster</span></span>
> * <span data-ttu-id="5fbbf-178">Ridimensionare i nodi del cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-178">Scale the DC/OS cluster nodes</span></span>
> * <span data-ttu-id="5fbbf-179">Eliminare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5fbbf-179">Delete the DC/OS cluster</span></span>

<span data-ttu-id="5fbbf-180">Passare all'esercitazione successiva per apprendere come bilanciare il carico delle applicazioni in DC/OS in Azure.</span><span class="sxs-lookup"><span data-stu-id="5fbbf-180">Advance to the next tutorial to learn about load balancing application in DC/OS on Azure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="5fbbf-181">Bilanciare il carico delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="5fbbf-181">Load balance applications</span></span>](container-service-load-balancing.md)