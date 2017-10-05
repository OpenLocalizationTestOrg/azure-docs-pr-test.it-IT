---
title: Creare un'app Web di base di Azure in IntelliJ | Documentazione Microsoft
description: Questa esercitazione spiega come usare Azure Toolkit per IntelliJ per creare un'app Web Hello World per Azure.
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
ms.openlocfilehash: 20b2c3d86f5bde9302647f345aa99b030d78613a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-basic-azure-web-app-in-intellij"></a><span data-ttu-id="8d0ce-103">Creare un'app Web di base di Azure in IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8d0ce-103">Create a basic Azure web app in IntelliJ</span></span>
<span data-ttu-id="8d0ce-104">Questa esercitazione spiega come creare e distribuire un'applicazione Hello World di base in Azure come app Web usando [Azure Toolkit per IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="8d0ce-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="8d0ce-105">Per semplicità è riportato un esempio JSP di base, ma è possibile adottare una procedura simile anche per un servlet Java, per quanto riguarda la distribuzione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="8d0ce-106">Al termine di questa esercitazione, l'applicazione visualizzata in un browser Web avrà un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Pagina Web di esempio][01]

## <a name="prerequisites"></a><span data-ttu-id="8d0ce-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8d0ce-108">Prerequisites</span></span>
* <span data-ttu-id="8d0ce-109">Java Developer Kit (JDK) versione 1.8 o successiva.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-109">A Java Developer Kit (JDK), v 1.8 or later.</span></span>
* <span data-ttu-id="8d0ce-110">IntelliJ IDEA Ultimate Edition.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-110">IntelliJ IDEA Ultimate Edition.</span></span> <span data-ttu-id="8d0ce-111">È possibile scaricarlo da <https://www.jetbrains.com/idea/download/index.html>.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-111">This can be downloaded from <https://www.jetbrains.com/idea/download/index.html>.</span></span>
* <span data-ttu-id="8d0ce-112">Distribuzione di un server Web basato su Java o un server applicazioni, ad esempio [Apache Tomcat] o [Jetty].</span><span class="sxs-lookup"><span data-stu-id="8d0ce-112">A distribution of a Java-based web server or application server, such as [Apache Tomcat] or [Jetty].</span></span>
* <span data-ttu-id="8d0ce-113">Una sottoscrizione di Azure, che può essere ottenuta all'indirizzo <https://azure.microsoft.com/free/> o <http://azure.microsoft.com/pricing/purchase-options/>.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-113">An Azure subscription, which can be acquired from <https://azure.microsoft.com/free/> or <http://azure.microsoft.com/pricing/purchase-options/>.</span></span>
* <span data-ttu-id="8d0ce-114">[Azure Toolkit per IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="8d0ce-114">The [Azure Toolkit for IntelliJ].</span></span> <span data-ttu-id="8d0ce-115">Per informazioni sull'installazione di Azure Toolkit, vedere [Installazione di Azure Toolkit for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="8d0ce-115">For information about installing the Azure Toolkit, see [Installing the Azure Toolkit for IntelliJ].</span></span>

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="8d0ce-116">Creare un'applicazione Hello World JSP</span><span class="sxs-lookup"><span data-stu-id="8d0ce-116">To create a Hello World application</span></span>
<span data-ttu-id="8d0ce-117">Creare innanzitutto un progetto Java.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-117">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="8d0ce-118">Avviare IntelliJ e fare clic sul menu **File**, quindi su **New** (Nuovo) e su **Project** (Progetto).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-118">Start IntelliJ and click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
    ![File > New Project (Nuovo progetto)][02]
2. <span data-ttu-id="8d0ce-120">Nella finestra di dialogo New Project (Nuovo progetto) selezionare **Java**, quindi **Web Application** (Applicazione Web) e fare clic su **Next** (Avanti) per aggiungere un SDK di progetto.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-120">In the New Project dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
    ![Finestra di dialogo Nuovo progetto][03a]
   
3. <span data-ttu-id="8d0ce-122">Nella finestra di dialogo Select Home Directory for JDK (Selezionare la home directory per JDK), selezionare la cartella in cui è installato JDK e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-122">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="8d0ce-123">Fare clic su **Next** (Avanti) nella finestra di dialogo New Project (Nuovo progetto) per continuare.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-123">Click **Next** in the New Project dialog box to continue.</span></span>
   
    ![Specificare la home directory di JDK][03b]
4. <span data-ttu-id="8d0ce-125">Ai fini di questa esercitazione, denominare il progetto **Java-Web-App-On-Azure**, quindi fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-125">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
    ![Finestra di dialogo Nuovo progetto][04]
5. <span data-ttu-id="8d0ce-127">Nella visualizzazione Project Explorer di IntelliJ espandere **Java-Web-App-On-Azure** e **web**, quindi fare doppio clic su **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-127">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
    ![Pagina di indice aperta][05c]
6. <span data-ttu-id="8d0ce-129">Quando viene aperto il file index.jsp in IntelliJ, aggiungere testo in modo da visualizzare dinamicamente **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="8d0ce-129">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="8d0ce-130">all'interno dell'elemento `<body>` esistente.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-130">within the existing `<body>` element.</span></span> <span data-ttu-id="8d0ce-131">Il contenuto `<body>` aggiornato deve avere un aspetto simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-131">Your updated `<body>` content should resemble the following example:</span></span>
   
    `<body><b><% out.println("Hello World!"); %></b></body>` 
7. <span data-ttu-id="8d0ce-132">Salvare index.jsp.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-132">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="8d0ce-133">Per distribuire l'applicazione in un contenitore di app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="8d0ce-133">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="8d0ce-134">Esistono diversi modi con cui è possibile distribuire un'applicazione Web Java in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-134">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="8d0ce-135">Questa esercitazione descrive uno dei modi più semplici: l'applicazione viene distribuita in un contenitore di app Web di Azure senza richiedere tipi di progetto specifici o strumenti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-135">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="8d0ce-136">JDK e il software del contenitore Web vengono forniti automaticamente da Azure senza la necessità di eseguire alcun caricamento. È sufficiente disporre dell'app Web Java.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-136">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="8d0ce-137">Di conseguenza, il processo di pubblicazione per l'applicazione richiederà alcuni secondi, non minuti.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-137">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="8d0ce-138">Prima di pubblicare l'applicazione è necessario configurare le impostazioni del modulo.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-138">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="8d0ce-139">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-139">To do so, use the following steps:</span></span>

1. <span data-ttu-id="8d0ce-140">In Project Explorer di IntelliJ fare clic con il pulsante destro del mouse sul progetto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="8d0ce-140">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="8d0ce-141">Quando viene visualizzato il menu di scelta rapida, fare clic su **Open Module Settings** (Apri impostazioni modulo).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-141">When the context menu appears, click **Open Module Settings**.</span></span>

    ![Open Module Settings (Apri impostazioni modulo)][05a]
2. <span data-ttu-id="8d0ce-143">Nella finestra di dialogo Project Structure (Struttura progetto):</span><span class="sxs-lookup"><span data-stu-id="8d0ce-143">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="8d0ce-144">a.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-144">a.</span></span> <span data-ttu-id="8d0ce-145">Fare clic su **Artifacts** (Elementi) nell'elenco **Project Settings** (Impostazioni progetto).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-145">Click **Artifacts** in the list of **Project Settings**.</span></span>
   <span data-ttu-id="8d0ce-146">b.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-146">b.</span></span> <span data-ttu-id="8d0ce-147">Modificare il nome dell'elemento nella casella **Nome** in modo che non contenga caratteri speciali o spazi vuoti; questa operazione è necessaria perché il nome verrà usato nell'URI (Uniform Resource Identifier).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-147">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>
   <span data-ttu-id="8d0ce-148">c.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-148">c.</span></span> <span data-ttu-id="8d0ce-149">Modificare il valore di **Type** (Tipo) in **Web Application: Archive** (Applicazione Web: archivio).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-149">Change the **Type** to **Web Application: Archive**.</span></span>
   <span data-ttu-id="8d0ce-150">d.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-150">d.</span></span> <span data-ttu-id="8d0ce-151">Fare clic su **OK** per chiudere la finestra di dialogo Project Structure (Struttura progetto).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-151">Click **OK** to close the Project Structure dialog box.</span></span>

    ![Open Module Settings (Apri impostazioni modulo)][05b]

<span data-ttu-id="8d0ce-153">Dopo aver configurato le impostazioni del modulo è possibile pubblicare l'applicazione in Azure con la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-153">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="8d0ce-154">In Project Explorer di IntelliJ fare clic con il pulsante destro del mouse sul progetto **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="8d0ce-154">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="8d0ce-155">Dal menu di scelta rapida visualizzato scegliere **Azure** e fare clic su **Publish as Azure Web App** (Pubblica come app Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-155">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
    ![Menu di scelta rapida per la pubblicazione in Azure][06]
2. <span data-ttu-id="8d0ce-157">Se non è già stato eseguito l'accesso ad Azure da IntelliJ, verrà chiesto di accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-157">If you have not already signed into Azure from IntelliJ, you will be prompted to sign into your Azure account.</span></span> <span data-ttu-id="8d0ce-158">Se si hanno più account Azure, durante il processo di accesso alcuni prompt apparentemente identici possono essere visualizzati più volte.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-158">(If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="8d0ce-159">In questo caso, continuare a seguire le istruzioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-159">When this happens, continue to follow the sign in instructions.)</span></span>
   
    ![Finestra di accesso di Azure][07]
3. <span data-ttu-id="8d0ce-161">Dopo aver eseguito l'accesso all'account Azure, nella finestra di dialogo **Manage Subscriptions** (Gestisci sottoscrizioni) viene visualizzato un elenco delle sottoscrizioni associate alle credenziali usate.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-161">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="8d0ce-162">Se sono elencate più sottoscrizioni e se ne vogliono usare solo alcune, è possibile deselezionare le sottoscrizioni che non si intende usare. Dopo aver selezionato le sottoscrizioni, fare clic su **Close**(Chiudi).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-162">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
    ![Gestisci sottoscrizioni][08]
4. <span data-ttu-id="8d0ce-164">Nella finestra di dialogo **Deploy to Azure Web App Container** (Distribuisci in un contenitore app Web di Azure) sono visualizzati tutti i contenitori di app Web creati in precedenza. Se non è stato creato alcun contenitore, l'elenco appare vuoto.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-164">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
    ![Contenitori di app][09]
5. <span data-ttu-id="8d0ce-166">Se non è stato creato alcun contenitore di app Web di Azure in precedenza o se si desidera pubblicare l'applicazione in un nuovo contenitore, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-166">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="8d0ce-167">In caso contrario, selezionare un contenitore di app Web esistente e andare al passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-167">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   1. <span data-ttu-id="8d0ce-168">Fare clic su **+**</span><span class="sxs-lookup"><span data-stu-id="8d0ce-168">Click **+**</span></span>
      
       ![Aggiungere un contenitore di app][10]
   2. <span data-ttu-id="8d0ce-170">Viene visualizzata la finestra di dialogo **New Web App Container** (Nuovo contenitore app Web), che verrà usata in diversi passaggi della procedura.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-170">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
       ![Nuovo contenitore di app][11a]
   3. <span data-ttu-id="8d0ce-172">In **DNS Label** (Etichetta DNS) specificare un'etichetta per il contenitore di app Web. Questa sarà l'etichetta DNS foglia dell'URL dell'host per l'applicazione Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-172">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="8d0ce-173">Si noti che il nome deve essere disponibile e conforme ai requisiti di denominazione delle app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-173">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>
   4. <span data-ttu-id="8d0ce-174">Nel menu a discesa **Contenitore Web** selezionare il software appropriato per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-174">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
       <span data-ttu-id="8d0ce-175">Attualmente è possibile scegliere fra Tomcat 8, Tomcat 7 o Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-175">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="8d0ce-176">Una distribuzione recente del software selezionato verrà fornita da Azure e sarà eseguita in una distribuzione recente di JDK 8 creata da Oracle e fornita da Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-176">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>
   5. <span data-ttu-id="8d0ce-177">Nel menu a discesa **Subscription** (Sottoscrizione) selezionare la sottoscrizione che si vuole usare per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>
   6. <span data-ttu-id="8d0ce-178">Nel menu a discesa **Resource Group** (Gruppo di risorse) selezionare il gruppo di risorse a cui si vuole associare l'app Web.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-178">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="8d0ce-179">I gruppi di risorse di Azure consentono di raggruppare le risorse correlate in modo che, ad esempio, possano essere eliminate insieme.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-179">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
       <span data-ttu-id="8d0ce-180">È possibile selezionare un gruppo di risorse esistente, se presente, e andare al passaggio g seguente o usare questa procedura per creare un nuovo gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-180">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="8d0ce-181">Selezionare **&lt;&lt; Create new Resource Group &gt;&gt;** (Crea nuovo gruppo di risorse) nel menu a discesa **Resource Group** (Gruppo di risorse).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-181">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="8d0ce-182">Verrà visualizzata la finestra di dialogo **Nuovo gruppo di risorse** :</span><span class="sxs-lookup"><span data-stu-id="8d0ce-182">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Nuovo gruppo di risorse][12]
      * <span data-ttu-id="8d0ce-184">Nella casella di testo **Nome** specificare un nome per il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-184">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="8d0ce-185">Nel menu a discesa **Area** selezionare il percorso del data center di Azure appropriato per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-185">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="8d0ce-186">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-186">Click **OK**.</span></span>
   7. <span data-ttu-id="8d0ce-187">Il menu a discesa **Piano di servizio app** elenca i piani di servizio app associati al gruppo di risorse selezionato.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-187">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="8d0ce-188">Un piano di servizio app specifica informazioni quali il percorso dell'app Web, il piano tariffario e le dimensioni dell'istanza di calcolo.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-188">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="8d0ce-189">È possibile usare un singolo piano di servizio app per più app Web. Per questo motivo viene gestito separatamente da una distribuzione di app Web specifica.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-189">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       <span data-ttu-id="8d0ce-190">È possibile selezionare un piano di servizio app esistente, se presente, e andare al passaggio h seguente o usare questa procedura per creare un nuovo piano di servizio app:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-190">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="8d0ce-191">Selezionare **&lt;&lt; Create new App Service Plan &gt;&gt;** (Crea nuovo piano di servizio app) nel menu a discesa **App Service Plan** (Piano di servizio app).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-191">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="8d0ce-192">Verrà visualizzata la finestra di dialogo **Nuovo piano di servizio app** :</span><span class="sxs-lookup"><span data-stu-id="8d0ce-192">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Nuovo piano di servizio app][13]
      * <span data-ttu-id="8d0ce-194">Nella casella di testo **Nome** specificare un nome per il nuovo piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-194">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="8d0ce-195">Nel menu a discesa **Località** selezionare la località del data center di Azure appropriata per il piano.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-195">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="8d0ce-196">Nel menu a discesa **Piano tariffario** selezionare la tariffa appropriata per il piano.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-196">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="8d0ce-197">Ai fini del test è possibile scegliere **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-197">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="8d0ce-198">Nel menu a discesa **Dimensioni istanza** selezionare le dimensioni dell'istanza appropriate per il piano.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-198">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="8d0ce-199">Ai fini del test è possibile scegliere **Piccolo**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-199">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="8d0ce-200">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-200">Click **OK**.</span></span>
   8. <span data-ttu-id="8d0ce-201">(Facoltativo) Per impostazione predefinita, una distribuzione recente di Java 8 verrà distribuita automaticamente da Azure nel contenitore di app Web come JVM.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-201">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="8d0ce-202">È tuttavia possibile selezionare una versione e una distribuzione di JVM diversa.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-202">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="8d0ce-203">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-203">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="8d0ce-204">Fare clic sulla scheda **JDK** nella finestra di dialogo **New Web App Container** (Nuovo contenitore app Web).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-204">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="8d0ce-205">È possibile scegliere una delle opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-205">You can choose from one of the following options:</span></span>
        
        * <span data-ttu-id="8d0ce-206">Distribuire il JDK predefinito offerto da Azure</span><span class="sxs-lookup"><span data-stu-id="8d0ce-206">Deploy the default JDK which is offered by Azure</span></span>
        * <span data-ttu-id="8d0ce-207">Distribuire un JDK di terze parti da un elenco a discesa di altri JDK disponibili in Azure</span><span class="sxs-lookup"><span data-stu-id="8d0ce-207">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
        * <span data-ttu-id="8d0ce-208">Distribuire un JDK personalizzato, che deve essere compresso come file ZIP e disponibile pubblicamente o nell'account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8d0ce-208">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
        ![Scheda JDK della finestra di dialogo New Web App Container (Nuovo contenitore app Web)][11b]
   9. <span data-ttu-id="8d0ce-210">Dopo aver completato tutti i passaggi precedenti, la finestra di dialogo New Web App Container dovrebbe essere simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-210">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
       ![Nuovo contenitore di app][14]
   10. <span data-ttu-id="8d0ce-212">Fare clic su **OK** per completare la creazione del nuovo contenitore di app Web.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-212">Click **OK** to complete the creation of your new Web App container.</span></span>
       
        <span data-ttu-id="8d0ce-213">Attendere alcuni secondi che venga aggiornato l'elenco dei contenitori di app Web. Il contenitore di app Web appena creato risulterà selezionato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-213">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>
