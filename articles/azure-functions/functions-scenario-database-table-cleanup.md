---
title: "aaaUse funzioni Azure tooperform un pulitura del database attività | Documenti Microsoft"
description: "Utilizzare le funzioni di Azure tooschedule un'attività che si connette tooAzure Database SQL tooperiodically eseguire la pulizia delle righe."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Utilizzare le funzioni di Azure tooconnect tooan Database SQL di Azure
Questo argomento viene illustrato come toouse toocreate di funzioni di Azure un processo che pulisce le righe in una tabella in un Database di SQL Azure. funzione Hello nuovo c# viene creato in base a un modello di trigger timer predefiniti nel portale di Azure hello. toosupport questo scenario, è necessario impostare anche una stringa di connessione di database come un'impostazione di app di funzione hello. Questo scenario viene utilizzata un'operazione bulk database hello. toohave la funzione processo singole operazioni CRUD in una tabella di App per dispositivi mobili, è opportuno utilizzare [associazioni di App per dispositivi mobili](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Prerequisiti

+ Questo argomento usa una funzione attivata da un timer. Hello completato i passaggi in argomento hello [creare una funzione in Azure che viene attivata da un timer](functions-create-scheduled-function.md) toocreate c# versione di questa funzione.   

+ In questo argomento viene illustrato un comando di Transact-SQL che esegue un'operazione di pulizia delle operazioni bulk in hello **SalesOrderHeader** tabella nel database di esempio AdventureWorksLT hello. database di esempio AdventureWorksLT hello toocreate, hello completato i passaggi in argomento hello [creare un database SQL di Azure nel portale di Azure hello](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Ottenere informazioni di connessione

Stringa di connessione hello tooget necessari per il database di hello è stato creato dopo avere completato [creare un database SQL di Azure nel portale di Azure hello](../sql-database/sql-database-get-started-portal.md).

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
 
3. Selezionare **database SQL** dal menu a sinistra, hello e selezionare il database in hello **database SQL** pagina.

4. Selezionare **Mostra le stringhe di connessione di database** hello copia completa e **ADO.NET** stringa di connessione.

    ![Copiare una stringa di connessione ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Impostare la stringa di connessione hello 

Un'app di funzione ospita esecuzione hello delle funzioni in Azure. È un stringhe di connessione di best practice toostore e altri segreti nelle impostazioni dell'app (funzione). Utilizzando le impostazioni dell'applicazione impedisce la diffusione accidentale della stringa di connessione hello con il codice. 

1. Passare tooyour funzione app creato [creare una funzione in Azure che viene attivata da un timer](functions-create-scheduled-function.md).

2. Selezionare **Funzionalità della piattaforma** > **Impostazioni applicazione**.
   
    ![Impostazioni applicazione per app di funzione hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Scorrere verso il basso troppo**le stringhe di connessione** e aggiungere una stringa di connessione utilizzando le impostazioni di hello come specificato nella tabella hello.
   
    ![Aggiungere impostazioni connessione stringa toohello funzione app.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Impostazione       | Valore consigliato | Descrizione             | 
    | ------------ | ------------------ | --------------------- | 
    | **Nome**  |  sqldb_connection  | Hello tooaccess utilizzati archiviati stringa di connessione nel codice di funzione.    |
    | **Valore** | Stringa copiata  | Dopo la stringa di connessione hello copiata nella sezione precedente hello. |
    | **Tipo** | Database SQL | Utilizzare connessione di Database SQL di hello predefinita. |   

3. Fare clic su **Salva**.

A questo punto, è possibile aggiungere hello funzione codice c# che si connette tooyour Database SQL.

## <a name="update-your-function-code"></a>Aggiornare il codice di funzione

1. Nell'app (funzione), Seleziona funzione di attivazione del timer hello.
 
3. Aggiungere hello riferimenti ad assembly nella parte superiore di hello hello esistente del codice di funzione seguente:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Aggiungere il seguente hello `using` funzione toohello istruzioni:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Sostituire hello **eseguire** funzione con hello seguente codice:
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    Questo comando di esempio aggiorna hello **stato** colonna in base alla data di spedizione hello. Aggiorna 32 righe di dati.

5. Fare clic su **salvare**, hello watch **registri** windows per hello successivamente funzione esecuzione, quindi annotare hello numero di righe aggiornate nella hello **SalesOrderHeader** tabella.

    ![Consente di visualizzare i log delle funzioni hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni come toouse funziona con la logica App toointegrate con altri servizi.

> [!div class="nextstepaction"] 
> [Creare una funzione che si integra con le app per la logica di Azure](functions-twitter-email.md)

Per ulteriori informazioni sulle funzioni, vedere hello seguenti argomenti:

* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)  
  Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.
* [Test di Funzioni di Azure](functions-test-a-function.md)  
  Descrive diversi strumenti e tecniche per il test delle funzioni.  
