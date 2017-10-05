---
title: Usare l'estensione di VM Docker di Azure | Documentazione Microsoft
description: Informazioni su come usare l'estensione di VM Docker per distribuire in modo rapido e sicuro un ambiente Docker in Azure con i modelli di Resource Manager e l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="ab8ae-103">Creare un ambiente Docker in Azure usando l'estensione di VM Docker</span><span class="sxs-lookup"><span data-stu-id="ab8ae-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="ab8ae-104">Docker è una nota piattaforma di creazione dell'immagine e gestione di contenitori che consente di lavorare rapidamente con contenitori in Linux.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="ab8ae-105">L'ambiente Azure offre vari modi per distribuire Docker a seconda delle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="ab8ae-106">Questo articolo è incentrato sull'uso dell'estensione di VM Docker e dei modelli di Azure Resource Manager con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="ab8ae-107">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="ab8ae-108">Panoramica dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="ab8ae-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="ab8ae-109">L'estensione di VM Docker di Azure installa e configura il daemon Docker, il client Docker e Docker Compose nella macchina virtuale (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="ab8ae-110">L'uso dell'estensione di VM Docker di Azure permette di ottenere un livello di controllo superiore e un maggior numero di funzionalità rispetto a quanto offerto dal semplice uso di Docker Machine o dalla creazione di un host Docker.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="ab8ae-111">Questi funzionalità aggiuntive, come ad esempio [Docker Compose](https://docs.docker.com/compose/overview/), rendono l'estensione di VM Docker di Azure la soluzione ideale per ambienti di sviluppo o di produzione più solidi.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="ab8ae-112">Per altre informazioni sui diversi metodi di distribuzione, incluso l'uso di Docker Machine e i servizi contenitore di Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="ab8ae-113">Per creare rapidamente il prototipo di un'applicazione, è possibile creare un singolo host di Docker usando [Docker Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="ab8ae-114">Per creare ambienti scalabili e pronti per la produzione che offrono maggiori strumenti di pianificazione e gestione, è possibile distribuire un [cluster Docker Swarm nei servizi contenitore di Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="ab8ae-115">Distribuire un modello con l'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="ab8ae-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="ab8ae-116">Usare un modello di avvio rapido esistente per creare una macchina virtuale Ubuntu che usa l'estensione di VM Docker di Azure per installare e configurare l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="ab8ae-117">Per visualizzare il modello, vedere [Distribuzione semplice di una VM Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="ab8ae-118">È necessario aver installato l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ab8ae-119">Creare prima un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ab8ae-120">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *westus*:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="ab8ae-121">Successivamente, distribuire una macchina virtuale con il comando [az group deployment create](/cli/azure/group/deployment#create) che include l'estensione di VM Docker di Azure da [questo modello di Azure Resource Manager su GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="ab8ae-122">Specificare i propri valori per *newStorageAccountName*, *adminUsername*, *adminPassword* e *dnsNameForPublicIP* come segue:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="ab8ae-123">L'operazione di distribuzione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="ab8ae-124">Al termine della distribuzione, [procedere al passaggio successivo](#deploy-your-first-nginx-container) per configurare SSH sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="ab8ae-125">Facoltativamente, per restituire il controllo al prompt e per consentire la distribuzione continua in background, aggiungere il flag `--no-wait` al comando precedente.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="ab8ae-126">Questo processo consente di eseguire altre operazioni nell'interfaccia della riga di comando mentre la distribuzione continua per alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="ab8ae-127">È possibile visualizzare i dettagli sullo stato dell'host Docker con il comando [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="ab8ae-128">L'esempio seguente controlla lo stato della macchina virtuale denominata *myDockerVM* (il nome predefinito del modello, non modificare questo nome) che appartiene al gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="ab8ae-129">Quando questo comando restituisce *Succeeded*, la distribuzione è stata completata ed è possibile configurare SSH sulla macchina virtuale nel passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="ab8ae-130">Distribuire il primo contenitore nginx</span><span class="sxs-lookup"><span data-stu-id="ab8ae-130">Deploy your first nginx container</span></span>
<span data-ttu-id="ab8ae-131">Per visualizzare i dettagli della VM, incluso il nome DNS, usare `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="ab8ae-132">Accedere tramite SSH al nuovo host Docker dal computer locale, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="ab8ae-133">Dopo aver effettuato l'accesso all'host Docker, eseguire un contenitore nginx:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="ab8ae-134">L'output è simile all'esempio seguente quando l'immagine nginx viene scaricata e un contenitore viene avviato:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="ab8ae-135">Per controllare lo stato dei contenitori in esecuzione sull'host Docker, fare come segue:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="ab8ae-136">L'output è simile all'esempio seguente, in cui viene mostrato che il contenitore nginx è in esecuzione e viene eseguito l'inoltro alle porte TCP 80 e 443:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="ab8ae-137">Per vedere il contenitore in azione, aprire un Web browser e immettere il nome DNS dell'host Docker:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![Esecuzione di un contenitore ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="ab8ae-139">Riferimento al modello dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="ab8ae-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="ab8ae-140">Nell'esempio precedente è stato usato un modello di avvio rapido esistente.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="ab8ae-141">È anche possibile distribuire l'estensione di VM Docker di Azure con i propri modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ab8ae-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="ab8ae-142">Per farlo, aggiungere quanto segue ai modello di Resource Manager, definendo in modo appropriato `vmName` della VM:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="ab8ae-143">Per altre procedure dettagliate relative all'uso di modelli di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab8ae-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ab8ae-144">Next steps</span></span>
<span data-ttu-id="ab8ae-145">Se lo si desidera, [configurare la porta TCP del daemon Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendere le [informazioni di sicurezza di Docker](https://docs.docker.com/engine/security/security/) oppure distribuire i contenitori con [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="ab8ae-146">Per altre informazioni sull'estensione di VM Docker di Azure, vedere il [Progetto GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="ab8ae-147">Per altre informazioni sulle opzioni di distribuzione di Docker aggiuntive in Azure, leggere:</span><span class="sxs-lookup"><span data-stu-id="ab8ae-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="ab8ae-148">Usare Docker Machine con il driver di Azure</span><span class="sxs-lookup"><span data-stu-id="ab8ae-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="ab8ae-149">[Introduzione a Docker e Compose per definire ed eseguire un'applicazione multi-contenitore in una macchina virtuale di Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="ab8ae-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="ab8ae-150">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="ab8ae-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

