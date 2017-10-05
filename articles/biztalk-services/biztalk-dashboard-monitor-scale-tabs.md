---
title: "Dashboard, Monitoraggio, Scalabilità, Configura e Connessioni ibride in Servizi BizTalk | Documentazione Microsoft"
description: "Informazioni sui controlli per monitorare le prestazioni nelle schede del portale classico per Servizi BizTalk: Dashboard, Monitoraggio, Scalabilità, Configura e Connessioni ibride. MABS, WABS"
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
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="92d1b-104">Analizzare le schede Dashboard, Monitor, Scala, Configura e Connessione ibrida</span><span class="sxs-lookup"><span data-stu-id="92d1b-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="92d1b-105">Dopo aver creato il servizio BizTalk e aver distribuito l'applicazione, è possibile modificare alcune impostazioni del servizio BizTalk e monitorare le prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="92d1b-106">Quando si apre il portale di Azure classico, viene visualizzata automaticamente la scheda **TUTTI GLI ELEMENTI** .</span><span class="sxs-lookup"><span data-stu-id="92d1b-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="92d1b-107">Per visualizzare il servizio BizTalk, selezionarlo nella scheda **TUTTI GLI ELEMENTI** oppure fare clic sulla scheda **SERVIZI BIZTALK**, quindi selezionare il nome del proprio servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="92d1b-108">Verrà aperta una nuova finestra con le schede seguenti:</span><span class="sxs-lookup"><span data-stu-id="92d1b-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="92d1b-109">In questo argomento vengono descritte queste schede.</span><span class="sxs-lookup"><span data-stu-id="92d1b-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="92d1b-110">Guida introduttiva (</span><span class="sxs-lookup"><span data-stu-id="92d1b-110">Quickstart (</span></span>![Guida introduttiva][Quickstart]<span data-ttu-id="92d1b-112">)</span><span class="sxs-lookup"><span data-stu-id="92d1b-112">)</span></span>
<span data-ttu-id="92d1b-113">A seconda dell'edizione di Servizi BizTalk, non tutte le opzioni elencate potrebbero essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="92d1b-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="92d1b-114"><strong>Ottenere gli strumenti</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="92d1b-115">Scaricare l'SDK di Servizi BizTalk per installare i modelli di progetto di Visual Studio sul computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="92d1b-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="92d1b-116">I modelli consentono di creare i progetti di Visual Studio <strong>BizTalk Services</strong> (bridge) e <strong>BizTalk Service Artifacts</strong> (Transform) distribuiti nel servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="92d1b-117">Gli articoli 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Come iniziare a usare Azure BizTalk Services SDK</a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installare Azure BizTalk Services SDK elencano tutte le procedure introduttive</a>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="92d1b-118"><strong>Creare contratti con il partner</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="92d1b-119">Consente di aprire il portale Servizi BizTalk di Azure ospitato su Azure dove aggiungere partner e creare contratti EDI X12, AS2 ed EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="92d1b-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="92d1b-120">L'articolo 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione di componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> elenca le procedure introduttive.</span><span class="sxs-lookup"><span data-stu-id="92d1b-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="92d1b-121"><strong>Altre informazioni sui Servizi BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="92d1b-122">Per altre informazioni sui Servizi BizTalk di Azure visitare l'<a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">area risorse</a>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="92d1b-123">Sulla barra delle applicazioni in basso è possibile:</span><span class="sxs-lookup"><span data-stu-id="92d1b-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="92d1b-124"><strong>Gestire</strong> la distribuzione delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="92d1b-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="92d1b-125">Viene aperto il portale di Servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="92d1b-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="92d1b-126">Il portale di Servizi BizTalk è l'ingresso alla configurazione EDI, incluse l'aggiunta di partner e la creazione di contratti X12, AS2 ed EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="92d1b-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="92d1b-127">Questa opzione ha la stessa funzione dell'opzione <strong>Crea contratti partner</strong> nella scheda <strong>Avvio rapido</strong>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="92d1b-128">L'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione di componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> contiene altre informazioni sul portale dei servizi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="92d1b-129"><strong>Informazioni di connessione</strong> dello spazio dei nomi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="92d1b-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="92d1b-130">Quando si seleziona Informazioni di connessione, vengono visualizzati i valori di Spazio dei nomi di Access Control, Autorità emittente predefinita e Chiave predefinita.</span><span class="sxs-lookup"><span data-stu-id="92d1b-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="92d1b-131">È possibile copiare questi valori.</span><span class="sxs-lookup"><span data-stu-id="92d1b-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="92d1b-132">È anche possibile aprire il portale di Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="92d1b-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="92d1b-133">L'articolo <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Creare uno spazio dei nomi di Controllo di accesso</a> offre altre informazioni sul portale di Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="92d1b-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="92d1b-134"><strong>Chiavi di sincronizzazione</strong> nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="92d1b-135">Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="92d1b-136">Queste chiavi di crittografia controllano l'accesso all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="92d1b-137">Il servizio BizTalk usa automaticamente la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="92d1b-138">L'opzione <strong>Chiavi di sincronizzazione</strong> consente agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="92d1b-139">Ad esempio, si potrebbe voler usare una nuova chiave primaria per l'account di archiviazione nel servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="92d1b-140">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="92d1b-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="92d1b-141">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="92d1b-142">Selezionare la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-142">Select the Secondary Key.</span></span> <span data-ttu-id="92d1b-143">Così facendo, il servizio BizTalk comincia a usare la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="92d1b-144">Nel portale di Azure classico, selezionare il proprio account di archiviazione e rigenerare la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="92d1b-145">Si tenga presente che il servizio BizTalk sta usando la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="92d1b-146">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="92d1b-147">Selezionare adesso la chiave primaria,</span><span class="sxs-lookup"><span data-stu-id="92d1b-147">Now, select the Primary Key.</span></span> <span data-ttu-id="92d1b-148">ossia la nuova chiave primaria rigenerata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="92d1b-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="92d1b-149">Nel portale di Azure classico, selezionare il proprio account di archiviazione e rigenerare la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="92d1b-150">Questo processo è denominato "chiavi di rollover".</span><span class="sxs-lookup"><span data-stu-id="92d1b-150">This process is called "rollover keys".</span></span> <span data-ttu-id="92d1b-151">Lo scopo è quello di consentire agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="92d1b-152"><strong>Eliminare</strong> l'applicazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="92d1b-153">Quando si fa clic su Elimina, il servizio BizTalk e tutti gli elementi distribuiti verranno rimossi.</span><span class="sxs-lookup"><span data-stu-id="92d1b-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="92d1b-154">Dashboard</span><span class="sxs-lookup"><span data-stu-id="92d1b-154">Dashboard</span></span>
<span data-ttu-id="92d1b-155">A seconda dell'edizione di Servizi BizTalk, non tutte le opzioni elencate potrebbero essere disponibili.</span><span class="sxs-lookup"><span data-stu-id="92d1b-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="92d1b-156">Quando si seleziona il nome del servizio BizTalk, viene visualizzata la scheda Dashboard,</span><span class="sxs-lookup"><span data-stu-id="92d1b-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="92d1b-157">in cui è possibile effettuare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="92d1b-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="92d1b-158">Panoramica sull'utilizzo: mostra il numero delle connessioni ibride usate</span><span class="sxs-lookup"><span data-stu-id="92d1b-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="92d1b-159">Visualizza anche l'uso dei dati espresso in GB.</span><span class="sxs-lookup"><span data-stu-id="92d1b-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="92d1b-160">Grafico delle metriche: mostra un elenco fisso di metriche delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="92d1b-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="92d1b-161">Include i valori in tempo reale riguardo l'integrità del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="92d1b-162">È anche possibile specificare il valore **Relativo** o **Assoluto** e l'**intervallo** di tempo delle metriche visualizzate nel grafico.</span><span class="sxs-lookup"><span data-stu-id="92d1b-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="92d1b-163">Per una descrizione delle metriche delle prestazioni, vedere la sezione [Metriche disponibili](#Metrics) in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="92d1b-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="92d1b-164">Riepilogo rapido: elenca le proprietà del servizio BizTalk</span><span class="sxs-lookup"><span data-stu-id="92d1b-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="92d1b-165"><strong>Aggiornare le credenziali di Database di rilevamento</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="92d1b-166">Consente di modificare il nome utente e la password usati per accedere al database di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="92d1b-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-167"><strong>Aggiornare il certificato SSL</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="92d1b-168">Consente di aggiornare il servizio BizTalk in modo da usare un certificato SSL diverso.</span><span class="sxs-lookup"><span data-stu-id="92d1b-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="92d1b-169">Quando si <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">crea il servizio BizTalk</a>, viene creato automaticamente un certificato SSL autofirmato.</span><span class="sxs-lookup"><span data-stu-id="92d1b-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-170"><strong>Scaricare il certificato</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="92d1b-171">Consente di scaricare il certificato SSL usato dal servizio BizTalk su un computer locale.</span><span class="sxs-lookup"><span data-stu-id="92d1b-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-172"><strong>Status</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="92d1b-173">Visualizza lo stato corrente del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="92d1b-174">Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Servizi BizTalk: Tabella degli stati del servizio</a>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-175"><strong>URL del servizio</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="92d1b-176">L'URL del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="92d1b-177">È uguale al valore di <strong>URL di dominio</strong> immesso al momento della creazione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-178"><strong>Indirizzo IP virtuale pubblico (VIP)</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="92d1b-179">Questo indirizzo IP viene assegnato al servizio BizTalk,</span><span class="sxs-lookup"><span data-stu-id="92d1b-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="92d1b-180">È usato per tutti gli endpoint di input ed è l'indirizzo di origine per il traffico in uscita.</span><span class="sxs-lookup"><span data-stu-id="92d1b-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="92d1b-181">Questo indirizzo IP appartiene al proprio servizio BizTalk, se viene creato.</span><span class="sxs-lookup"><span data-stu-id="92d1b-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="92d1b-182">Se si elimina il servizio BizTalk, l'indirizzo IP viene assegnato a un altro servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-183"><strong>Spazio dei nomi ACS</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="92d1b-184">Consente di eseguire l'autenticazione con il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-185"><strong>Edizione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="92d1b-186">Elenca l'edizione immessa al momento della creazione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-187"><strong>Posizione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="92d1b-188">Visualizza l'area geografica in cui è ospitato il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-189"><strong>Creato</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="92d1b-190">Visualizza la data e l'ora della creazione del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-191"><strong>Database di rilevamento</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="92d1b-192">Database SQL di Azure in cui sono archiviate le tabelle di rilevamento usate dal servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="92d1b-193">In 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Descrizione dei requisiti</a> sono disponibili informazioni dettagliate sul database di rilevamento.</span><span class="sxs-lookup"><span data-stu-id="92d1b-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-194"><strong>Memoria di monitoraggio/archiviazione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="92d1b-195">Nome dell'account di archiviazione di Azure in cui è archiviato l'output del monitoraggio del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="92d1b-196">In 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Descrizione dei requisiti</a> sono disponibili informazioni dettagliate sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-197"><strong>Nome sottoscrizione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="92d1b-198">Indica il nome della sottoscrizione che ospita il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="92d1b-199">La sottoscrizione consente di gestire l'accesso al portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="92d1b-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-200"><strong>ID sottoscrizione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="92d1b-201">Quando si crea una sottoscrizione viene generato automaticamente un ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="92d1b-202">Quando si utilizzano le API REST può essere necessario immettere l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="92d1b-203">[Servizi BizTalk: effettuare il provisioning mediante il portale di Azure classico](http://go.microsoft.com/fwlink/p/?LinkID=302280) sono elencati i passaggi per creare un servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="92d1b-204">Gestisci, Informazioni di connessione, Chiavi di sincronizzazione ed Elimina sulla barra delle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="92d1b-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="92d1b-205"><strong>Gestire</strong> la distribuzione delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="92d1b-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="92d1b-206">Viene aperto il portale di Servizi BizTalk di Azure.</span><span class="sxs-lookup"><span data-stu-id="92d1b-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="92d1b-207">Il portale di Servizi BizTalk è l'ingresso alla configurazione EDI, incluse l'aggiunta di partner e la creazione di contratti X12, AS2 ed EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="92d1b-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="92d1b-208">Questa opzione ha la stessa funzione dell'opzione <strong>Crea contratti partner</strong> nella scheda <strong>Avvio rapido</strong>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="92d1b-209">L'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione di componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> contiene altre informazioni sul portale dei servizi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-210"><strong>Informazioni di connessione</strong> dello spazio dei nomi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="92d1b-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="92d1b-211">Visualizza i valori di Spazio dei nomi di Access Control, Autorità emittente predefinita e Chiave predefinita, che possono essere copiati.</span><span class="sxs-lookup"><span data-stu-id="92d1b-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="92d1b-212">È anche possibile aprire il portale di Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="92d1b-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="92d1b-213">Questo portale di Controllo di accesso è lo stesso di quando si usa l'opzione Active Directory nel pannello di navigazione a sinistra.</span><span class="sxs-lookup"><span data-stu-id="92d1b-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="92d1b-214">L'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Gestione dello spazio dei nomi ACS</a> offre altre informazioni sul portale di Controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="92d1b-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-215"><strong>Chiavi di sincronizzazione</strong> nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="92d1b-216">Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="92d1b-217">Queste chiavi di crittografia controllano l'accesso all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="92d1b-218">Il servizio BizTalk usa automaticamente la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="92d1b-219">L'opzione <strong>Chiavi di sincronizzazione</strong> consente agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="92d1b-220">Ad esempio, si potrebbe voler usare una nuova chiave primaria per l'account di archiviazione nel servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="92d1b-221">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="92d1b-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="92d1b-222">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="92d1b-223">Selezionare la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-223">Select the Secondary Key.</span></span> <span data-ttu-id="92d1b-224">Così facendo, il servizio BizTalk comincia a usare la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="92d1b-225">Nel portale di Azure classico, selezionare il proprio account di archiviazione e rigenerare la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="92d1b-226">Si tenga presente che il servizio BizTalk sta usando la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="92d1b-227">Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>.</span><span class="sxs-lookup"><span data-stu-id="92d1b-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="92d1b-228">Selezionare adesso la chiave primaria,</span><span class="sxs-lookup"><span data-stu-id="92d1b-228">Now, select the Primary Key.</span></span> <span data-ttu-id="92d1b-229">ossia la nuova chiave primaria rigenerata dall'utente.</span><span class="sxs-lookup"><span data-stu-id="92d1b-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="92d1b-230">Nel portale di Azure classico, selezionare il proprio account di archiviazione e rigenerare la chiave secondaria.</span><span class="sxs-lookup"><span data-stu-id="92d1b-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="92d1b-231">Questo processo è denominato "chiavi di rollover".</span><span class="sxs-lookup"><span data-stu-id="92d1b-231">This process is called "rollover keys".</span></span> <span data-ttu-id="92d1b-232">Lo scopo è quello di consentire agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="92d1b-233"><strong>Eliminare</strong> l'applicazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="92d1b-234">Il servizio BizTalk e tutti gli elementi distribuiti verranno rimossi.</span><span class="sxs-lookup"><span data-stu-id="92d1b-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="92d1b-235">Monitoraggio</span><span class="sxs-lookup"><span data-stu-id="92d1b-235">Monitor</span></span>
<span data-ttu-id="92d1b-236">Non si applica all'edizione gratuita.</span><span class="sxs-lookup"><span data-stu-id="92d1b-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="92d1b-237">Quando si seleziona il nome del servizio BizTalk, la scheda Monitoraggio è disponibile e visualizza quanto indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="92d1b-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="92d1b-238">Grafico delle metriche: visualizza le metriche delle prestazioni selezionate</span><span class="sxs-lookup"><span data-stu-id="92d1b-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="92d1b-239">Include i valori in tempo reale riguardo l'integrità del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="92d1b-240">È l'utente a scegliere quali metriche visualizzare.</span><span class="sxs-lookup"><span data-stu-id="92d1b-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="92d1b-241">È possibile visualizzare fino a un massimo di sei metriche delle prestazioni simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="92d1b-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="92d1b-242">È anche possibile specificare il valore **Relativo** o **Assoluto** e l'**intervallo** di tempo delle metriche visualizzate.</span><span class="sxs-lookup"><span data-stu-id="92d1b-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="92d1b-243">Per rimuovere o visualizzare la metrica nel grafico</span><span class="sxs-lookup"><span data-stu-id="92d1b-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="92d1b-244">Selezionare la scheda **Monitoraggio** .</span><span class="sxs-lookup"><span data-stu-id="92d1b-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="92d1b-245">Selezionare **Aggiungi metriche** sulla barra delle applicazioni:</span><span class="sxs-lookup"><span data-stu-id="92d1b-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="92d1b-246">![Fare clic su Aggiungi metriche][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="92d1b-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="92d1b-247">Controllare la metrica delle prestazioni che si desidera visualizzare.</span><span class="sxs-lookup"><span data-stu-id="92d1b-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="92d1b-248">Fare clic sul segno di spunta per tornare alla scheda **Monitoraggio** .</span><span class="sxs-lookup"><span data-stu-id="92d1b-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="92d1b-249">Fare clic sul cerchio accanto alla metrica desiderata per visualizzarne il valore nel grafico.</span><span class="sxs-lookup"><span data-stu-id="92d1b-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="92d1b-250">Ad esempio, la metrica **Utilizzo CPU** è inattiva e il relativo output non è visualizzato nel grafico:</span><span class="sxs-lookup"><span data-stu-id="92d1b-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="92d1b-251">![Metrica Utilizzo CPU disabilitata][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="92d1b-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="92d1b-252">Selezionare il cerchio inattivo per abilitare la metrica **Utilizzo CPU** per visualizzarne l'output nel grafico:</span><span class="sxs-lookup"><span data-stu-id="92d1b-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="92d1b-253">![Metrica Utilizzo CPU abilitata][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="92d1b-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="92d1b-254">Per rimuovere una metrica dal grafico e dall'elenco, fare clic su **Elimina metrica** sulla barra delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="92d1b-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="92d1b-255">Per aggiungere di nuovo la metrica all'elenco, fare clic su **Aggiungi metriche** sulla barra delle applicazioni, controllare la metrica e fare clic sul segno di spunta per tornare alla scheda **Monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="92d1b-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="92d1b-256">Selezionare il cerchio in grigio per abilitare la metrica.</span><span class="sxs-lookup"><span data-stu-id="92d1b-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="92d1b-257"><a name="Metrics"></a>Metriche disponibili</span><span class="sxs-lookup"><span data-stu-id="92d1b-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="92d1b-258">Sono disponibili i contatori/le metriche seguenti:</span><span class="sxs-lookup"><span data-stu-id="92d1b-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="92d1b-259"><strong>Latenza RountdTrip</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="92d1b-260">Visualizza il tempo medio, espresso in millisecondi (ms), impiegato per l'elaborazione completa di un messaggio da parte del servizio BizTalk dal momento della ricezione attraverso tutti i bridge.</span><span class="sxs-lookup"><span data-stu-id="92d1b-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="92d1b-261">Vengono conteggiati solo i messaggi correttamente elaborati.</span><span class="sxs-lookup"><span data-stu-id="92d1b-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="92d1b-262">Quando si verificano gli eventi seguenti viene creato un timestamp:</span><span class="sxs-lookup"><span data-stu-id="92d1b-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="92d1b-263">Il messaggio accede al gateway</span><span class="sxs-lookup"><span data-stu-id="92d1b-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="92d1b-264">Il messaggio viene indirizzato alla destinazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="92d1b-265">Si riceve una risposta dalla destinazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-265">Destination response is received</span></span></li>
<li><span data-ttu-id="92d1b-266">La risposta di conferma della destinazione viene inviata al gateway</span><span class="sxs-lookup"><span data-stu-id="92d1b-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="92d1b-267">Questa metrica indica il risultato del calcolo seguente:</span><span class="sxs-lookup"><span data-stu-id="92d1b-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="92d1b-268">[La risposta di conferma della destinazione viene inviata al gateway] - [Il messaggio accede al gateway]</span><span class="sxs-lookup"><span data-stu-id="92d1b-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-269"><strong>Errore nell'origine</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="92d1b-270">Visualizza il numero totale di messaggi di cui il servizio BizTalk non eseguito correttamente il pull dagli endpoint di origine.</span><span class="sxs-lookup"><span data-stu-id="92d1b-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-271"><strong>Uso di CPU</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="92d1b-272">Consente di elencare il valore % tempo processore di tutte le istanze del ruolo.</span><span class="sxs-lookup"><span data-stu-id="92d1b-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-273"><strong>Latenza di elaborazione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="92d1b-274">Visualizza il tempo medio, espresso in millisecondi (ms), impiegato per l'elaborazione di un messaggio da parte del servizio BizTalk attraverso tutti i bridge, esclusi il tempo impiegato nelle destinazioni.</span><span class="sxs-lookup"><span data-stu-id="92d1b-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="92d1b-275">Vengono conteggiati solo i messaggi correttamente elaborati.</span><span class="sxs-lookup"><span data-stu-id="92d1b-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="92d1b-276">Quando si verifica uno degli eventi seguenti viene creato un timestamp:</span><span class="sxs-lookup"><span data-stu-id="92d1b-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="92d1b-277">Il messaggio accede al gateway</span><span class="sxs-lookup"><span data-stu-id="92d1b-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="92d1b-278">Il messaggio viene indirizzato alla destinazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="92d1b-279">Si riceve una risposta dalla destinazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-279">Destination response is received</span></span></li>
<li><span data-ttu-id="92d1b-280">La risposta di conferma della destinazione viene inviata al gateway</span><span class="sxs-lookup"><span data-stu-id="92d1b-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="92d1b-281">Questa metrica indica il risultato del calcolo seguente:</span><span class="sxs-lookup"><span data-stu-id="92d1b-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="92d1b-282">[La risposta di conferma della destinazione viene inviata al gateway] - [Il messaggio accede al gateway] - [Si riceve una risposta dalla destinazione] + [Il messaggio viene indirizzato alla destinazione]\\</span><span class="sxs-lookup"><span data-stu-id="92d1b-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-283"><strong>Errori nel processo</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="92d1b-284">Visualizza il numero totale di messaggi che il servizio BizTalk non ha elaborato correttamente attraverso tutti i bridge entro un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="92d1b-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-285"><strong>Messaggi inviati</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="92d1b-286">Visualizza il numero totale di messaggi inviati dal servizio BizTalk attraverso tutti i bridge entro un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="92d1b-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="92d1b-287">Questa metrica viene incrementata quando un messaggio inviato da una pipeline raggiunge la destinazione della route.</span><span class="sxs-lookup"><span data-stu-id="92d1b-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="92d1b-288">Questa metrica non indica la corretta elaborazione di un messaggio.</span><span class="sxs-lookup"><span data-stu-id="92d1b-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="92d1b-289">In uno scenario di tipo richiesta-risposta, la metrica viene incrementata quando la destinazione della route restituisce una conferma di ricezione alla pipeline.</span><span class="sxs-lookup"><span data-stu-id="92d1b-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-290"><strong>Messaggi ricevuti</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="92d1b-291">Visualizza il numero totale di messaggi ricevuti dal servizio BizTalk attraverso tutti i bridge entro un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="92d1b-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="92d1b-292">Questa metrica viene incrementata quando si riceve un nuovo messaggio inviato dalla pipeline.</span><span class="sxs-lookup"><span data-stu-id="92d1b-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-293"><strong>Messaggi in elaborazione</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="92d1b-294">Visualizza il numero totale di messaggi attualmente in corso di elaborazione da parte del servizio BizTalk entro un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="92d1b-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="92d1b-295"><strong>Messaggi elaborati</strong></span><span class="sxs-lookup"><span data-stu-id="92d1b-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="92d1b-296">Visualizza il numero totale di messaggi correttamente elaborati dal servizio BizTalk attraverso tutti i bridge entro un determinato intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="92d1b-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="92d1b-297">Questa metrica viene incrementata quando si riceve correttamente un messaggio inviato dalla pipeline, che viene quindi correttamente indirizzato alla destinazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="92d1b-298">Scalabilità</span><span class="sxs-lookup"><span data-stu-id="92d1b-298">Scale</span></span>
<span data-ttu-id="92d1b-299">Nella scheda Scale è possibile aggiungere o sottrarre il numero di unità utilizzate dal servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="92d1b-300">Per impostazione predefinita è configurata una sola unità.</span><span class="sxs-lookup"><span data-stu-id="92d1b-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="92d1b-301">È possibile aggiungere ulteriori unità per la scalabilità del servizio BizTalk.</span><span class="sxs-lookup"><span data-stu-id="92d1b-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="92d1b-302">Quando si aumenta la scalabilità si aumenta anche la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="92d1b-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="92d1b-303">Aumenta inoltre la quantità di risorse, inclusi i bridge distribuiti, i contratti, le connessioni LOB e la potenza di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="92d1b-304">Se ad esempio si aumenta la scalabilità da 1 unità a 2 unità,</span><span class="sxs-lookup"><span data-stu-id="92d1b-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="92d1b-305">è possibile distribuire un numero doppio di bridge, di contratti e di connessioni LOB, oltre a una quantità doppia di potenza di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="92d1b-306">Alcune edizioni di BizTalk non offrono un'opzione di scalabilità:</span><span class="sxs-lookup"><span data-stu-id="92d1b-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="92d1b-307">in questo caso è consentita una sola unità.</span><span class="sxs-lookup"><span data-stu-id="92d1b-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="92d1b-308">Per determinare il numero di unità in base al quale è possibile ridimensionare l'edizione in uso, vedere l'articolo [Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="92d1b-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="92d1b-309">L'aumento del numero di unità può incidere sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="92d1b-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="92d1b-310">Se si aumentano le unità, quando si seleziona **Salva** verrà visualizzato un messaggio che informa dell'impatto sulla fatturazione.</span><span class="sxs-lookup"><span data-stu-id="92d1b-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="92d1b-311">Sta all'utente sceglie se continuare.</span><span class="sxs-lookup"><span data-stu-id="92d1b-311">You then choose to continue.</span></span> <span data-ttu-id="92d1b-312">Quando si aumenta il numero di unità, lo stato del servizio BizTalk passa da Active ad Updating.</span><span class="sxs-lookup"><span data-stu-id="92d1b-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="92d1b-313">Nello stato Updating l'esecuzione del servizio BizTalk non verrà interrotta.</span><span class="sxs-lookup"><span data-stu-id="92d1b-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="92d1b-314">[Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md) viene definita una "Unità".</span><span class="sxs-lookup"><span data-stu-id="92d1b-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="92d1b-315">Configurare</span><span class="sxs-lookup"><span data-stu-id="92d1b-315">Configure</span></span>
<span data-ttu-id="92d1b-316">Non si applica alle connessioni ibride.</span><span class="sxs-lookup"><span data-stu-id="92d1b-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="92d1b-317">Imposta Stato backup su Nessuno o Automatico.</span><span class="sxs-lookup"><span data-stu-id="92d1b-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="92d1b-318">Se è impostato su Nessuno, non vengono creati backup automaticamente.</span><span class="sxs-lookup"><span data-stu-id="92d1b-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="92d1b-319">Se è impostato su Automatico, configurare il percorso di backup, la frequenza e la durata di mantenimento dei file di backup.</span><span class="sxs-lookup"><span data-stu-id="92d1b-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="92d1b-320">[Servizi BizTalk: backup e ripristino](biztalk-backup-restore.md) sono disponibili informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="92d1b-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="92d1b-321"><a name="HybridConnections"></a>Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="92d1b-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="92d1b-322">Le connessioni ibride consentono la connessione di un'applicazione Azure, come App Web o App per dispositivi mobili nel servizio app di Azure, a una risorsa locale che usa una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e la maggior parte dei servizi Web personalizzati.</span><span class="sxs-lookup"><span data-stu-id="92d1b-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="92d1b-323">Le connessioni ibride vengono gestite in Servizi BizTalk nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="92d1b-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="92d1b-324">Per creare connessioni ibride nel servizio app di Azure, vedere [Accedere alle risorse locali usando connessioni ibride nel servizio app di Azure](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="92d1b-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="92d1b-325">Per creare o gestire connessioni ibride in Siti Web di Azure, vedere l'articolo relativo alle [Connessioni ibride](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92d1b-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="92d1b-326">Avanti</span><span class="sxs-lookup"><span data-stu-id="92d1b-326">Next</span></span>
<span data-ttu-id="92d1b-327">Ora che è stata acquisita familiarità con le diverse schede è possibile ottenere altre informazioni sulle funzionalità dei Servizi BizTalk di Azure:</span><span class="sxs-lookup"><span data-stu-id="92d1b-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="92d1b-328">Servizi BizTalk: limitazione</span><span class="sxs-lookup"><span data-stu-id="92d1b-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="92d1b-329">Servizi BizTalk: nome e chiave dell'autorità emittente</span><span class="sxs-lookup"><span data-stu-id="92d1b-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="92d1b-330">Servizi BizTalk: backup e ripristino</span><span class="sxs-lookup"><span data-stu-id="92d1b-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="92d1b-331">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="92d1b-331">See Also</span></span>
* [<span data-ttu-id="92d1b-332">Connessioni ibride</span><span class="sxs-lookup"><span data-stu-id="92d1b-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="92d1b-333">Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium</span><span class="sxs-lookup"><span data-stu-id="92d1b-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="92d1b-334">Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="92d1b-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="92d1b-335">Servizi BizTalk: Tabella degli stati del servizio</span><span class="sxs-lookup"><span data-stu-id="92d1b-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="92d1b-336">Come iniziare a usare l'SDK di Servizi BizTalk di Azure</span><span class="sxs-lookup"><span data-stu-id="92d1b-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

