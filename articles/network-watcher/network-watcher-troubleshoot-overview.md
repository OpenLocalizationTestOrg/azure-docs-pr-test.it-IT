---
title: tooresource aaaIntroduction risoluzione dei problemi in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina fornisce una panoramica delle funzionalità di risoluzione dei problemi di hello Watcher di rete risorsa"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="fe431-103">Introduzione tooresource risoluzione dei problemi in Watcher di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="fe431-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="fe431-104">I gateway di rete virtuale forniscono la connettività tra le risorse locali e altre reti virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe431-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="fe431-105">Monitoraggio di questi gateway e le relative connessioni è fondamentale tooensuring comunicazione non viene interrotta.</span><span class="sxs-lookup"><span data-stu-id="fe431-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="fe431-106">Watcher di rete fornisce hello funzionalità tootroubleshoot gateway di rete virtuale e le connessioni.</span><span class="sxs-lookup"><span data-stu-id="fe431-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="fe431-107">Questo può essere chiamato tramite il portale di hello, PowerShell, CLI o API REST.</span><span class="sxs-lookup"><span data-stu-id="fe431-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="fe431-108">Quando viene chiamato, Watcher di rete individua integrità hello di gateway di rete virtuale hello o connessione e risultati appropriati hello restituito.</span><span class="sxs-lookup"><span data-stu-id="fe431-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="fe431-109">Questa richiesta è una transazione con esecuzione prolungata, vengono restituiti risultati hello una volta completata la diagnosi di hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="fe431-111">Risultati</span><span class="sxs-lookup"><span data-stu-id="fe431-111">Results</span></span>

<span data-ttu-id="fe431-112">Hello preliminare risultati assegnano un'immagine complessiva dell'integrità di hello della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="fe431-113">È possibile fornire informazioni più approfondite per le risorse come illustrato nella seguente sezione hello:</span><span class="sxs-lookup"><span data-stu-id="fe431-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="fe431-114">Hello elenco seguente include i valori hello restituiti con hello risolvere API:</span><span class="sxs-lookup"><span data-stu-id="fe431-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="fe431-115">**startTime** -questo valore è ora hello hello risolvere chiamata API avviato.</span><span class="sxs-lookup"><span data-stu-id="fe431-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="fe431-116">**endTime** -questo valore è ora hello quando la risoluzione dei problemi di hello è terminata.</span><span class="sxs-lookup"><span data-stu-id="fe431-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="fe431-117">**code**: questo valore è UnHealthy in caso di singolo errore di diagnosi.</span><span class="sxs-lookup"><span data-stu-id="fe431-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="fe431-118">**risultati** -risultati è una raccolta di risultati restituito nel gateway di rete virtuale di connessione o hello hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="fe431-119">**ID** -questo valore è il tipo di errore hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="fe431-120">**riepilogo** -questo valore è riportato un riepilogo dell'errore hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="fe431-121">**dettagliate** -questo valore fornisce una descrizione dettagliata dell'errore hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="fe431-122">**recommendedActions** -questa proprietà è una raccolta di tootake le azioni consigliate.</span><span class="sxs-lookup"><span data-stu-id="fe431-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="fe431-123">**actionText** -questo valore contiene testo hello che descrive quale tootake di azione.</span><span class="sxs-lookup"><span data-stu-id="fe431-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="fe431-124">**actionUri** -questo valore fornisce hello URI toodocumentation sulla tooact.</span><span class="sxs-lookup"><span data-stu-id="fe431-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="fe431-125">**actionUriText** -questo valore è una breve descrizione di testo dell'azione hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="fe431-126">Hello seguenti tabelle Mostra hello diversi tipi di errore (id in risultati da hello precede elenco) che sono disponibili e, se l'errore hello Crea registri.</span><span class="sxs-lookup"><span data-stu-id="fe431-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="fe431-127">Gateway</span><span class="sxs-lookup"><span data-stu-id="fe431-127">Gateway</span></span>

