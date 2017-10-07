---
title: webhook aaaConfigure avvisi metrica Azure | Documenti Microsoft
description: Reindirizza i sistemi non Azure tooother gli avvisi di Azure.
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Configurare un webhook in un avviso relativo alle metriche di Azure
Webhook consentono di Azure tooroute sistemi tooother di notifica per le azioni di post-elaborazione o personalizzati di avviso. È possibile utilizzare un webhook su un avviso tooroute è tooservices che invia SMS, registrare i bug, inviare una notifica di un team tramite servizi di chat o messaggistica o eseguire un numero qualsiasi di altre azioni. Questo articolo viene descritto come tooset un webhook su un avviso di metriche di Azure e il payload di hello per hello HTTP POST tooa webhook è simile. Per informazioni sull'installazione di hello e dello schema per un avviso di Log attività di Azure (avviso sugli eventi), [questa pagina viene visualizzata invece](insights-auditlog-to-webhook-email.md).

Contenuto di avviso hello HTTP POST in formato JSON, gli avvisi di Azure schema definito di sotto, tooa webhook URI fornito durante la creazione di avviso hello. L'URI deve essere un endpoint HTTP o HTTPS valido. Azure inserisce una voce per ogni richiesta quando viene attivato un avviso.

## <a name="configuring-webhooks-via-hello-portal"></a>Configurazione dei webhook tramite il portale di hello
È possibile aggiungere o aggiornare hello webhook URI nella schermata di creazione/aggiornamento avvisi hello in hello [portale](https://portal.azure.com/).

![Aggiungere una regola di avviso](./media/insights-webhooks-alerts/Alertwebhook.png)

È inoltre possibile configurare un webhook tooa toopost avviso URI utilizzando hello [i cmdlet di PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [CLI multipiattaforma](insights-cli-samples.md#work-with-alerts), o [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>L'autenticazione hello webhook
Hello webhook autenticazione utilizzando l'autorizzazione basata su token. Hello webhook URI viene salvato con un ID del token, ad esempio. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Schema del payload
operazione POST Hello contiene hello seguito payload JSON e lo schema per gli avvisi basati sulla metrica.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Campo | Mandatory | Set fisso di valori | Note |
|:--- |:--- |:--- |:--- |
| status |S |"Activated", "Resolved" |Stato di avviso hello in base alle condizioni di hello è stata impostata. |
| context |S | |contesto dell'avviso Hello. |
| timestamp |S | |ora di Hello in cui hello è stato generato l'avviso. |
| id |S | |Ogni regola di avviso ha un ID univoco. |
| name |S | |nome dell'avviso Hello. |
| description |S | |Descrizione dell'avviso hello. |
| conditionType |S |"Metric", "Event" |Sono supportati due tipi di avviso, Uno basato su una condizione di metrica e hello quella basata su un evento nel registro attività hello. Utilizzare toocheck questo valore se avviso hello è basato su eventi o di metrica. |
| condition |S | |Hello toocheck campi specifici per in base alle proprietà conditionType hello. |
| metricName |Per avvisi relativi alle metriche | |Controlla nome Hello della metrica di hello che definisce la regola di hello. |
| metricUnit |Per avvisi relativi alle metriche |"Bytes", "BytesPerSecond", "Count", "CountPerSecond", "Percent", "Seconds" |unità di Hello consentito nella metrica hello. [I valori consentiti sono elencati qui](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |Per avvisi relativi alle metriche | |valore effettivo di Hello della metrica hello che ha causato hello avviso. |
| threshold |Per avvisi relativi alle metriche | |valore di soglia Hello in cui hello viene attivato l'avviso. |
| windowSize |Per avvisi relativi alle metriche | |periodo di Hello di tempo in cui viene utilizzato toomonitor dell'attività degli avvisi in base alla soglia hello. Deve essere compreso tra 5 minuti e 1 giorno. Il formato della durata è conforme a ISO 8601. |
| timeAggregation |Per avvisi relativi alle metriche |"Average", "Last", "Maximum", "Minimum", "None", "Total" |Come hello i dati raccolti devono essere combinati nel tempo. valore predefinito di Hello è Media. [I valori consentiti sono elencati qui](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operator |Per avvisi relativi alle metriche | |Utilizzare l'operatore di Hello toocompare hello dati di metrica toohello set soglia corrente. |
| subscriptionId |S | |ID sottoscrizione di Azure. |
| resourceGroupName |S | |Nome del gruppo di risorse hello per hello influisce sulle risorse. |
| resourceName |S | |Nome di risorsa di hello influisce sulle risorse. |
| resourceType |S | |Tipo di risorsa di hello influisce sulle risorse. |
| resourceId |S | |ID di risorsa di hello influisce sulle risorse. |
| resourceRegion |S | |Area o un percorso di hello influisce sulle risorse. |
| portalLink |S | |Pagina Riepilogo risorse portale toohello collegamento diretto. |
| properties |N |Facoltativo |Set di `<Key, Value>` coppie (ad esempio `Dictionary<String, String>`) che include i dettagli sull'evento hello. campo di proprietà Hello è facoltativo. Personalizzata dell'interfaccia utente o la logica basata su app del flusso di lavoro, gli utenti possono immettere chiave/valore che può essere passati tramite payload hello. Hello alternativa toopass proprietà personalizzate toohello indietro webhook è tramite hello webhook uri stesso (come parametri di query) |

> [!NOTE]
> campo di proprietà Hello può essere impostato solo tramite hello [API REST di Azure monitoraggio](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni su avvisi di Azure e ai webhook video hello [integrare gli avvisi di Azure con PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Eseguire gli script di Automazione di Azure (runbook) sugli avvisi di Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Utilizzare la logica App toosend un SMS tramite Twilio da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Utilizzare la logica App toosend un margine di flessibilità messaggio da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Utilizzare la logica App toosend tooan un messaggio della coda di Azure da un avviso di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
