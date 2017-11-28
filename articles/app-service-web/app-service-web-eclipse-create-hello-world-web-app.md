---
title: aaaCreate un'app web basic di Azure usando Eclipse | Documenti Microsoft
description: Questa esercitazione viene illustrato come toouse hello Azure Toolkit per Eclipse toocreate un'App Web di Hello World per Azure.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: b2f42e0e7a5b98760ec02fab2fc38f9f07b1156b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="94891-103">Creare un'app Web di base di Azure con Eclipse</span><span class="sxs-lookup"><span data-stu-id="94891-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="94891-104">Questa esercitazione viene illustrato come toocreate e distribuire una base tooAzure applicazione Hello World come un'App Web utilizzando hello [Azure Toolkit per Eclipse].</span><span class="sxs-lookup"><span data-stu-id="94891-104">This tutorial shows how toocreate and deploy a basic Hello World application tooAzure as a Web App by using hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="94891-105">Per semplicità è riportato un esempio JSP di base, ma è possibile adottare una procedura simile anche per un servlet Java, per quanto riguarda la distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="94891-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="94891-106">Dopo aver completato questa esercitazione, l'applicazione avrà un aspetto simile toohello seguente illustrazione, quando viene visualizzata in un web browser:</span><span class="sxs-lookup"><span data-stu-id="94891-106">When you have completed this tutorial, your application will look similar toohello following illustration when you view it in a web browser:</span></span>

