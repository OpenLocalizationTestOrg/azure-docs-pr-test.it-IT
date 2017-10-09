---
title: aaaSet dell'ambiente di sviluppo in Mac OS X toowork con Azure Service Fabric | Documenti Microsoft
description: "Installare il runtime di hello, SDK e strumenti e creare un cluster di sviluppo locale. Dopo aver completato il programma di installazione, sarà pronto toobuild applicazioni su Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="69af0-104">Configurare l'ambiente di sviluppo in Mac OS X</span><span class="sxs-lookup"><span data-stu-id="69af0-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69af0-105">Windows</span><span class="sxs-lookup"><span data-stu-id="69af0-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="69af0-106">Linux</span><span class="sxs-lookup"><span data-stu-id="69af0-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="69af0-107">OSX</span><span class="sxs-lookup"><span data-stu-id="69af0-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="69af0-108">È possibile compilare toorun applicazioni di Service Fabric su cluster Linux utilizzando Mac OS X. Questo articolo descrive come tooset backup Mac per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="69af0-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69af0-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="69af0-109">Prerequisites</span></span>
<span data-ttu-id="69af0-110">Infrastruttura del servizio non viene eseguita in modo nativo su OS X. toorun un cluster di Service Fabric locale, offre una macchina virtuale di Ubuntu preconfigurata con Vagrant e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="69af0-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="69af0-111">Prima di iniziare, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="69af0-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="69af0-112">Vagrant (versione 1.8.4 o successiva)</span><span class="sxs-lookup"><span data-stu-id="69af0-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="69af0-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="69af0-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="69af0-114">È necessario toouse reciprocamente supportate versioni Vagrant e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="69af0-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="69af0-115">Vagrant potrebbe non funzionare correttamente in una versione di VirtualBox non supportata.</span><span class="sxs-lookup"><span data-stu-id="69af0-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="69af0-116">Creare hello macchina virtuale locale</span><span class="sxs-lookup"><span data-stu-id="69af0-116">Create hello local VM</span></span>
<span data-ttu-id="69af0-117">toocreate hello macchina virtuale locale che contiene un cluster di Service Fabric 5 nodi, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="69af0-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="69af0-118">Hello clone `Vagrantfile` repository</span><span class="sxs-lookup"><span data-stu-id="69af0-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="69af0-119">Questa procedura porta elenchi hello file `Vagrantfile` contenente hello VM configurazione insieme hello percorso hello VM viene scaricato dal.</span><span class="sxs-lookup"><span data-stu-id="69af0-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="69af0-120">Passare toohello clone locale del repository hello</span><span class="sxs-lookup"><span data-stu-id="69af0-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="69af0-121">(Facoltativo) Modificare le impostazioni di macchina virtuale di hello predefinite</span><span class="sxs-lookup"><span data-stu-id="69af0-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="69af0-122">Per impostazione predefinita, hello macchina virtuale locale è configurato come segue:</span><span class="sxs-lookup"><span data-stu-id="69af0-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="69af0-123">3 GB di memoria allocati</span><span class="sxs-lookup"><span data-stu-id="69af0-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="69af0-124">Rete privata host configurate all'indirizzo IP 192.168.50.50 abilitazione pass-through di traffico da hello Mac host</span><span class="sxs-lookup"><span data-stu-id="69af0-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="69af0-125">È possibile modificare queste impostazioni o aggiungere altri toohello configurazione macchina virtuale in hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="69af0-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="69af0-126">Vedere hello [documentazione Vagrant](http://www.vagrantup.com/docs) per l'elenco completo di hello delle opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="69af0-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="69af0-127">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="69af0-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="69af0-128">Questo passaggio Scarica l'immagine di macchina virtuale hello preconfigurato, in locale e quindi impostare un'infrastruttura locale di servizio del cluster all'avvio.</span><span class="sxs-lookup"><span data-stu-id="69af0-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="69af0-129">Si dovrebbero e tootake qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="69af0-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="69af0-130">Se il programma di installazione viene completata correttamente, viene visualizzato un messaggio nell'output di hello che indica il che avvio di tale cluster hello.</span><span class="sxs-lookup"><span data-stu-id="69af0-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![Avvio della configurazione del cluster dopo il provisioning della VM][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="69af0-132">Se il download VM hello richiede molto tempo, è possibile scaricare con wget o curl o tramite un browser passando toohello collegamento specificato dal **config.vm.box_url** nel file hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="69af0-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="69af0-133">Dopo aver scaricato localmente, modificare `Vagrantfile` toopoint toohello percorso locale in cui è stato scaricato immagine hello.</span><span class="sxs-lookup"><span data-stu-id="69af0-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="69af0-134">Ad esempio se è stato scaricato hello immagine too/home/users/test/azureservicefabric.tp8.box, quindi impostata **config.vm.box_url** toothat percorso.</span><span class="sxs-lookup"><span data-stu-id="69af0-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="69af0-135">Verificare che hello cluster è stato configurato correttamente passando tooService Fabric Explorer in http://192.168.50.50:19080/Esplora (presupponendo che si tiene hello predefinito IP di rete privata).</span><span class="sxs-lookup"><span data-stu-id="69af0-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Visualizzato dall'host hello Mac Service Fabric Explorer][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="69af0-137">Creare un'applicazione in Mac tramite Yeoman</span><span class="sxs-lookup"><span data-stu-id="69af0-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="69af0-138">Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="69af0-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="69af0-139">Eseguire procedure hello sotto tooensure che si dispone di hello Service Fabric modello yeoman generatore utilizzo nel computer.</span><span class="sxs-lookup"><span data-stu-id="69af0-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="69af0-140">È necessario toohave Node.js e NPM installato è mac.</span><span class="sxs-lookup"><span data-stu-id="69af0-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="69af0-141">Se non è possibile installare Node.js e NPM utilizzando Homebrew con hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="69af0-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="69af0-142">versioni di hello toocheck di Node.js e NPM installata nel Mac, è possibile utilizzare hello ``-v`` opzione.</span><span class="sxs-lookup"><span data-stu-id="69af0-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="69af0-143">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="69af0-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="69af0-144">Installare hello Yeoman generatore desiderato toouse, i passaggi hello hello Introduzione [documentazione](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="69af0-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="69af0-145">Applicazioni di infrastruttura servizio toocreate utilizzando Yeoman, seguire i passaggi hello-</span><span class="sxs-lookup"><span data-stu-id="69af0-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="69af0-146">toobuild un'applicazione di servizio Fabric Java su Mac, è necessario - JDK 1.8 e installato nel computer di hello Gradle.</span><span class="sxs-lookup"><span data-stu-id="69af0-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="69af0-147">Installazione di plug-in Service Fabric hello per Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="69af0-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="69af0-148">Service Fabric fornisce un plug-in per hello **Neon Eclipse IDE Java** che può semplificare il processo di hello di creazione, compilazione e distribuzione di servizi di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="69af0-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="69af0-149">È possibile seguire i passaggi di installazione hello indicati in questa generale [documentazione](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) sull'installazione o aggiornamento plug-in servizi dell'infrastruttura Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69af0-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="69af0-150">Per impostazione predefinita è supporta hello predefinito IP come indicato in hello ``Vagrantfile`` in hello ``Local.json`` dell'applicazione hello generato.</span><span class="sxs-lookup"><span data-stu-id="69af0-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="69af0-151">Nel caso in cui si modifica e si distribuiscono Vagrant con un indirizzo IP diverso, aggiornare hello IP corrispondente in ``Local.json`` anche dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="69af0-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69af0-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69af0-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="69af0-153">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="69af0-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="69af0-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse)</span><span class="sxs-lookup"><span data-stu-id="69af0-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="69af0-155">Creare un cluster di Service Fabric in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="69af0-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="69af0-156">Creare un cluster di Service Fabric utilizzando hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69af0-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="69af0-157">Comprendere il modello di applicazione del hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="69af0-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
