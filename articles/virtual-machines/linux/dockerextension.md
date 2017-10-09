---
title: hello aaaUse estensione della macchina virtuale Docker di Azure | Documenti Microsoft
description: Informazioni su come toouse hello tooquickly estensione Docker VM e in modo sicuro distribuisce un ambiente di Docker in Azure utilizzando i modelli di gestione risorse e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="7472e-103">Creare un ambiente di Docker in Azure utilizzando l'estensione della macchina virtuale Docker hello</span><span class="sxs-lookup"><span data-stu-id="7472e-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="7472e-104">Docker è una gestione dei contenitori più diffusi e imaging piattaforma che consente di utilizzare tooquickly contenitori in Linux.</span><span class="sxs-lookup"><span data-stu-id="7472e-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="7472e-105">In Azure, esistono diversi modi per distribuire Docker in base alle esigenze tooyour.</span><span class="sxs-lookup"><span data-stu-id="7472e-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="7472e-106">Questo articolo è incentrato sull'uso di estensione della macchina virtuale Docker hello e modelli di gestione risorse di Azure con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="7472e-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="7472e-107">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7472e-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="7472e-108">Panoramica dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="7472e-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="7472e-109">estensione della macchina virtuale Docker di Azure Hello installa e configura il daemon di Docker hello client Docker e Docker Compose nella macchina virtuale Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="7472e-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="7472e-110">Tramite l'estensione della macchina virtuale Docker di Azure hello, si dispone di più controllo e funzionalità rispetto a semplicemente tramite Docker macchina o la creazione di host Docker hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="7472e-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="7472e-111">Queste ulteriori funzionalità, ad esempio [Docker Compose](https://docs.docker.com/compose/overview/), assicurarsi di estensione della macchina virtuale Docker di Azure hello adatto per ambienti di sviluppo o di produzione più affidabili.</span><span class="sxs-lookup"><span data-stu-id="7472e-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="7472e-112">Per ulteriori informazioni sui metodi di distribuzione diversi hello, incluso l'utilizzo di Docker computer e servizi di contenitore di Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="7472e-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="7472e-113">prototipo tooquickly un'app, è possibile creare un singolo host Docker usando [Docker macchina](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="7472e-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="7472e-114">toobuild ambiente di produzione, scalabile ambienti che forniscono gli strumenti di pianificazione e di gestione aggiuntivi, è possibile distribuire un [Docker Swarm cluster in servizi di Azure contenitore](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7472e-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="7472e-115">Distribuire un modello con hello estensione della macchina virtuale Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="7472e-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="7472e-116">Si utilizza un toocreate di modello di avvio rapido una VM Ubuntu che utilizza tooinstall estensione di macchina virtuale Docker di Azure hello esistente e configurare host Docker hello.</span><span class="sxs-lookup"><span data-stu-id="7472e-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="7472e-117">È possibile visualizzare qui modello hello: [distribuzione semplice di una VM Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="7472e-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="7472e-118">È necessario più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7472e-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="7472e-119">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7472e-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7472e-120">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso:</span><span class="sxs-lookup"><span data-stu-id="7472e-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="7472e-121">Successivamente, distribuire una macchina virtuale con [distribuzione gruppo az creare](/cli/azure/group/deployment#create) che include l'estensione della macchina virtuale Docker di Azure hello da [questo modello di gestione risorse di Azure su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="7472e-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="7472e-122">Specificare i propri valori per *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP* come segue:</span><span class="sxs-lookup"><span data-stu-id="7472e-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="7472e-123">Sono necessari alcuni minuti per hello toofinish di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7472e-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="7472e-124">Una volta terminata la distribuzione di hello, [Sposta passaggio toonext](#deploy-your-first-nginx-container) tooSSH tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7472e-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="7472e-125">Facoltativamente, prompt dei comandi di tooinstead controllo restituito toohello e distribuzione hello let continuano in background hello, aggiungere hello `--no-wait` flag toohello precedente comando.</span><span class="sxs-lookup"><span data-stu-id="7472e-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="7472e-126">Questo processo consente tooperform altre operazioni in hello CLI mentre hello distribuzione continua per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="7472e-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="7472e-127">È quindi possibile visualizzare i dettagli sullo stato dell'host Docker hello con [Mostra vm az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="7472e-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="7472e-128">esempio Hello Controlla stato hello della macchina virtuale denominata hello *myDockerVM* (nome predefinito dal modello hello hello, non modificare questo nome) nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="7472e-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="7472e-129">Quando questo comando restituisce *Succeeded*, distribuzione hello è terminata ed è possibile SSH toohello VM in hello riportata dopo il passaggio.</span><span class="sxs-lookup"><span data-stu-id="7472e-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="7472e-130">Distribuire il primo contenitore nginx</span><span class="sxs-lookup"><span data-stu-id="7472e-130">Deploy your first nginx container</span></span>
<span data-ttu-id="7472e-131">Dettagli tooview della macchina virtuale, incluso il nome DNS hello, utilizzano `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="7472e-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="7472e-132">SSH tooyour Docker nuovo host dal computer locale come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7472e-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="7472e-133">Una volta effettuato l'accesso toohello host Docker, eseguire un contenitore nginx:</span><span class="sxs-lookup"><span data-stu-id="7472e-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="7472e-134">output di Hello è simile toohello seguente esempio come hello nginx immagine viene scaricata e un contenitore di avvio:</span><span class="sxs-lookup"><span data-stu-id="7472e-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="7472e-135">Controllare lo stato di hello di contenitori di hello in esecuzione sull'host Docker come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="7472e-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="7472e-136">output di Hello è simile toohello esempio seguente, che mostra che il contenitore nginx hello sia in esecuzione e le porte TCP 80 e 443 e inoltrati:</span><span class="sxs-lookup"><span data-stu-id="7472e-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="7472e-137">Aprire il contenitore in azione, toosee fino a un web browser e immettere il nome DNS hello dell'host Docker:</span><span class="sxs-lookup"><span data-stu-id="7472e-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Esecuzione di un contenitore ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="7472e-139">Riferimento al modello dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="7472e-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="7472e-140">Hello esempio precedente Usa un modello di avvio rapido esistente.</span><span class="sxs-lookup"><span data-stu-id="7472e-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="7472e-141">È inoltre possibile distribuire l'estensione della macchina virtuale Docker di Azure hello con i propri modelli di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="7472e-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="7472e-142">toodo in tal caso, aggiungere hello seguenti modelli di gestione risorse tooyour, la definizione di hello `vmName` della macchina virtuale in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="7472e-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="7472e-143">Per altre procedure dettagliate relative all'uso di modelli di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7472e-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7472e-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7472e-144">Next steps</span></span>
<span data-ttu-id="7472e-145">Potrebbe essere troppo[configurare la porta TCP di daemon Docker hello](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendere [sicurezza Docker](https://docs.docker.com/engine/security/security/), o distribuire contenitori usando [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="7472e-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="7472e-146">Per ulteriori informazioni sull'estensione della macchina virtuale Docker Azure stesso hello, vedere hello [GitHub progetto](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="7472e-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="7472e-147">Altre informazioni hello aggiuntive Docker opzioni di distribuzione in Azure:</span><span class="sxs-lookup"><span data-stu-id="7472e-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="7472e-148">Utilizzare computer Docker con hello Azure driver</span><span class="sxs-lookup"><span data-stu-id="7472e-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="7472e-149">[Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="7472e-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="7472e-150">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="7472e-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

