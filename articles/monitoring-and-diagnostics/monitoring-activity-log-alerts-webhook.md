---
title: "schema di webhook hello aaaUnderstand utilizzato negli avvisi del registro attività | Documenti Microsoft"
description: "Informazioni sullo schema hello di hello JSON che viene registrato l'URL del webhook tooa quando viene attivato un avviso di log di attività."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Webhook per gli avvisi del log attività di Azure
Come parte della definizione di hello di un gruppo di azioni, è possibile configurare webhook endpoint tooreceive attività Registro notifiche di avviso. Con webhook, è possibile distribuire questi sistemi tooother notifiche per le azioni di post-elaborazione o personalizzate. Questo articolo illustra i payload hello per hello HTTP POST tooa webhook è simile.

Per ulteriori informazioni sugli avvisi di log di attività, vedere come troppo[creare attività di Azure gli avvisi del registro](monitoring-activity-log-alerts.md).

Per informazioni su gruppi di azioni, vedere come troppo[creare gruppi di azioni](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>L'autenticazione hello webhook
Hello webhook possono utilizzare facoltativamente basata su token di autorizzazione per l'autenticazione. Hello webhook URI viene salvato con un ID del token, ad esempio, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Schema del payload
payload JSON Hello contenuti in hello operazione POST varia in base a campo data.context.activityLog.eventSource del payload hello.

###<a name="common"></a>Comune
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Amministrativo
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Per i dettagli su schemi specifici relativi agli avvisi del log attività per le notifiche sull'integrità del servizio, vedere [Notifiche sull'integrità del servizio](monitoring-service-notifications.md).

Per informazioni dettagliate specifiche dello schema su tutti gli avvisi di log altre attività, vedere [Panoramica del log attività Azure hello](monitoring-overview-activity-logs.md).

| Nome dell'elemento | Descrizione |
| --- | --- |
| status |Usato per avvisi relativi alle metriche. Impostare sempre troppo "attivato" per gli avvisi del registro attività. |
| context |Contesto dell'evento hello. |
| resourceProviderName |provider di risorse Hello di hello influisce sulle risorse. |
| conditionType |Sempre "Event". |
| name |Nome della regola di avviso hello. |
| id |ID risorsa dell'avviso hello. |
| description |Descrizione dell'avviso impostato quando viene creato l'avviso hello. |
| subscriptionId |ID sottoscrizione di Azure. |
| timestamp |Ora in cui hello è stato generato l'evento dal servizio di Azure che ha elaborato la richiesta hello hello. |
| resourceId |ID di risorsa di hello influisce sulle risorse. |
| resourceGroupName |Nome del gruppo di risorse hello per hello influisce sulle risorse. |
| properties |Set di `<Key, Value>` coppie (vale a dire `Dictionary<String, String>`) che include i dettagli sull'evento hello. |
| event |Elemento che contiene i metadati relativi a eventi hello. |
| autorizzazione |proprietà di controllo di accesso basato sui ruoli Hello dell'evento hello. Queste proprietà includono in genere azione hello, hello ruolo e ambito hello. |
| category |Categoria di eventi di hello. I valori supportati includono Administrative, Alert, Security, ServiceHealth e Recommendation. |
| caller |Indirizzo di posta elettronica dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità. Può essere null per alcune chiamate di sistema. |
| correlationId |In genere un GUID in formato stringa. Gli eventi con ID correlazione appartengono toohello stessa azione di dimensioni maggiori e in genere condividono un ID di correlazione. |
| eventDescription |Descrizione di testo statico dell'evento hello. |
| eventDataId |Identificatore univoco per l'evento hello. |
| eventSource |Nome di hello Azure servizio o dell'infrastruttura che l'evento generato hello. |
| httpRequest |Hello richiesta include in genere hello clientRequestId, clientIpAddress e il metodo HTTP (ad esempio PUT). |
| level |Uno dei seguenti valori hello: critico, errore, avviso, informativo e dettagliato. |
| operationId |In genere un GUID condiviso tra gli eventi di hello toosingle operazione corrispondente. |
| operationName |Nome dell'operazione di hello. |
| properties |Proprietà di evento hello. |
| status |Stringa. Stato dell'operazione di hello. I valori comuni includono: Started, In Progress, Succeeded, Failed, Active e Resolved. |
| subStatus |In genere include codice di stato HTTP hello della chiamata REST corrispondente hello. Può includere anche altre stringhe che descrivono uno stato secondario. I valori di stato secondario comuni includono OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504). |

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui log attività hello](monitoring-overview-activity-logs.md).
* [Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Utilizzare un toosend di logica app un SMS tramite Twilio da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di log di attività.
* [Utilizzare un toosend app logica un messaggio da un avviso Azure Slack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di log di attività.
* [Utilizzare un toosend app logica tooan un messaggio Azure coda da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di log di attività.
