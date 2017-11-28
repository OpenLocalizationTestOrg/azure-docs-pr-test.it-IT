---
title: aaaIndexing file multimediali con Azure Media Indexer
description: Azure Media Indexer consente toomake contenuto dei file multimediali ricercabili e toogenerate una trascrizione full-text per sottotitoli codificati e parole chiave. Questo argomento viene illustrato come toouse Media Indexer.
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Indicizzazione di file multimediali con Azure Media Indexer
Azure Media Indexer consente toomake contenuto dei file multimediali ricercabili e toogenerate una trascrizione full-text per sottotitoli codificati e parole chiave. È possibile elaborare un file multimediale o più file multimediali in un batch.  

> [!IMPORTANT]
> Quando l'indicizzazione dei contenuti, assicurarsi di toouse che i file multimediali con contenuto vocale molto chiaro (senza musica, rumore, effetti o fruscio del microfono). Alcuni esempi di contenuto appropriato includono riunioni registrate, lezioni o presentazioni. Hello contenuto seguente potrebbe non essere adatto per l'indicizzazione: film, programmi televisivi, qualsiasi valore con una combinazione di audio ed effetti sonori e, registrato di scarsa qualità contenuto con rumore di fondo (fruscio).
> 
> 

Un processo di indicizzazione è possibile generare hello seguente output:

* Chiusura dei file di sottotitoli nel hello seguenti formati: **SAMI**, **TTML**, e **WebVTT**.
  
    File di sottotitoli includono un tag denominato Recognizability, quali punteggi di un processo di indicizzazione in base a riconoscibilità vocale hello nel video di origine hello è.  È possibile utilizzare il valore di hello Recognizability tooscreen dei file di output ai fini dell'usabilità. Un punteggio basso comporterebbe insoddisfacente indicizzazione a causa di qualità tooaudio.
