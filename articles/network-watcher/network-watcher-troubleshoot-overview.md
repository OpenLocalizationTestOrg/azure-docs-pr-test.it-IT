---
title: Introduzione alla risoluzione dei problemi delle risorse in Azure Network Watcher | Microsoft Docs
description: "Questa pagina fornisce una panoramica delle funzionalità di risoluzione dei problemi delle risorse di Network Watcher"
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="6b83d-103">Introduzione alla risoluzione dei problemi delle risorse in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6b83d-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="6b83d-104">I gateway di rete virtuale forniscono la connettività tra le risorse locali e altre reti virtuali in Azure.</span><span class="sxs-lookup"><span data-stu-id="6b83d-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="6b83d-105">Il monitoraggio di questi gateway e delle rispettive connessioni è essenziale per assicurare che le comunicazioni non siano interrotte.</span><span class="sxs-lookup"><span data-stu-id="6b83d-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="6b83d-106">Network Watcher consente di risolvere i problemi dei gateway di rete virtuale e delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="6b83d-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="6b83d-107">Questo può essere chiamato dal portale, da PowerShell, dall'interfaccia della riga di comando o dall'API REST.</span><span class="sxs-lookup"><span data-stu-id="6b83d-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="6b83d-108">Quando viene chiamato, Network Watcher esegue la diagnostica dell'integrità del gateway di rete virtuale o della connessione e restituisce i risultati appropriati.</span><span class="sxs-lookup"><span data-stu-id="6b83d-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="6b83d-109">Questa richiesta è una transazione a esecuzione prolungata e i risultati vengono restituiti al termine della diagnosi.</span><span class="sxs-lookup"><span data-stu-id="6b83d-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="6b83d-111">Risultati</span><span class="sxs-lookup"><span data-stu-id="6b83d-111">Results</span></span>

<span data-ttu-id="6b83d-112">I risultati preliminari restituiti offrono un quadro complessivo dell'integrità della risorsa.</span><span class="sxs-lookup"><span data-stu-id="6b83d-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="6b83d-113">È possibile ottenere informazioni più approfondite per le risorse, come illustrato nella sezione seguente:</span><span class="sxs-lookup"><span data-stu-id="6b83d-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="6b83d-114">L'elenco seguente include i valori restituiti con l'API di risoluzione dei problemi:</span><span class="sxs-lookup"><span data-stu-id="6b83d-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="6b83d-115">**startTime**: questo valore indica l'ora di inizio della chiamata all'API di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="6b83d-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="6b83d-116">**endTime**: questo valore indica l'ora di fine della risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="6b83d-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="6b83d-117">**code**: questo valore è UnHealthy in caso di singolo errore di diagnosi.</span><span class="sxs-lookup"><span data-stu-id="6b83d-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="6b83d-118">**results**: indica una raccolta di risultati restituiti relativi alla connessione o al gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b83d-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="6b83d-119">**id**: questo valore è il tipo di errore.</span><span class="sxs-lookup"><span data-stu-id="6b83d-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="6b83d-120">**summary**: questo valore è un riepilogo dell'errore.</span><span class="sxs-lookup"><span data-stu-id="6b83d-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="6b83d-121">**detailed**: questo valore fornisce una descrizione dettagliata dell'errore.</span><span class="sxs-lookup"><span data-stu-id="6b83d-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="6b83d-122">**recommendedActions**: questa proprietà è una raccolta di azioni consigliate da eseguire.</span><span class="sxs-lookup"><span data-stu-id="6b83d-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="6b83d-123">**actionText**: questo valore contiene il testo che descrive l'azione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="6b83d-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="6b83d-124">**actionUri**: questo valore fornisce l'URI per la documentazione relativa all'azione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="6b83d-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="6b83d-125">**actionUriText**: questo valore è una breve descrizione del testo dell'azione.</span><span class="sxs-lookup"><span data-stu-id="6b83d-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="6b83d-126">Le tabelle seguenti illustrano i diversi tipi di errore (ID relativi ai risultati dell'elenco precedente) disponibili e indicano se l'errore crea log.</span><span class="sxs-lookup"><span data-stu-id="6b83d-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="6b83d-127">Gateway</span><span class="sxs-lookup"><span data-stu-id="6b83d-127">Gateway</span></span>

