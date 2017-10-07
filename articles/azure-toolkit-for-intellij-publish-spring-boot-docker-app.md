---
title: un'app Spring avvio come un contenitore Docker utilizzando aaaPublish hello Azure Toolkit per IntelliJ | Documenti Microsoft
description: Informazioni su come toopublish un tooMicrosoft app web Azure come un contenitore Docker usando hello Azure Toolkit per IntelliJ.
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="bff76-103">Pubblicare un'app Spring avvio come un contenitore Docker usando hello Azure Toolkit per IntelliJ</span><span class="sxs-lookup"><span data-stu-id="bff76-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="bff76-104">Hello [Spring Framework] è una soluzione open source che consente agli sviluppatori Java di creare applicazioni di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="bff76-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="bff76-105">Uno dei progetti comuni a più di hello che viene compilato in cui piattaforma è [avvio Spring], che fornisce un approccio semplificato per la creazione di applicazioni Java autonomo.</span><span class="sxs-lookup"><span data-stu-id="bff76-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="bff76-106">[Docker] è una soluzione open source che consente agli sviluppatori di automatizzare la distribuzione di hello, scalabilità e gestione delle applicazioni in esecuzione nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="bff76-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="bff76-107">In questa esercitazione illustra hello passaggi toodeploy un'applicazione di avvio molla come un tooMicrosoft contenitore Docker Azure tramite hello Azure Toolkit per IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="bff76-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="bff76-108">Clonare hello predefinito Spring avvio Docker repository</span><span class="sxs-lookup"><span data-stu-id="bff76-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="bff76-109">Hello passaggi seguenti consentono di eseguire la clonazione di repository di Docker avvio Spring hello utilizzando IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="bff76-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="bff76-110">Se si desidera toouse una riga di comando, vedere [distribuire un'applicazione di avvio molla su Linux nel servizio contenitore di Azure][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="bff76-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="bff76-111">Aprire IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="bff76-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="bff76-112">Nella schermata iniziale hello selezionare hello **GitHub** opzione hello **estrarre dal controllo della versione** elenco.</span><span class="sxs-lookup"><span data-stu-id="bff76-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![Opzione GitHub per il controllo della versione][CL01]