| <span data-ttu-id="fe431-128">Tipo di errore</span><span class="sxs-lookup"><span data-stu-id="fe431-128">Fault Type</span></span> | <span data-ttu-id="fe431-129">Motivo</span><span class="sxs-lookup"><span data-stu-id="fe431-129">Reason</span></span> | <span data-ttu-id="fe431-130">Log</span><span class="sxs-lookup"><span data-stu-id="fe431-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="fe431-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="fe431-131">NoFault</span></span> | <span data-ttu-id="fe431-132">Non viene rilevato alcun errore.</span><span class="sxs-lookup"><span data-stu-id="fe431-132">When no error is detected.</span></span> |<span data-ttu-id="fe431-133">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-133">Yes</span></span>|
| <span data-ttu-id="fe431-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="fe431-134">GatewayNotFound</span></span> | <span data-ttu-id="fe431-135">Non è possibile trovare il gateway o il gateway non è stato sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="fe431-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="fe431-136">No</span><span class="sxs-lookup"><span data-stu-id="fe431-136">No</span></span>|
| <span data-ttu-id="fe431-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="fe431-137">PlannedMaintenance</span></span> |  <span data-ttu-id="fe431-138">L'istanza del gateway è in fase di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="fe431-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="fe431-139">No</span><span class="sxs-lookup"><span data-stu-id="fe431-139">No</span></span>|
| <span data-ttu-id="fe431-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="fe431-140">UserDrivenUpdate</span></span> | <span data-ttu-id="fe431-141">È in corso l'aggiornamento utente.</span><span class="sxs-lookup"><span data-stu-id="fe431-141">When a user update is in progress.</span></span> <span data-ttu-id="fe431-142">Potrebbe trattarsi di un'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="fe431-142">This could be a resize operation.</span></span> | <span data-ttu-id="fe431-143">No</span><span class="sxs-lookup"><span data-stu-id="fe431-143">No</span></span> |
| <span data-ttu-id="fe431-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="fe431-144">VipUnResponsive</span></span> | <span data-ttu-id="fe431-145">Impossibile raggiungere l'istanza primaria di hello di hello Gateway.</span><span class="sxs-lookup"><span data-stu-id="fe431-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="fe431-146">Ciò accade quando hello probe di integrità non riesce.</span><span class="sxs-lookup"><span data-stu-id="fe431-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="fe431-147">No</span><span class="sxs-lookup"><span data-stu-id="fe431-147">No</span></span> |
| <span data-ttu-id="fe431-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="fe431-148">PlatformInActive</span></span> | <span data-ttu-id="fe431-149">Si verifica un problema con la piattaforma di hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="fe431-150">No</span><span class="sxs-lookup"><span data-stu-id="fe431-150">No</span></span>|
| <span data-ttu-id="fe431-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="fe431-151">ServiceNotRunning</span></span> | <span data-ttu-id="fe431-152">servizio di Hello sottostante non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fe431-152">hello underlying service is not running.</span></span> | <span data-ttu-id="fe431-153">No</span><span class="sxs-lookup"><span data-stu-id="fe431-153">No</span></span>|
| <span data-ttu-id="fe431-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="fe431-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="fe431-155">Nessuna connessione esista nel gateway hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="fe431-156">Questo è solo un avviso.</span><span class="sxs-lookup"><span data-stu-id="fe431-156">This is only a warning.</span></span>| <span data-ttu-id="fe431-157">No</span><span class="sxs-lookup"><span data-stu-id="fe431-157">No</span></span>|
| <span data-ttu-id="fe431-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="fe431-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="fe431-159">Le connessioni non sono connesse.</span><span class="sxs-lookup"><span data-stu-id="fe431-159">Connections are not connected.</span></span> <span data-ttu-id="fe431-160">Questo è solo un avviso.</span><span class="sxs-lookup"><span data-stu-id="fe431-160">This is only a warning.</span></span>| <span data-ttu-id="fe431-161">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-161">Yes</span></span>|
| <span data-ttu-id="fe431-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="fe431-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="fe431-163">utilizzo della CPU Gateway corrente Hello è > 95%.</span><span class="sxs-lookup"><span data-stu-id="fe431-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="fe431-164">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="fe431-165">Connessione</span><span class="sxs-lookup"><span data-stu-id="fe431-165">Connection</span></span>

