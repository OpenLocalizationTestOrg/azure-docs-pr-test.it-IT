---
title: cicli e gli ambiti o debatch dati nei flussi di lavoro - App Azure per la logica aaaCreate | Documenti Microsoft
description: "Creare cicli tooiterate tra i dati, le azioni in ambiti, gruppo o debatch toostart dati più flussi di lavoro in Azure App per la logica."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>Cicli, ambiti e debatching delle app per la logica
  
Logica App offre una serie di modi toowork con matrici, raccolte, batch e cicli all'interno di un flusso di lavoro.
  
## <a name="foreach-loop-and-arrays"></a>Matrici e cicli ForEach
  
Logica App consente tooloop su un set di dati ed eseguire un'azione per ogni elemento.  Ciò è possibile tramite hello `foreach` azione.  Nella finestra di progettazione hello, è possibile specificare tooadd una per ogni ciclo.  Dopo aver selezionato una matrice di hello desiderato tooiterate tramite, è possibile iniziare l'aggiunta di azioni.  Sono attualmente limitate tooonly un'azione per ogni ciclo foreach, ma questa limitazione verrà rimossa in hello in arrivo settimane.  Una volta all'interno di ciclo hello è possibile iniziare toospecify cosa dovrebbe accadere in ogni valore di matrice hello.

Se si usa la visualizzazione del codice, è possibile specificare un loop ForEach come nell'illustrazione che segue.  In questo esempio di loop ForEach viene inviato un messaggio di posta elettronica per ogni indirizzo di posta elettronica che contiene "microsoft.com":

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  Oggetto `foreach` azione possibile scorrere le matrici di too5, 000 righe.  Per impostazione predefinita, ogni iterazione verrà eseguita in parallelo alle altre.  

### <a name="sequential-foreach-loops"></a>Cicli ForEach sequenziali

tooenable un tooexecute ciclo foreach in sequenza, hello `Sequential` deve essere aggiunta l'opzione di operazione.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Ciclo Until
  
  È possibile eseguire un'azione o una serie di azioni finché non viene soddisfatta una condizione.  Hello scenario più comune per questo consiste nel chiamare un endpoint fino a ottenere una risposta hello che si sta cercando.  Nella finestra di progettazione hello, è possibile specificare tooadd un fino al ciclo.  Dopo l'aggiunta di azioni all'interno di ciclo hello, è possibile impostare la condizione di uscita hello, nonché hello i limiti di ciclo.  Si verifica un ritardo di 1 minuto tra i cicli del loop.
  
  Se si usa la visualizzazione del codice, è possibile specificare un loop Until come nell'illustrazione che segue.  Questo è un esempio di chiamata di un endpoint HTTP finché il corpo della risposta hello è il valore di hello 'Completato'.  Ciò avviene in presenza di una di queste condizioni: 
  
  * Lo stato della risposta HTTP è "Completed"
  * Sono stati fatti tentativi per 1 ora
  * Il ciclo è stato eseguito 100 volte
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn e scomposizione batch

In alcuni casi un trigger può ricevere una matrice di elementi desiderati toodebatch e avviare un flusso di lavoro per ogni elemento.  Questo può essere eseguito tramite hello `spliton` comando.  Per impostazione predefinita, se lo swagger del trigger specifica un payload che è una matrice, viene aggiunto `spliton` e viene avviata un'esecuzione per ogni elemento.  SplitOn possono essere aggiunti solo tooa trigger.  L'operazione può essere configurata manualmente o sottoposta a override nella visualizzazione del codice di definizione.  Attualmente è possibile SplitOn debatch matrici backup too5, gli elementi 000.  Non è possibile avere un `spliton` e inoltre implementare il modello di risposta sincrona hello.  Qualsiasi flusso di lavoro denominato che ha un `response` azione inoltre troppo`spliton` verrà eseguito in modo asincrono e inviare immediatamente `202 Accepted` risposta.  

SplitOn può essere specificato nella visualizzazione codice come hello di esempio seguente.  In questo caso viene ricevuta una matrice di elementi e la scomposizione dei batch avviene su ogni riga.

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>Ambiti

È possibile toogroup una serie di azioni tra loro tramite un ambito.  Ciò è particolarmente utile per implementare la gestione delle eccezioni.  Nella finestra di progettazione hello è possibile aggiungere un nuovo ambito e iniziare ad aggiungere le azioni all'interno.  È possibile definire gli ambiti nella visualizzazione di codice hello seguente:


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```