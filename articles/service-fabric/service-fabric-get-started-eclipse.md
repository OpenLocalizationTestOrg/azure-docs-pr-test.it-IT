---
title: Plug-in Azure Service Fabric per Eclipse | Microsoft Docs
description: Introduzione al plug-in Service Fabric per Eclipse.
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
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="477c7-103">Plug-in Service Fabric per lo sviluppo di applicazioni Java in Eclipse</span><span class="sxs-lookup"><span data-stu-id="477c7-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="477c7-104">Eclipse è uno degli ambienti di sviluppo integrato (IDE) più diffusi per sviluppatori Java.</span><span class="sxs-lookup"><span data-stu-id="477c7-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="477c7-105">Questo articolo illustra come configurare l'ambiente di sviluppo Eclipse per l'uso con Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="477c7-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="477c7-106">Spiega come installare il plug-in Service Fabric, creare un'applicazione Service Fabric e distribuire l'applicazione nel cluster di Service Fabric locale o remoto in Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="477c7-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="477c7-107">Installare o aggiornare il plug-in Service Fabric in Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="477c7-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="477c7-108">È possibile installare un plug-in Service Fabric in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="477c7-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="477c7-109">Il plug-in consente di semplificare il processo di compilazione e distribuzione di servizi Java.</span><span class="sxs-lookup"><span data-stu-id="477c7-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="477c7-110">Assicurarsi di avere installato la versione più recente di Eclipse Neon e la versione più recente di Buildship (1.0.17 o versione successiva):</span><span class="sxs-lookup"><span data-stu-id="477c7-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="477c7-111">Per verificare le versioni dei componenti installati, in Eclipse Neon scegliere **Help** > **Installation Details** (? > Dettagli installazione).</span><span class="sxs-lookup"><span data-stu-id="477c7-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="477c7-112">Per aggiornare Buildship, vedere [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update] (Eclipse Buildship: plug-in Eclipse per Gradle).</span><span class="sxs-lookup"><span data-stu-id="477c7-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="477c7-113">Per cercare e installare gli aggiornamenti di Eclipse Neon, passare a **Help** > **Check for Updates** (? > Controlla aggiornamenti).</span><span class="sxs-lookup"><span data-stu-id="477c7-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="477c7-114">Per installare il plug-in Service Fabric, in Eclipse Neon passare a **Help** > **Install New Software** (? > Installa nuovo software).</span><span class="sxs-lookup"><span data-stu-id="477c7-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="477c7-115">Nella casella **Work with** (Usa) immettere **http://dl.microsoft.com/eclipse**</span><span class="sxs-lookup"><span data-stu-id="477c7-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="477c7-116">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="477c7-116">Click **Add**.</span></span>

         ![Plug-in Service Fabric per Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="477c7-118">Selezionare il plug-in Service Fabric e fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="477c7-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="477c7-119">Completare la procedura di installazione e quindi accettare le Condizioni di licenza software Microsoft.</span><span class="sxs-lookup"><span data-stu-id="477c7-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="477c7-120">Se il plug-in Service Fabric è già installato, verificare che la versione sia la più recente.</span><span class="sxs-lookup"><span data-stu-id="477c7-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="477c7-121">Per verificare la disponibilità di aggiornamenti, passare a **Help** > **Installation Details** (? > Dettagli installazione).</span><span class="sxs-lookup"><span data-stu-id="477c7-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="477c7-122">Nell'elenco di plug-in installati selezionare Service Fabric e fare clic su **Update** (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="477c7-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="477c7-123">Verranno installati gli aggiornamenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="477c7-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="477c7-124">Se l'installazione o l'aggiornamento del plug-in Service Fabric è lento, il problema potrebbe essere dovuto a un'impostazione di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="477c7-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="477c7-125">Eclipse raccoglie i metadati di tutte le modifiche per aggiornare i siti registrati con l'istanza di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="477c7-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="477c7-126">Per velocizzare il processo di rilevamento e installazione di un aggiornamento del plug-in Service Fabric, passare a **Available Software Sites** (Siti software disponibili).</span><span class="sxs-lookup"><span data-stu-id="477c7-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="477c7-127">Deselezionare le caselle di controllo per tutti i siti eccetto quello che punta al percorso del plug-in Service Fabric (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="477c7-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="477c7-128">Creare un'applicazione di Service Fabric in Eclipse</span><span class="sxs-lookup"><span data-stu-id="477c7-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="477c7-129">In Eclipse Neon, passare a **File** > **New** > **Other** (File > Nuovo > Altro).</span><span class="sxs-lookup"><span data-stu-id="477c7-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="477c7-130">Selezionare **Service Fabric Project**, quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="477c7-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Pagina 1 del nuovo progetto di Service Fabric][create-application/p1]

2.  <span data-ttu-id="477c7-132">Immettere un nome per il progetto e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="477c7-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Pagina 2 del nuovo progetto di Service Fabric][create-application/p2]

3.  <span data-ttu-id="477c7-134">Dall'elenco dei modelli selezionare **Service Template** (Modello di servizio).</span><span class="sxs-lookup"><span data-stu-id="477c7-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="477c7-135">Selezionare il tipo di modello di servizio (Actor, Stateless, Container, or Guest Binary) e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="477c7-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Pagina 3 del nuovo progetto di Service Fabric][create-application/p3]

4.  <span data-ttu-id="477c7-137">Immettere il nome e i dettagli del servizio e fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="477c7-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Pagina 4 del nuovo progetto di Service Fabric][create-application/p4]

5. <span data-ttu-id="477c7-139">Quando si crea il primo progetto di Service Fabric, nella finestra di dialogo **Open Associated Perspective** (Apri prospettiva associata) fare clic su **Yes**.</span><span class="sxs-lookup"><span data-stu-id="477c7-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Pagina 5 del nuovo progetto di Service Fabric][create-application/p5]

6.  <span data-ttu-id="477c7-141">L'aspetto del nuovo progetto sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="477c7-141">Your new project looks like this:</span></span>

    ![Pagina 6 del nuovo progetto di Service Fabric][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="477c7-143">Creare e distribuire un'applicazione di Service Fabric in Eclipse</span><span class="sxs-lookup"><span data-stu-id="477c7-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="477c7-144">Fare clic con il pulsante destro del mouse sulla nuova applicazione di Service Fabric, quindi scegliere **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="477c7-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Menu di scelta rapida di Service Fabric][publish/RightClick]

2. <span data-ttu-id="477c7-146">Nel sottomenu selezionare l'opzione desiderata:</span><span class="sxs-lookup"><span data-stu-id="477c7-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="477c7-147">Per compilare l'applicazione senza pulizia, fare clic su **Build Application** (Compila applicazione).</span><span class="sxs-lookup"><span data-stu-id="477c7-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="477c7-148">Per eseguire una compilazione pulita dell'applicazione, fare clic su **Rebuild Application** (Ricompila applicazione).</span><span class="sxs-lookup"><span data-stu-id="477c7-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="477c7-149">Per eliminare gli artefatti di compilazione dall'applicazione, fare clic su **Clean Application** (Pulisci applicazione).</span><span class="sxs-lookup"><span data-stu-id="477c7-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="477c7-150">Da questo menu è anche possibile distribuire, annullare la distribuzione e pubblicare l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="477c7-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="477c7-151">Per eseguire la distribuzione nel cluster locale, fare clic su **Deploy Application** (Distribuisci applicazione).</span><span class="sxs-lookup"><span data-stu-id="477c7-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="477c7-152">Nella finestra di dialogo **Publish Application** (Pubblica applicazione) selezionare un profilo di pubblicazione:</span><span class="sxs-lookup"><span data-stu-id="477c7-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="477c7-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="477c7-153">**Local.json**</span></span>
        -  <span data-ttu-id="477c7-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="477c7-154">**Cloud.json**</span></span>

     <span data-ttu-id="477c7-155">Questi file JSON (JavaScript Object Notation) archiviano le informazioni necessarie per connettersi al cluster locale o nel cloud (Azure), ad esempio gli endpoint di connessione e le informazioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="477c7-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Menu di pubblicazione di Service Fabric][publish/Publish]

<span data-ttu-id="477c7-157">Un modo alternativo per distribuire l'applicazione di Service Fabric consiste nell'usare le configurazioni di esecuzione di Eclipse.</span><span class="sxs-lookup"><span data-stu-id="477c7-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="477c7-158">Passare a **Run** > **Run Configurations** (Esegui > Configurazioni di esecuzione).</span><span class="sxs-lookup"><span data-stu-id="477c7-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="477c7-159">In **Gradle Project** (Progetto Gradle) selezionare la configurazione di esecuzione **ServiceFabricDeployer**.</span><span class="sxs-lookup"><span data-stu-id="477c7-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="477c7-160">Nella scheda **Arguments** (Argomenti) del pannello destro selezionare **local** o **cloud** per **publishProfile**.</span><span class="sxs-lookup"><span data-stu-id="477c7-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="477c7-161">Il valore predefinito è **local**.</span><span class="sxs-lookup"><span data-stu-id="477c7-161">The default is **local**.</span></span> <span data-ttu-id="477c7-162">Per la distribuzione in un cluster remoto o cloud, selezionare **cloud**.</span><span class="sxs-lookup"><span data-stu-id="477c7-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="477c7-163">Per verificare che nei profili di pubblicazione siano inserite le informazioni corrette, modificare **Local.json** o **Cloud.json** in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="477c7-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="477c7-164">È possibile aggiungere o aggiornare i dettagli degli endpoint e delle credenziali di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="477c7-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="477c7-165">Verificare che **Working Directory** (Directory di lavoro) punti all'applicazione da distribuire.</span><span class="sxs-lookup"><span data-stu-id="477c7-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="477c7-166">Per cambiare applicazione, fare clic sul pulsante **Workspace** (Area di lavoro) e selezionare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="477c7-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="477c7-167">Fare clic su **Apply** (Applica) e quindi su **Run** (Esegui).</span><span class="sxs-lookup"><span data-stu-id="477c7-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="477c7-168">L'applicazione verrà compilata e distribuita dopo alcuni istanti.</span><span class="sxs-lookup"><span data-stu-id="477c7-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="477c7-169">È possibile monitorare lo stato della distribuzione in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="477c7-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="477c7-170">Aggiungere un servizio di Service Fabric all'applicazione di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="477c7-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="477c7-171">Per aggiungere un servizio di Service Fabric a un'applicazione di Service Fabric esistente seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="477c7-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="477c7-172">Fare clic con il pulsante destro del mouse sul progetto al quale aggiungere un servizio e quindi scegliere **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="477c7-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Pagina 1 dell'aggiunta di un servizio di Service Fabric][add-service/p1]

2.  <span data-ttu-id="477c7-174">Fare clic su **Add Service Fabric Service** (Aggiungi servizio di Service Fabric) e completare la procedura per aggiungere un servizio al progetto.</span><span class="sxs-lookup"><span data-stu-id="477c7-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="477c7-175">Selezionare il modello di servizio da aggiungere al progetto e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="477c7-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Pagina 2 dell'aggiunta di un servizio di Service Fabric][add-service/p2]

4.  <span data-ttu-id="477c7-177">Immettere il nome del servizio e altri eventuali dettagli necessari, quindi fare clic sul pulsante **Add Service** (Aggiungi servizio).</span><span class="sxs-lookup"><span data-stu-id="477c7-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Pagina 3 dell'aggiunta di un servizio di Service Fabric][add-service/p3]

5.  <span data-ttu-id="477c7-179">Dopo aver aggiunto il servizio, la struttura complessiva del progetto sarà simile al progetto seguente:</span><span class="sxs-lookup"><span data-stu-id="477c7-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Pagina 4 dell'aggiunta di un servizio di Service Fabric][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="477c7-181">Modifica versioni del manifesto dell'applicazione Java di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="477c7-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="477c7-182">Per modificare le versioni del manifesto, fare clic con il pulsante destro del mouse sul progetto, passare a **Service Fabric** e selezionare **Modifica versioni del manifesto...** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="477c7-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="477c7-183">Nella procedura guidata è possibile aggiornare le versioni del manifesto dell'applicazione, del manifesto del servizio e dei pacchetti di **codice**, **configurazione** e **dati**.</span><span class="sxs-lookup"><span data-stu-id="477c7-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="477c7-184">Selezionando l'opzione **Aggiorna automaticamente le versioni di applicazioni e servizi** e aggiornando la versione, le versioni del manifesto verranno aggiornate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="477c7-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="477c7-185">Ad esempio, selezionare prima la casella di controllo, quindi aggiornare la versione del **codice** da 0.0.0 a 0.0.1 e fare clic su **Fine**. La versione del manifesto del servizio e del manifesto dell'applicazione verrà aggiornata automaticamente a 0.0.1.</span><span class="sxs-lookup"><span data-stu-id="477c7-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="477c7-186">Aggiornare l'applicazione Java di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="477c7-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="477c7-187">In uno scenario di aggiornamento è stato ad esempio creato il progetto **App1** usando il plug-in Service Fabric in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="477c7-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="477c7-188">Il progetto è stato distribuito con il plug-in per creare un'applicazione denominata **fabric:/App1Application**.</span><span class="sxs-lookup"><span data-stu-id="477c7-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="477c7-189">Il tipo di applicazione è **App1AppicationType** e la versione dell'applicazione è 1.0.</span><span class="sxs-lookup"><span data-stu-id="477c7-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="477c7-190">Ora si vuole aggiornare l'applicazione senza interromperne la disponibilità.</span><span class="sxs-lookup"><span data-stu-id="477c7-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="477c7-191">Apportare prima le eventuali modifiche necessarie all'applicazione, quindi ricompilare il servizio modificato.</span><span class="sxs-lookup"><span data-stu-id="477c7-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="477c7-192">Aggiornare il file manifesto del servizio modificato (ServiceManifest.xml) con le versioni aggiornate del servizio e anche del codice, della configurazione o dei dati, a seconda delle esigenze.</span><span class="sxs-lookup"><span data-stu-id="477c7-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="477c7-193">Modificare anche il manifesto dell'applicazione (ApplicationManifest.xml) con il numero di versione aggiornato per l'applicazione e il servizio modificato.</span><span class="sxs-lookup"><span data-stu-id="477c7-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="477c7-194">Per aggiornare l'applicazione usando Eclipse Neon è possibile creare un profilo di configurazione di esecuzione duplicato</span><span class="sxs-lookup"><span data-stu-id="477c7-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="477c7-195">e quindi usarlo per aggiornare l'applicazione in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="477c7-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="477c7-196">Passare a **Run** > **Run Configurations** (Esegui > Configurazioni di esecuzione).</span><span class="sxs-lookup"><span data-stu-id="477c7-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="477c7-197">Nel pannello sinistro fare clic sulla piccola freccia a sinistra di **Gradle Project** (Progetto Gradle).</span><span class="sxs-lookup"><span data-stu-id="477c7-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="477c7-198">Fare clic con il pulsante destro del mouse su **ServiceFabricDeployer** e quindi scegliere **Duplicate** (Duplica).</span><span class="sxs-lookup"><span data-stu-id="477c7-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="477c7-199">Specificare un nuovo nome per questa configurazione, ad esempio **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="477c7-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="477c7-200">Nella scheda **Arguments** (Argomenti) nel pannello destro modificare **-Pconfig='deploy'** in **-Pconfig='upgrade'** e quindi fare clic su **Apply** (Applica).</span><span class="sxs-lookup"><span data-stu-id="477c7-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="477c7-201">Questo processo crea e salva un profilo di configurazione di esecuzione che può essere usato in qualsiasi momento per aggiornare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="477c7-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="477c7-202">Recupera anche la versione più recente del tipo di applicazione dal file manifesto dell'applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="477c7-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="477c7-203">L'aggiornamento dell'applicazione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="477c7-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="477c7-204">È possibile monitorare l'aggiornamento dell'applicazione in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="477c7-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="477c7-205">Migrazione di applicazioni Java di Service Fabric precedenti da usare con Maven</span><span class="sxs-lookup"><span data-stu-id="477c7-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="477c7-206">Le librerie Java di Service Fabric sono state recentemente spostate da Service Fabric Java SDK al repository di Maven.</span><span class="sxs-lookup"><span data-stu-id="477c7-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="477c7-207">Benché le nuove applicazioni generate con Eclipse genereranno i progetti aggiornati più recenti (in grado di interagire con Maven), è possibile aggiornare le applicazioni Java esistenti di Service Fabric senza stato o actor, che in precedenza usavano Service Fabric Java SDK, in modo che usino le dipendenze Java di Service Fabric da Maven.</span><span class="sxs-lookup"><span data-stu-id="477c7-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="477c7-208">Seguire la procedura riportata [qui](service-fabric-migrate-old-javaapp-to-use-maven.md) per assicurare che l'applicazione precedente funzioni con Maven.</span><span class="sxs-lookup"><span data-stu-id="477c7-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

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
