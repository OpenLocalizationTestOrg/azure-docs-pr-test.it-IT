---
title: aaaStore dati non strutturati tramite le funzioni di Azure e Cosmos DB
description: Archiviare dati non strutturati tramite Funzioni di Azure e Cosmos DB
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, Cosmos DB, calcolo dinamico, architettura senza server
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Archiviare dati non strutturati tramite Funzioni di Azure e Cosmos DB

[Azure DB Cosmos](https://azure.microsoft.com/services/cosmos-db/) è un ottimo modo toostore non strutturati e i dati JSON. Insieme a Funzioni di Azure, Cosmos DB semplifica e velocizza l'archiviazione dei dati con una quantità minore di codice rispetto a quella necessaria per l'archiviazione dei dati in un database relazionale.

Nelle funzioni di Azure, le associazioni di input e outpue forniscono dati di servizio tooexternal tooconnect una modalità dichiarativa dalla funzione. In questo argomento, informazioni su come tooupdate un esistente c# funzione tooadd un'associazione di output che archivia i dati non strutturati in un documento DB Cosmos. 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Aggiungere un binding di output

1. Espandere sia l'app per le funzioni sia la funzione.

1. Selezionare **integrazione** e **+ nuovo Output**, ovvero hello in alto a destra della pagina hello. Scegliere **Azure Cosmos DB**, quindi fare clic su **Seleziona**.

    ![Aggiungere un binding di output di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Hello utilizzare **output Azure Cosmos DB** impostazioni come specificato nella tabella hello: 

    ![Configurare il binding di output di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Impostazione      | Valore consigliato  | Descrizione                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Nome del parametro del documento** | taskDocument | Nome che fa riferimento a oggetto DB Cosmos toohello nel codice. |
    | **Database name** (Nome database) | taskDatabase | Nome del database toosave documenti. |
    | **Nome raccolta** | TaskCollection | Nome della raccolta di database di Cosmos DB. |
    | **Se true, Crea raccolta e il database DB Cosmos hello** | Selezionato | raccolta di Hello non esiste già, quindi crearla. |

4. Selezionare **New** toohello Avanti **connessione documento Cosmos DB** etichetta, quindi selezionare **+ Crea nuovo**. 

5. Hello utilizzare **nuovo account** impostazioni come specificato nella tabella hello: 

    ![Configurare la connessione di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Impostazione      | Valore consigliato  | Descrizione                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **ID** | Nome del database | ID univoco per il database DB Cosmos hello  |
    | **API** | SQL (DocumentDB) | Selezionare l'API di database documento hello.  |
    | **Sottoscrizione** | Sottoscrizione di Azure | Sottoscrizione di Azure  |
    | **Gruppo di risorse** | myResourceGroup |  Usare gruppo di risorse esistente hello che contiene l'app di funzione. |
    | **Posizione**  | Europa occidentale | Selezionare una posizione accanto tooeither l'app di funzione o tooother App che usano hello documenti archiviati.  |

6. Fare clic su **OK** database hello toocreate. Potrebbe richiedere alcuni database di hello toocreate minuti. Dopo aver creato il database di hello, stringa di connessione database hello è archiviato come un'impostazione di app di funzione. nome Hello di questa impostazione di app viene inserita nella **connessione ad account Cosmos DB**. 
 
8. Dopo aver impostata la stringa di connessione hello, selezionare **salvare** associazione hello toocreate.

## <a name="update-hello-function-code"></a>Aggiornare il codice di funzione hello

Sostituire hello c# funzione codice esistente con hello seguente codice:

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
In questo esempio di codice legge hello richiesta HTTP le stringhe di query e li assegna toofields in hello `taskDocument` oggetto. Hello `taskDocument` associazione invia dati dell'oggetto hello da questo toobe di parametro di associazione archiviati nel database di hello documento associato. database Hello viene creata la prima esecuzione funzione hello di hello.

## <a name="test-hello-function-and-database"></a>Funzione hello test e database

1. Finestra di destra hello espandere e selezionare **Test**. In **Query**, fare clic su **+ Aggiungi parametro** e aggiungere hello seguente stringa di query toohello parametri:

    + `name`
    + `task`
    + `duedate`

2. Fare clic su **Esegui** e verificare che venga restituito uno stato 200.

    ![Configurare il binding di output di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. Hello il lato sinistro di hello portale di Azure, espandere barra delle icone hello tipo `cosmos` in hello ricerca campo e selezionare **Azure Cosmos DB**.

    ![Cercare hello servizio Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Database selezionare hello è stato creato, quindi selezionare **Esplora dati**. Espandere hello **raccolte** nodi, selezionare nuovo documento hello e verificare che il documento hello contiene i valori di stringa di query, con alcuni metadati aggiuntivi. 

    ![Verificare la voce di Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

È stato aggiunto correttamente un trigger HTTP tooyour di associazione che contiene dati non strutturati in un database DB Cosmos.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Per ulteriori informazioni sul binding tooa DB Cosmos database, vedere [associazioni Azure funzioni Cosmos DB](functions-bindings-documentdb.md).
