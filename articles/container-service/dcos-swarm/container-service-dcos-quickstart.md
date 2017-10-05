---
title: Guida rapida al servizio contenitore di Azure - Distribuire un cluster DC/OS | Microsoft Docs
description: Guida rapida al servizio contenitore di Azure - Distribuire un cluster DC/OS
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a31170369de9bc1ddcddb97171281b0014af95f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-dcos-cluster"></a><span data-ttu-id="5241a-104">Distribuire un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5241a-104">Deploy a DC/OS cluster</span></span>

<span data-ttu-id="5241a-105">DC/OS fornisce una piattaforma distribuita per l'esecuzione di applicazioni in contenitori e moderne.</span><span class="sxs-lookup"><span data-stu-id="5241a-105">DC/OS provides a distributed platform for running modern and containerized applications.</span></span> <span data-ttu-id="5241a-106">Con il servizio contenitore di Azure, il provisioning di un cluster DC/OS pronto per la produzione è semplice e rapido.</span><span class="sxs-lookup"><span data-stu-id="5241a-106">With Azure Container Service, provisioning of a production ready DC/OS cluster is simple and quick.</span></span> <span data-ttu-id="5241a-107">Questa guida rapida illustra in dettaglio i passaggi di base necessari per distribuire un cluster DC/OS ed eseguire un carico di lavoro di base.</span><span class="sxs-lookup"><span data-stu-id="5241a-107">This quick start details the basic steps needed to deploy a DC/OS cluster and run basic workload.</span></span>

<span data-ttu-id="5241a-108">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="5241a-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="5241a-109">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="5241a-109">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5241a-110">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="5241a-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="5241a-111">Se è necessario eseguire l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5241a-111">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="5241a-112">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="5241a-112">Log in to Azure</span></span> 

<span data-ttu-id="5241a-113">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="5241a-113">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="5241a-114">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5241a-114">Create a resource group</span></span>

<span data-ttu-id="5241a-115">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5241a-115">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5241a-116">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="5241a-116">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5241a-117">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="5241a-117">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a><span data-ttu-id="5241a-118">Creare un cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5241a-118">Create DC/OS cluster</span></span>

