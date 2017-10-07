---
title: azione di query aaaAdd hello in App per la logica | Documenti Microsoft
description: Panoramica dell'azione query hello per eseguire azioni come matrice di filtro.
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Iniziare a utilizzare l'azione di query hello
Tramite l'azione di query hello, è possibile utilizzare batch e le matrici tooaccomplish dei flussi di lavoro:

* Creare un'attività per tutti i record ad alta priorità di un database.
* Salvare tutti gli allegati PDF per i messaggi di posta elettronica in un BLOB di Azure.

tooget avviato utilizzando l'azione di query hello in un'app di logica, vedere [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-query-action"></a>Utilizzare l'azione di query hello
Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica. [Altre informazioni sulle azioni](connectors-overview.md).  

azione di query Hello è attualmente un'unica operazione, detta matrice di filtro hello, che viene visualizzata nella finestra di progettazione hello. Ciò consente tooquery una matrice e restituire un set di risultati filtrati.

Ecco come è possibile aggiungerla in un'app per la logica:

1. Seleziona hello **nuovo passaggio** pulsante.
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di ricerca azione hello, digitare **filtro** hello toolist **matrice filtro** azione.
   
    ![Selezionare l'azione di query hello](./media/connectors-native-query/using-action-1.png)
4. Selezionare un toofilter di matrice. (hello seguente schermata Mostra matrice hello di risultati da una ricerca di Twitter.)
5. Creare una condizione tooevaluate su ogni elemento. (hello seguente schermata Filtra TWEET gli utenti che hanno bisogno di più di 100 seguenti).
   
    ![Azione di query completa hello](./media/connectors-native-query/using-action-2.png)
   
    azione di Hello output conterrà una nuova matrice che contiene solo i risultati che soddisfano i requisiti di filtro hello.
6. Fare clic su nell'angolo superiore sinistro hello di hello barra degli strumenti toosave e la logica app verrà entrambi salvare e pubblicare (attivare).

## <a name="query-action"></a>Azione di query
Ecco hello dettagli per l'azione di hello che supporta questo connettore. connettore Hello è un'opzione possibile.

| Azione | Descrizione |
| --- | --- |
| Filtra matrice |Valuta una condizione per ogni elemento in una matrice e restituisce i risultati di hello |

## <a name="action-details"></a>Informazioni dettagliate sulle azioni
l'azione di query Hello viene fornito con un'azione possibile. Hello nelle tabelle seguenti vengono descritti hello necessarie e i campi di input facoltativi per azione di hello e i dettagli di output corrispondenti hello associati mediante l'azione di hello.

### <a name="filter-array"></a>Filtra matrice
di seguito Hello sono campi di input per l'azione di hello, che esegue una richiesta HTTP in uscita.
Un asterisco (*) indica che è un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Da* |from |Hello matrice toofilter |
| Condizione* |dove |Hello tooevaluate condizione per ogni elemento |

<br>

### <a name="output-details"></a>Dettagli dell'output
di seguito Hello sono i dettagli di output per hello risposta HTTP.

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| Matrice filtrata |array |Matrice che contiene un oggetto per ogni risultato filtrato |

## <a name="next-steps"></a>Passaggi successivi
A questo punto, provare a piattaforma hello e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md). È possibile esplorare altri connettori disponibile in App per la logica di hello esaminando il nostro [elenco API](apis-list.md).

