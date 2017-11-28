---
title: aaaUsing record con un cluster di controller di dominio o sistema operativo di Azure | Documenti Microsoft
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
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="06611-104">Usare ACR con toodeploy di cluster un controller di dominio o del sistema operativo, l'applicazione</span><span class="sxs-lookup"><span data-stu-id="06611-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="06611-105">In questo articolo esamineremo come toouse del Registro di sistema di Azure contenitore con un cluster di controller di dominio o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="06611-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="06611-106">Utilizzando ACR consente tooprivately store e gestire le immagini contenitore.</span><span class="sxs-lookup"><span data-stu-id="06611-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="06611-107">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="06611-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="06611-108">Distribuire il Registro contenitori di Azure (se necessario)</span><span class="sxs-lookup"><span data-stu-id="06611-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="06611-109">Configurare l'autenticazione del record di controllo di accesso in un cluster del controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="06611-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="06611-110">Caricare un toohello immagine del Registro di sistema contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="06611-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="06611-111">Eseguire un'immagine contenitore da hello del Registro di sistema contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="06611-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="06611-112">È necessario un ACS controller di dominio o sistema operativo hello toocomplete cluster i passaggi in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="06611-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="06611-113">Se necessario, questo [script di esempio](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) può crearne uno appositamente.</span><span class="sxs-lookup"><span data-stu-id="06611-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="06611-114">Questa esercitazione richiede hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="06611-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="06611-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="06611-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="06611-116">Se è necessario tooupgrade, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="06611-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="06611-117">Distribuire il Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="06611-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="06611-118">Se necessario, creare un registro di sistema del contenitore di Azure con hello [az acr creare](/cli/azure/acr#create) comando.</span><span class="sxs-lookup"><span data-stu-id="06611-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="06611-119">esempio Hello crea un registro di sistema con un nome di generare in modo casuale.</span><span class="sxs-lookup"><span data-stu-id="06611-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="06611-120">Registro di sistema Hello viene inoltre configurato con un account di amministratore utilizzando hello `--admin-enabled` argomento.</span><span class="sxs-lookup"><span data-stu-id="06611-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="06611-121">Dopo aver creato il registro hello, hello CLI di Azure genera dati simili toohello successivi.</span><span class="sxs-lookup"><span data-stu-id="06611-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="06611-122">Prendere nota di hello `name` e `loginServer`, questi vengono utilizzati nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="06611-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

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

<span data-ttu-id="06611-123">Ottenere le credenziali del Registro di sistema di contenitore hello utilizzando hello [Mostra credenziale di az acr](/cli/azure/acr/credential) comando.</span><span class="sxs-lookup"><span data-stu-id="06611-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="06611-124">Hello Substitute `--name` con hello uno indicato nell'ultimo passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="06611-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="06611-125">Prendere nota di una password, che sarà necessaria in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="06611-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="06611-126">Per ulteriori informazioni sul Registro di sistema contenitore di Azure, vedere [registri contenitore Docker di introduzione tooprivate](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="06611-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="06611-127">Gestire l'autenticazione del record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="06611-127">Manage ACR authentication</span></span>

<span data-ttu-id="06611-128">metodo convenzionale per Hello immagine toopush e pull da un registro di sistema privato è toofirst l'autenticazione con il Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="06611-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="06611-129">toodo, è necessario utilizzare hello `docker login` comando in qualsiasi client necessarie del Registro di sistema di tooaccess hello privata.</span><span class="sxs-lookup"><span data-stu-id="06611-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="06611-130">Poiché un cluster di controller di dominio o del sistema operativo può contenere molti nodi, ognuno dei quali è necessario toobe autenticato con hello ACR, è utile tooautomate questo processo in ciascun nodo.</span><span class="sxs-lookup"><span data-stu-id="06611-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="06611-131">Creare uno spazio di archiviazione condiviso</span><span class="sxs-lookup"><span data-stu-id="06611-131">Create shared storage</span></span>

<span data-ttu-id="06611-132">Questo processo usa una condivisione di file di Azure che è stata montata in ogni nodo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="06611-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="06611-133">Se non è già stato impostato lo spazio di archiviazione condiviso, vedere [Creare e montare una condivisione di file per un cluster DC/OS](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="06611-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="06611-134">Configurare l'autenticazione del record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="06611-134">Configure ACR authentication</span></span>

