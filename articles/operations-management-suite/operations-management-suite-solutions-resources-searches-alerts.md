---
title: aaaSaved ricerche e avvisi in soluzioni OMS | Documenti Microsoft
description: "Soluzioni in OMS in genere comprendono le ricerche salvate nei dati tooanalyze Analitica Log raccolti dalla soluzione hello.  Si può anche definire utente hello toonotify di avvisi o automaticamente intervenire in problema grave di risposta tooa.  In questo articolo viene descritto come toodefine Analitica registro salvato avvisi e ricerche in un modello ARM in modo che possano essere incluse nelle soluzioni di gestione."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Aggiunta Log Analitica salvato tooOMS ricerche e gli avvisi la soluzione di gestione (anteprima)

> [!NOTE]
> Questa è una documentazione preliminare per la creazione di soluzioni di gestione in OMS attualmente disponibili in versione di anteprima. Qualsiasi schema descritto di seguito è soggetto toochange.   


[Soluzioni di gestione in OMS](operations-management-suite-solutions.md) includerà in genere [ricerche salvate](../log-analytics/log-analytics-log-searches.md) nei dati tooanalyze Analitica Log raccolti dalla soluzione hello.  Possono anche definire [avvisi](../log-analytics/log-analytics-alerts.md) toonotify hello utente o eseguire automaticamente azioni problema critico tooa di risposta.  In questo articolo viene descritto come toodefine Analitica Log salvate ricerche e avvisi in un [modello di gestione delle risorse](../resource-manager-template-walkthrough.md) in modo che possano essere incluse [soluzioni di gestione](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Hello esempi in questo articolo utilizzano parametri e variabili che sono entrambe soluzioni toomanagement necessarie o comuni e descritte in [la creazione di soluzioni di gestione in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone che si ha già familiarità con come troppo[creare una soluzione di gestione](operations-management-suite-solutions-creating.md) e la struttura di hello di un [modello ARM](../resource-group-authoring-templates.md) e file di soluzione.


## <a name="log-analytics-workspace"></a>Area di lavoro di Log Analytics
Tutte le risorse in Log Analytics sono contenute in un'[area di lavoro](../log-analytics/log-analytics-manage-access.md).  Come descritto in [OMS dell'area di lavoro e account di automazione](operations-management-suite-solutions.md#oms-workspace-and-automation-account) dell'area di lavoro di hello non è incluso nella soluzione di gestione di hello ma deve essere presente prima di installata la soluzione hello.  Se non è disponibile, l'installazione di soluzioni hello avrà esito negativo.

nome Hello dell'area di lavoro hello è nome hello di ogni risorsa Analitica di Log.  Questa operazione viene eseguita nella soluzione hello con hello **dell'area di lavoro** parametro come hello seguente esempio di una risorsa savedsearch.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Ricerche salvate
Includere [ricerche salvate](../log-analytics/log-analytics-log-searches.md) in una soluzione tooallow utenti tooquery di dati raccolti dalla soluzione.  Ricerche salvate verranno visualizzato in **Preferiti** nel portale OMS hello e **ricerche salvate** in hello portale di Azure.  È necessaria una ricerca salvata anche per ogni avviso.   

[Ricerca salvata Analitica log](../log-analytics/log-analytics-log-searches.md) risorse hanno un tipo di `Microsoft.OperationalInsights/workspaces/savedSearches` e hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Ogni proprietà hello di una ricerca salvata sono descritti nella seguente tabella hello. 

| Proprietà | Descrizione |
|:--- |:--- |
| category | categoria di Hello per la ricerca salvata hello.  Le ricerche salvate nella stessa soluzione spesso condividono hello un'unica categoria pertanto vengono raggruppati insieme nella console di hello. |
| displayname | Nome toodisplay per hello ricerca salvata nel portale di hello. |
| query | Eseguire una query toorun. |

> [!NOTE]
> Caratteri di escape toouse nella query hello potrebbe essere necessario se include caratteri che potrebbero essere interpretati come JSON.  Ad esempio, se la query è stata **OperationName:"Microsoft.Compute/virtualMachines/write tipo: AzureActivity"**, devono essere scritti nel file di soluzione hello come **OperationName tipo: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Avvisi
Gli [avvisi di Log Analytics](../log-analytics/log-analytics-alerts.md) vengono creati da regole di avviso che eseguono una ricerca salvata a intervalli regolari.  Se i risultati di hello di hello query corrispondono ai criteri specificati, viene creato un record di avviso e vengono eseguite uno o più azioni.  

Le regole di avviso in una soluzione di gestione sono costituite da hello seguenti tre risorse diverse.

- **Ricerca salvata.**  Definisce una ricerca nei log hello che verrà eseguita.  Una singola ricerca salvata può essere condivisa da più regole di avviso.
- **Pianificazione.**  Definisce la frequenza con cui hello ricerca nei log verrà eseguito.  Ogni regola di avviso avrà una sola pianificazione.
- **Azione di avviso.**  Ogni regola di avviso avrà una risorsa di azione con un tipo di **avviso** che definisce i dettagli di hello di hello avviso, ad esempio criteri hello verrà creato un record di avviso e hello gravità dell'avviso.  risorsa dell'azione Hello definirà facoltativamente una risposta di posta elettronica e il runbook.
- **Azione webhook (facoltativa).**  Se la regola di avviso hello chiamerà un webhook, quindi richiede una risorsa di un'ulteriore azione con un tipo di **Webhook**.    

Le risorse ricerca salvata sono illustrate sopra.  Hello altre risorse sono descritti di seguito.


### <a name="schedule-resource"></a>Risorsa pianificazione

Una ricerca salvata può avere una o più pianificazioni, ognuna delle quali rappresenta una regola di avviso separata. Hello pianificazione definisce la frequenza con cui hello ricerca viene eseguita e hello intervallo di tempo su cui hello vengono recuperati i dati.  Risorse di pianificazione dispongono di un tipo di `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` e hello seguente struttura. Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



Nella hello nella tabella seguente sono descritte le proprietà di Hello per le risorse di pianificazione.

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| Enabled       | Sì | Specifica se l'avviso di hello è abilitato quando viene creato. |
| interval      | Sì | La frequenza con cui hello query viene eseguita in pochi minuti. |
| queryTimeSpan | Sì | Periodo di tempo in minuti in base alla quale tooevaluate. |

risorse di pianificazione Hello dovrebbero dipendere hello ricerca salvata in modo che viene creato prima pianificazione hello.


### <a name="actions"></a>Azioni
Esistono due tipi di risorsa dell'azione specificata da hello **tipo** proprietà.  Una pianificazione richiede una **avviso** azione che definisce i dettagli di hello di regola di avviso hello e le azioni eseguite quando viene creato un avviso.  Può inoltre includere un **Webhook** azione se un webhook deve essere chiamato dall'avviso hello.  

Le risorse azione sono di tipo `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Azioni di avviso

Ogni pianificazione avrà un'azione **Alert**,  Definisce i dettagli di hello di avviso hello e, facoltativamente, le azioni di notifica e monitoraggio e aggiornamento.  Una notifica invia un messaggio di posta elettronica tooone o più indirizzi.  Una risoluzione avvia un runbook problema rilevato hello tooremediate tooattempt di automazione di Azure.

Le azioni avviso hanno hello seguente struttura.  Questo include variabili e parametri comuni che è possibile copiare e incollare il frammento di codice nel file di soluzione e modificare i nomi di parametro hello. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

Nella hello le tabelle seguenti sono descritte le proprietà di Hello per le risorse di azione di allarme.

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| Type | Sì | Tipo di azione hello.  Per le azioni di avviso, sarà **Alert**. |
| Nome | Sì | Nome visualizzato per l'avviso hello.  Si tratta di nome hello che viene visualizzato nella console di hello per regola di avviso hello. |
| Descrizione | No | Descrizione facoltativa dell'avviso hello. |
| Severity | Sì | Gravità di record di avviso hello da hello seguenti valori:<br><br> **Critical**<br>**Warning**<br>**Informational** |


##### <a name="threshold"></a>Soglia
Questa sezione è obbligatoria  Definisce le proprietà di hello di soglia di avviso hello.

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| Operatore | Sì | Operatore per il confronto di hello da hello seguenti valori:<br><br>**gt = maggiore di<br>lt = minore di** |
| Valore | Sì | risultati di hello toocompare valore Hello. |


##### <a name="metricstrigger"></a>MetricsTrigger
Questa sezione è facoltativa.  Includere la sezione per un avviso di misurazione delle metriche.

> [!NOTE]
> Gli avvisi di misurazione delle metriche sono attualmente disponibili in anteprima pubblica. 

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| TriggerCondition | Sì | Specifica se la soglia hello è per il numero totale di violazioni della sicurezza o violazioni consecutivi da hello seguenti valori:<br><br>**Total<br>Consecutive** |
| Operatore | Sì | Operatore per il confronto di hello da hello seguenti valori:<br><br>**gt = maggiore di<br>lt = minore di** |
| Valore | Sì | Numero di hello volte hello criteri deve essere avviso hello tootrigger soddisfatto. |

##### <a name="throttling"></a>Limitazione
Questa sezione è facoltativa.  Includere questa sezione se si desidera ricevere avvisi relativi toosuppress da hello stessa regola per un periodo di tempo dopo la creazione di un avviso.

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| DurationInMinutes | Sì, se è incluso l'elemento Throttling | Numero di minuti toosuppress avvisi dopo uno dal hello viene creata la regola di avviso stesso. |

##### <a name="emailnotification"></a>EmailNotification
 In questa sezione è facoltativa Include se si desidera hello avviso toosend tooone di posta elettronica o altri destinatari.

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| Destinatari | Sì | Elenco delimitato da virgole di posta elettronica indirizzi toosend notifica quando un avviso viene creato come nel seguente esempio hello.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Oggetto | Sì | Oggetto riga del messaggio di posta elettronica hello. |
| Attachment | No | Gli allegati non sono attualmente supportati.  Se questo elemento è incluso, il valore dovrà essere **None**. |


##### <a name="remediation"></a>Correzione
Questa sezione è facoltativa se si desidera che un runbook toostart nell'avviso toohello risposta Include. |

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| RunbookName | Sì | Nome di hello runbook toostart. |
| WebhookUri | Sì | URI del webhook hello per hello runbook. |
| Expiry | No | Data e ora in cui monitoraggio e aggiornamento hello scadenza. |

#### <a name="webhook-actions"></a>Azioni webhook

Le azioni Webhook avviano un processo chiamando un URL e fornendo facoltativamente toobe un payload inviato. Sono azioni tooRemediation simili, ma sono disponibili solo per webhook che può richiamare processi diversi dai runbook di automazione di Azure. Forniscono anche l'opzione aggiuntiva di hello di fornire un processo di payload recapitati toobe toohello remoto.

Se l'avviso chiamerà un webhook, quindi è necessario una risorsa di azione con un tipo di **Webhook** in aggiunta toohello **avviso** risorsa dell'azione.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

proprietà Hello per le risorse di azione Webhook sono descritte in hello le tabelle seguenti.

| Nome dell'elemento | Obbligatorio | Descrizione |
|:--|:--|:--|
| type | Sì | Tipo di azione hello.  Per le azioni webhook, sarà **Webhook**. |
| name | Sì | Nome visualizzato per l'azione di hello.  Non è visualizzato nella console di hello. |
| wehookUri | Sì | URI per il webhook hello. |
| customPayload | No | Payload personalizzato toobe inviati toohello webhook. formato Hello dipenderà quali webhook hello è previsto. |




## <a name="sample"></a>Esempio

Ecco un esempio di una soluzione che includono che include hello seguenti risorse:

- Ricerca salvata
- Pianificazione
- Azione di avviso
- Azione webhook

esempio utilizza Hello [parametri soluzione standard](operations-management-suite-solutions-solution-file.md#parameters) variabili comunemente utilizzati in una soluzione come anziché valori toohardcoding nelle definizioni di risorse hello.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Hello seguenti il file di parametro fornisce i valori di esempi per questa soluzione.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere visualizzazioni](operations-management-suite-solutions-resources-views.md) tooyour soluzione di gestione.
* [Aggiungere i runbook di automazione e altre risorse](operations-management-suite-solutions-resources-automation.md) tooyour soluzione di gestione.

