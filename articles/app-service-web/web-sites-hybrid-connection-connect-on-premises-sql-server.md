---
title: aaaConnect tooon locale di SQL Server da un'app web nel servizio App di Azure mediante connessioni ibride
description: Crea un'app web in Microsoft Azure e connetterla tooan database di SQL Server locale
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="e6e22-103">Connettersi a SQL Server locale tooon da un'app web nel servizio App di Azure mediante connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="e6e22-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="e6e22-104">Le connessioni ibride [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) risorse tooon locale di App Web che utilizzano una porta TCP statica.</span><span class="sxs-lookup"><span data-stu-id="e6e22-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="e6e22-105">Le risorse supportate includono Microsoft SQL Server, MySQL, HTTP API Web, servizio app e la maggior parte dei servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e6e22-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="e6e22-106">In questa esercitazione si apprenderà come toocreate un servizio App web app in hello [portale Azure](http://go.microsoft.com/fwlink/?LinkId=529715), connettersi utilizzando la nuova connessione ibrida funzionalità di hello hello web app tooyour locale SQL Server database, creare un semplice ASP.NET applicazione che utilizzerà la connessione ibrida hello e distribuire toohello applicazione hello App del servizio web app.</span><span class="sxs-lookup"><span data-stu-id="e6e22-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="e6e22-107">Hello completato web app in Azure archivia le credenziali dell'utente in un database di appartenenza che si trova in locale.</span><span class="sxs-lookup"><span data-stu-id="e6e22-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="e6e22-108">esercitazione Hello non presuppone alcun esperienze precedenti usando Azure o ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e6e22-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e22-109">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="e6e22-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e6e22-110">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="e6e22-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="e6e22-111">parte di App Web Hello della funzionalità di connessioni ibride hello è disponibile solo in hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6e22-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="e6e22-112">toocreate una connessione in servizi di BizTalk, vedere [connessioni ibride](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="e6e22-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e6e22-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e6e22-113">Prerequisites</span></span>
<span data-ttu-id="e6e22-114">toocomplete questa esercitazione, è necessario hello i seguenti prodotti.</span><span class="sxs-lookup"><span data-stu-id="e6e22-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="e6e22-115">Sono tutti disponibili in versioni gratuite, quindi è possibile avviare le attività di sviluppo per Azure in modo completamente gratuito.</span><span class="sxs-lookup"><span data-stu-id="e6e22-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="e6e22-116">**Sottoscrizione di Azure** : per una sottoscrizione gratuita, vedere [Versione di valutazione gratuita di Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6e22-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="e6e22-117">**Visual Studio 2013** -toodownload una versione di valutazione gratuita di Visual Studio 2013, vedere [download di Visual Studio](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="e6e22-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="e6e22-118">Installare questo prodotto prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="e6e22-118">Install this before continuing.</span></span>
* <span data-ttu-id="e6e22-119">**Microsoft .NET Framework 3.5 Service Pack 1**: se si usa il sistema operativo Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 o Windows Server 2008 R2, è possibile abilitare questo service pack in Pannello di controllo > Programmi e funzionalità > Attivazione o disattivazione delle funzionalità Windows.</span><span class="sxs-lookup"><span data-stu-id="e6e22-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="e6e22-120">In caso contrario, è possibile scaricarlo da hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="e6e22-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="e6e22-121">**SQL Server 2014 Express with Tools** -scaricare Microsoft SQL Server Express gratuita all'hello [pagina Database di piattaforma Web Microsoft](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6e22-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="e6e22-122">Scegliere hello **Express** (non LocalDB) versione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="e6e22-123">Hello **Express with Tools** versione include SQL Server Management Studio, che verrà utilizzato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="e6e22-124">**SQL Server Management Studio Express** : questo è incluso in SQL Server 2014 Express hello con download di strumenti indicato in precedenza, ma se è necessario tooinstall è separatamente, è possibile scaricare e installarlo da hello [SQL Server Express pagina di download](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="e6e22-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="e6e22-125">esercitazione Hello presuppone che si disponga di una sottoscrizione di Azure, di avere installato Visual Studio 2013 e di aver installato o abilitato .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="e6e22-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="e6e22-126">Hello esercitazione viene illustrato come tooinstall SQL Server 2014 Express in una configurazione che funziona bene con le connessioni ibride di hello Azure funzionalità (un'istanza predefinita con una porta TCP statica).</span><span class="sxs-lookup"><span data-stu-id="e6e22-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="e6e22-127">Prima di iniziare l'esercitazione hello, scaricare SQL Server 2014 Express with Tools dal percorso di hello indicato sopra, se non è installato SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e6e22-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="e6e22-128">Note</span><span class="sxs-lookup"><span data-stu-id="e6e22-128">Notes</span></span>
<span data-ttu-id="e6e22-129">toouse un SQL Server locale o un database di SQL Server Express con una connessione ibrida, TCP/IP deve toobe abilitata su una porta statica.</span><span class="sxs-lookup"><span data-stu-id="e6e22-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="e6e22-130">A differenza delle istanze denominate, le istanze predefinite di SQL Server usano la porta statica 1433.</span><span class="sxs-lookup"><span data-stu-id="e6e22-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="e6e22-131">computer Hello in cui si installa l'agente di gestione connessione ibrida locale hello:</span><span class="sxs-lookup"><span data-stu-id="e6e22-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="e6e22-132">Deve disporre di connettività in uscita tooAzure su:</span><span class="sxs-lookup"><span data-stu-id="e6e22-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="e6e22-133">Porta</span><span class="sxs-lookup"><span data-stu-id="e6e22-133">Port</span></span> | <span data-ttu-id="e6e22-134">Motivo</span><span class="sxs-lookup"><span data-stu-id="e6e22-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="e6e22-135">80</span><span class="sxs-lookup"><span data-stu-id="e6e22-135">80</span></span> |<span data-ttu-id="e6e22-136">**Obbligatorio** per la porta HTTP per la convalida del certificato e, facoltativamente, per la connettività dati.</span><span class="sxs-lookup"><span data-stu-id="e6e22-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="e6e22-137">443</span><span class="sxs-lookup"><span data-stu-id="e6e22-137">443</span></span> |<span data-ttu-id="e6e22-138">**Facoltativo** per la connettività dei dati.</span><span class="sxs-lookup"><span data-stu-id="e6e22-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="e6e22-139">Se non è disponibile la connettività in uscita too443, viene utilizzata la porta TCP 80.</span><span class="sxs-lookup"><span data-stu-id="e6e22-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="e6e22-140">5671 e 9352</span><span class="sxs-lookup"><span data-stu-id="e6e22-140">5671 and 9352</span></span> |<span data-ttu-id="e6e22-141">**Consigliato** ma facoltativo per la connettività dei dati.</span><span class="sxs-lookup"><span data-stu-id="e6e22-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="e6e22-142">Notare che questa modalità normalmente genera una maggiore velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="e6e22-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="e6e22-143">Se le porte toothese di connettività in uscita non è disponibile, viene utilizzata la porta TCP 443.</span><span class="sxs-lookup"><span data-stu-id="e6e22-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="e6e22-144">Deve essere in grado di tooreach hello *hostname*:*NumeroPorta* della risorsa locale.</span><span class="sxs-lookup"><span data-stu-id="e6e22-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="e6e22-145">passaggi di Hello in questo articolo si presuppongono che si sta utilizzando un browser hello dal computer hello che ospiterà l'agente di connessione ibrida locale hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="e6e22-146">Se si dispone già di SQL Server installata in una configurazione e in un ambiente che soddisfa le condizioni di hello descritte in precedenza, è possibile ignorare e avviare con [creare un database di SQL Server on-premise](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="e6e22-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="e6e22-147">R.</span><span class="sxs-lookup"><span data-stu-id="e6e22-147">A.</span></span> <span data-ttu-id="e6e22-148">Installare SQL Server Express, abilitare TCP/IP e creare un database SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="e6e22-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="e6e22-149">In questa sezione mostra come abilitare TCP/IP, SQL Server Express, tooinstall e creare un database in modo che l'applicazione web funzionerà con hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e22-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="e6e22-150">Installare SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="e6e22-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="e6e22-151">SQL Server Express, eseguire hello tooinstall **SQLEXPRWT_x64_ENU.exe** o **SQLEXPR_x86_ENU.exe** file scaricato.</span><span class="sxs-lookup"><span data-stu-id="e6e22-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="e6e22-152">verrà visualizzata Hello guidata di Centro installazione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e6e22-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![Installare SQL Server][SQLServerInstall]
2. <span data-ttu-id="e6e22-154">Scegliere **nuova installazione SQL Server autonomo o aggiungere funzionalità tooan esistente installazione**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="e6e22-155">Seguire le istruzioni di hello, accettando i valori predefiniti hello e le impostazioni, fino a ottenere toohello **configurazione istanza** pagina.</span><span class="sxs-lookup"><span data-stu-id="e6e22-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="e6e22-156">In hello **configurazione istanza** pagina, scegliere **istanza predefinita**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Scegliere Istanza predefinita][ChooseDefaultInstance]
   
    <span data-ttu-id="e6e22-158">Per impostazione predefinita, hello predefinito istanza di SQL Server è in ascolto delle richieste dai client di SQL Server sulla porta statica 1433, ovvero quali hello connessioni ibride funzionalità richiede.</span><span class="sxs-lookup"><span data-stu-id="e6e22-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="e6e22-159">Le istanze denominate usano le porte dinamiche e UDP, che non sono supportate da Connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="e6e22-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="e6e22-160">Accettare i valori predefiniti hello hello **configurazione Server** pagina.</span><span class="sxs-lookup"><span data-stu-id="e6e22-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="e6e22-161">In hello **configurazione motore di Database** pagina **modalità di autenticazione**, scegliere **modalità mista (autenticazione di SQL Server e l'autenticazione di Windows)**e fornire una password.</span><span class="sxs-lookup"><span data-stu-id="e6e22-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Scegliere Modalità mista][ChooseMixedMode]
   
    <span data-ttu-id="e6e22-163">In questa esercitazione l'utente userà l'autenticazione SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e6e22-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="e6e22-164">Essere password hello tooremember assicurarsi che forniscono, poiché sarà necessario in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e6e22-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="e6e22-165">Scorrere il resto di hello dell'installazione guidata del hello toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="e6e22-166">Abilitare TCP/IP</span><span class="sxs-lookup"><span data-stu-id="e6e22-166">Enable TCP/IP</span></span>
<span data-ttu-id="e6e22-167">tooenable TCP/IP, utilizzare Gestione configurazione di SQL Server, che è stato installato durante l'installazione di SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="e6e22-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="e6e22-168">Seguire i passaggi di hello in [Abilita protocollo di rete TCP/IP per SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="e6e22-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="e6e22-169">Creare un database SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="e6e22-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="e6e22-170">L'applicazione Web Visual Studio richiede un database di appartenenza al quale Azure può effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e6e22-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="e6e22-171">Ciò richiede un database di SQL Server o SQL Server Express (non hello LocalDB database hello Usa modello MVC per impostazione predefinita), pertanto si creeranno database delle appartenenze hello successivamente.</span><span class="sxs-lookup"><span data-stu-id="e6e22-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="e6e22-172">In SQL Server Management Studio connettersi toohello SQL Server appena installato.</span><span class="sxs-lookup"><span data-stu-id="e6e22-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="e6e22-173">(Se hello **connettersi tooServer** finestra di dialogo non viene visualizzata automaticamente, passare troppo**Esplora oggetti** nel riquadro di sinistra hello, fare clic su **Connetti**, quindi fare clic su **Motore di database**.) ![Connettersi tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="e6e22-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="e6e22-174">In **Tipo server** scegliere **Motore di database**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="e6e22-175">Per **nome Server**, è possibile utilizzare **localhost** o nome hello del computer di hello che si sta utilizzando.</span><span class="sxs-lookup"><span data-stu-id="e6e22-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="e6e22-176">Scegliere **l'autenticazione di SQL Server**e quindi accedere con nome utente dell'amministratore di sistema di hello e una password hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e6e22-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="e6e22-177">toocreate un nuovo database utilizzando SQL Server Management Studio, fare doppio clic su **database** in Esplora oggetti e quindi fare clic su **Nuovo Database**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Creare il nuovo database][SSMScreateNewDB]
3. <span data-ttu-id="e6e22-179">In hello **Nuovo Database** finestra di dialogo immettere MembershipDB per nome del database hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Provide database name][SSMSprovideDBname]
   
    <span data-ttu-id="e6e22-181">Si noti che non si apportano qualsiasi database toohello modifiche a questo punto.</span><span class="sxs-lookup"><span data-stu-id="e6e22-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="e6e22-182">informazioni sull'appartenenza Hello verranno aggiunto automaticamente in un secondo momento dall'applicazione web al momento dell'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="e6e22-183">In Esplora oggetti, se si espande **database**, si noterà che è stato creato il database delle appartenenze hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB created][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="e6e22-185">B.</span><span class="sxs-lookup"><span data-stu-id="e6e22-185">B.</span></span> <span data-ttu-id="e6e22-186">Creare un'app web nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="e6e22-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="e6e22-187">Se un'app web è già stato creato in hello portale di Azure che si desidera toouse per questa esercitazione, è possibile andare troppo[creare una connessione ibrida e un BizTalk Service](#CreateHC) e continua da tale posizione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="e6e22-188">In hello [portale Azure](https://portal.azure.com), fare clic su **New** > **Web e dispositivi mobili** > **app Web**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![New button][New]
