---
title: Usare Docker Machine per creare host Linux in Azure | Documentazione Microsoft
description: Descrive l'uso di Docker Machine per creare host Docker in Azure.
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
ms.openlocfilehash: a69951ed60edab8ae20374ab3869b468979c4907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-docker-machine-to-create-hosts-in-azure"></a><span data-ttu-id="fb16b-103">Come usare Docker Machine per creare host in Azure</span><span class="sxs-lookup"><span data-stu-id="fb16b-103">How to use Docker Machine to create hosts in Azure</span></span>
<span data-ttu-id="fb16b-104">Questa articolo illustra come usare [Docker Machine](https://docs.docker.com/machine/) per creare host in Azure.</span><span class="sxs-lookup"><span data-stu-id="fb16b-104">This article details how to use [Docker Machine](https://docs.docker.com/machine/) to create hosts in Azure.</span></span> <span data-ttu-id="fb16b-105">Il comando `docker-machine` crea una macchina virtuale (VM) Linux in Azure e quindi installa Docker.</span><span class="sxs-lookup"><span data-stu-id="fb16b-105">The `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="fb16b-106">Ciò consentirà di gestire gli host Docker in Azure usando gli stessi strumenti e flussi di lavoro locali.</span><span class="sxs-lookup"><span data-stu-id="fb16b-106">You can then manage your Docker hosts in Azure using the same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="fb16b-107">Creare VM con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="fb16b-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="fb16b-108">Ottenere prima di tutto l'ID sottoscrizione di Azure con [az account show](/cli/azure/account#show) nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="fb16b-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="fb16b-109">Le macchine virtuali host Docker vengono create in Azure con `docker-machine create` specificando *azure* come driver.</span><span class="sxs-lookup"><span data-stu-id="fb16b-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as the driver.</span></span> <span data-ttu-id="fb16b-110">Per altre informazioni, vedere la [documentazione del driver di Azure per Docker](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="fb16b-110">For more information, see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="fb16b-111">Nell'esempio seguente viene creata una macchina virtuale denominata *myVM*, viene creato un account utente denominato *azureuser* e viene aperta la porta *80* sulla macchina virtuale host.</span><span class="sxs-lookup"><span data-stu-id="fb16b-111">The following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on the host VM.</span></span> <span data-ttu-id="fb16b-112">Seguire le istruzioni visualizzate per accedere all'account Azure e concedere a Docker Machine le autorizzazioni necessarie per creare e gestire le risorse.</span><span class="sxs-lookup"><span data-stu-id="fb16b-112">Follow any prompts to log in to your Azure account and grant Docker Machine permissions to create and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="fb16b-113">L'output è simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="fb16b-113">The output looks similar to the following example:</span></span>

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
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="fb16b-114">Configurare la shell di Docker</span><span class="sxs-lookup"><span data-stu-id="fb16b-114">Configure your Docker shell</span></span>
<span data-ttu-id="fb16b-115">Per connettersi all'host Docker in Azure, definire le impostazioni di connessione appropriate.</span><span class="sxs-lookup"><span data-stu-id="fb16b-115">To connect to your Docker host in Azure, define the appropriate connection settings.</span></span> <span data-ttu-id="fb16b-116">Come indicato alla fine dell'output, visualizzare le informazioni di connessione per l'host Docker nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="fb16b-116">As noted at the end of the output, view the connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="fb16b-117">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="fb16b-117">The output is similar to the following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="fb16b-118">Per definire le impostazioni di connessione, è possibile eseguire il comando di configurazione suggerito (`eval $(docker-machine env myvmdocker)`) o impostare manualmente le variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="fb16b-118">To define the connection settings you can either run the suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set the environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="fb16b-119">Eseguire un contenitore</span><span class="sxs-lookup"><span data-stu-id="fb16b-119">Run a container</span></span>
<span data-ttu-id="fb16b-120">Per vedere un contenitore in azione, verrà eseguito un server Web NGINX di base.</span><span class="sxs-lookup"><span data-stu-id="fb16b-120">To see a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="fb16b-121">Creare un contenitore con `docker run` ed esporre la porta 80 al traffico Web nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="fb16b-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="fb16b-122">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="fb16b-122">The output is similar to the following example:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="fb16b-123">Visualizzare i contenitori in esecuzione con `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="fb16b-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="fb16b-124">Nell'output di esempio seguente si può vedere il contenitore NGINX in esecuzione con la porta 80 esposta:</span><span class="sxs-lookup"><span data-stu-id="fb16b-124">The following example output shows the NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-the-container"></a><span data-ttu-id="fb16b-125">Eseguire il test del contenitore</span><span class="sxs-lookup"><span data-stu-id="fb16b-125">Test the container</span></span>
<span data-ttu-id="fb16b-126">Ottenere l'indirizzo IP pubblico dell'host Docker come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb16b-126">Obtain the public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="fb16b-127">Per vedere il contenitore in azione, aprire un Web browser e immettere l'indirizzo IP pubblico indicato nell'output del comando precedente:</span><span class="sxs-lookup"><span data-stu-id="fb16b-127">To see the container in action, open a web browser and enter the public IP address noted in the output of the preceding command:</span></span>

![Esecuzione di un contenitore ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="fb16b-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb16b-129">Next steps</span></span>
<span data-ttu-id="fb16b-130">È anche possibile creare host con l'[estensione di VM Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="fb16b-130">You can also create hosts with the [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="fb16b-131">Per esempi sull'uso di Docker Compose, vedere [Introduzione a Docker e Compose in Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="fb16b-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