1. <span data-ttu-id="bff76-114">Immettere le credenziali in caso di richiesta toolog in.</span><span class="sxs-lookup"><span data-stu-id="bff76-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="bff76-115">Se si utilizza un nome utente e password toolog in tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="bff76-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![Finestra di dialogo per l'immissione del nome utente e password GitHub][CL02a]

   * <span data-ttu-id="bff76-117">Se si utilizza un token toolog in tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="bff76-117">If you are using a token toolog in tooGitHub:</span></span>

      ![Finestra di dialogo per l'immissione di un token GitHub][CL02b]

1. <span data-ttu-id="bff76-119">Immettere **https://github.com/spring-guides/gs-spring-boot-docker.git** per l'URL del repository hello, specificare il percorso locale e informazioni sulla cartella e quindi fare clic su **Clone**.</span><span class="sxs-lookup"><span data-stu-id="bff76-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Finestra di dialogo per la clonazione del repository][CL03]

1. <span data-ttu-id="bff76-121">Quando viene richiesto un progetto IntelliJ toocreate **n**.</span><span class="sxs-lookup"><span data-stu-id="bff76-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Rifiuto di un progetto IntelliJ toocreate][CL04]

1. <span data-ttu-id="bff76-123">Nella pagina di benvenuto hello, fare clic su **importazione progetto**.</span><span class="sxs-lookup"><span data-stu-id="bff76-123">On hello welcome page, click **Import Project**.</span></span>

   ![Selezione del progetto da importare][CL05]

1. <span data-ttu-id="bff76-125">Individuare il percorso di hello in cui è stato clonato il repository di avvio Spring hello, selezionare hello **completo** cartella radice hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bff76-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Selezionare una cartella per l'importazione][CL06]

1. <span data-ttu-id="bff76-127">Quando richiesto, scegliere **Create project from existing sources** (Crea progetto da origini esistenti).</span><span class="sxs-lookup"><span data-stu-id="bff76-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Opzione toocreate un progetto da origini esistenti][CL07]

1. <span data-ttu-id="bff76-129">Specificare il nome del progetto o accettare l'impostazione predefinita di hello, verificare hello percorso corretto toohello **completo** cartella e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bff76-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Specificare il nome di progetto hello][CL08]

1. <span data-ttu-id="bff76-131">Personalizzare le directory per l'importazione e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="bff76-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Scegliere le directory][CL09]

1. <span data-ttu-id="bff76-133">Esaminare tooimport librerie hello e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bff76-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Esaminare le librerie del progetto][CL10]

1. <span data-ttu-id="bff76-135">Struttura del modulo hello di esaminare e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="bff76-135">Review hello module structure, and then click **Next**.</span></span>

   ![Esaminare la struttura del modulo][CL11]

1. <span data-ttu-id="bff76-137">Specificare il JDK e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="bff76-137">Specify your JDK, and then click **Next**.</span></span>

   ![Specificare un JDK][CL12]

1. <span data-ttu-id="bff76-139">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bff76-139">Click **Finish**.</span></span>

   ![Pulsante Fine][CL13]

<span data-ttu-id="bff76-141">IntelliJ Importa hello Spring avvio app come un progetto e Visualizza struttura hello quando terminata l'importazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![App Spring Boot in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="bff76-143">Compilare l'app Spring Boot</span><span class="sxs-lookup"><span data-stu-id="bff76-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="bff76-144">Compilare l'applicazione hello utilizzando hello POM di Maven</span><span class="sxs-lookup"><span data-stu-id="bff76-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="bff76-145">Se non è già aperto, aprire finestra degli strumenti di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="bff76-146">Fare clic su **Visualizza** > **Finestre degli strumenti** > **Maven Projects** (Progetti Maven).</span><span class="sxs-lookup"><span data-stu-id="bff76-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Comandi Finestre degli strumenti e Maven Projects (Progetti Maven)][BU01]

1. <span data-ttu-id="bff76-148">Nella finestra strumento di Maven hello, fare doppio clic su **pacchetto** e selezionare **Esegui compilazione Maven**.</span><span class="sxs-lookup"><span data-stu-id="bff76-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="bff76-149">(Se il progetto di Maven non vengono visualizzate automaticamente, fare clic su hello **reimportare** icona sulla barra degli strumenti Maven hello.)</span><span class="sxs-lookup"><span data-stu-id="bff76-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Comando Run Maven Build (Esegui compilazione Maven)][BU02]

1. <span data-ttu-id="bff76-151">Una volta creata correttamente l'app Spring Boot, IntelliJ visualizzerà un messaggio **BUILD SUCCESS** (COMPILAZIONE COMPLETATA).</span><span class="sxs-lookup"><span data-stu-id="bff76-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Messaggio BUILD SUCCESS (COMPILAZIONE COMPLETATA)][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="bff76-153">Creare un elemento pronto per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="bff76-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="bff76-154">toopublish app Spring avvio, è necessario toocreate un elemento pronto per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bff76-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="bff76-155">Utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="bff76-155">Use hello following steps:</span></span>

1. <span data-ttu-id="bff76-156">Aprire il progetto dell'app Web in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="bff76-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="bff76-157">Fare clic su **File** e quindi fare clic su **Project Structure** (Struttura del progetto).</span><span class="sxs-lookup"><span data-stu-id="bff76-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Comando Project Structure (Struttura del progetto)][ART01]

1. <span data-ttu-id="bff76-159">Fare clic su hello verde plus (**+**) di simboli tooadd un elemento, fare clic su **JAR**e quindi fare clic su **vuoto**.</span><span class="sxs-lookup"><span data-stu-id="bff76-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Aggiungere un elemento][ART02]

1. <span data-ttu-id="bff76-161">Denominare l'elemento assicurandosi che non tooadd hello "JAR" estensione e quindi specificare la cartella di destinazione hello per hello Maven output.</span><span class="sxs-lookup"><span data-stu-id="bff76-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Specificare le proprietà dell'elemento][ART03]

