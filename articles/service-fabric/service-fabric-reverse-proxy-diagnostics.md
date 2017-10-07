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
# <a name="monitor-and-diagnose-request-processing-at-hello-reverse-proxy"></a>Monitoraggio e diagnosi l'elaborazione della richiesta al proxy inverso hello

A partire dalla versione di hello 5.7 dell'infrastruttura di servizio, sono disponibili per la raccolta eventi di proxy inverso. Hello eventi sono disponibili in due canali, una con solo gli eventi di errore correlati errore durante l'elaborazione di toorequest proxy inverso hello e secondo canale contenente gli eventi dettagliati con le voci per le richieste con esito positivo e non riuscite.

Fare riferimento troppo[raccogliere gli eventi di proxy inverso](service-fabric-diagnostics-event-aggregation-wad.md#collect-reverse-proxy-events) tooenable raccolta di eventi da questi canali in locale e i cluster di Azure Service Fabric.

## <a name="troubleshoot-using-diagnostics-logs"></a>Eseguire la risoluzione dei problemi usando i log di diagnostica
Di seguito sono riportati alcuni esempi su come i registri errori comuni di toointerpret hello che può verificarsi:

1. Il proxy inverso restituisce il codice di stato della risposta 504 (timeout).

    Un motivo potrebbe essere causa l'interruzione del servizio toohello tooreply nel periodo di timeout richiesta hello.
Hello primo evento seguente Registra dettagli hello della richiesta di hello ricevuto nel proxy inverso hello. Hello secondo evento indica che la richiesta hello non è riuscito durante l'inoltro tooservice, scadenza troppo "Errore interno = ERROR_WINHTTP_TIMEOUT" 

    payload Hello include:

    *  **traceId**: il GUID può essere utilizzato toocorrelate tutti gli eventi di hello corrispondente tooa singola richiesta. In hello di sotto di due eventi, hello traceId = **2f87b722-e254-4ac2-a802-fd315c1a0271**, implicando appartengono toohello stessa richiesta.
    *  **requestUrl**: hello URL (URL di proxy inverso) toowhich hello richiesta è stata inviata.
    *  **verb**: il verbo HTTP.
    *  **remoteAddress**: indirizzo del client invia una richiesta di hello.
    *  **resolvedServiceUrl**: richiesta in ingresso di servizio endpoint URL toowhich hello è stato risolto. 
    *  **errorDetails**: informazioni aggiuntive sull'errore hello.

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

2. Il proxy inverso restituisce il codice di stato della risposta 404 - Non trovato. 
    
    Di seguito è un evento di esempio in cui il proxy inverso restituisce 404 poiché non è riuscito hello toofind corrispondenza endpoint di servizio.
    le voci di payload Hello qui sono:
    *  **processRequestPhase**: indica la fase hello durante l'elaborazione della richiesta quando si è verificato un errore di hello, ***TryGetEndpoint*** ad es. durante il tentativo toofetch hello servizio endpoint tooforward per. 
    *  **errorDetails**: Elenca i criteri di ricerca di hello endpoint. Qui è possibile visualizzare tale listenerName hello specificato = **FrontEndListener** mentre l'elenco di endpoint replica hello contiene solo un listener con nome hello **OldListener**.
    
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
    Un altro esempio in cui il proxy inverso può restituire l'errore 404 non trovato è: ApplicationGateway\Http parametro di configurazione **SecureOnlyMode** è tootrue proxy inverso di hello in ascolto su **HTTPS**, Tuttavia, tutti gli endpoint di replica hello sono non sicuri (a cui è in ascolto su HTTP).
    Invertire restituisce proxy 404 poiché non è possibile trovare un endpoint in ascolto HTTPS tooforward hello richiesta. Analisi dei parametri di hello nel payload dell'evento hello consente toonarrow verso il basso problema hello:
    
    ```
        "errorDetails": "SecureOnlyMode = true, gateway protocol = https, listenerName = NewListener, replica endpoint = {\"Endpoints\":{\"OldListener\":\"Http:\/\/localhost:8491\/LocationApp\/\", \"NewListener\":\"Http:\/\/localhost:8492\/LocationApp\/\"}}"
    ```

3. Proxy inverso toohello di richiesta ha esito negativo con un errore di timeout. 
    i registri eventi di Hello contengono un evento con i dettagli della richiesta ricevuta hello (non mostrati qui).
    evento successivo Hello mostra che hello servizio ha restituito un codice di 404 stato e proxy inverso avvia nuovamente risolvere. 

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
    Quando la raccolta di tutti gli eventi di hello, viene visualizzato un flusso di eventi che mostra ogni risoluzione e il tentativo di inoltro.
    Hello ultimo evento serie hello viene illustrata l'elaborazione della richiesta hello non è riuscita con un valore di timeout e il numero di hello di tentativi di risoluzione ha esito positivo.
    
    > [!NOTE]
    > Consiglia di raccolta eventi dettagliati canale hello tookeep disabilitato per impostazione predefinita e abilitarla per la risoluzione dei problemi in base a una necessità.

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
    
    Se la raccolta è abilitata critico/errore solo per gli eventi, viene visualizzato un evento con informazioni dettagliate su hello timeout e il numero di hello di tentativi di risoluzione. 
    
    Se il servizio hello intenda toosend un utente toohello indietro codice di 404 stato, deve essere corredato da un'intestazione "X-ServiceFabric". Dopo la risoluzione di questo, si noterà proxy inverso inoltra hello stato codice toohello indietro client.  

4. Casi in cui hello client è disconnesso hello richiesta.

    Hello sotto evento viene registrato quando proxy inverso è inoltro hello risposta tooclient ma disconnessione hello del client:

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
> L'elaborazione delle richieste di eventi correlati toowebsocket non sono attualmente connessi. Questo verrà aggiunto nella prossima versione di hello.

## <a name="next-steps"></a>Passaggi successivi
* [Aggregazione e raccolta di eventi usando Diagnostica di Microsoft Azure](service-fabric-diagnostics-event-aggregation-wad.md) per abilitare la raccolta di log nei cluster di Azure.
* eventi di Service Fabric tooview in Visual Studio, vedere [monitoraggio e diagnosi localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).
* Fare riferimento troppo[configurare servizi di proxy inverso tooconnect toosecure](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/ReverseProxySecureSample#configure-reverse-proxy-to-connect-to-secure-services) per Gestione risorse di Azure tooconfigure proxy inverso sicuro con le opzioni di convalida certificato di servizio diverso hello esempi di modello.
* Lettura [Service Fabric proxy inverso](service-fabric-reverseproxy.md) toolearn altre.
