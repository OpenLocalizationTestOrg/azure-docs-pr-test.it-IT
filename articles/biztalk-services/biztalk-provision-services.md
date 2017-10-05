---
title: Creare servizi BizTalk di Azure nel portale di Azure | Documentazione Microsoft
description: Informazioni su come effettuare il provisioning o creare un servizio BizTalk di Azure nel portale di Azure; MABS, WABS
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
ms.openlocfilehash: eca77b4a82eb67e1755717bb4429f8d450a64dc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-biztalk-services-using-the-azure-portal"></a><span data-ttu-id="6c702-103">Creazione di servizi BizTalk tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6c702-103">Create BizTalk Services using the Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="6c702-104">Per accedere al portale di Azure, è necessario un account Azure e una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="6c702-105">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6c702-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="6c702-106">Vedere [Versione di valutazione gratuita di Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="6c702-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="6c702-107"><a name="CreateService"></a>Creare un servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="6c702-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="6c702-108">A seconda dell'edizione scelta, non tutte le impostazioni del servizio BizTalk Service saranno disponibili.</span><span class="sxs-lookup"><span data-stu-id="6c702-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="6c702-109">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="6c702-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="6c702-110">Nella del pannello di navigazione inferiore selezionare **NUOVO**:</span><span class="sxs-lookup"><span data-stu-id="6c702-110">In the bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="6c702-111">![Selezionare il pulsante New][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="6c702-111">![Select the New button][NEWButton]</span></span>
3. <span data-ttu-id="6c702-112">Selezionare **SERVIZI APP** > **SERVIZIO BIZTALK** > **CREAZIONE PERSONALIZZATA**:</span><span class="sxs-lookup"><span data-stu-id="6c702-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="6c702-113">![Selezionare BizTalk Service e quindi Custom Create][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="6c702-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="6c702-114">Immettere le impostazioni del servizio BizTalk:</span><span class="sxs-lookup"><span data-stu-id="6c702-114">Enter the BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="6c702-115"><strong>Nome del servizio BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="6c702-116">È possibile inserire qualsiasi nome, ma deve essere specifico.</span><span class="sxs-lookup"><span data-stu-id="6c702-116">You can enter any name but be specific.</span></span> <span data-ttu-id="6c702-117">Di seguito sono riportati alcuni esempi:</span><span class="sxs-lookup"><span data-stu-id="6c702-117">Some examples include:</span></span><br/><br/><span data-ttu-id="6c702-118">
    <em>azienda</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="6c702-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="6c702-119">
    <em>aziendaapplicazione</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="6c702-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="6c702-120">
    <em>applicazione</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="6c702-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="6c702-121">".biztalk.windows.net" viene aggiunto automaticamente al nome digitato.</span><span class="sxs-lookup"><span data-stu-id="6c702-121">".biztalk.windows.net" is automatically added to the name you enter.</span></span> <span data-ttu-id="6c702-122">Verrà creato un URL usato per accedere al servizio BizTalk, ad esempio <strong>https://<em>applicazione</em>.biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-123"><strong>Edizione</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="6c702-124">Se si è nella fase di testing/sviluppo, scegliere l'edizione <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="6c702-125">Se si è nella fase di produzione, vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">Servizi BizTalk: Grafico edizioni</a> per determinare se la scelta corretta per il proprio scenario aziendale sia l'edizione <strong>Premium</strong>, <strong>Standard</strong> o <strong>Basic</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-126"><strong>Area</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="6c702-127">Selezionare l'area geografica per ospitare il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-127">Select the geographic region to host your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-128"><strong>URL del dominio</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="6c702-129"><strong>Facoltativo</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="6c702-130">Per impostazione predefinita, l'URL del dominio è <em>NomeServizioBizTalk</em>.biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6c702-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="6c702-131">È anche possibile specificare un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="6c702-131">A custom domain can also be entered.</span></span> <span data-ttu-id="6c702-132">Se ad esempio il dominio è <em>contoso</em>, è possibile immettere:</span><span class="sxs-lookup"><span data-stu-id="6c702-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="6c702-133">
    <em>Azienda</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="6c702-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="6c702-134">
    <em>AziendaApplicazione</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="6c702-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="6c702-135">
    <em>Applicazione</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="6c702-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="6c702-136">
    <em>NomeServizioBizTalk</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="6c702-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="6c702-137">Fare clic sulla freccia AVANTI.</span><span class="sxs-lookup"><span data-stu-id="6c702-137">Select the NEXT arrow.</span></span>
<span data-ttu-id="6c702-138">5.</span><span class="sxs-lookup"><span data-stu-id="6c702-138">5.</span></span> <span data-ttu-id="6c702-139">Immettere le impostazioni per archiviazione e database:</span><span class="sxs-lookup"><span data-stu-id="6c702-139">Enter the Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="6c702-140"><strong>Account di archiviazione di monitoraggio/archiviazione</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="6c702-141">Selezionare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="6c702-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="6c702-142">Se si crea un nuovo account di archiviazione, specificarne il nome in <strong>Nome account di archiviazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-143"><strong>Database di rilevamento</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="6c702-144">Se si usa un database SQL di Azure esistente, non potrà essere usato da un altro servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="6c702-145">È necessario disporre dell'account di accesso e della password immessi durante la creazione del server di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-145">You need the login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="6c702-146"><strong>SUGGERIMENTO</strong> Creare il database di rilevamento e l'account di archiviazione di monitoraggio/archiviazione nella stessa area geografica del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="6c702-147">Fare clic sulla freccia AVANTI.</span><span class="sxs-lookup"><span data-stu-id="6c702-147">Select the NEXT arrow.</span></span>
<span data-ttu-id="6c702-148">6.</span><span class="sxs-lookup"><span data-stu-id="6c702-148">6.</span></span> <span data-ttu-id="6c702-149">Immettere le impostazioni del database:</span><span class="sxs-lookup"><span data-stu-id="6c702-149">Enter the Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="6c702-150"><strong>Nome</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="6c702-151">Disponibile quando nella schermata precedente è stata selezionata l'opzione <strong>Crea nuova istanza di database SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="6c702-152">Immettere il nome di un database SQL da usare con il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-152">Enter a SQL Database name to be used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-153"><strong>Server</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="6c702-154">Disponibile quando nella schermata precedente è stata selezionata l'opzione <strong>Crea nuova istanza di database SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="6c702-155">Selezionare un server di database SQL esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="6c702-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-156"><strong>Nome account di accesso del server</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="6c702-157">Immettere il proprio nome utente di accesso.</span><span class="sxs-lookup"><span data-stu-id="6c702-157">Enter the login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-158"><strong>Password di accesso server</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="6c702-159">Immettere la password di accesso.</span><span class="sxs-lookup"><span data-stu-id="6c702-159">Enter the login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="6c702-160"><strong>Area</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="6c702-161">Disponibile quando è stata selezionata l'opzione <strong>Crea nuova istanza di database SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="6c702-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="6c702-162">Selezionare l'area geografica per ospitare il database SQL.</span><span class="sxs-lookup"><span data-stu-id="6c702-162">Select the geographic region to host your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="6c702-163">Per completare la procedura guidata, fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="6c702-163">Select the check mark to complete the wizard.</span></span> <span data-ttu-id="6c702-164">Viene visualizzata l'icona di avanzamento: </span><span class="sxs-lookup"><span data-stu-id="6c702-164">The progress icon appears:</span></span>  
![Icona di avanzamento visualizzata al termine][ProgressComplete]

<span data-ttu-id="6c702-166">Al termine, viene creato il servizio BizTalk di Azure che sarà disponibile per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c702-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="6c702-167">Le impostazioni predefinite sono sufficienti.</span><span class="sxs-lookup"><span data-stu-id="6c702-167">The default settings are sufficient.</span></span> <span data-ttu-id="6c702-168">Se si desidera modificare le impostazioni predefinite, selezionare **SERVIZI BIZTALK** nel pannello di navigazione sinistro e quindi selezionare il proprio servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="6c702-169">Altre impostazioni sono disponibili nelle [schede Dashboard, Monitoraggio e Scalabilità](biztalk-dashboard-monitor-scale-tabs.md) in alto.</span><span class="sxs-lookup"><span data-stu-id="6c702-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span></span>

<span data-ttu-id="6c702-170">A seconda dello stato del servizio BizTalk, alcune operazioni potrebbero non essere completate.</span><span class="sxs-lookup"><span data-stu-id="6c702-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="6c702-171">Per un elenco di queste operazioni, vedere [Servizi BizTalk: Tabella degli stati del servizio](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="6c702-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="6c702-172">Passaggi di post-provisioning</span><span class="sxs-lookup"><span data-stu-id="6c702-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="6c702-173">Installare il certificato in un computer locale</span><span class="sxs-lookup"><span data-stu-id="6c702-173">Install the certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="6c702-174">Aggiungere un certificato per l'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="6c702-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="6c702-175">Ottenere lo spazio dei nomi ACS</span><span class="sxs-lookup"><span data-stu-id="6c702-175">Get the Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="6c702-176"><a name="InstallCert"></a>Installare il certificato in un computer locale</span><span class="sxs-lookup"><span data-stu-id="6c702-176"><a name="InstallCert"></a>Install the certificate on a local computer</span></span>
<span data-ttu-id="6c702-177">Come parte del provisioning del servizio BizTalk, un certificato autofirmato viene creato e associato alla sottoscrizione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="6c702-178">È necessario scaricare questo certificato e installarlo nei computer da cui si distribuiscono applicazioni del servizio BizTalk o si inviano messaggi all'endpoint del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="6c702-179">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="6c702-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="6c702-180">Fare clic su **SERVIZI BIZTALK** nel riquadro di spostamento sinistro e quindi selezionare la sottoscrizione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="6c702-181">Selezionare la scheda **Dashboard** .</span><span class="sxs-lookup"><span data-stu-id="6c702-181">Select the **Dashboard** tab.</span></span>
4. <span data-ttu-id="6c702-182">Selezionare **Scarica certificato SSL**:</span><span class="sxs-lookup"><span data-stu-id="6c702-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="6c702-183">![Modificare un certificato SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="6c702-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="6c702-184">Fare doppio clic sul certificato ed eseguire la procedura guidata per installarlo.</span><span class="sxs-lookup"><span data-stu-id="6c702-184">Double-click the certificate and run through the wizard to install the certificate.</span></span> <span data-ttu-id="6c702-185">Assicurarsi di installare il certificato nell'archivio **Autorità di certificazione radice attendibili** .</span><span class="sxs-lookup"><span data-stu-id="6c702-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="6c702-186"><a name="AddCert"></a>Aggiungere un certificato per l'ambiente di produzione</span><span class="sxs-lookup"><span data-stu-id="6c702-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="6c702-187">Il certificato autofirmato creato automaticamente durante la creazione dei Servizi BizTalk è destinato all'uso solo negli ambienti di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6c702-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="6c702-188">Per gli scenari di produzione, è necessario sostituirlo con un certificato di produzione.</span><span class="sxs-lookup"><span data-stu-id="6c702-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="6c702-189">Nella scheda **Dashboard** fare clic su **Aggiorna certificato SSL**.</span><span class="sxs-lookup"><span data-stu-id="6c702-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="6c702-190">Cercare il certificato SSL privato (*NomeCertificato*.pfx) che include il nome del servizio BizTalk, immettere la password e quindi fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="6c702-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span></span>

#### <span data-ttu-id="6c702-191"><a name="ACS"></a>Ottenere lo spazio dei nomi ACS</span><span class="sxs-lookup"><span data-stu-id="6c702-191"><a name="ACS"></a>Get the Access Control namespace</span></span>
1. <span data-ttu-id="6c702-192">Accedere al [portale di Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="6c702-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="6c702-193">Selezionare **SERVIZI BIZTALK** nel pannello di navigazione sinistro e quindi scegliere il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="6c702-194">Nella barra delle applicazioni selezionare **Informazioni di connessione**:</span><span class="sxs-lookup"><span data-stu-id="6c702-194">In the task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="6c702-195">![Selezionare Connection Information][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="6c702-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="6c702-196">Copiare i valori di ACS.</span><span class="sxs-lookup"><span data-stu-id="6c702-196">Copy the Access Control values.</span></span>

<span data-ttu-id="6c702-197">Quando si distribuisce un progetto di servizio BizTalk da Visual Studio, si inserisce questo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6c702-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="6c702-198">Lo spazio dei nomi del servizio di controllo di accesso viene creato automaticamente per il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-198">The Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="6c702-199">I valori di ACS possono essere usati con qualsiasi applicazione.</span><span class="sxs-lookup"><span data-stu-id="6c702-199">The Access Control values can be used with any application.</span></span> <span data-ttu-id="6c702-200">Dopo la creazione di Servizi BizTalk di Azure, lo spazio del nomi ACS controlla l'autenticazione con la distribuzione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="6c702-201">Se si vuole modificare la sottoscrizione o gestire lo spazio dei nomi, selezionare **ACTIVE DIRECTORY** nel riquadro di spostamento sinistro e quindi selezionare lo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6c702-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span></span> <span data-ttu-id="6c702-202">Le opzioni sono elencate nella bassa delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c702-202">The task bar lists your options.</span></span>

<span data-ttu-id="6c702-203">Facendo clic su **Manage** è possibile aprire il portale di gestione del servizio di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="6c702-203">Clicking **Manage** opens the Access Control Management Portal.</span></span> <span data-ttu-id="6c702-204">Nel portale di gestione del controllo di accesso il servizio BizTalk usa le **identità del servizio**:</span><span class="sxs-lookup"><span data-stu-id="6c702-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="6c702-205">![Identità del servizio di controllo di accesso nel portale di gestione del servizio][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="6c702-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="6c702-206">Le identità del servizio di controllo di accesso sono set di credenziali che consentono ad applicazioni o client di eseguire l'autenticazione direttamente con il servizio di controllo di accesso e di ricevere un token.</span><span class="sxs-lookup"><span data-stu-id="6c702-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c702-207">Il servizio BizTalk usa **Owner** come identità predefinita del servizio e il valore **Password**.</span><span class="sxs-lookup"><span data-stu-id="6c702-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span></span> <span data-ttu-id="6c702-208">Se si usa il valore della chiave simmetrica anziché il valore della password, potrebbe verificarsi un errore simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="6c702-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span></span><br/><br/><span data-ttu-id="6c702-209">*Non è stato possibile connettersi all'account di gestione del servizio di controllo di accesso con le credenziali specificate*</span><span class="sxs-lookup"><span data-stu-id="6c702-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span></span>
> 
> 

<span data-ttu-id="6c702-210">[Gestione dello spazio dei nomi del servizio di controllo di accesso](https://msdn.microsoft.com/library/azure/hh674478.aspx) sono fornite alcune linee guida e consigli utili.</span><span class="sxs-lookup"><span data-stu-id="6c702-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="6c702-211">Descrizione dei requisiti</span><span class="sxs-lookup"><span data-stu-id="6c702-211">Requirements explained</span></span>
<span data-ttu-id="6c702-212">Questi requisiti non si applicano all'edizione gratuita.</span><span class="sxs-lookup"><span data-stu-id="6c702-212">These requirements do not apply to the Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="6c702-213"><strong>Elementi necessari</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="6c702-214"><strong>Perché sono necessari</strong></span><span class="sxs-lookup"><span data-stu-id="6c702-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="6c702-215">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="6c702-215">Azure subscription</span></span></td>
<td><span data-ttu-id="6c702-216">La sottoscrizione determina chi può accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-216">The subscription determines who can sign in to the Azure portal.</span></span> <span data-ttu-id="6c702-217">Il titolare dell'account crea la sottoscrizione nella pagina <a HREF="https://account.windowsazure.com/Subscriptions"> Sottoscrizioni Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="6c702-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="6c702-218">L'account Azure può avere più sottoscrizioni e può essere gestito da qualsiasi utente autorizzato.</span><span class="sxs-lookup"><span data-stu-id="6c702-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="6c702-219">Il titolare di un account Azure crea, ad esempio, una sottoscrizione denominata <em>SottoscrizioneServizioBizTalk</em> e concede l'accesso alla sottoscrizione agli amministratori di BizTalk all'interno dell'azienda, ad esempio ContosoBTSAdmins@live.com.</span><span class="sxs-lookup"><span data-stu-id="6c702-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span></span> <span data-ttu-id="6c702-220">In questo scenario gli amministratori di BizTalk accedono al portale di Azure e hanno i diritti di amministratore completi per tutti i servizi ospitati nella sottoscrizione, inclusi i Servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="6c702-221">Gli amministratori di BizTalk non sono titolari dell'account Azure e pertanto non possono accedere alle informazioni di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="6c702-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span></span>
<br/><br/><span data-ttu-id="6c702-222">Nell'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Gestire le sottoscrizioni e gli account di archiviazione nel portale di Azure</a> sono disponibili altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6c702-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="6c702-223">Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6c702-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="6c702-224">Archivia le tabelle, le visualizzazioni e le stored procedure usate dal servizio BizTalk, inclusi i dati di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="6c702-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="6c702-225">Quando si crea un servizio BizTalk, è possibile usare un server di Azure SQL o un database SQL di Azure esistente oppure creare automaticamente un nuovo server o database.</span><span class="sxs-lookup"><span data-stu-id="6c702-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="6c702-226">La scalabilità del database SQL viene configurata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6c702-226">The SQL Database scale is automatically configured.</span></span> <span data-ttu-id="6c702-227">In genere, la scalabilità predefinita è sufficiente per un servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-227">Typically, the default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="6c702-228">La modifica della scalabilità incide sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="6c702-228">Changing the scale impacts pricing.</span></span> <span data-ttu-id="6c702-229">Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Account e fatturazione nel database SQL di Azure</a>
</span><span class="sxs-lookup"><span data-stu-id="6c702-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="6c702-230">
<strong>Note</strong>
</span><span class="sxs-lookup"><span data-stu-id="6c702-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="6c702-231">Quando si crea un nuovo server SQL di Azure e un nuovo database, Servizi di Azure viene abilitato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6c702-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="6c702-232">Il servizio BizTalk richiede che Servizi di Azure sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="6c702-232">The BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="6c702-233">Se si crea un nuovo database SQL di Azure su un server SQL di Azure esistente, le regole del firewall del server non vengono modificate.</span><span class="sxs-lookup"><span data-stu-id="6c702-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span></span> <span data-ttu-id="6c702-234">Di conseguenza, è possibile che altri servizi di Azure non possano accedere ai database del server.</span><span class="sxs-lookup"><span data-stu-id="6c702-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="6c702-235">Spazio dei nomi del servizio di controllo di accesso di Azure</span><span class="sxs-lookup"><span data-stu-id="6c702-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="6c702-236">Consente di eseguire l'autenticazione con Servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="6c702-237">Quando si distribuisce un progetto di servizio BizTalk da Visual Studio, si inserisce questo spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="6c702-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="6c702-238">Quando si crea un servizio BizTalk, lo spazio dei nomi del servizio di controllo di accesso viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6c702-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="6c702-239">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="6c702-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="6c702-240">Consente l'accesso alle tabelle, ai BLOB e alle code usati dal servizio BizTalk per salvare quando indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6c702-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span></span>

<ul>
<li><span data-ttu-id="6c702-241">File di log che monitorano il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-241">Log files that monitor the BizTalk Service.</span></span> <span data-ttu-id="6c702-242">L'output del monitoraggio viene anche visualizzato nella scheda **Monitoraggio** del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span></span></li>
<li><span data-ttu-id="6c702-243">Quando si crea un contratto X12 o AS2 tra partner, è possibile abilitare la funzionalità di archiviazione per archiviare le proprietà dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="6c702-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span></span> <span data-ttu-id="6c702-244">I dati vengono salvati nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6c702-244">This data is saved in the Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="6c702-245">Quando si crea un servizio BizTalk, è possibile usare un account di archiviazione esistente o crearne automaticamente uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="6c702-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="6c702-246">Le impostazioni di archiviazione predefinite sono sufficienti per un servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-246">The default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="6c702-247">Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="6c702-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="6c702-248">Queste chiavi controllano l'accesso all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6c702-248">These Keys control access to your Storage account.</span></span> <span data-ttu-id="6c702-249">Il servizio BizTalk utilizza automaticamente la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="6c702-249">The BizTalk Service automatically uses the Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="6c702-250">Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Archiviazione</a> per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="6c702-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="6c702-251">Certificato SSL privato</span><span class="sxs-lookup"><span data-stu-id="6c702-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="6c702-252">Quando si crea un servizio BizTalk di Azure, viene creato anche un URL HTTPS che include il nome del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="6c702-253">Questo URL viene configurato automaticamente per l'uso del certificato autofirmato solo per l'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="6c702-253">This URL is automatically configured to use a self-signed development-only certificate.</span></span> <span data-ttu-id="6c702-254">Per l'ambiente di produzione, è necessario un certificato SSL privato.</span><span class="sxs-lookup"><span data-stu-id="6c702-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="6c702-255">
<strong>Informazioni importanti sul certificato SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="6c702-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="6c702-256">La data di scadenza del certificato deve essere inferiore ai 5 anni.</span><span class="sxs-lookup"><span data-stu-id="6c702-256">The certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="6c702-257">Tutti i certificati privati richiedono una password.</span><span class="sxs-lookup"><span data-stu-id="6c702-257">All private certificates require a password.</span></span> <span data-ttu-id="6c702-258">Non dimenticare la password e, come procedura consigliata, condividerla con gli amministratori.</span><span class="sxs-lookup"><span data-stu-id="6c702-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="6c702-259">I certificati autofirmati possono essere utilizzati in ambienti di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="6c702-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="6c702-260">Quando si utilizzano certificati autofirmati, è necessario importare il certificato nell'archivio dei certificati personale e nell'archivio dei certificati delle autorità di certificazione radice disponibili nell'elenco locale.</span><span class="sxs-lookup"><span data-stu-id="6c702-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="6c702-261">Quando si invia la richiesta del certificato di produzione all'autorità di certificazione, specificare le proprietà del certificato seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c702-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="6c702-262"><strong>Utilizzo chiavi avanzato</strong>. Servizi BizTalk di Azure richiede almeno l'autenticazione server.</span><span class="sxs-lookup"><span data-stu-id="6c702-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="6c702-263"><strong>Nome comune</strong>. Immettere il nome di dominio completo (FQDN) dell'URL del servizio BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c702-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="6c702-264">Vedere <a HREF="#CreateService">Creare un servizio BizTalk</a> in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6c702-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="6c702-265">È possibile aggiungere un nuovo certificato o un certificato diverso al termine della creazione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6c702-265">A new or different certificate can be added after the BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting to any location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="6c702-266">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="6c702-266">Hybrid Connections</span></span>
<span data-ttu-id="6c702-267">Quando si crea un servizio BizTalk di Azure, è disponibile la scheda relativa alle **connessioni ibride** :</span><span class="sxs-lookup"><span data-stu-id="6c702-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span></span>

![scheda per le connessioni ibride][HybridConnectionTab]

<span data-ttu-id="6c702-269">Le connessioni ibride consentono la connessione di un sito Web o di un servizio mobile di Azure, a una risorsa locale che usa una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP, Servizi mobili e la maggior parte dei servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="6c702-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="6c702-270">Le connessioni ibride e BizTalk Adapter Service presentano differenze.</span><span class="sxs-lookup"><span data-stu-id="6c702-270">Hybrid Connections and the BizTalk Adapter Service are different.</span></span> <span data-ttu-id="6c702-271">BizTalk Adapter Service viene usato per la connessione di Servizi BizTalk di a un sistema line-of-business locale.</span><span class="sxs-lookup"><span data-stu-id="6c702-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="6c702-272">Per altre informazioni, inclusa la creazione e la gestione di connessioni ibride, vedere [Connessioni ibride](integration-hybrid-connection-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="6c702-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c702-273">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c702-273">Next steps</span></span>
<span data-ttu-id="6c702-274">Dopo la creazione del servizio BizTalk, è possibile acquisire familiarità con le diverse [schede Dashboard, Monitoraggio e Scalabilità di Servizi BizTalk](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="6c702-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="6c702-275">Il servizio BizTalk è pronto per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="6c702-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="6c702-276">Per iniziare a creare applicazioni, vedere [Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="6c702-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="6c702-277">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="6c702-277">See also</span></span>
* [<span data-ttu-id="6c702-278">Servizi BizTalk: tabella delle edizioni</span><span class="sxs-lookup"><span data-stu-id="6c702-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="6c702-279">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="6c702-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="6c702-280">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="6c702-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="6c702-281">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="6c702-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="6c702-282">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="6c702-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="6c702-283">Come iniziare a usare l'SDK di Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="6c702-283">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="6c702-284">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="6c702-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
