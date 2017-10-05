---
title: Usare l'estensione di macchina virtuale Docker in Azure con l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come usare l'estensione di VM Docker per distribuire in modo rapido e sicuro un ambiente Docker in Azure con i modelli di Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: a3cbcf63533f4042dcd695e141655c5814bd7068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension-with-the-azure-cli-10"></a><span data-ttu-id="d7cc8-103">Creare un ambiente Docker in Azure usando l'estensione di macchina virtuale Docker con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d7cc8-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="d7cc8-104">Docker è una nota piattaforma di creazione dell'immagine e gestione di contenitori che consente di lavorare rapidamente con contenitori in Linux (e anche Windows).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="d7cc8-105">L'ambiente Azure offre vari modi per distribuire Docker a seconda delle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="d7cc8-106">Questo articolo si concentra sull'uso dell'estensione di VM Docker e dei modelli di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="d7cc8-107">Per altre informazioni sui diversi metodi di distribuzione, incluso l'uso di Docker Machine e i servizi contenitore di Azure, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="d7cc8-108">Per creare rapidamente il prototipo di un'applicazione, è possibile creare un singolo host di Docker usando [Docker Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="d7cc8-109">Per gli ambienti più stabili ed estesi è possibile usare l'estensione di VM Docker di Azure che supporta anche [Docker Compose](https://docs.docker.com/compose/overview/) per generare distribuzioni di contenitore coerenti.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span></span> <span data-ttu-id="d7cc8-110">Questo articolo descrive come usare l'estensione di VM Docker di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-110">This article details using the Azure Docker VM extension.</span></span>
* <span data-ttu-id="d7cc8-111">Per creare ambienti scalabili e pronti per la produzione che offrono maggiori strumenti di pianificazione e gestione, è possibile distribuire un [cluster Docker Swarm nei servizi contenitore di Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d7cc8-112">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="d7cc8-112">CLI versions to complete the task</span></span>
<span data-ttu-id="d7cc8-113">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="d7cc8-114">[Interfaccia della riga di comando di Azure 1.0](#azure-docker-vm-extension-overview): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="d7cc8-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d7cc8-115">[Interfaccia della riga di comando di Azure 2.0](dockerextension.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="d7cc8-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for the resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="d7cc8-116">Panoramica dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="d7cc8-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="d7cc8-117">L'estensione di VM Docker di Azure installa e configura il daemon Docker, il client Docker e Docker Compose nella macchina virtuale (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="d7cc8-118">L'uso dell'estensione di VM Docker di Azure permette di ottenere un livello di controllo superiore e un maggior numero di funzionalità rispetto a quanto offerto dal semplice uso di Docker Machine o dalla creazione di un host Docker.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="d7cc8-119">Questi funzionalità aggiuntive, come ad esempio [Docker Compose](https://docs.docker.com/compose/overview/), rendono l'estensione di VM Docker di Azure la soluzione ideale per ambienti di sviluppo o di produzione più solidi.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="d7cc8-120">I modelli di Azure Resource Manager definiscono l'intera struttura dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-120">Azure Resource Manager templates define the entire structure of your environment.</span></span> <span data-ttu-id="d7cc8-121">I modelli consentono di creare e configurare le risorse, ad esempio le VM dell'host Docker, l'archiviazione, i controlli degli accessi in base al ruolo (RBAC) e la diagnostica.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="d7cc8-122">È possibile riusare questi modelli per creare distribuzioni aggiuntive in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-122">You can reuse these templates to create additional deployments in a consistent manner.</span></span> <span data-ttu-id="d7cc8-123">Per altre informazioni su Azure Resource Manager e relativi modelli, vedere la [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="d7cc8-124">Distribuire un modello con l'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="d7cc8-124">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="d7cc8-125">Usare un modello di avvio rapido esistente per creare una macchina virtuale Ubuntu che usa l'estensione di VM Docker di Azure per installare e configurare l'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="d7cc8-126">Per visualizzare il modello, vedere [Distribuzione semplice di una VM Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="d7cc8-127">È necessario installare e registrare l'[interfaccia della riga di comando Azure più recente](../../cli-install-nodejs.md) usando la modalità di Resource Manager nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="d7cc8-128">Distribuire il modello con l'interfaccia della riga di comando di Azure, specificando l'URI del modello.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-128">Deploy the template using the Azure CLI, specifying the template URI.</span></span> <span data-ttu-id="d7cc8-129">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella posizione *westus*.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-129">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span> <span data-ttu-id="d7cc8-130">Usare il nome e la posizione del gruppo di risorse nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="d7cc8-131">Rispondere ai prompt di richiesta di rinominare l'account di archiviazione, fornire il nome utente e la password e specificare il nome DNS.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="d7cc8-132">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-132">The output is similar to the following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for the following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="d7cc8-133">L'interfaccia della riga di comando di Azure fa tornare l'utente al menu principale di prompt dopo alcuni secondi, ma l'host Docker viene comunque creato e configurato dall'estensione di VM Docker di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span></span> <span data-ttu-id="d7cc8-134">L'operazione di distribuzione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="d7cc8-135">È possibile visualizzare i dettagli sullo stato dell'host Docker con il comando `azure vm show`.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-135">You can view details about the Docker host status using the `azure vm show` command.</span></span>

<span data-ttu-id="d7cc8-136">L'esempio seguente controlla lo stato della macchina virtuale denominata *myDockerVM* (il nome predefinito del modello, non modificare questo nome) che appartiene al gruppo di risorse *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-136">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*.</span></span> <span data-ttu-id="d7cc8-137">Immettere il nome del gruppo di risorse creato nel passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="d7cc8-138">L'output del comando `azure vm show` sarà simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-138">The output of the `azure vm show` command is similar to the following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myDockerVM"
+ Looking up the NIC "myVMNicD"
+ Looking up the public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="d7cc8-139">Nella parte superiore dell'output viene visualizzato il valore **ProvisioningState** della VM.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-139">Near the top of the output, you see the **ProvisioningState** of the VM.</span></span> <span data-ttu-id="d7cc8-140">Quando viene visualizzato *Succeeded*, la distribuzione è stata completata ed è possibile usare SSH per la VM.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-140">When this displays *Succeeded*, the deployment has finished and you can SSH to the VM.</span></span>

<span data-ttu-id="d7cc8-141">Verso la fine dell'output, *FQDN* visualizza il nome di dominio completo dell'host Docker.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-141">Towards the end of the output, *FQDN* displays the fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="d7cc8-142">Questo è l'FQDN che si usa per accedere tramite SSH all'host Docker nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="d7cc8-143">Distribuire il primo contenitore nginx</span><span class="sxs-lookup"><span data-stu-id="d7cc8-143">Deploy your first nginx container</span></span>
<span data-ttu-id="d7cc8-144">Al termine della distribuzione, accedere tramite SSH al nuovo host Docker dal computer locale.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span></span> <span data-ttu-id="d7cc8-145">Immettere il nome utente e l'FQDN nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="d7cc8-146">Dopo aver effettuato l'accesso all'host Docker, eseguire un contenitore nginx:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-146">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="d7cc8-147">L'output è simile all'esempio seguente quando l'immagine nginx viene scaricata e un contenitore viene avviato:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="d7cc8-148">Per controllare lo stato dei contenitori in esecuzione sull'host Docker, fare come segue:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-148">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="d7cc8-149">L'output è simile all'esempio seguente, in cui viene mostrato che il contenitore nginx è in esecuzione e viene eseguito l'inoltro alle porte TCP 80 e 443:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="d7cc8-150">Per vedere il contenitore in azione, aprire un Web browser e immettere il nome FQDN dell'host Docker:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span></span>

![Esecuzione di un contenitore ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="d7cc8-152">Riferimento al modello dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="d7cc8-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="d7cc8-153">Nell'esempio precedente è stato usato un modello di avvio rapido esistente.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-153">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="d7cc8-154">È anche possibile distribuire l'estensione di VM Docker di Azure con i propri modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7cc8-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="d7cc8-155">Per questo scopo, aggiungere quanto segue ai modello di Resource Manager, definendo in modo appropriato il *vmName* della VM:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-155">To do so, add the following to your Resource Manager templates, defining the *vmName* of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="d7cc8-156">Per altre procedure dettagliate relative all'uso di modelli di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7cc8-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7cc8-157">Next steps</span></span>
<span data-ttu-id="d7cc8-158">Se lo si desidera, [configurare la porta TCP del daemon Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendere le [informazioni di sicurezza di Docker](https://docs.docker.com/engine/security/security/) oppure distribuire i contenitori con [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="d7cc8-159">Per altre informazioni sull'estensione di VM Docker di Azure, vedere il [Progetto GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="d7cc8-160">Per altre informazioni sulle opzioni di distribuzione di Docker aggiuntive in Azure, leggere:</span><span class="sxs-lookup"><span data-stu-id="d7cc8-160">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="d7cc8-161">Usare Docker Machine con il driver di Azure</span><span class="sxs-lookup"><span data-stu-id="d7cc8-161">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="d7cc8-162">[Introduzione a Docker e Compose per definire ed eseguire un'applicazione multi-contenitore in una macchina virtuale di Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="d7cc8-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="d7cc8-163">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="d7cc8-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

