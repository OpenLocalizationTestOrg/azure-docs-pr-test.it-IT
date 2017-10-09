---
title: API REST degli avvisi di OMS Log Analitica aaaUsing
description: Hello Log Analitica avviso REST API consente toocreate e gestire gli avvisi in Analitica di Log che fa parte di Operations Management Suite (OMS).  Questo articolo fornisce informazioni dettagliate di hello API e alcuni esempi per l'esecuzione di diverse operazioni.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Creare e gestire regole di avviso in Log Analytics con l'API REST
Hello Log Analitica avviso REST API consente toocreate e gestire gli avvisi in Operations Management Suite (OMS).  Questo articolo fornisce informazioni dettagliate di hello API e alcuni esempi per l'esecuzione di diverse operazioni.

API REST di ricerca di Log Analitica Hello è RESTful e accessibile tramite hello REST API di gestione risorse di Azure. In questo documento sono disponibili esempi in cui hello API viene usata da una riga di comando di PowerShell usando [ARMClient](https://github.com/projectkudu/ARMClient), uno strumento della riga di comando open source che semplifica la chiamata hello API di gestione risorse di Azure. uso di Hello di ARMClient e PowerShell è una delle numerose opzioni tooaccess hello API di ricerca Log Analitica. Con questi strumenti è possibile utilizzare le aree di lavoro di hello API di gestione risorse di Azure RESTful toomake chiamate tooOMS ed eseguire i comandi di ricerca al loro interno. Hello API restituiscono tooyou risultati di ricerca in formato JSON, che consente i risultati della ricerca toouse hello in molti modi diversi a livello di codice.

## <a name="prerequisites"></a>Prerequisiti
Attualmente, gli avvisi possono essere creati solo con una ricerca salvata in Log Analytics.  È possibile fare riferimento toohello [API REST di ricerca Log](log-analytics-log-search-api.md) per ulteriori informazioni.

## <a name="schedules"></a>Pianificazioni
Una ricerca salvata può avere una o più pianificazioni. Hello pianificazione definisce la frequenza con cui hello ricerca viene eseguita e viene identificato l'intervallo di tempo hello su quali criteri hello.
Le pianificazioni sono proprietà hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Interval |La frequenza con cui hello ricerca viene eseguita. Il valore è espresso in minuti. |
| QueryTimeSpan |intervallo di tempo Hello su quale hello viene valutata criteri. Deve essere maggiore di intervallo tooor uguale. Il valore è espresso in minuti. |
| Versione |Hello versione API utilizzata.  Attualmente, questo deve sempre essere impostato too1. |

Si consideri ad esempio una query eventi con Interval pari a 15 minuti e Timespan pari a 30 minuti. In questo caso, query hello verrebbe eseguito ogni 15 minuti e potrebbe essere generato un avviso se i criteri di hello continuassero tooresolve tootrue in un intervallo di 30 minuti.

### <a name="retrieving-schedules"></a>Recupero delle pianificazioni
Hello utilizzare ottenere tooretrieve metodo tutte le pianificazioni per una ricerca salvata.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Metodo con un tooretrieve ID pianificazione hello utilizzare Get una determinata pianificazione per una ricerca salvata.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Di seguito è riportata una risposta di esempio per una pianificazione.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Creazione di una pianificazione
Utilizzare il metodo Put hello con un toocreate ID pianificazione univoca una nuova pianificazione.  Si noti che due pianificazioni non possono avere hello lo stesso ID, anche se sono associate con diverse ricerche salvate.  Quando si crea una pianificazione nella console OMS hello, viene creato un GUID per l'ID di pianificazione hello.

> [!NOTE]
> nome Hello per le ricerche salvate tutte, pianificazioni e le azioni create con hello Log Analitica API deve essere in lettere minuscole.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Modifica di una pianificazione
Utilizzare il metodo Put hello con una pianificazione esistente ID per hello stesso salvato ricerca toomodify che pianifica.  il corpo di Hello di hello richiesta deve includere hello etag della pianificazione hello.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Eliminazione delle pianificazioni
Utilizzare il metodo di eliminazione hello con un toodelete ID pianificazione una pianificazione.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Azioni
Una pianificazione può avere più azioni. Un'azione può definire uno o più tooperform processi, ad esempio l'invio di un messaggio di posta o l'avvio di un runbook, o è possibile definire una soglia che determina quando risultati hello di una ricerca corrispondono a certi criteri.  Alcune azioni verranno definiti sia in modo che i processi di hello vengono eseguiti quando viene raggiunta la soglia di hello.

Tutte le azioni sono proprietà hello in hello nella tabella seguente.  I vari tipi di avvisi hanno diverse proprietà aggiuntive che sono descritte di seguito.

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |Tipo di azione hello.  I valori possibili hello non sono attualmente gli avvisi e Webhook. |
| Nome |Nome visualizzato per l'avviso hello. |
| Versione |Hello versione API utilizzata.  Attualmente, questo deve sempre essere impostato too1. |

### <a name="retrieving-actions"></a>Recupero delle azioni
Hello utilizzare ottenere tooretrieve metodo tutte le azioni per una pianificazione.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Metodo con hello azione ID tooretrieve hello utilizzare Get una determinata azione per una pianificazione.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Creazione o modifica di azioni
Utilizzare il metodo Put hello con un ID azione toohello univoco pianificazione toocreate una nuova azione.  Quando si crea un'azione nella console OMS hello, un GUID è per ID hello azione.

> [!NOTE]
> nome Hello per le ricerche salvate tutte, pianificazioni e le azioni create con hello Log Analitica API deve essere in lettere minuscole.

Utilizzare il metodo Put hello con una ID per hello stesso salvato ricerca toomodify che pianifica delle azioni esistente.  il corpo di Hello di hello richiesta deve includere hello etag della pianificazione hello.

formato della richiesta per la creazione di una nuova azione Hello varia in base al tipo di azione in modo da questi esempi sono forniti nelle sezioni hello.

### <a name="deleting-actions"></a>Eliminazione delle azioni
Utilizzare il metodo di eliminazione hello con hello azione ID toodelete un'azione.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Azioni di avviso
Una pianificazione deve avere una sola azione di avviso.  Azioni avviso presentano uno o più delle sezioni hello hello nella tabella seguente.  Ciascuna è descritta in dettaglio di seguito.

| Sezione | Descrizione |
|:--- |:--- |
| Soglia |Criteri di esecuzione azione hello. |
| EmailNotification |Inviare posta elettronica ai destinatari toomultiple. |
| Correzione |Avvia un runbook in automazione di Azure tooattempt toocorrect identificato problema. |

#### <a name="thresholds"></a>Soglie
Un’azione di avviso deve avere una sola soglia.  Quando una ricerca salvata hello risultati corrispondano a soglia hello in un'azione associata con la ricerca, vengono eseguiti tutti gli altri processi in tale azione.  Inoltre, un'azione può contenere solo una soglia, in modo da poter essere utilizzata con azioni di altri tipi che non contengono soglie.

Le soglie dispongono di proprietà di hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| operatore |Operatore di confronto tra le soglie hello. <br> gt = Maggiore di <br> lt = minore di |
| Valore |Valore di soglia hello. |

Si consideri ad esempio una query eventi con Interval pari a 15 minuti, Timespan pari a 30 minuti e Threshold maggiore di 10. In questo caso, query hello verrebbe eseguito ogni 15 minuti e potrebbe essere generato un avviso se restituito 10 eventi creati in un intervallo di 30 minuti.

Di seguito è riportata una risposta di esempio per un'azione con una sola soglia.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione di soglia.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione di soglia esistente.  il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Notifica tramite posta elettronica
Notifiche di posta elettronica inviano tooone di posta elettronica o altri destinatari.  Sono incluse proprietà hello nelle hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| Recipients |Elenco di indirizzi di posta elettronica. |
| Oggetto |oggetto Hello di posta elettronica hello. |
| Attachment |Gli allegati non sono attualmente supportati, pertanto il valore corrispondente sarà sempre "None". |

Di seguito è riportata una risposta di esempio per un'azione di notifica di posta elettronica con una determinata soglia.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione di posta elettronica.  Hello seguente viene creata una notifica di posta elettronica con una soglia di posta elettronica hello viene inviato quando i risultati di hello della ricerca salvata hello superano la soglia di hello.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione di posta elettronica esistente.  il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Azioni correttive
Correzioni di avviare un runbook in automazione di Azure che tenta di problema hello toocorrect identificato dall'avviso hello.  È necessario creare un webhook per runbook hello utilizzato in un'azione correttiva e quindi specificare hello URI nella proprietà WebhookUri hello.  Quando si crea questa azione utilizzando la console di OMS hello, viene creato automaticamente un nuovo webhook per hello runbook.

Correzioni includono le proprietà di hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| RunbookName |Nome del runbook hello. Deve corrispondere un runbook pubblicato nell'account di automazione hello configurato nella soluzione di automazione nell'area di lavoro OMS hello. |
| WebhookUri |URI del webhook hello. |
| Expiry |Data di scadenza Hello e l'ora di hello webhook.  Se hello webhook non dispone di una scadenza, questo può essere una data futura valida. |

Di seguito è riportata una risposta di esempio per un'azione correttiva con una determinata soglia.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione di correzione.  Hello seguente viene creato un monitoraggio e aggiornamento con una soglia in modo hello runbook viene avviato quando risultati hello della ricerca salvata hello superano la soglia di hello.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione correttiva esistente.  il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Esempio
Di seguito è toocreate un esempio completo in un nuovo avviso di posta elettronica.  Verrà creata una nuova pianificazione con un'azione contenente una soglia e un messaggio di posta elettronica.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Azioni webhook
Le azioni Webhook avviano un processo chiamando un URL e fornendo facoltativamente toobe un payload inviato.  Sono azioni tooRemediation simili, ma sono disponibili solo per webhook che può richiamare processi diversi dai runbook di automazione di Azure.  Forniscono anche l'opzione aggiuntiva di hello di fornire un processo di payload recapitati toobe toohello remoto.

Le azioni Webhook non dispone di una soglia, ma invece devono essere aggiunti pianificazione tooa con un'azione con una soglia di avviso.  È possibile aggiungere più azioni Webhook che verranno tutti eseguite quando viene raggiunta la soglia di hello.

Le azioni Webhook includono le proprietà di hello in hello nella tabella seguente.

| Proprietà | Descrizione |
|:--- |:--- |
| WebhookUri |oggetto Hello di posta elettronica hello. |
| CustomPayload |Payload personalizzato toobe inviati toohello webhook.  formato Hello dipenderà quali webhook hello è previsto. |

Di seguito è riportato un esempio di risposta per un’azione webhook e un'azione di avviso associata con una determinata soglia.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Creazione o modifica di un’azione webhook
Per una pianificazione, utilizzare il metodo Put hello con un toocreate ID azione univoci una nuova azione webhook.  Hello seguente viene creato un Webhook di azione e un avviso con una soglia in modo che webhook hello verrà attivata quando risultati hello della ricerca salvata hello superano la soglia di hello.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Per una pianificazione, utilizzare il metodo Put hello con un toomodify di ID azione un'azione webhook esistente.  il corpo di Hello di hello richiesta deve includere hello etag dell'azione hello.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Passaggi successivi
* Hello utilizzare [ricerche nei log tooperform API REST](log-analytics-log-search-api.md) nel Log Analitica.

