---
title: aaaCreate servizi BizTalk di Azure nel portale di Azure hello | Documenti Microsoft
description: Informazioni su come tooprovision oppure creare servizi BizTalk di Azure nel portale di Azure; hello MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="accc0-103">Creazione di servizi di BizTalk tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="accc0-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="accc0-104">toosign in toohello portale di Azure, è necessario un account Azure e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="accc0-105">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="accc0-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="accc0-106">Vedere [Versione di valutazione gratuita di Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="accc0-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="accc0-107"><a name="CreateService"></a>Creare un servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="accc0-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="accc0-108">A seconda della versione scelta hello, non tutte le impostazioni di BizTalk Service potrebbero essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="accc0-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="accc0-109">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="accc0-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="accc0-110">Nel riquadro di spostamento inferiore hello, selezionare **NEW**:</span><span class="sxs-lookup"><span data-stu-id="accc0-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="accc0-111">![Selezionare nuovo pulsante hello][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="accc0-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="accc0-112">Selezionare **SERVIZI APP** > **SERVIZIO BIZTALK** > **CREAZIONE PERSONALIZZATA**:</span><span class="sxs-lookup"><span data-stu-id="accc0-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="accc0-113">![Selezionare BizTalk Service e quindi Custom Create][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="accc0-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="accc0-114">Immettere le impostazioni del servizio BizTalk hello:</span><span class="sxs-lookup"><span data-stu-id="accc0-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="accc0-115"><strong>Nome del servizio BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="accc0-116">È possibile inserire qualsiasi nome, ma deve essere specifico.</span><span class="sxs-lookup"><span data-stu-id="accc0-116">You can enter any name but be specific.</span></span> <span data-ttu-id="accc0-117">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="accc0-117">Some examples include:</span></span><br/><br/><span data-ttu-id="accc0-118">
    <em>azienda</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="accc0-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="accc0-119">
    <em>aziendaapplicazione</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="accc0-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="accc0-120">
    <em>applicazione</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="accc0-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="accc0-121">". <yourbiztalkservicename>.BizTalk.Windows.NET" è aggiunto automaticamente toohello nome immesso.</span><span class="sxs-lookup"><span data-stu-id="accc0-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="accc0-122">Crea un URL che viene utilizzato tooaccess il BizTalk del servizio, ad esempio <strong>https://<em>myapplication</em>. <yourbiztalkservicename>.BizTalk.Windows.NET</strong>.</span><span class="sxs-lookup"><span data-stu-id="accc0-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-123"><strong>Edizione</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="accc0-124">Se si è in fase di test/sviluppo hello, scegliere <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="accc0-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="accc0-125">Se si è in fase di produzione hello, utilizzare hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">servizi BizTalk: grafico edizioni</a> toodetermine se <strong>Premium</strong>, <strong>Standard</strong>, o <strong>Basic</strong>hello scelta corretta per lo scenario aziendale.</span><span class="sxs-lookup"><span data-stu-id="accc0-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-126"><strong>Area</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="accc0-127">Selezionare hello area geografica toohost il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-128"><strong>URL del dominio</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="accc0-129"><strong>Facoltativo</strong>.</span><span class="sxs-lookup"><span data-stu-id="accc0-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="accc0-130">Per impostazione predefinita, è l'URL del dominio hello <em>Nomeserviziobiztalk</em>. <yourbiztalkservicename>.BizTalk.Windows.NET.</span><span class="sxs-lookup"><span data-stu-id="accc0-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="accc0-131">È anche possibile specificare un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="accc0-131">A custom domain can also be entered.</span></span> <span data-ttu-id="accc0-132">Se ad esempio il dominio è <em>contoso</em>, è possibile immettere:</span><span class="sxs-lookup"><span data-stu-id="accc0-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="accc0-133">
    <em>Azienda</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="accc0-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="accc0-134">
    <em>AziendaApplicazione</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="accc0-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="accc0-135">
    <em>Applicazione</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="accc0-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="accc0-136">
    <em>NomeServizioBizTalk</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="accc0-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="accc0-137">Selezionare sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="accc0-138">5.</span><span class="sxs-lookup"><span data-stu-id="accc0-138">5.</span></span> <span data-ttu-id="accc0-139">Immettere hello archiviazione e le impostazioni del Database:</span><span class="sxs-lookup"><span data-stu-id="accc0-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="accc0-140"><strong>Account di archiviazione di monitoraggio/archiviazione</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="accc0-141">Selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="accc0-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="accc0-142">Se si crea un nuovo account di archiviazione, immettere hello <strong>nome Account di archiviazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="accc0-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-143"><strong>Database di rilevamento</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="accc0-144">Se si usa un database SQL di Azure esistente, non potrà essere usato da un altro servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="accc0-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="accc0-145">È necessario il nome di account di accesso hello e una password immesse al momento della creazione di Server di Database SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="accc0-146"><strong>Suggerimento</strong> Crea database di rilevamento hello e account di archiviazione di monitoraggio/archiviazione in hello stessa area come hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="accc0-147">Selezionare sulla freccia avanti hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="accc0-148">6.</span><span class="sxs-lookup"><span data-stu-id="accc0-148">6.</span></span> <span data-ttu-id="accc0-149">Immettere le impostazioni del Database hello:</span><span class="sxs-lookup"><span data-stu-id="accc0-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="accc0-150"><strong>Nome</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="accc0-151">Disponibile quando <strong>creare una nuova istanza di Database SQL</strong> è selezionata nella schermata precedente hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="accc0-152">Immettere un toobe Nome Database SQL utilizzato per il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-153"><strong>Server</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="accc0-154">Disponibile quando <strong>creare una nuova istanza di Database SQL</strong> è selezionata nella schermata precedente hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="accc0-155">Selezionare un server di database SQL esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="accc0-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-156"><strong>Nome account di accesso del server</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="accc0-157">Immettere nome utente account di accesso di hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-158"><strong>Password di accesso server</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="accc0-159">Immettere la password di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="accc0-160"><strong>Area</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="accc0-161">Disponibile quando è stata selezionata l'opzione <strong>Crea nuova istanza di database SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="accc0-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="accc0-162">Selezionare hello area geografica toohost il Database SQL.</span><span class="sxs-lookup"><span data-stu-id="accc0-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="accc0-163">Selezionare hello segno di spunta toocomplete hello guidata.</span><span class="sxs-lookup"><span data-stu-id="accc0-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="accc0-164">viene visualizzata l'icona di stato di avanzamento Hello:</span><span class="sxs-lookup"><span data-stu-id="accc0-164">hello progress icon appears:</span></span>  
![Icona di avanzamento visualizzata al termine][ProgressComplete]

<span data-ttu-id="accc0-166">Al termine, hello servizio BizTalk di Azure viene creato e pronto per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="accc0-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="accc0-167">le impostazioni predefinite di Hello sono sufficienti.</span><span class="sxs-lookup"><span data-stu-id="accc0-167">hello default settings are sufficient.</span></span> <span data-ttu-id="accc0-168">Se si desiderano toochange le impostazioni predefinite di hello, selezionare **servizi BIZTALK** in hello riquadro di spostamento a sinistra e quindi selezionare il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="accc0-169">Vengono visualizzate le impostazioni aggiuntive in hello [schede Dashboard, Monitor e Scale](biztalk-dashboard-monitor-scale-tabs.md) nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="accc0-170">A seconda dello stato hello di hello BizTalk Service, esistono alcune operazioni non possono essere completate.</span><span class="sxs-lookup"><span data-stu-id="accc0-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="accc0-171">Per un elenco di queste operazioni, andare troppo[grafico dello stato di servizi BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="accc0-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="accc0-172">Passaggi di post-provisioning</span><span class="sxs-lookup"><span data-stu-id="accc0-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="accc0-173">Installare il certificato di hello in un computer locale</span><span class="sxs-lookup"><span data-stu-id="accc0-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="accc0-174">Aggiungere un certificato per l'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="accc0-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="accc0-175">Ottenere lo spazio dei nomi di controllo di accesso hello</span><span class="sxs-lookup"><span data-stu-id="accc0-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="accc0-176"><a name="InstallCert"></a>Installare il certificato di hello in un computer locale</span><span class="sxs-lookup"><span data-stu-id="accc0-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="accc0-177">Come parte del provisioning del servizio BizTalk, un certificato autofirmato viene creato e associato alla sottoscrizione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="accc0-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="accc0-178">È necessario scaricare il certificato e installarlo nel computer in cui si distribuiscono applicazioni BizTalk Service o invia messaggi tooa endpoint BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="accc0-179">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="accc0-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="accc0-180">Selezionare **servizi BIZTALK** in hello riquadro di spostamento a sinistra e quindi selezionare la sottoscrizione di BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="accc0-181">Seleziona hello **Dashboard** scheda.</span><span class="sxs-lookup"><span data-stu-id="accc0-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="accc0-182">Selezionare **Scarica certificato SSL**:</span><span class="sxs-lookup"><span data-stu-id="accc0-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="accc0-183">![Modificare un certificato SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="accc0-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="accc0-184">Fare doppio clic sul certificato hello ed eseguire certificato hello tooinstall di hello procedura guidata.</span><span class="sxs-lookup"><span data-stu-id="accc0-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="accc0-185">Assicurarsi di installare il certificato di hello in hello **autorità di certificazione radice attendibili** archiviare.</span><span class="sxs-lookup"><span data-stu-id="accc0-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="accc0-186"><a name="AddCert"></a>Aggiungere un certificato per l'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="accc0-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="accc0-187">certificato autofirmato Hello che viene creato automaticamente quando la creazione di servizi BizTalk è destinata solo negli ambienti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="accc0-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="accc0-188">Per gli scenari di produzione, è necessario sostituirlo con un certificato di produzione.</span><span class="sxs-lookup"><span data-stu-id="accc0-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="accc0-189">In hello **Dashboard** , selezionare **certificato SSL di aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="accc0-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="accc0-190">Selezionare il certificato SSL privato di tooyour (*CertificateName*con estensione pfx) che include il nome di BizTalk Service, immettere la password di hello e quindi fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="accc0-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="accc0-191"><a name="ACS"></a>Ottenere lo spazio dei nomi di controllo di accesso hello</span><span class="sxs-lookup"><span data-stu-id="accc0-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="accc0-192">Accedi toohello [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="accc0-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="accc0-193">Selezionare **servizi BIZTALK** in hello riquadro di spostamento a sinistra e quindi selezionare il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="accc0-194">Nella barra delle applicazioni hello, selezionare **informazioni di connessione**:</span><span class="sxs-lookup"><span data-stu-id="accc0-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="accc0-195">![Selezionare Connection Information][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="accc0-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="accc0-196">Copiare i valori di controllo di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="accc0-197">Quando si distribuisce un progetto di servizio BizTalk da Visual Studio, si inserisce questo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="accc0-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="accc0-198">spazio dei nomi controllo di accesso di Hello viene creato automaticamente per il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="accc0-199">i valori di controllo di accesso Hello è utilizzabile con qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="accc0-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="accc0-200">Creazione di servizi BizTalk di Azure, questo spazio dei nomi di controllo di accesso controlla autenticazione hello con la distribuzione di BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="accc0-201">Se si desidera toochange hello sottoscrizione o la gestione dello spazio dei nomi hello, selezionare **ACTIVE DIRECTORY** in hello riquadro di spostamento a sinistra e quindi selezionare lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="accc0-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="accc0-202">barra delle applicazioni Hello Elenca le opzioni.</span><span class="sxs-lookup"><span data-stu-id="accc0-202">hello task bar lists your options.</span></span>

<span data-ttu-id="accc0-203">Fare clic su **Gestisci** apre hello portale di gestione di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="accc0-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="accc0-204">Nel portale di gestione di controllo di accesso hello, hello utilizza BizTalk Service **identità del servizio**:</span><span class="sxs-lookup"><span data-stu-id="accc0-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="accc0-205">![Identità del servizio ACS nel portale di gestione di controllo di accesso hello][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="accc0-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="accc0-206">Hello identità del servizio controllo di accesso è un insieme di credenziali che consentono alle applicazioni o client tooauthenticate direttamente con il controllo di accesso e di ricevere un token.</span><span class="sxs-lookup"><span data-stu-id="accc0-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="accc0-207">Usa Hello BizTalk Service **proprietario** per identità di servizio predefinita hello e hello **Password** valore.</span><span class="sxs-lookup"><span data-stu-id="accc0-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="accc0-208">Se si utilizza il valore di chiave simmetrica hello anziché hello valore della Password, hello può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="accc0-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="accc0-209">*Impossibile connettersi account servizio di gestione di controllo di accesso toohello hello specificato credenziali*</span><span class="sxs-lookup"><span data-stu-id="accc0-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="accc0-210">[Gestione dello spazio dei nomi del servizio di controllo di accesso](https://msdn.microsoft.com/library/azure/hh674478.aspx) sono fornite alcune linee guida e consigli utili.</span><span class="sxs-lookup"><span data-stu-id="accc0-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="accc0-211">Descrizione dei requisiti</span><span class="sxs-lookup"><span data-stu-id="accc0-211">Requirements explained</span></span>
<span data-ttu-id="accc0-212">Questi requisiti si applicano toohello edizione gratuita.</span><span class="sxs-lookup"><span data-stu-id="accc0-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="accc0-213"><strong>Elementi necessari</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="accc0-214"><strong>Perché sono necessari</strong></span><span class="sxs-lookup"><span data-stu-id="accc0-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="accc0-215">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="accc0-215">Azure subscription</span></span></td>
<td><span data-ttu-id="accc0-216">sottoscrizione Hello determina chi può accedere toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="accc0-217">titolare dell'Account Hello Crea sottoscrizione hello <a HREF="https://account.windowsazure.com/Subscriptions"> sottoscrizioni Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="accc0-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="accc0-218">Hello account Azure può disporre di più sottoscrizioni e può essere gestito da chiunque è consentito.</span><span class="sxs-lookup"><span data-stu-id="accc0-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="accc0-219">Ad esempio, il titolare dell'account di Azure crea una sottoscrizione denominata <em>BizTalkServiceSubscription</em> e offre hello amministratori BizTalk all'interno dell'azienda (ad esempio, ContosoBTSAdmins@live.com) accesso toothis sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="accc0-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="accc0-220">In questo scenario, gli amministratori BizTalk hello Accedi toohello portale di Azure e sono servizi del hello ospitato tooall diritti di amministratore completi nella sottoscrizione di hello, inclusi servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="accc0-221">gli amministratori di BizTalk Hello non sono titolari dell'account Azure hello e pertanto non hanno accesso le informazioni di fatturazione tooany.</span><span class="sxs-lookup"><span data-stu-id="accc0-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="accc0-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gestire le sottoscrizioni e gli account di archiviazione nel portale di Azure hello</a> vengono fornite ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="accc0-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="accc0-223">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="accc0-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="accc0-224">Archivia hello tabelle, viste e stored procedure utilizzate da BizTalk Service, inclusi i dati di rilevamento hello hello.</span><span class="sxs-lookup"><span data-stu-id="accc0-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="accc0-225">Quando si crea un servizio BizTalk, è possibile usare un server di Azure SQL o un database SQL di Azure esistente oppure creare automaticamente un nuovo server o database.</span><span class="sxs-lookup"><span data-stu-id="accc0-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="accc0-226">Hello scalabilità del Database SQL viene configurato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="accc0-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="accc0-227">In genere, la scala predefinita hello è sufficiente per un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="accc0-228">Modifica scala hello ha un impatto sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="accc0-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="accc0-229">Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Account e fatturazione nel database SQL di Azure</a>
</span><span class="sxs-lookup"><span data-stu-id="accc0-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="accc0-230">
<strong>Note</strong>
</span><span class="sxs-lookup"><span data-stu-id="accc0-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="accc0-231">Quando si crea un nuovo server SQL di Azure e un nuovo database, Servizi di Azure viene abilitato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="accc0-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="accc0-232">Hello BizTalk Service richiede servizi di Azure essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="accc0-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="accc0-233">Se si crea un nuovo Database SQL di Azure in un Server SQL Azure esistente, hello regole del firewall di hello Server non vengono modificati.</span><span class="sxs-lookup"><span data-stu-id="accc0-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="accc0-234">Di conseguenza, è possibile che altri servizi di Azure non sono consentiti i database del Server di accesso toohello.</span><span class="sxs-lookup"><span data-stu-id="accc0-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="accc0-235">Spazio dei nomi del servizio di controllo di accesso di Azure</span><span class="sxs-lookup"><span data-stu-id="accc0-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="accc0-236">Consente di eseguire l'autenticazione con Servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="accc0-237">Quando si distribuisce un progetto di servizio BizTalk da Visual Studio, si inserisce questo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="accc0-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="accc0-238">Quando si crea un BizTalk Service, lo spazio dei nomi di controllo di accesso hello viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="accc0-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="accc0-239">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="accc0-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="accc0-240">Consente di accedere a tootables, BLOB e code usate con i seguenti hello toosave di BizTalk Service:</span><span class="sxs-lookup"><span data-stu-id="accc0-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="accc0-241">File di log che hello monitoraggio BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="accc0-242">monitoraggio di output di Hello viene visualizzato anche nella hello **monitoraggio** scheda hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="accc0-243">Quando si crea un X12 o AS2 accordo tra partner, è possibile abilitare la proprietà messaggio hello archiviazione funzionalità toostore.</span><span class="sxs-lookup"><span data-stu-id="accc0-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="accc0-244">Questi dati vengono salvati in hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="accc0-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="accc0-245">Quando si crea un servizio BizTalk, è possibile usare un account di archiviazione esistente o crearne automaticamente uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="accc0-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="accc0-246">le impostazioni di archiviazione di Hello predefinite sono sufficienti per un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="accc0-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="accc0-247">Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="accc0-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="accc0-248">Queste chiavi controllano accesso tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="accc0-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="accc0-249">Hello BizTalk Service utilizza automaticamente hello chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="accc0-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="accc0-250">Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Archiviazione</a> per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="accc0-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="accc0-251">Certificato SSL privato</span><span class="sxs-lookup"><span data-stu-id="accc0-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="accc0-252">Quando si crea un servizio BizTalk di Azure, viene creato anche un URL HTTPS che include il nome del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="accc0-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="accc0-253">Questo URL è toouse configurato automaticamente un certificato autofirmato solo allo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="accc0-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="accc0-254">Per l'ambiente di produzione, è necessario un certificato SSL privato.</span><span class="sxs-lookup"><span data-stu-id="accc0-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="accc0-255">
<strong>Informazioni importanti sul certificato SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="accc0-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="accc0-256">Data di scadenza certificato Hello deve essere inferiore ai 5 anni.</span><span class="sxs-lookup"><span data-stu-id="accc0-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="accc0-257">Tutti i certificati privati richiedono una password.</span><span class="sxs-lookup"><span data-stu-id="accc0-257">All private certificates require a password.</span></span> <span data-ttu-id="accc0-258">Non dimenticare la password e, come procedura consigliata, condividerla con gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="accc0-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="accc0-259">I certificati autofirmati possono essere utilizzati in ambienti di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="accc0-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="accc0-260">Quando si utilizzano certificati autofirmati, importare l'archivio certificati personali di hello certificati tooyour e hello archivio certificati Autorità di certificazione radice attendibili.</span><span class="sxs-lookup"><span data-stu-id="accc0-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="accc0-261">Quando si invia l'autorità di certificazione tooyour richiesta certificato produzione hello, assegnare hello seguenti proprietà certificato:</span><span class="sxs-lookup"><span data-stu-id="accc0-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="accc0-262"><strong>Utilizzo chiavi avanzato</strong>. Servizi BizTalk di Azure richiede almeno l'autenticazione server.</span><span class="sxs-lookup"><span data-stu-id="accc0-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="accc0-263"><strong>Nome comune</strong>: immettere il nome di dominio completo hello (FQDN) dell'URL di servizio BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="accc0-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="accc0-264">Vedere <a HREF="#CreateService">Creare un servizio BizTalk</a> in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="accc0-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="accc0-265">È possibile aggiungere un certificato nuovo o diverso dopo hello BizTalk Service viene creato.</span><span class="sxs-lookup"><span data-stu-id="accc0-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="accc0-266">connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="accc0-266">Hybrid Connections</span></span>
<span data-ttu-id="accc0-267">Quando si crea un servizio BizTalk di Azure, hello **connessioni ibride** scheda è disponibile:</span><span class="sxs-lookup"><span data-stu-id="accc0-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![scheda per le connessioni ibride][HybridConnectionTab]

<span data-ttu-id="accc0-269">Le connessioni ibride sono usate tooconnect di Azure del sito Web tooany servizio mobile di Azure in locale o risorse che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP, servizi mobili e la maggior parte dei servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="accc0-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="accc0-270">Le connessioni ibride e hello servizio Adapter BizTalk sono diversi.</span><span class="sxs-lookup"><span data-stu-id="accc0-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="accc0-271">Hello servizio Adapter BizTalk è il sistema Line-of-Business (LOB) locale di tooconnect utilizzati servizi BizTalk di Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="accc0-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="accc0-272">Vedere [connessioni ibride](integration-hybrid-connection-overview.md) toolearn altre, incluse la creazione e gestione delle connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="accc0-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="accc0-273">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="accc0-273">Next steps</span></span>
<span data-ttu-id="accc0-274">Dopo aver creato un BizTalk Service, acquisire familiarità con diversi hello [servizi BizTalk: schede Dashboard, Monitor e Scale](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="accc0-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="accc0-275">Il servizio BizTalk è pronto per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="accc0-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="accc0-276">creazione di applicazioni, andare troppo toostart[servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="accc0-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="accc0-277">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="accc0-277">See also</span></span>
* [<span data-ttu-id="accc0-278">Servizi BizTalk: tabella delle edizioni</span><span class="sxs-lookup"><span data-stu-id="accc0-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="accc0-279">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="accc0-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="accc0-280">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="accc0-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="accc0-281">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="accc0-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="accc0-282">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="accc0-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="accc0-283">Come è possibile utilizzare hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="accc0-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="accc0-284">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="accc0-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
