---
title: aaaAzure Service Fabric inversa diagnostica proxy | Documenti Microsoft
description: Informazioni su come toomonitor e diagnosticare l'elaborazione della richiesta al proxy inverso hello.
services: service-fabric
documentationcenter: .net
author: kavyako
manager: vipulm
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: kavyako
ms.openlocfilehash: 9687b9688dc26ba619cbdfab1b1f49a3035345c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a><span data-ttu-id="e6e3a-103">Monitoraggio e diagnosi l'elaborazione della richiesta al proxy inverso hello</span><span class="sxs-lookup"><span data-stu-id="e6e3a-103">Monitor and diagnose request processing at hello reverse proxy</span></span>

<span data-ttu-id="e6e3a-104">A partire dalla versione di hello 5.7 dell'infrastruttura di servizio, sono disponibili per la raccolta eventi di proxy inverso.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-104">Starting with hello 5.7 release of Service Fabric, reverse proxy events are available for collection.</span></span> <span data-ttu-id="e6e3a-105">Hello eventi sono disponibili in due canali, una con solo gli eventi di errore correlati errore durante l'elaborazione di toorequest proxy inverso hello e secondo canale contenente gli eventi dettagliati con le voci per le richieste con esito positivo e non riuscite.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-105">hello events are available in two channels, one with only error events related toorequest processing failure at hello reverse proxy and second channel containing verbose events with entries for both successful and failed requests.</span></span>

