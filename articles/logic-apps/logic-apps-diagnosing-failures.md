---
title: errori aaaDiagnose - App Azure per la logica | Documenti Microsoft
description: Comuni toounderstand modi in cui la logica App non sono stati superati
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a>Eseguire una diagnosi degli errori delle app per la logica
Se si verificano errori o problemi con le applicazioni di logica, esistono due approcci consentono di comprendere meglio provengano errori hello.  

## <a name="azure-portal-tools"></a>Strumenti del portale di Azure
Hello portale di Azure fornisce molti strumenti toodiagnose ogni app per la logica in ogni fase.

### <a name="trigger-history"></a>Cronologia di attivazione

Ogni app per la logica ha almeno un trigger. Se si nota che non sono la generazione di applicazioni, cercare nella cronologia di trigger hello per altre informazioni. È possibile accedere a cronologia trigger hello nel pannello principale di hello logica app'ss.

![Individuazione cronologia trigger hello][1]

la cronologia di trigger Hello Elenca tutti i tentativi di trigger che ha effettuato l'app logica. È possibile fare clic su ogni toodrill tentativo trigger i dettagli di hello, in particolare, qualsiasi input o output di hello tentativo trigger generato. Se si trova il trigger non riuscito, selezionare il tentativo di trigger hello e scegliere hello **output** collegamento tooreview qualsiasi errore generato i messaggi, ad esempio, per le credenziali FTP che non sono valide.

potrebbe essere visualizzato in base ai diversi stati Hello sono:

* **Operazione ignorata**. endpoint Hello toocheck polling per i dati di stato e ha ricevuto una risposta che nessun dato è disponibile.
* **Operazione completata**. trigger Hello ha ricevuto una risposta che dati non sono disponibili. Questo può essere il risultato di un trigger manuale, un trigger di ricorrenza o un trigger di poll. Questo stato è generalmente seguito da hello **generato** stato, ma potrebbe non essere la presenza di una condizione o un comando di SplitOn nella visualizzazione codice che non è stata soddisfatta.
* **Operazione non riuscita**. È stato generato un errore.

#### <a name="start-a-trigger-manually"></a>Avviare manualmente un trigger

Se si desidera hello logica app toocheck per un trigger disponibile immediatamente senza attendere l'occorrenza successiva di hello, fare clic su **selezionare Trigger** nel pannello principale di hello tooforce un segno di spunta. Ad esempio, facendo clic su questo collegamento con un trigger di sincronizzazione determina hello del flusso di lavoro tooimmediately polling dell'area di sincronizzazione per i nuovi file.

### <a name="run-history"></a>Cronologia di esecuzione

Ogni trigger attivato comporta un'esecuzione. È possibile accedere a informazioni sull'esecuzione dal pannello principale hello, che contiene molti dettagli che aiutano a capire cosa è successo durante il flusso di lavoro hello.

![Individuazione hello cronologia di esecuzione][2]

Un'esecuzione viene visualizzato uno dei seguenti stati hello:

* **Operazione completata**. Tutte le azioni hanno avuto esito positivo. Se si è verificato un errore, tale errore è stato gestito da un'azione che si è verificato in un secondo momento nel flusso di lavoro hello. Errore di hello, ovvero è stato gestito da un'azione che è stata impostata toorun dopo un'azione non riuscita.
* **Operazione non riuscita**. Almeno un'azione ha esito negativo che non è stata gestita da un'azione nel flusso di lavoro hello.
* **Operazione annullata**. flusso di lavoro Hello era in esecuzione ma ha ricevuto una richiesta di annullamento.
* **In esecuzione**. flusso di lavoro Hello è attualmente in esecuzione. Questo stato può verificarsi per i flussi di lavoro limitate, o a causa di hello prezzi piano corrente. Per informazioni dettagliate, vedere [i limiti di azione nella pagina relativa ai prezzi hello](https://azure.microsoft.com/pricing/details/app-service/plans/). Configurazione della diagnostica (grafici hello che vengono visualizzati nella cronologia di esecuzione hello) inoltre possibile fornire informazioni su tutti gli eventi di limitazione che si verificano.

Quando si analizza una cronologia di esecuzione, è possibile visualizzare ulteriori dettagli.  

#### <a name="trigger-outputs"></a>Output dei trigger

Trigger genera Mostra hello i dati provenienti da trigger hello. Questi output consentono di determinare se tutte le proprietà sono state restituite come previsto.

> [!NOTE]
> Se si notano contenuti poco chiari, potrebbe essere utile comprendere il modo in cui le App per la logica di Azure [gestiscono i diversi tipi di contenuto](../logic-apps/logic-apps-content-type.md).
> 

![Esempi di output di trigger][3]

#### <a name="action-inputs-and-outputs"></a>Input e output delle azioni

È possibile analizzare hello input e output che ha ricevuta un'azione. Questi dati sono utili per comprendere hello dimensioni e la forma di output di hello, nonché per individuare eventuali messaggi di errore che potrebbero essere stati generati.

![Input e output delle azioni][4]

## <a name="debug-workflow-runtime"></a>Debug del runtime del flusso di lavoro

Insieme a monitoraggio hello input, output e i trigger di un'esecuzione, è possibile aggiungere alcuni passaggi tooa del flusso di lavoro che consentono il debug. 
[RequestBin](http://requestb.in) è uno strumento utile che è possibile aggiungere come passaggio in un flusso di lavoro. Se si utilizza RequestBin, è possibile impostare un controllo toodetermine hello esatta dimensione della richiesta HTTP, forma e formato di una richiesta HTTP. È possibile creare un RequestBin e incollare l'URL di hello in un'app di logica di azione HTTP POST con il contenuto del corpo che si desidera tootest, ad esempio, un'espressione o un altro output di passaggio. Dopo aver eseguito hello logica app, è possibile aggiornare il toosee RequestBin come richiesta hello valido quando generati dal motore di App per la logica di hello.

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