| <span data-ttu-id="6b83d-128">Tipo di errore</span><span class="sxs-lookup"><span data-stu-id="6b83d-128">Fault Type</span></span> | <span data-ttu-id="6b83d-129">Motivo</span><span class="sxs-lookup"><span data-stu-id="6b83d-129">Reason</span></span> | <span data-ttu-id="6b83d-130">Log</span><span class="sxs-lookup"><span data-stu-id="6b83d-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="6b83d-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="6b83d-131">NoFault</span></span> | <span data-ttu-id="6b83d-132">Non viene rilevato alcun errore.</span><span class="sxs-lookup"><span data-stu-id="6b83d-132">When no error is detected.</span></span> |<span data-ttu-id="6b83d-133">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-133">Yes</span></span>|
| <span data-ttu-id="6b83d-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="6b83d-134">GatewayNotFound</span></span> | <span data-ttu-id="6b83d-135">Non è possibile trovare il gateway o il gateway non è stato sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="6b83d-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="6b83d-136">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-136">No</span></span>|
| <span data-ttu-id="6b83d-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="6b83d-137">PlannedMaintenance</span></span> |  <span data-ttu-id="6b83d-138">L'istanza del gateway è in fase di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="6b83d-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="6b83d-139">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-139">No</span></span>|
| <span data-ttu-id="6b83d-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="6b83d-140">UserDrivenUpdate</span></span> | <span data-ttu-id="6b83d-141">È in corso l'aggiornamento utente.</span><span class="sxs-lookup"><span data-stu-id="6b83d-141">When a user update is in progress.</span></span> <span data-ttu-id="6b83d-142">Potrebbe trattarsi di un'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6b83d-142">This could be a resize operation.</span></span> | <span data-ttu-id="6b83d-143">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-143">No</span></span> |
| <span data-ttu-id="6b83d-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="6b83d-144">VipUnResponsive</span></span> | <span data-ttu-id="6b83d-145">Non è possibile raggiungere l'istanza primaria del gateway.</span><span class="sxs-lookup"><span data-stu-id="6b83d-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="6b83d-146">Ciò si verifica in caso di errore del probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="6b83d-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="6b83d-147">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-147">No</span></span> |
| <span data-ttu-id="6b83d-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="6b83d-148">PlatformInActive</span></span> | <span data-ttu-id="6b83d-149">Si è verificato un errore con la piattaforma.</span><span class="sxs-lookup"><span data-stu-id="6b83d-149">There is an issue with the platform.</span></span> | <span data-ttu-id="6b83d-150">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-150">No</span></span>|
| <span data-ttu-id="6b83d-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="6b83d-151">ServiceNotRunning</span></span> | <span data-ttu-id="6b83d-152">Il servizio sottostante non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6b83d-152">The underlying service is not running.</span></span> | <span data-ttu-id="6b83d-153">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-153">No</span></span>|
| <span data-ttu-id="6b83d-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="6b83d-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="6b83d-155">Non esistono connessioni sul gateway.</span><span class="sxs-lookup"><span data-stu-id="6b83d-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="6b83d-156">Questo è solo un avviso.</span><span class="sxs-lookup"><span data-stu-id="6b83d-156">This is only a warning.</span></span>| <span data-ttu-id="6b83d-157">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-157">No</span></span>|
| <span data-ttu-id="6b83d-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="6b83d-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="6b83d-159">Le connessioni non sono connesse.</span><span class="sxs-lookup"><span data-stu-id="6b83d-159">Connections are not connected.</span></span> <span data-ttu-id="6b83d-160">Questo è solo un avviso.</span><span class="sxs-lookup"><span data-stu-id="6b83d-160">This is only a warning.</span></span>| <span data-ttu-id="6b83d-161">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-161">Yes</span></span>|
| <span data-ttu-id="6b83d-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="6b83d-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="6b83d-163">L'utilizzo della CPU del gateway corrente è > 95%.</span><span class="sxs-lookup"><span data-stu-id="6b83d-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="6b83d-164">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="6b83d-165">Connessione</span><span class="sxs-lookup"><span data-stu-id="6b83d-165">Connection</span></span>

