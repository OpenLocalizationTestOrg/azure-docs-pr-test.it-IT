---
title: i flussi di lavoro aaaDefine con JSON - App Azure per la logica | Documenti Microsoft
description: Come le definizioni di flusso di lavoro toowrite in JSON per App per la logica
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Creare definizioni dei flussi di lavoro per le app per la logica usando JSON

È possibile creare definizioni flusso di lavoro per [App per la logica di Azure](logic-apps-what-are-logic-apps.md) con il semplice linguaggio dichiarativo JSON. Se hai già fatto, esaminare innanzitutto [come toocreate la prima app logica con progettazione applicazione logica](logic-apps-create-a-logic-app.md). Vedere anche hello [completo di riferimento per il linguaggio di definizione del flusso di lavoro hello](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Ripetere i passaggi in un elenco

tooiterate tramite una matrice non too10, 000 elementi e per esegue un'azione per ogni elemento, utilizza hello [tipo foreach](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Gestire gli errori in caso di problemi

In genere, si desidera tooinclude un *passaggio di correzione* , ovvero una logica che esegue *se e solo se* esito negativo di uno o più chiamate. In questo esempio ottiene i dati da varie posizioni, ma se hello chiamata non riesce, è opportuno tooPOST un messaggio in un punto in modo è possibile tenere traccia di errore in un secondo momento:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

toospecify che `postToErrorMessageQueue` viene eseguito solo dopo aver `readData` è `Failed`, utilizzare hello `runAfter` proprietà, ad esempio, toospecify un elenco di valori possibili, in modo che `runAfter` potrebbe essere `["Succeeded", "Failed"]`.

Infine, poiché in questo esempio gestisce ora errore hello, abbiamo non contrassegnare non è più hello runas `Failed`. Poiché è stato aggiunto il passaggio di hello per la gestione di questo errore in questo esempio, eseguire hello ha `Succeeded` anche se un unico passaggio `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Eseguire due o più passaggi in parallelo

toorun più operazioni in parallelo, hello `runAfter` proprietà deve essere equivalente in fase di esecuzione. 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

In questo esempio, entrambi `branch1` e `branch2` impostati toorun dopo `readData`. Di conseguenza, entrambi i rami vengono eseguiti in parallelo. timestamp Hello per entrambi i rami è identico.

![Parallelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Creare un join di due rami paralleli

È possibile unire due azioni che vengono impostate toorun in parallelo tramite l'aggiunta di elementi toohello `runAfter` proprietà esempio hello precedente.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Parallelo](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-tooa-different-configuration"></a>Eseguire il mapping di configurazione diversi tooa degli elementi di elenco

Successivamente, si supponga che si desidera tooget contenuto diverso in base al valore di hello di una proprietà. È possibile creare una mappa di valori toodestinations come parametro:  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

In questo caso, si ottiene prima un elenco di articoli. In base alla categoria di hello che è stata definita come parametro, hello secondo passo utilizza toolook una mappa di hello URL per ottenere il contenuto di hello.

Alcune volte toonote qui: 

*   Hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) funzione controlla se la categoria hello corrisponde a uno di hello noto categorie definite.

*   Dopo aver ottenuto la categoria hello, è possibile effettuare il pull elemento hello dalla mappa hello utilizzando le parentesi quadre:`parameters[...]`

## <a name="process-strings"></a>Elaborare le stringhe

È possibile utilizzare varie stringhe toomanipulate di funzioni. Ad esempio, supponiamo di che avere una stringa che si desidera che il sistema di tooa toopass, ma non siamo certi su una gestione corretta per la codifica dei caratteri. Un'opzione è toobase64 codificare questa stringa. Tuttavia, tooavoid escape in un URL, verrà tooreplace alcuni caratteri. 

È necessario anche una sottostringa di nome dell'ordine di hello, poiché non vengono utilizzati i primi cinque caratteri hello.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

Lavoro all'interno di toooutside:

1. Ottenere hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) per il nome dell'autore di ordine di hello, pertanto è ottenere nuovamente hello numero totale di caratteri.

2. Sottrarre 5 perché si vuole ottenere una stringa più breve.

3. In realtà, richiedere hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Iniziare in corrispondenza dell'indice `5` e passare hello resto della stringa hello.

4. Convertire questo tooa sottostringa [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) stringa.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)hello tutti `+` caratteri con `-` caratteri.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)hello tutti `/` caratteri con `_` caratteri.

## <a name="work-with-date-times"></a>Uso di date e ore

Data ora può essere utile, in particolare se si siano cercando toopull dati da un'origine dati che non supporta naturalmente *trigger*. È anche possibile usare date e ore per trovare la durata di diversi passaggi.

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

In questo esempio è estrarre hello `startTime` dal passaggio precedente hello. È quindi ottenere l'ora corrente di hello e sottrarre un secondo:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

È possibile usare altre unità di tempo, ad esempio `minutes` o `hours`. Infine si potranno confrontare questi due valori. Se hello primo valore è minore di secondo valore hello e più di un secondo trascorso hello primo ordine.

tooformat date, è possibile utilizzare i formattatori di stringa. Ad esempio, hello tooget RFC1123, utilizziamo [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). toolearn sulla formattazione di data, vedere [il linguaggio di definizione del flusso di lavoro](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Parametri di distribuzione per diversi ambienti

In genere, i cicli di vita di distribuzione prevedono un ambiente di sviluppo, un ambiente di staging e un ambiente di produzione. Ad esempio, è possibile utilizzare hello stessa definizione in tutti questi ambienti, ma utilizzano database diversi. Analogamente, è possibile toouse hello stessa definizione in aree geografiche diverse per la disponibilità elevata, ma desidera database ogni logica app istanza tootalk toothat dell'area.
Questo scenario è diverso da che accetta i parametri in *runtime* in alternativa, è possibile utilizzare hello `trigger()` funzione esempio hello precedente.

È possibile iniziare con una definizione di base, come questo esempio:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

In hello effettivo `PUT` richiesta per le app logica hello, è possibile fornire il parametro hello `uri`. Dato che un valore predefinito non esiste più, payload dell'applicazione hello logica richiede questo parametro:

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

In ogni ambiente, è possibile fornire un valore diverso per hello `connection` parametro. 

Per tutti hello opzioni che è necessario per la creazione e gestione delle app di logica, vedere hello [documentazione dell'API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
