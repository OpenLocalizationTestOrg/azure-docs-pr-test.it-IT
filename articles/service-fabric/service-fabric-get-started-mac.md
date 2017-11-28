---
title: Configurare l'ambiente di sviluppo in Mac OS X per l'interazione con Azure Service Fabric| Microsoft Docs
description: "Installare il runtime, l'SDK e gli strumenti e creare un cluster di sviluppo locale. Al termine della configurazione, sarà possibile iniziare a creare applicazioni in Mac OS X."
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
ms.openlocfilehash: 8b4fc0ab9034263418cac42ced203035e0a8fcad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="9f89c-104">Configurare l'ambiente di sviluppo in Mac OS X</span><span class="sxs-lookup"><span data-stu-id="9f89c-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f89c-105">Windows</span><span class="sxs-lookup"><span data-stu-id="9f89c-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="9f89c-106">Linux</span><span class="sxs-lookup"><span data-stu-id="9f89c-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="9f89c-107">OSX</span><span class="sxs-lookup"><span data-stu-id="9f89c-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="9f89c-108">È possibile creare applicazioni di Service Fabric da eseguire in cluster Linux usando Mac OS X. Questo articolo illustra come configurare il computer Mac per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="9f89c-108">You can build Service Fabric applications to run on Linux clusters using Mac OS X. This article covers how to set up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f89c-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9f89c-109">Prerequisites</span></span>
<span data-ttu-id="9f89c-110">Service Fabric non viene eseguito in modo nativo in OS X. Per eseguire un cluster di Service Fabric locale, viene creata una macchina virtuale Ubuntu preconfigurata con Vagrant e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="9f89c-110">Service Fabric does not run natively on OS X. To run a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="9f89c-111">Prima di iniziare, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="9f89c-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="9f89c-112">Vagrant (versione 1.8.4 o successiva)</span><span class="sxs-lookup"><span data-stu-id="9f89c-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="9f89c-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="9f89c-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="9f89c-114">È necessario usare versioni con supporto reciproco di Vagrant e VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="9f89c-114">You need to use mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="9f89c-115">Vagrant potrebbe non funzionare correttamente in una versione di VirtualBox non supportata.</span><span class="sxs-lookup"><span data-stu-id="9f89c-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-the-local-vm"></a><span data-ttu-id="9f89c-116">Creare la VM locale</span><span class="sxs-lookup"><span data-stu-id="9f89c-116">Create the local VM</span></span>
<span data-ttu-id="9f89c-117">Per creare la VM locale contenente un cluster di Service Fabric a 5 nodi, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9f89c-117">To create the local VM containing a 5-node Service Fabric cluster, perform the following steps:</span></span>

1. <span data-ttu-id="9f89c-118">Clonare il repository `Vagrantfile`</span><span class="sxs-lookup"><span data-stu-id="9f89c-118">Clone the `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="9f89c-119">Questo passaggio scarica il file `Vagrantfile` contenente la configurazione della VM con il percorso da cui viene scaricata la VM.</span><span class="sxs-lookup"><span data-stu-id="9f89c-119">This steps bring downs the file `Vagrantfile` containing the VM configuration along with the location the VM is downloaded from.</span></span>

2. <span data-ttu-id="9f89c-120">Passare al clone locale del repository</span><span class="sxs-lookup"><span data-stu-id="9f89c-120">Navigate to the local clone of the repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="9f89c-121">(Facoltativo) Modificare le impostazioni predefinite della VM</span><span class="sxs-lookup"><span data-stu-id="9f89c-121">(Optional) Modify the default VM settings</span></span>

    <span data-ttu-id="9f89c-122">Per impostazione predefinita, la VM locale è configurata come segue:</span><span class="sxs-lookup"><span data-stu-id="9f89c-122">By default, the local VM is configured as follows:</span></span>

   * <span data-ttu-id="9f89c-123">3 GB di memoria allocati</span><span class="sxs-lookup"><span data-stu-id="9f89c-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="9f89c-124">Rete host privata configurata all'indirizzo IP 192.168.50.50 che consente il pass-through del traffico dall'host Mac</span><span class="sxs-lookup"><span data-stu-id="9f89c-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from the Mac host</span></span>

     <span data-ttu-id="9f89c-125">È possibile modificare una di queste impostazioni o aggiungere altre opzioni di configurazione della VM in `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="9f89c-125">You can change either of these settings or add other configuration to the VM in the `Vagrantfile`.</span></span> <span data-ttu-id="9f89c-126">Per l'elenco completo delle opzioni di configurazione, vedere la [documentazione di Vagrant](http://www.vagrantup.com/docs) .</span><span class="sxs-lookup"><span data-stu-id="9f89c-126">See the [Vagrant documentation](http://www.vagrantup.com/docs) for the full list of configuration options.</span></span>