2. <span data-ttu-id="e6e22-190">Configurare l'applicazione web e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Website name][WebsiteCreationBlade]
3. <span data-ttu-id="e6e22-192">Dopo alcuni istanti, viene creato l'app web hello e viene visualizzato il pannello app web.</span><span class="sxs-lookup"><span data-stu-id="e6e22-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="e6e22-193">Pannello Hello è un dashboard scorrevole verticalmente che consente di gestire l'app web.</span><span class="sxs-lookup"><span data-stu-id="e6e22-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Website running][WebSiteRunningBlade]
   
    <span data-ttu-id="e6e22-195">tooverify hello web app è in tempo reale, è possibile fare clic su hello **Sfoglia** pagina predefinita di icona toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="e6e22-196">Successivamente, si creerà una connessione ibrida e un servizio BizTalk per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="e6e22-197">C.</span><span class="sxs-lookup"><span data-stu-id="e6e22-197">C.</span></span> <span data-ttu-id="e6e22-198">Creare una connessione ibrida e servizi BizTalk</span><span class="sxs-lookup"><span data-stu-id="e6e22-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="e6e22-199">Indietro nel portale di hello, toosettings, fare clic su **rete** > **configurare gli endpoint della connessione ibrida**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Connessioni ibride][CreateHCHCIcon]
