---
title: hello aaaUse estensione della macchina virtuale Docker di Azure con hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come toouse hello tooquickly estensione VM Docker e distribuire in modo sicuro un ambiente di Docker in Azure utilizzando i modelli di gestione risorse.
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
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="247f8-103">Creare un ambiente di Docker in Azure utilizzando l'estensione della macchina virtuale Docker hello con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="247f8-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="247f8-104">Docker è una gestione dei contenitori più diffusi e immagini piattaforma che consente di utilizzare tooquickly contenitori in Linux (e anche Windows).</span><span class="sxs-lookup"><span data-stu-id="247f8-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="247f8-105">In Azure, esistono diversi modi per distribuire Docker in base alle esigenze tooyour.</span><span class="sxs-lookup"><span data-stu-id="247f8-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="247f8-106">In questo articolo è incentrato sull'uso di estensione della macchina virtuale Docker hello e modelli di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="247f8-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="247f8-107">Per ulteriori informazioni sui metodi di distribuzione diversi hello, incluso l'utilizzo di Docker computer e servizi di contenitore di Azure, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="247f8-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="247f8-108">prototipo tooquickly un'app, è possibile creare un singolo host Docker usando [Docker macchina](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="247f8-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="247f8-109">Per gli ambienti più grandi e più stabili, è possibile utilizzare l'estensione della macchina virtuale Docker di Azure hello, che supporta inoltre [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate le distribuzioni di contenitore coerente.</span><span class="sxs-lookup"><span data-stu-id="247f8-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="247f8-110">Questo articolo presenta utilizzando l'estensione della macchina virtuale Docker di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="247f8-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="247f8-111">toobuild ambiente di produzione, scalabile ambienti che forniscono gli strumenti di pianificazione e di gestione aggiuntivi, è possibile distribuire un [Docker Swarm cluster in servizi di Azure contenitore](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="247f8-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="247f8-112">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="247f8-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="247f8-113">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="247f8-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="247f8-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="247f8-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="247f8-115">[Azure CLI 2.0](dockerextension.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="247f8-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="247f8-116">Panoramica dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="247f8-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="247f8-117">estensione della macchina virtuale Docker di Azure Hello installa e configura il daemon di Docker hello client Docker e Docker Compose nella macchina virtuale Linux (VM).</span><span class="sxs-lookup"><span data-stu-id="247f8-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="247f8-118">Tramite l'estensione della macchina virtuale Docker di Azure hello, si dispone di più controllo e funzionalità rispetto a semplicemente tramite Docker macchina o la creazione di host Docker hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="247f8-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="247f8-119">Queste ulteriori funzionalità, ad esempio [Docker Compose](https://docs.docker.com/compose/overview/), assicurarsi di estensione della macchina virtuale Docker di Azure hello adatto per ambienti di sviluppo o di produzione più affidabili.</span><span class="sxs-lookup"><span data-stu-id="247f8-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="247f8-120">Modelli di gestione risorse di Azure definiscono l'intera struttura di hello dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="247f8-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="247f8-121">I modelli consentono di toocreate e configurare le risorse, ad esempio host Docker hello macchine virtuali, archiviazione, i controlli di accesso basato sui ruoli (RBAC) e diagnostica.</span><span class="sxs-lookup"><span data-stu-id="247f8-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="247f8-122">È possibile riutilizzare le distribuzioni di modelli toocreate aggiuntive in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="247f8-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="247f8-123">Per altre informazioni su Azure Resource Manager e relativi modelli, vedere la [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="247f8-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="247f8-124">Distribuire un modello con hello estensione della macchina virtuale Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="247f8-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="247f8-125">Si utilizza un toocreate di modello di avvio rapido una VM Ubuntu che utilizza tooinstall estensione di macchina virtuale Docker di Azure hello esistente e configurare host Docker hello.</span><span class="sxs-lookup"><span data-stu-id="247f8-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="247f8-126">È possibile visualizzare qui modello hello: [distribuzione semplice di una VM Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="247f8-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="247f8-127">È necessario hello [CLI di Azure più recenti](../../cli-install-nodejs.md) installato e registrato con modalità di gestione risorse di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="247f8-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="247f8-128">Distribuire il modello di hello utilizzando hello CLI di Azure, specificare il modello di hello URI.</span><span class="sxs-lookup"><span data-stu-id="247f8-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="247f8-129">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *westus* percorso.</span><span class="sxs-lookup"><span data-stu-id="247f8-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="247f8-130">Usare il nome e la posizione del gruppo di risorse nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="247f8-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="247f8-131">Risposte hello richieste tooname account di archiviazione, fornire un nome utente e una password e specificare un nome DNS.</span><span class="sxs-lookup"><span data-stu-id="247f8-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="247f8-132">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="247f8-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="247f8-133">Hello CLI di Azure restituisce toohello prompt dopo pochi secondi, ma l'host Docker ancora viene creato e configurato da hello estensione della macchina virtuale Docker di Azure.</span><span class="sxs-lookup"><span data-stu-id="247f8-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="247f8-134">Sono necessari alcuni minuti per hello toofinish di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="247f8-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="247f8-135">È possibile visualizzare i dettagli sullo stato dell'host Docker hello utilizzando hello `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="247f8-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="247f8-136">esempio Hello Controlla stato hello della macchina virtuale denominata hello *myDockerVM* (nome predefinito dal modello hello hello, non modificare questo nome) nel gruppo di risorse hello denominato *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="247f8-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="247f8-137">Immettere il nome di hello hello del gruppo di risorse creato nel passaggio precedente hello:</span><span class="sxs-lookup"><span data-stu-id="247f8-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="247f8-138">output di hello Hello `azure vm show` è simile toohello seguente esempio di comando:</span><span class="sxs-lookup"><span data-stu-id="247f8-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
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

<span data-ttu-id="247f8-139">Parte superiore di hello di output di hello, vedrai hello **ProvisioningState** di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="247f8-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="247f8-140">Quando si visualizza *Succeeded*, distribuzione hello è terminata ed è possibile SSH toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="247f8-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="247f8-141">Verso la fine hello dell'output di hello, *FQDN* Visualizza hello nome di dominio completo dell'host Docker.</span><span class="sxs-lookup"><span data-stu-id="247f8-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="247f8-142">Questo nome di dominio completo è ciò che si usa tooSSH tooyour Docker host hello rimanenti passaggi.</span><span class="sxs-lookup"><span data-stu-id="247f8-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="247f8-143">Distribuire il primo contenitore nginx</span><span class="sxs-lookup"><span data-stu-id="247f8-143">Deploy your first nginx container</span></span>
<span data-ttu-id="247f8-144">Una volta distribuzione hello è stata completata, SSH tooyour nuovo host Docker da un computer locale.</span><span class="sxs-lookup"><span data-stu-id="247f8-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="247f8-145">Immettere il nome utente e l'FQDN nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="247f8-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="247f8-146">Una volta effettuato l'accesso toohello host Docker, eseguire un contenitore nginx:</span><span class="sxs-lookup"><span data-stu-id="247f8-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="247f8-147">output di Hello è simile toohello seguente esempio come hello nginx immagine viene scaricata e un contenitore di avvio:</span><span class="sxs-lookup"><span data-stu-id="247f8-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="247f8-148">Controllare lo stato di hello di contenitori di hello in esecuzione sull'host Docker come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="247f8-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="247f8-149">output di Hello è simile toohello esempio seguente, che mostra che il contenitore nginx hello sia in esecuzione e le porte TCP 80 e 443 e inoltrati:</span><span class="sxs-lookup"><span data-stu-id="247f8-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="247f8-150">Aprire il contenitore in azione, toosee fino a un web browser e immettere il nome FQDN hello dell'host Docker:</span><span class="sxs-lookup"><span data-stu-id="247f8-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Esecuzione di un contenitore ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="247f8-152">Riferimento al modello dell'estensione di VM Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="247f8-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="247f8-153">Hello esempio precedente Usa un modello di avvio rapido esistente.</span><span class="sxs-lookup"><span data-stu-id="247f8-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="247f8-154">È inoltre possibile distribuire l'estensione della macchina virtuale Docker di Azure hello con i propri modelli di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="247f8-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="247f8-155">toodo in tal caso, aggiungere hello seguenti modelli di gestione risorse tooyour, la definizione di hello *vmName* della macchina virtuale in modo appropriato:</span><span class="sxs-lookup"><span data-stu-id="247f8-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

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

<span data-ttu-id="247f8-156">Per altre procedure dettagliate relative all'uso di modelli di Resource Manager, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="247f8-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="247f8-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="247f8-157">Next steps</span></span>
<span data-ttu-id="247f8-158">Potrebbe essere troppo[configurare la porta TCP di daemon Docker hello](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendere [sicurezza Docker](https://docs.docker.com/engine/security/security/), o distribuire contenitori usando [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="247f8-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="247f8-159">Per ulteriori informazioni sull'estensione della macchina virtuale Docker Azure stesso hello, vedere hello [GitHub progetto](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="247f8-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="247f8-160">Altre informazioni hello aggiuntive Docker opzioni di distribuzione in Azure:</span><span class="sxs-lookup"><span data-stu-id="247f8-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="247f8-161">Utilizzare computer Docker con hello Azure driver</span><span class="sxs-lookup"><span data-stu-id="247f8-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="247f8-162">[Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="247f8-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="247f8-163">Distribuire un cluster del servizio contenitore di Azure</span><span class="sxs-lookup"><span data-stu-id="247f8-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

