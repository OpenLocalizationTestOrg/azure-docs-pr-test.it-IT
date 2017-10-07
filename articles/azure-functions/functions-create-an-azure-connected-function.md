---
title: una funzione che si connette a servizi tooAzure aaaCreate | Documenti Microsoft
description: Utilizzare le funzioni di Azure toocreate un'applicazione senza che si connette tooother Azure servizi.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: Funzioni di Azure, Funzioni, elaborazione eventi, webhook, calcolo dinamico, architettura senza server
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Utilizzare le funzioni di Azure toocreate una funzione che si connette tooother Azure servizi

In questo argomento viene illustrata la modalità toocreate una funzione in funzioni di Azure che toomessages su un hello di coda e copie di archiviazione di Azure è in ascolto dei messaggi toorows in una tabella di archiviazione di Azure. Una funzione di timer di attivazione è tooload utilizzati messaggi nella coda di hello. Una seconda funzione legge dalla coda hello e scrive nella tabella toohello messaggi. Coda hello sia la tabella hello vengono creati automaticamente dalle funzioni di Azure in base alle definizioni di associazione hello. 

toomake cose più interessante, una funzione scritta in JavaScript e altri hello è scritto in c# script. Questo dimostra che un'app per le funzioni può avere funzioni scritte in linguaggi diversi. 

