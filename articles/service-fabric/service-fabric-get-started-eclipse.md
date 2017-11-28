---
title: aaaAzure Service Fabric plug-in per Eclipse | Documenti Microsoft
description: Introduzione a hello Service Fabric plug-in per Eclipse.
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
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="35ce8-103">Plug-in Service Fabric per lo sviluppo di applicazioni Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="35ce8-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="35ce8-104">Eclipse è uno dei più diffuse hello integrato (IDE) di ambienti di sviluppo per gli sviluppatori Java.</span><span class="sxs-lookup"><span data-stu-id="35ce8-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="35ce8-105">In questo articolo viene descritto come tooset backup il toowork ambiente di sviluppo Eclipse con Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="35ce8-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="35ce8-106">Scopri hello tooinstall Service Fabric plug-in, creare un'applicazione di Service Fabric e distribuire il Service Fabric applicazione tooa locale o remoto dell'infrastruttura del servizio cluster in Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="35ce8-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="35ce8-107">Installare o aggiornare hello plug-in Eclipse Neon di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="35ce8-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="35ce8-108">È possibile installare un plug-in Service Fabric in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="35ce8-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="35ce8-109">Hello plug-in consente di semplificare il processo di hello della compilazione e distribuzione di servizi di linguaggio.</span><span class="sxs-lookup"><span data-stu-id="35ce8-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="35ce8-110">Verificare di disporre di più recente di Eclipse Neon hello e hello versione Buildship (1.0.17 o una versione successiva) installato:</span><span class="sxs-lookup"><span data-stu-id="35ce8-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="35ce8-111">versioni di hello toocheck dei componenti installati, in Eclipse Neon, andare troppo**Guida** > **i dettagli di installazione**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="35ce8-112">vedere tooupdate Buildship, [Buildship Eclipse: Plug-in Eclipse per Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="35ce8-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="35ce8-113">toocheck per e installa gli aggiornamenti per Neon Eclipse, andare troppo**Guida** > **Controlla aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="35ce8-114">hello tooinstall Service Fabric plug-in, in Eclipse Neon, andare troppo**Guida** > **installa nuovo Software**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="35ce8-115">In hello **utilizzano** immettere **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="35ce8-116">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-116">Click **Add**.</span></span>

         ![Plug-in Service Fabric per Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="35ce8-118">Selezionare i plug-in Service Fabric hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="35ce8-119">Completare i passaggi di installazione hello e quindi accettare condizioni di licenza Software Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="35ce8-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="35ce8-120">Se si dispone già di hello Service Fabric di plug-in installato, accertarsi di avere la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="35ce8-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="35ce8-121">toocheck per gli aggiornamenti disponibili, andare troppo**Guida** > **i dettagli di installazione**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="35ce8-122">Nell'elenco di hello del plug-in installati, selezionare Service Fabric e quindi fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="35ce8-123">Verranno installati gli aggiornamenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="35ce8-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="35ce8-124">Se l'installazione o aggiornamento hello plug-in Service Fabric è lenta, potrebbe essere dovuto impostazione Eclipse tooan.</span><span class="sxs-lookup"><span data-stu-id="35ce8-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="35ce8-125">Eclipse raccoglie i metadati in tutti i siti tooupdate modifiche che sono registrati con l'istanza di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="35ce8-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="35ce8-126">toospeed backup processo hello di rilevamento e installazione di un aggiornamento di Service Fabric plug-in, andare troppo**siti Software disponibili**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="35ce8-127">Deselezionare le caselle di controllo hello per tutti i siti, ad eccezione di hello quello che punta toohello percorso plug-in Service Fabric (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="35ce8-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="35ce8-128">Creare un'applicazione di Service Fabric in Eclipse</span><span class="sxs-lookup"><span data-stu-id="35ce8-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="35ce8-129">In Eclipse Neon, andare troppo**File** > **New** > **altri**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="35ce8-130">Selezionare **Service Fabric Project**, quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="35ce8-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Pagina 1 del nuovo progetto di Service Fabric][create-application/p1]

2.  <span data-ttu-id="35ce8-132">Immettere un nome per il progetto e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="35ce8-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Pagina 2 del nuovo progetto di Service Fabric][create-application/p2]

3.  <span data-ttu-id="35ce8-134">Nell'elenco dei modelli di hello selezionare **modello di servizio**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="35ce8-135">Selezionare il tipo di modello di servizio (Actor, Stateless, Container, or Guest Binary) e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="35ce8-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Pagina 3 del nuovo progetto di Service Fabric][create-application/p3]

4.  <span data-ttu-id="35ce8-137">Immettere il nome di servizio hello e dettagli del servizio e quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Pagina 4 del nuovo progetto di Service Fabric][create-application/p4]

5. <span data-ttu-id="35ce8-139">Quando si crea il primo progetto, Service Fabric in hello **Open Perspective associata** la finestra di dialogo, fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Pagina 5 del nuovo progetto di Service Fabric][create-application/p5]

6.  <span data-ttu-id="35ce8-141">L'aspetto del nuovo progetto sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="35ce8-141">Your new project looks like this:</span></span>

    ![Pagina 6 del nuovo progetto di Service Fabric][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="35ce8-143">Creare e distribuire un'applicazione di Service Fabric in Eclipse</span><span class="sxs-lookup"><span data-stu-id="35ce8-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="35ce8-144">Fare clic con il pulsante destro del mouse sulla nuova applicazione di Service Fabric, quindi scegliere **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu di scelta rapida di Service Fabric][publish/RightClick]

2. <span data-ttu-id="35ce8-146">Nel sottomenu hello, selezionare l'opzione hello desiderata:</span><span class="sxs-lookup"><span data-stu-id="35ce8-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="35ce8-147">Fare clic su un'applicazione hello toobuild senza la pulizia, **applicazione compilazione**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="35ce8-148">Fare clic su una compilazione pulita dell'applicazione hello, toodo **ricompilare applicazione**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="35ce8-149">Fare clic su un'applicazione hello tooclean di artefatti compilati, **applicazione pulita**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="35ce8-150">Da questo menu è anche possibile distribuire, annullare la distribuzione e pubblicare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="35ce8-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="35ce8-151">cluster locale tooyour toodeploy, fare clic su **distribuire applicazione**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="35ce8-152">In hello **pubblica l'applicazione** finestra di dialogo, selezionare un profilo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="35ce8-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="35ce8-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="35ce8-153">**Local.json**</span></span>
        -  <span data-ttu-id="35ce8-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="35ce8-154">**Cloud.json**</span></span>

     <span data-ttu-id="35ce8-155">Questi file JavaScript Object Notation (JSON) le informazioni (ad esempio endpoint della connessione e informazioni di sicurezza) che sono necessario tooconnect tooyour locale o cloud (Azure).</span><span class="sxs-lookup"><span data-stu-id="35ce8-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Menu di pubblicazione di Service Fabric][publish/Publish]

<span data-ttu-id="35ce8-157">Un modo alternativo di toodeploy l'applicazione di Service Fabric è usando Eclipse configurazioni di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="35ce8-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="35ce8-158">Andare troppo**eseguire** > **eseguire configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="35ce8-159">In **Gradle progetto**selezionare hello **ServiceFabricDeployer** configurazione di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="35ce8-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="35ce8-160">Nel riquadro di destra hello, su hello **argomenti** scheda per **publishProfile**selezionare **locale** o **cloud**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="35ce8-161">valore predefinito di Hello è **locale**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-161">hello default is **local**.</span></span> <span data-ttu-id="35ce8-162">tooa toodeploy remoto o un cloud di cluster **cloud**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="35ce8-163">che informazioni corrette hello viene popolate in hello tooensure profili di pubblicazione, modificare **Local.json** o **Cloud.json** in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="35ce8-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="35ce8-164">È possibile aggiungere o aggiornare i dettagli degli endpoint e delle credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="35ce8-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="35ce8-165">Verificare che **la Directory di lavoro** punta applicazione toohello da toodeploy.</span><span class="sxs-lookup"><span data-stu-id="35ce8-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="35ce8-166">toochange hello applicazione, fare clic su hello **dell'area di lavoro** e quindi selezionare un'applicazione hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="35ce8-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="35ce8-167">Fare clic su **Apply** (Applica) e quindi su **Run** (Esegui).</span><span class="sxs-lookup"><span data-stu-id="35ce8-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="35ce8-168">L'applicazione verrà compilata e distribuita dopo alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="35ce8-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="35ce8-169">È possibile monitorare lo stato di distribuzione hello in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="35ce8-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="35ce8-170">Aggiungere un tooyour di servizio dell'applicazione di Service Fabric di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="35ce8-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="35ce8-171">un'infrastruttura a servizio tooan esistente Service Fabric applicazione di servizio, tooadd hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="35ce8-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="35ce8-172">Progetto di hello pulsante destro del mouse si desidera che un servizio tooadd e quindi fare clic su **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Pagina 1 dell'aggiunta di un servizio di Service Fabric][add-service/p1]

2.  <span data-ttu-id="35ce8-174">Fare clic su **Aggiungi servizio Service Fabric**, e hello completo di set di passaggi tooadd un progetto di servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="35ce8-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="35ce8-175">Modello di servizio selezionare hello desidera tooadd tooyour progetto e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Pagina 2 dell'aggiunta di un servizio di Service Fabric][add-service/p2]

4.  <span data-ttu-id="35ce8-177">Immettere il nome di servizio hello (e altri dettagli, in base alle esigenze) e quindi fare clic su hello **Aggiungi servizio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="35ce8-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Pagina 3 dell'aggiunta di un servizio di Service Fabric][add-service/p3]

5.  <span data-ttu-id="35ce8-179">Dopo aver aggiunto il servizio di hello, la struttura del progetto complessivo è simile toohello progetto seguente:</span><span class="sxs-lookup"><span data-stu-id="35ce8-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Pagina 4 dell'aggiunta di un servizio di Service Fabric][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="35ce8-181">Modifica versioni del manifesto dell'applicazione Java di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="35ce8-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="35ce8-182">versioni di manifesto tooedit, fare clic con il pulsante destro sul progetto hello, andare troppo**Service Fabric** e selezionare **modifica manifesto versioni...**  da hello menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="35ce8-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="35ce8-183">Nella procedura guidata hello, è possibile aggiornare le versioni di manifesto hello manifesto dell'applicazione, manifesto del servizio e hello per **codice**, **Config** e **dati** pacchetti.</span><span class="sxs-lookup"><span data-stu-id="35ce8-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="35ce8-184">Se si seleziona l'opzione hello **aggiornare automaticamente versioni dell'applicazione e servizio** e quindi di aggiornare una versione, le versioni di manifesto hello quindi verranno aggiornate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="35ce8-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="35ce8-185">toogive un esempio, innanzitutto selezionare hello casella di controllo, quindi hello aggiornamento versione **codice** versione da visualizzata sarà 0.0.0 too0.0.1 e fare clic su **fine**, quindi service versione del manifesto e manifesto dell'applicazione versione sarà too0.0.1 aggiornate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="35ce8-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="35ce8-186">Aggiornare l'applicazione Java di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="35ce8-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="35ce8-187">Per uno scenario di aggiornamento, ad esempio creato hello **App1** progetto tramite hello Service Fabric plug-in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="35ce8-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="35ce8-188">È distribuito usando hello toocreate di plug-in un'applicazione denominata **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="35ce8-189">tipo di applicazione Hello è **App1AppicationType**, e versione dell'applicazione hello è 1.0.</span><span class="sxs-lookup"><span data-stu-id="35ce8-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="35ce8-190">A questo punto, si desidera tooupgrade dell'applicazione senza interrompere la disponibilità.</span><span class="sxs-lookup"><span data-stu-id="35ce8-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="35ce8-191">In primo luogo, apportare le modifiche dell'applicazione tooyour e quindi ricompilare il servizio di hello modificato.</span><span class="sxs-lookup"><span data-stu-id="35ce8-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="35ce8-192">Hello aggiornamento modifica il file manifesto del servizio (ServiceManifest.xml) con versioni aggiornata di hello per servizio hello (e codice, configurazione o dati, se pertinente).</span><span class="sxs-lookup"><span data-stu-id="35ce8-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="35ce8-193">Inoltre, modificare il manifesto dell'applicazione hello (ApplicationManifest.xml) con numero di versione di hello aggiornato per un'applicazione hello e hello servizio modificato.</span><span class="sxs-lookup"><span data-stu-id="35ce8-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="35ce8-194">tooupgrade l'applicazione mediante Neon Eclipse, è possibile creare un profilo di configurazione di esecuzione duplicati.</span><span class="sxs-lookup"><span data-stu-id="35ce8-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="35ce8-195">Utilizzare quindi tooupgrade l'applicazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="35ce8-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="35ce8-196">Andare troppo**eseguire** > **eseguire configurazioni**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="35ce8-197">Nel riquadro di sinistra hello, fare clic su hello piccola freccia toohello sinistro **Gradle progetto**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="35ce8-198">Fare clic con il pulsante destro del mouse su **ServiceFabricDeployer** e quindi scegliere **Duplicate** (Duplica).</span><span class="sxs-lookup"><span data-stu-id="35ce8-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="35ce8-199">Specificare un nuovo nome per questa configurazione, ad esempio **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="35ce8-200">Nel riquadro di destra hello, su hello **argomenti** modificare **- ipconfig = 'Distribuisci'** troppo**- ipconfig = 'Aggiorna'**, quindi fare clic su **applica**.</span><span class="sxs-lookup"><span data-stu-id="35ce8-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="35ce8-201">Questo processo crea e salva un profilo di configurazione di esecuzione è possibile utilizzare qualsiasi tooupgrade ora l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="35ce8-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="35ce8-202">Ottiene anche hello applicazione aggiornata tipo più recente dal file manifesto dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="35ce8-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="35ce8-203">aggiornamento dell'applicazione Hello richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="35ce8-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="35ce8-204">È possibile monitorare l'aggiornamento dell'applicazione hello in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="35ce8-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="35ce8-205">La migrazione precedente toobe di applicazioni Java di infrastruttura del servizio utilizzato con Maven</span><span class="sxs-lookup"><span data-stu-id="35ce8-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="35ce8-206">È stato spostato nella librerie di Service Fabric Java recente dal repository tooMaven Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="35ce8-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="35ce8-207">Mentre le nuove applicazioni hello generati usando Eclipse, genererà progetti aggiornati più recente (che saranno in grado di toowork con Maven), è possibile aggiornare l'infrastruttura esistente di servizio senza stato o applicazioni Java attore che usavano hello Service Fabric SDK per Java versioni precedenti, toouse hello Service Fabric Java dipendenze Maven.</span><span class="sxs-lookup"><span data-stu-id="35ce8-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="35ce8-208">Seguire i passaggi di hello indicati [qui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure precedente applicazione funziona con Maven.</span><span class="sxs-lookup"><span data-stu-id="35ce8-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