2. <span data-ttu-id="e6e22-201">Nel Pannello di connessioni ibride hello, fare clic su **Aggiungi** > **nuova connessione ibrida**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="e6e22-202">In hello **creare la connessione ibrida** pannello:</span><span class="sxs-lookup"><span data-stu-id="e6e22-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="e6e22-203">Per **nome**, specificare un nome per la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="e6e22-204">Per **Hostname**, immettere il nome di computer hello del computer host SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e6e22-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="e6e22-205">Per **porta**, immettere 1433 (porta hello predefinita per SQL Server).</span><span class="sxs-lookup"><span data-stu-id="e6e22-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="e6e22-206">Fare clic su **BizTalk Service** > **nuovo servizio BizTalk** e immettere un nome per il servizio BizTalk hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Creare una connessione ibrida][TwinCreateHCBlades]
4. <span data-ttu-id="e6e22-208">Fare clic su **OK** due volte.</span><span class="sxs-lookup"><span data-stu-id="e6e22-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="e6e22-209">Quando il processo di hello viene completata, hello **notifiche** area farà lampeggiare una verde **successo** hello e **connessione ibrida** pannello mostrerà hello nuova connessione ibrida lo stato di Hello **non connesso**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![One hybrid connection created][CreateHCOneConnectionCreated]