È possibile vedere la dimostrazione di questo scenario in un [video di Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Creare una funzione che scrive toohello coda

Prima di potersi connettere tooa coda di archiviazione, è necessario toocreate una funzione che carica la coda di messaggi hello. Questa funzione JavaScript utilizza un trigger timer che scrive una coda di messaggi toohello ogni 10 secondi. Se si dispone già di un account Azure, consultare hello [provare Azure funzioni](https://functions.azure.com/try) esperienza, o [creare l'account di Azure gratuita](https://azure.microsoft.com/free/).

1. Andare toohello portale di Azure e individuare l'app di funzione.

2. Fare clic su **Nuova funzione** > **TimerTrigger-JavaScript**. 

3. Nome funzione hello **FunctionsBindingsDemo1**, immettere un valore dell'espressione cron `0/10 * * * * *` per **pianificazione**, quindi fare clic su **crea**.
   
    ![Aggiungere una funzione attivata da un timer](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    A questo punto è stata creata una funzione attivata da un timer che viene eseguita ogni 10 secondi.

5. In hello **sviluppare** scheda, fare clic su **log** e visualizzare le attività di hello nel log di hello. Si noti che viene scritta una voce di log ogni 10 secondi.
   
    ![Funzionamento di visualizzazione hello log tooverify hello (funzione)](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Aggiungere un'associazione di output della coda dei messaggi

1. In hello **integrazione** scegliere **nuovo Output** > **coda di archiviazione di Azure** > **selezionare**.

    ![Aggiungere una funzione attivata da un timer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Immettere `myQueueItem` per **nome del parametro messaggio** e `functions-bindings` per **nome coda**, selezionare un oggetto esistente **connessione ad account di archiviazione** oppure fare clic su **nuova** toocreate uno spazio di archiviazione account di connessione e quindi fare clic su **salvare**.  

    ![Creare una coda di archiviazione toohello associazione hello output](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. In hello **sviluppare** scheda, aggiungere hello toohello codice che segue:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Individuare hello *se* istruzione circa 9 della funzione hello di riga e di codice seguente hello di inserimento dopo tale istruzione.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Questo codice crea un **myQueueItem** e imposta il relativo **ora** timeStamp corrente di proprietà toohello. Aggiunge quindi hello nuova coda elemento toohello del contesto **myQueueItem** associazione.

3. Fare clic su **Salva ed esegui**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Visualizzare gli aggiornamenti di archiviazione usando Storage Explorer
È possibile verificare che la funzione sta visualizzando i messaggi nella coda di hello che è stato creato.  È possibile connettersi tooyour coda di archiviazione tramite Cloud Explorer in Visual Studio. Tuttavia, portale hello rende facile tooconnect tooyour account di archiviazione tramite Esplora archivi di Microsoft Azure.

1. In hello **integrazione** , fare clic sulla coda di associazione di output > **documentazione**Scopri hello stringa di connessione per l'account di archiviazione e copiare il valore di hello. Utilizzare questo account di archiviazione tooyour tooconnect valore.

    ![Scaricare Azure Storage Explorer](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Se non è già stato fatto, scaricare e installare [Microsoft Azure Storage Explorer](http://storageexplorer.com). 
 
3. In Esplora archivi, fare clic su hello tooAzure archiviazione icona della connessione, incollare la stringa di connessione hello nel campo hello e completare la procedura guidata hello.

    ![Storage Explorer aggiunge una connessione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. In **locale e associata**, espandere **gli account di archiviazione** > l'account di archiviazione > **code** > **funzioni-bindings**e verificare che i messaggi vengono scritti toohello coda.

    ![Visualizzazione di messaggi nella coda di hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Se la coda hello non esiste o è vuota, è probabilmente un problema con l'associazione di funzione o il codice.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Creare una funzione che legge dalla coda hello

Ora che hai aggiunti toohello coda di messaggi, è possibile creare un'altra funzione che legge dalla coda hello hello scrive i messaggi e in modo permanente tooan tabella di archiviazione di Azure.

1. Fare clic su **Nuova funzione** > **QueueTrigger-CSharp**. 
 
2. Nome funzione hello `FunctionsBindingsDemo2`, immettere **funzioni associazioni** in hello **nome coda** campo, selezionare un account di archiviazione esistente o crearne uno e quindi fare clic su **crea**.

    ![Aggiungere una funzione timer della coda di output](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Facoltativo) È possibile verificare che hello nuovo funzionamento visualizzando nuova coda hello in soluzioni di archiviazione come prima. È anche possibile usare Visual Studio Cloud Explorer.  

4. (Facoltativo) Aggiornare hello **funzioni associazioni** coda e notare che sono stati rimossi elementi dalla coda hello. Hello rimozione si verifica perché la funzione hello associato toohello **funzioni associazioni** coda come una funzione di trigger e hello input legge coda hello. 
 
## <a name="add-a-table-output-binding"></a>Aggiungere un'associazione di output della tabella

1. In FunctionsBindingsDemo2 fare clic su **Integrazione** > **Nuovo output** > **Archiviazione tabelle di Azure** > **Seleziona**.

    ![Aggiungere una tabella di archiviazione di Azure tooan associazione](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Immettere `functionbindings` per **Nome tabella** e `myTable` per **Nome del parametro della tabella**, scegliere una **Connessione dell'account di archiviazione** o crearne una nuova e quindi fare clic su **Salva**.

    ![Configurare l'associazione di tabella di archiviazione hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. In hello **sviluppare** scheda, sostituire il codice di funzione esistente hello con hello seguente:
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Hello **TableItem** classe rappresenta una riga nella tabella di archiviazione hello e si aggiunta hello elemento toohello `myTable` insieme di **TableItem** oggetti. È necessario impostare hello **PartitionKey** e **RowKey** tooinsert in grado di proprietà toobe nella tabella hello.

4. Fare clic su **Salva**.  Infine, è possibile verificare il funzionamento di funzione hello visualizzando la tabella hello in soluzioni di archiviazione o di Visual Studio Cloud Explorer.

5. (Facoltativo) Nell'account di archiviazione in Esplora archivi, espandere **tabelle** > **functionsbindings** e verificare che le righe vengono aggiunte toohello tabella. È possibile eseguire stesso hello in Cloud Explorer in Visual Studio.

    ![Visualizzazione di righe nella tabella hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Se la tabella hello non esiste o è vuota, è probabilmente un problema con l'associazione di funzione o il codice. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulle funzioni di Azure, vedere hello seguenti argomenti:

* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](functions-reference.md)  
  Informazioni di riferimento per programmatori in merito alla codifica delle funzioni e alla definizione di trigger e associazioni.
* [Test di Funzioni di Azure](functions-test-a-function.md)  
  Descrive diversi strumenti e tecniche per il test delle funzioni.
* [Come tooscale funzioni di Azure](functions-scale.md)  
  Vengono descritti i piani di servizio disponibili con le funzioni di Azure, piano di hosting consumo hello e come toochoose hello giusta. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