1. <span data-ttu-id="bff76-163">Creare un manifesto per l'elemento (facoltativo):</span><span class="sxs-lookup"><span data-stu-id="bff76-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="bff76-164">a.</span><span class="sxs-lookup"><span data-stu-id="bff76-164">a.</span></span> <span data-ttu-id="bff76-165">Fare clic su **Create Manifest** (Crea manifesto).</span><span class="sxs-lookup"><span data-stu-id="bff76-165">Click **Create Manifest**.</span></span>

      ![Fare clic sul pulsante Crea manifesto hello][ART04a]

   <span data-ttu-id="bff76-167">b.</span><span class="sxs-lookup"><span data-stu-id="bff76-167">b.</span></span> <span data-ttu-id="bff76-168">Scegliere il percorso predefinito hello per artefatto hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bff76-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Specificare il percorso dell'elemento][ART04b]

   <span data-ttu-id="bff76-170">c.</span><span class="sxs-lookup"><span data-stu-id="bff76-170">c.</span></span> <span data-ttu-id="bff76-171">Fare clic sui puntini di sospensione hello (**... **) toolocate classe principale di hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Individuare la classe principale][ART04c]

   <span data-ttu-id="bff76-173">d.</span><span class="sxs-lookup"><span data-stu-id="bff76-173">d.</span></span> <span data-ttu-id="bff76-174">Scegliere la classe principale e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bff76-174">Choose your main class, and then click **OK**.</span></span>

      ![Specificare la classe principale][ART04d]

1. <span data-ttu-id="bff76-176">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="bff76-176">Click **OK**.</span></span>

   ![Chiudere la finestra di dialogo di hello struttura del progetto][ART05]

> [!NOTE]
> <span data-ttu-id="bff76-178">Per ulteriori informazioni sulla creazione di elementi in IntelliJ, vedere [gli elementi di configurazione] nel sito Web JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="bff76-179">Hello artefatto per la distribuzione di compilazione</span><span class="sxs-lookup"><span data-stu-id="bff76-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="bff76-180">Fare clic su **Build** (Compila) e quindi su **Artifacts** (Elementi).</span><span class="sxs-lookup"><span data-stu-id="bff76-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Comando Build Artifacts (Compila elementi)][BU04]

1. <span data-ttu-id="bff76-182">Quando hello **artefatto di compilazione** menu di scelta rapida viene visualizzato, fare clic su **compilare**.</span><span class="sxs-lookup"><span data-stu-id="bff76-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menu di scelta rapida Build Artifact (Compila elemento)][BU05]

<span data-ttu-id="bff76-184">IntelliJ deve essere visualizzato artefatto hello completato per l'app avvio Spring nella finestra strumento di hello progetto.</span><span class="sxs-lookup"><span data-stu-id="bff76-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Elemento creato][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="bff76-186">Pubblicare il tooAzure app web con un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="bff76-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="bff76-187">Se non è stato firmato in tooyour account Azure, seguire hello [accesso le istruzioni per hello Azure Toolkit per IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="bff76-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="bff76-188">Nella finestra degli strumenti di Esplora progetti hello, fare clic sul progetto hello e quindi selezionare **Azure** > **pubblica come contenitore Docker**.</span><span class="sxs-lookup"><span data-stu-id="bff76-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Comando Publish as Docker Container (Pubblica come contenitore Docker)][PU01]

