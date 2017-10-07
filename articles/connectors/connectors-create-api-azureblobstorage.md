---
title: hello aaaAdd connettore in App per la logica di archiviazione blob Azure | Documenti Microsoft
description: Avviare e configurare connettore di archiviazione blob di Azure hello in un'app di logica
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>Utilizzare il connettore di archiviazione blob di Azure hello in una app logica
Tooupload di connettore archiviazione Blob di Azure hello usare, aggiornare, ottenere ed eliminare BLOB nell'account di archiviazione, tutti in un'app di logica.  

Con Archiviazione BLOB di Azure:

* Il flusso di lavoro si crea caricando nuovi progetti o recuperando file aggiornati di recente.
* Utilizzare i metadati del file tooget azioni, eliminare un file, la copia di file e altro ancora. Ad esempio, quando viene aggiornato uno strumento in un sito Web di Azure (trigger), viene aggiornato un file nell'archivio BLOB (azione). 

Questo argomento viene illustrato come toouse hello blob connettore di archiviazione in un'app di logica.

toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

toolearn informazioni sulle App per la logica, vedere [quali sono le app logica](../logic-apps/logic-apps-what-are-logic-apps.md) e [creare un'app di logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-blob-storage"></a>La connessione di archiviazione blob tooAzure
Prima che la logica app possa accedere a qualsiasi servizio, creare innanzitutto un *connessione* toohello servizio. Una connessione fornisce la connettività tra un'app per la logica e un altro servizio. Ad esempio, account di archiviazione tooa tooconnect, creare innanzitutto un'archiviazione blob *connessione*. toocreate una connessione, immettere le credenziali di hello utilizzato normalmente il servizio di hello tooaccess ci si connette a. Immettere quindi hello credenziali tooyour archiviazione toocreate hello connessione ad account di archiviazione di Azure. 

#### <a name="create-hello-connection"></a>Creare una connessione hello
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>Usare un trigger
Questo connettore non include trigger. Usare altri trigger toostart hello logica app, ad esempio un trigger di ricorrenza, un trigger HTTP Webhook, i trigger disponibili con altri connettori e altro ancora. [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) illustra un esempio.

## <a name="use-an-action"></a>Usare un'azione
Un'azione è un'operazione effettuata dal flusso di lavoro hello definito in un'app di logica.

1. Selezionare hello sul segno più. Vedrai diverse opzioni: **aggiungere un'azione**, **aggiungere una condizione**, o uno dei hello **più** opzioni.
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di testo hello, digitare "blob" tooget un elenco di tutte le azioni disponibili hello.
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. Nell'esempio scegliere **AzureBlob - Ottieni metadati file in base al percorso**. Se esiste già una connessione, quindi selezionare hello **...** (Mostra selezione) pulsante tooselect un file.
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    Se viene chiesto di hello informazioni di connessione, quindi immettere connessione hello toocreate dettagli di hello. [Creare una connessione hello](connectors-create-api-azureblobstorage.md#create-the-connection) in questo argomento vengono descritte queste proprietà. 
   
   > [!NOTE]
   > In questo esempio è ottenere hello metadati di un file. toosee hello metadati, aggiungere un'altra operazione che crea un nuovo file usando un altro connettore. Ad esempio, aggiungere un'azione di OneDrive che crea un nuovo file "test" in base ai metadati hello. 


5. **Salvare** le modifiche (angolo superiore sinistro della barra degli strumenti hello). L'app per la logica viene salvata e può essere attivata automaticamente.

> [!TIP]
> [Esplora archivi](http://storageexplorer.com/) è un ottimo strumento troppo gestire più account di archiviazione.

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/azureblobconnector/). 

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md). Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).

