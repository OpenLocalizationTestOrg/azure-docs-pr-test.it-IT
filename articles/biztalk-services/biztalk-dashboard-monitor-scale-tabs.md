---
title: "aaaDashboard, monitoraggio, scalabilità, configura e le connessioni ibride in servizi BizTalk | Documenti Microsoft"
description: "Informazioni sui controlli hello e monitorare le prestazioni nelle schede portale classico hello per i servizi BizTalk: Dashboard, monitoraggio, scalabilità, configura e le connessioni ibride. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="90567-104">Esaminare le schede del Dashboard, monitoraggio, scalabilità, configura e connessione ibrida hello</span><span class="sxs-lookup"><span data-stu-id="90567-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="90567-105">Dopo aver creato il BizTalk Service e distribuire l'applicazione, è possibile modificare alcune delle impostazioni del servizio BizTalk hello e monitorare le prestazioni dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="90567-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="90567-106">Quando si apre hello portale di Azure classico, viene automaticamente indirizzato alla hello **tutti gli elementi** scheda tooview il BizTalk Service, selezionare il BizTalk Service in hello **tutti gli elementi** tab o seleziona hello **Servizi BIZTALK** ; e quindi selezionare il nome di BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="90567-107">Verrà visualizzata una nuova finestra con hello seguenti schede.</span><span class="sxs-lookup"><span data-stu-id="90567-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="90567-108">In questo argomento vengono descritte queste schede.</span><span class="sxs-lookup"><span data-stu-id="90567-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="90567-109">Guida introduttiva (</span><span class="sxs-lookup"><span data-stu-id="90567-109">Quickstart (</span></span>![Guida introduttiva][Quickstart]<span data-ttu-id="90567-111">)</span><span class="sxs-lookup"><span data-stu-id="90567-111">)</span></span>
<span data-ttu-id="90567-112">A seconda di hello BizTalk Services Edition, tutte le opzioni elencate non siano disponibili.</span><span class="sxs-lookup"><span data-stu-id="90567-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="90567-113"><strong>Ottenere strumenti hello</strong></span><span class="sxs-lookup"><span data-stu-id="90567-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="90567-114">Scaricare i modelli di progetto Visual Studio per la hello tooinstall hello BizTalk Services SDK nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="90567-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="90567-115">Questi modelli creano hello <strong>servizi BizTalk</strong> (bridge) e hello <strong>elementi del servizio BizTalk</strong> progetti di Visual Studio (Transform) che sono distribuiti tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="90567-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Come avviare in uso hello Azure BizTalk Services SDK </a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">hello installare Azure BizTalk Services SDK</a> elenchi hello tooget passaggi avviato.</span><span class="sxs-lookup"><span data-stu-id="90567-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="90567-117"><strong>Creare contratti con il partner</strong></span><span class="sxs-lookup"><span data-stu-id="90567-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="90567-118">Verrà visualizzata la hello portale servizi BizTalk di Azure ospitati in Azure in cui si aggiungere partner e creare X12, AS2 e i contratti EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="90567-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="90567-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione dei componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> elenchi hello tooget passaggi avviato.</span><span class="sxs-lookup"><span data-stu-id="90567-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="90567-120"><strong>Altre informazioni sui Servizi BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="90567-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="90567-121">Passare toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn informazioni sui servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="90567-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="90567-122">Nella barra delle applicazioni hello nella parte inferiore di hello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="90567-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="90567-123"><strong>Gestire</strong> la distribuzione delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="90567-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="90567-124">È possibile aprire il portale di servizi BizTalk di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="90567-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="90567-125">Portale dei servizi BizTalk di Hello è hello entrata tooEDI configurazione, incluse l'aggiunta di partner e la creazione di X12, AS2 e i contratti EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="90567-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="90567-126">Questo è hello identico <strong>creare accordi tra partner</strong> su hello <strong>avvio rapido</strong> scheda.</span><span class="sxs-lookup"><span data-stu-id="90567-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="90567-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione dei componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> vengono fornite ulteriori informazioni su hello portale dei servizi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="90567-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="90567-128"><strong>Informazioni di connessione</strong> di hello Namespace di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="90567-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="90567-129">Quando si seleziona informazioni di connessione, quindi hello Namespace di controllo di accesso, autorità di certificazione predefinita e vengono visualizzati chiave predefinita.</span><span class="sxs-lookup"><span data-stu-id="90567-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="90567-130">È possibile copiare questi valori.</span><span class="sxs-lookup"><span data-stu-id="90567-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="90567-131">È inoltre possibile aprire hello portale controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="90567-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="90567-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Creare un controllo di accesso Namespace</a> vengono fornite ulteriori informazioni sul portale di Access Control hello.</span><span class="sxs-lookup"><span data-stu-id="90567-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="90567-133"><strong>Le chiavi di sincronizzazione</strong> in hello Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="90567-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="90567-134">Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="90567-135">Queste chiavi di crittografia di controllo accesso tooyour Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90567-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="90567-136">Il BizTalk Service utilizza automaticamente hello chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="90567-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="90567-137"><strong>Sincronizzare le chiavi</strong> abilitare gli utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="90567-138">Ad esempio, si desidera hello BizTalk Service toouse una nuova chiave primaria per hello Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90567-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="90567-139">toodo questo:</span><span class="sxs-lookup"><span data-stu-id="90567-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="90567-140">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="90567-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="90567-141">Selezionare hello chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-141">Select hello Secondary Key.</span></span> <span data-ttu-id="90567-142">Quando si esegue questa operazione, hello BizTalk Service avvia utilizzando hello chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="90567-143">Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave primaria hello.</span><span class="sxs-lookup"><span data-stu-id="90567-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="90567-144">Tenere presente, il BizTalk Service utilizza hello chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="90567-145">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="90567-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="90567-146">A questo punto, selezionare hello chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="90567-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="90567-147">Questo è hello nuova chiave primaria è stata rigenerata.</span><span class="sxs-lookup"><span data-stu-id="90567-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="90567-148">Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="90567-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="90567-149">Questo processo è denominato "chiavi di rollover".</span><span class="sxs-lookup"><span data-stu-id="90567-149">This process is called "rollover keys".</span></span> <span data-ttu-id="90567-150">scopo di Hello è tooenable utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="90567-151"><strong>Eliminare</strong> l'applicazione</span><span class="sxs-lookup"><span data-stu-id="90567-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="90567-152">Quando si seleziona, Elimina, il BizTalk Service e vengono rimossi tutti gli elementi distribuiti tooit.</span><span class="sxs-lookup"><span data-stu-id="90567-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="90567-153">Dashboard</span><span class="sxs-lookup"><span data-stu-id="90567-153">Dashboard</span></span>
<span data-ttu-id="90567-154">A seconda di hello BizTalk Services Edition, tutte le opzioni elencate non siano disponibili.</span><span class="sxs-lookup"><span data-stu-id="90567-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="90567-155">Quando si seleziona il nome di BizTalk Service, viene visualizzata nella scheda Dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="90567-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="90567-156">in cui è possibile effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="90567-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="90567-157">Panoramica sull'utilizzo: Mostra il numero di hello di utilizzate connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="90567-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="90567-158">Visualizza anche l'utilizzo di dati hello in GB.</span><span class="sxs-lookup"><span data-stu-id="90567-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="90567-159">Grafico delle metriche: mostra un elenco fisso di metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="90567-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="90567-160">Queste metriche forniscono valori in tempo reale relativamente integrità hello di hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="90567-161">È anche possibile scegliere hello **relativo** o **assoluto** hello e valori di intervallo di tempo **intervallo** di metriche di hello che vengono visualizzate nel grafico hello.</span><span class="sxs-lookup"><span data-stu-id="90567-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="90567-162">Per una descrizione di queste misurazioni delle prestazioni, andare troppo[le metriche disponibili](#Metrics) in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="90567-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="90567-163">Riepilogo rapido: elenca le proprietà del servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="90567-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="90567-164"><strong>Aggiornare le credenziali di Database di rilevamento</strong></span><span class="sxs-lookup"><span data-stu-id="90567-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="90567-165">Le modifiche hello nome utente e password utilizzati toolog in hello Database di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="90567-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-166"><strong>Aggiornare il certificato SSL</strong></span><span class="sxs-lookup"><span data-stu-id="90567-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="90567-167">Può aggiornare hello BizTalk Service toouse un certificato SSL diverso.</span><span class="sxs-lookup"><span data-stu-id="90567-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="90567-168">Un certificato SSL autofirmato viene creato automaticamente quando si <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">creare hello BizTalk Service</a>.</span><span class="sxs-lookup"><span data-stu-id="90567-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-169"><strong>Scaricare il certificato</strong></span><span class="sxs-lookup"><span data-stu-id="90567-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="90567-170">È possibile scaricare il certificato SSL hello utilizzato dal computer locale tooa BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-171"><strong>Status</strong></span><span class="sxs-lookup"><span data-stu-id="90567-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="90567-172">Visualizza lo stato corrente di hello del BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="90567-173">Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Servizi BizTalk: Tabella degli stati del servizio</a>.</span><span class="sxs-lookup"><span data-stu-id="90567-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="90567-174"><strong>URL del servizio</strong></span><span class="sxs-lookup"><span data-stu-id="90567-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="90567-175">Hello URL per il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="90567-176">Questo è hello stesso come hello <strong>URL di dominio</strong> immesso quando si crea il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-177"><strong>Indirizzo IP virtuale pubblico (VIP)</strong></span><span class="sxs-lookup"><span data-stu-id="90567-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="90567-178">indirizzo IP Hello assegnato tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="90567-179">Viene utilizzato per tutti gli endpoint di input e hello indirizzo di origine per il traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="90567-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="90567-180">Questo indirizzo IP appartiene tooyour BizTalk Service fino a quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="90567-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="90567-181">Se si elimina hello BizTalk Service, l'indirizzo IP hello viene assegnato tooanother BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-182"><strong>Spazio dei nomi ACS</strong></span><span class="sxs-lookup"><span data-stu-id="90567-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="90567-183">Esegue l'autenticazione con hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-184"><strong>Edizione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="90567-185">Elenca hello che Edition immesso quando viene creato hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-186"><strong>Posizione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="90567-187">Consente di visualizzare hello area geografica che ospita il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-188"><strong>Creato</strong></span><span class="sxs-lookup"><span data-stu-id="90567-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="90567-189">Hello di data e ora hello Visualizza BizTalk Service è stato creato.</span><span class="sxs-lookup"><span data-stu-id="90567-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-190"><strong>Database di rilevamento</strong></span><span class="sxs-lookup"><span data-stu-id="90567-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="90567-191">nome del Database SQL di Azure Hello che archivia hello utilizzate per il BizTalk Service tabelle di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="90567-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="90567-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">SPIEGAZIONE requisiti</a> fornisce informazioni dettagliate su Database di rilevamento hello.</span><span class="sxs-lookup"><span data-stu-id="90567-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-193"><strong>Memoria di monitoraggio/archiviazione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="90567-194">nome account di archiviazione di Azure Hello che archivia il monitoraggio dell'output del BizTalk Service hello.</span><span class="sxs-lookup"><span data-stu-id="90567-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="90567-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">SPIEGAZIONE requisiti</a> fornisce informazioni dettagliate su hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90567-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-196"><strong>Nome sottoscrizione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="90567-197">Elenca sottoscrizione hello che ospita il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="90567-198">sottoscrizione Hello regola accesso toohello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="90567-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-199"><strong>ID sottoscrizione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="90567-200">Quando si crea una sottoscrizione viene generato automaticamente un ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90567-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="90567-201">Quando si utilizza l'API REST, potrebbe essere necessario hello tooenter ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="90567-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="90567-202">[Servizi BizTalk: Portale classico di Azure tramite il Provisioning](http://go.microsoft.com/fwlink/p/?LinkID=302280) elenchi hello passaggi toocreate un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="90567-203">Informazioni di connessione, le chiavi di sincronizzazione, gestione ed eliminare nella barra delle applicazioni hello:</span><span class="sxs-lookup"><span data-stu-id="90567-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="90567-204"><strong>Gestire</strong> la distribuzione delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="90567-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="90567-205">Apre hello portale servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="90567-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="90567-206">Portale dei servizi BizTalk di Hello è hello entrata tooEDI configurazione, incluse l'aggiunta di partner e la creazione di X12, AS2 e i contratti EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="90567-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="90567-207">Questo è hello identico <strong>creare accordi tra partner</strong> su hello <strong>avvio rapido</strong> scheda.</span><span class="sxs-lookup"><span data-stu-id="90567-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="90567-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione dei componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> vengono fornite ulteriori informazioni su hello portale dei servizi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="90567-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-209"><strong>Informazioni di connessione</strong> di hello Namespace di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="90567-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="90567-210">Consente di visualizzare hello Namespace di controllo di accesso, l'autorità di certificazione predefinita e valori di chiave predefinita. che può essere copiato.</span><span class="sxs-lookup"><span data-stu-id="90567-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="90567-211">È inoltre possibile aprire hello portale controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="90567-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="90567-212">Questo portale di controllo di accesso è hello come utilizzando l'opzione di Active Directory hello nel riquadro di spostamento a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="90567-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="90567-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">La gestione di ACS Namespace</a> vengono fornite ulteriori informazioni sul portale di Access Control hello.</span><span class="sxs-lookup"><span data-stu-id="90567-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-214"><strong>Le chiavi di sincronizzazione</strong> in hello Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="90567-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="90567-215">Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="90567-216">Queste chiavi di crittografia di controllo accesso tooyour Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90567-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="90567-217">Il BizTalk Service utilizza automaticamente hello chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="90567-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="90567-218"><strong>Sincronizzare le chiavi</strong> abilitare gli utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="90567-219">Ad esempio, si desidera hello BizTalk Service toouse una nuova chiave primaria per hello Account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="90567-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="90567-220">toodo questo:</span><span class="sxs-lookup"><span data-stu-id="90567-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="90567-221">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="90567-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="90567-222">Selezionare hello chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-222">Select hello Secondary Key.</span></span> <span data-ttu-id="90567-223">Quando si esegue questa operazione, hello BizTalk Service avvia utilizzando hello chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="90567-224">Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave primaria hello.</span><span class="sxs-lookup"><span data-stu-id="90567-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="90567-225">Tenere presente, il BizTalk Service utilizza hello chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="90567-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="90567-226">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="90567-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="90567-227">A questo punto, selezionare hello chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="90567-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="90567-228">Questo è hello nuova chiave primaria è stata rigenerata.</span><span class="sxs-lookup"><span data-stu-id="90567-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="90567-229">Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="90567-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="90567-230">Questo processo è denominato "chiavi di rollover".</span><span class="sxs-lookup"><span data-stu-id="90567-230">This process is called "rollover keys".</span></span> <span data-ttu-id="90567-231">scopo di Hello è tooenable utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="90567-232"><strong>Eliminare</strong> l'applicazione</span><span class="sxs-lookup"><span data-stu-id="90567-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="90567-233">Il BizTalk Service e tutti gli elementi distribuiti tooit vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="90567-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="90567-234">Monitorare</span><span class="sxs-lookup"><span data-stu-id="90567-234">Monitor</span></span>
<span data-ttu-id="90567-235">Non si applica toohello edizione gratuita.</span><span class="sxs-lookup"><span data-stu-id="90567-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="90567-236">Quando si seleziona il nome di BizTalk Service, nella scheda Monitoraggio hello è disponibile e viene visualizzato il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="90567-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="90567-237">Metrica grafico: Hello Visualizza selezionato le metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="90567-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="90567-238">Queste metriche forniscono valori in tempo reale relativamente integrità hello di hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="90567-239">È l'utente a scegliere quali metriche visualizzare.</span><span class="sxs-lookup"><span data-stu-id="90567-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="90567-240">È possibile visualizzare fino a un massimo di sei metriche delle prestazioni simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="90567-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="90567-241">È anche possibile scegliere hello **relativo** o **assoluto** hello e valori di intervallo di tempo **intervallo** di metriche di hello che vengono visualizzate.</span><span class="sxs-lookup"><span data-stu-id="90567-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="90567-242">tooremove o visualizzare le metriche nel grafico hello:</span><span class="sxs-lookup"><span data-stu-id="90567-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="90567-243">Seleziona hello **monitoraggio** scheda.</span><span class="sxs-lookup"><span data-stu-id="90567-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="90567-244">Selezionare **Aggiungi metriche** nella barra delle applicazioni hello:</span><span class="sxs-lookup"><span data-stu-id="90567-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="90567-245">![Fare clic su Aggiungi metriche][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="90567-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="90567-246">Controllare le metriche delle prestazioni di hello desiderato toodisplay.</span><span class="sxs-lookup"><span data-stu-id="90567-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="90567-247">Selezionare hello segno di spunta tooreturn toohello **monitoraggio** scheda.</span><span class="sxs-lookup"><span data-stu-id="90567-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="90567-248">Selezionare hello cerchio Avanti toohello metrica toodisplay valore del tale metrica grafico hello.</span><span class="sxs-lookup"><span data-stu-id="90567-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="90567-249">Ad esempio, hello **l'utilizzo della CPU** metrica è inattivo; l'output non viene visualizzata nel grafico hello:</span><span class="sxs-lookup"><span data-stu-id="90567-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="90567-250">![Metrica Utilizzo CPU disabilitata][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="90567-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="90567-251">Seleziona hello in grigio hello tooenable cerchio **l'utilizzo della CPU** toodisplay metrica l'output nel grafico hello:</span><span class="sxs-lookup"><span data-stu-id="90567-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="90567-252">![Metrica Utilizzo CPU abilitata][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="90567-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="90567-253">Selezionare una metrica dal grafico visualizzato hello ed elenco hello tooremove **Elimina metrica** nella barra delle applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="90567-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="90567-254">tooadd hello metrica toohello indietro elenco, selezionare **Aggiungi metriche** hello sulla barra delle applicazioni, controllare la metrica hello e selezionare hello segno di spunta tooreturn toohello **monitoraggio** scheda. Cerchio tooenable hello metrica disabilitata hello Seleziona.</span><span class="sxs-lookup"><span data-stu-id="90567-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="90567-255"><a name="Metrics"></a>Metriche disponibili</span><span class="sxs-lookup"><span data-stu-id="90567-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="90567-256">Hello contatori/metriche delle prestazioni seguenti sono disponibile:</span><span class="sxs-lookup"><span data-stu-id="90567-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="90567-257"><strong>Latenza RountdTrip</strong></span><span class="sxs-lookup"><span data-stu-id="90567-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="90567-258">Consente di visualizzare hello tempo medio in millisecondi (ms) tooprocess che viene ricevuto un messaggio dal messaggio hello in fase di hello fino a quando il messaggio hello viene completamente elaborato da hello BizTalk Service tra tutti i Bridge.</span><span class="sxs-lookup"><span data-stu-id="90567-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="90567-259">Vengono conteggiati solo i messaggi correttamente elaborati.</span><span class="sxs-lookup"><span data-stu-id="90567-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="90567-260">Quando si verifica hello dopo gli eventi, viene creato un timestamp:</span><span class="sxs-lookup"><span data-stu-id="90567-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="90567-261">Gateway hello viene inserito un messaggio</span><span class="sxs-lookup"><span data-stu-id="90567-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="90567-262">Il messaggio è indirizzato toohello destinazione</span><span class="sxs-lookup"><span data-stu-id="90567-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="90567-263">Si riceve una risposta dalla destinazione</span><span class="sxs-lookup"><span data-stu-id="90567-263">Destination response is received</span></span></li>
<li><span data-ttu-id="90567-264">Destinazione acknowledgement risposta inviata toohello gateway</span><span class="sxs-lookup"><span data-stu-id="90567-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="90567-265">Questa metrica Mostra il risultato di hello di hello calcolo seguente:</span><span class="sxs-lookup"><span data-stu-id="90567-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="90567-266">[Destinazione acknowledgement risposta inviata toohello gateway] - [viene inserito un messaggio gateway hello]</span><span class="sxs-lookup"><span data-stu-id="90567-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-267"><strong>Errore nell'origine</strong></span><span class="sxs-lookup"><span data-stu-id="90567-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="90567-268">Visualizza hello il numero totale di messaggi non riusciti da hello BizTalk Service durante l'estrazione dei messaggi dagli endpoint di origine hello.</span><span class="sxs-lookup"><span data-stu-id="90567-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-269"><strong>Uso di CPU</strong></span><span class="sxs-lookup"><span data-stu-id="90567-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="90567-270">Elenca hello % tempo processore medio di tutte le istanze di ruolo.</span><span class="sxs-lookup"><span data-stu-id="90567-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-271"><strong>Latenza di elaborazione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="90567-272">Consente di visualizzare hello tempo medio In millisecondi (ms) tooprocess un messaggio hello BizTalk Service tra tutti i bridge, escluso il tempo di hello impiegato nelle destinazioni.</span><span class="sxs-lookup"><span data-stu-id="90567-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="90567-273">Vengono conteggiati solo i messaggi correttamente elaborati.</span><span class="sxs-lookup"><span data-stu-id="90567-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="90567-274">Quando ognuno dei seguenti eventi hello si verificano, viene creato un timestamp:</span><span class="sxs-lookup"><span data-stu-id="90567-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="90567-275">Gateway hello viene inserito un messaggio</span><span class="sxs-lookup"><span data-stu-id="90567-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="90567-276">Il messaggio è indirizzato toohello destinazione</span><span class="sxs-lookup"><span data-stu-id="90567-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="90567-277">Si riceve una risposta dalla destinazione</span><span class="sxs-lookup"><span data-stu-id="90567-277">Destination response is received</span></span></li>
<li><span data-ttu-id="90567-278">Destinazione acknowledgement risposta inviata toohello gateway</span><span class="sxs-lookup"><span data-stu-id="90567-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="90567-279">Questa metrica Mostra il risultato di hello di hello calcolo seguente:</span><span class="sxs-lookup"><span data-stu-id="90567-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="90567-280">[Destinazione acknowledgement risposta inviata toohello gateway] - [viene inserito un messaggio gateway hello] - [destinazione risposte] + [messaggio è indirizzato toohello destinazione]</span><span class="sxs-lookup"><span data-stu-id="90567-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-281"><strong>Errori nel processo</strong></span><span class="sxs-lookup"><span data-stu-id="90567-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="90567-282">Visualizza hello il numero totale di messaggi non riusciti durante l'elaborazione da hello BizTalk Service tra tutti i bridge hello all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="90567-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-283"><strong>Messaggi inviati</strong></span><span class="sxs-lookup"><span data-stu-id="90567-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="90567-284">Visualizza hello il numero totale di messaggi inviati dall'hello BizTalk Service tra tutti i Bridge all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="90567-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="90567-285">Questa metrica viene incrementata quando un messaggio inviato da una pipeline raggiunga la destinazione di route hello.</span><span class="sxs-lookup"><span data-stu-id="90567-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="90567-286">Questa metrica non indica la corretta elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="90567-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="90567-287">In uno scenario Request / Reply, metrica hello viene incrementato quando la destinazione di route hello invia una pipeline di ricezione acknowledgement toohello indietro.</span><span class="sxs-lookup"><span data-stu-id="90567-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-288"><strong>Messaggi ricevuti</strong></span><span class="sxs-lookup"><span data-stu-id="90567-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="90567-289">Visualizza hello il numero totale di messaggi ricevuti dalle hello BizTalk Service tra tutti i Bridge all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="90567-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="90567-290">Questa metrica viene incrementata quando viene ricevuto un nuovo messaggio dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="90567-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-291"><strong>Messaggi in elaborazione</strong></span><span class="sxs-lookup"><span data-stu-id="90567-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="90567-292">Consente di visualizzare hello numero totale di messaggi attualmente elaborati in hello BizTalk Service all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="90567-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="90567-293"><strong>Messaggi elaborati</strong></span><span class="sxs-lookup"><span data-stu-id="90567-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="90567-294">Consente di visualizzare hello numero totale dei messaggi correttamente elaborati da hello BizTalk Service tra tutti i Bridge all'interno di un intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="90567-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="90567-295">Questa metrica viene incrementata quando un messaggio viene ricevuto correttamente da pipeline hello e di destinazione toohello indirizzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="90567-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="90567-296">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="90567-296">Scale</span></span>
<span data-ttu-id="90567-297">Nella scheda Scala hello, è possibile aggiungere o sottrarre hello numero di unità utilizzata per il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="90567-298">Per impostazione predefinita è configurata una sola unità.</span><span class="sxs-lookup"><span data-stu-id="90567-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="90567-299">Unità aggiuntive possono essere aggiunti tooscale il BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="90567-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="90567-300">Quando si aumenta la scala hello, si stanno aumentando la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="90567-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="90567-301">quantità di Hello delle risorse aumenta anche, come bridge distribuiti, contratti, le connessioni LOB e potenza di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="90567-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="90567-302">Ad esempio, si aumenta scala hello da 1 unità too2 unità.</span><span class="sxs-lookup"><span data-stu-id="90567-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="90567-303">In questo caso, è possibile distribuire hello doppie numero di Bridge, double contratti hello, double connessioni LOB hello e potenza di elaborazione hello double.</span><span class="sxs-lookup"><span data-stu-id="90567-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="90567-304">Alcune edizioni di BizTalk non offrono un'opzione di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="90567-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="90567-305">in questo caso è consentita una sola unità.</span><span class="sxs-lookup"><span data-stu-id="90567-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="90567-306">toodetermine il numero di unità può essere ridimensionato l'edizione, vedere troppo[servizi BizTalk: grafico edizioni](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="90567-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="90567-307">Aumentare il numero di hello unità può influire sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="90567-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="90567-308">Se si aumenta l'unità di hello, selezionando **salvare** viene visualizzato un messaggio che indica se la fatturazione è stata interessata.</span><span class="sxs-lookup"><span data-stu-id="90567-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="90567-309">Scegliere quindi toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90567-309">You then choose toocontinue.</span></span> <span data-ttu-id="90567-310">Quando si aumenta il numero di hello di unità, lo stato di BizTalk Service hello cambia da tooUpdating attivo.</span><span class="sxs-lookup"><span data-stu-id="90567-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="90567-311">In hello lo stato di aggiornamento, il BizTalk Service continua toorun.</span><span class="sxs-lookup"><span data-stu-id="90567-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="90567-312">[Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md) viene definita una "Unità".</span><span class="sxs-lookup"><span data-stu-id="90567-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="90567-313">Configurare</span><span class="sxs-lookup"><span data-stu-id="90567-313">Configure</span></span>
<span data-ttu-id="90567-314">Non è applicabile tooHybrid connessioni.</span><span class="sxs-lookup"><span data-stu-id="90567-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="90567-315">Imposta hello stato Backup tooNone o automatico.</span><span class="sxs-lookup"><span data-stu-id="90567-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="90567-316">Quando impostato tooNone, non viene creato automaticamente alcun backup.</span><span class="sxs-lookup"><span data-stu-id="90567-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="90567-317">Quando impostato tooAutomatic, configurare un percorso di backup hello, frequenza di hello di hello backup e il tempo tookeep hello i file di backup.</span><span class="sxs-lookup"><span data-stu-id="90567-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="90567-318">[Servizi BizTalk: Backup e ripristino](biztalk-backup-restore.md) fornisce dettagli hello.</span><span class="sxs-lookup"><span data-stu-id="90567-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="90567-319"><a name="HybridConnections"></a>Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="90567-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="90567-320">Le connessioni ibride connettono un'applicazione Azure, ad esempio le applicazioni Web o App per dispositivi mobili in Azure App Service, risorsa locale tooan che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e più servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="90567-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="90567-321">Le connessioni ibride vengono gestite nei servizi BizTalk nel portale di Azure classico hello.</span><span class="sxs-lookup"><span data-stu-id="90567-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="90567-322">toocreate connessioni ibride in Azure App Service, vedere [accesso risorse locali mediante connessioni ibride in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="90567-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="90567-323">toocreate o gestire le connessioni ibride in servizi BizTalk di Azure, vedere [connessioni ibride](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="90567-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="90567-324">Avanti</span><span class="sxs-lookup"><span data-stu-id="90567-324">Next</span></span>
<span data-ttu-id="90567-325">Ora che si ha familiarità con diverse schede hello, ulteriori informazioni sulle funzionalità di servizi BizTalk di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="90567-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="90567-326">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="90567-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="90567-327">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="90567-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="90567-328">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="90567-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="90567-329">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="90567-329">See Also</span></span>
* [<span data-ttu-id="90567-330">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="90567-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="90567-331">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="90567-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="90567-332">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="90567-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="90567-333">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="90567-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="90567-334">Come è possibile utilizzare hello Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="90567-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

