---
title: un'app Spring avvio come un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="b567f-103">Pubblicare un'app Spring avvio come un contenitore Docker usando hello Azure Toolkit per Eclipse</span><span class="sxs-lookup"><span data-stu-id="b567f-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="b567f-104">Hello [Spring Framework] è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="b567f-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="b567f-105">Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonomo.</span><span class="sxs-lookup"><span data-stu-id="b567f-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="b567f-106">[Docker] è una soluzione open source che consente agli sviluppatori di automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="b567f-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="b567f-107">In questa esercitazione illustra hello passaggi toodeploy un'applicazione di avvio molla come un tooMicrosoft contenitore Docker Azure tramite hello Azure Toolkit per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b567f-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="b567f-108">Clonare il repository di Docker avvio Spring hello predefinito</span><span class="sxs-lookup"><span data-stu-id="b567f-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="b567f-109">Archivio pubblico hello di importazione</span><span class="sxs-lookup"><span data-stu-id="b567f-109">Import hello public repository</span></span>

<span data-ttu-id="b567f-110">Hello passaggi seguenti consentono di eseguire la clonazione di computer locale tooyour hello Spring avvio Docker repository utilizzando IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="b567f-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="b567f-111">Se si desidera toouse una riga di comando, vedere [distribuire un'applicazione di avvio molla su Linux nel servizio contenitore di Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="b567f-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="b567f-112">Aprire Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b567f-112">Open Eclipse.</span></span>

1. <span data-ttu-id="b567f-113">Fare clic su **File** > **Import** (Importa).</span><span class="sxs-lookup"><span data-stu-id="b567f-113">Click **File** > **Import**.</span></span>

   ![Opzione Import (Importa) del menu File][CL01]

1. <span data-ttu-id="b567f-115">Quando hello **importazione** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="b567f-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="b567f-116">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-116">a.</span></span> <span data-ttu-id="b567f-117">Espandere **Git**.</span><span class="sxs-lookup"><span data-stu-id="b567f-117">Expand **Git**.</span></span>

   <span data-ttu-id="b567f-118">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-118">b.</span></span> <span data-ttu-id="b567f-119">Selezionare **Projects from Git** (Progetti da Git).</span><span class="sxs-lookup"><span data-stu-id="b567f-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="b567f-120">c.</span><span class="sxs-lookup"><span data-stu-id="b567f-120">c.</span></span> <span data-ttu-id="b567f-121">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-121">Click **Next**.</span></span>

   ![Finestra di dialogo Import (Importa)][CL02]

1. <span data-ttu-id="b567f-123">In hello **selezionare l'origine del Repository** pagina:</span><span class="sxs-lookup"><span data-stu-id="b567f-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="b567f-124">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-124">a.</span></span> <span data-ttu-id="b567f-125">Selezionare **Clone URI** (Clona URI).</span><span class="sxs-lookup"><span data-stu-id="b567f-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="b567f-126">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-126">b.</span></span> <span data-ttu-id="b567f-127">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-127">Click **Next**.</span></span>

   ![Selezionare la pagina origine del repository][CL03]