<span data-ttu-id="e6e22-211">A questo punto, è stata completata una parte importante dell'infrastruttura di connessione di hello cloud ibrido.</span><span class="sxs-lookup"><span data-stu-id="e6e22-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="e6e22-212">Nel passaggio successivo verrà creato un elemento locale corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e6e22-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="e6e22-213">D.</span><span class="sxs-lookup"><span data-stu-id="e6e22-213">D.</span></span> <span data-ttu-id="e6e22-214">Installare connessione hello toocomplete di hello locale di Hybrid Connection Manager</span><span class="sxs-lookup"><span data-stu-id="e6e22-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="e6e22-215">Ora che infrastruttura di connessione ibrida hello è stata completata, si creerà un'applicazione web che lo utilizza.</span><span class="sxs-lookup"><span data-stu-id="e6e22-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="e6e22-216">E.</span><span class="sxs-lookup"><span data-stu-id="e6e22-216">E.</span></span> <span data-ttu-id="e6e22-217">Creare un progetto web ASP.NET base, modificare una stringa di connessione database hello ed eseguire progetto hello in locale</span><span class="sxs-lookup"><span data-stu-id="e6e22-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="e6e22-218">Create a basic ASP.NET project</span><span class="sxs-lookup"><span data-stu-id="e6e22-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="e6e22-219">In Visual Studio, su hello **File** menu, creare un nuovo progetto:</span><span class="sxs-lookup"><span data-stu-id="e6e22-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![New Visual Studio project][HCVSNewProject]
2. <span data-ttu-id="e6e22-221">In hello **modelli** sezione di hello **nuovo progetto** finestra di dialogo Seleziona **Web** e scegliere **applicazione Web ASP.NET**, quindi fare clic su  **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Choose ASP.NET Web Application][HCVSChooseASPNET]
3. <span data-ttu-id="e6e22-223">In hello **nuovo progetto ASP.NET** finestra di dialogo, scegliere **MVC**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Choose MVC][HCVSChooseMVC]
4. <span data-ttu-id="e6e22-225">Dopo aver creato il progetto di hello, verrà visualizzata la pagina file Leggimi di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="e6e22-226">Non eseguire ancora il progetto web hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-226">Do not run hello web project yet.</span></span>
   
    ![Readme page][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="e6e22-228">Modificare hello stringa di connessione di database per un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e6e22-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="e6e22-229">In questo passaggio, si modifica stringa di connessione hello che indica l'applicazione in cui toofind locale SQL Server Express database.</span><span class="sxs-lookup"><span data-stu-id="e6e22-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="e6e22-230">stringa di connessione Hello è il file Web. config dell'applicazione hello, che contiene informazioni di configurazione per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="e6e22-231">tooensure che l'applicazione utilizza database hello creati in SQL Server Express e non i hello uno in LocalDB predefinito di Visual Studio, è importante completare questo passaggio prima di eseguire il progetto.</span><span class="sxs-lookup"><span data-stu-id="e6e22-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="e6e22-232">In Esplora soluzioni fare doppio clic sul file Web. config hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="e6e22-234">Modifica hello **connectionStrings** database di SQL Server toohello toopoint sezione sul computer locale, la seguente sintassi hello in hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e6e22-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Stringa di connessione][HCVSConnectionString]
   
    <span data-ttu-id="e6e22-236">Quando la composizione di stringa di connessione hello, tenere seguente hello presente:</span><span class="sxs-lookup"><span data-stu-id="e6e22-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="e6e22-237">Se ci si connette tooa denominato istanza anziché un'istanza predefinita (ad esempio, YourServer\SQLEXPRESS), è necessario configurare le porte statiche toouse di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e6e22-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="e6e22-238">Per informazioni sulla configurazione delle porte statiche, vedere [come tooconfigure toolisten di SQL Server su una porta specifica](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="e6e22-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="e6e22-239">Per impostazione predefinita le istanze denominate usano UDP e le porte dinamiche, che non sono supportate dalle connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="e6e22-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="e6e22-240">È consigliabile specificare hello porta (1433 per impostazione predefinita, come illustrato nell'esempio hello) nella stringa di connessione hello in modo che è necessario che SQL Server locale è abilitato TCP e utilizza la porta corretta hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="e6e22-241">Tenere presente che toouse tooconnect di autenticazione di SQL Server, specificare ID utente hello e una password nella stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="e6e22-242">Fare clic su **salvare** nel file Web. config hello toosave di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6e22-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="e6e22-243">Eseguire il progetto hello in locale e registrare un nuovo utente</span><span class="sxs-lookup"><span data-stu-id="e6e22-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="e6e22-244">A questo punto, eseguire il nuovo progetto web in locale fare clic sul pulsante Sfoglia hello in Debug.</span><span class="sxs-lookup"><span data-stu-id="e6e22-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="e6e22-245">In questo esempio viene usato Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="e6e22-245">This example uses Internet Explorer.</span></span>
   
    ![Run project][HCVSRunProject]
2. <span data-ttu-id="e6e22-247">Scegliere hello angolo superiore destro della pagina web predefinita di hello, **registrare** tooregister un nuovo account:</span><span class="sxs-lookup"><span data-stu-id="e6e22-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Register a new account][HCVSRegisterLocally]
3. <span data-ttu-id="e6e22-249">Immettere un nome utente e una password:</span><span class="sxs-lookup"><span data-stu-id="e6e22-249">Enter a user name and password:</span></span>
   
    ![Enter user name and password][HCVSCreateNewAccount]
   
    <span data-ttu-id="e6e22-251">Verrà creato automaticamente un database in SQL Server locale che contiene informazioni sull'appartenenza hello per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="e6e22-252">Una delle tabelle di hello (**dbo. AspNetUsers**) contiene le credenziali utente di app come quelle appena immesso hello di web.</span><span class="sxs-lookup"><span data-stu-id="e6e22-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="e6e22-253">Questa tabella verrà visualizzato in un secondo momento nell'esercitazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="e6e22-254">Chiudere una finestra del browser hello della pagina web predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="e6e22-255">Questo arresta un'applicazione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6e22-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="e6e22-256">Ora pronti per la successiva hello, ovvero toopublish hello applicazione tooAzure ed eseguirne il test.</span><span class="sxs-lookup"><span data-stu-id="e6e22-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="e6e22-257">F.</span><span class="sxs-lookup"><span data-stu-id="e6e22-257">F.</span></span> <span data-ttu-id="e6e22-258">Pubblicare hello web applicazione tooAzure ed eseguirne il test</span><span class="sxs-lookup"><span data-stu-id="e6e22-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="e6e22-259">A questo punto, si sarà pubblicare il tooyour applicazione App del servizio web app e come testarlo toosee come la connessione ibrida hello configurati in precedenza è viene utilizzato tooconnect database toohello app web nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e6e22-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="e6e22-260">Pubblicare un'applicazione web hello</span><span class="sxs-lookup"><span data-stu-id="e6e22-260">Publish hello web application</span></span>
1. <span data-ttu-id="e6e22-261">È possibile scaricare il profilo di pubblicazione per app di servizio App web nel portale di Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="e6e22-262">Nel Pannello di hello per le app web, fare clic su **profilo di pubblicazione Get**e quindi salvare computer tooyour di file hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Scarica profilo di pubblicazione][PortalDownloadPublishProfile]
   
    <span data-ttu-id="e6e22-264">Quindi il file verrà importato nell'applicazione Web di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6e22-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="e6e22-265">In Visual Studio, nome del progetto hello in Esplora soluzioni e scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Select publish][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="e6e22-267">In hello **pubblica sul Web** della finestra di dialogo hello **profilo** scegliere **importazione**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Importa][HCVSPublishWebDialogImport]