* File di parole chiave (XML).
* File BLOB di indicizzazione audio (AIB, Audio Indexing Blob) da usare con SQL Server.
  
    Per altre informazioni, vedere [Uso dei file AIB con Azure Media Indexer e SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

Questo argomento viene illustrato come l'indicizzazione toocreate processi troppo**indicizzare un asset** e **indicizzare più file**.

Per aggiornamenti di Azure Media Indexer hello più recenti, vedere [blog di servizi multimediali](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Uso di file configurazione e manifesto per l'indicizzazione delle attività
È possibile specificare più informazioni per le attività di indicizzazione usando una configurazione di attività. Ad esempio, è possibile specificare quali toouse metadati per il file di supporto. Questi metadati sono utilizzati da hello language motore tooexpand proprio vocabolario e migliorano notevolmente l'accuratezza del riconoscimento vocale hello.  Si sono in grado di toospecify anche i file di output desiderato.

È anche possibile elaborare più file multimediali contemporaneamente usando un file manifesto.

Per altre informazioni, vedere [Set di impostazioni di attività per Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Indicizzare un asset
Hello metodo seguente consente di caricare un file multimediale come asset e creare una risorsa di processo tooindex hello.

Si noti che se non viene specificato alcun file di configurazione, file di supporto hello verrà indicizzato con tutte le impostazioni predefinite.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>File di output
Per impostazione predefinita, un processo di indicizzazione genera i seguenti file di output di hello. nel primo asset di output hello verranno archiviati i file Hello.

Quando è presente più di un file multimediale di input, l'indicizzatore genererà un file manifesto per gli output dei processi hello, denominato "JobResult.txt". Per ogni file multimediale di input, hello risultante file AIB, SAMI, TTML, WebVTT e i file (parola chiave), sono in sequenza e numerati denominati utilizzando hello "Alias".

| Nome file | Descrizione |
| --- | --- |
| **InputFileName.aib** |File BLOB di indicizzazione audio. <br/><br/> Un file AIB (Audio Indexing Blob) è un file binario in cui è possibile eseguire ricerche full-text con Microsoft SQL Server.  file AIB Hello è più potente hello semplici file di sottotitoli perché contiene alternative per ogni parola, offrendo un'esperienza di ricerca molto più completa. <br/> <br/>Richiede l'installazione di hello del componente aggiuntivo Indexer SQL hello in un computer in esecuzione Microsoft SQL server 2008 o versione successivo. Ricerca hello file AIB con Microsoft SQL ricerca full-text server fornisce risultati più precisi maggiore hello di ricerca di file di sottotitoli generati da WAMI chiuso. Questo avviene perché hello AIB contiene parole alternative con un suono simile, mentre i file di didascalia chiusi hello contengono hello più elevata probabilità di word per ogni segmento dell'audio hello. Se la ricerca di descrizioni vocali è della massima importanza, è consigliabile toouse hello file Aib unitamente a Microsoft SQL Server.<br/><br/> toodownload hello componente aggiuntivo, fare clic su <a href="http://aka.ms/indexersql">componente aggiuntivo di SQL Azure Media Indexer</a>. <br/><br/>Si è anche possibile tooutilize altri motori di ricerca come Apache Lucene/Solr hello indice di toosimply video basati su hello chiuso didascalia e la parola chiave file XML, ma il risultato sarà nei risultati della ricerca meno precisi. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |File di sottotitoli (CC, Closed Caption) in formato SAMI, TTML e WebVTT.<br/><br/>Possono essere utilizzati toomake audio e video file toopeople accessibile con problemi uditivi.<br/><br/>File di sottotitoli chiusi includono un tag denominato <b>Recognizability</b> che assegna un punteggio a un processo di indicizzazione in base alla riconoscibilità vocale hello nel video di origine hello è.  È possibile utilizzare il valore di hello di <b>Recognizability</b> tooscreen file ai fini dell'usabilità di output. Un punteggio basso comporterebbe insoddisfacente indicizzazione a causa di qualità tooaudio. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Parola chiave e file di informazioni. <br/><br/>File di parole chiave è un file XML che contiene parole chiave estratte da contenuti vocali hello, con la frequenza e informazioni relative all'offset. <br/><br/>Il file di informazioni è un file di testo che contiene informazioni granulari su ogni termine riconosciuto. prima riga Hello è speciale e contiene il punteggio di Recognizability hello. Ogni riga successiva è un elenco separato da tabulazioni di hello dati seguenti: avviare ora, l'ora di fine, parola o frase, confidenza. Hello tempi sono espressi in secondi e confidenza hello viene fornito come un numero da 1 a 0. <br/><br/>Riga di esempio: "1.20    1.45    word    0.67" <br/><br/>Questi file possono essere utilizzati per diversi scopi, ad esempio, analitica vocale tooperform, o, ad esempio, Bing, Google o Microsoft SharePoint toomake hello file multimediali più individuabili o toodeliver anche utilizzati toosearch esposto motori di annunci pubblicitari più pertinenti. |
| **JobResult.txt** |Manifesto di output, presente solo quando l'indicizzazione di più file, contenenti hello le seguenti informazioni:<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>Errore</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Se non tutti i file multimediali di input vengono indicizzati correttamente, un processo di indicizzazione hello avrà esito negativo con codice errore 4000. Per altre informazioni, vedere [Codici di errore](#error_codes).

## <a name="index-multiple-files"></a>indicizzare più file
metodo Hello Carica più file multimediali come asset e tooindex un processo tutti questi file vengono creati in un batch.

Un file manifesto con estensione lst hello viene creato e caricato nell'asset hello. file manifesto Hello hello elenco di tutti i file di asset hello. Per altre informazioni, vedere [Set di impostazioni di attività per Azure Media Indexer](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Processo parzialmente completato
Se non tutti i file multimediali di input vengono indicizzati correttamente, un processo di indicizzazione hello avrà esito negativo con codice errore 4000. Per altre informazioni, vedere [Codici di errore](#error_codes).

Hello stessi output (i processi completati) vengono generati. È possibile fare riferimento toohello output file manifesto toofind quale file di input è stati eseguiti, in base toohello valori di colonna di errore. Per i file di input che non è riuscita, hello risultante file AIB, SAMI, TTML, WebVTT e non verranno generato il file (parola chiave).

### <a id="preset"></a> Set di impostazioni di attività per Azure Media Indexer
è possibile personalizzare l'elaborazione da Azure Media Indexer Hello fornendo un'attività facoltativa preimpostata insieme ad attività hello.  esempio Hello descrive il formato di hello di questo file di configurazione xml.

| Nome | Valore richiesto | Descrizione |
| --- | --- | --- |
| **input** |false |File di asset che si desidera tooindex.</p><p>Azure Media Indexer supporta i seguenti formati di file multimediali hello: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>È possibile specificare il nome di file hello (s) in hello **nome** o **elenco** attributo di hello **input** elemento (come illustrato di seguito). Se non si specifica quale tooindex di file di asset, file primario hello viene selezionato. Se è impostato alcun file di asset primario, viene indicizzato hello primo file di asset di input hello.</p><p>tooexplicitly specificare nome del file hello asset, eseguire:<br/>`<input name="TestFile.wmv">`<br/><br/>È anche possibile indicizzare più file di asset contemporaneamente (backup di file too10). toodo questo:<br/><br/><ol class="ordered"><li><p>Creare un file di testo (file manifesto) con estensione .lst. </p></li><li><p>Aggiungere un elenco di tutti i nomi di file di asset hello nel file manifesto toothis asset di input. </p></li><li><p>Aggiungere (caricare) manifesto file toohello asset.  </p></li><li><p>Specificare il nome di hello del file manifesto hello nell'attributo list di input hello.<br/>`<input list="input.lst">`</li></ol><br/><br/>Nota: Se si aggiunta più di 10 file manifesto di file toohello, hello indicizzazione processo avrà esito negativo con codice di errore 2006 hello. |
| **metadata** |false |Metadati per hello specificati file di asset utilizzati per l'adeguamento del vocabolario.  Tooprepare utile indicizzatore toorecognize vocabolario non standard parole come nomi propri.<br/>`<metadata key="..." value="..."/>` <br/><br/>È possibile assegnare i **valori** delle **chiavi** predefinite. È attualmente supportato hello seguenti chiavi:<br/><br/>"title" e "description" - usati per la lingua di vocabolario adattamento tootweak hello del modello per il processo e migliorare l'accuratezza del riconoscimento vocale.  i valori Hello seme Internet ricerche toofind attinenti documenti di testo, usando dizionario interno hello hello contenuto tooaugment per durata hello dell'attività di indicizzazione.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **Funzionalità** <br/><br/> Aggiunto nella versione 1.2. Funzionalità supportata solo hello è attualmente il riconoscimento vocale ("ASR"). |false |funzionalità di riconoscimento vocale Hello è hello le chiavi delle impostazioni seguenti:<table><tr><th><p>Chiave</p></th>        <th><p>Descrizione</p></th><th><p>Valore di esempio</p></th></tr><tr><td><p>Lingua</p></td><td><p>Hello riconosciuto nel file multimediale hello toobe di linguaggio naturale.</p></td><td><p>Inglese, spagnolo</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>un elenco delimitato da punto e virgola dei formati di didascalia di output di hello desiderato (se presente)</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Flag booleano che specifica se è o meno un file AIB (da utilizzare obbligatoriamente con IFilter Indexer del cliente hello e SQL Server).  Per altre informazioni, vedere <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Uso dei file AIB con Azure Media Indexer e SQL Server</a>.</p></td><td><p>True; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Flag booleano che specifica se sia o meno necessario un file XML di parole chiave.</p></td><td><p>True; False. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Flag booleano che specifica se consentire o meno tooforce completo didascalie (indipendentemente dal livello di confidenza).  </p><p>Valore predefinito è false, nel qual caso parole e frasi inferiore a livello di confidenza 50% vengono omesse dall'output di hello didascalia finale e sostituite da puntini di sospensione ("...").  puntini di sospensione Hello sono utili per il controllo di qualità di didascalia e il controllo.</p></td><td><p>True; False. </p></td></tr></table> |

### <a id="error_codes"></a>Codici di errore
Nel caso di hello di un errore, è necessario segnalare Azure Media Indexer eseguire il backup di uno dei seguenti codici di errore hello:

| Codice | Nome | Possibili cause |
| --- | --- | --- |
| 2000 |Configurazione non valida. |Configurazione non valida. |
| 2001 |Asset di input non valido |Asset di input mancanti o vuoti. |
| 2002 |File manifesto non valido |Il manifesto è vuoto oppure contiene elementi non validi. |
| 2003 |File di supporto toodownload non riuscita |URL non valido nel file manifesto. |
| 2004 |Protocollo non supportato |Il protocollo dell'URL multimediale non è supportato. |
| 2005 |Tipo di file non supportato |Il tipo di file multimediale di input non è supportato. |
| 2006 |Troppi file di input |Sono presenti più di 10 file nel manifesto di input hello. |
| 3000 |File di supporto toodecode non riuscita |Codec multimediale non supportato  <br/>oppure<br/> File multimediale danneggiato <br/>oppure<br/> Nessun flusso audio nei file multimediali di input. |
| 4000 |Indicizzazione batch parzialmente completata |Alcuni file multimediali di input hello sono file non è stato possibile toobe indicizzato. Per altre informazioni, vedere <a href="#output_files">File di output</a>. |
| Altro |Errori interni |Contattare il team di supporto. indexer@microsoft.com |

## <a id="supported_languages"></a>Lingue supportate
Attualmente, sono supportate le lingue inglese e spagnolo hello. Per ulteriori informazioni, vedere [hello post di blog versione v 1.2](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Collegamenti correlati
[Panoramica di Analisi servizi multimediali di Azure](media-services-analytics-overview.md)

[Uso dei file AIB con Azure Media Indexer e SQL Server](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Indicizzazione dei file multimediali con Azure Media Indexer 2 Preview](media-services-process-content-with-indexer2.md)

