---
title: aaaCreate Docker ospitata in Azure con Docker macchina | Documenti Microsoft
description: Viene descritto l'utilizzo di host di macchina Docker toocreate docker in Azure.
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="fc65c-103">Creare host Docker in Azure con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="fc65c-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="fc65c-104">Esecuzione [Docker](https://www.docker.com/) contenitori richiede un host macchina virtuale in esecuzione hello daemondocker.</span><span class="sxs-lookup"><span data-stu-id="fc65c-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="fc65c-105">Questo argomento viene descritto come hello toouse [macchina docker](https://docs.docker.com/machine/) comando toocreate nuove macchine virtuali Linux, configurato con hello daemon Docker, in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="fc65c-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="fc65c-106">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="fc65c-106">**Note:**</span></span> 

* <span data-ttu-id="fc65c-107">*Questo articolo si basa sulla versione di Docker Machine 0.9.0-rc2 o versione successiva*</span><span class="sxs-lookup"><span data-stu-id="fc65c-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="fc65c-108">*Contenitori di Windows saranno supportati tramite docker-macchina in hello prossimo futuro*</span><span class="sxs-lookup"><span data-stu-id="fc65c-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="fc65c-109">Creare VM con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="fc65c-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="fc65c-110">Creare le macchine virtuali host docker in Azure con hello `docker-machine create` comando utilizzando hello `azure` driver.</span><span class="sxs-lookup"><span data-stu-id="fc65c-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="fc65c-111">Hello driver Azure richiede l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fc65c-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="fc65c-112">È possibile utilizzare hello [CLI di Azure](cli-install-nodejs.md) o hello [portale Azure](https://portal.azure.com) tooretrieve la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fc65c-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="fc65c-113">**Utilizzo di hello portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="fc65c-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="fc65c-114">Selezionare **sottoscrizioni** da hello spostamento a sinistra pagina e copia hello id sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fc65c-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="fc65c-115">**Utilizzo di hello CLI di Azure**</span><span class="sxs-lookup"><span data-stu-id="fc65c-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="fc65c-116">Tipo ```azure account list``` e l'id sottoscrizione hello di copia.</span><span class="sxs-lookup"><span data-stu-id="fc65c-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="fc65c-117">Tipo `docker-machine create --driver azure` toosee hello opzioni e i relativi valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="fc65c-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="fc65c-118">È inoltre possibile visualizzare hello [documentazione del Driver Azure Docker](https://docs.docker.com/machine/drivers/azure/) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="fc65c-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="fc65c-119">Hello esempio seguente si basa su hello [i valori predefiniti](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ma se lo si desidera impostare questi valori:</span><span class="sxs-lookup"><span data-stu-id="fc65c-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="fc65c-120">dns di Azure per il nome di hello associato a indirizzo IP pubblico hello e i certificati generati.</span><span class="sxs-lookup"><span data-stu-id="fc65c-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="fc65c-121">Questo è il nome DNS hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fc65c-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="fc65c-122">Hello VM può quindi in modo sicuro arrestare, rilasciare l'indirizzo IP dinamico hello e fornire hello possibilità tooreconnect dopo hello vm inizia nuovamente con un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="fc65c-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="fc65c-123">prefisso del nome Hello deve essere univoco per tale area UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="fc65c-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="fc65c-124">Aprire la porta 80 in hello macchina virtuale per l'accesso a internet in uscita</span><span class="sxs-lookup"><span data-stu-id="fc65c-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="fc65c-125">dimensioni di archiviazione premium più veloce di VM tooutilize hello</span><span class="sxs-lookup"><span data-stu-id="fc65c-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="fc65c-126">archiviazione Premium utilizzato per il disco di macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="fc65c-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="fc65c-127">Scegliere un host di Docker con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="fc65c-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="fc65c-128">Dopo aver creato una voce nella macchina di docker per l'host, è possibile impostare l'host predefinito hello durante l'esecuzione di comandi di docker.</span><span class="sxs-lookup"><span data-stu-id="fc65c-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="fc65c-129">Tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc65c-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="fc65c-130">Tramite Bash</span><span class="sxs-lookup"><span data-stu-id="fc65c-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="fc65c-131">È ora possibile eseguire i comandi di docker per gli host specificati hello</span><span class="sxs-lookup"><span data-stu-id="fc65c-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="fc65c-132">Eseguire un contenitore</span><span class="sxs-lookup"><span data-stu-id="fc65c-132">Run a container</span></span>
<span data-ttu-id="fc65c-133">Con un host è configurato, è ora possibile eseguire un tootest di server web semplice se l'host è stato configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="fc65c-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="fc65c-134">Qui è usare un'immagine standard nginx, specificare che deve restare in attesa sulla porta 80 e se si riavvia, macchina virtuale host hello contenitore hello verrà riavviato anche (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="fc65c-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="fc65c-135">output di Hello dovrebbe essere simile alla seguente hello:</span><span class="sxs-lookup"><span data-stu-id="fc65c-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="fc65c-136">Contenitore di test hello</span><span class="sxs-lookup"><span data-stu-id="fc65c-136">Test hello container</span></span>
<span data-ttu-id="fc65c-137">Esaminare i contenitori in esecuzione usando `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="fc65c-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="fc65c-138">E, hello toosee contenitore, tipo di esecuzione `docker-machine ip <VM name>` toofind tooenter indirizzo IP di hello nel browser hello:</span><span class="sxs-lookup"><span data-stu-id="fc65c-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Esecuzione di un contenitore ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="fc65c-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="fc65c-140">Summary</span></span>
<span data-ttu-id="fc65c-141">Docker Machine consente di eseguire facilmente il provisioning di host Docker in Azure per le convalide di host Docker singoli.</span><span class="sxs-lookup"><span data-stu-id="fc65c-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="fc65c-142">Per la produzione di hosting di contenitori, vedere hello [servizio contenitore di Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="fc65c-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="fc65c-143">toodevelop .NET Core applicazioni con Visual Studio, vedere [Docker Tools per Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="fc65c-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