| <span data-ttu-id="fe431-166">Tipo di errore</span><span class="sxs-lookup"><span data-stu-id="fe431-166">Fault Type</span></span> | <span data-ttu-id="fe431-167">Motivo</span><span class="sxs-lookup"><span data-stu-id="fe431-167">Reason</span></span> | <span data-ttu-id="fe431-168">Log</span><span class="sxs-lookup"><span data-stu-id="fe431-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="fe431-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="fe431-169">NoFault</span></span> | <span data-ttu-id="fe431-170">Non viene rilevato alcun errore.</span><span class="sxs-lookup"><span data-stu-id="fe431-170">When no error is detected.</span></span> |<span data-ttu-id="fe431-171">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-171">Yes</span></span>|
| <span data-ttu-id="fe431-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="fe431-172">GatewayNotFound</span></span> | <span data-ttu-id="fe431-173">Non è possibile trovare il gateway o il gateway non è stato sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="fe431-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="fe431-174">No</span><span class="sxs-lookup"><span data-stu-id="fe431-174">No</span></span>|
| <span data-ttu-id="fe431-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="fe431-175">PlannedMaintenance</span></span> | <span data-ttu-id="fe431-176">L'istanza del gateway è in fase di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="fe431-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="fe431-177">No</span><span class="sxs-lookup"><span data-stu-id="fe431-177">No</span></span>|
| <span data-ttu-id="fe431-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="fe431-178">UserDrivenUpdate</span></span> | <span data-ttu-id="fe431-179">È in corso l'aggiornamento utente.</span><span class="sxs-lookup"><span data-stu-id="fe431-179">When a user update is in progress.</span></span> <span data-ttu-id="fe431-180">Potrebbe trattarsi di un'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="fe431-180">This could be a resize operation.</span></span>  | <span data-ttu-id="fe431-181">No</span><span class="sxs-lookup"><span data-stu-id="fe431-181">No</span></span> |
| <span data-ttu-id="fe431-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="fe431-182">VipUnResponsive</span></span> | <span data-ttu-id="fe431-183">Impossibile raggiungere l'istanza primaria di hello di hello Gateway.</span><span class="sxs-lookup"><span data-stu-id="fe431-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="fe431-184">Verifica quando hello probe di integrità non riesce.</span><span class="sxs-lookup"><span data-stu-id="fe431-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="fe431-185">No</span><span class="sxs-lookup"><span data-stu-id="fe431-185">No</span></span> |
| <span data-ttu-id="fe431-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="fe431-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="fe431-187">La configurazione della connessione non è presente.</span><span class="sxs-lookup"><span data-stu-id="fe431-187">Connection configuration is missing.</span></span> | <span data-ttu-id="fe431-188">No</span><span class="sxs-lookup"><span data-stu-id="fe431-188">No</span></span> |
| <span data-ttu-id="fe431-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="fe431-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="fe431-190">Connessione Hello è contrassegnato come "disconnessa".</span><span class="sxs-lookup"><span data-stu-id="fe431-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="fe431-191">No</span><span class="sxs-lookup"><span data-stu-id="fe431-191">No</span></span>|
| <span data-ttu-id="fe431-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="fe431-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="fe431-193">servizio sottostante Hello non dispone di hello che connessione configurata.</span><span class="sxs-lookup"><span data-stu-id="fe431-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="fe431-194">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-194">Yes</span></span> |
| <span data-ttu-id="fe431-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="fe431-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="fe431-196">Hello servizio sottostante viene contrassegnato come standby.</span><span class="sxs-lookup"><span data-stu-id="fe431-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="fe431-197">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-197">Yes</span></span>|
| <span data-ttu-id="fe431-198">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="fe431-198">Authentication</span></span> | <span data-ttu-id="fe431-199">Mancata corrispondenza della chiave precondivisa.</span><span class="sxs-lookup"><span data-stu-id="fe431-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="fe431-200">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-200">Yes</span></span>|
| <span data-ttu-id="fe431-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="fe431-201">PeerReachability</span></span> | <span data-ttu-id="fe431-202">gateway di Hello peer non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="fe431-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="fe431-203">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-203">Yes</span></span>|
| <span data-ttu-id="fe431-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="fe431-204">IkePolicyMismatch</span></span> | <span data-ttu-id="fe431-205">gateway peer Hello dispone di criteri di IKE che non sono supportati da Azure.</span><span class="sxs-lookup"><span data-stu-id="fe431-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="fe431-206">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-206">Yes</span></span>|
| <span data-ttu-id="fe431-207">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="fe431-207">WfpParse Error</span></span> | <span data-ttu-id="fe431-208">Errore durante l'analisi dei log di piattaforma filtro Windows hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="fe431-209">Sì</span><span class="sxs-lookup"><span data-stu-id="fe431-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="fe431-210">Tipi di gateway supportati</span><span class="sxs-lookup"><span data-stu-id="fe431-210">Supported Gateway types</span></span>

