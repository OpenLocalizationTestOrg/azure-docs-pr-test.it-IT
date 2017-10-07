---
title: aaaSchema Aggiorna anteprima di agosto-1-2015 - App Azure per la logica | Documenti Microsoft
description: Creare definizioni JSON per App per la logica di Azure con la versione dello schema 2015-08-01-preview
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Aggiornamenti dello schema per App per la logica di Azure: anteprima del 1° agosto 2015

Questo nuovo schema e l'API di versione per App di logica di Azure include importanti miglioramenti che App per la logica di rendere più affidabile e facile toouse:

*   Hello **APIApp** tipo di azione è aggiornato tooa nuova [ **APIConnection** ](#api-connections) tipo di azione.
*   **Ripetere** viene rinominato troppo[**Foreach**](#foreach).
*   Hello [ **HTTP Listener** App per le API](#http-listener) non è più necessario.
*   La chiamata a flussi di lavoro figlio usa un [nuovo schema](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Spostare le connessioni tooAPI

cambiamento Hello è che non è più necessario toodeploy App per le API alla sottoscrizione di Azure è possibile utilizzare le API. Esistono metodi hello che è possibile utilizzare le API:

* API gestite
* API Web personalizzate

Ciascun metodo viene gestito in modo leggermente diverso perché prevede modelli di gestione e hosting diversi. Uno dei vantaggi di questo modello è non sta non è più vincolata tooresources che vengono distribuite nel gruppo di risorse di Azure. 

### <a name="managed-apis"></a>API gestite

Microsoft gestisce alcune API per conto dell'utente, ad esempio Office 365, Salesforce, Twitter e FTP. È possibile usare alcune API gestite così come sono, ad esempio Bing Translate, mentre altre richiedono una configurazione. Questa configurazione è detta *connessione*.

Quando si usa Office 365, ad esempio, è necessario creare una connessione contenente il token di accesso a Office 365. Questo token in modo sicuro è archiviato e aggiornato in modo che l'app logica può chiamare sempre il metodo hello API di Office 365. In alternativa, se si desidera tooconnect tooyour FTP o SQL server, è necessario creare una connessione con la stringa di connessione hello. 

In questa definizione, queste azioni sono denominate `APIConnection`. Di seguito è riportato un esempio di una connessione che chiama un messaggio di posta elettronica di Office 365 toosend:

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

Hello `host` oggetto è parte di input connessioni tooAPI univoco, che contiene due parti: `api` e `connection`.

Hello `api` ha runtime hello URL dell'API che gestita con una diversa in cui è ospitato. È possibile visualizzare tutti hello disponibili API gestite chiamando `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Quando si utilizza un'API, hello API potrebbe o potrebbe non disporre *parametri di connessione* definito. Se non hello API, nessun *connessione* è obbligatorio. In caso di hello API, è necessario creare una connessione. nome di hello prescelto connessione Hello creato. Per fare riferimento nome hello in hello `connection` oggetto all'interno di hello `host` oggetto. una connessione in un gruppo di risorse, chiamata toocreate:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Con hello corpo seguente:

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Distribuire API gestite in un modello di Azure Resource Manager

È possibile creare un'applicazione completa in un modello di Azure Resource Manager, purché non sia necessario l'accesso interattivo.
Se l'accesso è obbligatorio, è possibile impostare tutti gli elementi con il modello di gestione risorse di Azure hello, ma è comunque necessario connessioni di hello toovisit hello tooauthorize portale. 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

È possibile visualizzare in questo esempio le connessioni hello sono solo le risorse che risiedono nel gruppo di risorse. Fanno riferimento a tooyou disponibili di API gestita hello nella sottoscrizione.

### <a name="your-custom-web-apis"></a>API Web personalizzate

Se si utilizzano le tue API, quelli non gestiti da Microsoft, utilizzare incorporato hello **HTTP** toocall azione li. Per un'esperienza ideale, si consiglia di esporre un endpoint swagger per l'API. Questo endpoint consente gli input di hello progettazione applicazione logica toorender hello e output per l'API. Senza Swagger, progettazione hello può mostrare solo hello input e output come oggetti JSON opachi.

Ecco un hello di esempio che mostra nuova `metadata.apiDefinitionUrl` proprietà:

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

Se si ospita l'API Web nel servizio App di Azure, l'API Web viene visualizzato automaticamente nell'elenco di hello di azioni disponibili nella finestra di progettazione hello. In caso contrario, sono presenti toopaste URL hello direttamente. endpoint Swagger Hello deve essere non autenticate toobe utilizzabile in hello progettazione applicazione logica, anche se è possibile proteggere hello stessa interfaccia API con qualsiasi metodo che supporta Swagger.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Chiamare le app per le API già distribuite con 2015-08-01-preview

Se già stato distribuito un'App per le API, è possibile chiamare l'applicazione hello con hello **HTTP** azione.

Ad esempio, se si utilizzano file toolist dell'area di sincronizzazione, il **2014-12-01-preview** definizione di versione dello schema potrebbe essere simile al seguente:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

È possibile costruire azione HTTP equivalente hello simile a questo esempio, mentre sezione parametri hello di definizione dell'app logica hello rimane invariato:

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

La tabella seguente illustra le singole proprietà:

| Proprietà dell'azione | Descrizione |
| --- | --- |
| `type` |`Http` anziché `APIapp` |
| `metadata.apiDefinitionUrl` |toouse in hello progettazione applicazione logica, questa azione includono l'endpoint dei metadati hello, che viene creato da:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Costituito da: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Sempre `POST` |
| `inputs.body` |Parametri dell'App toohello identici API |
| `inputs.authentication` |L'autenticazione di App per le API di toohello identico |

Questo approccio dovrebbe funzionare per tutte le azioni delle app per le API. Tenere tuttavia presente che queste app per le api precedenti non sono più supportate. È pertanto consigliabile spostare tooone di hello due altre opzioni precedenti, un'API gestita o ospita l'API Web personalizzato.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Rinominare 'repeat' too'foreach'

Per la versione di schema hello precedente, è pervenuta quantità i suggerimenti dei clienti che **ripetere** creava notevole confusione e che non è stata correttamente acquisire **ripetere** fosse effettivamente un ciclo foreach. Di conseguenza, è stata rinominata `repeat` troppo`foreach`. Ad esempio, in precedenza si sarebbe scritto:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

Ora si scriverebbe:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

funzione Hello `@repeatItem()` è stato utilizzato in precedenza tooreference elemento corrente di hello scorsa. Questa funzione è ora semplificata troppo`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Fare riferimento agli output da "foreach"

Per semplificare le operazioni, gli output hello `foreach` azioni non sono incapsulate in un oggetto denominato `repeatItems`. Mentre hello di output di hello precedente `repeat` esempio fosse:

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

Ora tali output sono:

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

In precedenza, il tooget toohello corpo dell'azione di hello quando si fa riferimento a questi output:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

Ora, invece, è possibile eseguire:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

Con queste modifiche, hello funzioni `@repeatItem()`, `@repeatBody()`, e `@repeatOutputs()` vengono rimossi.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Listener HTTP nativo

Hello funzionalità HTTP Listener sono ora incorporate. Pertanto, non è più necessario toodeploy un'App per le API del Listener HTTP. Vedere [hello dettagli completi per informazioni su come toomake il qui callable di logica app endpoint](../logic-apps/logic-apps-http-endpoint.md). 

Con queste modifiche, sono state rimosse hello `@accessKeys()` funzione, pertanto abbiamo sostituito con hello `@listCallbackURL()` funzione per ottenere l'endpoint di hello quando necessario. Ora è anche necessario definire almeno un trigger nell'app per la logica. Se si desidera troppo`/run` hello del flusso di lavoro, è necessario disporre di uno di questi trigger: `manual`, `apiConnectionWebhook`, o `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Chiamare flussi di lavoro figlio

In precedenza, la chiamata di flussi di lavoro figlio, è necessario passare toohello del flusso di lavoro, ottenere il token di accesso di hello e concatenamento dei token di hello nella definizione di applicazione hello logica in cui si desidera toocall tale flusso di lavoro figlio. Con nuovo schema hello, hello logica App motore genera automaticamente una firma di accesso condiviso in fase di esecuzione per hello del flusso di lavoro figlio in modo da non avere troppo incollato alcun dato segreto definizione hello. Di seguito è fornito un esempio:

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

Un secondo miglioramento è che verrà ugualmente figlio hello richiesta in ingresso toohello accesso completo di flussi di lavoro. Ciò significa che è possibile passare parametri hello *query* sezione e in hello *intestazioni* oggetto e che è possibile definire completamente hello intero corpo.

Infine, sono presenti flussi di lavoro figlio toohello le modifiche necessarie. Mentre in precedenza è possibile chiamare direttamente un flusso di lavoro figlio, a questo punto è necessario definire un endpoint di trigger nel flusso di lavoro di hello per toocall padre hello. In genere, si aggiunge un trigger con `manual` digitare e quindi utilizzare tale trigger nella definizione di hello padre. Hello nota `host` proprietà di un `triggerName` perché è sempre necessario specificare i trigger di cui si sta chiamando.

## <a name="other-changes"></a>Altre modifiche

### <a name="new-queries-property"></a>Nuova proprietà "queries"

Tutti i tipi di azione ora supportano un nuovo input denominato `queries`. L'input può essere un oggetto strutturato, anziché dover stringa hello tooassemble manualmente.

### <a name="renamed-parse-function-toojson"></a>Rinominato too'json() funzione 'Parse ()' '

Si sta aggiungendo a breve, i tipi di contenuto più in modo hello è stato rinominato `parse()` funzione troppo`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Presto disponibile: API Enterprise Integration

Non è gestite versioni ancora hello Enterprise Integration API, ad esempio AS2. Nel frattempo, è possibile utilizzare le APIs BizTalk distribuito esistente tramite hello azione HTTP. Per informazioni dettagliate, vedere "Utilizzo delle App già distribuite API" in hello [roadmap integrazione](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