| <span data-ttu-id="6b83d-166">Tipo di errore</span><span class="sxs-lookup"><span data-stu-id="6b83d-166">Fault Type</span></span> | <span data-ttu-id="6b83d-167">Motivo</span><span class="sxs-lookup"><span data-stu-id="6b83d-167">Reason</span></span> | <span data-ttu-id="6b83d-168">Log</span><span class="sxs-lookup"><span data-stu-id="6b83d-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="6b83d-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="6b83d-169">NoFault</span></span> | <span data-ttu-id="6b83d-170">Non viene rilevato alcun errore.</span><span class="sxs-lookup"><span data-stu-id="6b83d-170">When no error is detected.</span></span> |<span data-ttu-id="6b83d-171">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-171">Yes</span></span>|
| <span data-ttu-id="6b83d-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="6b83d-172">GatewayNotFound</span></span> | <span data-ttu-id="6b83d-173">Non è possibile trovare il gateway o il gateway non è stato sottoposto a provisioning.</span><span class="sxs-lookup"><span data-stu-id="6b83d-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="6b83d-174">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-174">No</span></span>|
| <span data-ttu-id="6b83d-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="6b83d-175">PlannedMaintenance</span></span> | <span data-ttu-id="6b83d-176">L'istanza del gateway è in fase di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="6b83d-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="6b83d-177">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-177">No</span></span>|
| <span data-ttu-id="6b83d-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="6b83d-178">UserDrivenUpdate</span></span> | <span data-ttu-id="6b83d-179">È in corso l'aggiornamento utente.</span><span class="sxs-lookup"><span data-stu-id="6b83d-179">When a user update is in progress.</span></span> <span data-ttu-id="6b83d-180">Potrebbe trattarsi di un'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6b83d-180">This could be a resize operation.</span></span>  | <span data-ttu-id="6b83d-181">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-181">No</span></span> |
| <span data-ttu-id="6b83d-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="6b83d-182">VipUnResponsive</span></span> | <span data-ttu-id="6b83d-183">Non è possibile raggiungere l'istanza primaria del gateway.</span><span class="sxs-lookup"><span data-stu-id="6b83d-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="6b83d-184">Ciò si verifica in caso di errore del probe di integrità.</span><span class="sxs-lookup"><span data-stu-id="6b83d-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="6b83d-185">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-185">No</span></span> |
| <span data-ttu-id="6b83d-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="6b83d-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="6b83d-187">La configurazione della connessione non è presente.</span><span class="sxs-lookup"><span data-stu-id="6b83d-187">Connection configuration is missing.</span></span> | <span data-ttu-id="6b83d-188">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-188">No</span></span> |
| <span data-ttu-id="6b83d-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="6b83d-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="6b83d-190">La connessione viene contrassegnata come "disconnected".</span><span class="sxs-lookup"><span data-stu-id="6b83d-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="6b83d-191">No</span><span class="sxs-lookup"><span data-stu-id="6b83d-191">No</span></span>|
| <span data-ttu-id="6b83d-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="6b83d-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="6b83d-193">La connessione per il servizio sottostante non è stata configurata.</span><span class="sxs-lookup"><span data-stu-id="6b83d-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="6b83d-194">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-194">Yes</span></span> |
| <span data-ttu-id="6b83d-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="6b83d-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="6b83d-196">Il servizio sottostante viene contrassegnato come "standby".</span><span class="sxs-lookup"><span data-stu-id="6b83d-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="6b83d-197">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-197">Yes</span></span>|
| <span data-ttu-id="6b83d-198">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="6b83d-198">Authentication</span></span> | <span data-ttu-id="6b83d-199">Mancata corrispondenza della chiave precondivisa.</span><span class="sxs-lookup"><span data-stu-id="6b83d-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="6b83d-200">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-200">Yes</span></span>|
| <span data-ttu-id="6b83d-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="6b83d-201">PeerReachability</span></span> | <span data-ttu-id="6b83d-202">Il gateway peer non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="6b83d-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="6b83d-203">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-203">Yes</span></span>|
| <span data-ttu-id="6b83d-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="6b83d-204">IkePolicyMismatch</span></span> | <span data-ttu-id="6b83d-205">Il gateway peer ha criteri IKE non supportati da Azure.</span><span class="sxs-lookup"><span data-stu-id="6b83d-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="6b83d-206">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-206">Yes</span></span>|
| <span data-ttu-id="6b83d-207">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="6b83d-207">WfpParse Error</span></span> | <span data-ttu-id="6b83d-208">Si è verificato un errore durante l'analisi del log WFP.</span><span class="sxs-lookup"><span data-stu-id="6b83d-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="6b83d-209">Sì</span><span class="sxs-lookup"><span data-stu-id="6b83d-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="6b83d-210">Tipi di gateway supportati</span><span class="sxs-lookup"><span data-stu-id="6b83d-210">Supported Gateway types</span></span>

