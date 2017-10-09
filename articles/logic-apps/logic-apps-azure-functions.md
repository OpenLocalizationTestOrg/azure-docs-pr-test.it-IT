---
title: codice aaaCustom per le app di logica di Azure con le funzioni di Azure | Documenti Microsoft
description: Creare ed eseguire un codice personalizzato per le app per la logica di Azure con Funzioni di Azure
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Aggiungere ed eseguire un codice personalizzato per le app per la logica di Azure tramite Funzioni di Azure

toorun frammenti personalizzati di c# o Node. js in App per la logica, è possibile creare funzioni personalizzate mediante le funzioni di Azure. 
Le [Funzioni di Azure](../azure-functions/functions-overview.md) offrono funzionalità di calcolo indipendenti dal server in Microsoft Azure e sono utili per eseguire queste attività:

* Formattazione avanzata o calcolo di campi nelle app per la logica
* Esecuzione di calcoli in un flusso di lavoro.
* Estendere le funzionalità di hello logica app con le funzioni che sono supportate in c# o node.js

## <a name="create-custom-functions-for-your-logic-apps"></a>Creare funzioni personalizzate per le app per la logica

È consigliabile creare una funzione nel portale di Azure funzioni hello da hello **Webhook generico - nodo** o **Webhook - generico c#** modelli. risultato Hello viene creato un popolati automaticamente un modello che accetta `application/json` da un'app di logica. Le funzioni che vengono creati tramite questi modelli vengono rilevate automaticamente e visualizzate in hello progettazione applicazione logica in **funzioni di Azure nella mia area.**

Nel portale di Azure su hello hello **integrazione** riquadro per la funzione, il modello viene mostrato che **modalità** impostare troppo**Webhook** e **Webhook tipo** è troppo**JSON generico**. 

Funzioni Webhook accettare una richiesta e passarlo nel metodo hello tramite un `data` variabile. È possibile accedere a proprietà hello del payload usando la notazione come `data.function-name`. Ad esempio, una semplice funzione JavaScript che converte un valore DateTime in una stringa di data aspetto hello di esempio seguente:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Chiamare Funzioni di Azure da app per la logica

contenitori di hello toolist nella sottoscrizione e funzione select hello che si desidera toocall, in Progettazione applicazione logica, fare clic su hello **azioni** menu, quindi scegliere **funzioni di Azure nella mia area**.

Dopo aver selezionato la funzione hello, sono frequenti toospecify un oggetto payload di input. Questo oggetto è il messaggio hello logica app invia toohello funzione hello e deve essere un oggetto JSON. Ad esempio, se si desidera toopass in hello **Data ultima modifica** data da un trigger di Salesforce, payload di funzione hello potrebbe essere simile al seguente:

![Data ultima modifica][1]

## <a name="trigger-logic-apps-from-a-function"></a>Attivare app per la logica da una funzione

È possibile attivare un'app per la logica all'interno di una funzione. Vedere [App per la logica come endpoint che è possibile chiamare](logic-apps-http-endpoint.md). Creare un'app di logica che include un trigger manuale, quindi da all'interno della funzione, generare un URL di attivazione manuale toohello HTTP POST con payload hello che si desidera inviare toohello logica app.

### <a name="create-a-function-from-logic-app-designer"></a>Creare una funzione dalla finestra di progettazione delle app per la logica

È anche possibile creare una funzione di webhook node.js da Progettazione hello. Selezionare prima di tutto **Funzioni di Azure nell'area** , quindi scegliere un contenitore per la funzione. Se si dispone ancora di un contenitore, è necessario toocreate da hello [portale di Azure funzioni](https://functions.azure.com/signin). Selezionare quindi **Crea nuovo**.  

toogenerate un modello basato su dati hello che si desidera toocompute, specificare l'oggetto di contesto hello pianificare toopass in una funzione. Deve trattarsi di un oggetto JSON. Ad esempio, se si passa nel contenuto del file hello da un'azione di FTP, il payload di contesto hello è simile in questo esempio:

![Payload di contesto][2]

> [!NOTE]
> Poiché non è stato eseguito il cast di questo oggetto sotto forma di stringa, payload JSON toohello venga aggiunto direttamente il contenuto di hello. Tuttavia, si verifica un errore se l'oggetto hello non è un token JSON (ovvero, una stringa o un formato JSON/matrice di oggetti). oggetto hello toocast sotto forma di stringa, aggiunge le virgolette come illustrato nella figura prima di hello in questo articolo.
> 

finestra di progettazione Hello genera quindi un modello di funzione che è possibile creare inline. Le variabili sono create in precedenza in base al contesto hello pianificare toopass nella funzione hello.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