1. <span data-ttu-id="bff76-190">Quando hello **distribuire contenitore Docker in Azure** viene visualizzata la finestra di dialogo, vengono visualizzati gli host Docker esistenti.</span><span class="sxs-lookup"><span data-stu-id="bff76-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="bff76-191">Se si sceglie toodeploy tooan esistente host, è possibile ignorare toostep 4.</span><span class="sxs-lookup"><span data-stu-id="bff76-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="bff76-192">In caso contrario, utilizzare hello seguendo i passaggi toocreate un host:</span><span class="sxs-lookup"><span data-stu-id="bff76-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="bff76-193">a.</span><span class="sxs-lookup"><span data-stu-id="bff76-193">a.</span></span> <span data-ttu-id="bff76-194">Fare clic su hello verde plus (**+**) simbolo.</span><span class="sxs-lookup"><span data-stu-id="bff76-194">Click hello green plus (**+**) symbol.</span></span>

      ![Aggiungere un nuovo host Docker][PU02]

   <span data-ttu-id="bff76-196">b.</span><span class="sxs-lookup"><span data-stu-id="bff76-196">b.</span></span> <span data-ttu-id="bff76-197">Quando hello **creare Host Docker** viene visualizzata la finestra di dialogo, è possibile scegliere le impostazioni predefinite hello tooaccept o è possibile specificare le impostazioni personalizzate per il nuovo host Docker.</span><span class="sxs-lookup"><span data-stu-id="bff76-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="bff76-198">(Per una descrizione dettagliata di hello diverse impostazioni, vedere [pubblicare un'app web come un contenitore Docker usando hello Azure Toolkit per IntelliJ][Publish Container with Azure Toolkit].) Fare clic su **Avanti** una volta specificate le impostazioni toouse.</span><span class="sxs-lookup"><span data-stu-id="bff76-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Specificare le opzioni per l'host Docker][PU03a]

   <span data-ttu-id="bff76-200">c.</span><span class="sxs-lookup"><span data-stu-id="bff76-200">c.</span></span> <span data-ttu-id="bff76-201">È possibile scegliere le credenziali di accesso esistente toouse da un insieme di credenziali chiave di Azure, oppure è possibile scegliere tooenter nuove credenziali di accesso di Docker.</span><span class="sxs-lookup"><span data-stu-id="bff76-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="bff76-202">Dopo aver specificato le opzioni, fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="bff76-202">Click **Finish** when you have specified your options.</span></span>

      ![Specificare le credenziali per l'host Docker][PU03b]

1. <span data-ttu-id="bff76-204">Selezionare l'host Docker e quindi fare clic su **Next** (Avanti).</span><span class="sxs-lookup"><span data-stu-id="bff76-204">Select your Docker host, and then click **Next**.</span></span>

   ![Selezionare hello Docker host toouse][PU04]

1. <span data-ttu-id="bff76-206">Hello ultima pagina di hello **distribuire contenitore Docker in Azure** finestra di dialogo specificare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="bff76-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="bff76-207">a.</span><span class="sxs-lookup"><span data-stu-id="bff76-207">a.</span></span> <span data-ttu-id="bff76-208">È possibile scegliere un nome personalizzato per il contenitore hello che ospiterà il contenitore Docker toospecify oppure è possibile accettare l'impostazione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="bff76-209">b.</span><span class="sxs-lookup"><span data-stu-id="bff76-209">b.</span></span> <span data-ttu-id="bff76-210">Immettere le porte TCP hello per l'host docker usando hello la seguente sintassi: *[porta esterna]*:*[porta interna]*.</span><span class="sxs-lookup"><span data-stu-id="bff76-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="bff76-211">Ad esempio, **80:8080** specifica una porta esterna dell'80 e la porta interna Spring avvio hello predefinita del 8080.</span><span class="sxs-lookup"><span data-stu-id="bff76-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="bff76-212">Se è stato personalizzato la porta interna (ad esempio, modificando il file di application.yml hello), è necessario il numero di porta hello toospecify per hello toooccur routing corretto in Azure.</span><span class="sxs-lookup"><span data-stu-id="bff76-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="bff76-213">c.</span><span class="sxs-lookup"><span data-stu-id="bff76-213">c.</span></span> <span data-ttu-id="bff76-214">Dopo aver configurato queste opzioni, fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="bff76-214">After you have configured these options, click **Finish**.</span></span>

   ![Distribuire un contenitore Docker in Azure][PU05]

1. <span data-ttu-id="bff76-216">Al termine hello Azure Toolkit pubblicazione, hello Visualizza Log attività Azure **pubblicato** per lo stato di hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Distribuzione dell'host Docker completata][PU06]

## <a name="next-steps"></a><span data-ttu-id="bff76-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bff76-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="bff76-219">vedere toolearn sui metodi aggiuntivi per la creazione di applicazioni di avvio Spring utilizzando IntelliJ, [creazione di progetti di avvio Spring](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) nel sito Web JetBrains hello.</span><span class="sxs-lookup"><span data-stu-id="bff76-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configurazione di elementi)
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
