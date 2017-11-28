---
title: Estensione della macchina virtuale Docker per Linux aaaUsing | Documenti Microsoft
description: Viene descritto Docker e alle estensioni di macchine virtuali di Azure hello e come macchine virtuali di Azure che sono host docker utilizzando toocreate hello CLI di Azure nel modello di distribuzione classica.
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
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="472ae-103">Con estensione della macchina virtuale Docker hello hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="472ae-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="472ae-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="472ae-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="472ae-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="472ae-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="472ae-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="472ae-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="472ae-107">[Docker](https://www.docker.com/) è uno dei hello approcci di virtualizzazione più diffusi che utilizza [contenitori di Linux](http://en.wikipedia.org/wiki/LXC) anziché le macchine virtuali come modalità di isolamento dei dati e di elaborazione per le risorse condivise.</span><span class="sxs-lookup"><span data-stu-id="472ae-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="472ae-108">È possibile utilizzare l'estensione della macchina virtuale Docker hello gestiti da [agente Linux di Azure] toocreate una macchina virtuale Docker che ospita qualsiasi numero di contenitori per le applicazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="472ae-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="472ae-109">In questo argomento viene descritto come toocreate una macchina virtuale Docker da hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="472ae-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="472ae-110">toosee toocreate una macchina virtuale Docker hello riga di comando, vedere [come toouse hello estensione della macchina virtuale Docker dall'interfaccia della riga di comando di Azure (Azure CLI) hello].</span><span class="sxs-lookup"><span data-stu-id="472ae-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="472ae-111">toosee una descrizione di alto livello dei contenitori e i relativi vantaggi, vedere hello [Docker elevato livello di lavagna](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="472ae-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="472ae-112">Creare una nuova macchina virtuale da hello raccolta immagini</span><span class="sxs-lookup"><span data-stu-id="472ae-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="472ae-113">primo passaggio Hello richiede una macchina virtuale di Azure da un'immagine Linux che supporta hello estensione della macchina virtuale Docker, utilizzando un'immagine Ubuntu 14.04 LTS da hello raccolta immagini come un'immagine server di esempio e Ubuntu 14.04 Desktop come un client.</span><span class="sxs-lookup"><span data-stu-id="472ae-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="472ae-114">Nel portale di hello, fare clic su **+ nuovo** in hello in basso a sinistra angolo toocreate una nuova istanza della macchina virtuale e selezionare un'immagine Ubuntu 14.04 LTS selezioni hello disponibile o da hello completare la raccolta di immagini, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="472ae-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="472ae-115">Attualmente, solo le immagini Ubuntu 14.04 LTS più recenti di luglio 2014 supportano hello estensione della macchina virtuale Docker.</span><span class="sxs-lookup"><span data-stu-id="472ae-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Creare una nuova immagine Ubuntu](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="472ae-117">Creare i certificati Docker</span><span class="sxs-lookup"><span data-stu-id="472ae-117">Create Docker Certificates</span></span>
<span data-ttu-id="472ae-118">Dopo avere hello che VM è stato creato, assicurarsi che Docker sia installato nel computer client.</span><span class="sxs-lookup"><span data-stu-id="472ae-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="472ae-119">(per informazioni dettagliate, vedere le [istruzioni di installazione di Docker](https://docs.docker.com/installation/#installation)).</span><span class="sxs-lookup"><span data-stu-id="472ae-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="472ae-120">Creare i file di certificato e la chiave per la comunicazione di Docker in base troppo hello[in esecuzione di Docker con https] e posizionarli nel hello  **`~/.docker`**  directory sul computer client.</span><span class="sxs-lookup"><span data-stu-id="472ae-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="472ae-121">attualmente, Hello Docker estensione della macchina virtuale nel portale di hello richiede credenziali con codificata base 64.</span><span class="sxs-lookup"><span data-stu-id="472ae-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="472ae-122">Riga di comando hello, utilizzare  **`base64`**  o preferito di un'altra codifica negli argomenti strumento toocreate con codifica base64.</span><span class="sxs-lookup"><span data-stu-id="472ae-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="472ae-123">Eseguire questa operazione con un semplice set di file di certificato e la chiave potrebbe essere toothis simile:</span><span class="sxs-lookup"><span data-stu-id="472ae-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

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

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="472ae-124">Aggiungere l'estensione della macchina virtuale Docker hello</span><span class="sxs-lookup"><span data-stu-id="472ae-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="472ae-125">tooadd hello estensione della macchina virtuale Docker, individuare l'istanza VM hello creata e scorrere verso il basso troppo**estensioni** e farvi clic sopra toobring estensioni VM, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="472ae-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="472ae-126">Questa funzionalità è supportata nel portale di anteprima hello solo: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="472ae-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="472ae-127">Aggiungere un'estensione</span><span class="sxs-lookup"><span data-stu-id="472ae-127">Add an Extension</span></span>
<span data-ttu-id="472ae-128">Fare clic su hello **+ Aggiungi** toodisplay hello possibili estensioni VM è possibile aggiungere toothis macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="472ae-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="472ae-129">Selezionare l'estensione della macchina virtuale Docker hello</span><span class="sxs-lookup"><span data-stu-id="472ae-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="472ae-130">Scegliere l'estensione della macchina virtuale Docker, che comporta la descrizione di Docker hello e collegamenti importanti, hello e quindi fare clic su **crea** alla procedura di installazione hello toobegin hello inferiore.</span><span class="sxs-lookup"><span data-stu-id="472ae-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="472ae-131">Aggiungere il certificato e i file di chiave:</span><span class="sxs-lookup"><span data-stu-id="472ae-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="472ae-132">Nei campi modulo hello, immettere le versioni hello con codifica base64 del certificato CA, il certificato Server e la chiave del Server, come illustrato nella seguente immagine hello.</span><span class="sxs-lookup"><span data-stu-id="472ae-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="472ae-133">Si noti che (ad esempio hello prima immagine) hello 2376 viene compilato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="472ae-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="472ae-134">È possibile immettere qui qualsiasi endpoint, ma passaggio successivo hello sarà tooopen backup hello endpoint corrispondente.</span><span class="sxs-lookup"><span data-stu-id="472ae-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="472ae-135">Se si modifica l'impostazione predefinita di hello, assicurarsi che tooopen backup hello corrispondenti endpoint nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="472ae-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="472ae-136">Aggiungere hello Endpoint di comunicazione di Docker</span><span class="sxs-lookup"><span data-stu-id="472ae-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="472ae-137">Quando si visualizza il gruppo di risorse hello è stato creato, selezionare il gruppo di sicurezza di rete associato con la macchina virtuale hello e fare clic su **le regole di sicurezza in ingresso** tooview hello regole come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="472ae-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="472ae-138">Fare clic su **+ Aggiungi** tooadd un'altra regola, nel caso predefinito hello, immettere un nome per l'endpoint di hello (in questo esempio, **Docker**) e 2376 'intervallo porte di destinazione'.</span><span class="sxs-lookup"><span data-stu-id="472ae-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="472ae-139">Impostare con valore di protocollo hello **TCP**, fare clic su **OK** regola hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="472ae-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="472ae-140">Testare il client Docker e l'host Docker di Azure</span><span class="sxs-lookup"><span data-stu-id="472ae-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="472ae-141">Individuare e copiare hello nome di dominio della macchina virtuale e nella riga di comando hello del computer client, tipo `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (dove *dockerextension* viene sostituito da hello sottodominio per la macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="472ae-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="472ae-142">risultato Hello dovrebbe apparire simile toothis:</span><span class="sxs-lookup"><span data-stu-id="472ae-142">hello result should appear similar toothis:</span></span>

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

<span data-ttu-id="472ae-143">Dopo aver completato hello sopra passaggi, è ora un host Docker completamente funzionale in esecuzione in una macchina virtuale di Azure, configurato toobe connesso tooremotely da altri client.</span><span class="sxs-lookup"><span data-stu-id="472ae-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="472ae-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="472ae-144">Next steps</span></span>
<span data-ttu-id="472ae-145">Si è pronti toogo toohello [manuale dell'utente Docker] e usare la macchina virtuale Docker.</span><span class="sxs-lookup"><span data-stu-id="472ae-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="472ae-146">Se si desidera tooautomate creazione host Docker in macchine virtuali di Azure tramite l'interfaccia della riga di comando, vedere [come toouse hello estensione della macchina virtuale Docker dall'interfaccia della riga di comando di Azure (Azure CLI) hello]</span><span class="sxs-lookup"><span data-stu-id="472ae-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
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
[come toouse hello estensione della macchina virtuale Docker dall'interfaccia della riga di comando di Azure (Azure CLI) hello]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[agente Linux di Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[in esecuzione di Docker con https]:http://docs.docker.com/articles/https/
[manuale dell'utente Docker]:https://docs.docker.com/userguide/