<span data-ttu-id="fe431-211">Hello elenco riportato di seguito viene illustrato il supporto di hello Mostra quali i gateway e le connessioni sono supportate con la risoluzione dei problemi di controllo di rete.</span><span class="sxs-lookup"><span data-stu-id="fe431-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="fe431-212">**Tipi di gateway**</span><span class="sxs-lookup"><span data-stu-id="fe431-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="fe431-213">VPN</span><span class="sxs-lookup"><span data-stu-id="fe431-213">VPN</span></span>      | <span data-ttu-id="fe431-214">Supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-214">Supported</span></span>        |
|<span data-ttu-id="fe431-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fe431-215">ExpressRoute</span></span> | <span data-ttu-id="fe431-216">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-216">Not Supported</span></span> |
|<span data-ttu-id="fe431-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="fe431-217">Hypernet</span></span> | <span data-ttu-id="fe431-218">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-218">Not Supported</span></span>|
|<span data-ttu-id="fe431-219">**Tipi di VPN**</span><span class="sxs-lookup"><span data-stu-id="fe431-219">**VPN types**</span></span> | |
|<span data-ttu-id="fe431-220">Basato su route</span><span class="sxs-lookup"><span data-stu-id="fe431-220">Route Based</span></span> | <span data-ttu-id="fe431-221">Supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-221">Supported</span></span>|
|<span data-ttu-id="fe431-222">Basata su criteri</span><span class="sxs-lookup"><span data-stu-id="fe431-222">Policy Based</span></span> | <span data-ttu-id="fe431-223">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-223">Not Supported</span></span>|
|<span data-ttu-id="fe431-224">**Tipi di connessione**</span><span class="sxs-lookup"><span data-stu-id="fe431-224">**Connection types**</span></span>||
|<span data-ttu-id="fe431-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="fe431-225">IPSec</span></span>| <span data-ttu-id="fe431-226">Supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-226">Supported</span></span>|
|<span data-ttu-id="fe431-227">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="fe431-227">VNet2Vnet</span></span>| <span data-ttu-id="fe431-228">Supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-228">Supported</span></span>|
|<span data-ttu-id="fe431-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="fe431-229">ExpressRoute</span></span>| <span data-ttu-id="fe431-230">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-230">Not Supported</span></span>|
|<span data-ttu-id="fe431-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="fe431-231">Hypernet</span></span>| <span data-ttu-id="fe431-232">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-232">Not Supported</span></span>|
|<span data-ttu-id="fe431-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="fe431-233">VPNClient</span></span>| <span data-ttu-id="fe431-234">Non supportato</span><span class="sxs-lookup"><span data-stu-id="fe431-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="fe431-235">File di log</span><span class="sxs-lookup"><span data-stu-id="fe431-235">Log files</span></span>

