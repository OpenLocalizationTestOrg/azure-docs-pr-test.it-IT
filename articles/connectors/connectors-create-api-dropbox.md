---
title: connettore aaaDropbox nelle app di logica di Azure | Documenti Microsoft
description: "Creare app per la logica in Servizio app di Azure. Connettersi tooDropbox toomanage i file. In Dropbox è possibile eseguire diverse azioni, ad esempio caricare, aggiornare, ottenere ed eliminare file."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Iniziare con il connettore di Dropbox hello
Connettersi tooDropbox toomanage i file. In Dropbox è possibile eseguire diverse azioni, ad esempio caricare, aggiornare, ottenere ed eliminare file.

toouse [i connettori](apis-list.md), è necessario innanzitutto toocreate un'app di logica. Come prima operazione [creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Connettersi tooDropbox
Prima che la logica app possa accedere a qualsiasi servizio, è necessario innanzitutto toocreate un *connessione* toohello servizio. Una connessione fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, in ordine tooconnect tooDropbox, è necessario innanzitutto una Dropbox *connessione*. toocreate una connessione, è necessario credenziali hello tooprovide utilizzato normalmente il servizio di hello tooaccess desiderato tooconnect per. Nell'esempio di hello Dropbox, in tal caso, sarebbe necessario hello credenziali tooyour account Dropbox in ordine toocreate hello connessione tooDropbox. [Altre informazioni sulle connessioni]()

### <a name="create-a-connection-toodropbox"></a>Creare una connessione tooDropbox
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Usare un trigger Dropbox
Un trigger è un evento che può essere utilizzato toostart flusso di lavoro hello definito in un'app di logica. [Altre informazioni sui trigger](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

In questo esempio utilizzeremo hello **quando viene creato un file** trigger. Quando si verifica questo trigger, chiameremo hello **ottenere il contenuto del file con percorso** azione Dropbox. 

1. Immettere *dropbox* nella casella di ricerca hello sulla progettazione di App per la logica di hello, quindi selezionare hello **Dropbox - quando viene creato un file** trigger.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Selezionare la cartella hello in cui si desidera tootrack la creazione di file. Seleziona... (identificato nella casella hello rosso) e Sfoglia toohello cartella in cui l'input del tooselect per trigger hello.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Usare un'azione Dropbox
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica. [Altre informazioni sulle azioni](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Ora che hello trigger è stato aggiunto, seguire questi tooadd passaggi un'azione che verrà visualizzato il contenuto di hello del nuovo file.

1. Selezionare **+ nuovo passaggio** azione hello tooadd desideri tootake quando viene creato un nuovo file.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Selezionare **Aggiungi un'azione**. Questa casella di ricerca hello viene visualizzata in cui è possibile cercare qualsiasi azione si desidera tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Immettere *dropbox* toosearch per azioni correlate tooDropbox.  
4. Selezionare **Dropbox - Get contenuto del file con percorso** come hello tootake azione quando viene creato un nuovo file in hello Dropbox cartella selezionata. verrà visualizzata la finestra di blocco di controllo azione Hello. Si sarà richiesta tooauthorize tooaccess di app la logica di Dropbox account se si è già stato in precedenza.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Seleziona... (posizione destra hello di hello **percorso del File** controllo) e individuare il percorso di file toohello toouse desiderato. In alternativa, usare hello **percorso del file** toospeed token backup la creazione di app logica.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Salvare il lavoro e creare un nuovo file in Dropbox tooactivate il flusso di lavoro.  

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/dropbox/).

## <a name="more-connectors"></a>Altri connettori
Tornare indietro toohello [elenco API](apis-list.md).