4. <span data-ttu-id="e6e22-269">Sfoglia tooyour scaricato il profilo di pubblicazione, selezionarlo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Sfoglia tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="e6e22-271">Le informazioni di pubblicazione viene importate e lo visualizza in hello **connessione** scheda della finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="e6e22-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Click Publish][HCVSClickPublish]
   
    <span data-ttu-id="e6e22-273">Fare clic su **Pubblica**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="e6e22-274">Al termine del processo di pubblicazione, il browser verrà avviare e Mostra l'applicazione ASP.NET ormai, ad eccezione del fatto che ora è in tempo reale nel cloud di Azure hello!</span><span class="sxs-lookup"><span data-stu-id="e6e22-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="e6e22-275">Successivamente, si utilizzerà il toosee di applicazione web in tempo reale la connessione ibrida in azione.</span><span class="sxs-lookup"><span data-stu-id="e6e22-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="e6e22-276">Hello test completa l'applicazione web in Azure</span><span class="sxs-lookup"><span data-stu-id="e6e22-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="e6e22-277">In primo piano hello destra della pagina web in Azure, scegliere **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Test log in][HCTestLogIn]
2. <span data-ttu-id="e6e22-279">Il servizio App di app web è ora connesso database delle appartenenze dell'applicazione web tooyour sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="e6e22-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="e6e22-280">tooverify, accedere con hello stesse credenziali immesse hello locale del database in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e6e22-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Hello greeting][HCTestHelloContoso]
3. <span data-ttu-id="e6e22-282">toofurther testare la nuova connessione ibrida, esegue la disconnessione dell'applicazione web di Azure e registrare come altro utente.</span><span class="sxs-lookup"><span data-stu-id="e6e22-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="e6e22-283">Specificare un nuovo nome utente e password, quindi fare clic su **Registra**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test register another user][HCTestRegisterRelecloud]
4. <span data-ttu-id="e6e22-285">tooverify che hello credenziali del nuovo utente sono state archiviate nel database locale tramite la connessione ibrida, aprire SQL Management Studio nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="e6e22-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="e6e22-286">In Esplora oggetti espandere hello **MembershipDB** database e quindi espandere **tabelle**.</span><span class="sxs-lookup"><span data-stu-id="e6e22-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="e6e22-287">Pulsante destro del mouse hello **dbo. AspNetUsers** l'appartenenza di tabella e scegliere **seleziona le prime 1000 righe** risultati hello tooview.</span><span class="sxs-lookup"><span data-stu-id="e6e22-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Visualizzare i risultati di hello][HCTestSSMSTree]
5. <span data-ttu-id="e6e22-289">La tabella di appartenenza locale verranno visualizzati entrambi gli account - hello uno creato in locale e hello uno creato in hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e22-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="e6e22-290">Hello creata nel cloud hello è stato salvato il database locale tooyour tramite funzionalità di connessione ibrida di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e22-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Registered users in on-premises database][HCTestShowMemberDb]

