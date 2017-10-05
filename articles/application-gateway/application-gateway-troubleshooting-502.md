---
title: Risolvere gli errori di gateway non valido (502) nel gateway applicazione di Azure | Microsoft Docs
description: Informazioni su come risolvere gli errori 502 del gateway applicazione
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
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="09c09-103">Risoluzione degli errori del gateway non valido nel gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="09c09-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="09c09-104">Informazioni su come risolvere gli errori di gateway non valido (502) ricevuti durante l'uso di un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="09c09-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="09c09-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="09c09-105">Overview</span></span>

<span data-ttu-id="09c09-106">Dopo aver configurato un gateway applicazione, uno degli errori che gli utenti possono riscontrare è "Errore del server: 502 - Risposta non valida ricevuta dal server Web in funzione come server proxy o gateway".</span><span class="sxs-lookup"><span data-stu-id="09c09-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="09c09-107">Questo errore può verificarsi a causa dei principali motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="09c09-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="09c09-108">Il [pool back-end del gateway applicazione di Azure non è configurato o è vuoto](#empty-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="09c09-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="09c09-109">Nessuna delle macchine virtuali o istanze nel [set di scalabilità di macchine virtuali è integra](#unhealthy-instances-in-backendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="09c09-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="09c09-110">Le macchine virtuali o le istanze back-end del set di scalabilità di macchine virtuali [non rispondono al probe di integrità predefinito](#problems-with-default-health-probe.md).</span><span class="sxs-lookup"><span data-stu-id="09c09-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="09c09-111">[Configurazione dei probe di integrità personalizzati](#problems-with-custom-health-probe.md) non valida o inappropriata.</span><span class="sxs-lookup"><span data-stu-id="09c09-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="09c09-112">[Problemi di timeout della richiesta o di connettività](#request-time-out) con le richieste degli utenti.</span><span class="sxs-lookup"><span data-stu-id="09c09-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="09c09-113">BackendAddressPool vuoto</span><span class="sxs-lookup"><span data-stu-id="09c09-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="09c09-114">Causa</span><span class="sxs-lookup"><span data-stu-id="09c09-114">Cause</span></span>

<span data-ttu-id="09c09-115">Se nel pool di indirizzi back-end non sono presenti VM o set di scalabilità di macchine virtuali configurati, il gateway applicazione non può instradare le richieste del cliente e genera un errore di gateway non valido.</span><span class="sxs-lookup"><span data-stu-id="09c09-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="09c09-116">Soluzione</span><span class="sxs-lookup"><span data-stu-id="09c09-116">Solution</span></span>

<span data-ttu-id="09c09-117">Verificare che il pool di indirizzi back-end non sia vuoto.</span><span class="sxs-lookup"><span data-stu-id="09c09-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="09c09-118">A tale scopo è possibile usare PowerShell, l'interfaccia della riga di comando o il portale.</span><span class="sxs-lookup"><span data-stu-id="09c09-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="09c09-119">L'output del cmdlet precedente dovrebbe contenere un pool di indirizzi back-end non vuoto.</span><span class="sxs-lookup"><span data-stu-id="09c09-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="09c09-120">Di seguito è riportato un esempio in cui vengono restituiti due pool configurati con indirizzi IP o FQDN (nome di dominio completo) per le macchine virtuali back-end.</span><span class="sxs-lookup"><span data-stu-id="09c09-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="09c09-121">Lo stato del provisioning di BackendAddressPool deve essere "Succeeded".</span><span class="sxs-lookup"><span data-stu-id="09c09-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="09c09-122">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="09c09-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="09c09-123">Istanze non integre in BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="09c09-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="09c09-124">Causa</span><span class="sxs-lookup"><span data-stu-id="09c09-124">Cause</span></span>

<span data-ttu-id="09c09-125">Se tutte le istanze di BackendAddressPool non sono integre, il gateway applicazione non avrà back-end a cui instradare la richiesta dell'utente.</span><span class="sxs-lookup"><span data-stu-id="09c09-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="09c09-126">Questo potrebbe anche verificarsi quando le istanze back-end sono integre ma non è stata distribuita l'applicazione necessaria.</span><span class="sxs-lookup"><span data-stu-id="09c09-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="09c09-127">Soluzione</span><span class="sxs-lookup"><span data-stu-id="09c09-127">Solution</span></span>

<span data-ttu-id="09c09-128">Verificare che le istanze siano integre e che l'applicazione sia configurata correttamente.</span><span class="sxs-lookup"><span data-stu-id="09c09-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="09c09-129">Controllare se le istanze back-end riescono a rispondere a un ping da un'altra VM nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="09c09-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="09c09-130">Se configurato con un endpoint pubblico, verificare che sia valida la richiesta del browser per l'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="09c09-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="09c09-131">Problemi con il probe di integrità predefinito</span><span class="sxs-lookup"><span data-stu-id="09c09-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="09c09-132">Causa</span><span class="sxs-lookup"><span data-stu-id="09c09-132">Cause</span></span>

<span data-ttu-id="09c09-133">Gli errori 502 possono anche indicare frequentemente che il probe di integrità predefinito non riesce a raggiungere le VM back-end.</span><span class="sxs-lookup"><span data-stu-id="09c09-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="09c09-134">Quando viene eseguito il provisioning di un'istanza del gateway applicazione, viene automaticamente configurato il probe di integrità predefinito per ogni BackendAddressPool tramite le proprietà del BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="09c09-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="09c09-135">Per impostare il probe non è necessaria alcuna azione da parte dell'utente.</span><span class="sxs-lookup"><span data-stu-id="09c09-135">No user input is required to set this probe.</span></span> <span data-ttu-id="09c09-136">In particolare, quando viene configurata una regola di bilanciamento del carico, viene creata un'associazione tra BackendHttpSetting e BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="09c09-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="09c09-137">Il probe predefinito viene configurato per ognuna di queste associazioni e il gateway applicazione avvia una connessione di controllo di integrità periodica su ogni istanza nel BackendAddressPool, sulla porta specificata nell'elemento BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="09c09-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="09c09-138">La tabella seguente elenca i valori associati al probe di integrità predefinito.</span><span class="sxs-lookup"><span data-stu-id="09c09-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="09c09-139">Proprietà probe</span><span class="sxs-lookup"><span data-stu-id="09c09-139">Probe property</span></span> | <span data-ttu-id="09c09-140">Valore</span><span class="sxs-lookup"><span data-stu-id="09c09-140">Value</span></span> | <span data-ttu-id="09c09-141">Descrizione</span><span class="sxs-lookup"><span data-stu-id="09c09-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="09c09-142">URL probe</span><span class="sxs-lookup"><span data-stu-id="09c09-142">Probe URL</span></span> |<span data-ttu-id="09c09-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="09c09-143">http://127.0.0.1/</span></span> |<span data-ttu-id="09c09-144">Percorso URL</span><span class="sxs-lookup"><span data-stu-id="09c09-144">URL path</span></span> |
| <span data-ttu-id="09c09-145">Interval</span><span class="sxs-lookup"><span data-stu-id="09c09-145">Interval</span></span> |<span data-ttu-id="09c09-146">30</span><span class="sxs-lookup"><span data-stu-id="09c09-146">30</span></span> |<span data-ttu-id="09c09-147">Intervallo di probe in secondi</span><span class="sxs-lookup"><span data-stu-id="09c09-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="09c09-148">Timeout</span><span class="sxs-lookup"><span data-stu-id="09c09-148">Time-out</span></span> |<span data-ttu-id="09c09-149">30</span><span class="sxs-lookup"><span data-stu-id="09c09-149">30</span></span> |<span data-ttu-id="09c09-150">Timeout di probe in secondi</span><span class="sxs-lookup"><span data-stu-id="09c09-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="09c09-151">Soglia non integra</span><span class="sxs-lookup"><span data-stu-id="09c09-151">Unhealthy threshold</span></span> |<span data-ttu-id="09c09-152">3</span><span class="sxs-lookup"><span data-stu-id="09c09-152">3</span></span> |<span data-ttu-id="09c09-153">Numero di tentativi di probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-153">Probe retry count.</span></span> <span data-ttu-id="09c09-154">Il server back-end viene contrassegnato come inattivo dopo che il numero di errori di probe consecutivi ha raggiunto una soglia non integra.</span><span class="sxs-lookup"><span data-stu-id="09c09-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="09c09-155">Soluzione</span><span class="sxs-lookup"><span data-stu-id="09c09-155">Solution</span></span>

* <span data-ttu-id="09c09-156">Verificare che sia stato configurato un sito predefinito e che sia in ascolto su 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="09c09-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="09c09-157">Se BackendHttpSetting specifica una porta diversa da 80, il sito predefinito deve essere configurato per ascoltare tale porta.</span><span class="sxs-lookup"><span data-stu-id="09c09-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="09c09-158">La chiamata a http://127.0.0.1:port deve restituire un codice risultato HTTP di 200.</span><span class="sxs-lookup"><span data-stu-id="09c09-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="09c09-159">Questo valore deve essere restituito entro il periodo di timeout di 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="09c09-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="09c09-160">Verificare che la porta configurata sia aperta e che non esistano regole del firewall o gruppi di sicurezza di rete di Azure che bloccano il traffico in ingresso o in uscita sulla porta configurata.</span><span class="sxs-lookup"><span data-stu-id="09c09-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="09c09-161">Se le macchine virtuali classiche di Azure o il servizio cloud vengono usati con indirizzi FQDN o IP pubblici, verificare che l' [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) corrispondente sia aperto.</span><span class="sxs-lookup"><span data-stu-id="09c09-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="09c09-162">Se la macchina virtuale è stata configurata tramite Azure Resource Manager e si trova all'esterno della rete virtuale in cui è distribuito il gateway applicazione, è necessario configurare un [Gruppo di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) per consentire l'accesso alla porta desiderata.</span><span class="sxs-lookup"><span data-stu-id="09c09-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="09c09-163">Problemi con il probe di integrità personalizzato</span><span class="sxs-lookup"><span data-stu-id="09c09-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="09c09-164">Causa</span><span class="sxs-lookup"><span data-stu-id="09c09-164">Cause</span></span>

<span data-ttu-id="09c09-165">Il probe di integrità personalizzato consente una maggiore flessibilità per la ricerca di comportamenti predefiniti del probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="09c09-166">Quando si usano probe personalizzati, gli utenti possono configurare l'intervallo di probe, l'URL e il percorso da testare, nonché il numero di risposte non riuscite da accettare prima di contrassegnare l'istanza del pool back-end come non integra.</span><span class="sxs-lookup"><span data-stu-id="09c09-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="09c09-167">Vengono aggiunte le seguenti proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="09c09-167">The following additional properties are added.</span></span>

| <span data-ttu-id="09c09-168">Proprietà probe</span><span class="sxs-lookup"><span data-stu-id="09c09-168">Probe property</span></span> | <span data-ttu-id="09c09-169">Descrizione</span><span class="sxs-lookup"><span data-stu-id="09c09-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09c09-170">Nome</span><span class="sxs-lookup"><span data-stu-id="09c09-170">Name</span></span> |<span data-ttu-id="09c09-171">Nome del probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-171">Name of the probe.</span></span> <span data-ttu-id="09c09-172">Questo nome viene usato per fare riferimento al probe nelle impostazioni HTTP back-end</span><span class="sxs-lookup"><span data-stu-id="09c09-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="09c09-173">Protocol</span><span class="sxs-lookup"><span data-stu-id="09c09-173">Protocol</span></span> |<span data-ttu-id="09c09-174">Protocollo usato per inviare il probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-174">Protocol used to send the probe.</span></span> <span data-ttu-id="09c09-175">Il probe usa il protocollo definito nelle impostazioni HTTP del back-end.</span><span class="sxs-lookup"><span data-stu-id="09c09-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="09c09-176">Host</span><span class="sxs-lookup"><span data-stu-id="09c09-176">Host</span></span> |<span data-ttu-id="09c09-177">Nome host per inviare il probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-177">Host name to send the probe.</span></span> <span data-ttu-id="09c09-178">Applicabile solo quando vengono configurati più siti nel gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="09c09-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="09c09-179">Questo nome è diverso dal nome host della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="09c09-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="09c09-180">Path</span><span class="sxs-lookup"><span data-stu-id="09c09-180">Path</span></span> |<span data-ttu-id="09c09-181">Percorso relativo del probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-181">Relative path of the probe.</span></span> <span data-ttu-id="09c09-182">Il percorso valido inizia da "/".</span><span class="sxs-lookup"><span data-stu-id="09c09-182">The valid path starts from '/'.</span></span> <span data-ttu-id="09c09-183">Il probe viene inviato a \<protocollo\>://\<host\>:\<porta\>\<percorso\></span><span class="sxs-lookup"><span data-stu-id="09c09-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="09c09-184">Interval</span><span class="sxs-lookup"><span data-stu-id="09c09-184">Interval</span></span> |<span data-ttu-id="09c09-185">Intervallo di probe in secondi.</span><span class="sxs-lookup"><span data-stu-id="09c09-185">Probe interval in seconds.</span></span> <span data-ttu-id="09c09-186">Si tratta dell'intervallo di tempo tra due probe consecutivi.</span><span class="sxs-lookup"><span data-stu-id="09c09-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="09c09-187">Timeout</span><span class="sxs-lookup"><span data-stu-id="09c09-187">Time-out</span></span> |<span data-ttu-id="09c09-188">Timeout del probe in secondi.</span><span class="sxs-lookup"><span data-stu-id="09c09-188">Probe time-out in seconds.</span></span> <span data-ttu-id="09c09-189">Se non viene ricevuta una risposta valida entro questo periodo di timeout, il probe viene contrassegnato come non riuscito.</span><span class="sxs-lookup"><span data-stu-id="09c09-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="09c09-190">Soglia non integra</span><span class="sxs-lookup"><span data-stu-id="09c09-190">Unhealthy threshold</span></span> |<span data-ttu-id="09c09-191">Numero di tentativi di probe.</span><span class="sxs-lookup"><span data-stu-id="09c09-191">Probe retry count.</span></span> <span data-ttu-id="09c09-192">Il server back-end viene contrassegnato come inattivo dopo che il numero di errori di probe consecutivi ha raggiunto una soglia non integra.</span><span class="sxs-lookup"><span data-stu-id="09c09-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="09c09-193">Soluzione</span><span class="sxs-lookup"><span data-stu-id="09c09-193">Solution</span></span>

<span data-ttu-id="09c09-194">Verificare che il probe di integrità personalizzato sia configurato correttamente in base alla tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="09c09-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="09c09-195">In aggiunta alle procedure di risoluzione dei problemi precedenti, verificare anche quanto segue:</span><span class="sxs-lookup"><span data-stu-id="09c09-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="09c09-196">Verificare che il probe sia specificato correttamente secondo le istruzioni della [guida](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="09c09-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="09c09-197">Se il gateway applicazione è configurato per un singolo sito, per impostazione predefinita il nome dell'host deve essere specificato come "127.0.0.1", se non diversamente configurato nel probe personalizzato.</span><span class="sxs-lookup"><span data-stu-id="09c09-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="09c09-198">Verificare che la chiamata a http://\<host\>:\<porta\>\<percorso\> restituisca un codice risultato HTTP di 200.</span><span class="sxs-lookup"><span data-stu-id="09c09-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="09c09-199">Assicurarsi che Intervallo, Timeout e Soglia non integra siano compresi in intervalli accettabili.</span><span class="sxs-lookup"><span data-stu-id="09c09-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="09c09-200">Se si usa un probe HTTPS, assicurarsi che il server back-end non richieda SNI configurando un certificato di fallback nello stesso server back-end.</span><span class="sxs-lookup"><span data-stu-id="09c09-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="09c09-201">Assicurarsi che i valori di Interval, Time-out e UnhealtyThreshold siano compresi in intervalli accettabili.</span><span class="sxs-lookup"><span data-stu-id="09c09-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="09c09-202">Timeout della richiesta</span><span class="sxs-lookup"><span data-stu-id="09c09-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="09c09-203">Causa</span><span class="sxs-lookup"><span data-stu-id="09c09-203">Cause</span></span>

<span data-ttu-id="09c09-204">Quando viene ricevuta una richiesta dell'utente, il gateway applicazione applica le regole configurate alla richiesta e la instrada a un'istanza del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="09c09-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="09c09-205">Attende quindi la risposta dall'istanza back-end per un intervallo di tempo configurabile.</span><span class="sxs-lookup"><span data-stu-id="09c09-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="09c09-206">Per impostazione predefinita, l'intervallo è impostato su **30 secondi**.</span><span class="sxs-lookup"><span data-stu-id="09c09-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="09c09-207">Se il gateway applicazione non riceve una risposta dall'applicazione back-end in questo intervallo, alla richiesta dell'utente viene assegnato un errore 502.</span><span class="sxs-lookup"><span data-stu-id="09c09-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="09c09-208">Soluzione</span><span class="sxs-lookup"><span data-stu-id="09c09-208">Solution</span></span>

<span data-ttu-id="09c09-209">Il gateway applicazione consente agli utenti di configurare questa impostazione tramite BackendHttpSetting, applicabile a pool diversi.</span><span class="sxs-lookup"><span data-stu-id="09c09-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="09c09-210">I diversi pool back-end possono avere BackendHttpSetting differenti e quindi una diversa configurazione del timeout della richiesta.</span><span class="sxs-lookup"><span data-stu-id="09c09-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="09c09-211">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09c09-211">Next steps</span></span>

<span data-ttu-id="09c09-212">Se i passaggi precedenti non risolvono il problema, aprire un [ticket di supporto](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="09c09-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

