---
title: "aaaCall un webhook sugli avvisi di Log attività di Azure | Documenti Microsoft"
description: "Route servizi attività di log eventi tooother per le azioni personalizzate. Inviare ad esempio SMS, registrare i bug o inviare notifiche al team tramite servizio di chat o messaggistica."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Chiamare un webhook negli avvisi dei log attività di Azure
Webhook consentono di Azure tooroute sistemi tooother di notifica per le azioni di post-elaborazione o personalizzati di avviso. È possibile utilizzare un webhook su un avviso tooroute è tooservices che invia SMS, registrare i bug, inviare una notifica di un team tramite servizi di chat o messaggistica o eseguire un numero qualsiasi di altre azioni. In questo articolo viene descritto come tooset toobe un webhook chiamato quando un generato avvisi di Log attività di Azure. Viene inoltre illustrato il payload di hello per hello HTTP POST tooa webhook è simile. Per informazioni sull'installazione di hello e lo schema per un avviso metrica Azure [questa pagina viene visualizzata invece](insights-webhooks-alerts.md). È inoltre possibile impostare un messaggio di avviso toosend Log attività quando attivato.

> [!NOTE]
> Questa funzionalità è attualmente in anteprima e verrà rimossa in un determinato hello future.
>
>

È possibile impostare un avviso di Log attività utilizzando hello [i cmdlet di PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [CLI multipiattaforma](insights-cli-samples.md#work-with-alerts), o [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn933805.aspx). Attualmente, non è possibile impostare uno utilizzando hello portale di Azure.

## <a name="authenticating-hello-webhook"></a>L'autenticazione hello webhook
Hello webhook autenticazione utilizzando uno dei seguenti metodi:

1. **Autorizzazione basata su token** -hello webhook URI viene salvato con un ID del token, ad esempio,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Autorizzazione di base** -hello webhook URI viene salvato con un nome utente e password, ad esempio,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Schema del payload
operazione POST Hello contiene hello seguito payload JSON e lo schema per gli avvisi basati su Log attività. Questo schema è simile toohello utilizzato da avvisi basati sulla metrica.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Nome dell'elemento | Descrizione |
| --- | --- |
| status |Usato per avvisi relativi alle metriche. Impostare sempre troppo "attivato" per gli avvisi del registro attività. |
| context |Contesto dell'evento hello. |
| resourceProviderName |provider di risorse Hello di hello influisce sulle risorse. |
| conditionType |Sempre "Event". |
| name |Nome della regola di avviso hello. |
| id |ID risorsa dell'avviso hello. |
| description |Descrizione avviso durante la creazione dell'avviso hello come set. |
| subscriptionId |ID sottoscrizione di Azure. |
| timestamp |Ora in cui hello è stato generato l'evento dal servizio di Azure che ha elaborato la richiesta hello hello. |
| resourceId |ID di risorsa di hello influisce sulle risorse. |
| resourceGroupName |Nome del gruppo di risorse hello per hello interessati risorsa |
| properties |Set di `<Key, Value>` coppie (ad esempio `Dictionary<String, String>`) che include i dettagli sull'evento hello. |
| event |Elemento che contiene i metadati sull'evento hello. |
| autorizzazione |proprietà RBAC Hello dell'evento hello. In genere includono hello "action" e "ruolo" hello "ambito". |
| category |Categoria di eventi di hello. I valori supportati includono Administrative, Alert, Security, ServiceHealth, Recommendation. |
| caller |Indirizzo di posta elettronica dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità. Può essere null per alcune chiamate di sistema. |
| correlationId |In genere un GUID in formato stringa. Gli eventi con ID correlazione appartengono toohello stessa azione di dimensioni maggiori e in genere condividono un ID di correlazione. |
| eventDescription |Descrizione di testo statico dell'evento hello. |
| eventDataId |Identificatore univoco per l'evento hello. |
| eventSource |Nome di hello Azure servizio o dell'infrastruttura che l'evento generato hello. |
| httpRequest |In genere include hello "clientRequestId", "clientIpAddress" e "method" (il metodo HTTP, ad esempio PUT). |
| level |Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose". |
| operationId |In genere un GUID condiviso tra gli eventi di hello toosingle operazione corrispondente. |
| operationName |Nome dell'operazione di hello. |
| properties |Proprietà di evento hello. |
| status |Stringa. Stato dell'operazione di hello. I valori comuni includono: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved". |
| subStatus |In genere include codice di stato HTTP hello della chiamata REST corrispondente hello. Può includere anche altre stringhe che descrivono uno stato secondario. I valori di stato secondario comuni includono: OK (codice di stato HTTP: 200), Created (codice di stato HTTP: 201), Accepted (codice di stato HTTP: 202), No Content (codice di stato HTTP: 204), Bad Request (codice di stato HTTP: 400), Not Found (codice di stato HTTP: 404), Conflict (codice di stato HTTP: 409), Internal Server Error (codice di stato HTTP: 500), Service Unavailable (codice di stato HTTP: 503), Gateway Timeout (codice di stato HTTP: 504) |

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su hello Log attività](monitoring-overview-activity-logs.md)
* [Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Utilizzare la logica App toosend un SMS tramite Twilio da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di Log attività.
* [Utilizzare la logica App toosend un messaggio da un avviso Azure Slack](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di Log attività.
* [Utilizzare la logica App toosend tooan un messaggio della coda di Azure da un avviso Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). In questo esempio è per gli avvisi di metrica, ma può essere modificato toowork con un avviso di Log attività.