6. <span data-ttu-id="8d0ce-214">A questo punto è possibile completare la distribuzione iniziale dell'app Web in Azure. Fare clic su **OK** per distribuire l'applicazione Java nel contenitore di app Web selezionato.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-214">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="8d0ce-215">Per impostazione predefinita, l'applicazione verrà distribuita come sottodirectory del server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-215">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="8d0ce-216">Se si vuole distribuire l'applicazione come applicazione radice, selezionare la casella di controllo **Deploy to root** (Distribuisci a radice) prima di fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-216">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
    ![Distribuire in Azure][15]
7. <span data-ttu-id="8d0ce-218">Verrà quindi aperta la visualizzazione **Azure Activity Log** (Log attività di Azure) in cui è indicato lo stato della distribuzione dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-218">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
    ![Indicatore di stato][16]
   
    <span data-ttu-id="8d0ce-220">Il processo di distribuzione dell'app Web in Azure dovrebbe richiedere solo alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-220">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="8d0ce-221">Quando l'applicazione è pronta, viene visualizzato un collegamento denominato **Published** in the **Status** .</span><span class="sxs-lookup"><span data-stu-id="8d0ce-221">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="8d0ce-222">Quando si fa clic sul collegamento, si passa alla home page dell'app Web distribuita oppure è possibile seguire la procedura indicata nella sezione seguente per passare all'app Web.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-222">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="8d0ce-223">Passaggio all'app Web in Azure</span><span class="sxs-lookup"><span data-stu-id="8d0ce-223">Browsing to your Web App on Azure</span></span>