1. <span data-ttu-id="b567f-129">In hello **Git Repository di origine** pagina:</span><span class="sxs-lookup"><span data-stu-id="b567f-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="b567f-130">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-130">a.</span></span> <span data-ttu-id="b567f-131">Per **URI**, immettere `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="b567f-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="b567f-132">Questo passaggio deve popolare automaticamente hello **Host** e **il percorso del Repository** i campi con hello correggere i valori.</span><span class="sxs-lookup"><span data-stu-id="b567f-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="b567f-133">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-133">b.</span></span> <span data-ttu-id="b567f-134">repository di avvio Spring Hello è pubblica, pertanto non è necessario tooenter nome Git utente e password.</span><span class="sxs-lookup"><span data-stu-id="b567f-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="b567f-135">c.</span><span class="sxs-lookup"><span data-stu-id="b567f-135">c.</span></span> <span data-ttu-id="b567f-136">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-136">Click **Next**.</span></span>

   ![Pagina del repository Git di origine][CL04]

1. <span data-ttu-id="b567f-138">In hello **selezione ramo** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Pagina Branch Selection (Selezione ramo)][CL05]

1. <span data-ttu-id="b567f-140">In hello **destinazione locale** pagina:</span><span class="sxs-lookup"><span data-stu-id="b567f-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="b567f-141">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-141">a.</span></span> <span data-ttu-id="b567f-142">Specificare hello cartella locale in cui si desidera il repository locale.</span><span class="sxs-lookup"><span data-stu-id="b567f-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="b567f-143">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-143">b.</span></span> <span data-ttu-id="b567f-144">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-144">Click **Next**.</span></span>

   ![Pagina Local Destination (Destinazione locale)][CL06]

1. <span data-ttu-id="b567f-146">In hello **toouse una procedura guidata per l'importazione di progetti selezionare** pagina:</span><span class="sxs-lookup"><span data-stu-id="b567f-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="b567f-147">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-147">a.</span></span> <span data-ttu-id="b567f-148">Selezionare **Import as a general project** (Importa come progetto generale).</span><span class="sxs-lookup"><span data-stu-id="b567f-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="b567f-149">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-149">b.</span></span> <span data-ttu-id="b567f-150">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-150">Click **Next**.</span></span>

   !["Seleziona toouse una procedura guidata per l'importazione di progetti"][CL07]

1. <span data-ttu-id="b567f-152">In hello **importazione progetti** pagina:</span><span class="sxs-lookup"><span data-stu-id="b567f-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="b567f-153">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-153">a.</span></span> <span data-ttu-id="b567f-154">Specificare il nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="b567f-154">Specify your project name.</span></span>
   
   <span data-ttu-id="b567f-155">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-155">b.</span></span> <span data-ttu-id="b567f-156">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b567f-156">Click **Finish**.</span></span>

   ![Pagina Import Projects (Importa progetti)][CL08]

1. <span data-ttu-id="b567f-158">Quando è clonare il repository di hello, vengono visualizzati tutti i file hello elencati in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b567f-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Repository locale][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="b567f-160">Creare un progetto Maven dal repository locale</span><span class="sxs-lookup"><span data-stu-id="b567f-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="b567f-161">repository di Docker avvio Spring Hello contiene un progetto di Maven completato, che verrà utilizzato per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b567f-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="b567f-162">Fare clic su **File** > **Import** (Importa).</span><span class="sxs-lookup"><span data-stu-id="b567f-162">Click **File** > **Import**.</span></span>

   ![Importare i comandi nel menu File hello][CL01]

1. <span data-ttu-id="b567f-164">Quando hello **importazione** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="b567f-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="b567f-165">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-165">a.</span></span> <span data-ttu-id="b567f-166">Espandere **Maven**.</span><span class="sxs-lookup"><span data-stu-id="b567f-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="b567f-167">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-167">b.</span></span> <span data-ttu-id="b567f-168">Selezionare **Existing Maven Projects** (Progetti Maven esistenti).</span><span class="sxs-lookup"><span data-stu-id="b567f-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="b567f-169">c.</span><span class="sxs-lookup"><span data-stu-id="b567f-169">c.</span></span> <span data-ttu-id="b567f-170">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="b567f-170">Click **Next**.</span></span>

   ![Finestra di dialogo Import (Importa)][MV01]

1. <span data-ttu-id="b567f-172">In hello **progetti Maven** pagina:</span><span class="sxs-lookup"><span data-stu-id="b567f-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="b567f-173">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-173">a.</span></span> <span data-ttu-id="b567f-174">Per **Directory radice**, specificare hello **completo** cartella nel repository locale.</span><span class="sxs-lookup"><span data-stu-id="b567f-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="b567f-175">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-175">b.</span></span> <span data-ttu-id="b567f-176">Espandere hello **avanzate** sezione e immettere un nome personalizzato per **modello nome**.</span><span class="sxs-lookup"><span data-stu-id="b567f-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="b567f-177">c.</span><span class="sxs-lookup"><span data-stu-id="b567f-177">c.</span></span> <span data-ttu-id="b567f-178">Casella di selezione hello hello **pom.xml** file nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b567f-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="b567f-179">d.</span><span class="sxs-lookup"><span data-stu-id="b567f-179">d.</span></span> <span data-ttu-id="b567f-180">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b567f-180">Click **Finish**.</span></span>

   ![Pagina Maven Projects (Progetti Maven)][MV02]

1. <span data-ttu-id="b567f-182">Quando il progetto di Maven hello viene aperto correttamente, viene visualizzato un secondo progetto elencato in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b567f-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Progetto Maven locale][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="b567f-184">Compilazione dell'app Spring Boot mediante Maven</span><span class="sxs-lookup"><span data-stu-id="b567f-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="b567f-185">In Project Explorer di Eclipse hello, selezionare il progetto di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="b567f-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="b567f-186">Fare clic su **Run** > **Run As** > **Maven build** (Esegui > Esegui come > Compilazione Maven)</span><span class="sxs-lookup"><span data-stu-id="b567f-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Comandi toorun come compilazione Maven][BU01]

1. <span data-ttu-id="b567f-188">Quando l'applicazione viene compilata correttamente, finestra di console hello Mostra stato hello.</span><span class="sxs-lookup"><span data-stu-id="b567f-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Completamento della compilazione Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="b567f-190">Pubblicare il tooAzure app web con un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="b567f-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="b567f-191">In Project Explorer di Eclipse hello, selezionare il progetto di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="b567f-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="b567f-192">Fare clic su hello Azure **pubblica** menu e quindi fare clic su **pubblica come contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="b567f-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Comando Publish as Docker Container (Pubblica come contenitore Docker)][PU01]

1. <span data-ttu-id="b567f-194">Quando hello **distribuzione contenitore Docker in Azure** viene visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="b567f-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="b567f-195">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-195">a.</span></span> <span data-ttu-id="b567f-196">Immettere il nome di un'immagine Docker personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b567f-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="b567f-197">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-197">b.</span></span> <span data-ttu-id="b567f-198">Per **artefatto toodeploy**, specificare hello percorso toohello **gs-spring-avvio-docker-0.1.0.jar** file appena compilato.</span><span class="sxs-lookup"><span data-stu-id="b567f-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Specificare le opzioni per Docker][PU02]

   <span data-ttu-id="b567f-200">Verranno visualizzati tutti gli host Docker esistenti.</span><span class="sxs-lookup"><span data-stu-id="b567f-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="b567f-201">Se si sceglie toodeploy tooan esistente host, è possibile ignorare toostep 5.</span><span class="sxs-lookup"><span data-stu-id="b567f-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="b567f-202">In caso contrario, utilizzare hello seguendo i passaggi toocreate un host:</span><span class="sxs-lookup"><span data-stu-id="b567f-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="b567f-203">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-203">a.</span></span> <span data-ttu-id="b567f-204">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b567f-204">Click **Add**.</span></span>

      ![Aggiungere un nuovo host Docker][PU03]

   <span data-ttu-id="b567f-206">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-206">b.</span></span> <span data-ttu-id="b567f-207">Quando hello **creare Host Docker** viene visualizzata la finestra di dialogo, è possibile scegliere le impostazioni predefinite hello tooaccept o è possibile specificare le impostazioni personalizzate per il nuovo host Docker.</span><span class="sxs-lookup"><span data-stu-id="b567f-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="b567f-208">(Per una descrizione dettagliata di hello diverse impostazioni, vedere [pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per IntelliJ][Publish Container with Azure Toolkit].) Fare clic su **Avanti** una volta specificate le impostazioni toouse.</span><span class="sxs-lookup"><span data-stu-id="b567f-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Specificare le opzioni per l'host Docker][PU04]

   <span data-ttu-id="b567f-210">c.</span><span class="sxs-lookup"><span data-stu-id="b567f-210">c.</span></span> <span data-ttu-id="b567f-211">È possibile scegliere le credenziali di accesso esistente toouse da un insieme di credenziali chiave di Azure, oppure è possibile scegliere tooenter nuove credenziali di accesso di Docker.</span><span class="sxs-lookup"><span data-stu-id="b567f-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="b567f-212">Dopo aver specificato le opzioni, fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="b567f-212">Click **Finish** when you have specified your options.</span></span>

      ![Specificare le credenziali per l'host Docker][PU05]

1. <span data-ttu-id="b567f-214">Selezionare l'host Docker e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="b567f-214">Select your Docker host, and then click **Next**.</span></span>

   ![Selezionare toouse host Docker][PU06]

1. <span data-ttu-id="b567f-216">Hello ultima pagina di hello **distribuzione contenitore Docker in Azure** finestra di dialogo specificare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b567f-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="b567f-217">a.</span><span class="sxs-lookup"><span data-stu-id="b567f-217">a.</span></span> <span data-ttu-id="b567f-218">È possibile scegliere un nome personalizzato per il contenitore hello che ospiterà il contenitore Docker toospecify oppure è possibile accettare l'impostazione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="b567f-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="b567f-219">b.</span><span class="sxs-lookup"><span data-stu-id="b567f-219">b.</span></span> <span data-ttu-id="b567f-220">Immettere le porte TCP hello per l'host docker usando hello la seguente sintassi: *[porta esterna]*:*[porta interna]*.</span><span class="sxs-lookup"><span data-stu-id="b567f-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="b567f-221">Ad esempio, **80:8080** specifica una porta esterna dell'80 e la porta interna Spring avvio hello predefinita del 8080.</span><span class="sxs-lookup"><span data-stu-id="b567f-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="b567f-222">Se è stato personalizzato la porta interna (ad esempio, modificando il file di application.yml hello), è necessario il numero di porta hello toospecify per hello toooccur routing corretto in Azure.</span><span class="sxs-lookup"><span data-stu-id="b567f-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="b567f-223">c.</span><span class="sxs-lookup"><span data-stu-id="b567f-223">c.</span></span> <span data-ttu-id="b567f-224">Dopo aver configurato queste opzioni, fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="b567f-224">After you configure these options, click **Finish**.</span></span>

   ![Distribuire un contenitore Docker in Azure][PU07]

1. <span data-ttu-id="b567f-226">Al termine hello Azure Toolkit pubblicazione, hello Visualizza Log attività Azure **pubblicato** per lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="b567f-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Distribuzione dell'host Docker completata][PU08]

## <a name="next-steps"></a><span data-ttu-id="b567f-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b567f-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[avvio Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
