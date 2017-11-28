---
title: aaaAccess risorse locali mediante connessioni ibride in Azure App Service
description: Creare una connessione tra un'app Web nel servizio app di Azure e una risorsa locale che usa una porta TCP statica
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="2bc00-103">Accesso alle risorse locali usando connessioni ibride nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="2bc00-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="2bc00-104">È possibile connettersi a una risorsa servizio App di Azure app tooany locale che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e la maggior parte dei servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2bc00-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="2bc00-105">In questo articolo illustra come toocreate una connessione ibrida tra servizio App e un database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="2bc00-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="2bc00-106">parte di App Web Hello della funzionalità di connessioni ibride hello è disponibile solo in hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2bc00-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="2bc00-107">toocreate una connessione in servizi di BizTalk, vedere [connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="2bc00-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="2bc00-108">Questo contenuto si applica anche tooMobile App in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2bc00-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2bc00-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2bc00-109">Prerequisites</span></span>
* <span data-ttu-id="2bc00-110">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bc00-110">An Azure subscription.</span></span> <span data-ttu-id="2bc00-111">Per una sottoscrizione gratuita, vedere [Versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bc00-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="2bc00-112">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="2bc00-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2bc00-113">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="2bc00-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="2bc00-114">toouse un SQL Server locale o un database di SQL Server Express con una connessione ibrida, TCP/IP deve toobe abilitata su una porta statica.</span><span class="sxs-lookup"><span data-stu-id="2bc00-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="2bc00-115">È consigliabile usare un'istanza predefinita di on SQL Server, perché usa la porta statica 1433.</span><span class="sxs-lookup"><span data-stu-id="2bc00-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="2bc00-116">Per informazioni sull'installazione e configurazione di SQL Server Express per l'utilizzo con le connessioni ibride, vedere [tooan connessione SQL Server locale da un sito web di Azure mediante connessioni ibride](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="2bc00-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="2bc00-117">computer Hello in cui si installa agente di gestione connessione ibrida locale hello descritto più avanti in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="2bc00-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="2bc00-118">Deve essere in grado di tooconnect tooAzure attraverso la porta 5671</span><span class="sxs-lookup"><span data-stu-id="2bc00-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="2bc00-119">Deve essere in grado di tooreach hello *hostname*:*NumeroPorta* della risorsa locale.</span><span class="sxs-lookup"><span data-stu-id="2bc00-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="2bc00-120">passaggi di Hello in questo articolo si presuppongono che si sta utilizzando un browser hello dal computer hello che ospiterà l'agente di connessione ibrida locale hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="2bc00-121">Creare un'app web nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="2bc00-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="2bc00-122">Se è già stato creato un'app web o App per dispositivi mobili di back-end in hello portale di Azure che si desidera toouse per questa esercitazione, è possibile andare troppo[creare una connessione ibrida e un BizTalk Service](#CreateHC) e iniziare da qui.</span><span class="sxs-lookup"><span data-stu-id="2bc00-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="2bc00-123">In hello nell'angolo superiore sinistro di hello [portale Azure](https://portal.azure.com), fare clic su **New** > **Web e dispositivi mobili** > **App Web**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Nuova applicazione web][NewWebsite]
2. <span data-ttu-id="2bc00-125">In hello **app Web** pannello, specificare un URL e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="2bc00-127">Dopo alcuni istanti, viene creato l'app web hello e viene visualizzato il pannello app web.</span><span class="sxs-lookup"><span data-stu-id="2bc00-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="2bc00-128">Pannello Hello è un dashboard scorrevole verticalmente che consente di gestire il sito.</span><span class="sxs-lookup"><span data-stu-id="2bc00-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Website running][WebSiteRunningBlade]
4. <span data-ttu-id="2bc00-130">sito hello tooverify è attivo, è possibile scegliere hello **Sfoglia** pagina predefinita di icona toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Fare clic su Sfoglia toosee app web][Browse]
   
    ![Pagina di applicazione web predefinita][DefaultWebSitePage]

<span data-ttu-id="2bc00-133">Successivamente, si creerà una connessione ibrida e un servizio BizTalk per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="2bc00-134">Creare una connessione ibrida e servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="2bc00-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="2bc00-135">Nel pannello dell'app Web fare clic su **Tutte le impostazioni** > **Rete** > **Configurare gli endpoint della connessione ibrida**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connessioni ibride][CreateHCHCIcon]
2. <span data-ttu-id="2bc00-137">Nel Pannello di connessioni ibride hello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="2bc00-138">Hello **aggiungere una connessione ibrida** apre blade.</span><span class="sxs-lookup"><span data-stu-id="2bc00-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="2bc00-139">Poiché questa è la prima connessione ibrida, hello **nuova connessione ibrida** opzione è preselezionato e hello **creare la connessione ibrida** pannello verrà visualizzata.</span><span class="sxs-lookup"><span data-stu-id="2bc00-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Creare una connessione ibrida][TwinCreateHCBlades]
   
    <span data-ttu-id="2bc00-141">In hello **blade di connessione ibrida crea**:</span><span class="sxs-lookup"><span data-stu-id="2bc00-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="2bc00-142">Per **nome**, specificare un nome per la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="2bc00-143">Per **Hostname**, immettere il nome di hello del computer locale hello che ospita la risorsa.</span><span class="sxs-lookup"><span data-stu-id="2bc00-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="2bc00-144">Per **porta**, immettere il numero di porta hello che la risorsa locale utilizza (1433 per un'istanza predefinita di SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2bc00-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="2bc00-145">Fare clic su **Servizio BizTalk**</span><span class="sxs-lookup"><span data-stu-id="2bc00-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="2bc00-146">Hello **Crea servizio BizTalk** apre blade.</span><span class="sxs-lookup"><span data-stu-id="2bc00-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="2bc00-147">Immettere un nome per il servizio BizTalk hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Crea servizio BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="2bc00-149">Hello **Crea servizio BizTalk** pannello chiude e si ritorna toohello **creare la connessione ibrida** blade.</span><span class="sxs-lookup"><span data-stu-id="2bc00-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="2bc00-150">Nel Pannello di connessione ibrida crea hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Fare clic su OK.][CreateBTScomplete]
6. <span data-ttu-id="2bc00-152">Al termine del processo di hello, area di notifica hello in hello portale indica che la connessione hello è stata creata correttamente.</span><span class="sxs-lookup"><span data-stu-id="2bc00-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="2bc00-153">Nel pannello dell'app web hello, hello **connessioni ibride** icona Mostra che è stata creata la connessione ibrida 1 ora.</span><span class="sxs-lookup"><span data-stu-id="2bc00-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="2bc00-155">A questo punto, è stata completata una parte importante dell'infrastruttura di connessione di hello cloud ibrido.</span><span class="sxs-lookup"><span data-stu-id="2bc00-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="2bc00-156">Nel passaggio successivo verrà creato un elemento locale corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2bc00-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="2bc00-157">Installare connessione hello toocomplete di hello locale di Hybrid Connection Manager</span><span class="sxs-lookup"><span data-stu-id="2bc00-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="2bc00-158">Nel pannello dell'app web hello, fare clic su **tutte le impostazioni** > **rete** > **configurare gli endpoint della connessione ibrida**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Hybrid connections icon][HCIcon]
2. <span data-ttu-id="2bc00-160">In hello **connessioni ibride** blade, hello **stato** colonna per hello aggiunti di recente endpoint Mostra **non connesso**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="2bc00-161">Fare clic su tooconfigure connessione hello è.</span><span class="sxs-lookup"><span data-stu-id="2bc00-161">Click hello connection tooconfigure it.</span></span>
   
    ![Non connesso][NotConnected]
   
    <span data-ttu-id="2bc00-163">verrà visualizzata la finestra di blade di connessione ibrida Hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="2bc00-165">Nel Pannello di hello, fare clic su **Listener installazione**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Click Listener Setup][ClickListenerSetup]