![Anteprima dell'app Hello World][01]

## <a name="prerequisites"></a><span data-ttu-id="94891-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94891-108">Prerequisites</span></span>
* <span data-ttu-id="94891-109">Java Developer Kit (JDK) versione 1.8 o successiva.</span><span class="sxs-lookup"><span data-stu-id="94891-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="94891-110">IDE Eclipse per sviluppatori Java EE, Luna o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="94891-110">Eclipse IDE for Java EE Developers, Luna or later.</span></span> <span data-ttu-id="94891-111">È possibile scaricare il pacchetto all'indirizzo <http://www.eclipse.org/downloads/>.</span><span class="sxs-lookup"><span data-stu-id="94891-111">This can be downloaded from <http://www.eclipse.org/downloads/>.</span></span>
* <span data-ttu-id="94891-112">Distribuzione di un server Web basato su Java o un server applicazioni, ad esempio [Apache Tomcat] o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="94891-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="94891-113">Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="94891-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="94891-114">Hello [Azure Toolkit per Eclipse].</span><span class="sxs-lookup"><span data-stu-id="94891-114">hello [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="94891-115">Per informazioni sull'installazione hello Azure Toolkit, vedere [installazione hello Azure Toolkit per Eclipse].</span><span class="sxs-lookup"><span data-stu-id="94891-115">For information about installing hello Azure Toolkit, see [Installing hello Azure Toolkit for Eclipse].</span></span>

## <a name="toocreate-a-hello-world-application"></a><span data-ttu-id="94891-116">toocreate un'applicazione Hello World</span><span class="sxs-lookup"><span data-stu-id="94891-116">toocreate a Hello World application</span></span>
<span data-ttu-id="94891-117">Creare innanzitutto un progetto Java.</span><span class="sxs-lookup"><span data-stu-id="94891-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="94891-118">Avviare Eclipse e nel menu hello scegliere **File**, fare clic su **New**, quindi fare clic su **progetto Web dinamico**.</span><span class="sxs-lookup"><span data-stu-id="94891-118">Start Eclipse, and at hello menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="94891-119">(Se non viene visualizzato **progetto Web dinamico** elencati tra i progetti disponibili dopo aver fatto clic **File** e **New**, quindi hello seguente: fare clic su **File**, fare clic su **New**, fare clic su **progetto...** , espandere **Web**, fare clic su **progetto Web dinamico**, fare clic su **Avanti**.)</span><span class="sxs-lookup"><span data-stu-id="94891-119">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do hello following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>
2. <span data-ttu-id="94891-120">Ai fini di questa esercitazione, denominare il progetto di hello **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="94891-120">For purposes of this tutorial, name hello project **MyWebApp**.</span></span> <span data-ttu-id="94891-121">Verrà visualizzata una schermata simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="94891-121">Your screen will appear similar toohello following:</span></span>
   
    ![Creazione di un nuovo progetto Web dinamico][02]
3. <span data-ttu-id="94891-123">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="94891-123">Click **Finish**.</span></span>
4. <span data-ttu-id="94891-124">Nella visualizzazione Project Explorer (Esplora progetti) di Eclipse espandere **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="94891-124">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="94891-125">Fare clic con il pulsante destro del mouse su **WebContent**, scegliere **New** e quindi fare clic su **JSP File**.</span><span class="sxs-lookup"><span data-stu-id="94891-125">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
5. <span data-ttu-id="94891-126">In hello **New JSP File** della finestra di dialogo file hello nome **index.jsp**, mantenere come cartella padre di hello **MyWebApp/WebContent**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="94891-126">In hello **New JSP File** dialog box, name hello file **index.jsp**, keep hello parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>
6. <span data-ttu-id="94891-127">In hello **Select JSP Template** la finestra di dialogo, ai fini di questa esercitazione, selezionare **New JSP File (html)**, quindi fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="94891-127">In hello **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
7. <span data-ttu-id="94891-128">All'apertura del file index.jsp in Eclipse, aggiungere la visualizzazione del testo toodynamically **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="94891-128">When your index.jsp file opens in Eclipse, add in text toodynamically display **Hello World!**</span></span> <span data-ttu-id="94891-129">all'interno di hello esistente `<body>` elemento.</span><span class="sxs-lookup"><span data-stu-id="94891-129">within hello existing `<body>` element.</span></span> <span data-ttu-id="94891-130">L'aggiornamento `<body>` contenuto dovrebbe essere simile a hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="94891-130">Your updated `<body>` content should resemble hello following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
8. <span data-ttu-id="94891-131">Salvare index.jsp.</span><span class="sxs-lookup"><span data-stu-id="94891-131">Save index.jsp.</span></span>

## <a name="toodeploy-your-application-tooan-azure-web-app-container"></a><span data-ttu-id="94891-132">toodeploy il tooan applicazione contenitore di App Web di Azure</span><span class="sxs-lookup"><span data-stu-id="94891-132">toodeploy your application tooan Azure Web App Container</span></span>
<span data-ttu-id="94891-133">Esistono diversi modi con cui è possibile distribuire un tooAzure di applicazione web Java.</span><span class="sxs-lookup"><span data-stu-id="94891-133">There are several ways by which you can deploy a Java web application tooAzure.</span></span> <span data-ttu-id="94891-134">Questa esercitazione viene descritto uno dei più semplice hello: l'applicazione sarà distribuito tooan contenitore di App Web di Azure: nessun tipo di progetto speciale né altri strumenti sono necessari.</span><span class="sxs-lookup"><span data-stu-id="94891-134">This tutorial describes one of hello simplest: your application will be deployed tooan Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="94891-135">Hello JDK hello web contenitore software e verrà fornito automaticamente da Azure, pertanto non c'è alcuna necessità tooupload proprio; è sufficiente l'App Web Java.</span><span class="sxs-lookup"><span data-stu-id="94891-135">hello JDK and hello web container software will be provided for you by Azure, so there is no need tooupload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="94891-136">Di conseguenza, processo di pubblicazione per l'applicazione hello richiederà secondi, minuti non.</span><span class="sxs-lookup"><span data-stu-id="94891-136">As a result, hello publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="94891-137">In Project Explorer (Esplora progetti) di Eclipse fare clic con il pulsante destro del mouse su **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="94891-137">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>
2. <span data-ttu-id="94891-138">Nel menu di scelta rapida hello, selezionare **Azure**, quindi fare clic su **pubblica come App Web di Azure...**</span><span class="sxs-lookup"><span data-stu-id="94891-138">In hello context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
    ![Publish as Azure Web App][03]
   
    <span data-ttu-id="94891-140">In alternativa, mentre il progetto di applicazione web è stato selezionato in Esplora progetti hello, è possibile fare clic su hello **pubblica** pulsante a discesa sulla barra degli strumenti hello e selezionare **pubblica come App Web di Azure** da qui:</span><span class="sxs-lookup"><span data-stu-id="94891-140">Alternatively, while your web application project is selected in hello Project Explorer, you can click hello **Publish** dropdown button on hello toolbar and select **Publish as Azure Web App** from there:</span></span>
   
    ![Publish as Azure Web App][14]
3. <span data-ttu-id="94891-142">Se non hanno già effettuato l'accesso a Azure da Eclipse, sarà possibile toosign richiesta nell'account Azure:</span><span class="sxs-lookup"><span data-stu-id="94891-142">If you have not already signed into Azure from Eclipse, you will be prompted toosign into your Azure account:</span></span>
   
    ![Finestra di dialogo di accesso di Azure][04]
   
    <span data-ttu-id="94891-144">Se si dispone di più account di Azure, alcune delle richieste di hello durante hello Accedi processo potrebbe essere visualizzato più volte, anche se appaiono toobe hello stesso.</span><span class="sxs-lookup"><span data-stu-id="94891-144">If you have multiple Azure accounts, some of hello prompts during hello sign in process may be shown more than once, even if they appear toobe hello same.</span></span> <span data-ttu-id="94891-145">In questo caso, continuare dopo il segno di hello nelle istruzioni.</span><span class="sxs-lookup"><span data-stu-id="94891-145">When this happens, continue following hello sign in instructions.</span></span>
4. <span data-ttu-id="94891-146">Dopo aver completato l'accesso all'account Azure, hello **Gestisci sottoscrizioni** la finestra di dialogo verrà visualizzato un elenco di sottoscrizioni associate le credenziali.</span><span class="sxs-lookup"><span data-stu-id="94891-146">After you have successfully signed into your Azure account, hello **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="94891-147">Se sono presenti più sottoscrizioni elencate e si desidera toowork con solo un sottoinsieme specifico di essi, è possibile deselezionare l'opzione hello desiderati toouse.</span><span class="sxs-lookup"><span data-stu-id="94891-147">If there are multiple subscriptions listed and you want toowork with only a specific subset of them, you may optionally uncheck hello ones you do want toouse.</span></span> <span data-ttu-id="94891-148">Dopo aver selezionato le sottoscrizioni, fare clic su **Close**(Chiudi).</span><span class="sxs-lookup"><span data-stu-id="94891-148">When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Finestra di dialogo Gestisci sottoscrizioni][05]
5. <span data-ttu-id="94891-150">Quando hello **tooAzure contenitore di App Web di distribuire** viene visualizzata la finestra di dialogo, verrà visualizzato qualsiasi contenitore di App Web creato in precedenza; se non è stato creato tutti i contenitori, elenco hello sarà vuoto.</span><span class="sxs-lookup"><span data-stu-id="94891-150">When hello **Deploy tooAzure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, hello list will be empty.</span></span>
   
    ![Distribuire la finestra di dialogo di tooAzure contenitore di App Web][06]
6. <span data-ttu-id="94891-152">Se non create un contenitore di App Web di Azure prima o se si desidera toopublish nel nuovo contenitore tooa di applicazione, utilizzare hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="94891-152">If you have not created an Azure Web App Container before, or if you would like toopublish your application tooa new container, use hello following steps.</span></span> <span data-ttu-id="94891-153">In caso contrario, selezionare un contenitore di App Web esistente e ignorare toostep 7 seguente.</span><span class="sxs-lookup"><span data-stu-id="94891-153">Otherwise, select an existing Web App Container and skip toostep 7 below.</span></span>
   
   1. <span data-ttu-id="94891-154">Fare clic su **Nuovo**</span><span class="sxs-lookup"><span data-stu-id="94891-154">Click **New...**</span></span>
      
       ![Distribuire la finestra di dialogo di tooAzure contenitore di App Web][15]
   2. <span data-ttu-id="94891-156">Hello **nuovo contenitore di App Web** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="94891-156">hello **New Web App Container** dialog box will be displayed:</span></span>
      
       ![Finestra di dialogo New Web App Container (Nuovo contenitore App Web)][07a]
   3. <span data-ttu-id="94891-158">Immettere un **etichetta DNS** per il contenitore di App Web; verrà formato etichetta DNS foglia di hello dell'URL host hello per l'applicazione web in Azure.</span><span class="sxs-lookup"><span data-stu-id="94891-158">Enter a **DNS Label** for your Web App Container; this will form hello leaf DNS label of hello host URL for your web application in Azure.</span></span> <span data-ttu-id="94891-159">Si noti che nome hello deve essere disponibile e conforme tooAzure requisiti di denominazione App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-159">(Note that hello name must be available and conform tooAzure Web App naming requirements.)</span></span>
   4. <span data-ttu-id="94891-160">In hello **contenitore Web** dal menu a discesa, selezionare hello del software di appropriato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94891-160">In hello **Web Container** drop-down menu, select hello appropriate software for your application.</span></span>
      
       <span data-ttu-id="94891-161">Attualmente è possibile scegliere fra Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="94891-161">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="94891-162">Una distribuzione recente del software hello selezionata verrà fornita da Azure e verrà eseguito in una distribuzione recente di JDK 8 creata da Oracle e fornita da Azure.</span><span class="sxs-lookup"><span data-stu-id="94891-162">A recent distribution of hello selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="94891-163">In hello **sottoscrizione** dal menu a discesa, selezionare hello sottoscrizione toouse per questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="94891-163">In hello **Subscription** drop-down menu, select hello subscription you want toouse for this deployment.</span></span>
   6. <span data-ttu-id="94891-164">In hello **gruppo di risorse** dal menu a discesa, seleziona hello gruppo di risorse a cui si desidera tooassociate App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-164">In hello **Resource Group** drop-down menu, select hello Resource Group with which you want tooassociate your Web App.</span></span> <span data-ttu-id="94891-165">(Gruppi di risorse di azure consente si toogroup correlate alle risorse in modo che, ad esempio, possibile eliminati insieme).</span><span class="sxs-lookup"><span data-stu-id="94891-165">(Azure Resource Groups allow you toogroup related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="94891-166">È possibile selezionare un gruppo di risorse esistente (se sono presenti) e Ignora toostep g seguente o utilizzare hello seguendo questi passaggi toocreate un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="94891-166">You can select an existing Resource Group (if you have any) and skip toostep g below, or use hello following these steps toocreate a new Resource Group:</span></span>
      
      * <span data-ttu-id="94891-167">Fare clic su **Nuovo**</span><span class="sxs-lookup"><span data-stu-id="94891-167">Click **New...**</span></span>
      * <span data-ttu-id="94891-168">Hello **nuovo gruppo di risorse** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="94891-168">hello **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Finestra di dialogo Nuovo gruppo di risorse][08]
      * <span data-ttu-id="94891-170">In hello hello **nome** casella di testo, specificare un nome per il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="94891-170">In hello hello **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="94891-171">In hello hello **area** menu a discesa, selezionare hello appropriato data center di Azure percorso per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="94891-171">In hello hello **Region** drop-down menu, select hello appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="94891-172">Facoltativo: Per impostazione predefinita, una distribuzione recente di Java 8 verrà distribuita da Azure automaticamente il contenitore di app web di tooyour come la JVM.</span><span class="sxs-lookup"><span data-stu-id="94891-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically tooyour web app container as your JVM.</span></span> <span data-ttu-id="94891-173">Tuttavia, è possibile specificare una versione diversa e la distribuzione di hello JVM se richiesto per l'App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-173">However, you can specify a different version and distribution of hello JVM if your Web App requires it.</span></span> <span data-ttu-id="94891-174">hello toospecify JDK per l'App Web, fare clic su hello **JDK** scheda e selezionare una delle seguenti opzioni hello:</span><span class="sxs-lookup"><span data-stu-id="94891-174">toospecify hello JDK for your Web App, click hello **JDK** tab, and select one of hello following options:</span></span>
        
        * <span data-ttu-id="94891-175">**Distribuire predefinito hello JDK offerta dal servizio App Web di Azure**: questa opzione verrà distribuito a una distribuzione recente di Java 8.</span><span class="sxs-lookup"><span data-stu-id="94891-175">**Deploy hello default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
        * <span data-ttu-id="94891-176">**Distribuire una 3rd party JDK disponibile in Azure**: questa opzione consente di toochoose dall'elenco di hello di JDK forniti da Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="94891-176">**Deploy a 3rd party JDK available on Azure**: This option allows you toochoose from hello list of JDKs which are provided by Microsoft Azure.</span></span>
        * <span data-ttu-id="94891-177">**Distribuzione di JDK da questo percorso di download**: questa opzione consente di toospecify la propria distribuzione di JDK, che deve essere compresso come un file ZIP e caricati tooeither un percorso di download disponibile pubblicamente o una risorsa di archiviazione di Azure con un account per il quale si ha accesso.</span><span class="sxs-lookup"><span data-stu-id="94891-177">**Deploy my own JDK from this download location**: This option allows you toospecify your own JDK distribution, which must be packaged as a ZIP file and uploaded tooeither a publicly available download location or an Azure storage account for which you have access.</span></span>
          
          ![Finestra di dialogo New Web App Container (Nuovo contenitore App Web)][07b]
   7. <span data-ttu-id="94891-179">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="94891-179">Click **OK**.</span></span>
   8. <span data-ttu-id="94891-180">Hello **piano di servizio App** dal menu a discesa sono elencati i piani di servizio app hello associati hello gruppo di risorse selezionato.</span><span class="sxs-lookup"><span data-stu-id="94891-180">hello **App Service Plan** drop-down menu lists hello app service plans that are associated with hello Resource Group that you selected.</span></span> <span data-ttu-id="94891-181">(I piani di servizio app consente di specificare informazioni quali il percorso di hello dell'App Web, hello piano tariffario e dimensioni di istanze di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="94891-181">(App Service Plans specify information such as hello location of your Web App, hello pricing tier and hello compute instance size.</span></span> <span data-ttu-id="94891-182">È possibile usare un singolo piano di servizio app per più app Web. Per questo motivo viene gestito separatamente da una distribuzione di app Web specifica.</span><span class="sxs-lookup"><span data-stu-id="94891-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="94891-183">È possibile selezionare un piano di servizio App esistente (se sono presenti) e ignorare toostep h riportato di seguito oppure utilizzare hello seguendo questi passaggi toocreate un piano di servizio App nuovo:</span><span class="sxs-lookup"><span data-stu-id="94891-183">You can select an existing App Service Plan (if you have any) and skip toostep h below, or use hello following these steps toocreate a new App Service Plan:</span></span>
      
      * <span data-ttu-id="94891-184">Fare clic su **Nuovo**</span><span class="sxs-lookup"><span data-stu-id="94891-184">Click **New...**</span></span>
      * <span data-ttu-id="94891-185">Hello **piano di servizio App nuovo** verrà visualizzata la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="94891-185">hello **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Finestra di dialogo New App Service Plan (Nuovo piano di servizio app)][09]
      * <span data-ttu-id="94891-187">In hello hello **nome** casella di testo, specificare un nome per il piano di servizio App nuovo.</span><span class="sxs-lookup"><span data-stu-id="94891-187">In hello hello **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="94891-188">In hello hello **percorso** menu a discesa, selezionare hello appropriato data center di Azure percorso per il piano di hello.</span><span class="sxs-lookup"><span data-stu-id="94891-188">In hello hello **Location** drop-down menu, select hello appropriate Azure data center location for hello plan.</span></span>
      * <span data-ttu-id="94891-189">In hello hello **tariffario** dal menu a discesa, seleziona hello prezzi per il piano di hello appropriato.</span><span class="sxs-lookup"><span data-stu-id="94891-189">In hello hello **Pricing Tier** drop-down menu, select hello appropriate pricing for hello plan.</span></span> <span data-ttu-id="94891-190">Ai fini del test è possibile scegliere **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="94891-190">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="94891-191">In hello hello **dimensioni istanze** dal menu a discesa, dimensioni di istanza appropriata di hello selezionare per il piano di hello.</span><span class="sxs-lookup"><span data-stu-id="94891-191">In hello hello **Instance Size** drop-down menu, select hello appropriate instance size for hello plan.</span></span> <span data-ttu-id="94891-192">Ai fini del test è possibile scegliere **Piccolo**.</span><span class="sxs-lookup"><span data-stu-id="94891-192">For testing purposes you can choose **Small**.</span></span>
   9. <span data-ttu-id="94891-193">Dopo aver completato tutti hello sopra passaggi, la finestra di dialogo Nuovo contenitore di App Web di hello dovrebbe essere simile a hello nella figura riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="94891-193">Once you have completed all of hello above steps, hello New Web App Container dialog box should resemble hello following illustration:</span></span>
      
       ![Finestra di dialogo New Web App Container (Nuovo contenitore App Web)][10]
   10. <span data-ttu-id="94891-195">Fare clic su **OK** creazione hello toocomplete del nuovo contenitore App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-195">Click **OK** toocomplete hello creation of your new Web App container.</span></span>
       
        <span data-ttu-id="94891-196">Attendere alcuni secondi per elenco hello di hello App Web contenitori toobe aggiornato e il contenitore di app web appena creato dovrebbe ora essere selezionato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="94891-196">Wait a few seconds for hello list of hello Web App containers toobe refreshed, and your newly-created web app container should now be selected in hello list.</span></span>
7. <span data-ttu-id="94891-197">Si è ora pronto toocomplete hello la distribuzione iniziale di tooAzure l'App Web:</span><span class="sxs-lookup"><span data-stu-id="94891-197">You are now ready toocomplete hello initial deployment of your Web App tooAzure:</span></span>
   
    ![Distribuire la finestra di dialogo di tooAzure contenitore di App Web][11]
   
    <span data-ttu-id="94891-199">Fare clic su **OK** toodeploy toohello di applicazione del linguaggio selezionato contenitore di App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-199">Click **OK** toodeploy your Java application toohello selected Web App container.</span></span>
   
    <span data-ttu-id="94891-200">Per impostazione predefinita, l'applicazione verrà distribuita come sottodirectory hello del server delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="94891-200">By default, your application will be deployed as a subdirectory of hello application server.</span></span> <span data-ttu-id="94891-201">Se si vuole toobe distribuito come applicazione radice hello, controllare hello **distribuire tooroot** casella di controllo prima di scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="94891-201">If you want it toobe deployed as hello root application, check hello **Deploy tooroot** checkbox before clicking **OK**.</span></span>
8. <span data-ttu-id="94891-202">Successivamente, si dovrebbe essere hello **Log attività Azure** visualizzazione, che indica lo stato di distribuzione hello dell'App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-202">Next, you should see hello **Azure Activity Log** view, which will indicate hello deployment status of your Web App.</span></span>
   
    ![Azure Activity Log][12]
   
    <span data-ttu-id="94891-204">il processo di Hello di distribuzione tooAzure l'App Web debba richiedere solo pochi secondi toocomplete.</span><span class="sxs-lookup"><span data-stu-id="94891-204">hello process of deploying your Web App tooAzure should take only a few seconds toocomplete.</span></span> <span data-ttu-id="94891-205">Quando l'inizio di applicazione, verrà visualizzato un collegamento denominato **pubblicato** in hello **stato** colonna.</span><span class="sxs-lookup"><span data-stu-id="94891-205">When your application ready, you will see a link named **Published** in hello **Status** column.</span></span> <span data-ttu-id="94891-206">Quando si fa clic sul collegamento hello, si passerà home page dell'App Web tooyour distribuito.</span><span class="sxs-lookup"><span data-stu-id="94891-206">When you click hello link, it will take you tooyour deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="94891-207">Aggiornamento dell'app Web</span><span class="sxs-lookup"><span data-stu-id="94891-207">Updating your web app</span></span>
<span data-ttu-id="94891-208">L'aggiornamento di un'app Web di Azure in esecuzione è un processo semplice e rapido. Sono disponibili due opzioni per l'aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="94891-208">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="94891-209">È possibile aggiornare la distribuzione di hello di un'App Web Java esistente.</span><span class="sxs-lookup"><span data-stu-id="94891-209">You can update hello deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="94891-210">È possibile pubblicare un aggiuntiva toohello applicazione Java nello stesso contenitore di App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-210">You can publish an additional Java application toohello same Web App Container.</span></span>

<span data-ttu-id="94891-211">In entrambi i casi, il processo di hello è identico e richiede solo pochi secondi:</span><span class="sxs-lookup"><span data-stu-id="94891-211">In either case, hello process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="94891-212">In Esplora progetti di Eclipse hello, fare doppio clic su un'applicazione Java hello desiderati tooupdate o aggiungere tooan contenitore di App Web esistente.</span><span class="sxs-lookup"><span data-stu-id="94891-212">In hello Eclipse project explorer, right-click hello Java application you want tooupdate or add tooan existing Web App Container.</span></span>
2. <span data-ttu-id="94891-213">Quando viene visualizzato il menu di scelta rapida hello, selezionare **Azure** e quindi **pubblica come App Web di Azure...**</span><span class="sxs-lookup"><span data-stu-id="94891-213">When hello context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="94891-214">Poiché è già stato effettuato l'accesso in precedenza, verrà visualizzato un elenco dei contenitori di app Web esistenti.</span><span class="sxs-lookup"><span data-stu-id="94891-214">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="94891-215">Selezionare hello uno desiderati toopublish o pubblicare nuovamente il clic tooand di applicazioni Java **OK**.</span><span class="sxs-lookup"><span data-stu-id="94891-215">Select hello one you want toopublish or re-publish your Java application tooand click **OK**.</span></span>

<span data-ttu-id="94891-216">Pochi secondi dopo, hello **Log attività Azure** visualizzazione saranno inclusi distribuzione aggiornata come **pubblicato** e si sarà in grado di tooverify l'applicazione aggiornata in un web browser.</span><span class="sxs-lookup"><span data-stu-id="94891-216">A few seconds later, hello **Azure Activity Log** view will show your updated deployment as **Published** and you will be able tooverify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="94891-217">Avvio, arresto o riavvio di un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="94891-217">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="94891-218">toostart o arrestare un contenitore di App Web di Azure esistente, (incluse tutte le applicazioni Java hello distribuito in essa contenuti), è possibile usare hello **Esplora Azure** visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="94891-218">toostart or stop an existing Azure Web App container, (including all hello deployed Java applications in it), you can use hello **Azure Explorer** view.</span></span>

<span data-ttu-id="94891-219">Se hello **Esplora Azure** vista non è già aperta, è possibile aprirlo facendo clic quindi **finestra** menu in Eclipse, quindi fare clic su **Mostra visualizzazione**, quindi **altri...** , quindi **Azure**, quindi fare clic su **Esplora Azure**.</span><span class="sxs-lookup"><span data-stu-id="94891-219">If hello **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="94891-220">Se non è stato precedentemente eseguito, verrà chiesto toodo così.</span><span class="sxs-lookup"><span data-stu-id="94891-220">If you have not previously logged in, it will prompt you toodo so.</span></span>

<span data-ttu-id="94891-221">Quando hello **Esplora Azure** viene visualizzato, utilizzare seguire questi passaggi toostart o arrestare l'App Web:</span><span class="sxs-lookup"><span data-stu-id="94891-221">When hello **Azure Explorer** view is displayed, use follow these steps toostart or stop your Web App:</span></span> 

1. <span data-ttu-id="94891-222">Espandere hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="94891-222">Expand hello **Azure** node.</span></span>
2. <span data-ttu-id="94891-223">Espandere hello **App Web** nodo.</span><span class="sxs-lookup"><span data-stu-id="94891-223">Expand hello **Web Apps** node.</span></span> 
3. <span data-ttu-id="94891-224">Pulsante destro del mouse hello desiderato App Web.</span><span class="sxs-lookup"><span data-stu-id="94891-224">Right-click hello desired Web App.</span></span>
4. <span data-ttu-id="94891-225">Quando viene visualizzato il menu di scelta rapida hello, fare clic su **avviare**, **arrestare**, o **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="94891-225">When hello context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="94891-226">Si noti che le opzioni di menu hello che riconoscano il contesto, pertanto è possibile arrestare un'app web in esecuzione o avviare un'app web che non è attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94891-226">Note that hello menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Arresto di un'app Web esistente][13]

## <a name="next-steps"></a><span data-ttu-id="94891-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94891-228">Next Steps</span></span>
<span data-ttu-id="94891-229">Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="94891-229">For more information about hello Azure Toolkits for Java IDEs, see hello following links:</span></span>

* <span data-ttu-id="94891-230">[Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94891-230">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="94891-231">[installazione hello Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="94891-231">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="94891-232">*Creare un’app Web Hello World per Azure in Eclipse (questo articolo)*</span><span class="sxs-lookup"><span data-stu-id="94891-232">*Create a Hello World Web App for Azure in Eclipse (This Article)*</span></span>
  * <span data-ttu-id="94891-233">[Novità in Azure Toolkit per Eclipse hello]</span><span class="sxs-lookup"><span data-stu-id="94891-233">[What's New in hello Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="94891-234">[Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94891-234">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="94891-235">[Installazione di hello Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94891-235">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="94891-236">[Creare un'App Web Hello World per Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="94891-236">[Create a Hello World Web App for Azure in IntelliJ]</span></span>
  * <span data-ttu-id="94891-237">[Novità in Azure Toolkit per IntelliJ hello]</span><span class="sxs-lookup"><span data-stu-id="94891-237">[What's New in hello Azure Toolkit for IntelliJ]</span></span>

<span data-ttu-id="94891-238">Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="94891-238">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<span data-ttu-id="94891-239">Per ulteriori informazioni sulla creazione di App Web di Azure, vedere hello [Panoramica di App Web].</span><span class="sxs-lookup"><span data-stu-id="94891-239">For additional information about creating Azure Web Apps, see hello [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ../azure-toolkit-for-intellij.md
[Create a Hello World Web App for Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[installazione hello Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novità in Azure Toolkit per Eclipse hello]: ../azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ../azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Panoramica di App Web]: ./app-service-web-overview.md
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/app-service-web-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/app-service-web-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/app-service-web-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/app-service-web-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/app-service-web-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/app-service-web-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/app-service-web-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/app-service-web-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/app-service-web-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/app-service-web-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/app-service-web-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/app-service-web-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/app-service-web-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/app-service-web-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/app-service-web-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
