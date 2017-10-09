---
title: tooalerts aaaResponses in OMS Log Analitica | Documenti Microsoft
description: Gli avvisi nel registro Analitica identificare importanti informazioni nel repository OMS e in modo proattivo ricevere una notifica di problemi o richiamare azioni tooattempt toocorrect li.  In questo articolo viene descritto come toocreate una regola di avviso e azioni diverse a dettagli hello possono assumere.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a>Aggiungere regole di tooalert azioni nel registro Analitica
Quando un [viene creato l'avviso nel Log Analitica](log-analytics-alerts.md), è possibile hello [configurazione regola di avviso hello](log-analytics-alerts.md) tooperform una o più azioni.  Questo articolo descrive hello diverse azioni che sono disponibili e i dettagli sulla configurazione di ogni tipo.

| Azione | Descrizione |
|:--|:--|
| [Indirizzo di posta elettronica](#email-actions) | Invia un messaggio di posta elettronica con i dettagli di hello di hello avviso tooone o altri destinatari. |
| [Webhook](#webhook-actions) | Richiamare un processo esterno tramite una singola richiesta HTTP POST. |
| [Runbook](#runbook-actions) | Avviare un runbook in Automazione di Azure. |


## <a name="email-actions"></a>Azioni di posta elettronica
Azioni di posta elettronica Invia messaggio di posta elettronica con i dettagli di hello di hello avviso tooone o altri destinatari.  È possibile specificare l'oggetto hello del messaggio di posta elettronica hello, ma il contenuto è un formato standard costruito dal Log Analitica.  Include informazioni di riepilogo, ad esempio nome hello di avviso hello toodetails aggiunta di record tooten restituito dalla ricerca log hello.  Include inoltre una ricerca di log tooa collegamento in Analitica di Log che verrà restituito l'intero set di record di hello dalla query.   Hello mittente del messaggio di posta elettronica hello è *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* . 

Messaggio di posta elettronica azioni richiedono proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Oggetto |Nel messaggio di posta elettronica hello del soggetto.  È possibile modificare il corpo di hello del messaggio di posta elettronica hello. |
| Destinatari |Indirizzi di tutti i destinatari di posta elettronica.  Se si specifica più di un indirizzo, quindi gli indirizzi di hello separato con un punto e virgola (;). |


## <a name="webhook-actions"></a>Azioni webhook

Le azioni Webhook consentono tooinvoke un processo esterno tramite una singola richiesta HTTP POST.  servizio Hello chiamato deve supportare webhook e determinare come verrà utilizzato alcun payload riceve.  È anche possibile chiamare un'API REST che non supportano in modo specifico webhook come richiesta di hello è in un formato che hello che riconosce API.  Esempi di utilizzo di un webhook nell'avviso tooan risposta invia un messaggio [Slack](http://slack.com) o la creazione di un evento imprevisto in [PagerDuty](http://pagerduty.com/).  Una procedura dettagliata completa di creazione di una regola di avviso con un margine di flessibilità di toocall webhook è disponibile all'indirizzo [Webhook negli avvisi di Log Analitica](log-analytics-alerts-webhooks.md).

Le azioni Webhook richiedono proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| URL webhook |Hello l'URL del webhook hello. |
| Payload JSON personalizzato |Payload personalizzato toosend con hello webhook.  Vedere di seguito per altri dettagli. |


Un payload in formato JSON che dati hello inviato servizio esterno toohello Webhook includono un URL.  Per impostazione predefinita, il payload di hello includerà i valori hello hello nella tabella seguente.  È possibile scegliere tooreplace il payload con uno personalizzato personalizzati.  In tal caso è possibile utilizzare le variabili di hello nella tabella hello per ognuna delle hello parametri tooinclude al relativo valore nel payload personalizzato.

| . | Variabile | Descrizione |
|:--- |:--- |:--- |
| AlertRuleName |#alertrulename |Nome della regola di avviso hello. |
| AlertThresholdOperator |#thresholdoperator |Operatore di soglia per la regola di avviso hello.  *Maggiore di* o *Minore di*. |
| AlertThresholdValue |#thresholdvalue |Valore di soglia per la regola di avviso hello. |
| LinkToSearchResults |#linktosearchresults |Collegamento tooLog Analitica Registro ricerca che restituisce i record di hello dalla query hello hello avviso creato. |
| ResultCount |#searchresultcount |Numero di record nei risultati della ricerca hello. |
| SearchIntervalEndtimeUtc |#searchintervalendtimeutc |Ora di fine per la query hello in formato UTC. |
| SearchIntervalInSeconds |#searchinterval |Intervallo di tempo per la regola di avviso hello. |
| SearchIntervalStartTimeUtc |#searchintervalstarttimeutc |Ora di inizio per la query hello in formato UTC. |
| SearchQuery |#searchquery |Query di ricerca di log utilizzato dalla regola di avviso hello. |
| SearchResults |Vedere di seguito |Record restituiti dalla query hello in formato JSON.  Limitato toohello innanzitutto 5.000 record. |
| WorkspaceID |#workspaceid |ID dell'aea di lavoro di OMS. |

Ad esempio, è possibile specificare hello seguente payload personalizzato che include un singolo parametro chiamato *testo*.  Questo parametro si aspetta servizio Hello che chiama questo webhook.

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

Il payload di esempio risolverebbe toosomething come hello seguenti quando inviato toohello webhook.

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

risultati della ricerca tooinclude in un payload personalizzato, aggiungere hello successiva riga come proprietà di livello superiore in payload json hello.  

    "IncludeSearchResults":true

Ad esempio, un payload personalizzato che include solo nome avviso hello e i risultati della ricerca hello toocreate, è possibile utilizzare hello seguente. 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


È possibile eseguire un esempio completo di creazione di una regola di avviso con toostart un webhook di un servizio esterno in [creare un'azione webhook avviso in OMS Log Analitica toosend messaggio tooSlack](log-analytics-alerts-webhooks.md).

## <a name="runbook-actions"></a>Azioni runbook
Le azioni runbook avviano un runbook in Automazione di Azure.  In ordine toouse questo tipo di azione, è necessario disporre di hello [soluzione di automazione](log-analytics-add-solutions.md) installato e configurato nell'area di lavoro OMS.  È possibile selezionare hello runbook nell'account di automazione hello configurato nella soluzione di automazione hello.

Azioni runbook richiedono proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:---|
| Runbook | Runbook che si desidera toostart quando viene creato un avviso. |
| Esegui in | Specificare **Azure** toorun hello runbook nel cloud hello.  Specificare **worker ibrido** toorun hello runbook su un agente con [Runbook Worker ibrido](../automation/automation-hybrid-runbook-worker.md ) installato.  |

Azioni runbook avviano runbook hello con un [webhook](../automation/automation-webhooks.md).  Quando si crea una regola di avviso hello, verrà creato automaticamente un nuovo webhook per hello runbook con il nome di hello **OMS avviso correzione** seguito da un GUID.  

Non è direttamente possibile popolare i parametri di runbook hello ma hello [$WebhookData parametro](../automation/automation-webhooks.md) include hello dettagli dell'avviso hello, inclusi hello risultati della ricerca log hello che li ha creati.  runbook Hello sarà necessario toodefine **$WebhookData** come parametro per tale tooaccess hello proprietà dell'avviso hello.  Hello avviso dati sono disponibili in formato json in una singola proprietà denominata **SearchResults** in hello **RequestBody** proprietà di **$WebhookData**.  Questa operazione avrà le proprietà di hello in hello nella tabella seguente.

| Nodo | Description |
|:--- |:--- |
| id |Percorso e il GUID della ricerca hello. |
| __metadata |Informazioni su hello avviso inclusi hello numero di record e lo stato dei risultati della ricerca hello. |
| value |Voce separata per ogni record nei risultati della ricerca hello.  Dettagli Hello della voce hello corrisponderà hello proprietà e i valori del record di hello. |

Ad esempio, hello runbook seguente sarebbe estrarre record hello restituiti dalla ricerca nei log hello e assegnare proprietà diverse in base al tipo di hello di ogni record.  Si noti che runbook hello viene avviato tramite la conversione **RequestBody** da json in modo che non possono essere gestiti come un oggetto in PowerShell.

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a>Passaggi successivi
- Completare una procedura dettagliata per la [configurazione di un webhook](log-analytics-alerts-webhooks.md) con una regola di avviso.  
- Informazioni su come toowrite [i runbook in automazione di Azure](https://azure.microsoft.com/documentation/services/automation) tooremediate problemi identificati tramite gli avvisi.
