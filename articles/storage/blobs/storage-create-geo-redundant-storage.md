---
title: "Applicare la disponibilità elevata ai dati delle applicazioni in Azure | Microsoft Docs"
description: "Usare l'archiviazione con ridondanza geografica e accesso in lettura per applicare la disponibilità elevata ai dati delle applicazioni"
services: storage
documentationcenter: 
author: georgewallace
manager: jeconnoc
editor: 
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: gwallace
ms.custom: mvc
ms.openlocfilehash: 63ca91c2eadf7b003427e9716d99621fca1b1a19
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="make-your-application-data-highly-available-with-azure-storage"></a>Applicare la disponibilità elevata ai dati delle applicazioni con l'archiviazione di Azure

Questa è la prima di una serie di esercitazioni. Questa esercitazione illustra come applicare la disponibilità elevata ai dati delle applicazioni in Azure. Al termine, si dispone di un'applicazione console principale di .NET che carica e recupera un blob da un [geograficamente ridondante con accesso in lettura](../common/storage-redundancy.md#read-access-geo-redundant-storage) account di archiviazione (RA-GRS). L'archiviazione con ridondanza geografica e accesso in lettura funziona replicando le transazioni dall'area primaria all'area secondaria. Il processo di replica garantisce che i dati nell'area secondaria abbiano coerenza finale. L'applicazione usa il criterio [Interruttore](https://docs.microsoft.com/azure/architecture/patterns/circuit-breaker) per determinare l'endpoint a cui connettersi. L'applicazione passa all'endpoint secondario quando viene simulato un errore.

Nella prima parte della serie si apprenderà come:

> [!div class="checklist"]
> * Creare un account di archiviazione
> * Scaricare l'esempio
> * Impostare la stringa di connessione
> * Eseguire l'applicazione console

## <a name="prerequisites"></a>Prerequisiti

Per completare questa esercitazione:

* Installare [Visual Studio 2017](https://www.visualstudio.com/downloads/) con i carichi di lavoro seguenti:
  - **Sviluppo di Azure**

  ![Sviluppo di Azure (in Web e cloud)](media/storage-create-geo-redundant-storage/workloads.png)

* Scaricare e installare [Fiddler](https://www.telerik.com/download/fiddler)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-the-azure-portal"></a>Accedere al Portale di Azure

Accedere al [Portale di Azure](https://portal.azure.com/).

## <a name="create-a-storage-account"></a>Creare un account di archiviazione

Un account di archiviazione offre uno spazio dei nomi univoco per archiviare gli oggetti dati di Archiviazione di Azure e accedere a tali oggetti.

Seguire questa procedura per creare un account di archiviazione con ridondanza geografica e accesso in lettura:

1. Selezionare il pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.

2. Selezionare **Archiviazione** nella pagina **Nuovo** e selezionare **Account di archiviazione: BLOB, File, Tabelle, Code** in **In primo piano**.
3. Compilare il modulo dell'account di archiviazione con le informazioni seguenti, come illustrato nell'immagine seguente e selezionare **Crea**:

   | Impostazione       | Valore consigliato | Descrizione |
   | ------------ | ------------------ | ------------------------------------------------- |
   | **Nome** | mystorageaccount | Un valore univoco per l'account di archiviazione |
   | **Modello di distribuzione** | Gestione risorse  | Gestione risorse include le funzionalità più recenti.|
   | **Tipo di account** | Scopo generico | Per informazioni dettagliate sui tipi di account, consultare i [tipi di account di archiviazione](../common/storage-introduction.md#types-of-storage-accounts) |
   | **Prestazioni** | Standard | Standard è sufficiente per lo scenario di esempio. |
   | **Replica**| Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS). | È necessario ai fini dell'esempio. |
   |**Trasferimento sicuro necessario** | Disabled| Il trasferimento sicuro non è necessario per questo scenario. |
   |**Sottoscrizione** | sottoscrizione in uso |Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni). |
   |**ResourceGroup** | myResourceGroup |Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). |
   |**Posizione** | Stati Uniti orientali | Scegliere un paese. |

![Creare un account di archiviazione](media/storage-create-geo-redundant-storage/figure1.png)

## <a name="download-the-sample"></a>Scaricare l'esempio

[Scaricare il progetto di esempio](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs/archive/master.zip).

Estrarre, ovvero decomprimere il file storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs.zip.
Il progetto di esempio contiene un'applicazione console.

## <a name="set-the-connection-string"></a>Impostare la stringa di connessione

Nell'applicazione è necessario inserire la stringa di connessione per l'account di archiviazione. È consigliabile archiviare la stringa di connessione all'interno di una variabile di ambiente nel computer locale che esegue l'applicazione. Seguire uno degli esempi di seguito a seconda del sistema operativo per creare la variabile di ambiente.

Nel portale di Azure, passare all'account di archiviazione. Selezionare **le chiavi di accesso** in **impostazioni** nell'account di archiviazione. Copia il **stringa di connessione** dalla chiave primaria o secondaria. Sostituire \<yourconnectionstring\> con la connessione effettiva stringa eseguendo uno dei seguenti comandi in base al sistema operativo. Questo comando Salva una variabile di ambiente al computer locale. In Windows, la variabile di ambiente non è disponibile fino a ricaricare la **prompt dei comandi** o shell in uso. Sostituire  **\<storageConnectionString\>**  nell'esempio seguente:

### <a name="linux"></a>Linux

```bash
export storageconnectionstring=<yourconnectionstring>
```

### <a name="windows"></a>Windows

```cmd
setx storageconnectionstring "<yourconnectionstring>"
```

![File App config](media/storage-create-geo-redundant-storage/figure2.png)

## <a name="run-the-console-application"></a>Eseguire l'applicazione console

In Visual Studio premere **F5** o selezionare **Avvia** per avviare il debug dell'applicazione. Visual studio automaticamente ripristini i pacchetti NuGet mancanti se configurato, visitare la pagina per [installare e reinstallare i pacchetti con ripristino del pacchetto](https://docs.microsoft.com/nuget/consume-packages/package-restore#package-restore-overview) per altre informazioni.

Si apre una finestra della console e l'applicazione avvia l'esecuzione. L'applicazione carica l'immagine **HelloWorld.png** dalla soluzione nell'account di archiviazione. L'applicazione verifica che l'immagine sia stata replicata nell'endpoint RA-GRS secondario. Si avvia quindi il download dell'immagine fino a 999 volte. Ogni lettura è rappresentato da un **P** o **S**. **P** rappresenta l'endpoint primario e **S** rappresenta l'endpoint secondario.

![App console in esecuzione](media/storage-create-geo-redundant-storage/figure3.png)

Nell'esempio di codice l'attività `RunCircuitBreakerAsync` nel file `Program.cs` viene usata per scaricare un'immagine dall'account di archiviazione con il metodo [DownloadToFileAsync](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadtofileasync?view=azure-dotnet). Prima del download viene definito [OperationContext](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.operationcontext?view=azure-dotnet). Il contesto dell'operazione definisce i gestori dell'evento, generati quando il download viene completato correttamente o se un download ha esito negativo ed esegue un nuovo tentativo.

### <a name="retry-event-handler"></a>Riprovare il gestore dell'evento

Il `OperationContextRetrying` gestore eventi viene chiamato quando il download dell'immagine non riesce e viene impostato su Riprova. Se viene raggiunto il numero massimo di tentativi, vengono definiti nell'applicazione, il [LocationMode](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.locationmode?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_LocationMode) della richiesta viene modificato in `SecondaryOnly`. Questa impostazione forza l'applicazione a tentare di scaricare l'immagine dall'endpoint secondario. Questa configurazione riduce il tempo necessario per richiedere che l'immagine non venga ripetuta all'infinito come endpoint primario.

```csharp
private static void OperationContextRetrying(object sender, RequestEventArgs e)
{
    retryCount++;
    Console.WriteLine("Retrying event because of failure reading the primary. RetryCount = " + retryCount);

    // Check if we have had more than n retries in which case switch to secondary.
    if (retryCount >= retryThreshold)
    {

        // Check to see if we can fail over to secondary.
        if (blobClient.DefaultRequestOptions.LocationMode != LocationMode.SecondaryOnly)
        {
            blobClient.DefaultRequestOptions.LocationMode = LocationMode.SecondaryOnly;
            retryCount = 0;
        }
        else
        {
            throw new ApplicationException("Both primary and secondary are unreachable. Check your application's network connection. ");
        }
    }
}
```

### <a name="request-completed-event-handler"></a>Gestore dell'evento per la richiesta completata

Quando il download dell'immagine riesce viene chiamato il gestore dell'evento `OperationContextRequestCompleted`. Se l'applicazione usa l'endpoint secondario, continua a usarlo fino a 20 volte. Dopo 20 volte, l'applicazione imposta la [LocationMode](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.blob.blobrequestoptions.locationmode?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_LocationMode) al `PrimaryThenSecondary` e ritenta l'endpoint primario. Se una richiesta ha esito positivo, l'applicazione continua a leggere l'endpoint primario.

```csharp
private static void OperationContextRequestCompleted(object sender, RequestEventArgs e)
{
    if (blobClient.DefaultRequestOptions.LocationMode == LocationMode.SecondaryOnly)
    {
        // You're reading the secondary. Let it read the secondary [secondaryThreshold] times, 
        //    then switch back to the primary and see if it's available now.
        secondaryReadCount++;
        if (secondaryReadCount >= secondaryThreshold)
        {
            blobClient.DefaultRequestOptions.LocationMode = LocationMode.PrimaryThenSecondary;
            secondaryReadCount = 0;
        }
    }
}
```

## <a name="next-steps"></a>Passaggi successivi

Nella prima parte della serie, è stato descritto come applicare la disponibilità elevata a un'applicazione con gli account di archiviazione RA-GRS, ad esempio come:

> [!div class="checklist"]
> * Creare un account di archiviazione
> * Scaricare l'esempio
> * Impostare la stringa di connessione
> * Eseguire l'applicazione console

Passare alla seconda parte della serie per informazioni su come simulare un errore e forzare l'applicazione a usare l'endpoint RA-GRS secondario.

> [!div class="nextstepaction"]
> [Simulare un errore nella connessione all'endpoint di archiviazione primario](storage-simulate-failure-ragrs-account-app.md)
