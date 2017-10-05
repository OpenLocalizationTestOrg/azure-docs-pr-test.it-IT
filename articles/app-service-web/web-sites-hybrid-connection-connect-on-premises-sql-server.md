---
title: Connettersi a un'istanza di SQL Server locale da un'app Web di Azure App Service mediante Connessioni ibride
description: Creare un sito Web in Microsoft Azure e connetterlo a un database di SQL Server locale
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="ba294-103">Connettersi a un'istanza di SQL Server locale da un'app Web di Azure App Service mediante Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="ba294-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="ba294-104">Le connessioni ibride possono connettere le App Web di [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) a risorse locali che usano una porta TCP statica.</span><span class="sxs-lookup"><span data-stu-id="ba294-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="ba294-105">Le risorse supportate includono Microsoft SQL Server, MySQL, HTTP API Web, servizio app e la maggior parte dei servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="ba294-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="ba294-106">Questa esercitazione spiega come creare un'app Web del servizio app nel [portale di Azure](http://go.microsoft.com/fwlink/?LinkId=529715), connettere l'app Web al database SQL Server locale mediante la nuova funzionalità Connessione ibrida, creare una semplice applicazione ASP.NET che usa la connessione ibrida e distribuire l'applicazione nell'app Web del servizio app.</span><span class="sxs-lookup"><span data-stu-id="ba294-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="ba294-107">Il sito Web completato su Azure memorizza le credenziali dell'utente in un database di appartenenza locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="ba294-108">In questa esercitazione si presuppone che l'utente non abbia mai usato Azure o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ba294-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="ba294-109">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="ba294-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ba294-110">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="ba294-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="ba294-111">La parte relativa alle app Web della funzionalità Connessioni ibride è disponibile solo nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba294-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba294-112">Per creare una connessione nei servizi BizTalk, vedere [Connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="ba294-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ba294-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ba294-113">Prerequisites</span></span>
<span data-ttu-id="ba294-114">Per completare l'esercitazione, sono necessari i prodotti seguenti.</span><span class="sxs-lookup"><span data-stu-id="ba294-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="ba294-115">Sono tutti disponibili in versioni gratuite, quindi è possibile avviare le attività di sviluppo per Azure in modo completamente gratuito.</span><span class="sxs-lookup"><span data-stu-id="ba294-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="ba294-116">**Sottoscrizione di Azure** : per una sottoscrizione gratuita, vedere [Versione di valutazione gratuita di Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ba294-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="ba294-117">**Visual Studio 2013** : per scaricare una versione di valutazione gratuita di Visual Studio 2013, vedere [Download di Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="ba294-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="ba294-118">Installare questo prodotto prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="ba294-118">Install this before continuing.</span></span>
* <span data-ttu-id="ba294-119">**Microsoft .NET Framework 3.5 Service Pack 1**: se si usa il sistema operativo Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 o Windows Server 2008 R2, è possibile abilitare questo service pack in Pannello di controllo > Programmi e funzionalità > Attivazione o disattivazione delle funzionalità Windows.</span><span class="sxs-lookup"><span data-stu-id="ba294-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="ba294-120">In alternativa, è possibile scaricarlo dall' [Area download Microsoft](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="ba294-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="ba294-121">**SQL Server 2014 Express with Tools** : scaricare Microsoft SQL Server Express gratuitamente dalla [pagina del database della piattaforma Web Microsoft](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba294-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="ba294-122">Scegliere la versione **Express** (non LocalDB).</span><span class="sxs-lookup"><span data-stu-id="ba294-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="ba294-123">La versione **Express with Tools** include SQL Server Management Studio, che verrà usato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ba294-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="ba294-124">**SQL Server Management Studio Express** : incluso con il download di SQL Server 2014 Express with Tools citato sopra; tuttavia, per installarlo separatamente è possibile scaricarlo e installarlo dalla [pagina di download di SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba294-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="ba294-125">In questa esercitazione si presuppone che l'utente disponga di una sottoscrizione di Azure, che abbia installato Visual Studio 2013 e che abbia installato o abilitato .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="ba294-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="ba294-126">L'esercitazione illustra come installare SQL Server 2014 Express in una configurazione adatta alla funzionalità Connessioni ibride di Azure (un'istanza predefinita con la porta TCP statica).</span><span class="sxs-lookup"><span data-stu-id="ba294-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="ba294-127">Prima di iniziare l'esercitazione, scaricare SQL Server 2014 Express with Tools dalla posizione indicata sopra se SQL Server non è installato.</span><span class="sxs-lookup"><span data-stu-id="ba294-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="ba294-128">Note</span><span class="sxs-lookup"><span data-stu-id="ba294-128">Notes</span></span>
<span data-ttu-id="ba294-129">Per usare un'istanza di SQL Server locale o un database SQL Server Express con una connessione ibrida, TCP/IP deve essere abilitato su una porta statica.</span><span class="sxs-lookup"><span data-stu-id="ba294-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="ba294-130">A differenza delle istanze denominate, le istanze predefinite di SQL Server usano la porta statica 1433.</span><span class="sxs-lookup"><span data-stu-id="ba294-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="ba294-131">Il computer in cui si installa l'agente Hybrid Connection Manager locale:</span><span class="sxs-lookup"><span data-stu-id="ba294-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="ba294-132">Deve avere una connettività in uscita ad Azure usando:</span><span class="sxs-lookup"><span data-stu-id="ba294-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="ba294-133">Porta</span><span class="sxs-lookup"><span data-stu-id="ba294-133">Port</span></span> | <span data-ttu-id="ba294-134">Motivo</span><span class="sxs-lookup"><span data-stu-id="ba294-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="ba294-135">80</span><span class="sxs-lookup"><span data-stu-id="ba294-135">80</span></span> |<span data-ttu-id="ba294-136">**Obbligatorio** per la porta HTTP per la convalida del certificato e, facoltativamente, per la connettività dati.</span><span class="sxs-lookup"><span data-stu-id="ba294-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="ba294-137">443</span><span class="sxs-lookup"><span data-stu-id="ba294-137">443</span></span> |<span data-ttu-id="ba294-138">**Facoltativo** per la connettività dei dati.</span><span class="sxs-lookup"><span data-stu-id="ba294-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="ba294-139">Se la connettività in uscita alla porta 443 non è disponibile, viene usata la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="ba294-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="ba294-140">5671 e 9352</span><span class="sxs-lookup"><span data-stu-id="ba294-140">5671 and 9352</span></span> |<span data-ttu-id="ba294-141">**Consigliato** ma facoltativo per la connettività dei dati.</span><span class="sxs-lookup"><span data-stu-id="ba294-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="ba294-142">Notare che questa modalità normalmente genera una maggiore velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="ba294-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="ba294-143">Se la connettività in uscita a questa porta non è disponibile, viene usata la porta TCP 443.</span><span class="sxs-lookup"><span data-stu-id="ba294-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="ba294-144">Deve essere in grado di raggiungere il *hostname*:*numero di porta* della risorsa locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="ba294-145">I passaggi indicati in questo articolo presuppongono che l'utente usi il browser dal computer che ospiterà l'agente di connessione ibrida locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="ba294-146">Se SQL Server è già installato in una configurazione e in un ambiente che soddisfano le condizioni descritte sopra, è possibile ignorare questo passaggio e iniziare dal passaggio [Creare un database SQL Server locale](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="ba294-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="ba294-147">R.</span><span class="sxs-lookup"><span data-stu-id="ba294-147">A.</span></span> <span data-ttu-id="ba294-148">Installare SQL Server Express, abilitare TCP/IP e creare un database SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="ba294-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="ba294-149">Questa sezione illustra come installare SQL Server Express, abilitare TCP/IP e creare un database in modo che l'applicazione Web funzioni con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba294-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="ba294-150">Installare SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="ba294-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="ba294-151">Per installare SQL Server Express, eseguire il file **SQLEXPRWT_x64_ENU.exe** o **SQLEXPR_x86_ENU.exe** scaricato.</span><span class="sxs-lookup"><span data-stu-id="ba294-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="ba294-152">Viene visualizzata la procedura guidata Centro installazione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ba294-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![Installare SQL Server][SQLServerInstall]
2. <span data-ttu-id="ba294-154">Scegliere **Nuova installazione autonoma di SQL Server o aggiunta di funzionalità a un'installazione esistente**.</span><span class="sxs-lookup"><span data-stu-id="ba294-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="ba294-155">Seguire le istruzioni, accettando le scelte e le impostazioni predefinite, fino a visualizzare la pagina **Configurazione istanza** .</span><span class="sxs-lookup"><span data-stu-id="ba294-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="ba294-156">Nella pagina **Configurazione istanza** scegliere **Istanza predefinita**.</span><span class="sxs-lookup"><span data-stu-id="ba294-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Scegliere Istanza predefinita][ChooseDefaultInstance]
   
    <span data-ttu-id="ba294-158">Per impostazione predefinita, l'istanza predefinita di SQL Server è in ascolto delle richieste provenienti dai client SQL Server sulla porta statica 1433, che è la porta richiesta dalla funzionalità Connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="ba294-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="ba294-159">Le istanze denominate usano le porte dinamiche e UDP, che non sono supportate da Connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="ba294-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="ba294-160">Accettare i valori predefiniti nella pagina **Configurazione server** .</span><span class="sxs-lookup"><span data-stu-id="ba294-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="ba294-161">Nella pagina **Configurazione del motore di database**, in **Modalità di autenticazione**, scegliere **Modalità mista (autenticazione di SQL Server e autenticazione di Windows)** e specificare una password.</span><span class="sxs-lookup"><span data-stu-id="ba294-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Scegliere Modalità mista][ChooseMixedMode]
   
    <span data-ttu-id="ba294-163">In questa esercitazione l'utente userà l'autenticazione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ba294-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="ba294-164">Prendere nota della password specificata, perché sarà necessaria in seguito.</span><span class="sxs-lookup"><span data-stu-id="ba294-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="ba294-165">Eseguire gli altri passaggi della procedura guidata per completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="ba294-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="ba294-166">Abilitare TCP/IP</span><span class="sxs-lookup"><span data-stu-id="ba294-166">Enable TCP/IP</span></span>
<span data-ttu-id="ba294-167">Per abilitare TCP/IP, si userà Gestione configurazione SQL Server, installato al momento dell'installazione di SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="ba294-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="ba294-168">Prima di continuare, seguire la procedura riportata in [Abilitare un protocollo di rete TCP/IP per SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ba294-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="ba294-169">Creare un database SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="ba294-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="ba294-170">L'applicazione Web Visual Studio richiede un database di appartenenza al quale Azure può effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="ba294-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="ba294-171">Ciò richiede un database SQL Server o SQL Server Express (non il database LocalDB usato dal modello MVC per impostazione predefinita), quindi il database di appartenenza verrà creato nel prossimo passaggio.</span><span class="sxs-lookup"><span data-stu-id="ba294-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="ba294-172">In SQL Server Management Studio connettersi all'istanza di SQL Server appena installata</span><span class="sxs-lookup"><span data-stu-id="ba294-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="ba294-173">(se la finestra di dialogo **Connetti al server** non viene visualizzata automaticamente, passare a **Esplora oggetti** nel riquadro sinistro, fare clic su **Connetti** e quindi fare clic su **Motore di database**). ![Connetti al server][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="ba294-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="ba294-174">In **Tipo server** scegliere **Motore di database**.</span><span class="sxs-lookup"><span data-stu-id="ba294-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="ba294-175">In **Nome server** è possibile usare **localhost** o il nome del computer.</span><span class="sxs-lookup"><span data-stu-id="ba294-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="ba294-176">Scegliere **Autenticazione di SQL Server**, quindi accedere con il nome utente e la password creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ba294-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="ba294-177">Per creare un nuovo database usando SQL Server Management Studio, fare clic con il pulsante destro del mouse su **Database** in Esplora oggetti, quindi fare clic su **Nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="ba294-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Creare il nuovo database][SSMScreateNewDB]
3. <span data-ttu-id="ba294-179">Nella finestra di dialogo **Nuovo database** immettere MembershipDB come nome del database, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba294-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="ba294-181">Si noti che in questa fase non vengono apportate modifiche al database.</span><span class="sxs-lookup"><span data-stu-id="ba294-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="ba294-182">Le informazioni di appartenenza verranno aggiunte automaticamente in seguito dall'applicazione Web quando questa verrà eseguita.</span><span class="sxs-lookup"><span data-stu-id="ba294-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="ba294-183">In Esplora oggetti, se si espande **Database**si noterà che il database di appartenenza è stato creato.</span><span class="sxs-lookup"><span data-stu-id="ba294-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="ba294-185">B.</span><span class="sxs-lookup"><span data-stu-id="ba294-185">B.</span></span> <span data-ttu-id="ba294-186">Creazione di un'app Web nel portale di Azure ##</span><span class="sxs-lookup"><span data-stu-id="ba294-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="ba294-187">Se nel portale di Azure è già stato creato un sito Web da usare per questa esercitazione, è possibile passare a [Creare una connessione ibrida e servizi BizTalk](#CreateHC) e proseguire da quel punto.</span><span class="sxs-lookup"><span data-stu-id="ba294-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="ba294-188">Nel [portale di Azure](https://portal.azure.com) fare clic su **Nuovo** > **Web e dispositivi mobili** > **App Web**.</span><span class="sxs-lookup"><span data-stu-id="ba294-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="ba294-190">Configurare l'applicazione web e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ba294-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="ba294-192">Dopo alcuni momenti, l'app Web viene creata e viene visualizzato il relativo pannello.</span><span class="sxs-lookup"><span data-stu-id="ba294-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="ba294-193">Il pannello è un dashboard scorrevole verticalmente che consente di gestire il sito.</span><span class="sxs-lookup"><span data-stu-id="ba294-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="ba294-195">Per verificare se il sito è online, è possibile fare clic sull'icona **Sfoglia** per visualizzare la pagina predefinita.</span><span class="sxs-lookup"><span data-stu-id="ba294-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="ba294-196">Verranno quindi creati una connessione ibrida e un servizio BizTalk per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="ba294-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="ba294-197">C.</span><span class="sxs-lookup"><span data-stu-id="ba294-197">C.</span></span> <span data-ttu-id="ba294-198">Creare una connessione ibrida e servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="ba294-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="ba294-199">Nel portale passare alle impostazioni e fare clic su **Rete** > **Configurare gli endpoint di connessione ibrida**.</span><span class="sxs-lookup"><span data-stu-id="ba294-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connessioni ibride][CreateHCHCIcon]
2. <span data-ttu-id="ba294-201">Nel pannello Connessioni ibride fare clic su **Aggiungi** > **Nuova connessione ibrida**.</span><span class="sxs-lookup"><span data-stu-id="ba294-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="ba294-202">Nel pannello **Crea connessione ibrida** :</span><span class="sxs-lookup"><span data-stu-id="ba294-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="ba294-203">In **Nome**specificare un nome per la connessione.</span><span class="sxs-lookup"><span data-stu-id="ba294-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="ba294-204">In **Nome host**immettere il nome computer del computer host SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ba294-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="ba294-205">In **Porta**immettere 1433 (la porta predefinita per SQL Server).</span><span class="sxs-lookup"><span data-stu-id="ba294-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="ba294-206">Fare clic su **Servizio BizTalk** > **Nuovo servizio BizTalk** e immettere un nome per il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="ba294-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Creare una connessione ibrida][TwinCreateHCBlades]
4. <span data-ttu-id="ba294-208">Fare clic su **OK** due volte.</span><span class="sxs-lookup"><span data-stu-id="ba294-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="ba294-209">Al termine del processo, nell'area **Notifiche** verrà visualizzato il messaggio **OPERAZIONE RIUSCITA** verde lampeggiante e il pannello **Connessione ibrida** mostrerà la nuova connessione ibrida con lo stato **Non connesso**.</span><span class="sxs-lookup"><span data-stu-id="ba294-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="ba294-211">A questo punto è stata completata una parte importante dell'infrastruttura della connessione ibrida cloud.</span><span class="sxs-lookup"><span data-stu-id="ba294-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="ba294-212">Nel passaggio successivo verrà creato un elemento locale corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ba294-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="ba294-213">D.</span><span class="sxs-lookup"><span data-stu-id="ba294-213">D.</span></span> <span data-ttu-id="ba294-214">Installare l'istanza locale di Hybrid Connection Manager per completare la connessione</span><span class="sxs-lookup"><span data-stu-id="ba294-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="ba294-215">Dopo aver completato l'infrastruttura della connessione ibrida, verrà creata un'applicazione Web che la userà.</span><span class="sxs-lookup"><span data-stu-id="ba294-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="ba294-216">E.</span><span class="sxs-lookup"><span data-stu-id="ba294-216">E.</span></span> <span data-ttu-id="ba294-217">E. Creare un progetto Web ASP.NET di base, modificare la stringa di connessione del database ed eseguire il progetto a livello locale</span><span class="sxs-lookup"><span data-stu-id="ba294-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="ba294-218">Create a basic ASP.NET project</span><span class="sxs-lookup"><span data-stu-id="ba294-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="ba294-219">Nel menu **File** di Visual Studio creare un nuovo progetto:</span><span class="sxs-lookup"><span data-stu-id="ba294-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="ba294-221">Nella sezione **Modelli** della finestra di dialogo **Nuovo progetto** selezionare **Web** e scegliere **Applicazione Web ASP.NET**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba294-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="ba294-223">Nella finestra di dialogo **Nuovo progetto ASP.NET** scegliere **MVC**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba294-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="ba294-225">Dopo la creazione del progetto, viene visualizzata la pagina Leggimi dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba294-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="ba294-226">Non eseguire ancora il progetto.</span><span class="sxs-lookup"><span data-stu-id="ba294-226">Do not run the web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="ba294-228">Modificare la stringa di connessione del database per l'applicazione</span><span class="sxs-lookup"><span data-stu-id="ba294-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="ba294-229">In questo passaggio verrà modificata la stringa di connessione che comunica all'applicazione dove trovare il database SQL Server Express locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="ba294-230">La stringa di connessione si trova nel file Web.config dell'applicazione, che contiene le informazioni di configurazione relative all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba294-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ba294-231">Per assicurarsi che l'applicazione usi il database creato in SQL Server Express, e non quello presente nel database LocalDB predefinito di Visual Studio, è importante completare questo passaggio prima di eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="ba294-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="ba294-232">In Esplora soluzioni fare doppio clic sul file Web.config.</span><span class="sxs-lookup"><span data-stu-id="ba294-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="ba294-234">Modificare la sezione **connectionStrings** per puntare al database SQL Server sul computer locale, usando la sintassi dell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="ba294-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Stringa di connessione][HCVSConnectionString]
   
    <span data-ttu-id="ba294-236">Quando si compone la stringa di connessione, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ba294-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="ba294-237">Se si effettua la connessione a un'istanza denominata invece che a un'istanza predefinita (ad esempio, Server\SQLEXPRESS), è necessario configurare l'istanza di SQL Server in modo che usi le porte statiche.</span><span class="sxs-lookup"><span data-stu-id="ba294-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="ba294-238">Per informazioni sulla configurazione di porte statiche, vedere [Come configurare SQL Server per l'ascolto su una porta specifica](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="ba294-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="ba294-239">Per impostazione predefinita le istanze denominate usano UDP e le porte dinamiche, che non sono supportate dalle connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="ba294-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="ba294-240">Si consiglia di specificare la porta (1433 per impostazione predefinita, come mostrato nell'esempio) nella stringa di connessione in modo da assicurarsi che TCP sia abilitato sull'istanza di SQL Server locale e usi la porta corretta.</span><span class="sxs-lookup"><span data-stu-id="ba294-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="ba294-241">Ricordare di usare Autenticazione SQL Server per connettersi, specificando l'ID utente e la password nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="ba294-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="ba294-242">Fare clic su **Salva** in Visual Studio per salvare il file Web.config.</span><span class="sxs-lookup"><span data-stu-id="ba294-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="ba294-243">Eseguire il progetto a livello locale e registrare un nuovo utente</span><span class="sxs-lookup"><span data-stu-id="ba294-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="ba294-244">Ora eseguire il nuovo progetto Web a livello locale facendo clic sul pulsante Sfoglia in Debug.</span><span class="sxs-lookup"><span data-stu-id="ba294-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="ba294-245">In questo esempio viene usato Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ba294-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="ba294-247">Nell'angolo superiore destro della pagina Web predefinita scegliere **Registra** per registrare un nuovo account:</span><span class="sxs-lookup"><span data-stu-id="ba294-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="ba294-249">Immettere un nome utente e una password:</span><span class="sxs-lookup"><span data-stu-id="ba294-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="ba294-251">Nell'istanza di SQL Server locale si crea automaticamente un database che contiene le informazioni di appartenenza per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba294-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="ba294-252">Una delle tabelle (**dbo.AspNetUsers**) contiene credenziali utente del sito Web simili a quelle appena immesse.</span><span class="sxs-lookup"><span data-stu-id="ba294-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="ba294-253">Questa tabella verrà visualizzata successivamente in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ba294-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="ba294-254">Chiudere la finestra del browser relativa alla pagina Web predefinita.</span><span class="sxs-lookup"><span data-stu-id="ba294-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="ba294-255">In questo modo l'applicazione viene arrestata in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba294-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="ba294-256">Ora è possibile eseguire il passaggio successivo, che prevede la pubblicazione dell'applicazione in Azure e il relativo test.</span><span class="sxs-lookup"><span data-stu-id="ba294-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="ba294-257">F.</span><span class="sxs-lookup"><span data-stu-id="ba294-257">F.</span></span> <span data-ttu-id="ba294-258">F. Pubblicare l'applicazione Web in Azure e testarla</span><span class="sxs-lookup"><span data-stu-id="ba294-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="ba294-259">Ora l'applicazione verrà pubblicata nel sito Web di Azure e testata per verificare in che modo la connessione ibrida creata in precedenza viene usata per connettere l'applicazione del sito Web al database presente nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="ba294-260">Publish the web application</span><span class="sxs-lookup"><span data-stu-id="ba294-260">Publish the web application</span></span>
1. <span data-ttu-id="ba294-261">È possibile scaricare il profilo di pubblicazione per l'app Web del servizio app nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba294-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="ba294-262">Nel pannello dell'app Web scegliere **Scarica profilo di pubblicazione**, quindi salvare il file nel computer.</span><span class="sxs-lookup"><span data-stu-id="ba294-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Scaricare un profilo di pubblicazione][PortalDownloadPublishProfile]
   
    <span data-ttu-id="ba294-264">Quindi il file verrà importato nell'applicazione Web di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba294-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="ba294-265">In Visual Studio fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni e selezionare **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ba294-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="ba294-267">Nella scheda **Profilo** della finestra di dialogo **Pubblica sito Web** scegliere **Importa**.</span><span class="sxs-lookup"><span data-stu-id="ba294-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Importa][HCVSPublishWebDialogImport]
4. <span data-ttu-id="ba294-269">Passare al profilo di pubblicazione scaricato, selezionarlo e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba294-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Browse to profile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="ba294-271">Le informazioni di pubblicazione vengono importate e visualizzate nella scheda **Connessione** della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="ba294-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Click Publish][HCVSClickPublish]
   
    <span data-ttu-id="ba294-273">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="ba294-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="ba294-274">Al termine della pubblicazione verrà avviato il browser che visualizzerà l'applicazione ASP.NET ormai nota, con la differenza che ora è disponibile nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba294-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="ba294-275">Quindi, l'applicazione Web verrà usata per vedere la relativa connessione ibrida in azione.</span><span class="sxs-lookup"><span data-stu-id="ba294-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="ba294-276">Testare in Azure l'applicazione Web completata</span><span class="sxs-lookup"><span data-stu-id="ba294-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="ba294-277">Nella parte superiore destra della pagina Web in Azure, scegliere **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="ba294-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="ba294-279">L'app Web del servizio app e è ora connessa al database di appartenenza dell'applicazione Web sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="ba294-280">Per effettuare una verifica, accedere con le stesse credenziali immesse precedentemente nel database locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="ba294-282">Per testare ulteriormente la nuova connessione ibrida, effettuare la disconnessione dall'applicazione Web Azure e registrarsi come un altro utente.</span><span class="sxs-lookup"><span data-stu-id="ba294-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="ba294-283">Specificare un nuovo nome utente e password, quindi fare clic su **Registra**.</span><span class="sxs-lookup"><span data-stu-id="ba294-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="ba294-285">Per verificare che le credenziali del nuovo utente siano state archiviate nel database locale tramite la connessione ibrida, aprire SQL Management Studio sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="ba294-286">In Esplora oggetti espandere il database **MembershipDB**, quindi espandere **Tabelle**.</span><span class="sxs-lookup"><span data-stu-id="ba294-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="ba294-287">Fare clic con il pulsante destro del mouse sulla tabella di appartenenza **dbo.AspNetUsers** e scegliere **Select Top 1000 Rows** (Seleziona prime 1000 righe) per visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="ba294-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![View the results][HCTestSSMSTree]
5. <span data-ttu-id="ba294-289">La tabella di appartenenza locale ora mostra entrambi gli account, quello creato localmente e quello creato nel cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba294-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="ba294-290">L'account creato nel cloud è stato salvato nel database locale mediante la funzionalità Connessioni ibride di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba294-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="ba294-292">È stata creata e implementata un'applicazione Web ASP.NET che usa una connessione ibrida tra un sito Web nel cloud di Azure e un database SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="ba294-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="ba294-293">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="ba294-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="ba294-294">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="ba294-294">See Also</span></span>
[<span data-ttu-id="ba294-295">Panoramica delle connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="ba294-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="ba294-296">Josh Twist presenta le connessioni ibride (video Channel 9)</span><span class="sxs-lookup"><span data-stu-id="ba294-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="ba294-297">Panoramica delle connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="ba294-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="ba294-298">Servizi BizTalk: schede Dashboard, Monitor, Scala, Configura e Connessione ibrida</span><span class="sxs-lookup"><span data-stu-id="ba294-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="ba294-299">Creazione di un cloud ibrido reale con portabilità continua delle applicazioni (video Channel 9)</span><span class="sxs-lookup"><span data-stu-id="ba294-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="ba294-300">Accesso alle risorse locali usando connessioni ibride nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ba294-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="ba294-301">Panoramica dell'identità ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ba294-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
