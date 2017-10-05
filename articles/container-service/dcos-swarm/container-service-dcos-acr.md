---
title: Uso di Registro contenitori di Azure (ACR) con un cluster DC/OS | Microsoft Docs
description: Usare Registro contenitori di Azure con un cluster DC/OS nel servizio contenitore di Azure
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, contenitori, micro-servizi, Mesos, Azure, FileShare, CIFS
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 618d32ca919e50d41b85c800225fe72c3b94e537
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="eaa1f-104">Usare Registro contenitori di Azure (ACR) con un cluster DC/OS per distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="eaa1f-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="eaa1f-105">In questo articolo viene illustrato l'uso del Registro contenitori di Azure con un cluster del controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-105">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="eaa1f-106">L'uso del record di controllo di accesso consente di archiviare privatamente e di gestire le immagini del contenitore.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-106">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="eaa1f-107">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="eaa1f-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eaa1f-108">Distribuire il Registro contenitori di Azure (se necessario)</span><span class="sxs-lookup"><span data-stu-id="eaa1f-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="eaa1f-109">Configurare l'autenticazione del record di controllo di accesso in un cluster del controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="eaa1f-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="eaa1f-110">Caricare un'immagine nel Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="eaa1f-110">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="eaa1f-111">Eseguire un'immagine del contenitore dal Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="eaa1f-111">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="eaa1f-112">È necessario un cluster del controller di dominio/sistema operativo del servizio contenitore di Azure per completare i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="eaa1f-113">Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="eaa1f-114">Questa esercitazione richiede l'interfaccia della riga di comando di Azure 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eaa1f-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="eaa1f-116">Se è necessario eseguire l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eaa1f-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="eaa1f-117">Distribuire il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="eaa1f-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="eaa1f-118">Se necessario, creare un Registro contenitori di Azure con il comando [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="eaa1f-118">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="eaa1f-119">Nell'esempio seguente viene creato un registro con un nome generato in modo casuale.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-119">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="eaa1f-120">Il registro viene anche configurato con un account amministratore tramite l'argomento `--admin-enabled`.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-120">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="eaa1f-121">Dopo la creazione del registro, l'interfaccia della riga di comando di Azure restituisce dati simili ai seguenti.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-121">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="eaa1f-122">Annotare `name` e `loginServer`, che verranno usati nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-122">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="eaa1f-123">Ottenere le credenziali del registro contenitori tramite il comando [az acr credential show](/cli/azure/acr/credential).</span><span class="sxs-lookup"><span data-stu-id="eaa1f-123">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="eaa1f-124">Sostituire `--name` con il valore annotato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-124">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="eaa1f-125">Prendere nota di una password, che sarà necessaria in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="eaa1f-126">Per altre informazioni sul Registro contenitori di Azure, vedere [Introduzione ai registri per contenitori Docker privati](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="eaa1f-126">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="eaa1f-127">Gestire l'autenticazione del record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="eaa1f-127">Manage ACR authentication</span></span>

<span data-ttu-id="eaa1f-128">Il modo convenzionale per effettuare il push e il pull di un'immagine da un registro privato consiste nell'eseguire prima l'autenticazione con il registro.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-128">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="eaa1f-129">A tale scopo, usare il `docker login` comando in qualsiasi client che richieda l'accesso al registro privato.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-129">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="eaa1f-130">Poiché un cluster di controller di dominio/sistema operativo può contenere molti nodi, ognuno dei quali deve essere autenticato con il record di controllo di accesso, è utile automatizzare questo processo in ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-130">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="eaa1f-131">Creare uno spazio di archiviazione condiviso</span><span class="sxs-lookup"><span data-stu-id="eaa1f-131">Create shared storage</span></span>

<span data-ttu-id="eaa1f-132">Questo processo usa una condivisione di file di Azure che è stata montata in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-132">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="eaa1f-133">Se non è già stato impostato lo spazio di archiviazione condiviso, vedere [Creare e montare una condivisione di file per un cluster DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="eaa1f-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="eaa1f-134">Configurare l'autenticazione del record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="eaa1f-134">Configure ACR authentication</span></span>

<span data-ttu-id="eaa1f-135">Innanzitutto, ottenere il nome di dominio completo del master del controller di dominio/sistema operativo e archiviarlo in una variabile.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-135">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="eaa1f-136">Creare un collegamento SSH con il master (o il primo master) del cluster basato su controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-136">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="eaa1f-137">Aggiornare il nome utente se è stato usato un valore non predefinito al momento della creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-137">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="eaa1f-138">Eseguire il comando seguente per l'accesso al Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-138">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="eaa1f-139">Sostituire `--username` con il nome del registro contenitori e `--password` con una delle password fornite.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-139">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="eaa1f-140">Sostituire l'ultimo argomento *mycontainerregistry.azurecr.io* nell'esempio con il nome loginServer del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-140">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="eaa1f-141">Questo comando archivia i valori di autenticazione in locale nel percorso `~/.docker`.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-141">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="eaa1f-142">Creare un file compresso che contenga i valori di autenticazione del registro contenitori.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-142">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="eaa1f-143">Copiare questo file nello spazio di archiviazione condiviso del cluster.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-143">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="eaa1f-144">Questo passaggio rende il file disponibile in tutti i nodi del cluster del controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-144">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="eaa1f-145">Caricare un'immagine nel record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="eaa1f-145">Upload image to ACR</span></span>

<span data-ttu-id="eaa1f-146">A questo punto, da un computer di sviluppo o da qualsiasi altro sistema con Docker installato, creare un'immagine e caricarla nel Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-146">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="eaa1f-147">Creare un contenitore dall'immagine Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-147">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="eaa1f-148">Ora è possibile acquisire il contenitore in una nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-148">Now capture the container into a new image.</span></span> <span data-ttu-id="eaa1f-149">È necessario che l'immagine includa il nome `loginServer` del registro contenitori nel formato `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-149">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="eaa1f-150">Accedere al Registro contenitori di Azure.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-150">Login into the Azure Container Registry.</span></span> <span data-ttu-id="eaa1f-151">Sostituire il nome con il nome loginServer, --username con il nome del registro contenitori, e -- password con una delle password fornite.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-151">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="eaa1f-152">Infine, caricare l'immagine nel registro dei record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-152">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="eaa1f-153">In questo esempio si carica un'immagine denominata dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="eaa1f-154">Eseguire un'immagine dal record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="eaa1f-154">Run an image from ACR</span></span>

<span data-ttu-id="eaa1f-155">Per usare un'immagine dal registro dei record di controllo di accesso, creare il nome del file *acrDemo.json* e copiarvi il seguente testo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-155">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="eaa1f-156">Sostituire il nome dell'immagine con il nome del registro contenitori loginServer e il nome dell'immagine, ad esempio `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-156">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="eaa1f-157">Annotare la proprietà `uris`.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-157">Take note of the `uris` property.</span></span> <span data-ttu-id="eaa1f-158">Questa proprietà contiene la posizione del file di autenticazione del registro contenitori, che in questo caso corrisponde alla condivisione del file di Azure che è montato in ogni nodo del cluster del controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-158">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="eaa1f-159">Distribuire l'applicazione con l'interfaccia della riga di comando del controller di dominio/sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="eaa1f-159">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="eaa1f-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eaa1f-160">Next steps</span></span>

<span data-ttu-id="eaa1f-161">In questa esercitazione è necessario configurare il controller di dominio/sistema operativo per usare il Registro contenitori di Azure che comprende le seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="eaa1f-161">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eaa1f-162">Distribuire il Registro contenitori di Azure (se necessario)</span><span class="sxs-lookup"><span data-stu-id="eaa1f-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="eaa1f-163">Configurare l'autenticazione del record di controllo di accesso in un cluster del controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="eaa1f-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="eaa1f-164">Caricare un'immagine nel Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="eaa1f-164">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="eaa1f-165">Eseguire un'immagine del contenitore dal Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="eaa1f-165">Run a container image from the Azure Container Registry</span></span>