<span data-ttu-id="06611-135">Innanzitutto, ottenere hello FQDN di hello DC/OS master e archiviarlo in una variabile.</span><span class="sxs-lookup"><span data-stu-id="06611-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="06611-136">Creare una connessione SSH con hello master (o master prima di hello) del cluster basato su controller di dominio/OS.</span><span class="sxs-lookup"><span data-stu-id="06611-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="06611-137">Aggiornare il nome utente hello se è stato utilizzato un valore non predefinito durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="06611-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="06611-138">Comando che segue di esecuzione hello toologin toohello del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="06611-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="06611-139">Sostituire hello `--username` con nome hello del Registro di sistema contenitore hello e hello `--password` con una delle password hello fornito.</span><span class="sxs-lookup"><span data-stu-id="06611-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="06611-140">Sostituire l'ultimo argomento hello *mycontainerregistry.azurecr.io* nell'esempio hello con nome loginServer hello del Registro di sistema di hello contenitore.</span><span class="sxs-lookup"><span data-stu-id="06611-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="06611-141">Questo comando Archivia i valori di autenticazione hello localmente in hello `~/.docker` percorso.</span><span class="sxs-lookup"><span data-stu-id="06611-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="06611-142">Creare un file compresso che contiene i valori di autenticazione hello contenitore del Registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="06611-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="06611-143">Copiare questa risorsa di archiviazione di file toohello condiviso del cluster.</span><span class="sxs-lookup"><span data-stu-id="06611-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="06611-144">Questo passaggio rende disponibili in tutti i nodi del cluster di controller di dominio/OS hello file hello.</span><span class="sxs-lookup"><span data-stu-id="06611-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="06611-145">Caricare l'immagine tooACR</span><span class="sxs-lookup"><span data-stu-id="06611-145">Upload image tooACR</span></span>

<span data-ttu-id="06611-146">Ora da un computer di sviluppo, o qualsiasi altro sistema con Docker installato, creare un'immagine e caricarlo toohello del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="06611-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="06611-147">Creare un contenitore dall'immagine Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="06611-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="06611-148">Ora l'acquisizione hello contenitore in una nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="06611-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="06611-149">nome dell'immagine Hello deve hello tooinclude `loginServer` nome di hello contenitore registrywith un formato di `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="06611-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="06611-150">Account di accesso in hello del Registro di sistema contenitore di Azure.</span><span class="sxs-lookup"><span data-stu-id="06611-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="06611-151">Sostituire hello con nome loginServer hello, hello - nome utente con nome hello del Registro di sistema contenitore hello e hello - password con una delle password hello fornito.</span><span class="sxs-lookup"><span data-stu-id="06611-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="06611-152">Infine, caricare del Registro di sistema di hello immagine toohello record.</span><span class="sxs-lookup"><span data-stu-id="06611-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="06611-153">In questo esempio si carica un'immagine denominata dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="06611-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="06611-154">Eseguire un'immagine dal record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="06611-154">Run an image from ACR</span></span>

<span data-ttu-id="06611-155">toouse un'immagine dal Registro di sistema ACR hello, creare un file di nomi *acrDemo.json* e hello copia seguente testo al suo interno.</span><span class="sxs-lookup"><span data-stu-id="06611-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="06611-156">Sostituire il nome di immagine hello con hello contenitore del Registro di sistema loginServer nome e il nome dell'immagine, ad esempio `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="06611-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="06611-157">Prendere nota di hello `uris` proprietà.</span><span class="sxs-lookup"><span data-stu-id="06611-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="06611-158">Questa proprietà contiene hello percorso file hello contenitore del Registro di sistema l'autenticazione, ovvero in questo caso condivisione di file di Azure hello montato in ogni nodo nel cluster di controller di dominio/OS hello.</span><span class="sxs-lookup"><span data-stu-id="06611-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

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

<span data-ttu-id="06611-159">Distribuire un'applicazione hello con hello CLI DC / ° c.</span><span class="sxs-lookup"><span data-stu-id="06611-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="06611-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06611-160">Next steps</span></span>

<span data-ttu-id="06611-161">In questa esercitazione sono configuri toouse controller di dominio o del sistema operativo Azure contenitore Registro di sistema inclusi hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="06611-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="06611-162">Distribuire il Registro contenitori di Azure (se necessario)</span><span class="sxs-lookup"><span data-stu-id="06611-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="06611-163">Configurare l'autenticazione del record di controllo di accesso in un cluster del controller di dominio/sistema operativo</span><span class="sxs-lookup"><span data-stu-id="06611-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="06611-164">Caricare un toohello immagine del Registro di sistema contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="06611-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="06611-165">Eseguire un'immagine contenitore da hello del Registro di sistema contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="06611-165">Run a container image from hello Azure Container Registry</span></span>