<span data-ttu-id="6b83d-211">L'elenco seguente mostra i gateway e le connessioni supportate con la risoluzione dei problemi di Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="6b83d-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="6b83d-212">**Tipi di gateway**</span><span class="sxs-lookup"><span data-stu-id="6b83d-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="6b83d-213">VPN</span><span class="sxs-lookup"><span data-stu-id="6b83d-213">VPN</span></span>      | <span data-ttu-id="6b83d-214">Supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-214">Supported</span></span>        |
|<span data-ttu-id="6b83d-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6b83d-215">ExpressRoute</span></span> | <span data-ttu-id="6b83d-216">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-216">Not Supported</span></span> |
|<span data-ttu-id="6b83d-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="6b83d-217">Hypernet</span></span> | <span data-ttu-id="6b83d-218">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-218">Not Supported</span></span>|
|<span data-ttu-id="6b83d-219">**Tipi di VPN**</span><span class="sxs-lookup"><span data-stu-id="6b83d-219">**VPN types**</span></span> | |
|<span data-ttu-id="6b83d-220">Basato su route</span><span class="sxs-lookup"><span data-stu-id="6b83d-220">Route Based</span></span> | <span data-ttu-id="6b83d-221">Supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-221">Supported</span></span>|
|<span data-ttu-id="6b83d-222">Basata su criteri</span><span class="sxs-lookup"><span data-stu-id="6b83d-222">Policy Based</span></span> | <span data-ttu-id="6b83d-223">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-223">Not Supported</span></span>|
|<span data-ttu-id="6b83d-224">**Tipi di connessione**</span><span class="sxs-lookup"><span data-stu-id="6b83d-224">**Connection types**</span></span>||
|<span data-ttu-id="6b83d-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="6b83d-225">IPSec</span></span>| <span data-ttu-id="6b83d-226">Supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-226">Supported</span></span>|
|<span data-ttu-id="6b83d-227">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="6b83d-227">VNet2Vnet</span></span>| <span data-ttu-id="6b83d-228">Supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-228">Supported</span></span>|
|<span data-ttu-id="6b83d-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6b83d-229">ExpressRoute</span></span>| <span data-ttu-id="6b83d-230">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-230">Not Supported</span></span>|
|<span data-ttu-id="6b83d-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="6b83d-231">Hypernet</span></span>| <span data-ttu-id="6b83d-232">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-232">Not Supported</span></span>|
|<span data-ttu-id="6b83d-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="6b83d-233">VPNClient</span></span>| <span data-ttu-id="6b83d-234">Non supportato</span><span class="sxs-lookup"><span data-stu-id="6b83d-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="6b83d-235">File di log</span><span class="sxs-lookup"><span data-stu-id="6b83d-235">Log files</span></span>