4. <span data-ttu-id="9f89c-127">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="9f89c-127">Create the VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="9f89c-128">In questo passaggio viene scaricata e avviata in locale l'immagine di VM preconfigurata e vi viene quindi configurato un cluster di Service Fabric locale.</span><span class="sxs-lookup"><span data-stu-id="9f89c-128">This step downloads the preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="9f89c-129">È probabile che questo passaggio richieda alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9f89c-129">You should expect it to take a few minutes.</span></span> <span data-ttu-id="9f89c-130">Se la configurazione ha esito positivo, nell'output verrà visualizzato un messaggio che indica che è in corso l'avvio del cluster.</span><span class="sxs-lookup"><span data-stu-id="9f89c-130">If setup completes successfully, you see a message in the output indicating that the cluster is starting up.</span></span>

    ![Avvio della configurazione del cluster dopo il provisioning della VM][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="9f89c-132">Se il download della VM impiega troppo tempo, è possibile scaricarla con wget o curl oppure un browser passando al collegamento specificato da **config.vm.box_url** nel file `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="9f89c-132">If the VM download is taking a long time, you can download it using wget or curl or through a browser by navigating to the link specified by **config.vm.box_url** in the file `Vagrantfile`.</span></span> <span data-ttu-id="9f89c-133">Dopo averla scaricata in locale, modificare `Vagrantfile` in modo che punti al percorso locale in cui si è scaricata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="9f89c-133">After downloading it locally, edit `Vagrantfile` to point to the local path where you downloaded the image.</span></span> <span data-ttu-id="9f89c-134">Se, ad esempio, si è scaricata l'immagine in /home/users/test/azureservicefabric.tp8.box, impostare **config.vm.box_url** su tale percorso.</span><span class="sxs-lookup"><span data-stu-id="9f89c-134">For example if you downloaded the image to /home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** to that path.</span></span>
    >

5. <span data-ttu-id="9f89c-135">Verificare che il cluster sia stato configurato correttamente passando a Service Fabric Explorer all'indirizzo http://192.168.50.50:19080/Explorer, presupponendo che sia stato mantenuto l'IP predefinito della rete privata.</span><span class="sxs-lookup"><span data-stu-id="9f89c-135">Test that the cluster has been set up correctly by navigating to Service Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept the default private network IP).</span></span>

    ![Visualizzazione di Service Fabric Explorer dal Mac host][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="9f89c-137">Creare un'applicazione in Mac tramite Yeoman</span><span class="sxs-lookup"><span data-stu-id="9f89c-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="9f89c-138">Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="9f89c-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="9f89c-139">Seguire questa procedura per assicurarsi che nella macchina virtuale sia disponibile il generatore di modelli Yeoman di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9f89c-139">Please follow the steps below to ensure you have the Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="9f89c-140">È necessario che Node.js e NPM siano installati nel computer Mac.</span><span class="sxs-lookup"><span data-stu-id="9f89c-140">You need to have Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="9f89c-141">In caso contrario, è possibile installare Node.js e NPM tramite Homebrew usando il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="9f89c-141">If not you can install Node.js and NPM using Homebrew using the following.</span></span> <span data-ttu-id="9f89c-142">Per verificare le versioni di Node.js e NPM installate nel computer Mac, è possibile usare l'opzione ``-v``.</span><span class="sxs-lookup"><span data-stu-id="9f89c-142">To check the versions of Node.js and NPM installed on your Mac, you can use the ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="9f89c-143">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="9f89c-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="9f89c-144">Installare il generatore Yeoman da usare, seguendo la procedura disponibile nella [documentazione](service-fabric-get-started-linux.md) introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9f89c-144">Install the Yeoman generator you want to use, following the steps in the getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="9f89c-145">Per creare applicazioni Service Fabric tramite Yeoman, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="9f89c-145">To create Service Fabric Applications using Yeoman, follow the steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="9f89c-146">Per compilare un'applicazione Java per Service Fabric nel computer Mac, è necessario che JDK 1.8 e Gradle siano installati nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9f89c-146">To build a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on the machine.</span></span>


## <a name="install-the-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="9f89c-147">Installare il plug-in Service Fabric per Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="9f89c-147">Install the Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="9f89c-148">Service Fabric offre un plug-in per **Eclipse Neon per l'ambiente IDE Java** che può semplificare il processo di creazione, compilazione e distribuzione di servizi Java.</span><span class="sxs-lookup"><span data-stu-id="9f89c-148">Service Fabric provides a plugin for the **Eclipse Neon for Java IDE** that can simplify the process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="9f89c-149">È possibile seguire la procedura di installazione illustrata in questa [documentazione](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) generale sull'installazione e l'aggiornamento del plug-in Service Fabric Eclipse.</span><span class="sxs-lookup"><span data-stu-id="9f89c-149">You can follow the installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="9f89c-150">Per impostazione predefinita, viene supportato l'indirizzo IP predefinito, come indicato in ``Vagrantfile`` nel file``Local.json`` dell'applicazione generata.</span><span class="sxs-lookup"><span data-stu-id="9f89c-150">By default we support the default IP as mentioned in the ``Vagrantfile`` in the ``Local.json`` of the generated application.</span></span> <span data-ttu-id="9f89c-151">Se si modifica tale impostazione e si distribuisce Vagrant con un indirizzo IP diverso, aggiornare anche l'indirizzo IP corrispondente nel file ``Local.json`` dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9f89c-151">In case you change that and deploy Vagrant with a different IP, please update the corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f89c-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9f89c-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="9f89c-153">Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando Yeoman</span><span class="sxs-lookup"><span data-stu-id="9f89c-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* <span data-ttu-id="9f89c-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Creare e distribuire la prima applicazione Java di Service Fabric in Linux usando il plug-in Service Fabric per Eclipse)</span><span class="sxs-lookup"><span data-stu-id="9f89c-154">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* [<span data-ttu-id="9f89c-155">Creare un cluster di Service Fabric nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9f89c-155">Create a Service Fabric cluster in the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="9f89c-156">Creare un cluster di Service Fabric con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f89c-156">Create a Service Fabric cluster using the Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="9f89c-157">Informazioni sul modello applicativo di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9f89c-157">Understand the Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
