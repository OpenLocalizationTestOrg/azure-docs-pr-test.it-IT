---
title: ospita aaaUse macchina Docker toocreate Linux in Azure | Documenti Microsoft
description: Viene descritto come toouse macchina Docker toocreate Docker ospitata in Azure.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a><span data-ttu-id="82c16-103">Come toouse Docker macchina toocreate ospitata in Azure</span><span class="sxs-lookup"><span data-stu-id="82c16-103">How toouse Docker Machine toocreate hosts in Azure</span></span>
<span data-ttu-id="82c16-104">Questo articolo come dettagli toouse [Docker macchina](https://docs.docker.com/machine/) host toocreate in Azure.</span><span class="sxs-lookup"><span data-stu-id="82c16-104">This article details how toouse [Docker Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span></span> <span data-ttu-id="82c16-105">Hello `docker-machine` comando crea una macchina virtuale Linux (VM) in Azure, quindi installa Docker.</span><span class="sxs-lookup"><span data-stu-id="82c16-105">hello `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="82c16-106">È quindi possibile gestire gli host Docker in Azure tramite hello stessi strumenti locali e i flussi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="82c16-106">You can then manage your Docker hosts in Azure using hello same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="82c16-107">Creare VM con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="82c16-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="82c16-108">Ottenere prima di tutto l'ID sottoscrizione di Azure con [az account show](/cli/azure/account#show) nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="82c16-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="82c16-109">Creare le macchine virtuali host Docker in Azure con `docker-machine create` specificando *azure* come driver hello.</span><span class="sxs-lookup"><span data-stu-id="82c16-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as hello driver.</span></span> <span data-ttu-id="82c16-110">Per ulteriori informazioni, vedere hello [documentazione del Driver di Azure di Docker](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="82c16-110">For more information, see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="82c16-111">esempio Hello crea una macchina virtuale denominata *myVM*, crea un account utente denominato *azureuser*e l'apertura della porta *80* in hello host macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="82c16-111">hello following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on hello host VM.</span></span> <span data-ttu-id="82c16-112">Seguire toolog qualsiasi richiesta in tooyour account Azure e concedere toocreate autorizzazioni macchina Docker e gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="82c16-112">Follow any prompts toolog in tooyour Azure account and grant Docker Machine permissions toocreate and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="82c16-113">output di Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="82c16-113">hello output looks similar toohello following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="82c16-114">Configurare la shell di Docker</span><span class="sxs-lookup"><span data-stu-id="82c16-114">Configure your Docker shell</span></span>
<span data-ttu-id="82c16-115">host di tooconnect tooyour Docker in Azure, definire le impostazioni di connessione appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="82c16-115">tooconnect tooyour Docker host in Azure, define hello appropriate connection settings.</span></span> <span data-ttu-id="82c16-116">Come indicato alla fine di hello dell'output di hello, visualizzare informazioni di connessione hello per l'host Docker come segue:</span><span class="sxs-lookup"><span data-stu-id="82c16-116">As noted at hello end of hello output, view hello connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="82c16-117">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="82c16-117">hello output is similar toohello following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="82c16-118">è possibile l'esecuzione hello le impostazioni di connessione di toodefine hello consigliate comando di configurazione (`eval $(docker-machine env myvmdocker)`), oppure è possibile impostare le variabili di ambiente hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="82c16-118">toodefine hello connection settings you can either run hello suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set hello environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="82c16-119">Eseguire un contenitore</span><span class="sxs-lookup"><span data-stu-id="82c16-119">Run a container</span></span>
<span data-ttu-id="82c16-120">toosee un contenitore in azione, consente l'esecuzione di un server Web NGINX di base.</span><span class="sxs-lookup"><span data-stu-id="82c16-120">toosee a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="82c16-121">Creare un contenitore con `docker run` ed esporre la porta 80 al traffico Web nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="82c16-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="82c16-122">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="82c16-122">hello output is similar toohello following example:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="82c16-123">Visualizzare i contenitori in esecuzione con `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="82c16-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="82c16-124">Hello output di esempio seguente viene illustrato hello NGINX contenitore in esecuzione con la porta 80 esposti:</span><span class="sxs-lookup"><span data-stu-id="82c16-124">hello following example output shows hello NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a><span data-ttu-id="82c16-125">Contenitore di test hello</span><span class="sxs-lookup"><span data-stu-id="82c16-125">Test hello container</span></span>
<span data-ttu-id="82c16-126">Ottenere hello indirizzo IP dell'host Docker come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="82c16-126">Obtain hello public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="82c16-127">contenitore hello toosee in azione, aprire un web browser e immettere l'indirizzo IP pubblico hello indicato nell'output di hello di hello precedente comando:</span><span class="sxs-lookup"><span data-stu-id="82c16-127">toosee hello container in action, open a web browser and enter hello public IP address noted in hello output of hello preceding command:</span></span>

![Esecuzione di un contenitore ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="82c16-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82c16-129">Next steps</span></span>
<span data-ttu-id="82c16-130">È inoltre possibile creare l'host con hello [estensione della macchina virtuale Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="82c16-130">You can also create hosts with hello [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="82c16-131">Per esempi sull'uso di Docker Compose, vedere [Introduzione a Docker e Compose in Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="82c16-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