<span data-ttu-id="fe431-236">file di log sulla risoluzione dei problemi di Hello risorse vengono archiviati in un account di archiviazione dopo la risoluzione dei problemi di risorse completata.</span><span class="sxs-lookup"><span data-stu-id="fe431-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="fe431-237">Hello immagine seguente mostra contenuto di esempio hello di una chiamata che ha restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="fe431-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![File ZIP][1]

> [!NOTE]
> <span data-ttu-id="fe431-239">In alcuni casi, solo un subset hello di file di log viene scritto toostorage.</span><span class="sxs-lookup"><span data-stu-id="fe431-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="fe431-240">Per istruzioni sul download di file dall'account di archiviazione di azure, consultare troppo[Introduzione all'archiviazione Blob di Azure usando .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="fe431-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="fe431-241">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="fe431-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="fe431-242">Ulteriori informazioni su soluzioni di archiviazione sono reperibile qui in hello seguente collegamento: [Esplora archivi](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="fe431-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="fe431-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="fe431-243">ConnectionStats.txt</span></span>

<span data-ttu-id="fe431-244">Hello **ConnectionStats.txt** file contiene statistiche generali di hello connessione, inclusi i byte in ingresso e in uscita, lo stato di connessione e hello ora hello è stata stabilita una connessione.</span><span class="sxs-lookup"><span data-stu-id="fe431-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="fe431-245">Se hello chiamata toohello risoluzione dei problemi di API restituisce integro, unica hello restituito nel file zip hello è un **ConnectionStats.txt** file.</span><span class="sxs-lookup"><span data-stu-id="fe431-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="fe431-246">contenuto Hello di questo file è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="fe431-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="fe431-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="fe431-247">CPUStats.txt</span></span>

<span data-ttu-id="fe431-248">Hello **CPUStats.txt** file contiene l'utilizzo della CPU e memoria disponibile in fase di hello del test.</span><span class="sxs-lookup"><span data-stu-id="fe431-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="fe431-249">contenuto Hello di questo file è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="fe431-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="fe431-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="fe431-250">IKEErrors.txt</span></span>

<span data-ttu-id="fe431-251">Hello **IKEErrors.txt** file contiene gli eventuali errori di IKE che sono stati trovati durante il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="fe431-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="fe431-252">Hello esempio seguente viene illustrato il contenuto di hello di un file IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="fe431-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="fe431-253">Gli errori potrebbero essere diversi in base al problema hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="fe431-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="fe431-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="fe431-255">Hello **Scrubbed wfpdiag.txt** file di log contiene il log di piattaforma filtro Windows hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="fe431-256">Questo log contiene la registrazione del pacchetto ignorato e degli errori IKE/AuthIP.</span><span class="sxs-lookup"><span data-stu-id="fe431-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="fe431-257">Hello esempio seguente viene illustrato il contenuto di hello del file di Scrubbed wfpdiag.txt hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="fe431-258">In questo esempio, hello la chiave condivisa di una connessione non è corretta come si può notare dalla riga di 3 hello dal basso hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="fe431-259">Hello di esempio seguente è semplicemente un frammento di codice dell'intero log hello, come log hello può risultare lungo in base al problema hello.</span><span class="sxs-lookup"><span data-stu-id="fe431-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="fe431-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="fe431-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="fe431-261">Hello **wfpdiag.txt.sum** file è un registro contenente i buffer hello e gli eventi elaborati.</span><span class="sxs-lookup"><span data-stu-id="fe431-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="fe431-262">Hello esempio seguente è contenuto hello di un file di wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="fe431-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="fe431-263">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fe431-263">Next steps</span></span>

<span data-ttu-id="fe431-264">Informazioni su come gateway VPN toodiagnose e le connessioni tramite hello portale visitando [risoluzione dei problemi Gateway - portale di Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fe431-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
