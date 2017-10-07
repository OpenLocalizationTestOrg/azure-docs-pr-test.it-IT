---
title: errori del Gateway non valido di Gateway applicazione Azure (502) aaaTroubleshoot | Documenti Microsoft
description: Informazioni su come errori tootroubleshoot 502 Gateway applicazione
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="631ff-103">Risoluzione degli errori del gateway non valido nel gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="631ff-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="631ff-104">Informazioni su come errori (502) gateway non valido di tootroubleshoot ricevuto quando si usa il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="631ff-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="631ff-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="631ff-105">Overview</span></span>

<span data-ttu-id="631ff-106">Dopo aver configurato un gateway applicazione, uno degli errori di hello che gli utenti possono incontrare è "Errore del Server: 502 - server Web ha ricevuto una risposta non valida che agisce come gateway o proxy server".</span><span class="sxs-lookup"><span data-stu-id="631ff-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="631ff-107">Questo errore può verificarsi a causa di toohello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="631ff-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="631ff-108">Il [pool back-end del gateway applicazione di Azure non è configurato o è vuoto](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="631ff-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="631ff-109">Nessuna delle macchine virtuali hello o le istanze in [Set di scalabilità della macchina virtuale sono integri](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="631ff-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="631ff-110">Macchine virtuali o le istanze di Set di scalabilità della macchina virtuale back-end sono [non risponde probe di integrità predefinito toohello](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="631ff-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="631ff-111">[Configurazione dei probe di integrità personalizzati](#problems-with-custom-health-probe.md) non valida o inappropriata.</span><span class="sxs-lookup"><span data-stu-id="631ff-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="631ff-112">[Problemi di timeout della richiesta o di connettività](#request-time-out) con le richieste degli utenti.</span><span class="sxs-lookup"><span data-stu-id="631ff-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="631ff-113">BackendAddressPool vuoto</span><span class="sxs-lookup"><span data-stu-id="631ff-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="631ff-114">Causa</span><span class="sxs-lookup"><span data-stu-id="631ff-114">Cause</span></span>

<span data-ttu-id="631ff-115">Se hello Gateway applicazione non dispone di nessuna macchina virtuale o il Set di scalabilità della macchina virtuale è configurato nel pool di indirizzi back-end di hello, grado di instradare le richieste del cliente e genera un errore di gateway non valido.</span><span class="sxs-lookup"><span data-stu-id="631ff-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="631ff-116">Soluzione</span><span class="sxs-lookup"><span data-stu-id="631ff-116">Solution</span></span>

<span data-ttu-id="631ff-117">Verificare che il pool di indirizzi back-end di hello non sia vuoto.</span><span class="sxs-lookup"><span data-stu-id="631ff-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="631ff-118">A tale scopo è possibile usare PowerShell, l'interfaccia della riga di comando o il portale.</span><span class="sxs-lookup"><span data-stu-id="631ff-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="631ff-119">output di Hello dalla precedente cmdlet hello deve contenere i pool di indirizzi back-end non vuoto.</span><span class="sxs-lookup"><span data-stu-id="631ff-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="631ff-120">Di seguito è riportato un esempio in cui vengono restituiti due pool configurati con indirizzi IP o FQDN (nome di dominio completo) per le macchine virtuali back-end.</span><span class="sxs-lookup"><span data-stu-id="631ff-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="631ff-121">stato di hello BackendAddressPool provisioning Hello deve essere 'completato'.</span><span class="sxs-lookup"><span data-stu-id="631ff-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="631ff-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="631ff-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="631ff-123">Istanze non integre in BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="631ff-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="631ff-124">Causa</span><span class="sxs-lookup"><span data-stu-id="631ff-124">Cause</span></span>

<span data-ttu-id="631ff-125">Se tutte le istanze di hello di BackendAddressPool sono integri, Gateway applicazione non avrebbero qualsiasi richiesta utente tooroute back-end.</span><span class="sxs-lookup"><span data-stu-id="631ff-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="631ff-126">Potrebbe anche trattarsi case hello quando le istanze di back-end sono integri, ma non dispone di un'applicazione hello necessario distribuita.</span><span class="sxs-lookup"><span data-stu-id="631ff-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="631ff-127">Soluzione</span><span class="sxs-lookup"><span data-stu-id="631ff-127">Solution</span></span>

<span data-ttu-id="631ff-128">Verificare che le istanze di hello siano integri e un'applicazione hello sia configurata correttamente.</span><span class="sxs-lookup"><span data-stu-id="631ff-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="631ff-129">Controllare se le istanze di back-end hello sono in grado di toorespond tooa ping da un'altra macchina virtuale nella stessa rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="631ff-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="631ff-130">Se configurato con un punto di fine pubblico, assicurarsi che un'applicazione di web browser toohello richiesta è utilizzabile dai servizi.</span><span class="sxs-lookup"><span data-stu-id="631ff-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="631ff-131">Problemi con il probe di integrità predefinito</span><span class="sxs-lookup"><span data-stu-id="631ff-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="631ff-132">Causa</span><span class="sxs-lookup"><span data-stu-id="631ff-132">Cause</span></span>

<span data-ttu-id="631ff-133">502 errori possono anche essere indicative che hello probe di integrità predefinito è tooreach non in grado di macchine virtuali di back-end.</span><span class="sxs-lookup"><span data-stu-id="631ff-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="631ff-134">Quando viene eseguito il provisioning di un'istanza di Gateway applicazione, viene configurato automaticamente un tooeach probe di integrità predefinito BackendAddressPool utilizzando le proprietà di hello BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="631ff-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="631ff-135">Input dell'utente è obbligatorio tooset questo probe.</span><span class="sxs-lookup"><span data-stu-id="631ff-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="631ff-136">In particolare, quando viene configurata una regola di bilanciamento del carico, viene creata un'associazione tra BackendHttpSetting e BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="631ff-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="631ff-137">Un probe predefinito viene configurato per ognuna di queste associazioni e un'istanza di integrità periodici controllo connessione tooeach in hello BackendAddressPool hello porta specificata nell'elemento BackendHttpSetting hello avvia di Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="631ff-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="631ff-138">Nella tabella seguente sono elencati i valori di hello associati probe di integrità hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="631ff-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="631ff-139">Proprietà probe</span><span class="sxs-lookup"><span data-stu-id="631ff-139">Probe property</span></span> | <span data-ttu-id="631ff-140">Valore</span><span class="sxs-lookup"><span data-stu-id="631ff-140">Value</span></span> | <span data-ttu-id="631ff-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="631ff-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="631ff-142">URL probe</span><span class="sxs-lookup"><span data-stu-id="631ff-142">Probe URL</span></span> |<span data-ttu-id="631ff-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="631ff-143">http://127.0.0.1/</span></span> |<span data-ttu-id="631ff-144">Percorso URL</span><span class="sxs-lookup"><span data-stu-id="631ff-144">URL path</span></span> |
| <span data-ttu-id="631ff-145">Interval</span><span class="sxs-lookup"><span data-stu-id="631ff-145">Interval</span></span> |<span data-ttu-id="631ff-146">30</span><span class="sxs-lookup"><span data-stu-id="631ff-146">30</span></span> |<span data-ttu-id="631ff-147">Intervallo di probe in secondi</span><span class="sxs-lookup"><span data-stu-id="631ff-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="631ff-148">Timeout</span><span class="sxs-lookup"><span data-stu-id="631ff-148">Time-out</span></span> |<span data-ttu-id="631ff-149">30</span><span class="sxs-lookup"><span data-stu-id="631ff-149">30</span></span> |<span data-ttu-id="631ff-150">Timeout di probe in secondi</span><span class="sxs-lookup"><span data-stu-id="631ff-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="631ff-151">Soglia non integra</span><span class="sxs-lookup"><span data-stu-id="631ff-151">Unhealthy threshold</span></span> |<span data-ttu-id="631ff-152">3</span><span class="sxs-lookup"><span data-stu-id="631ff-152">3</span></span> |<span data-ttu-id="631ff-153">Numero di tentativi di probe.</span><span class="sxs-lookup"><span data-stu-id="631ff-153">Probe retry count.</span></span> <span data-ttu-id="631ff-154">server di back-end Hello è contrassegnato come inattivo dopo il conteggio degli errori di probe consecutivi hello raggiunge la soglia non integra hello.</span><span class="sxs-lookup"><span data-stu-id="631ff-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="631ff-155">Soluzione</span><span class="sxs-lookup"><span data-stu-id="631ff-155">Solution</span></span>

* <span data-ttu-id="631ff-156">Verificare che sia stato configurato un sito predefinito e che sia in ascolto su 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="631ff-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="631ff-157">Se BackendHttpSetting specifica una porta diversa dalla 80, sito predefinito hello deve essere configurato toolisten su tale porta.</span><span class="sxs-lookup"><span data-stu-id="631ff-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="631ff-158">Hello toohttp://127.0.0.1:port chiamata deve restituire un codice di risultato HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="631ff-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="631ff-159">Questo metodo deve essere restituito nel periodo di timeout di 30 secondi hello.</span><span class="sxs-lookup"><span data-stu-id="631ff-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="631ff-160">Verificare che la porta configurata è aperta e che non esistono regole del firewall o i gruppi di sicurezza rete di Azure, che blocca il traffico in ingresso o in uscita sulla porta hello configurato.</span><span class="sxs-lookup"><span data-stu-id="631ff-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="631ff-161">Se un servizio Cloud o macchine virtuali di Azure classiche è usato con FQDN o indirizzo IP pubblico, assicurarsi di hello corrispondenti [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) viene aperto.</span><span class="sxs-lookup"><span data-stu-id="631ff-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="631ff-162">Se hello VM è configurato con Azure Resource Manager e non è compreso tra reti virtuali in cui viene distribuito il Gateway applicazione, hello [Network Security Group](../virtual-network/virtual-networks-nsg.md) deve essere configurato tooallow accesso hello desiderato porta.</span><span class="sxs-lookup"><span data-stu-id="631ff-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="631ff-163">Problemi con il probe di integrità personalizzato</span><span class="sxs-lookup"><span data-stu-id="631ff-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="631ff-164">Causa</span><span class="sxs-lookup"><span data-stu-id="631ff-164">Cause</span></span>

<span data-ttu-id="631ff-165">Probe di integrità personalizzato consentono una maggiore flessibilità toohello di ricerca predefinite comportamento.</span><span class="sxs-lookup"><span data-stu-id="631ff-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="631ff-166">Quando si utilizzano probe personalizzati, gli utenti possono configurare intervallo probe "hello", l'URL di hello e percorso tootest e quanti tooaccept risposte non riuscito prima di contrassegnare l'istanza del pool back-end di hello come non integro.</span><span class="sxs-lookup"><span data-stu-id="631ff-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="631ff-167">Hello seguenti proprietà aggiuntive viene aggiunte.</span><span class="sxs-lookup"><span data-stu-id="631ff-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="631ff-168">Proprietà probe</span><span class="sxs-lookup"><span data-stu-id="631ff-168">Probe property</span></span> | <span data-ttu-id="631ff-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="631ff-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="631ff-170">Nome</span><span class="sxs-lookup"><span data-stu-id="631ff-170">Name</span></span> |<span data-ttu-id="631ff-171">Nome del probe hello.</span><span class="sxs-lookup"><span data-stu-id="631ff-171">Name of hello probe.</span></span> <span data-ttu-id="631ff-172">Questo nome è di tipo probe toohello toorefer utilizzati nelle impostazioni HTTP back-end.</span><span class="sxs-lookup"><span data-stu-id="631ff-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="631ff-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="631ff-173">Protocol</span></span> |<span data-ttu-id="631ff-174">Protocollo utilizzato probe hello toosend.</span><span class="sxs-lookup"><span data-stu-id="631ff-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="631ff-175">probe Hello hello protocollo definito nelle impostazioni HTTP back-end di hello</span><span class="sxs-lookup"><span data-stu-id="631ff-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="631ff-176">Host</span><span class="sxs-lookup"><span data-stu-id="631ff-176">Host</span></span> |<span data-ttu-id="631ff-177">Probe di hello toosend nome host.</span><span class="sxs-lookup"><span data-stu-id="631ff-177">Host name toosend hello probe.</span></span> <span data-ttu-id="631ff-178">Applicabile solo quando vengono configurati più siti nel gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="631ff-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="631ff-179">Questo nome è diverso dal nome host della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="631ff-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="631ff-180">Path</span><span class="sxs-lookup"><span data-stu-id="631ff-180">Path</span></span> |<span data-ttu-id="631ff-181">Percorso relativo del probe hello.</span><span class="sxs-lookup"><span data-stu-id="631ff-181">Relative path of hello probe.</span></span> <span data-ttu-id="631ff-182">path valido Hello inizia con '/'.</span><span class="sxs-lookup"><span data-stu-id="631ff-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="631ff-183">probe Hello viene inviato troppo\<protocollo\>://\<host\>:\<porta\>\<percorso\></span><span class="sxs-lookup"><span data-stu-id="631ff-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="631ff-184">Interval</span><span class="sxs-lookup"><span data-stu-id="631ff-184">Interval</span></span> |<span data-ttu-id="631ff-185">Intervallo di probe in secondi.</span><span class="sxs-lookup"><span data-stu-id="631ff-185">Probe interval in seconds.</span></span> <span data-ttu-id="631ff-186">Questo è l'intervallo di tempo hello tra due probe consecutivi.</span><span class="sxs-lookup"><span data-stu-id="631ff-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="631ff-187">Timeout</span><span class="sxs-lookup"><span data-stu-id="631ff-187">Time-out</span></span> |<span data-ttu-id="631ff-188">Timeout del probe in secondi.</span><span class="sxs-lookup"><span data-stu-id="631ff-188">Probe time-out in seconds.</span></span> <span data-ttu-id="631ff-189">Se una risposta valida non viene ricevuta entro questo periodo di timeout, probe hello è contrassegnato come non riuscito.</span><span class="sxs-lookup"><span data-stu-id="631ff-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="631ff-190">Soglia non integra</span><span class="sxs-lookup"><span data-stu-id="631ff-190">Unhealthy threshold</span></span> |<span data-ttu-id="631ff-191">Numero di tentativi di probe.</span><span class="sxs-lookup"><span data-stu-id="631ff-191">Probe retry count.</span></span> <span data-ttu-id="631ff-192">server di back-end Hello è contrassegnato come inattivo dopo il conteggio degli errori di probe consecutivi hello raggiunge la soglia non integra hello.</span><span class="sxs-lookup"><span data-stu-id="631ff-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="631ff-193">Soluzione</span><span class="sxs-lookup"><span data-stu-id="631ff-193">Solution</span></span>

<span data-ttu-id="631ff-194">Convalidare tale hello che probe di integrità personalizzato sia configurato correttamente come hello tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="631ff-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="631ff-195">Inoltre, toohello precedente risoluzione dei problemi, anche verificare hello segue:</span><span class="sxs-lookup"><span data-stu-id="631ff-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="631ff-196">Verificare che probe hello sia specificato correttamente in base alle hello [Guida](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="631ff-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="631ff-197">Se il Gateway applicazione è configurato per un singolo sito, da hello predefinito Host nome deve essere specificato come '127.0.0.1', se non diversamente configurato in probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="631ff-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="631ff-198">Verificare che una chiamata toohttp: / /\<host\>:\<porta\>\<percorso\> restituisce un codice di risultato HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="631ff-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="631ff-199">Verificare che siano all'interno di intervalli accettabili hello intervallo, timeout e UnhealtyThreshold.</span><span class="sxs-lookup"><span data-stu-id="631ff-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="631ff-200">Se tramite HTTPS probe, assicurarsi che il server back-end hello non richiede SNI tramite la configurazione di un certificato di fallback sul server back-end di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="631ff-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="631ff-201">Verificare che siano all'interno di intervalli accettabili hello intervallo, timeout e UnhealtyThreshold.</span><span class="sxs-lookup"><span data-stu-id="631ff-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="631ff-202">Timeout della richiesta</span><span class="sxs-lookup"><span data-stu-id="631ff-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="631ff-203">Causa</span><span class="sxs-lookup"><span data-stu-id="631ff-203">Cause</span></span>

<span data-ttu-id="631ff-204">Quando viene ricevuta una richiesta dell'utente, Gateway applicazione applica hello configurata regole toohello richiesta e lo indirizza tooa istanza del pool di back-end.</span><span class="sxs-lookup"><span data-stu-id="631ff-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="631ff-205">È in attesa per un intervallo di tempo per una risposta dall'istanza di back-end hello configurabile.</span><span class="sxs-lookup"><span data-stu-id="631ff-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="631ff-206">Per impostazione predefinita, l'intervallo è impostato su **30 secondi**.</span><span class="sxs-lookup"><span data-stu-id="631ff-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="631ff-207">Se il gateway applicazione non riceve una risposta dall'applicazione back-end in questo intervallo, alla richiesta dell'utente viene assegnato un errore 502.</span><span class="sxs-lookup"><span data-stu-id="631ff-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="631ff-208">Soluzione</span><span class="sxs-lookup"><span data-stu-id="631ff-208">Solution</span></span>

<span data-ttu-id="631ff-209">Gateway applicazione consente agli utenti tooconfigure questa impostazione tramite BackendHttpSetting, che può essere quindi applicati toodifferent pool.</span><span class="sxs-lookup"><span data-stu-id="631ff-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="631ff-210">I diversi pool back-end possono avere BackendHttpSetting differenti e quindi una diversa configurazione del timeout della richiesta.</span><span class="sxs-lookup"><span data-stu-id="631ff-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="631ff-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="631ff-211">Next steps</span></span>

<span data-ttu-id="631ff-212">Se hello passaggi precedenti non risolvono il problema di hello, aprire un [ticket di supporto](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="631ff-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