<span data-ttu-id="e6e22-292">A questo punto, aver creato e distribuito un'applicazione web ASP.NET che usa una connessione ibrida tra un'app web nel cloud di Azure hello e un database di SQL Server locale.</span><span class="sxs-lookup"><span data-stu-id="e6e22-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="e6e22-293">Congratulazioni.</span><span class="sxs-lookup"><span data-stu-id="e6e22-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="e6e22-294">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="e6e22-294">See Also</span></span>
[<span data-ttu-id="e6e22-295">Panoramica delle connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="e6e22-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="e6e22-296">Josh Twist presenta le connessioni ibride (video Channel 9)</span><span class="sxs-lookup"><span data-stu-id="e6e22-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="e6e22-297">Panoramica delle connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="e6e22-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="e6e22-298">Servizi BizTalk: schede Dashboard, Monitor, Scala, Configura e Connessione ibrida</span><span class="sxs-lookup"><span data-stu-id="e6e22-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="e6e22-299">Creazione di un cloud ibrido reale con portabilità continua delle applicazioni (video Channel 9)</span><span class="sxs-lookup"><span data-stu-id="e6e22-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="e6e22-300">Accesso alle risorse locali usando connessioni ibride nel Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="e6e22-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="e6e22-301">Panoramica dell'identità ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e6e22-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
