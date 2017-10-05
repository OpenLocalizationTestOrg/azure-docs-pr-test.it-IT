---
title: Uso dell'estensione della VM Docker per Linux in Azure
description: Descrive Docker e le estensioni di Macchine virtuali di Azure e mostra come creare a livello di codice le macchine virtuali in Azure che siano host Docker dalla riga di comando usando l'interfaccia della riga di comando di Azure.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: a542332c921862241f1f000e6a8f0a0ae0e8a934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-from-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="8ca25-103">Uso dell’estensione della VM Docker dall’interfaccia della riga di comando di Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="8ca25-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="8ca25-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8ca25-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8ca25-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="8ca25-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8ca25-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="8ca25-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8ca25-107">Per informazioni sull'uso dell'estensione della VM Docker personalizzata con il modello di Resource Manager, vedere [qui](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ca25-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8ca25-108">Questo argomento descrive come creare una VM con l'estensione della VM Docker dalla modalità di gestione dei servizi (asm) nell'interfaccia della riga di comando di Azure su qualsiasi piattaforma.</span><span class="sxs-lookup"><span data-stu-id="8ca25-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="8ca25-109">[Docker](https://www.docker.com/) è uno dei più popolari approcci alla virtualizzazione che usa [contenitori Linux](http://en.wikipedia.org/wiki/LXC) invece di macchine virtuali allo scopo di isolare i dati ed eseguire i calcoli su risorse condivise.</span><span class="sxs-lookup"><span data-stu-id="8ca25-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="8ca25-110">È possibile usare l'estensione della macchina virtuale Docker per l'[Agente Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per creare una VM Docker che ospiti un numero qualsiasi di contenitori per le applicazioni su Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca25-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="8ca25-111">Per assistere a una discussione di alto livello sui contenitori e i relativi vantaggi, guardare questa [sessione con lavagna condivisa relativa a Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="8ca25-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-to-use-the-docker-vm-extension-with-azure"></a><span data-ttu-id="8ca25-112">Come usare l'estensione della VM Docker con Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-112">How to use the Docker VM Extension with Azure</span></span>
<span data-ttu-id="8ca25-113">Per usare l'estensione della VM Docker con Azure è necessario installare una versione dell'[interfaccia della riga di comando di Azure](https://github.com/Azure/azure-sdk-tools-xplat) successiva alla versione 0.8.6 (al momento della stesura di questo articolo, la versione corrente è la 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="8ca25-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span></span> <span data-ttu-id="8ca25-114">È possibile installare l’interfaccia della riga di comando di Azure su Mac, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="8ca25-114">You can install the Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="8ca25-115">Il processo completo di utilizzo di Docker su Azure è semplice:</span><span class="sxs-lookup"><span data-stu-id="8ca25-115">The complete process to use Docker on Azure is simple:</span></span>

* <span data-ttu-id="8ca25-116">Installare l’interfaccia della riga di comando di Azure e le relative dipendenze sul computer dal quale si intende controllare Azure (su Windows, si tratterà di una distribuzione Linux in esecuzione come macchina virtuale)</span><span class="sxs-lookup"><span data-stu-id="8ca25-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="8ca25-117">Usare i comandi di Docker per l’interfaccia della riga di comando di Azure per creare un host Docker della VM in Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span></span>
* <span data-ttu-id="8ca25-118">Usare i comandi locali di Docker per gestire i contenitori Docker nella VM Docker in Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca25-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="8ca25-119">Installare l'interfaccia della riga di comando di Azure </span><span class="sxs-lookup"><span data-stu-id="8ca25-119">Install the Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="8ca25-120">Per installare e configurare l’interfaccia della riga di comando di Azure, vedere [Come installare e configurare l'interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8ca25-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="8ca25-121">Per confermare l'installazione, digitare `azure` nel prompt dei comandi. Dopo pochi secondi verrà visualizzata la grafica ASCII dell’interfaccia della riga di comando di Azure, in cui sono elencati i comandi di base disponibili.</span><span class="sxs-lookup"><span data-stu-id="8ca25-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span></span> <span data-ttu-id="8ca25-122">Se l'installazione è andata a buon fine, sarà possibile digitare `azure help vm` e verificare che uno dei comandi elencati corrisponda a "docker".</span><span class="sxs-lookup"><span data-stu-id="8ca25-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="8ca25-123">Docker include strumenti per Windows, ovvero [Docker Machine](https://docs.docker.com/installation/windows/), che consentono anche di automatizzare la creazione di un client Docker da usare per gestire macchine virtuali di Azure come host Docker.</span><span class="sxs-lookup"><span data-stu-id="8ca25-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-the-azure-cli-to-to-your-azure-account"></a><span data-ttu-id="8ca25-124">Connettere l'interfaccia della riga di comando di Azure al proprio account Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-124">Connect the Azure CLI to to your Azure Account</span></span>
<span data-ttu-id="8ca25-125">Prima di poter usare l'interfaccia della riga di comando di Azure è necessario associare alla stessa le credenziali del proprio account Azure sulla propria piattaforma.</span><span class="sxs-lookup"><span data-stu-id="8ca25-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span></span> <span data-ttu-id="8ca25-126">La sezione [Come connettersi alla sottoscrizione di Azure](../../../xplat-cli-connect.md) spiega come scaricare e importare il file **.publishsettings** o associare l'interfaccia della riga di comando di Azure a un ID organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8ca25-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="8ca25-127">Ci sono alcune differenze di comportamento quando si usa l'uno o l'altro metodo di autenticazione, perciò assicurarsi di leggere il documento sopra riportato per comprendere le diverse funzionalità.</span><span class="sxs-lookup"><span data-stu-id="8ca25-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-the-docker-vm-extension-for-azure"></a><span data-ttu-id="8ca25-128">Installare Docker e usare l'estensione della VM Docker per Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-128">Install Docker and use the Docker VM Extension for Azure</span></span>
<span data-ttu-id="8ca25-129">Per installare Docker in locale sul proprio computer seguire le [istruzioni di installazione di Docker](https://docs.docker.com/installation/#installation) .</span><span class="sxs-lookup"><span data-stu-id="8ca25-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span></span>

<span data-ttu-id="8ca25-130">Per usare Docker con una macchina virtuale di Azure, l'immagine Linux usata per la VM deve avere installato l'[agente VM Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ca25-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="8ca25-131">Al momento esistono solo due tipi di immagine che offrono queste funzionalità:</span><span class="sxs-lookup"><span data-stu-id="8ca25-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="8ca25-132">un'immagine Ubuntu dalla raccolta immagini di Azure o</span><span class="sxs-lookup"><span data-stu-id="8ca25-132">An Ubuntu image from the Azure Image Gallery or</span></span>
* <span data-ttu-id="8ca25-133">un'immagine Linux personalizzata creata con l'agente VM Linux Azure installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="8ca25-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="8ca25-134">Per altre informazioni su come costruire una VM Linux con l'agente VM di Azure, vedere [Agente VM Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ca25-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span></span>

### <a name="using-the-azure-image-gallery"></a><span data-ttu-id="8ca25-135">Uso della raccolta immagini di Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-135">Using the Azure Image Gallery</span></span>
<span data-ttu-id="8ca25-136">Da una sessione Bash o Terminal, usare il seguente comando dell’interfaccia della riga di comando di Azure per trovare l'immagine più recente di Ubuntu nella raccolta di VM da usare digitando</span><span class="sxs-lookup"><span data-stu-id="8ca25-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="8ca25-137">e selezionare uno dei nomi di immagine, ad esempio `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, quindi usare il comando seguente per creare una nuova macchina virtuale usando tale immagine.</span><span class="sxs-lookup"><span data-stu-id="8ca25-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="8ca25-138">dove:</span><span class="sxs-lookup"><span data-stu-id="8ca25-138">where:</span></span>

* <span data-ttu-id="8ca25-139">*&lt;vm-cloudservice name&gt;* è il nome della VM che diventerà il computer host del contenitore Docker in Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span></span>
* <span data-ttu-id="8ca25-140">*&lt;username&gt;* è il nome utente dell'utente ROOT predefinito della VM</span><span class="sxs-lookup"><span data-stu-id="8ca25-140">*&lt;username&gt;* is the username of the default root user of the VM</span></span>
* <span data-ttu-id="8ca25-141">*&lt;password&gt;* è la password dell'account *username* che soddisfa gli standard di complessità per Azure</span><span class="sxs-lookup"><span data-stu-id="8ca25-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="8ca25-142">Attualmente, una password deve contenere almeno 8 caratteri, un carattere minuscolo e uno maiuscolo, un numero e un carattere speciale, ad esempio uno dei seguenti: `!@#$%^&+=`</span><span class="sxs-lookup"><span data-stu-id="8ca25-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="8ca25-143">Il punto alla fine della frase precedente NON è un carattere speciale.</span><span class="sxs-lookup"><span data-stu-id="8ca25-143">No, the period at the end of the preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="8ca25-144">Se il comando ha avuto esito positivo, verrà visualizzato un output simile al seguente, a seconda degli argomenti e delle opzioni precisi usati:</span><span class="sxs-lookup"><span data-stu-id="8ca25-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="8ca25-145">La creazione di una macchina virtuale può richiedere alcuni minuti, ma dopo che ne è stato effettuato il provisioning (il valore dello stato è `ReadyRole`) viene avviato il daemon Docker ed è possibile connettersi all'host contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="8ca25-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span></span>
> 
> 

<span data-ttu-id="8ca25-146">Per testare la VM Docker creata in Azure, digitare</span><span class="sxs-lookup"><span data-stu-id="8ca25-146">To test the Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="8ca25-147">dove *&lt;vm-name-you-used&gt;* è il nome della macchina virtuale usata nella chiamata a `azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="8ca25-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span></span> <span data-ttu-id="8ca25-148">Viene visualizzato codice simile al seguente, che indica che la VM host di Docker è in fase di elaborazione in Azure ed è in attesa dei comandi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8ca25-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="8ca25-149">Ora è possibile provare a connettersi utilizzando il client docker per ottenere informazioni (in alcune configurazioni del client Docker, ad esempio nei Mac, è necessario utilizzare `sudo`):</span><span class="sxs-lookup"><span data-stu-id="8ca25-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="8ca25-150">Per essere certi che tutto funzioni, è possibile esaminare la macchina virtuale per l'estensione Docker:</span><span class="sxs-lookup"><span data-stu-id="8ca25-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="8ca25-151">Autenticazione della VM host di Docker</span><span class="sxs-lookup"><span data-stu-id="8ca25-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="8ca25-152">Oltre a creare la VM di Docker, il comando `azure vm docker create` crea automaticamente anche i certificati necessari che consentono al computer client Docker di connettersi all'host contenitore di Azure con il protocollo HTTPS. I certificati saranno archiviati sulle macchine client e host, secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="8ca25-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span></span> <span data-ttu-id="8ca25-153">Nei tentativi  successivi, i certificati esistenti verranno riutilizzati e condivisi con il nuovo host.</span><span class="sxs-lookup"><span data-stu-id="8ca25-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span></span>

<span data-ttu-id="8ca25-154">Per impostazione predefinita, i certificati vengono inseriti in `~/.docker`e Docker verrà configurato per l'esecuzione sulla porta **2376**.</span><span class="sxs-lookup"><span data-stu-id="8ca25-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span></span> <span data-ttu-id="8ca25-155">Per scegliere una porta o una directory differente, usare una delle seguenti opzioni della riga di comando `azure vm docker create` per configurare la VM host del contenitore Docker in modo da usare una porta differente o certificati differenti per connettere i client:</span><span class="sxs-lookup"><span data-stu-id="8ca25-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port to use for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="8ca25-156">Il daemon Docker sull'host è configurato per restare in ascolto delle connessioni client e autenticarle sulla porta specificata usando i certificati generati dal comando `azure vm docker create` .</span><span class="sxs-lookup"><span data-stu-id="8ca25-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span></span> <span data-ttu-id="8ca25-157">La macchina client deve avere questi certificati per poter accedere all'host Docker.</span><span class="sxs-lookup"><span data-stu-id="8ca25-157">The client machine must have these certificates to gain access to the Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="8ca25-158">Un host di rete in esecuzione senza questi certificati sarà vulnerabile a chiunque possa connettersi alla macchina.</span><span class="sxs-lookup"><span data-stu-id="8ca25-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span></span> <span data-ttu-id="8ca25-159">Prima di modificare la configurazione predefinita, assicurarsi di aver compreso i rischi a cui si sottopongono i computer e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8ca25-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8ca25-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ca25-160">Next steps</span></span>
* <span data-ttu-id="8ca25-161">È ora possibile passare alla [guida dell'utente di Docker] e usare la VM Docker.</span><span class="sxs-lookup"><span data-stu-id="8ca25-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="8ca25-162">Per creare una VM abilitata per Docker incorporata nel nuovo portale, vedere l'articolo su [come usare l'estensione della VM Docker con il portale].</span><span class="sxs-lookup"><span data-stu-id="8ca25-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span></span>
* <span data-ttu-id="8ca25-163">L'estensione della VM Docker di Azure supporta anche Docker Compose, che usa un file YAML dichiarativo per eseguire un'applicazione modellata dallo sviluppatore in qualsiasi ambiente e generare una distribuzione coerente.</span><span class="sxs-lookup"><span data-stu-id="8ca25-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="8ca25-164">Vedere [Introduzione a Docker e Compose per definire ed eseguire un'applicazione multi-contenitore in una macchina virtuale di Azure].</span><span class="sxs-lookup"><span data-stu-id="8ca25-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How to use the Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 to another azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 to another azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md
<span data-ttu-id="8ca25-165">[come usare l'estensione della VM Docker con il portale]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span><span class="sxs-lookup"><span data-stu-id="8ca25-165">[How to use the Docker VM Extension with the Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span></span>

<span data-ttu-id="8ca25-166">[guida dell'utente di Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="8ca25-166">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>

<span data-ttu-id="8ca25-167">[Introduzione a Docker e Compose per definire ed eseguire un'applicazione multi-contenitore in una macchina virtuale di Azure]:../docker-compose-quickstart.md</span><span class="sxs-lookup"><span data-stu-id="8ca25-167">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine]:../docker-compose-quickstart.md</span></span>
