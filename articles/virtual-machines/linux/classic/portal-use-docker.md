---
title: Uso di estensioni VM Docker per Linux | Microsoft Docs
description: Descrive Docker e le estensioni di Macchine virtuali di Azure e come creare le macchine virtuali di Azure che siano host Docker usando l'interfaccia della riga di comando di Azure nel modello di distribuzione classica.
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 932744208d9d53c87e31dcdf9e34539750be4bdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-with-the-azure-classic-portal"></a><span data-ttu-id="d1cba-103">Come usare l'estensione della VM Docker con il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="d1cba-103">Using the Docker VM Extension with the Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="d1cba-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d1cba-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d1cba-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="d1cba-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d1cba-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="d1cba-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="d1cba-107">[Docker](https://www.docker.com/) è uno dei più popolari approcci alla virtualizzazione che usa [contenitori Linux](http://en.wikipedia.org/wiki/LXC) invece di macchine virtuali allo scopo di isolare i dati ed eseguire i calcoli su risorse condivise.</span><span class="sxs-lookup"><span data-stu-id="d1cba-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="d1cba-108">È possibile usare l'estensione della VM Docker per l' [Agente Linux di Azure] per creare una macchina virtuale Docker che ospiti un numero qualsiasi di contenitori per le applicazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1cba-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="d1cba-109">Questo argomento descrive come creare una VM Docker dal portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="d1cba-109">This topic describes how to create a Docker VM from the Azure classic portal.</span></span> <span data-ttu-id="d1cba-110">Per scoprire come creare una macchina virtuale Docker nella riga di comando, vedere [Come usare l'estensione della VM Docker dall'interfaccia della riga di comando di Azure].</span><span class="sxs-lookup"><span data-stu-id="d1cba-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="d1cba-111">Per assistere a una discussione di alto livello sui contenitori e i relativi vantaggi, guardare questa [sessione con lavagna condivisa relativa a Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="d1cba-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-the-image-gallery"></a><span data-ttu-id="d1cba-112">Creare una nuova VM dalla Raccolta immagini</span><span class="sxs-lookup"><span data-stu-id="d1cba-112">Create a new VM from the Image Gallery</span></span>
<span data-ttu-id="d1cba-113">Il primo passaggio richiede una VM di Azure da un'immagine Linux che supporti l'estensione della VM Docker, usando un'immagine di Ubuntu 14.04 LTS dalla Raccolta immagini come immagine del server di esempio e Ubuntu 14.04 Desktop come client.</span><span class="sxs-lookup"><span data-stu-id="d1cba-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="d1cba-114">Nel portale, fare clic su **+ Nuovo** in basso a sinistra per creare una nuova istanza di VM, quindi selezionare un'immagine di Ubuntu 14.04 LTS dalle opzioni disponibili oppure dalla Raccolta immagini completa, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d1cba-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="d1cba-115">Attualmente, solo le immagini di Ubuntu 14.04 LTS successive al mese di luglio 2014 supportano l'estensione della VM Docker.</span><span class="sxs-lookup"><span data-stu-id="d1cba-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span></span>
> 
> 

![Creare una nuova immagine Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="d1cba-117">Creare i certificati Docker</span><span class="sxs-lookup"><span data-stu-id="d1cba-117">Create Docker Certificates</span></span>
<span data-ttu-id="d1cba-118">Dopo aver creato la VM, assicurarsi di aver installato Docker sul computer client</span><span class="sxs-lookup"><span data-stu-id="d1cba-118">After the VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="d1cba-119">(per informazioni dettagliate, vedere le [istruzioni di installazione di Docker](https://docs.docker.com/installation/#installation)).</span><span class="sxs-lookup"><span data-stu-id="d1cba-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="d1cba-120">Creare il certificato e i file di chiave per la comunicazione di Docker seguendo le istruzioni di [Esecuzione di Docker con https], quindi inserirli nella directory **`~/.docker`** sul computer client.</span><span class="sxs-lookup"><span data-stu-id="d1cba-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="d1cba-121">L'estensione della VM Docker nel portale attualmente richiede credenziali con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="d1cba-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="d1cba-122">Nella riga di comando, usare **`base64`** o  un altro strumento di codifica per creare argomenti con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="d1cba-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span></span> <span data-ttu-id="d1cba-123">L'esecuzione di questa operazione con un semplice set di file di chiave e certificati potrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d1cba-123">Doing this with a simple set of certificate and key files might look similar to this:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-the-docker-vm-extension"></a><span data-ttu-id="d1cba-124">Aggiungere l'estensione della VM Docker</span><span class="sxs-lookup"><span data-stu-id="d1cba-124">Add the Docker VM Extension</span></span>
<span data-ttu-id="d1cba-125">Per aggiungere l'estensione della VM Docker, individuare l'istanza della VM creata e scorrere verso il basso fino a **Estensioni** , quindi fare clic per visualizzare le estensioni della VM, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d1cba-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="d1cba-126">Questa funzionalità è supportata solo nel portale di anteprima: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="d1cba-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="d1cba-127">Aggiungere un'estensione</span><span class="sxs-lookup"><span data-stu-id="d1cba-127">Add an Extension</span></span>
<span data-ttu-id="d1cba-128">Fare clic su **+ Aggiungi** per visualizzare le potenziali estensioni che è possibile aggiungere a questa VM.</span><span class="sxs-lookup"><span data-stu-id="d1cba-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-the-docker-vm-extension"></a><span data-ttu-id="d1cba-129">Selezionare l'estensione della VM Docker</span><span class="sxs-lookup"><span data-stu-id="d1cba-129">Select the Docker VM Extension</span></span>
<span data-ttu-id="d1cba-130">Scegliere l'estensione della VM Docker che visualizza la descrizione di Docker e collegamenti importanti, quindi fare clic su **Crea** nella parte inferiore per iniziare la procedura di installazione.</span><span class="sxs-lookup"><span data-stu-id="d1cba-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="d1cba-131">Aggiungere il certificato e i file di chiave:</span><span class="sxs-lookup"><span data-stu-id="d1cba-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="d1cba-132">Nei campi modulo, immettere le versioni con codifica Base 64 del certificato della CA, del certificato del server e della chiave del server, come illustrato nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="d1cba-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="d1cba-133">Notare che (come nell'immagine precedente) il valore 2376 è inserito per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d1cba-133">Note that (as in the preceding image) the 2376 is filled in by default.</span></span> <span data-ttu-id="d1cba-134">È possibile immettere qualsiasi endpoint in questa fase, ma il passaggio successivo consiste nell'aprire l'endpoint corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d1cba-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span></span> <span data-ttu-id="d1cba-135">Se si modifica il valore predefinito, assicurarsi di aprire l'endpoint corrispondente nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d1cba-135">If you change the default, make sure to open up the matching endpoint in the next step.</span></span>
> 
> 

## <a name="add-the-docker-communication-endpoint"></a><span data-ttu-id="d1cba-136">Aggiungere l'endpoint di comunicazione del Docker</span><span class="sxs-lookup"><span data-stu-id="d1cba-136">Add the Docker Communication Endpoint</span></span>
<span data-ttu-id="d1cba-137">Quando si visualizza il gruppo di risorse creato, selezionare il gruppo di sicurezza di rete associato alla VM, quindi fare clic su **Regole di sicurezza in ingresso** per visualizzare le regole, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d1cba-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="d1cba-138">Fare clic su **+ Aggiungi** per aggiungere un'altra regola e, in caso di impostazione predefinita, immettere un nome per l'endpoint (in questo esempio **Docker**) e 2376 per 'Intervallo di porte di destinazione'.</span><span class="sxs-lookup"><span data-stu-id="d1cba-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="d1cba-139">Impostare il valore del protocollo su **TCP**, quindi fare clic su **OK** per creare la regola.</span><span class="sxs-lookup"><span data-stu-id="d1cba-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="d1cba-140">Testare il client Docker e l'host Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="d1cba-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="d1cba-141">Individuare e copiare il nome del dominio della macchina virtuale e, nella riga di comando del computer client, digitare `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` , dove *dockerextension* verrà sostituito con il sottodominio della propria macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1cba-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span></span>

<span data-ttu-id="d1cba-142">Il risultato sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d1cba-142">The result should appear similar to this:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="d1cba-143">Dopo avere completato i passaggi sopra elencati, si sarà ottenuto un host Docker completamente funzionante eseguito in una macchina virtuale di Azure e configurato per accettare connessioni remote da altri client.</span><span class="sxs-lookup"><span data-stu-id="d1cba-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="d1cba-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1cba-144">Next steps</span></span>
<span data-ttu-id="d1cba-145">È ora possibile passare alla [guida dell'utente di Docker] e usare la VM Docker.</span><span class="sxs-lookup"><span data-stu-id="d1cba-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="d1cba-146">Per automatizzare la creazione di host Docker in macchine virtuali di Azure tramite l'interfaccia della riga di comando, vedere [Come usare l'estensione della VM Docker dall'interfaccia della riga di comando di Azure]</span><span class="sxs-lookup"><span data-stu-id="d1cba-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from the Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add the Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
<span data-ttu-id="d1cba-147">[Come usare l'estensione della VM Docker dall'interfaccia della riga di comando di Azure]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span><span class="sxs-lookup"><span data-stu-id="d1cba-147">[How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span></span>
<span data-ttu-id="d1cba-148">[Agente Linux di Azure]:../agent-user-guide.md</span><span class="sxs-lookup"><span data-stu-id="d1cba-148">[Azure Linux Agent]:../agent-user-guide.md</span></span>
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md

<span data-ttu-id="d1cba-149">[Esecuzione di Docker con https]:http://docs.docker.com/articles/https/</span><span class="sxs-lookup"><span data-stu-id="d1cba-149">[Running Docker with https]:http://docs.docker.com/articles/https/</span></span>
<span data-ttu-id="d1cba-150">[guida dell'utente di Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="d1cba-150">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>
