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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="9c1d5-103">Creare definizioni dei flussi di lavoro per le app per la logica usando JSON</span><span class="sxs-lookup"><span data-stu-id="9c1d5-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="9c1d5-104">È possibile creare definizioni flusso di lavoro per [App per la logica di Azure](logic-apps-what-are-logic-apps.md) con il semplice linguaggio dichiarativo JSON.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="9c1d5-105">Se hai già fatto, esaminare innanzitutto [come toocreate la prima app logica con progettazione applicazione logica](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9c1d5-106">Vedere anche hello [completo di riferimento per il linguaggio di definizione del flusso di lavoro hello](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="9c1d5-107">Ripetere i passaggi in un elenco</span><span class="sxs-lookup"><span data-stu-id="9c1d5-107">Repeat steps over a list</span></span>

<span data-ttu-id="9c1d5-108">tooiterate tramite una matrice non too10, 000 elementi e per esegue un'azione per ogni elemento, utilizza hello [tipo foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="9c1d5-109">Gestire gli errori in caso di problemi</span><span class="sxs-lookup"><span data-stu-id="9c1d5-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="9c1d5-110">In genere, si desidera tooinclude un *passaggio di correzione* , ovvero una logica che esegue *se e solo se* esito negativo di uno o più chiamate.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="9c1d5-111">In questo esempio ottiene i dati da varie posizioni, ma se hello chiamata non riesce, è opportuno tooPOST un messaggio in un punto in modo è possibile tenere traccia di errore in un secondo momento:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="9c1d5-112">toospecify che `postToErrorMessageQueue` viene eseguito solo dopo aver `readData` è `Failed`, utilizzare hello `runAfter` proprietà, ad esempio, toospecify un elenco di valori possibili, in modo che `runAfter` potrebbe essere `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="9c1d5-113">Infine, poiché in questo esempio gestisce ora errore hello, abbiamo non contrassegnare non è più hello runas `Failed`.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="9c1d5-114">Poiché è stato aggiunto il passaggio di hello per la gestione di questo errore in questo esempio, eseguire hello ha `Succeeded` anche se un unico passaggio `Failed`.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="9c1d5-115">Eseguire due o più passaggi in parallelo</span><span class="sxs-lookup"><span data-stu-id="9c1d5-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="9c1d5-116">toorun più operazioni in parallelo, hello `runAfter` proprietà deve essere equivalente in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="9c1d5-117">In questo esempio, entrambi `branch1` e `branch2` impostati toorun dopo `readData`.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="9c1d5-118">Di conseguenza, entrambi i rami vengono eseguiti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="9c1d5-119">timestamp Hello per entrambi i rami è identico.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-119">hello timestamp for both branches is identical.</span></span>

![Parallelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="9c1d5-121">Creare un join di due rami paralleli</span><span class="sxs-lookup"><span data-stu-id="9c1d5-121">Join two parallel branches</span></span>

<span data-ttu-id="9c1d5-122">È possibile unire due azioni che vengono impostate toorun in parallelo tramite l'aggiunta di elementi toohello `runAfter` proprietà esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="9c1d5-124">Eseguire il mapping di configurazione diversi tooa degli elementi di elenco</span><span class="sxs-lookup"><span data-stu-id="9c1d5-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="9c1d5-125">Successivamente, si supponga che si desidera tooget contenuto diverso in base al valore di hello di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="9c1d5-126">È possibile creare una mappa di valori toodestinations come parametro:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="9c1d5-127">In questo caso, si ottiene prima un elenco di articoli.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="9c1d5-128">In base alla categoria di hello che è stata definita come parametro, hello secondo passo utilizza toolook una mappa di hello URL per ottenere il contenuto di hello.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="9c1d5-129">Alcune volte toonote qui:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="9c1d5-130">Hello [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) funzione controlla se la categoria hello corrisponde a uno di hello noto categorie definite.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="9c1d5-131">Dopo aver ottenuto la categoria hello, è possibile effettuare il pull elemento hello dalla mappa hello utilizzando le parentesi quadre:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="9c1d5-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="9c1d5-132">Elaborare le stringhe</span><span class="sxs-lookup"><span data-stu-id="9c1d5-132">Process strings</span></span>

<span data-ttu-id="9c1d5-133">È possibile utilizzare varie stringhe toomanipulate di funzioni.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="9c1d5-134">Ad esempio, supponiamo di che avere una stringa che si desidera che il sistema di tooa toopass, ma non siamo certi su una gestione corretta per la codifica dei caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="9c1d5-135">Un'opzione è toobase64 codificare questa stringa.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="9c1d5-136">Tuttavia, tooavoid escape in un URL, verrà tooreplace alcuni caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="9c1d5-137">È necessario anche una sottostringa di nome dell'ordine di hello, poiché non vengono utilizzati i primi cinque caratteri hello.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="9c1d5-138">Lavoro all'interno di toooutside:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="9c1d5-139">Ottenere hello [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) per il nome dell'autore di ordine di hello, pertanto è ottenere nuovamente hello numero totale di caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="9c1d5-140">Sottrarre 5 perché si vuole ottenere una stringa più breve.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="9c1d5-141">In realtà, richiedere hello [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="9c1d5-142">Iniziare in corrispondenza dell'indice `5` e passare hello resto della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="9c1d5-143">Convertire questo tooa sottostringa [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) stringa.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="9c1d5-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)hello tutti `+` caratteri con `-` caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="9c1d5-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)hello tutti `/` caratteri con `_` caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="9c1d5-146">Uso di date e ore</span><span class="sxs-lookup"><span data-stu-id="9c1d5-146">Work with Date Times</span></span>

<span data-ttu-id="9c1d5-147">Data ora può essere utile, in particolare se si siano cercando toopull dati da un'origine dati che non supporta naturalmente *trigger*.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="9c1d5-148">È anche possibile usare date e ore per trovare la durata di diversi passaggi.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="9c1d5-149">In questo esempio è estrarre hello `startTime` dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="9c1d5-150">È quindi ottenere l'ora corrente di hello e sottrarre un secondo:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="9c1d5-151">È possibile usare altre unità di tempo, ad esempio `minutes` o `hours`.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="9c1d5-152">Infine si potranno confrontare questi due valori.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="9c1d5-153">Se hello primo valore è minore di secondo valore hello e più di un secondo trascorso hello primo ordine.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="9c1d5-154">tooformat date, è possibile utilizzare i formattatori di stringa.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="9c1d5-155">Ad esempio, hello tooget RFC1123, utilizziamo [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="9c1d5-156">toolearn sulla formattazione di data, vedere [il linguaggio di definizione del flusso di lavoro](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="9c1d5-157">Parametri di distribuzione per diversi ambienti</span><span class="sxs-lookup"><span data-stu-id="9c1d5-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="9c1d5-158">In genere, i cicli di vita di distribuzione prevedono un ambiente di sviluppo, un ambiente di staging e un ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="9c1d5-159">Ad esempio, è possibile utilizzare hello stessa definizione in tutti questi ambienti, ma utilizzano database diversi.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="9c1d5-160">Analogamente, è possibile toouse hello stessa definizione in aree geografiche diverse per la disponibilità elevata, ma desidera database ogni logica app istanza tootalk toothat dell'area.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="9c1d5-161">Questo scenario è diverso da che accetta i parametri in *runtime* in alternativa, è possibile utilizzare hello `trigger()` funzione esempio hello precedente.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="9c1d5-162">È possibile iniziare con una definizione di base, come questo esempio:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="9c1d5-163">In hello effettivo `PUT` richiesta per le app logica hello, è possibile fornire il parametro hello `uri`.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="9c1d5-164">Dato che un valore predefinito non esiste più, payload dell'applicazione hello logica richiede questo parametro:</span><span class="sxs-lookup"><span data-stu-id="9c1d5-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

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

<span data-ttu-id="9c1d5-165">In ogni ambiente, è possibile fornire un valore diverso per hello `connection` parametro.</span><span class="sxs-lookup"><span data-stu-id="9c1d5-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="9c1d5-166">Per tutti hello opzioni che è necessario per la creazione e gestione delle app di logica, vedere hello [documentazione dell'API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c1d5-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
