---
title: gli endpoint REST aaaCall con HTTP + Swagger connettore per le app di logica di Azure | Documenti Microsoft
description: Connettersi tooREST endpoint da App per la logica tramite Swagger con hello HTTP + connettore Swagger
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Introduzione a salve HTTP + azione Swagger

È possibile creare un endpoint REST di prima classe connettore tooany tramite un [Swagger documento](https://swagger.io) quando si Usa HTTP hello + Swagger azione nel flusso di lavoro logica app. È anche possibile estendere la logica App toocall qualsiasi endpoint REST con un'esperienza di progettazione applicazione la logica di prima classe.

toolearn toocreate logica App con i connettori, vedere [crea una nuova app logica](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Usare HTTP + Swagger come trigger o azione

salve HTTP + Swagger trigger e action lavoro hello stesso come hello [azione HTTP](connectors-native-http.md) , ma forniscono una migliore esperienza di progettazione applicazione logica esponendo struttura hello API e gli output di hello [metadati Swagger](https://swagger.io) . È inoltre possibile utilizzare hello HTTP + connettore Swagger come trigger. Se si vuole tooimplement un trigger di polling, seguire il polling di hello modello descritto in [creare toocall API personalizzato altri sistemi, servizi e le API da logica app](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Altre informazioni sui [trigger e le azioni nelle app per la logica](connectors-overview.md).

Di seguito è riportato un esempio di come toouse hello HTTP + Swagger operazione come un'azione in un flusso di lavoro in un'app di logica.

1. Seleziona hello **nuovo passaggio** pulsante.
2. Selezionare **Aggiungi un'azione**.
3. Nella casella di ricerca azione hello, digitare **swagger** hello toolist HTTP + Swagger azione.
   
    ![Selezionare l'azione HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. Digitare l'URL hello per un documento di Swagger:
   
   * toowork da hello progettazione logica App hello URL deve essere un endpoint HTTPS e avere abilitata la condivisione CORS.
   * Se il documento di Swagger hello non soddisfa questo requisito, è possibile utilizzare [archiviazione di Azure con CORS abilitato](#hosting-swagger-from-storage) documento hello toostore.
5. Fare clic su **Avanti** tooread e rendering da hello Swagger documento.
6. Aggiungere i parametri necessari per la chiamata hello HTTP.
   
    ![Completare l'azione HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave e pubblicare l'app logica, fare clic su **salvare** sulla barra degli strumenti della finestra di progettazione.

### <a name="host-swagger-from-azure-storage"></a>Ospitare Swagger da Archiviazione di Azure
È possibile tooreference un documento di Swagger che non è ospitato o che non soddisfa i requisiti di sicurezza e cross-origin hello per progettazione hello. tooresolve questo problema, è possibile archiviare documenti Swagger hello in archiviazione di Azure e abilitare CORS tooreference hello documenti.  

Di seguito sono toocreate passaggi hello, configurare e archiviare documenti Swagger in archiviazione di Azure:

1. [Creare un account di Archiviazione di Azure con Archiviazione BLOB di Azure](../storage/common/storage-create-storage-account.md). tooperform questo passaggio, impostazione delle autorizzazioni troppo**accesso pubblico**.

2. Abilitare CORS nel blob hello. 

   tooautomatically configurare questa impostazione, è possibile utilizzare [questo script di PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Caricare blob toohello file Swagger di hello. 

   È possibile eseguire questo passaggio da hello [portale di Azure](https://portal.azure.com) o da uno strumento come [Azure Storage Explorer](http://storageexplorer.com/).

4. Fare riferimento a un documento di toohello collegamento HTTPS nell'archiviazione Blob di Azure. 

   collegamento Hello viene utilizzato questo formato:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Dettagli tecnici
Di seguito sono hello i dettagli per azioni e trigger hello da questo HTTP + Swagger connettore supporta.

## <a name="http--swagger-triggers"></a>Trigger HTTP + Swagger
Un trigger è un evento che può essere utilizzato toostart hello flusso di lavoro che è definito in un'app di logica. [Altre informazioni sui trigger.](connectors-overview.md) Hello HTTP + Swagger connettore dispone di un trigger.

| Trigger | Descrizione |
| --- | --- |
| HTTP + Swagger |Effettuare una chiamata HTTP e restituiscono contenuto della risposta hello |

## <a name="http--swagger-actions"></a>Azioni HTTP + Swagger
Un'azione è un'operazione che viene eseguita dal flusso di lavoro hello è definito in un'app di logica. [Ulteriori informazioni sulle azioni.](connectors-overview.md) Hello HTTP + Swagger connettore dispone di un'azione possibile.

| Azione | Descrizione |
| --- | --- |
| HTTP + Swagger |Effettuare una chiamata HTTP e restituiscono contenuto della risposta hello |

### <a name="action-details"></a>Informazioni dettagliate sulle azioni
Hello HTTP + Swagger connettore viene fornito con un'azione possibile. Di seguito è informazioni su ognuna delle azioni di hello, i relativi campi di input obbligatori e facoltativi e hello corrispondente dettagli output associati al loro utilizzo.

#### <a name="http--swagger"></a>HTTP + Swagger
Eseguire una richiesta HTTP in uscita con l'assistenza dei metadati Swagger.
L'asterisco (*) indica un campo obbligatorio.

| Nome visualizzato | Nome proprietà | Descrizione |
| --- | --- | --- |
| Metodo* |statico |Toouse verbo HTTP. |
| URI* |Uri |URI di richiesta HTTP hello. |
| Headers |headers |Oggetto JSON di tooinclude intestazioni HTTP. |
| Corpo |body |Hello corpo della richiesta HTTP. |
| Autenticazione |authentication |Autenticazione toouse per richiesta. Per ulteriori informazioni, vedere hello [connettore HTTP](connectors-native-http.md#authentication). |

**Dettagli dell'output**

Risposta HTTP

| Nome proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| headers |object |Intestazioni della risposta |
| Corpo |object |Oggetto della risposta |
| Codice di stato |int |Stato codice HTTP |

### <a name="http-responses"></a>Risposte HTTP
Quando si effettuano chiamate toovarious azioni, si potrebbero ottenere alcune risposte. Di seguito è riportata una tabella contenente le risposte e le descrizioni corrispondenti.

| Nome | Descrizione |
| --- | --- |
| 200 |OK |
| 202 |Accepted |
| 400 |Richiesta non valida |
| 401 |Non autorizzata |
| 403 |Accesso negato |
| 404 |Non trovato |
| 500 |Errore interno del server. Si è verificato un errore sconosciuto. |

- - -
## <a name="next-steps"></a>Passaggi successivi

* [Creare un'app per la logica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Trovare altri connettori](apis-list.md)