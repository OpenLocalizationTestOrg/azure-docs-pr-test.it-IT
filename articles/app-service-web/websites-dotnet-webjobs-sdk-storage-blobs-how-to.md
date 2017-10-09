---
title: aaaHow toouse archiviazione blob di Azure con hello WebJobs SDK
description: Informazioni su come toouse Azure blob storage con hello WebJobs SDK. Attivare un processo quando viene visualizzato un nuovo BLOB in un contenitore e gestire i BLOB non elaborabili.
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a>La modalità di archiviazione con blob di Azure toouse hello WebJobs SDK
## <a name="overview"></a>Panoramica
Questa guida fornisce c# degli esempi di codice che mostrano come tootrigger un processo quando un blob di Azure viene creato o aggiornato. utilizzo di esempi di codice Hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md) versione 1. x.

Per esempi di codice che mostrano come toocreate BLOB, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Guida di Hello presuppone che si conosca [toocreate un progetto processo Web in Visual Studio con connessione come stringhe di account di archiviazione punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o troppo[più account di archiviazione](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Come tootrigger una funzione quando un blob viene creato o aggiornato
Questa sezione viene illustrato come hello toouse `BlobTrigger` attributo. 

> [!NOTE]
> Hello WebJobs SDK toowatch file log di analisi per i BLOB nuovo o modificato. Questo processo non è in tempo reale; una funzione potrebbe non viene generata finché diversi minuti o più dopo aver creato il blob hello. I [log di archiviazione vengono creati in base al principio del "massimo sforzo"](https://msdn.microsoft.com/library/azure/hh343262.aspx). Non è garantito che tutti gli eventi vengano acquisiti. In alcune condizioni, l'acquisizione dei log potrebbe non riuscire. Se i limiti di velocità e affidabilità hello dei trigger di blob non sono accettabili per l'applicazione, hello consigliato metodo è un messaggio nella coda toocreate quando si crea il blob hello e utilizza hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attributo invece di Hello `BlobTrigger` attributo nella funzione hello che elabora i blob hello.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Singolo segnaposto per il nome di BLOB con estensione
Hello nell'esempio di codice seguente consente di copiare BLOB di testo che vengono visualizzati in hello *input* contenitore toohello *output* contenitore:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di contenitore hello e un segnaposto per il nome di blob hello. In questo esempio, se un blob denominato *Blob1.txt* viene creato in hello *input* contenitore, la funzione hello crea un blob denominato *Blob1.txt* in hello *output*  contenitore. 

È possibile specificare un modello di nome con segnaposto per nome blob hello, come illustrato nel seguente esempio di codice hello:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Questo codice copia solo BLOB con nomi che iniziano con "original-". Ad esempio, *originale Blob1.txt* in hello *input* contenitore viene copiato troppo*copia Blob1.txt* in hello *output* contenitore.

Se è necessario un modello di nome toospecify per i nomi di blob con parentesi graffe nel nome di hello, raddoppiare le parentesi graffe di hello. Ad esempio, se si desidera BLOB toofind in hello *immagini* contenitore i cui nomi simile al seguente:

        {20140101}-soundfile.mp3

usare questa soluzione per il modello:

        images/{{20140101}}-{name}

Nell'esempio hello hello *nome* il valore di segnaposto *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Segnaposto di nome ed estensione di BLOB separati
Hello seguenti modifiche di esempio di codice hello estensione di file come copia di blob che vengono visualizzati in hello *input* contenitore toohello *output* contenitore. codice Hello Registra estensione hello di hello *input* blob e imposta l'estensione hello di hello *output* blob troppo*. txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a id="types"></a>Tipi che è possibile associare tooblobs
È possibile utilizzare hello `BlobTrigger` attributo hello seguenti tipi:

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* Altri tipi deserializzati da [ICloudBlobStreamBinder](#icbsb) 

Se si desidera toowork direttamente con hello account di archiviazione di Azure, è inoltre possibile aggiungere un `CloudStorageAccount` firma del metodo toohello parametro.

Per esempi, vedere hello [blob codice di associazione nel repository di azure-sdk-processi Web hello in GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Recupero di contenuto di testo blob dall'associazione toostring
Se si prevede che il BLOB di testo, `BlobTrigger` può essere applicato tooa `string` parametro. esempio di codice seguente Hello associa un tooa blob testo `string` parametro denominato `logMessage`. funzione Hello utilizza tale contenuto hello toowrite dei parametri di hello blob toohello dashboard WebJobs SDK. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a> Ottenere contenuti di BLOB serializzati tramite ICloudBlobStreamBinder
Hello nell'esempio di codice seguente viene utilizzata una classe che implementa `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind toohello un blob di attributo `WebImage` tipo.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

Hello `WebImage` codice di associazione è disponibile in un `WebImageBinder` classe che deriva da `ICloudBlobStreamBinder`.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a>Recupero di percorso blob hello per hello attivazione blob
nome del contenitore tooget hello e nome del blob del blob hello che ha attivato la funzione hello, includere un `blobTrigger` parametro nella firma della funzione hello di stringa.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Come non elaborabili toohandle BLOB
Quando un `BlobTrigger` funzione ha esito negativo, hello SDK chiama nuovamente, in caso di errore hello è stato causato da un errore temporaneo. Se l'errore hello è causato da contenuto hello del blob hello, funzione hello ha esito negativo di ogni volta che tenta di blob hello tooprocess. Per impostazione predefinita, hello SDK chiama una funzione i tempi di too5 per un blob specificato. Se non riesce try quinto hello, hello SDK aggiunge una coda di messaggi tooa denominata *non elaborabili processi Web-blobtrigger*.

Hello il numero massimo di tentativi è configurabile. Hello stesso [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) impostazione viene utilizzata per la gestione di messaggi non elaborabili blob e la gestione dei messaggi di coda non elaborabile. 

messaggio della coda Hello per i BLOB non elaborabile è un oggetto JSON contenente hello le proprietà seguenti:

* FunctionId (in formato hello *{nome del processo Web}*. Funzioni. *{Nome della funzione}*, ad esempio: WebJob1.Functions.CopyBlob)
* BlobType ("BlockBlob" o "PageBlob")
* ContainerName
* BlobName
* ETag (identificatore di versione del BLOB, ad esempio: "0x8D1DC6E70A277EF")

In seguito hello esempio di codice, hello `CopyBlob` funzione dispone di codice che causa toofail ogni volta che viene chiamato. Dopo aver hello SDK chiama per il numero massimo di hello di tentativi, viene creato un messaggio nella coda di messaggi non elaborabili blob hello e che il messaggio viene elaborato da hello `LogPoisonBlob` (funzione). 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Hello SDK deserializza automaticamente messaggio JSON. Ecco hello `PoisonBlobMessage` classe: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a> Algoritmo di polling di BLOB
Hello WebJobs SDK analizza tutti i contenitori specificati da `BlobTrigger` attributi all'avvio dell'applicazione. In un account di archiviazione di grandi dimensioni l'analisi può richiedere tempo, pertanto l'individuazione di nuovi BLOB e l'esecuzione delle funzioni `BlobTrigger` potrebbero non essere immediate.

toodetect BLOB nuove o modificate dopo l'avvio dell'applicazione, hello che SDK legge periodicamente dall'archiviazione blob hello Registra. Hello blob vengono memorizzati nel buffer e registri solo ottengano scritta fisicamente ogni 10 minuti oppure in tal caso, pertanto potrebbero esserci un ritardo significativo dopo un blob viene creato o aggiornato prima hello corrispondente `BlobTrigger` funzione viene eseguita. 

Si verifica un'eccezione per i BLOB creati tramite hello `Blob` attributo. Quando hello WebJobs SDK crea un nuovo blob, passa immediatamente nuovo blob hello tooany corrispondenza `BlobTrigger` funzioni. Pertanto se si dispone di una catena di blob input e output, hello SDK possa elaborarli in modo efficiente. Se invece si desidera una bassa latenza per l'esecuzione delle funzioni di elaborazione dei BLOB creati o aggiornati in altri modi, è consigliabile usare `QueueTrigger` anziché `BlobTrigger`.

### <a id="receipts"></a> Conferme di BLOB
Hello WebJobs SDK garantisce che nessun `BlobTrigger` funzione viene chiamato più volte per hello stesso nuovo o aggiornato i blob. Ciò avviene tramite la gestione di *blob conferme di recapito* in ordine toodetermine se è stata elaborata una versione di blob specificato.

BLOB conferme di recapito vengono archiviati in un contenitore denominato *ospita-processi Web di azure* nell'account di archiviazione Azure hello specificato dalla stringa di connessione AzureWebJobsStorage hello. Un carico di blob è hello le seguenti informazioni:

* funzione che è stato chiamato per blob hello Hello ("*{nome del processo Web}*. Funzioni. *{Nome della funzione}*", ad esempio:"WebJob1.Functions.CopyBlob")
* nome del contenitore Hello
* tipo di blob Hello ("BlockBlob" o "PageBlob")
* nome del blob Hello
* Hello ETag (un identificatore di versione del blob, ad esempio: "0x8D1DC6E70A277EF")

Se si desidera tooforce rielaborazione di un blob, è possibile eliminare manualmente conferma di blob hello per tale blob da hello *ospita-processi Web di azure* contenitore.

## <a id="queues"></a>Argomenti correlati cui all'articolo code hello
Per informazioni su come l'elaborazione di blob toohandle attivata da un messaggio nella coda o per i processi Web scenari SDK non tooblob specifico, l'elaborazione, vedere [toouse Azure come coda di archiviazione con hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Argomenti trattati in tale articolo includono hello informazioni seguenti:

* Funzioni asincrone
* Più istanze
* Arresto normale
* Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione
* Impostare le stringhe di connessione SDK hello nel codice.
* Impostare i valori per i parametri del costruttore WebJobs SDK nel codice
* Configurare `MaxDequeueCount` per la gestione di BLOB non elaborabili.
* Attivare manualmente una funzione
* Scrivere i log

## <a id="nextsteps"></a> Passaggi successivi
Questa guida fornisce esempi di codice che mostrano come toohandle scenari comuni per l'utilizzo con Azure BLOB. Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