<span data-ttu-id="e6e3a-106">Fare riferimento troppo[raccogliere gli eventi di proxy inverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable raccolta di eventi da questi canali in locale e i cluster di Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-106">Refer too[Collect reverse proxy events](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable collecting events from these channels in local and Azure Service Fabric clusters.</span></span>

## <a name="troubleshoot-using-diagnostics-logs"></a><span data-ttu-id="e6e3a-107">Eseguire la risoluzione dei problemi usando i log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="e6e3a-107">Troubleshoot using diagnostics logs</span></span>
<span data-ttu-id="e6e3a-108">Di seguito sono riportati alcuni esempi su come i registri errori comuni di toointerpret hello che può verificarsi:</span><span class="sxs-lookup"><span data-stu-id="e6e3a-108">Here are some examples on how toointerpret hello common failure logs that one can encounter:</span></span>

1. <span data-ttu-id="e6e3a-109">Il proxy inverso restituisce il codice di stato della risposta 504 (timeout).</span><span class="sxs-lookup"><span data-stu-id="e6e3a-109">Reverse proxy returns response status code 504 (Timeout).</span></span>

    <span data-ttu-id="e6e3a-110">Un motivo potrebbe essere causa l'interruzione del servizio toohello tooreply nel periodo di timeout richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-110">One reason could be due toohello service failing tooreply within hello request timeout period.</span></span>
<span data-ttu-id="e6e3a-111">Hello primo evento seguente Registra dettagli hello della richiesta di hello ricevuto nel proxy inverso hello.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-111">hello first event below logs hello details of hello request received at hello reverse proxy.</span></span> <span data-ttu-id="e6e3a-112">Hello secondo evento indica che la richiesta hello non è riuscito durante l'inoltro tooservice, scadenza troppo "Errore interno = ERROR_WINHTTP_TIMEOUT"</span><span class="sxs-lookup"><span data-stu-id="e6e3a-112">hello second event indicates that hello request failed while forwarding tooservice, due too"internal error = ERROR_WINHTTP_TIMEOUT"</span></span> 

    <span data-ttu-id="e6e3a-113">payload Hello include:</span><span class="sxs-lookup"><span data-stu-id="e6e3a-113">hello payload includes:</span></span>

    *  <span data-ttu-id="e6e3a-114">**traceId**: il GUID può essere utilizzato toocorrelate tutti gli eventi di hello corrispondente tooa singola richiesta.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-114">**traceId**: This GUID can be used toocorrelate all hello events corresponding tooa single request.</span></span> <span data-ttu-id="e6e3a-115">In hello di sotto di due eventi, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implicando appartengono toohello stessa richiesta.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-115">In hello below two events, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implying they belong toohello same request.</span></span>
    *  <span data-ttu-id="e6e3a-116">**requestUrl**: hello URL (URL di proxy inverso) toowhich hello richiesta è stata inviata.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-116">**requestUrl**: hello URL (Reverse proxy URL) toowhich hello request was sent.</span></span>
    *  <span data-ttu-id="e6e3a-117">**verb**: il verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-117">**verb**: HTTP verb.</span></span>
    *  <span data-ttu-id="e6e3a-118">**remoteAddress**: indirizzo del client invia una richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-118">**remoteAddress**: Address of client sending hello request.</span></span>
    *  <span data-ttu-id="e6e3a-119">**resolvedServiceUrl**: richiesta in ingresso di servizio endpoint URL toowhich hello è stato risolto.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-119">**resolvedServiceUrl**: Service endpoint URL toowhich hello incoming request was resolved.</span></span> 
    *  <span data-ttu-id="e6e3a-120">**errorDetails**: informazioni aggiuntive sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-120">**errorDetails**: Additional information about hello failure.</span></span>

    ```
    {
      "Timestamp": "2017-07-20T15:57:59.9871163-07:00",
      "ProviderName": "Microsoft-ServiceFabric",
      "Id": 51477,
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Request url = https://localhost:19081/LocationApp/LocationFEService?zipcode=98052, verb = GET, remote (client) address = ::1, resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052, request processing start time =     15:58:00.074114 (745,608.196 MSec) ",
      "ProcessId": 57696,
      "Level": "Informational",
      "Keywords": "0x1000000000000021",
      "EventName": "ReverseProxy",
      "ActivityID": null,
      "RelatedActivityID": null,
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?zipcode=98052",
        "verb": "GET",
        "remoteAddress": "::1",
        "resolvedServiceUrl": "Https://localhost:8491/LocationApp/?zipcode=98052",
        "requestStartTime": "2017-07-20T15:58:00.0741142-07:00"
      }
    }

    {
      "Timestamp": "2017-07-20T16:00:01.3173605-07:00",
      ...
      "Message": "2f87b722-e254-4ac2-a802-fd315c1a0271 Error while forwarding request tooservice: response status code = 504, description = Reverse proxy Timeout, phase = FinishSendRequest, internal error = ERROR_WINHTTP_TIMEOUT ",
      ...
      "Payload": {
        "traceId": "2f87b722-e254-4ac2-a802-fd315c1a0271",
        "statusCode": 504,
        "description": "Reverse Proxy Timeout",
        "sendRequestPhase": "FinishSendRequest",
        "errorDetails": "internal error = ERROR_WINHTTP_TIMEOUT"
      }
    }
    ```

2. <span data-ttu-id="e6e3a-121">Il proxy inverso restituisce il codice di stato della risposta 404 - Non trovato.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-121">Reverse proxy returns response status code 404 (Not Found).</span></span> 
    
    <span data-ttu-id="e6e3a-122">Di seguito è un evento di esempio in cui il proxy inverso restituisce 404 poiché non è riuscito hello toofind corrispondenza endpoint di servizio.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-122">Here is an example event where reverse proxy returns 404 since it failed toofind hello matching service endpoint.</span></span>
    <span data-ttu-id="e6e3a-123">le voci di payload Hello qui sono:</span><span class="sxs-lookup"><span data-stu-id="e6e3a-123">hello payload  entries of interest here are:</span></span>
    *  <span data-ttu-id="e6e3a-124">**processRequestPhase**: indica la fase hello durante l'elaborazione della richiesta quando si è verificato un errore di hello, ***TryGetEndpoint*** ad es.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-124">**processRequestPhase**: Indicates hello phase during request processing when hello failure occurred, ***TryGetEndpoint*** i.e</span></span> <span data-ttu-id="e6e3a-125">durante il tentativo toofetch hello servizio endpoint tooforward per.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-125">while trying toofetch hello service endpoint tooforward to.</span></span> 
    *  <span data-ttu-id="e6e3a-126">**errorDetails**: Elenca i criteri di ricerca di hello endpoint.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-126">**errorDetails**: Lists hello endpoint search criteria.</span></span> <span data-ttu-id="e6e3a-127">Qui è possibile visualizzare tale listenerName hello specificato = **FrontEndListener** mentre l'elenco di endpoint replica hello contiene solo un listener con nome hello **OldListener**.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-127">Here you can see that hello listenerName specified = **FrontEndListener** whereas hello replica endpoint list only contains a listener with hello name **OldListener**.</span></span>
    
    ```
    {
      ...
      "Message": "c1cca3b7-f85d-4fef-a162-88af23604343 Error while processing request, cannot forward tooservice: request url = https://localhost:19081/LocationApp/LocationFEService?ListenerName=FrontEndListener&zipcode=98052, verb = GET, remote (client) address = ::1, request processing start time = 16:43:02.686271 (3,448,220.353 MSec), error = FABRIC_E_ENDPOINT_NOT_FOUND, message = , phase = TryGetEndoint, SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"\":\"Https:\/\/localhost:8491\/LocationApp\/\"}} ",
      "ProcessId": 57696,
      "Level": "Warning",
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "c1cca3b7-f85d-4fef-a162-88af23604343",
        "requestUrl": "https://localhost:19081/LocationApp/LocationFEService?ListenerName=NewListener&zipcode=98052",
        ...
        "processRequestPhase": "TryGetEndoint",
        "errorDetails": "SecureOnlyMode = false, gateway protocol = https, listenerName = FrontEndListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Https:\/\/localhost:8491\/LocationApp\/\"}}"
      }
    }
    ```
    <span data-ttu-id="e6e3a-128">Un altro esempio in cui il proxy inverso può restituire l'errore 404 non trovato è: ApplicationGateway\Http parametro di configurazione **SecureOnlyMode** è tootrue proxy inverso di hello in ascolto su **HTTPS**, Tuttavia, tutti gli endpoint di replica hello sono non sicuri (a cui è in ascolto su HTTP).</span><span class="sxs-lookup"><span data-stu-id="e6e3a-128">Another example where reverse proxy can return 404 Not Found is: ApplicationGateway\Http configuration parameter **SecureOnlyMode** is set tootrue with hello reverse proxy listening on **HTTPS**, however all of hello replica endpoints are unsecure (listening on HTTP).</span></span>
    <span data-ttu-id="e6e3a-129">Invertire restituisce proxy 404 poiché non è possibile trovare un endpoint in ascolto HTTPS tooforward hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-129">Reverse proxy returns 404 since it cannot find an endpoint listening on HTTPS tooforward hello request.</span></span> <span data-ttu-id="e6e3a-130">Analisi dei parametri di hello nel payload dell'evento hello consente toonarrow verso il basso problema hello:</span><span class="sxs-lookup"><span data-stu-id="e6e3a-130">Analyzing hello parameters in hello event payload helps toonarrow down hello issue:</span></span>
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. <span data-ttu-id="e6e3a-131">Proxy inverso toohello di richiesta ha esito negativo con un errore di timeout.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-131">Request toohello reverse proxy fails with a timeout error.</span></span> 
    <span data-ttu-id="e6e3a-132">i registri eventi di Hello contengono un evento con i dettagli della richiesta ricevuta hello (non mostrati qui).</span><span class="sxs-lookup"><span data-stu-id="e6e3a-132">hello event logs contain an event with hello received request details (not shown here).</span></span>
    <span data-ttu-id="e6e3a-133">evento successivo Hello mostra che hello servizio ha restituito un codice di 404 stato e proxy inverso avvia nuovamente risolvere.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-133">hello next event shows that hello service responded with a 404 status code and reverse proxy initiates a re-resolve.</span></span> 

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Request tooservice returned: status code = 404, status description = , Reresolving ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "statusCode": 404,
        "statusDescription": ""
      }
    }
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Re-resolved service url = Https://localhost:8491/LocationApp/?zipcode=98052 ",
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "requestUrl": "Https://localhost:8491/LocationApp/?zipcode=98052"
      }
    }
    ```
    <span data-ttu-id="e6e3a-134">Quando la raccolta di tutti gli eventi di hello, viene visualizzato un flusso di eventi che mostra ogni risoluzione e il tentativo di inoltro.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-134">When collecting all hello events, you see a train of events showing every resolve and forward attempt.</span></span>
    <span data-ttu-id="e6e3a-135">Hello ultimo evento serie hello viene illustrata l'elaborazione della richiesta hello non è riuscita con un valore di timeout e il numero di hello di tentativi di risoluzione ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-135">hello last event in hello series shows hello request processing has failed with a timeout, along with hello number of successful resolve attempts.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="e6e3a-136">Consiglia di raccolta eventi dettagliati canale hello tookeep disabilitato per impostazione predefinita e abilitarla per la risoluzione dei problemi in base a una necessità.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-136">It is recommended tookeep hello  verbose channel event collection disabled by default and enable it for troubleshooting on a need basis.</span></span>

    ```
    {
      ...
      "Message": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e Error while processing request: number of successful resolve attempts = 12, error = FABRIC_E_TIMEOUT, message = , phase = ResolveServicePartition,  ",
      "EventName": "ReverseProxy",
      ...
      "Payload": {
        "traceId": "7ac6212c-c8c4-4c98-9cf7-c187a94f141e",
        "resolveCount": 12,
        "errorval": -2147017729,
        "errorMessage": "",
        "processRequestPhase": "ResolveServicePartition",
        "errorDetails": ""
      }
    }
    ```
    
    <span data-ttu-id="e6e3a-137">Se la raccolta è abilitata critico/errore solo per gli eventi, viene visualizzato un evento con informazioni dettagliate su hello timeout e il numero di hello di tentativi di risoluzione.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-137">If collection is enabled for critical/error events only, you see one event with details about hello timeout and hello number of resolve attempts.</span></span> 
    
    <span data-ttu-id="e6e3a-138">Se il servizio hello intenda toosend un utente toohello indietro codice di 404 stato, deve essere corredato da un'intestazione "X-ServiceFabric".</span><span class="sxs-lookup"><span data-stu-id="e6e3a-138">If hello service intends toosend a 404 status code back toohello user, it should be accompanied by an "X-ServiceFabric" header.</span></span> <span data-ttu-id="e6e3a-139">Dopo la risoluzione di questo, si noterà proxy inverso inoltra hello stato codice toohello indietro client.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-139">After fixing this, you will see that reverse proxy forwards hello status code back toohello client.</span></span>  

4. <span data-ttu-id="e6e3a-140">Casi in cui hello client è disconnesso hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-140">Cases when hello client has disconnected hello request.</span></span>

    <span data-ttu-id="e6e3a-141">Hello sotto evento viene registrato quando proxy inverso è inoltro hello risposta tooclient ma disconnessione hello del client:</span><span class="sxs-lookup"><span data-stu-id="e6e3a-141">hello below event is recorded when reverse proxy is forwarding hello response tooclient but hello client disconnects:</span></span>

    ```
    {
      ...
      "Message": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8 Unable toosend response tooclient: phase = SendResponseHeaders, error = -805306367, internal error = ERROR_SUCCESS ",
      "ProcessId": 57696,
      "Level": "Warning",
      ...
      "EventName": "ReverseProxy",
      "Payload": {
        "traceId": "6e2571a3-14a8-4fc7-93bb-c202c23b50b8",
        "sendResponsePhase": "SendResponseHeaders",
        "errorval": -805306367,
        "winHttpError": "ERROR_SUCCESS"
      }
    }
    ```

> [!NOTE]
> <span data-ttu-id="e6e3a-142">L'elaborazione delle richieste di eventi correlati toowebsocket non sono attualmente connessi.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-142">Events related toowebsocket request processing are not currently logged.</span></span> <span data-ttu-id="e6e3a-143">Questo verrà aggiunto nella prossima versione di hello.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-143">This will be added in hello next release.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6e3a-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6e3a-144">Next steps</span></span>
* <span data-ttu-id="e6e3a-145">[Aggregazione e raccolta di eventi usando Diagnostica di Microsoft Azure](service-fabric-diagnostics-event-aggregation-wad.md) per abilitare la raccolta di log nei cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-145">[Event aggregation and collection using Windows Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md) for enabling log collection in Azure clusters.</span></span>
* <span data-ttu-id="e6e3a-146">eventi di Service Fabric tooview in Visual Studio, vedere [monitoraggio e diagnosi localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="e6e3a-146">tooview Service Fabric events in Visual Studio, see [Monitor and diagnose locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>
* <span data-ttu-id="e6e3a-147">Fare riferimento troppo[configurare servizi di proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) per Gestione risorse di Azure tooconfigure proxy inverso sicuro con le opzioni di convalida certificato di servizio diverso hello esempi di modello.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-147">Refer too[Configure reverse proxy tooconnect toosecure services](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) for Azure Resource Manager template samples tooconfigure secure reverse proxy with hello different service certificate validation options.</span></span>
* <span data-ttu-id="e6e3a-148">Lettura [Service Fabric proxy inverso](service-fabric-reverseproxy.md) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="e6e3a-148">Read [Service Fabric reverse proxy](service-fabric-reverseproxy.md) toolearn more.</span></span>
