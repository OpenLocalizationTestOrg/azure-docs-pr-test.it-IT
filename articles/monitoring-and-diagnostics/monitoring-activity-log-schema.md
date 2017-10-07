---
title: "Schema di eventi del registro attività aaaAzure | Documenti Microsoft"
description: "Comprensione hello schema di eventi per i dati emessi in hello Log attività"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Schema degli eventi del log attività di Azure
Hello **Log attività Azure** è un log che fornisce informazioni approfondite tutti gli eventi a livello di sottoscrizione che si sono verificati in Azure. Questo articolo descrive allo schema di eventi hello per ogni categoria di dati.

## <a name="administrative"></a>Amministrativo
Questa categoria include i record di hello di tutti create, update, delete e azione di operazioni eseguite tramite Gestione risorse. Esempi di tipi di eventi visualizzati in questa categoria includono hello "Crea macchina virtuale" e "gruppo di sicurezza di rete delete" ogni azione eseguita da un utente o applicazione usando Gestione risorse viene modellato come un'operazione su un determinato tipo di risorsa. Se il tipo di operazione hello è scrivere, Delete o azione, i record di hello inizio hello sia esito positivo o esito negativo dell'operazione vengono registrati nella categoria amministrativa hello. categoria amministrativa Hello include anche qualsiasi controllo di accesso basato su toorole modifiche in una sottoscrizione.

### <a name="sample-event"></a>Evento di esempio
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Descrizioni delle proprietà
| Nome dell'elemento | Description |
| --- | --- |
| autorizzazione |BLOB di proprietà RBAC dell'evento hello. In genere include le proprietà di "azione", "role" e "scope" hello. |
| caller |Indirizzo di posta elettronica dell'utente hello che ha eseguito l'operazione di hello, attestazione UPN o attestazione nome SPN in base alla disponibilità. |
| channels |Uno dei seguenti valori hello: "Admin", "Operation" |
| claims |token JWT Hello utilizzati da Active Directory tooauthenticate hello utente o applicazione tooperform questa operazione nella console di gestione risorse. |
| correlationId |In genere un GUID in formato stringa hello. Gli eventi che condividono un valore correlationId appartengono toohello stessa azione. |
| description |Testo statico che descrive un evento. |
| eventDataId |Identificatore univoco di un evento. |
| httpRequest |BLOB hello che descrive la richiesta Http. In genere include hello "clientRequestId", "clientIpAddress" e "method" (metodo HTTP. ad esempio PUT). |
| level |Livello dell'evento hello. Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose" |
| resourceGroupName |Nome del gruppo di risorse hello per hello influisce sulle risorse. |
| resourceProviderName |Nome del provider di risorse hello per hello interessati risorsa |
| resourceId |Id di risorsa di hello influisce sulle risorse. |
| operationId |Un GUID condiviso tra eventi di hello corrispondenti tooa singola operazione. |
| operationName |Nome dell'operazione di hello. |
| properties |Set di `<Key, Value>` coppie (dizionario) che descrive hello dettagli dell'evento hello. |
| status |Stringa che descrive lo stato di hello dell'operazione di hello. Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus |In genere il codice di stato HTTP della corrispondente chiamata REST hello hello, ma può includere anche altre stringhe che descrive uno stato secondario, ad esempio i valori comuni: OK (codice di stato HTTP: 200), creato (codice di stato HTTP: 201), accettato (codice di stato HTTP: 202), il contenuto No (HTTP Codice di stato: 204), richiesta non valida (codice di stato HTTP: 400), non è stata trovata (codice di stato HTTP: 404), dei conflitti (codice di stato HTTP: 409), errore interno del Server (codice di stato HTTP: 500), Service non disponibile (codice di stato HTTP: 503), Timeout del Gateway (codice di stato HTTP: 504). |
| eventTimestamp |Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente. |
| submissionTimestamp |Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query. |
| subscriptionId |ID sottoscrizione di Azure. |

## <a name="service-health"></a>Integrità del servizio
Questa categoria include i record di hello di eventuali problemi di integrità servizio che si sono verificati in Azure. Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "SQL Azure negli Stati Uniti orientali si è verificati i tempi di inattività". Eventi di integrità del servizio sono disponibili in cinque tipi: azione richiesta, del recupero assistito, evento imprevisto, manutenzione, informazioni o sicurezza e vengono visualizzate solo se si dispone di una risorsa nella sottoscrizione hello che potrebbe essere interessata dall'evento hello.