<span data-ttu-id="8d0ce-224">Per trovare l'app Web in Azure, è possibile usare la visualizzazione **Azure Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-224">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="8d0ce-225">Se la visualizzazione **Azure Explorer** non è già aperta, aprirla facendo clic sul menu **View** (Visualizza) in IntelliJ, quindi su **Tool Windows** (Finestre degli strumenti) e su **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-225">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="8d0ce-226">Se non è già stato eseguito l'accesso in precedenza, verrà richiesto di accedere.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-226">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="8d0ce-227">Quando viene aperta la visualizzazione **Azure Explorer**, seguire questa procedura per trovare l'app Web:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-227">When the **Azure Explorer** view is displayed, use follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="8d0ce-228">Espandere il nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="8d0ce-228">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="8d0ce-229">Espandere il nodo **Web Apps** (App Web).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-229">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="8d0ce-230">Fare clic con il pulsante destro del mouse sull'app Web desiderata.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-230">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="8d0ce-231">Quando viene visualizzato il menu di scelta rapida, fare clic su **Open in Browser**(Apri nel browser).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-231">When the context menu appears, click **Open in Browser**.</span></span>
   
    ![Sfogliare l'app Web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="8d0ce-233">Aggiornamento dell'app Web</span><span class="sxs-lookup"><span data-stu-id="8d0ce-233">Updating your web app</span></span>
<span data-ttu-id="8d0ce-234">L'aggiornamento di un'app Web di Azure in esecuzione è un processo semplice e rapido. Sono disponibili due opzioni per l'aggiornamento:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-234">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="8d0ce-235">È possibile aggiornare la distribuzione di un'app Web Java esistente.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-235">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="8d0ce-236">È possibile pubblicare un'applicazione Java aggiuntiva nello stesso contenitore di app Web.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-236">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="8d0ce-237">In entrambi i casi, il processo è identico e richiede solo pochi secondi:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-237">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="8d0ce-238">In Project Explorer di IntelliJ fare clic con il pulsante destro del mouse sull'applicazione Java che si vuole aggiornare o aggiungere a un contenitore di app Web esistente.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-238">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="8d0ce-239">Dal menu di scelta rapida visualizzato selezionare **Azure**, quindi **Publish as Azure Web App** (Pubblica come App Web di Azure).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-239">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="8d0ce-240">Poiché è già stato effettuato l'accesso in precedenza, verrà visualizzato un elenco dei contenitori di app Web esistenti.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-240">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="8d0ce-241">Selezionare il contenitore in cui si vuole pubblicare o ripubblicare l'applicazione Java e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-241">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="8d0ce-242">Pochi secondi dopo nella visualizzazione **Azure Activity Log** (Log attività di Azure) la distribuzione aggiornata apparirà come **Published** (Pubblicata) e sarà possibile verificare l'applicazione aggiornata in un browser Web.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-242">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="8d0ce-243">Avvio, arresto o riavvio di un'app Web esistente</span><span class="sxs-lookup"><span data-stu-id="8d0ce-243">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="8d0ce-244">Per avviare o arrestare un contenitore di app Web di Azure esistente, incluse tutte le applicazioni Java in esso distribuite, è possibile usare la visualizzazione **Azure Explorer** .</span><span class="sxs-lookup"><span data-stu-id="8d0ce-244">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="8d0ce-245">Se la visualizzazione **Azure Explorer** non è già aperta, aprirla facendo clic sul menu **View** (Visualizza) in IntelliJ, quindi su **Tool Windows** (Finestre degli strumenti) e su **Service Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-245">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="8d0ce-246">Se non è già stato eseguito l'accesso in precedenza, verrà richiesto di accedere.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-246">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="8d0ce-247">Quando appare la visualizzazione **Azure Explorer** , per avviare o arrestare l'app Web seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-247">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="8d0ce-248">Espandere il nodo **Azure** .</span><span class="sxs-lookup"><span data-stu-id="8d0ce-248">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="8d0ce-249">Espandere il nodo **Web Apps** (App Web).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-249">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="8d0ce-250">Fare clic con il pulsante destro del mouse sull'app Web desiderata.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-250">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="8d0ce-251">Quando viene visualizzato il menu di scelta rapida, fare clic su **Start** (Avvia), **Stop** (Arresta) o **Restart** (Riavvia).</span><span class="sxs-lookup"><span data-stu-id="8d0ce-251">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="8d0ce-252">Si noti che le opzioni di menu sono sensibili al contesto, quindi è possibile arrestare solo un'app Web in esecuzione o avviare un'app Web al momento non in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="8d0ce-252">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
    ![Arrestare l'app Web][18]

## <a name="next-steps"></a><span data-ttu-id="8d0ce-254">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d0ce-254">Next Steps</span></span>
<span data-ttu-id="8d0ce-255">Per ulteriori informazioni sui Toolkit di Azure per gli IDE di Java, consultare i seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="8d0ce-255">For more information about the Azure Toolkits for Java IDEs, see the following links:</span></span>

* <span data-ttu-id="8d0ce-256">[Toolkit di Azure per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-256">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8d0ce-257">[Installare il Toolkit di Azure per Eclipse.]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-257">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="8d0ce-258">[Creare un'app Web Hello World per Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-258">[Create a Hello World Web App for Azure in Eclipse]</span></span>
  * <span data-ttu-id="8d0ce-259">[Novità di Azure Toolkit per Eclipse]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-259">[What's New in the Azure Toolkit for Eclipse]</span></span>
* <span data-ttu-id="8d0ce-260">[Azure Toolkit per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-260">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8d0ce-261">[Installazione di Azure Toolkit for IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-261">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="8d0ce-262">*Creare un’app Web Hello World per Azure in IntelliJ (questo articolo)*</span><span class="sxs-lookup"><span data-stu-id="8d0ce-262">*Create a Hello World Web App for Azure in IntelliJ (This Article)*</span></span>
  * <span data-ttu-id="8d0ce-263">[Novità del Toolkit di Azure per IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="8d0ce-263">[What's New in the Azure Toolkit for IntelliJ]</span></span>

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="8d0ce-264">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="8d0ce-264">See Also</span></span>
<span data-ttu-id="8d0ce-265">Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure].</span><span class="sxs-lookup"><span data-stu-id="8d0ce-265">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<span data-ttu-id="8d0ce-266">Per altre informazioni sulla creazione di App Web di Azure, vedere la [Panoramica delle App Web].</span><span class="sxs-lookup"><span data-stu-id="8d0ce-266">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ../azure-toolkit-for-eclipse.md
[Azure Toolkit per IntelliJ]: ../azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Installare il Toolkit di Azure per Eclipse.]: ../azure-toolkit-for-eclipse-installation.md
[Installazione di Azure Toolkit for IntelliJ]: ../azure-toolkit-for-intellij-installation.md
[Novità di Azure Toolkit per Eclipse]: ../azure-toolkit-for-eclipse-whats-new.md
[Novità del Toolkit di Azure per IntelliJ]: ../azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Panoramica delle App Web]: ./app-service-web-overview.md
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
