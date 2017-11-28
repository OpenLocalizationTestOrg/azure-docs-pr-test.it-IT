---
title: un'applicazione web di Azure di base in IntelliJ aaaCreate | Documenti Microsoft
description: Questa esercitazione viene illustrato come toouse hello Azure Toolkit per IntelliJ toocreate un'App Web di Hello World per Azure.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: erikre
editor: 
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4667497213cac3ddf754d164e614c809f338cce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="98fea-103">Creare un'app Web di base di Azure in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="98fea-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="98fea-104">Questa esercitazione viene illustrato come toocreate e distribuire una base tooAzure applicazione Hello World come un'App Web utilizzando hello [Azure Toolkit per IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="98fea-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="98fea-105">Per semplicità è riportato un esempio JSP di base, ma è possibile adottare una procedura simile anche per un servlet Java, per quanto riguarda la distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="98fea-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="98fea-106">Dopo aver completato questa esercitazione, l'applicazione avrà un aspetto simile toohello seguente illustrazione, quando viene visualizzata in un web browser:</span><span class="sxs-lookup"><span data-stu-id="98fea-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Pagina Web di esempio][01]

## <a name="prerequisites"></a><span data-ttu-id="98fea-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="98fea-108">Prerequisites</span></span>
* <span data-ttu-id="98fea-109">Java Developer Kit (JDK) versione 1.8 o successiva.</span><span class="sxs-lookup"><span data-stu-id="98fea-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="98fea-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="98fea-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="98fea-111">È possibile scaricarlo da <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="98fea-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="98fea-112">Distribuzione di un server Web basato su Java o un server applicazioni, ad esempio [Apache Tomcat] o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="98fea-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="98fea-113">Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="98fea-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="98fea-114">Hello [Azure Toolkit per IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="98fea-114">hello [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="98fea-115">Per informazioni sull'installazione hello Azure Toolkit, vedere [installazione hello Azure Toolkit per IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="98fea-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for IntelliJ].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="98fea-116">toocreate un'applicazione Hello World</span><span class="sxs-lookup"><span data-stu-id="98fea-116">toocreate a Hello World application</span></span>
<span data-ttu-id="98fea-117">Creare innanzitutto un progetto Java.</span><span class="sxs-lookup"><span data-stu-id="98fea-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="98fea-118">Avviare IntelliJ e fare clic su hello **File** menu, quindi fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="98fea-118">Start IntelliJ and click hello **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![File > New Project (Nuovo progetto)][02]
2. <span data-ttu-id="98fea-120">Nella finestra di dialogo Nuovo progetto di hello, selezionare **Java**, quindi **applicazione Web**, quindi fare clic su **New** tooadd un SDK di progetto.</span><span class="sxs-lookup"><span data-stu-id="98fea-120">In hello New Project dialog box, select **Java**, then **Web Application**, and then click **New** tooadd a Project SDK.</span></span>
   
    ![Finestra di dialogo Nuovo progetto][03a]
   
3. <span data-ttu-id="98fea-122">In hello selezione della Home Directory per la finestra di dialogo JDK, selezionare hello cartella in cui è installato il pacchetto JDK e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="98fea-122">In hello Select Home Directory for JDK dialog box, select hello folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="98fea-123">Fare clic su **Avanti** in toocontinue casella finestra di dialogo Nuovo progetto di hello.</span><span class="sxs-lookup"><span data-stu-id="98fea-123">Click **Next** in hello New Project dialog box toocontinue.</span></span>
   
    ![Specificare la home directory di JDK][03b]
4. <span data-ttu-id="98fea-125">Ai fini di questa esercitazione, denominare il progetto di hello **Java-Web-App-in-Azure**, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="98fea-125">For purposes of this tutorial, name hello project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto][04]
5. <span data-ttu-id="98fea-127">Nella visualizzazione Project Explorer di IntelliJ espandere **Java-Web-App-On-Azure** e **web**, quindi fare doppio clic su **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="98fea-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Pagina di indice aperta][05c]
6. <span data-ttu-id="98fea-129">All'apertura del file index.jsp in IntelliJ, aggiungere la visualizzazione del testo toodynamically **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="98fea-129">When your index.jsp file opens in IntelliJ, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="98fea-130">all'interno di hello esistente `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="98fea-130">within hello existing `<body>` element.</span></span> <span data-ttu-id="98fea-131">L'aggiornamento `<body>` contenuto dovrebbe essere simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="98fea-131">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="98fea-132">Salvare index.jsp.</span><span class="sxs-lookup"><span data-stu-id="98fea-132">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="98fea-133">toodeploy il tooan applicazione contenitore di App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="98fea-133">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="98fea-134">Esistono diversi modi con cui è possibile distribuire un tooAzure di applicazione web Java.</span><span class="sxs-lookup"><span data-stu-id="98fea-134">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="98fea-135">Questa esercitazione viene descritto uno dei più semplice hello: l'applicazione sarà distribuito tooan contenitore di App Web di Azure: nessun tipo di progetto speciale né altri strumenti sono necessari.</span><span class="sxs-lookup"><span data-stu-id="98fea-135">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="98fea-136">Hello JDK hello web contenitore software e verrà fornito automaticamente da Azure, pertanto non c'è alcuna necessità tooupload proprio; è sufficiente l'App Web Java.</span><span class="sxs-lookup"><span data-stu-id="98fea-136">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="98fea-137">Di conseguenza, processo di pubblicazione per l'applicazione hello richiederà secondi, minuti non.</span><span class="sxs-lookup"><span data-stu-id="98fea-137">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="98fea-138">Prima di pubblicare l'applicazione, è innanzitutto necessario tooconfigure le impostazioni del modulo.</span><span class="sxs-lookup"><span data-stu-id="98fea-138">Before you publish your application, you first need tooconfigure your module settings.</span></span> <span data-ttu-id="98fea-139">toodo in tal caso, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="98fea-139">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="98fea-140">In Esplora progetti del IntelliJ pulsante destro del mouse hello **Java-Web-App-in-Azure** progetto.</span><span class="sxs-lookup"><span data-stu-id="98fea-140">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="98fea-141">Quando viene visualizzato il menu di scelta rapida hello, fare clic su **aprire le impostazioni del modulo**.</span><span class="sxs-lookup"><span data-stu-id="98fea-141">When hello context menu appears, click **Open Module Settings**.</span></span>

    ![Open Module Settings (Apri impostazioni modulo)][05a]
2. <span data-ttu-id="98fea-143">Quando viene visualizzata la finestra di dialogo di hello struttura del progetto:</span><span class="sxs-lookup"><span data-stu-id="98fea-143">When hello Project Structure dialog box appears:</span></span>

   <span data-ttu-id="98fea-144">a.</span><span class="sxs-lookup"><span data-stu-id="98fea-144">a.</span></span> <span data-ttu-id="98fea-145">Fare clic su **elementi** nell'elenco di hello di **impostazioni progetto**.</span><span class="sxs-lookup"><span data-stu-id="98fea-145">Click **Artifacts** in hello list of **Project Settings**.</span></span>
   <span data-ttu-id="98fea-146">b.</span><span class="sxs-lookup"><span data-stu-id="98fea-146">b.</span></span> <span data-ttu-id="98fea-147">Nome dell'artefatto modifica hello in hello **nome** casella in modo che non contenga spazi o caratteri speciali; questa operazione è necessaria perché verrà usati nome hello in hello identificatore URI (Uniform Resource).</span><span class="sxs-lookup"><span data-stu-id="98fea-147">Change hello artifact name in hello **Name** box so that it doesn't contain whitespace or special characters; this is necessary since hello name will be used in hello Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="98fea-148">c.</span><span class="sxs-lookup"><span data-stu-id="98fea-148">c.</span></span> <span data-ttu-id="98fea-149">Hello modifica **tipo** troppo**applicazione Web: archivio**.</span><span class="sxs-lookup"><span data-stu-id="98fea-149">Change hello **Type** too**Web Application: Archive**.</span></span>
   <span data-ttu-id="98fea-150">d.</span><span class="sxs-lookup"><span data-stu-id="98fea-150">d.</span></span> <span data-ttu-id="98fea-151">Fare clic su **OK** la finestra di dialogo di tooclose hello struttura del progetto.</span><span class="sxs-lookup"><span data-stu-id="98fea-151">Click **OK** tooclose hello Project Structure dialog box.</span></span>

    ![Open Module Settings (Apri impostazioni modulo)][05b]

<span data-ttu-id="98fea-153">Dopo aver configurato le impostazioni del modulo, è possibile pubblicare l'applicazione tooAzure utilizzando hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="98fea-153">When you have configured your module settings, you can publish your application tooAzure by using hello following steps:</span></span>

1. <span data-ttu-id="98fea-154">In Esplora progetti del IntelliJ pulsante destro del mouse hello **Java-Web-App-in-Azure** progetto.</span><span class="sxs-lookup"><span data-stu-id="98fea-154">In IntelliJ's Project Explorer, right-click hello **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="98fea-155">Quando viene visualizzato il menu di scelta rapida hello, selezionare **Azure**, quindi fare clic su **pubblica come App Web di Azure...**</span><span class="sxs-lookup"><span data-stu-id="98fea-155">When hello context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu di scelta rapida per la pubblicazione in Azure][06]
2. <span data-ttu-id="98fea-157">Se non hanno già effettuato l'accesso a Azure da IntelliJ, sarà richiesta toosign all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="98fea-157">If you have not already signed into Azure from IntelliJ, you will be prompted toosign into your Azure account.</span></span> <span data-ttu-id="98fea-158">(Se si dispone di più account di Azure, alcune delle richieste di hello durante il processo di accesso hello potrebbero essere visualizzati più volte, anche se appaiono toobe hello stesso.</span><span class="sxs-lookup"><span data-stu-id="98fea-158">(If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="98fea-159">In questo caso, continuare toofollow hello sign in istruzioni).</span><span class="sxs-lookup"><span data-stu-id="98fea-159">When this happens, continue toofollow hello sign in instructions.)</span></span>
   
    ![Finestra di accesso di Azure][07]
3. <span data-ttu-id="98fea-161">Dopo aver completato l'accesso all'account Azure, hello **Gestisci sottoscrizioni** la finestra di dialogo verrà visualizzato un elenco di sottoscrizioni associate le credenziali.</span><span class="sxs-lookup"><span data-stu-id="98fea-161">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="98fea-162">(Se sono presenti più sottoscrizioni elencate e si desidera toowork con solo un sottoinsieme specifico di essi, è possibile facoltativamente deselezionare sottoscrizioni hello non si desidera toouse.) Dopo aver selezionato le sottoscrizioni, fare clic su **Close**(Chiudi).</span><span class="sxs-lookup"><span data-stu-id="98fea-162">(If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello subscriptions you don't want toouse.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Gestisci sottoscrizioni][08]
4. <span data-ttu-id="98fea-164">Quando hello **tooAzure contenitore di App Web di distribuire** viene visualizzata la finestra di dialogo, verrà visualizzato qualsiasi contenitore di App Web creato in precedenza; se non è stato creato tutti i contenitori, elenco hello sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="98fea-164">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Contenitori di app][09]
5. <span data-ttu-id="98fea-166">Se non create un contenitore di App Web di Azure prima o se si desidera toopublish nel nuovo contenitore tooa di applicazione, utilizzare hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="98fea-166">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="98fea-167">In caso contrario, selezionare un contenitore di App Web esistente e ignorare toostep 6 seguente.</span><span class="sxs-lookup"><span data-stu-id="98fea-167">Otherwise, select an existing Web App Container and skip toostep 6 below.</span></span>
   
   1. <span data-ttu-id="98fea-168">Fare clic su **+**</span><span class="sxs-lookup"><span data-stu-id="98fea-168">Click **+**</span></span>
      
       ![Aggiungere un contenitore di app][10]
   2. <span data-ttu-id="98fea-170">Hello **nuovo contenitore di App Web** verrà visualizzata la finestra di dialogo, che sarà utilizzato per hello next diversi passaggi.</span><span class="sxs-lookup"><span data-stu-id="98fea-170">hello **New Web App Container** dialog box will be displayed, which will be used for hello next several steps.</span></span>
      
       ![Nuovo contenitore di app][11a]
   3. <span data-ttu-id="98fea-172">Immettere un **etichetta DNS** per il contenitore di App Web; verrà formato etichetta DNS foglia di hello dell'URL host hello per l'applicazione web in Azure.</span><span class="sxs-lookup"><span data-stu-id="98fea-172">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="98fea-173">Si noti che nome hello deve essere disponibile e conforme tooAzure requisiti di denominazione App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-173">Note that hello name must be available and conform tooAzure Web App naming requirements.</span></span>
   4. <span data-ttu-id="98fea-174">In hello **contenitore Web** dal menu a discesa, selezionare hello del software di appropriato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="98fea-174">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="98fea-175">Attualmente è possibile scegliere fra Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="98fea-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="98fea-176">Una distribuzione recente del software hello selezionata verrà fornita da Azure e verrà eseguito in una distribuzione recente di JDK 8 creata da Oracle e fornita da Azure.</span><span class="sxs-lookup"><span data-stu-id="98fea-176">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="98fea-177">In hello **sottoscrizione** dal menu a discesa, selezionare hello sottoscrizione toouse per questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="98fea-177">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="98fea-178">In hello **gruppo di risorse** dal menu a discesa, seleziona hello gruppo di risorse a cui si desidera tooassociate App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-178">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="98fea-179">(Gruppi di risorse di azure consente si toogroup correlate alle risorse in modo che, ad esempio, possibile eliminati insieme).</span><span class="sxs-lookup"><span data-stu-id="98fea-179">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="98fea-180">È possibile selezionare un gruppo di risorse esistente (se sono presenti) e Ignora toostep g seguente, o a seguito di hello utilizzare passaggi toocreate un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="98fea-180">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="98fea-181">Selezionare  **&lt; &lt; Crea nuovo gruppo di risorse &gt; &gt;**  in hello **gruppo di risorse** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="98fea-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in hello **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="98fea-182">Hello **nuovo gruppo di risorse** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="98fea-182">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nuovo gruppo di risorse][12]
      * <span data-ttu-id="98fea-184">In hello hello **nome** casella di testo, specificare un nome per il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98fea-184">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="98fea-185">In hello hello **area** menu a discesa, selezionare hello appropriato data center di Azure percorso per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="98fea-185">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="98fea-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="98fea-186">Click **OK**.</span></span>
   7. <span data-ttu-id="98fea-187">Hello **piano di servizio App** dal menu a discesa sono elencati i piani di servizio app hello associati hello gruppo di risorse selezionato.</span><span class="sxs-lookup"><span data-stu-id="98fea-187">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="98fea-188">(Un piano di servizio App consente di specificare informazioni quali il percorso di hello dell'App Web, hello piano tariffario e dimensioni di istanze di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="98fea-188">(An App Service Plan specifies information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="98fea-189">È possibile usare un singolo piano di servizio app per più app Web. Per questo motivo viene gestito separatamente da una distribuzione di app Web specifica.</span><span class="sxs-lookup"><span data-stu-id="98fea-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="98fea-190">È possibile selezionare un piano di servizio App esistente (se sono presenti) e ignorare toostep h riportato di seguito oppure utilizzare hello seguendo i passaggi toocreate un piano di servizio App nuovo:</span><span class="sxs-lookup"><span data-stu-id="98fea-190">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="98fea-191">Selezionare  **&lt; &lt; crea piano di servizio App nuovo &gt; &gt;**  in hello **piano di servizio App** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="98fea-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in hello **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="98fea-192">Hello **piano di servizio App nuovo** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="98fea-192">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nuovo piano di servizio app][13]
      * <span data-ttu-id="98fea-194">In hello hello **nome** casella di testo, specificare un nome per il piano di servizio App nuovo.</span><span class="sxs-lookup"><span data-stu-id="98fea-194">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="98fea-195">In hello hello **percorso** menu a discesa, selezionare hello appropriato data center di Azure percorso per il piano di hello.</span><span class="sxs-lookup"><span data-stu-id="98fea-195">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="98fea-196">In hello hello **tariffario** dal menu a discesa, seleziona hello prezzi per il piano di hello appropriato.</span><span class="sxs-lookup"><span data-stu-id="98fea-196">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="98fea-197">Ai fini del test è possibile scegliere **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="98fea-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="98fea-198">In hello hello **dimensioni istanze** dal menu a discesa, dimensioni di istanza appropriata di hello selezionare per il piano di hello.</span><span class="sxs-lookup"><span data-stu-id="98fea-198">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="98fea-199">Ai fini del test è possibile scegliere **Piccolo**.</span><span class="sxs-lookup"><span data-stu-id="98fea-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="98fea-200">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="98fea-200">Click **OK**.</span></span>
   8. <span data-ttu-id="98fea-201">(Facoltativo) Per impostazione predefinita, una distribuzione recente di Java 8 verrà automaticamente distribuita come la JVM dal contenitore di app web di Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="98fea-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure tooyour web app container.</span></span> <span data-ttu-id="98fea-202">Tuttavia, è possibile selezionare una versione diversa e la distribuzione di hello JVM.</span><span class="sxs-lookup"><span data-stu-id="98fea-202">However, you can select a different version and distribution of hello JVM.</span></span> <span data-ttu-id="98fea-203">toodo in tal caso, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="98fea-203">toodo so, use hello following steps:</span></span>
      
      * <span data-ttu-id="98fea-204">Fare clic su hello **JDK** scheda hello **nuovo contenitore di App Web** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="98fea-204">Click hello **JDK** tab in hello **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="98fea-205">È possibile scegliere una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="98fea-205">You can choose from one of hello following options:</span></span>
        
        * <span data-ttu-id="98fea-206">Distribuire predefinito hello JDK fornito da Azure</span><span class="sxs-lookup"><span data-stu-id="98fea-206">Deploy hello default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="98fea-207">Distribuire un JDK di terze parti da un elenco a discesa di altri JDK disponibili in Azure</span><span class="sxs-lookup"><span data-stu-id="98fea-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="98fea-208">Distribuire un JDK personalizzato, che deve essere compresso come file ZIP e disponibile pubblicamente o nell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="98fea-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Scheda JDK della finestra di dialogo New Web App Container (Nuovo contenitore app Web)][11b]
   9. <span data-ttu-id="98fea-210">Dopo aver completato tutti hello sopra passaggi, la finestra di dialogo Nuovo contenitore di App Web di hello dovrebbe essere simile a hello nella figura riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="98fea-210">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Nuovo contenitore di app][14]
   10. <span data-ttu-id="98fea-212">Fare clic su **OK** creazione hello toocomplete del nuovo contenitore App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-212">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="98fea-213">Attendere alcuni secondi per elenco hello di hello App Web contenitori toobe aggiornato e il contenitore di app web appena creato dovrebbe ora essere selezionato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="98fea-213">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
6. <span data-ttu-id="98fea-214">Si è ora pronto toocomplete hello la distribuzione iniziale di tooAzure l'App Web; Fare clic su **OK** toodeploy toohello di applicazione del linguaggio selezionato contenitore di App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-214">You are now ready toocomplete hello initial deployment of your Web App tooAzure; click **OK** toodeploy your Java application toohello selected Web App container.</span></span> <span data-ttu-id="98fea-215">Per impostazione predefinita, l'applicazione verrà distribuita come sottodirectory hello del server delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="98fea-215">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="98fea-216">Se si vuole toobe distribuito come applicazione radice hello, controllare hello **distribuire tooroot** casella di controllo prima di scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="98fea-216">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
   
    ![Distribuire tooAzure][15]
7. <span data-ttu-id="98fea-218">Successivamente, si dovrebbe essere hello **Log attività Azure** visualizzazione, che indica lo stato di distribuzione hello dell'App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-218">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Indicatore di stato][16]
   
    <span data-ttu-id="98fea-220">il processo di Hello di distribuzione tooAzure l'App Web debba richiedere solo pochi secondi toocomplete.</span><span class="sxs-lookup"><span data-stu-id="98fea-220">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="98fea-221">Quando l'inizio di applicazione, verrà visualizzato un collegamento denominato **pubblicato** in hello **stato** colonna.</span><span class="sxs-lookup"><span data-stu-id="98fea-221">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="98fea-222">Quando si fa clic sul collegamento hello, si passerà home page dell'App Web tooyour distribuito o è possibile utilizzare i passaggi di hello in hello seguente sezione toobrowse tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="98fea-222">When you click hello link, it will take you tooyour deployed Web App's home page, or you can use hello steps in hello following section toobrowse tooyour web app.</span></span>

## <a name="browsing-tooyour-web-app-on-azure"></a><span data-ttu-id="98fea-223">Esplorazione tooyour App Web in Azure</span><span class="sxs-lookup"><span data-stu-id="98fea-223">Browsing tooyour Web App on Azure</span></span>
<span data-ttu-id="98fea-224">toobrowse tooyour App Web in Azure, è possibile utilizzare hello **Esplora Azure** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="98fea-224">toobrowse tooyour Web App on Azure, you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="98fea-225">Se hello **Esplora Azure** vista non è già aperta, è possibile aprirlo facendo clic quindi **vista** IntelliJ, quindi scegliere **finestre degli strumenti**, quindi fare clic su  **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="98fea-225">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="98fea-226">Se non è stato precedentemente eseguito, verrà chiesto toodo così.</span><span class="sxs-lookup"><span data-stu-id="98fea-226">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="98fea-227">Quando hello **Esplora Azure** viene visualizzato, utilizzare seguire tooyour di toobrowse App Web questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="98fea-227">When hello **Azure Explorer** view is displayed, use follow these steps toobrowse tooyour Web App:</span></span> 

1. <span data-ttu-id="98fea-228">Espandere hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="98fea-228">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="98fea-229">Espandere hello **App Web** nodo.</span><span class="sxs-lookup"><span data-stu-id="98fea-229">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="98fea-230">Pulsante destro del mouse hello desiderato App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-230">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="98fea-231">Quando viene visualizzato il menu di scelta rapida hello, fare clic su **Apri nel Browser**.</span><span class="sxs-lookup"><span data-stu-id="98fea-231">When hello context menu appears, click **Open in Browser**.</span></span>
   
    ![Sfogliare l'app Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="98fea-233">Aggiornamento dell'app Web</span><span class="sxs-lookup"><span data-stu-id="98fea-233">Updating your web app</span></span>
<span data-ttu-id="98fea-234">L'aggiornamento di un'app Web di Azure in esecuzione è un processo semplice e rapido. Sono disponibili due opzioni per l'aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="98fea-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="98fea-235">È possibile aggiornare la distribuzione di hello di un'App Web Java esistente.</span><span class="sxs-lookup"><span data-stu-id="98fea-235">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="98fea-236">È possibile pubblicare un aggiuntiva toohello applicazione Java nello stesso contenitore di App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-236">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="98fea-237">In entrambi i casi, il processo di hello è identico e richiede solo pochi secondi:</span><span class="sxs-lookup"><span data-stu-id="98fea-237">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="98fea-238">In Esplora progetti di hello IntelliJ, fare doppio clic su un'applicazione Java hello desiderati tooupdate o aggiungere tooan contenitore di App Web esistente.</span><span class="sxs-lookup"><span data-stu-id="98fea-238">In hello IntelliJ project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="98fea-239">Quando viene visualizzato il menu di scelta rapida hello, selezionare **Azure** e quindi **pubblica come App Web di Azure...**</span><span class="sxs-lookup"><span data-stu-id="98fea-239">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="98fea-240">Poiché è già stato effettuato l'accesso in precedenza, verrà visualizzato un elenco dei contenitori di app Web esistenti.</span><span class="sxs-lookup"><span data-stu-id="98fea-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="98fea-241">Selezionare hello uno desiderati toopublish o pubblicare nuovamente il clic tooand di applicazioni Java **OK**.</span><span class="sxs-lookup"><span data-stu-id="98fea-241">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="98fea-242">Pochi secondi dopo, hello **Log attività Azure** visualizzazione saranno inclusi distribuzione aggiornata come **pubblicato** e si sarà in grado di tooverify l'applicazione aggiornata in un web browser.</span><span class="sxs-lookup"><span data-stu-id="98fea-242">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="98fea-243">Avvio, arresto o riavvio di un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="98fea-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="98fea-244">toostart o arrestare un contenitore di App Web di Azure esistente, (incluse tutte le applicazioni Java hello distribuito in essa contenuti), è possibile usare hello **Esplora Azure** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="98fea-244">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="98fea-245">Se hello **Esplora Azure** vista non è già aperta, è possibile aprirlo facendo clic quindi **vista** IntelliJ, quindi scegliere **finestre degli strumenti**, quindi fare clic su  **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="98fea-245">If hello **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="98fea-246">Se non è stato precedentemente eseguito, verrà chiesto toodo così.</span><span class="sxs-lookup"><span data-stu-id="98fea-246">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="98fea-247">Quando hello **Esplora Azure** viene visualizzato, utilizzare seguire questi passaggi toostart o arrestare l'App Web:</span><span class="sxs-lookup"><span data-stu-id="98fea-247">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="98fea-248">Espandere hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="98fea-248">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="98fea-249">Espandere hello **App Web** nodo.</span><span class="sxs-lookup"><span data-stu-id="98fea-249">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="98fea-250">Pulsante destro del mouse hello desiderato App Web.</span><span class="sxs-lookup"><span data-stu-id="98fea-250">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="98fea-251">Quando viene visualizzato il menu di scelta rapida hello, fare clic su **avviare**, **arrestare**, o **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="98fea-251">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="98fea-252">Si noti che le opzioni di menu hello che riconoscano il contesto, pertanto è possibile arrestare un'app web in esecuzione o avviare un'app web che non è attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="98fea-252">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Arrestare l'app Web][18]

## <a name="next-steps"></a><span data-ttu-id="98fea-254">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98fea-254">Next Steps</span></span>
<span data-ttu-id="98fea-255">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="98fea-255">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="98fea-256">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="98fea-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="98fea-257">[L'installazione di hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="98fea-257">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="98fea-258">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="98fea-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="98fea-259">[Novità in Azure Toolkit per Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="98fea-259">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="98fea-260">[Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="98fea-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="98fea-261">[installazione hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="98fea-261">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="98fea-262">*Creare un’app Web Hello World per Azure in IntelliJ (questo articolo)*</span><span class="sxs-lookup"><span data-stu-id="98fea-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="98fea-263">[Novità in Azure Toolkit per IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="98fea-263">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="98fea-264">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="98fea-264">See Also</span></span>
<span data-ttu-id="98fea-265">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="98fea-265">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="98fea-266">Per ulteriori informazioni sulla creazione di App Web di Azure, vedere hello [Panoramica di App Web].</span><span class="sxs-lookup"><span data-stu-id="98fea-266">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[installazione hello Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novità in Azure Toolkit per Eclipse hello]: ../azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ../azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Panoramica di App Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-SDK-Dialog.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05a]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Module-Settings.png
[05b]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Project-Structure-Dialog.png
[05c]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11a]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[11b]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container-JDK-Tab.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png
