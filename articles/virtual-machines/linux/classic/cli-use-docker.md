---
title: hello aaaUsing estensione della macchina virtuale Docker per Linux in Azure
description: Descrive Docker ed estensioni di macchine virtuali di Azure hello e tooprogrammatically per la creazione di macchine virtuali in Azure che sono host docker dalla riga di comando di hello tramite hello CLI di Azure.
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
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="4045e-103">Utilizzo di hello estensione della macchina virtuale Docker da hello interfaccia della riga di comando di Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4045e-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="4045e-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4045e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4045e-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="4045e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4045e-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="4045e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4045e-107">Per informazioni sull'utilizzo di estensione della macchina virtuale Docker hello con modello di gestione risorse di hello, vedere [qui](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4045e-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="4045e-108">In questo argomento viene descritto come una macchina virtuale con hello estensione della macchina virtuale Docker da hello toocreate servizio la modalità di gestione (asm) in Azure CLI su qualsiasi piattaforma.</span><span class="sxs-lookup"><span data-stu-id="4045e-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="4045e-109">[Docker](https://www.docker.com/) è uno dei hello approcci di virtualizzazione più diffusi che utilizza [contenitori di Linux](http://en.wikipedia.org/wiki/LXC) anziché le macchine virtuali come modalità di isolamento dei dati e di elaborazione per le risorse condivise.</span><span class="sxs-lookup"><span data-stu-id="4045e-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="4045e-110">È possibile utilizzare l'estensione della macchina virtuale Docker hello e hello [agente Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate una macchina virtuale Docker che ospita qualsiasi numero di contenitori per le applicazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="4045e-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="4045e-111">toosee una descrizione di alto livello dei contenitori e i relativi vantaggi, vedere hello [Docker elevato livello di lavagna](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="4045e-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="4045e-112">Come toouse hello estensione della macchina virtuale Docker con Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="4045e-113">estensione della macchina virtuale Docker toouse hello con Azure, è necessario installare una versione di hello [interfaccia della riga di comando di Azure](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) superiore 0.8.6 (come di questo hello scrittura corrente versione 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="4045e-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="4045e-114">È possibile installare hello CLI di Azure in Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="4045e-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="4045e-115">processo completo di Hello toouse Docker in Azure è semplice:</span><span class="sxs-lookup"><span data-stu-id="4045e-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="4045e-116">Installare hello CLI di Azure e le relative dipendenze nel computer di hello da cui si desidera toocontrol Azure (in Windows, questa è una distribuzione di Linux in esecuzione come macchina virtuale)</span><span class="sxs-lookup"><span data-stu-id="4045e-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="4045e-117">Utilizzare toocreate i comandi di Docker CLI di Azure hello un host macchina virtuale Docker in Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="4045e-118">Utilizzare hello locale Docker comandi toomanage ai contenitori di Docker nella macchina virtuale Docker in Azure.</span><span class="sxs-lookup"><span data-stu-id="4045e-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="4045e-119">Installare hello interfaccia della riga di comando di Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="4045e-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="4045e-120">tooinstall e configurare hello CLI di Azure, vedere [come tooinstall hello interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4045e-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="4045e-121">installazione di hello tooconfirm, tipo `azure` al prompt dei comandi di hello e dopo un breve istante dovrebbe hello Azure CLI ASCII art, in cui sono elencati hello basic comandi tooyou disponibili.</span><span class="sxs-lookup"><span data-stu-id="4045e-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="4045e-122">Se l'installazione hello funzionava correttamente, dovrebbe essere in grado di tootype `azure help vm` e verificare che uno dei comandi elencato hello è "docker".</span><span class="sxs-lookup"><span data-stu-id="4045e-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="4045e-123">Docker include strumenti per Windows, [Docker macchina](https://docs.docker.com/installation/windows/), che è anche possibile usare la creazione di hello tooautomate di un client di docker che è possibile utilizzare toowork con macchine virtuali di Azure come host docker.</span><span class="sxs-lookup"><span data-stu-id="4045e-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="4045e-124">Connettersi hello Azure CLI tootooyour Account di Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="4045e-125">Prima di poter usare hello CLI di Azure è necessario associare le credenziali dell'account Azure hello CLI di Azure sulla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="4045e-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="4045e-126">Hello sezione [come tooconnect tooyour sottoscrizione di Azure](../../../xplat-cli-connect.md) illustra tooeither scaricare e importare il **publishsettings** file o associare la CLI di Azure con un id organizzazione.</span><span class="sxs-lookup"><span data-stu-id="4045e-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="4045e-127">Esistono alcune differenze nel comportamento quando si utilizza uno o hello altri metodi di autenticazione, pertanto essere certi tooread hello documento sopra toounderstand funzionalità diverse di hello.</span><span class="sxs-lookup"><span data-stu-id="4045e-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="4045e-128">Installare Docker e utilizzare hello estensione della macchina virtuale Docker per Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="4045e-129">Seguire hello [le istruzioni di installazione di Docker](https://docs.docker.com/installation/#installation) tooinstall Docker in locale nel computer.</span><span class="sxs-lookup"><span data-stu-id="4045e-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="4045e-130">toouse Docker con una macchina virtuale di Azure, immagine di Linux hello utilizzata per hello macchina virtuale deve avere hello [agente VM Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installato.</span><span class="sxs-lookup"><span data-stu-id="4045e-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="4045e-131">Al momento esistono solo due tipi di immagine che offrono queste funzionalità:</span><span class="sxs-lookup"><span data-stu-id="4045e-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="4045e-132">Un'immagine Ubuntu da hello raccolta immagini di Azure o</span><span class="sxs-lookup"><span data-stu-id="4045e-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="4045e-133">Un'immagine personalizzata di Linux che è stato creato con l'agente VM Linux di Azure hello installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="4045e-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="4045e-134">Vedere [agente VM Linux di Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per ulteriori informazioni su come toobuild una VM Linux personalizzato con hello agente VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="4045e-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="4045e-135">Utilizzo di hello raccolta immagini di Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="4045e-136">Da una sessione Terminal o Bash, utilizzare il comando CLI di Azure toolocate hello immagine Ubuntu più recente in hello VM raccolta toouse digitando seguente hello</span><span class="sxs-lookup"><span data-stu-id="4045e-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="4045e-137">e selezionare uno dei nomi di immagine hello, ad esempio `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, e il comando che segue hello utilizzare toocreate una nuova macchina virtuale utilizzando tale immagine.</span><span class="sxs-lookup"><span data-stu-id="4045e-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="4045e-138">dove:</span><span class="sxs-lookup"><span data-stu-id="4045e-138">where:</span></span>

* <span data-ttu-id="4045e-139">*&lt;nome VM cloudservice&gt;*  nome hello di hello VM che verranno configurati come computer di host contenitore Docker hello in Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="4045e-140">*&lt;nome utente&gt;*  hello nomeutente dell'utente di radice predefinito hello di hello VM</span><span class="sxs-lookup"><span data-stu-id="4045e-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="4045e-141">*&lt;password&gt;*  password hello di hello *username* account conforme agli standard di hello di complessità per Azure</span><span class="sxs-lookup"><span data-stu-id="4045e-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="4045e-142">Attualmente, una password deve essere di almeno 8 caratteri e contenere una lettera minuscola e una lettera maiuscola, un numero e un carattere speciale, ad esempio uno dei seguenti caratteri hello: `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="4045e-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="4045e-143">No, il periodo di hello alla fine hello hello prima frase non è un carattere speciale.</span><span class="sxs-lookup"><span data-stu-id="4045e-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="4045e-144">Se il comando hello ha esito positivo, dovrebbe essere simile alla seguente hello, a seconda di argomenti di preciso hello e le opzioni utilizzate:</span><span class="sxs-lookup"><span data-stu-id="4045e-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="4045e-145">La creazione di una macchina virtuale può richiedere alcuni minuti, ma dopo è stato eseguito il provisioning (il valore di stato hello è `ReadyRole`) hello avvio di Docker daemon (Buongiorno servizio Docker) ed è possibile connettersi toohello host del contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="4045e-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="4045e-146">hello tootest macchina virtuale Docker è stato creato in Azure, tipo</span><span class="sxs-lookup"><span data-stu-id="4045e-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="4045e-147">dove  *&lt;vm-name--utilizzati&gt;*  hello nome della macchina virtuale hello utilizzato nella chiamata troppo`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="4045e-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="4045e-148">Dovrebbe essere simile toohello seguenti, che indica che la macchina virtuale Host Docker sia attivo e in esecuzione in Azure e in attesa per i comandi.</span><span class="sxs-lookup"><span data-stu-id="4045e-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="4045e-149">Ora è possibile provare tooconnect utilizzando le informazioni di tooobtain client docker (in alcune installazioni di client Docker, ad esempio che nel Mac, è possibile toouse `sudo`):</span><span class="sxs-lookup"><span data-stu-id="4045e-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

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

<span data-ttu-id="4045e-150">Solo toobe assicurarsi che sia di funzionare, è possibile esaminare hello macchina virtuale per l'estensione Docker hello:</span><span class="sxs-lookup"><span data-stu-id="4045e-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="4045e-151">Autenticazione della VM host di Docker</span><span class="sxs-lookup"><span data-stu-id="4045e-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="4045e-152">Inoltre toocreating hello VM Docker, hello `azure vm docker create` comando crea automaticamente anche tooallow certificati necessari hello client computer tooconnect toohello Azure contenitore host Docker con HTTPS e i certificati di hello vengono archiviati sia Hello computer client e host, come appropriato.</span><span class="sxs-lookup"><span data-stu-id="4045e-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="4045e-153">Durante i successivi tentativi, i certificati esistenti hello vengono riutilizzati e condivise con nuovo host hello.</span><span class="sxs-lookup"><span data-stu-id="4045e-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="4045e-154">Per impostazione predefinita, i certificati vengono inseriti nella `~/.docker`, e Docker sarà toorun configurato sulla porta **2376**.</span><span class="sxs-lookup"><span data-stu-id="4045e-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="4045e-155">Se si desidera toouse una porta diversa o una directory, quindi è possibile utilizzare uno dei seguenti hello `azure vm docker create` tooconfigure opzioni della riga di comando del Docker contenitore host VM toouse una porta diversa o certificati diversi per la connessione client:</span><span class="sxs-lookup"><span data-stu-id="4045e-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="4045e-156">è configurato toolisten per Hello daemon Docker nell'host di hello e autenticare le connessioni sul hello specificato porta tramite hello certificati generati da hello client `azure vm docker create` comando.</span><span class="sxs-lookup"><span data-stu-id="4045e-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="4045e-157">computer client Hello deve disporre di questi host Docker toohello di certificati toogain accesso.</span><span class="sxs-lookup"><span data-stu-id="4045e-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="4045e-158">Un host di rete in esecuzione senza questi certificati sarà vulnerabile tooanyone che può essere tooconnect toohello macchina.</span><span class="sxs-lookup"><span data-stu-id="4045e-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="4045e-159">Prima di modificare una configurazione predefinita di hello, assicurarsi di aver compreso hello rischi tooyour computer e applicazioni.</span><span class="sxs-lookup"><span data-stu-id="4045e-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4045e-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4045e-160">Next steps</span></span>
* <span data-ttu-id="4045e-161">Si è pronti toogo toohello [manuale dell'utente Docker] e usare la macchina virtuale Docker.</span><span class="sxs-lookup"><span data-stu-id="4045e-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="4045e-162">toocreate una macchina virtuale Docker abilitati nel nuovo portale di hello, vedere [come toouse hello estensione della macchina virtuale Docker con hello portale].</span><span class="sxs-lookup"><span data-stu-id="4045e-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="4045e-163">Hello estensione della macchina virtuale Docker di Azure supporta Docker Compose, che utilizza un dichiarativa YAML file tootake, un'applicazione modellata sviluppatore in qualsiasi ambiente e generare una distribuzione uniforme.</span><span class="sxs-lookup"><span data-stu-id="4045e-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="4045e-164">Vedere [Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure].</span><span class="sxs-lookup"><span data-stu-id="4045e-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[come toouse hello estensione della macchina virtuale Docker con hello portale]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[manuale dell'utente Docker]:https://docs.docker.com/userguide/

[Introduzione a Docker e comporre toodefine e di eseguire un'applicazione multi-contenitore in una macchina virtuale Azure]:../docker-compose-quickstart.md