4. <span data-ttu-id="2bc00-167">Hello **le proprietà di connessione ibrida** apre blade.</span><span class="sxs-lookup"><span data-stu-id="2bc00-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="2bc00-168">In **locale di Hybrid Connection Manager**, scegliere **fare clic qui tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Fare clic qui tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="2bc00-170">In hello applicazione eseguita avviso di sicurezza, scegliere **eseguire** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="2bc00-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Scegliere Esegui toocontinue][ApplicationRunWarning]
6. <span data-ttu-id="2bc00-172">In hello **controllo dell'Account utente** finestra di dialogo, scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Choose Yes][UAC]
7. <span data-ttu-id="2bc00-174">Hello Hybrid Connection Manager viene scaricato e installato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2bc00-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Installazione][HCMInstalling]
8. <span data-ttu-id="2bc00-176">Al termine dell'installazione di hello, fare clic su **Chiudi**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-176">When hello install completes, click **Close**.</span></span>
   
    ![Fare clic su Chiudi][HCMInstallComplete]
   
    <span data-ttu-id="2bc00-178">In hello **connessioni ibride** blade, hello **stato** colonna Mostra ora **connesso**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Stato connesso][HCStatusConnected]

<span data-ttu-id="2bc00-180">Ora che infrastruttura di connessione ibrida hello è stata completata, è possibile creare un'applicazione ibrida che lo utilizza.</span><span class="sxs-lookup"><span data-stu-id="2bc00-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="2bc00-181">Hello nelle sezioni seguenti illustrano come toouse una connessione ibrida con un progetto di back-end App Mobile.</span><span class="sxs-lookup"><span data-stu-id="2bc00-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="2bc00-182">Configurare il database di SQL Server di hello .NET App Mobile back-end progetto tooconnect toohello</span><span class="sxs-lookup"><span data-stu-id="2bc00-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="2bc00-183">In Servizio app, un progetto di back-end .NET per App per dispositivi mobili è semplicemente un'app Web ASP.NET dotata di un SDK per App per dispositivi mobili installato e inizializzato.</span><span class="sxs-lookup"><span data-stu-id="2bc00-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="2bc00-184">toouse l'app web come un back-end dell'App per dispositivi mobili, è necessario [download e l'inizializzazione di back-end .NET le app mobili hello SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="2bc00-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="2bc00-185">Per App per dispositivi mobili, è anche necessario toodefine una stringa di connessione per il database locale hello e modificare hello back-end toouse questa connessione.</span><span class="sxs-lookup"><span data-stu-id="2bc00-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="2bc00-186">In Esplora soluzioni in Visual Studio, il file Web. config hello open per il back-end Mobile App .NET, individuare hello **connectionStrings** sezione, aggiungere una nuova voce di SqlClient seguente hello, quali toohello punti SQL locale Database del server:</span><span class="sxs-lookup"><span data-stu-id="2bc00-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="2bc00-187">Ricordare tooreplace `<**secure_password**>` in questa stringa con password hello creata per *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="2bc00-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="2bc00-188">Fare clic su **salvare** nel file Web. config hello toosave di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2bc00-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2bc00-189">Questa impostazione di connessione viene utilizzata durante l'esecuzione nel computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="2bc00-190">Durante l'esecuzione in Azure, questa impostazione è sottoposta a override dall'impostazione di connessione hello definito nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="2bc00-191">Espandere hello **modelli** cartelle e file del modello dati aprire hello, che termina *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="2bc00-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="2bc00-192">Modificare hello **DbContext** toopass costruttore di istanza hello valore `OnPremisesDBConnection` toohello base **DbContext** costruttore, simile toohello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2bc00-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="2bc00-193">servizio Hello utilizzeranno hello nuovo connessione toohello database SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2bc00-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="2bc00-194">Aggiornare la stringa di connessione di hello App Mobile back-end toouse hello locale</span><span class="sxs-lookup"><span data-stu-id="2bc00-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="2bc00-195">Successivamente, è necessario tooadd un'impostazione app per la nuova stringa di connessione in modo che può essere utilizzato da Azure.</span><span class="sxs-lookup"><span data-stu-id="2bc00-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="2bc00-196">In hello [portale di Azure](https://portal.azure.com) hello codice app web back-end per l'App Mobile, fare clic su **tutte le impostazioni**, quindi **le impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="2bc00-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="2bc00-197">In hello **impostazioni app Web** pannello, scorrere verso il basso troppo**le stringhe di connessione** e aggiungere un nuovo **SQL Server** stringa di connessione denominata `OnPremisesDBConnection` con un valore come `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="2bc00-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="2bc00-198">Sostituire `<**secure_password**>` con password sicura di hello per il database locale.</span><span class="sxs-lookup"><span data-stu-id="2bc00-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Stringa di connessione del database locale](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="2bc00-200">Premere **salvare** stringa di connessione e la connessione ibrida hello toosave appena creato.</span><span class="sxs-lookup"><span data-stu-id="2bc00-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="2bc00-201">A questo punto è possibile ripubblicare il progetto server di hello e provare di hello nuova connessione con il client App per dispositivi mobili esistenti.</span><span class="sxs-lookup"><span data-stu-id="2bc00-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="2bc00-202">Dati verranno leggere e scritti database locale toohello utilizzando la connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="2bc00-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="2bc00-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bc00-203">Next Steps</span></span>
* <span data-ttu-id="2bc00-204">Per informazioni sulla creazione di un'applicazione web ASP.NET che usa una connessione ibrida, vedere [tooan connessione SQL Server locale da un sito web di Azure mediante connessioni ibride](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="2bc00-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="2bc00-205">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2bc00-205">Additional Resources</span></span>
[<span data-ttu-id="2bc00-206">Panoramica delle connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="2bc00-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="2bc00-207">Josh Twist presenta le connessioni ibride (video Channel 9)</span><span class="sxs-lookup"><span data-stu-id="2bc00-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="2bc00-208">Sito Web delle connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="2bc00-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="2bc00-209">Servizi BizTalk: schede Dashboard, Monitor, Scala, Configura e Connessione ibrida</span><span class="sxs-lookup"><span data-stu-id="2bc00-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="2bc00-210">Creazione di un cloud ibrido reale con portabilità continua delle applicazioni (video Channel 9)</span><span class="sxs-lookup"><span data-stu-id="2bc00-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="2bc00-211">Connettersi tooan on-premise a SQL Server da servizi mobili di Azure mediante connessioni ibride (video di Channel 9)</span><span class="sxs-lookup"><span data-stu-id="2bc00-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="2bc00-212">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="2bc00-212">What's changed</span></span>
* <span data-ttu-id="2bc00-213">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="2bc00-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