<span data-ttu-id="5241a-119">Creare un cluster DC/OS con il comando [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="5241a-119">Create a DC/OS cluster with the [az acs create](/cli/azure/acs#create) command.</span></span>

<span data-ttu-id="5241a-120">L'esempio seguente crea un cluster DC/OS denominato *myDCOSCluster* e crea le chiavi SSH se non esistono già.</span><span class="sxs-lookup"><span data-stu-id="5241a-120">The following example creates a DC/OS cluster named *myDCOSCluster* and creates SSH keys if they do not already exist.</span></span> <span data-ttu-id="5241a-121">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="5241a-121">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

<span data-ttu-id="5241a-122">Dopo alcuni minuti, il comando viene completato e restituisce le informazioni sulla distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5241a-122">After several minutes, the command completes, and returns information about the deployment.</span></span>

## <a name="connect-to-dcos-cluster"></a><span data-ttu-id="5241a-123">Connettersi al cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5241a-123">Connect to DC/OS cluster</span></span>

<span data-ttu-id="5241a-124">Dopo aver creato un cluster DC/OS, è possibile accedervi tramite un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5241a-124">Once a DC/OS cluster has been created, it can be accesses through an SSH tunnel.</span></span> <span data-ttu-id="5241a-125">Eseguire il comando seguente per restituire l'indirizzo IP pubblico del master DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5241a-125">Run the following command to return the public IP address of the DC/OS master.</span></span> <span data-ttu-id="5241a-126">L'indirizzo IP viene archiviato in una variabile e usato nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="5241a-126">This IP address is stored in a variable and used in the next step.</span></span>

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

<span data-ttu-id="5241a-127">Per creare il tunnel SSH, eseguire il comando seguente e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="5241a-127">To create the SSH tunnel, run the following command and follow the on-screen instructions.</span></span> <span data-ttu-id="5241a-128">Se la porta 80 è già in uso, il comando non riesce.</span><span class="sxs-lookup"><span data-stu-id="5241a-128">If port 80 is already in use, the command fails.</span></span> <span data-ttu-id="5241a-129">Aggiornare la porta di tunneling selezionandone una non in uso, come `85:localhost:80`.</span><span class="sxs-lookup"><span data-stu-id="5241a-129">Update the tunneled port to one not in use, such as `85:localhost:80`.</span></span> 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

<span data-ttu-id="5241a-130">Il tunnel SSH può essere testato passando a `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="5241a-130">The SSH tunnel can be tested by browsing to `http://localhost`.</span></span> <span data-ttu-id="5241a-131">Se è stata usata una porta diversa dalla 80, modificare il percorso corrispondentemente.</span><span class="sxs-lookup"><span data-stu-id="5241a-131">If a port other that 80 has been used, adjust the location to match.</span></span> 

<span data-ttu-id="5241a-132">Se il tunnel SSH è stato creato correttamente, viene restituito il portale di DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5241a-132">If the SSH tunnel was successfully created, the DC/OS portal is returned.</span></span>

![Interfaccia utente di DC/OS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a><span data-ttu-id="5241a-134">Installare l'interfaccia della riga di comando di DC/OS</span><span class="sxs-lookup"><span data-stu-id="5241a-134">Install DC/OS CLI</span></span>

<span data-ttu-id="5241a-135">L'interfaccia della riga di comando di DC/OS viene usata per gestire un cluster DC/OS dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="5241a-135">The DC/OS command line interface is used to manage a DC/OS cluster from the command-line.</span></span> <span data-ttu-id="5241a-136">Installare l'interfaccia della riga di comando di DC/OS con il comando [az acs dcos install-cli](/azure/acs/dcos#install-cli).</span><span class="sxs-lookup"><span data-stu-id="5241a-136">Install the DC/OS cli using the [az acs dcos install-cli](/azure/acs/dcos#install-cli) command.</span></span> <span data-ttu-id="5241a-137">Se si usa Azure CloudShell, l'interfaccia della riga di comando di DC/OS è già installata.</span><span class="sxs-lookup"><span data-stu-id="5241a-137">If you are using Azure CloudShell, the DC/OS CLI is already installed.</span></span> 

<span data-ttu-id="5241a-138">Se si esegue l'interfaccia della riga di comando di Azure in macOS o Linux, potrebbe essere necessario eseguire il comando con sudo.</span><span class="sxs-lookup"><span data-stu-id="5241a-138">If you are running the Azure CLI on macOS or Linux, you might need to run the command with sudo.</span></span>

```azurecli
az acs dcos install-cli
```

<span data-ttu-id="5241a-139">Prima di poter usare l'interfaccia della riga di comando con il cluster, deve essere configurato per usare il tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5241a-139">Before the CLI can be used with the cluster, it must be configured to use the SSH tunnel.</span></span> <span data-ttu-id="5241a-140">A tale scopo, eseguire il comando seguente, modificando la porta se necessario.</span><span class="sxs-lookup"><span data-stu-id="5241a-140">To do so, run the following command, adjusting the port if needed.</span></span>

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a><span data-ttu-id="5241a-141">Eseguire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="5241a-141">Run an application</span></span>

<span data-ttu-id="5241a-142">Il meccanismo di pianificazione predefinito per un cluster DC/OS del servizio contenitore di Azure è Marathon.</span><span class="sxs-lookup"><span data-stu-id="5241a-142">The default scheduling mechanism for an ACS DC/OS cluster is Marathon.</span></span> <span data-ttu-id="5241a-143">Marathon viene usato per avviare un'applicazione e gestire lo stato dell'applicazione nel cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5241a-143">Marathon is used to start an application and manage the state of the application on the DC/OS cluster.</span></span> <span data-ttu-id="5241a-144">Per pianificare un'applicazione tramite Marathon, creare un file denominato *marathon-app.json* e copiarvi il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="5241a-144">To schedule an application through Marathon, create a file named *marathon-app.json*, and copy the following contents into it.</span></span> 

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

<span data-ttu-id="5241a-145">Eseguire il comando seguente per pianificare l'esecuzione dell'applicazione nel cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5241a-145">Run the following command to schedule the application to run on the DC/OS cluster.</span></span>

```azurecli
dcos marathon app add marathon-app.json
```

<span data-ttu-id="5241a-146">Per visualizzare lo stato di distribuzione per l'app, eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5241a-146">To see the deployment status for the app, run the following command.</span></span>

```azurecli
dcos marathon app list
```

<span data-ttu-id="5241a-147">Quando il valore della colonna **WAITING** (Attesa) passa da *True* a *False*, la distribuzione dell'applicazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="5241a-147">When the **WAITING** column value switches from *True* to *False*, application deployment has completed.</span></span>

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

<span data-ttu-id="5241a-148">Ottenere l'indirizzo IP pubblico degli agenti del cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="5241a-148">Get the public IP address of the DC/OS cluster agents.</span></span>

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

<span data-ttu-id="5241a-149">Passando a questo indirizzo viene restituito il sito NGINX predefinito.</span><span class="sxs-lookup"><span data-stu-id="5241a-149">Browsing to this address returns the default NGINX site.</span></span>

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a><span data-ttu-id="5241a-151">Eliminare il cluster DC/OS</span><span class="sxs-lookup"><span data-stu-id="5241a-151">Delete DC/OS cluster</span></span>

<span data-ttu-id="5241a-152">Quando non serve più, è possibile rimuovere il gruppo di risorse, il cluster DC/OS e tutte le risorse correlate tramite il comando [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="5241a-152">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, DC/OS cluster, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a><span data-ttu-id="5241a-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5241a-153">Next steps</span></span>

<span data-ttu-id="5241a-154">In questa guida rapida è stato distribuito un cluster DC/OS ed è stato eseguito un contenitore Docker semplice nel cluster.</span><span class="sxs-lookup"><span data-stu-id="5241a-154">In this quick start, you’ve deployed a DC/OS cluster and have run a simple Docker container on the cluster.</span></span> <span data-ttu-id="5241a-155">Per altre informazioni sul servizio contenitore di Azure, continuare con le esercitazioni relative a questo servizio.</span><span class="sxs-lookup"><span data-stu-id="5241a-155">To learn more about Azure Container Service, continue to the ACS tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5241a-156">Gestire un cluster DC/OS del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="5241a-156">Manage an ACS DC/OS Cluster</span></span>](container-service-dcos-manage-tutorial.md)