### <a name="sample-event"></a>Evento di esempio
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Descrizioni delle proprietà
Nome dell'elemento | Descrizione
-------- | -----------
channels | È uno dei seguenti valori hello: "Admin", "Operation"
correlationId | È in genere un GUID in formato stringa hello. Gli eventi che appartengono toohello stessa azione condividono di solito hello stesso correlationId.
description | Descrizione dell'evento hello.
eventDataId | Identificatore univoco di Hello di un evento.
eventName | titolo Hello dell'evento hello.
level | Livello dell'evento hello. Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose"
resourceProviderName | Nome del provider di risorse hello per hello influisce sulle risorse. Se non è noto, sarà null.
resourceType| tipo di Hello della risorsa di hello influisce sulle risorse. Se non è noto, sarà null.
subStatus | In genere, null per gli eventi di integrità del servizio.
eventTimestamp | Timestamp dell'evento hello è stato generato e inviato toohello Log attività.
submissionTimestamp |   Timestamp dell'evento hello è diventato disponibile nel Log attività hello.
subscriptionId | Hello sottoscrizione di Azure in cui è stato registrato questo evento.
status | Stringa che descrive lo stato di hello dell'operazione di hello. Alcuni valori comuni sono: Active, Resolved.
operationName | Nome dell'operazione di hello. In genere, Microsoft.ServiceHealth/incident/action.
category | "ServiceHealth"
resourceId | Id di risorsa di hello interessati risorsa, se noto. L'ID sottoscrizione viene fornito diversamente.
Properties.title | Hello titolo localizzato per la comunicazione. L'inglese è una lingua predefinita hello.
Properties.communication | Hello localizzata dettagli di comunicazione hello con il markup HTML. Inglese è l'impostazione predefinita di hello.
Properties.incidentType | Valori possibili: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifica l'evento imprevisto di hello che è associato questo evento. Utilizzare questo evento imprevisto di toocorrelate hello eventi tooan correlati.
Properties.impactedServices | Un escape blob JSON che descrive i servizi di hello e le aree che sono interessate da evento imprevisto di hello. Un elenco di servizi, ognuno dei quali ha un nome di servizio e un elenco delle aree interessate, ognuna con un nome di area.
Properties.defaultLanguageTitle | comunicazione Hello in inglese
Properties.defaultLanguageContent | comunicazione Hello in inglese come markup html o testo normale
Properties.stage | I valori possibili di AssistedRecovery, ActionRequired, Information, Incident, Security sono Active e Resolved. Per la manutenzione i valori possibili sono: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete
Properties.communicationId | comunicazione Hello questo evento è associato.

## <a name="alert"></a>Avviso
Questa categoria include i record di hello di tutte le attivazioni di avvisi di Azure. Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "% della CPU nella macchina virtuale myVM è stato superato l'80 per hello negli ultimi 5 minuti." In diversi sistemi Azure il concetto di avviso prevede la possibilità di definire una regola di qualche tipo e di ricevere una notifica quando le condizioni corrispondono a tale regola. Ogni volta che un tipo di avviso Azure supportato 'attiva,' o condizioni hello sono soddisfatto toogenerate una notifica, un record di attivazione hello viene inoltre inserito toothis categoria di hello Log attività.

### <a name="sample-event"></a>Evento di esempio

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Descrizioni delle proprietà
| Nome dell'elemento | Descrizione |
| --- | --- |
| caller | Sempre Microsoft.Insights/alertRules |
| channels | Sempre "Admin, Operation" |
| claims | Blob JSON con hello nome SPN (service principal name) o risorsa di tipo, del motore degli avvisi hello. |
| correlationId | Un GUID in formato stringa hello. |
| description |Descrizione di testo statico dell'evento di avviso hello. |
| eventDataId |Identificatore univoco dell'evento di avviso hello. |
| level |Livello dell'evento hello. Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose" |
| resourceGroupName |Nome del gruppo di risorse hello per hello in presenza di risorse è un avviso di metrica. Per altri tipi di avviso, questo è il nome di hello hello del gruppo di risorse che contiene l'avviso hello stesso. |
| resourceProviderName |Nome del provider di risorse hello per hello in presenza di risorse è un avviso di metrica. Per altri tipi di avviso, si tratta di nome hello del provider di risorse hello per avviso hello stesso. |
| resourceId | Nome dell'ID di risorsa hello per hello in presenza di risorse è un avviso di metrica. Per altri tipi di avviso, questo è l'ID della risorsa di avviso hello stessa risorsa hello. |
| operationId |Un GUID condiviso tra eventi di hello corrispondenti tooa singola operazione. |
| operationName |Nome dell'operazione di hello. |
| properties |Set di `<Key, Value>` coppie (dizionario) che descrive hello dettagli dell'evento hello. |
| status |Stringa che descrive lo stato di hello dell'operazione di hello. Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | In genere null per gli avvisi. |
| eventTimestamp |Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente. |
| submissionTimestamp |Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query. |
| subscriptionId |ID sottoscrizione di Azure. |

### <a name="properties-field-per-alert-type"></a>Campo delle proprietà per ogni tipo di avviso
campo di proprietà Hello conterrà valori diversi a seconda dell'origine dell'evento di avviso hello hello. Due comuni provider di eventi di avviso sono gli avvisi e gli avvisi delle metriche del log attività.

