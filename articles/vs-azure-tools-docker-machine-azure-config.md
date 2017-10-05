---
title: Creare host Docker in Azure con Docker Machine | Microsoft Docs
description: Descrive l'uso di Docker Machine per creare host Docker in Azure.
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
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="3ec67-103">Creare host Docker in Azure con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="3ec67-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="3ec67-104">L'esecuzione dei contenitori [Docker](https://www.docker.com/) richiede una VM host che esegue il daemon Docker.</span><span class="sxs-lookup"><span data-stu-id="3ec67-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="3ec67-105">Questo argomento descrive come usare il comando [docker-machine](https://docs.docker.com/machine/) per creare nuove macchine virtuali Linux, configurate con il daemon Docker, in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="3ec67-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="3ec67-106">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="3ec67-106">**Note:**</span></span> 

* <span data-ttu-id="3ec67-107">*Questo articolo si basa sulla versione di Docker Machine 0.9.0-rc2 o versione successiva*</span><span class="sxs-lookup"><span data-stu-id="3ec67-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="3ec67-108">*I contenitori Windows saranno supportati tramite Docker Machine nel prossimo futuro*</span><span class="sxs-lookup"><span data-stu-id="3ec67-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="3ec67-109">Creare VM con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="3ec67-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="3ec67-110">Creare macchine virtuali host di Docker in Azure con il comando `docker-machine create` usando il driver `azure`.</span><span class="sxs-lookup"><span data-stu-id="3ec67-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="3ec67-111">Il driver Azure richiede l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ec67-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="3ec67-112">È possibile usare l'[interfaccia della riga di comando di Azure](cli-install-nodejs.md) o il [Portale di Azure](https://portal.azure.com) per recuperare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ec67-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="3ec67-113">**Uso del portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="3ec67-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="3ec67-114">Selezionare **Sottoscrizioni** nella pagina di esplorazione a sinistra e copiare l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ec67-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="3ec67-115">**Uso dell'interfaccia della riga di comando di Azure**</span><span class="sxs-lookup"><span data-stu-id="3ec67-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="3ec67-116">Digitare ```azure account list``` e copiare l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="3ec67-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="3ec67-117">Digitare `docker-machine create --driver azure` per visualizzare le opzioni e i relativi valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="3ec67-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="3ec67-118">È anche possibile visualizzare la [documentazione del driver di Azure per Docker](https://docs.docker.com/machine/drivers/azure/) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="3ec67-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="3ec67-119">L'esempio seguente si basa sui [valori predefiniti](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ma imposta facoltativamente questi valori:</span><span class="sxs-lookup"><span data-stu-id="3ec67-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="3ec67-120">azure-dns per il nome associato all'indirizzo IP pubblico e ai certificati generati.</span><span class="sxs-lookup"><span data-stu-id="3ec67-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="3ec67-121">Questo è il nome DNS della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ec67-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="3ec67-122">La macchina virtuale può quindi arrestare e rilasciare in modo sicuro l'indirizzo IP dinamico e consentire di riconnettersi dopo che una macchina virtuale viene avviata nuovamente con un nuovo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="3ec67-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="3ec67-123">Il prefisso del nome deve essere univoco per tale area, ovvero UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="3ec67-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="3ec67-124">porta 80 aperta sulla macchina virtuale per l'accesso Internet in uscita</span><span class="sxs-lookup"><span data-stu-id="3ec67-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="3ec67-125">dimensioni della macchina virtuale per usare l'archiviazione Premium più veloce</span><span class="sxs-lookup"><span data-stu-id="3ec67-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="3ec67-126">archiviazione Premium usata per il disco della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3ec67-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="3ec67-127">Scegliere un host di Docker con Docker Machine</span><span class="sxs-lookup"><span data-stu-id="3ec67-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="3ec67-128">Dopo aver creato un ingresso nella Docker Machine per l'host, è possibile impostare l'host predefinito quando si eseguono comandi di Docker.</span><span class="sxs-lookup"><span data-stu-id="3ec67-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="3ec67-129">Tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ec67-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="3ec67-130">Tramite Bash</span><span class="sxs-lookup"><span data-stu-id="3ec67-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="3ec67-131">È ora possibile eseguire i comandi di Docker con l'host specificato</span><span class="sxs-lookup"><span data-stu-id="3ec67-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="3ec67-132">Eseguire un contenitore</span><span class="sxs-lookup"><span data-stu-id="3ec67-132">Run a container</span></span>
<span data-ttu-id="3ec67-133">Dopo aver configurato l'host, è possibile eseguire un semplice server Web per verificare che la configurazione dell'host sia corretta.</span><span class="sxs-lookup"><span data-stu-id="3ec67-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="3ec67-134">In questo esempio viene usata un'immagine nginx standard. Specificare che deve essere in ascolto sulla porta 80 e che, se la VM dell'host viene riavviata, anche il contenitore deve essere riavviato (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="3ec67-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="3ec67-135">L'output dovrebbe essere simile a quanto segue.</span><span class="sxs-lookup"><span data-stu-id="3ec67-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="3ec67-136">Eseguire il test del contenitore</span><span class="sxs-lookup"><span data-stu-id="3ec67-136">Test the container</span></span>
<span data-ttu-id="3ec67-137">Esaminare i contenitori in esecuzione usando `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="3ec67-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="3ec67-138">Quindi per vedere il contenitore in esecuzione digitare `docker-machine ip <VM name>` per trovare l'indirizzo IP da immettere nel browser:</span><span class="sxs-lookup"><span data-stu-id="3ec67-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Esecuzione di un contenitore ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="3ec67-140">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="3ec67-140">Summary</span></span>
<span data-ttu-id="3ec67-141">Docker Machine consente di eseguire facilmente il provisioning di host Docker in Azure per le convalide di host Docker singoli.</span><span class="sxs-lookup"><span data-stu-id="3ec67-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="3ec67-142">Per l'hosting di produzione di contenitori, vedere l'articolo sul [servizio contenitore di Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="3ec67-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="3ec67-143">Per sviluppare applicazioni .NET Core con Visual Studio, vedere gli [Strumenti Docker per Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="3ec67-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