<span data-ttu-id="6b83d-236">I file di log della risoluzione dei problemi delle risorse vengono archiviati in un account di archiviazione al termine della risoluzione dei problemi delle risorse.</span><span class="sxs-lookup"><span data-stu-id="6b83d-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="6b83d-237">L'immagine seguente mostra i contenuti di esempio di una chiamata che ha generato un errore.</span><span class="sxs-lookup"><span data-stu-id="6b83d-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![File ZIP][1]

> [!NOTE]
> <span data-ttu-id="6b83d-239">In alcuni casi, solo un sottoinsieme di file di log viene scritto nella risorsa di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6b83d-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="6b83d-240">Per istruzioni sul download di file dall'account di archiviazione di Azure, vedere [Introduzione all'archivio BLOB di Azure con .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="6b83d-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="6b83d-241">Un altro strumento che può essere usato è Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="6b83d-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="6b83d-242">Altre informazioni su Storage Explorer sono reperibili facendo clic sul collegamento seguente: [Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6b83d-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="6b83d-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="6b83d-243">ConnectionStats.txt</span></span>

<span data-ttu-id="6b83d-244">Il file **ConnectionStats.txt** contiene lo stato complessivo della connessione, inclusi i byte in ingresso e in uscita e l'ora in cui è stata stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="6b83d-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="6b83d-245">Se la chiamata all'API di risoluzione dei problemi restituisce uno stato integro, l'unico elemento restituito nel file ZIP è un file **ConnectionStats.txt**.</span><span class="sxs-lookup"><span data-stu-id="6b83d-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="6b83d-246">I contenuti di questo file sono simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6b83d-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="6b83d-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="6b83d-247">CPUStats.txt</span></span>

<span data-ttu-id="6b83d-248">Il file **CPUStats.txt** contiene l'utilizzo della CPU e la memoria disponibile in fase di test.</span><span class="sxs-lookup"><span data-stu-id="6b83d-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="6b83d-249">I contenuti di questo file sono simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6b83d-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="6b83d-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="6b83d-250">IKEErrors.txt</span></span>

<span data-ttu-id="6b83d-251">Il file **IKEErrors.txt** contiene eventuali errori IKE trovati durante il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="6b83d-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="6b83d-252">L'esempio seguente mostra i contenuti di un file IKEErrors.txt.</span><span class="sxs-lookup"><span data-stu-id="6b83d-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="6b83d-253">È possibile che gli errori visualizzati siano diversi, in base al problema specifico.</span><span class="sxs-lookup"><span data-stu-id="6b83d-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="6b83d-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="6b83d-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="6b83d-255">Il file di log **Scrubbed-wfpdiag.txt** contiene il log WFP.</span><span class="sxs-lookup"><span data-stu-id="6b83d-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="6b83d-256">Questo log contiene la registrazione del pacchetto ignorato e degli errori IKE/AuthIP.</span><span class="sxs-lookup"><span data-stu-id="6b83d-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="6b83d-257">L'esempio seguente mostra i contenuti del file Scrubbed-wfpdiag.txt.</span><span class="sxs-lookup"><span data-stu-id="6b83d-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="6b83d-258">In questo esempio la chiave condivisa di una connessione non è valida, come illustrato dalla terza riga dal basso.</span><span class="sxs-lookup"><span data-stu-id="6b83d-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="6b83d-259">L'esempio seguente è solo un frammento di codice dell'intero log, ma il log può essere lungo, a seconda del problema specifico.</span><span class="sxs-lookup"><span data-stu-id="6b83d-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="6b83d-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="6b83d-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="6b83d-261">Il file **wfpdiag.txt.sum** è un log che mostra i buffer e gli eventi elaborati.</span><span class="sxs-lookup"><span data-stu-id="6b83d-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="6b83d-262">L'esempio seguente illustra i contenuti di un file wfpdiag.txt.sum.</span><span class="sxs-lookup"><span data-stu-id="6b83d-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="6b83d-263">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b83d-263">Next steps</span></span>

<span data-ttu-id="6b83d-264">Per informazioni sulla diagnosi dei gateway VPN e delle connessioni con il portale, vedere [Risoluzione dei problemi del gateway - Portale di Azure](network-watcher-troubleshoot-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b83d-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