#### <a name="properties-for-activity-log-alerts"></a>Proprietà degli avvisi del log attività
| Nome dell'elemento | Descrizione |
| --- | --- |
| properties.subscriptionId | ID sottoscrizione Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato. |
| properties.eventDataId | dati evento Hello con ID di evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato. |
| properties.resourceGroup | gruppo di risorse Hello da hello attività Registra evento che ha causato questo toobe regola di avviso di log attività attivato. |
| properties.resourceId | ID di risorsa Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato. |
| properties.eventTimestamp | timestamp dell'evento Hello dell'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato. |
| properties.operationName | nome dell'operazione Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato. |
| properties.status | stato Hello dall'evento di registro attività hello, che ha causato questo toobe regola di avviso di log attività attivato.|

#### <a name="properties-for-metric-alerts"></a>Proprietà degli avvisi delle metriche
| Nome dell'elemento | Descrizione |
| --- | --- |
| properties.RuleUri | ID di risorsa di hello metrica regola di avviso stesso. |
| properties.RuleName | nome Hello della regola di avviso metrica hello. |
| properties.RuleDescription | descrizione di Hello della regola di avviso metrica hello (come definito nella regola di avviso hello). |
| properties.Threshold | valore di soglia Hello utilizzato nella valutazione di hello della regola di avviso metrica hello. |
| properties.WindowSizeInMinutes | dimensione della finestra Hello utilizzato nella valutazione di hello della regola di avviso metrica hello. |
| properties.Aggregation | tipo di aggregazione Hello definito nella regola di avviso metrica hello. |
| properties.Operator | operatore condizionale Hello utilizzato nella valutazione di hello della regola di avviso metrica hello. |
| properties.MetricName | nome della metrica Hello della metrica hello utilizzato nella valutazione di hello della regola di avviso metrica hello. |
| properties.MetricUnit | unità di metrica Hello metrica hello utilizzato nella valutazione di hello della regola di avviso metrica hello. |

## <a name="autoscale"></a>Autoscale
Questa categoria include i record di hello di qualsiasi operazione toohello correlati gli eventi del motore di scalabilità automatica hello in base alle impostazioni di scalabilità automatica che è stato definito nella sottoscrizione. Un esempio di hello tipo di evento che verrà visualizzato in questa categoria è "Scalabilità automatica scalabilità verticale azione non riuscita". Utilizza la scalabilità automatica, è possibile automaticamente scalare in orizzontale o ridimensionare in hello numero di istanze in un tipo di risorsa supportati è basato sull'ora del giorno e/o caricamento dati (metrici) utilizzando un'impostazione di scalabilità automatica. Quando vengono soddisfatte le condizioni di hello tooscale verso l'alto o verso il basso, hello start e ha avuto esito positivo o gli eventi non riusciti verranno registrati in questa categoria.

### <a name="sample-event"></a>Evento di esempio
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Descrizioni delle proprietà
| Nome dell'elemento | Descrizione |
| --- | --- |
| caller | Sempre Microsoft.Insights/autoscaleSettings |
| channels | Sempre "Admin, Operation" |
| claims | Blob JSON con tipo di nome SPN (service principal name) o risorse del motore di scalabilità automatica hello hello. |
| correlationId | Un GUID in formato stringa hello. |
| description |Descrizione di testo statico dell'evento di scalabilità automatica hello. |
| eventDataId |Identificatore univoco dell'evento di scalabilità automatica hello. |
| level |Livello dell'evento hello. Uno dei seguenti valori hello: "Critical", "Error", "Avviso", "Informational" e "Verbose" |
| resourceGroupName |Nome del gruppo di risorse hello per l'impostazione di scalabilità automatica hello. |
| resourceProviderName |Nome del provider di risorse hello per l'impostazione di scalabilità automatica hello. |
| resourceId |Id risorsa dell'impostazione di scalabilità automatica hello. |
| operationId |Un GUID condiviso tra eventi di hello corrispondenti tooa singola operazione. |
| operationName |Nome dell'operazione di hello. |
| properties |Set di `<Key, Value>` coppie (dizionario) che descrive hello dettagli dell'evento hello. |
| properties.Description | Descrizione dettagliata di quali motore di scalabilità automatica hello stava eseguendo. |
| properties.ResourceName | ID di risorsa di hello interessati risorse (hello risorsa su cui hello l'esecuzione dell'azione di ridimensionamento) |
| properties.OldInstancesCount | numero di Hello di istanze prima azione di scalabilità automatica hello ha effetto. |
| properties.NewInstancesCount | numero di Hello di istanze dopo l'azione di scalabilità automatica hello ha effetto. |
| properties.LastScaleActionTime | Hello timestamp di quando è eseguita hello azione di scalabilità automatica. |
| status |Stringa che descrive lo stato di hello dell'operazione di hello. Alcuni dei valori comuni sono: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | In genere null per il ridimensionamento automatico. |
| eventTimestamp |Timestamp dell'evento hello è stato generato da hello di elaborazione del servizio Azure hello richiesta evento hello corrispondente. |
| submissionTimestamp |Timestamp dell'evento hello è diventato disponibile per l'esecuzione di query. |
| subscriptionId |ID sottoscrizione di Azure. |

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni su hello Log attività (in precedenza i log di controllo)](monitoring-overview-activity-logs.md)
* [Flusso hello Log attività Azure tooEvent hub](monitoring-stream-activity-logs-event-hubs.md)
