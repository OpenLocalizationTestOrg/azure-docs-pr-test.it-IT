---
title: "processo di importazione aaaPreparing unità disco rigido per un'importazione/esportazione di Azure | Documenti Microsoft"
description: "Informazioni su come tooprepare unità disco rigido utilizzando hello toocreate strumento WAImportExport un processo di importazione per hello servizio importazione/esportazione di Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: 3f247a9efee29da2d18140353edc9dd7103a0761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparazione dei dischi rigidi per un processo di importazione

Hello strumento WAImportExport è hello unità strumento di preparazione e che è possibile utilizzare con hello [servizio di importazione/esportazione di Microsoft Azure](storage-import-export-service.md). È possibile utilizzare questo strumento toocopy dati toohello unità disco rigido verrà tooship tooan Data Center di Azure. Al termine di un processo di importazione, è possibile utilizzare questo toorepair strumento tutti i blob che sono stati danneggiati, mancano o in conflitto con altri BLOB. Dopo aver ricevuto hello unità da un processo di esportazione completato, è possibile utilizzare questo strumento toorepair tutti i file danneggiati o mancanti nelle unità hello. In questo articolo, passiamo rispetto all'utilizzo di questo strumento hello.

## <a name="prerequisites"></a>Prerequisiti

### <a name="requirements-for-waimportexportexe"></a>Requisiti per WAImportExport.exe

- **Configurazione del computer**
  - Windows 7, Windows Server 2008 R2 o un sistema operativo Windows più recente
  - Deve essere installato .NET Framework 4. Vedere [domande frequenti su](#faq) sulla toocheck se .net Framework è installata nel computer di hello.
- **Chiave dell'account di archiviazione** -è necessario almeno una delle chiavi dell'account hello hello account di archiviazione.

### <a name="preparing-disk-for-import-job"></a>Preparazione del disco per il processo di importazione

- **BitLocker:** BitLocker è necessario attivare lo strumento WAImportExport hello macchina in esecuzione hello. Vedere hello [domande frequenti su](#faq) come tooenable BitLocker.
- **Dischi:** accessibili dal computer in cui viene eseguito lo strumento WAImportExport. Vedere le [domande frequenti](#faq) per le specifiche del disco.
- **File di origine** -file hello Prevedi tooimport devono essere accessibili dal computer di copia hello, che si trovino in una condivisione di rete o un disco rigido locale.

### <a name="repairing-a-partially-failed-import-job"></a>Ripristino di un processo di importazione parzialmente non riuscito

- **Copiare il file di log** generato quando il servizio Importazione/Esportazione di Azure copia i dati tra l'account di archiviazione e il disco. Il file si trova nell'account di archiviazione di destinazione.

### <a name="repairing-a-partially-failed-export-job"></a>Ripristino di un processo di esportazione parzialmente non riuscito

- **Copiare il file di log** generato quando il servizio Importazione/Esportazione di Azure copia i dati tra l'account di archiviazione e il disco. Il file si trova nell'account di archiviazione di origine.
- **File manifesto**: [facoltativo] si trova nell'unità esportata restituita da Microsoft.

## <a name="download-and-install-waimportexport"></a>Scaricare e installare WAImportExport

Scaricare hello [versione più recente di WAImportExport.exe](https://www.microsoft.com/download/details.aspx?id=55280). Estrarre directory tooa contenuto compresso hello nel computer in uso.

L'attività successiva è toocreate i file CSV.

## <a name="prepare-hello-dataset-csv-file"></a>Preparare i file CSV di hello set di dati

### <a name="what-is-dataset-csv"></a>Definizione del file CSV dataset

File CSV DataSet è il valore di hello del flag /dataset è un file CSV che contiene un elenco di directory e/o di un elenco di file copiati toobe tootarget unità. è toodetermine quali directory Hello primo passaggio toocreating un processo di importazione e file si stanno tooimport. Può trattarsi di un elenco di directory, di un elenco di file univoci o di una combinazione di entrambi gli elementi. Quando viene inclusa una directory, tutti i file nella directory hello e nelle relative sottodirectory faranno parte del processo di importazione hello.

Per ogni file o directory toobe importato, è necessario identificare una directory virtuale di destinazione o di un blob nel servizio Blob di Azure hello. Si utilizzerà queste destinazioni come strumento di WAImportExport toohello di input. Directory devono essere delimitate con il carattere di barra rovesciata hello "/".

Hello nella tabella seguente vengono illustrati alcuni esempi di destinazioni blob:

| File o directory di origine | BLOB o directory virtuale di destinazione |
| --- | --- |
| H:\Video | https://mystorageaccount.blob.core.windows.net/video |
| H:\Photo | https://mystorageaccount.blob.core.windows.net/photo |
| K:\Temp\FavoriteVideo.ISO | https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO |
| \\myshare\john\music | https://mystorageaccount.blob.core.windows.net/music |

### <a name="sample-datasetcsv"></a>Esempio di dataset.csv

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
"F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
"F:\50M_original\","containername/",BlockBlob,rename,"None",None
```

### <a name="dataset-csv-file-fields"></a>Campi del file CSV dataset

| Campo | Descrizione |
| --- | --- |
| BasePath | **[Obbligatorio]**<br/>il valore di Hello di questo parametro rappresenta l'origine hello hello toobe di dati importati in cui si trova. strumento Hello verrà copia in modo ricorsivo tutti i dati che si trovano in questo percorso.<br><br/>**Valori consentiti**: questo è toobe un percorso valido nel computer locale o un percorso di condivisione valido e deve essere accessibile dall'utente hello. percorso della directory Hello deve essere un percorso assoluto (non un percorso relativo). Se il percorso di hello termina con "\\", che rappresenta una directory else un percorso che terminano senza"\\" rappresenta un file.<br/>In questo campo non sono consentiti regex. Se hello percorso contiene spazi, inserirlo in "".<br><br/>**Esempio**: "c:\Directory\c\Directory\File.txt"<br>"\\\\FBaseFilesharePath.domain.net\nomecondivisione\directory\"  |
| DstBlobPathOrPrefix | **[Obbligatorio]**<br/> Hello percorso toohello directory virtuale di destinazione nell'account di archiviazione Windows Azure. la directory virtuale Hello può o non esiste già. Se non esiste, il servizio Importazione/Esportazione ne crea una.<br/><br/>Essere toouse che i nomi di contenitore valido quando si specificano BLOB o directory virtuale di destinazione. Tenere presente che i nomi di contenitore devono essere costituiti da lettere minuscole. Per le regole sulla denominazione dei contenitori, vedere [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata) (Assegnazione di nome e riferimento a contenitori, BLOB e metadati). Se viene specificata radice, solo la struttura di directory hello dell'origine hello viene replicata nel contenitore blob di destinazione hello. Se si desidera una struttura di directory diversi rispetto a hello uno nell'origine, più righe di mapping nel file CSV<br/><br/>È possibile specificare un contenitore o un prefisso di BLOB come music/70s/. Hello directory di destinazione deve iniziare con il nome di contenitore hello, seguito da una barra rovesciata "/" e può includere una directory di blob virtuale che termina con "/".<br/><br/>Quando il contenitore di destinazione di hello è contenitore radice hello, è necessario specificare in modo esplicito il contenitore di radice hello, inclusa la barra hello, come $root /. Poiché i BLOB nel contenitore radice hello non può includere "/" nei relativi nomi, le eventuali sottodirectory nella directory di origine hello non verrà copiata quando directory di destinazione hello contenitore radice hello.<br/><br/>**Esempio**<br/>Se il percorso blob di destinazione hello è https://mystorageaccount.blob.core.windows.net/video, il valore di hello di questo campo può essere video /  |
| BlobType | **[Facoltativo]**  block &amp;#124; page<br/>Attualmente il servizio Importazione/Esportazione supporta 2 tipi di BLOB. di pagine e in blocchi. Per impostazione predefinita, tutti i file vengono importati come BLOB in blocchi. E \*con estensione vhd e \*vhdx verranno importati come Page BlobsThere è un limite per hello-blob in blocchi e blob di pagine dimensioni consentite. Per altre informazioni, vedere [Obiettivi di scalabilità per BLOB, code, tabelle e file](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).  |
| Disposition | **[Facoltativo]** rename &#124; no-overwrite &#124; overwrite <br/> Questo campo specifica il meccanismo di copia hello durante l'importazione ovvero Quando i dati vengono caricati toohello account di archiviazione dal disco hello. Le opzioni disponibili sono: ridenominazione &#124; sovrascriverla &#124; no-overwrite. Impostazioni predefinite troppo "rename" Se non specificato. <br/><br/>**Rename**: se è presente un oggetto con lo stesso nome, viene creata una copia nella destinazione.<br/>Sovrascrittura: sovrascrive file hello con file più recente. file Hello con wins ultima modifica.<br/>**No-overwrite**: scrittura hello Ignora file se è già presente.|
| MetadataFile | **[Facoltativo]** <br/>Hello valore toothis campo è di tipo file di metadati hello che può essere fornito se hello uno deve toopreserve hello metadati degli oggetti hello o fornisce metadati personalizzati. Percorso file di metadati toohello dei blob di destinazione hello. Per altre informazioni, vedere [Import/Export service Metadata and Properties File Format](storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione) |
| PropertiesFile | **[Facoltativo]** <br/>Percorso file di proprietà toohello per i BLOB di destinazione hello. Per altre informazioni, vedere [Import/Export service Metadata and Properties File Format](storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione). |

## <a name="prepare-initialdriveset-or-additionaldriveset-csv-file"></a>Preparare il file CSV InitialDriveSet o AdditionalDriveSet

### <a name="what-is-driveset-csv"></a>Definizione del file CSV driveset

Hello valore del flag di /InitialDriveSet o /AdditionalDriveSet hello è un file CSV che contiene l'elenco hello di dischi lettere di unità hello toowhich vengono mappate in modo che hello strumento possibile correttamente hello un elenco di selezione dei dischi toobe preparato. Se la dimensione dei dati hello è maggiore di dimensioni di un singolo disco, lo strumento WAImportExport hello distribuirà dati hello tra più dischi elencati in questo file CSV in modo ottimizzato.

Vi è alcun limite per il numero di hello dei dati di hello dischi non può essere scritti tooin una singola sessione. strumento Hello distribuisce i dati in base alle dimensioni del disco e le dimensioni della cartella. Selezionerà disco hello più hello oggetto-dimensioni ottimizzate. Hello dati si caricano toohello account di archiviazione sarà convergente toohello back-struttura di directory che è stato specificato nel file di set di dati. In ordine toocreate un driveset CSV, procedura hello riportata di seguito.

### <a name="create-basic-volume-and-assign-drive-letter"></a>Creare un volume di base e assegnare una lettera di unità

In ordine toocreate un volume di base e assegnare una lettera di unità, seguendo le istruzioni di hello per "Più semplice la creazione della partizione" assegnato al [Panoramica di Gestione disco](https://technet.microsoft.com/library/cc754936.aspx).

### <a name="sample-initialdriveset-and-additionaldriveset-csv-file"></a>File CSV InitialDriveSet e AdditionalDriveSet di esempio

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631
H,Format,SilentMode,Encrypt,
```

### <a name="driveset-csv-file-fields"></a>Campi del file CSV driveset

| Fields | Valore |
| --- | --- |
| DriveLetter | **[Obbligatorio]**<br/> Ogni unità che viene fornito lo strumento toohello come destinazione hello deve disporre di un volume NTFS semplice su di esso e una lettera di unità assegnata tooit.<br/> <br/>**Esempio**: R o r |
| FormatOption | **[Obbligatorio]** Format &amp;#124; AlreadyFormatted<br/><br/> **Formato**: specificare questo formatterà tutti i dati su disco hello hello. <br/>**AlreadyFormatted**: strumento di hello ignorerà la formattazione quando il valore specificato. |
| SilentOrPromptOnFormat | **[Obbligatorio]** SilentMode &#124; PromptOnFormat<br/><br/>**SilentMode**: specificare questo valore verrà abilitata strumento hello toorun di utente in modalità invisibile all'utente. <br/>**PromptOnFormat**: strumento di hello richiederà hello utente tooconfirm se azione hello effettivamente è destinato a tutti i formati.<br/><br/>Se il valore non è impostato, il comando viene interrotto e viene visualizzato il messaggio di errore "Incorrect value for SilentOrPromptOnFormat: none" (Valore non corretto per SilentOrPromptOnFormat: none) |
| Crittografia | **[Obbligatorio]** Encrypt &#124; AlreadyEncrypted<br/> valore di Hello di questo campo decide quali tooencrypt disco e che non a. <br/><br/>**Crittografare**: strumento formatterà unità hello. Se il valore del campo "FormatOption" è "Format" questo valore è obbligatorio toobe "Encrypt". Se in questo caso viene specificato"AlreadyEncrypted", viene restituito l'errore seguente: "When Format is specified, Encrypt must also be specified" (Quando viene specificato Format, è necessario specificare anche Encrypt).<br/>**AlreadyEncrypted**: strumento per decrittografare l'unità hello utilizzando BitLockerKey fornito nel campo "ExistingBitLockerKey" hello. Se il valore del campo "FormatOption" è "AlreadyFormatted", il valore di questo campo può essere "Encrypt" o "AlreadyEncrypted". |
| ExistingBitLockerKey | **[Obbligatorio]** Se il valore del campo "Encryption" è "AlreadyEncrypted",<br/> il valore di Hello di questo campo è di tipo chiave BitLocker hello associato al disco particolare hello. <br/><br/>Questo campo deve essere lasciato vuoto se il valore di hello del campo "Crittografia" è "Encrypt".  Se in questo caso è specificata una chiave BitLocker, viene restituito l'errore seguente: "Bitlocker Key should not be specified" (Non specificare la chiave BitLocker).<br/>  **Esempio**: 060456-014509-132033-080300-252615-584177-672089-411631|

##  <a name="preparing-disk-for-import-job"></a>Preparazione del disco per il processo di importazione

unità tooprepare per un processo di importazione, chiamare lo strumento WAImportExport hello con hello **PrepImport** comando. I parametri da includere varia a seconda se questo è hello prima sessione di copia o di una sessione di copia successive.

### <a name="first-session"></a>Prima sessione

Prima sessione di copia tooCopy uno strumento di WAImportExport disco (a seconda di quello specificato nel file CSV) singolo o multiplo tooa Single/Multiple Directory comando PrepImport per hello innanzitutto copiare le directory di sessione toocopy e/o file con una nuova sessione di copia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Esempio:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:\*\*\*\*\*\*\*\*\*\*\*\*\* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

### <a name="add-data-in-subsequent-session"></a>Aggiungere dati in una sessione successiva

Nelle sessioni di copia successive, non è necessario toospecify parametri iniziali di hello. È necessario toouse hello stesso file di registro affinché hello strumento tooremember punto in cui era in hello sessione precedente. stato di Hello della sessione di copia hello viene scritto il file di registro toohello. Di seguito è hello sintassi per una copia successive directory di sessione toocopy aggiuntive e o file:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<DifferentSessionId>  [DataSet:<differentdataset.csv>]
```

**Esempio:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

### <a name="add-drives-toolatest-session"></a>Aggiungere unità toolatest sessione

Se non è contenuto nell'unità specificate in InitialDriveset dati hello, possono essere utilizzati sessione di copia toosame hello strumento tooadd unità aggiuntive. 

>[!NOTE] 
>id di sessione Hello deve corrispondere l'id di sessione precedente hello. File journal deve corrispondere hello quella specificata nella sessione precedente.
>
```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AdditionalDriveSet:<newdriveset.csv>
```

**Esempio:**

```
WAImportExport.exe PrepImport /j:SameJournalTest.jrn /id:session#2  /AdditionalDriveSet:driveset-2.csv
```

### <a name="abort-hello-latest-session"></a>Interrompere hello sessione più recente:

Se una sessione di copia viene interrotta e non è possibile tooresume (ad esempio, se una directory di origine e inaccessibile), è necessario terminare hello sessione corrente in modo che è possibile eseguire il rollback precedente e le nuove sessioni di copia possono essere avviate:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /AbortSession
```

**Esempio:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /AbortSession
```

Hello solo ultima sessione di copia, se è stato terminato in modo anomalo, può essere interrotta. Si noti che non è possibile terminare hello prima sessione di copia per un'unità. È invece necessario riavviare la sessione di copia hello con un nuovo file journal.

### <a name="resume-a-latest-interrupted-session"></a>Riprendere l'ultima sessione interrotta

Se una sessione di copia viene interrotta per qualsiasi motivo, è possibile ripristinarla eseguendo lo strumento hello con solo i file journal hello specificato:

```
WAImportExport.exe PrepImport /j:<SameJournalFile> /id:<SameSessionId> /ResumeSession
```

**Esempio:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /ResumeSession
```

> [!IMPORTANT] 
> Quando si riprende una sessione di copia, non modificare le directory e file di dati di origine hello aggiungendo o rimuovendo i file.

## <a name="waimportexport-parameters"></a>Parametri di WAImportExport

| Parametri | Descrizione |
| --- | --- |
|     /j:&lt;FileJournal&gt;  | **Obbligatorio**<br/> Percorso file journal di toohello. Un file journal tiene traccia di un set di unità e record hello lo stato di avanzamento preparazione queste unità. file journal Hello deve sempre essere specificato.  |
|     /logdir:&lt;DirectoryLog&gt;  | **Facoltativo**. directory dei log Hello.<br/> File di log dettagliati, nonché alcuni file temporanei saranno scritti toothis directory. Se non specificato directory corrente verrà utilizzato come directory dei log hello. Hello directory log può essere specificata solo una volta per hello stesso file journal.  |
|     /id:&lt;IdSessione&gt;  | **Obbligatorio**<br/> Hello Id di sessione utilizzato tooidentify una sessione di copia. È utilizzato tooensure accurata del recupero di una sessione di copia interrotta.  |
|     /ResumeSession  | Facoltativo. Se hello ultima sessione di copia è stata terminata in modo anomalo, questo parametro può essere specificato tooresume hello sessione.   |
|     /AbortSession  | Facoltativo. Se hello ultima sessione di copia è stata terminata in modo anomalo, questo parametro può essere specificato tooabort hello sessione.  |
|     /sn:&lt;NomeAccountArchiviazione&gt;  | **Obbligatorio**<br/> Applicabile solo per RepairImport e RepairExport. nome Hello hello dell'account di archiviazione.  |
|     /sk:&lt;ChiaveAccountArchiviazione&gt;  | **Obbligatorio**<br/> chiave di Hello hello dell'account di archiviazione. |
|     /InitialDriveSet:&lt;driveset.csv&gt;  | **Richiesto** quando si esegue hello prima sessione di copia<br/> Un file CSV che contiene un elenco di unità tooprepare.  |
|     /AdditionalDriveSet:&lt;driveset.csv&gt; | **Obbligatoria**. Quando si aggiungono unità toocurrent sessione di copia. <br/> Un file CSV che contiene un elenco di unità aggiuntive toobe aggiunto.  |
|      /r:&lt;FileRipristino&gt; | **Obbligatorio** Applicabile solo per RepairImport e RepairExport.<br/> Percorso file toohello per tenere traccia dello stato di ripristino. Ogni unità deve contenere un solo file di ripristino.  |
|     /d:&lt;DirectoryDestinazione&gt; | **Obbligatoria**. Applicabile solo per RepairImport e RepairExport. Per RepairImport, uno o più toorepair directory delimitato da punto e virgola; Per RepairExport, toorepair una directory, ad esempio, la directory radice dell'unità di hello.  |
|     /CopyLogFile:&lt;FileLogCopiaUnità&gt; | **Obbligatorio** Applicabile solo per RepairImport e RepairExport. File di log Copia percorso toohello unità (dettagliato o errore).  |
|     /ManifestFile:&lt;FileManifestoUnità&gt; | **Obbligatorio** Applicabile solo per RepairImport e RepairExport.<br/> File manifesto dell'unità toohello percorso.  |
|     /PathMapFile:&lt;FileMappingPercorsoUnità&gt; | **Facoltativo**. Applicabile solo per RepairImport.<br/> Percorso file toohello contenente i mapping di toolocations file percorsi toohello relativo unità radice del file effettivi (delimitato da tabulazione). Quando questo parametro viene specificato per la prima volta, viene popolato con percorsi di file con destinazioni vuote, perché si tratta di file non trovati in TargetDirectories, con accesso negato, con nome non valido o esistenti in più directory. file di mapping di percorso Hello può essere modificate manualmente tooinclude i percorsi di destinazione corretto hello e specifica nuovamente per i percorsi dei file hello hello strumento tooresolve correttamente.  |
|     /ExportBlobListFile:&lt;FileElencoBlobEsportazione&gt; | **Obbligatoria**. Applicabile solo per PreviewExport.<br/> Toohello percorso XML del file contenente l'elenco dei percorsi blob o prefissi di percorso per toobe BLOB hello esportata blob. formato del file Hello è hello stesso formato hello blob elenco blob in hello operazione Put Job del servizio di importazione/esportazione hello API REST.  |
|     /DriveSize:&lt;DimensioneUnità&gt; | **Obbligatoria**. Applicabile solo per PreviewExport.<br/>  Dimensione dell'unità toobe usato per l'esportazione. Ad esempio: 500 GB, 1,5 TB. Nota: 1 GB = 1.000.000.000 di byte, 1 TB = 1.000.000.000.000 di byte  |
|     /DataSet:&lt;dataset.csv&gt; | **Obbligatorio**<br/> Un file CSV che contiene un elenco di directory e/o di un elenco di file toobe copiati tootarget unità.  |
|     /silentmode  | **Facoltativo**.<br/> Se non è specificato verrà visualizzato un promemoria si hello requisito delle unità ed è necessario toocontinue la conferma.  |

## <a name="tool-output"></a>Output dello strumento

### <a name="sample-drive-manifest-file"></a>Esempio di file manifesto dell'unità

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DriveManifest Version="2011-MM-DD">
   <Drive>
      <DriveId>drive-id</DriveId>
      <StorageAccountKey>storage-account-key</StorageAccountKey>
      <ClientCreator>client-creator</ClientCreator>
      <!-- First Blob List -->
      <BlobList Id="session#1-0">
         <!-- Global properties and metadata that applies tooall blobs -->
         <MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>
         <PropertiesPath Hash="md5-hash">global-properties-file-path</PropertiesPath>
         <!-- First Blob -->
         <Blob>
            <BlobPath>blob-path-relative-to-account</BlobPath>
            <FilePath>file-path-relative-to-transfer-disk</FilePath>
            <ClientData>client-data</ClientData>
            <Length>content-length</Length>
            <ImportDisposition>import-disposition</ImportDisposition>
            <!-- page-range-list-or-block-list -->
            <!-- page-range-list -->
            <PageRangeList>
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
               <PageRange Offset="1073741824" Length="512" Hash="md5-hash" />
            </PageRangeList>
            <!-- block-list -->
            <BlockList>
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
               <Block Offset="1073741824" Length="4194304" Id="block-id" Hash="md5-hash" />
            </BlockList>
            <MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>
            <PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>
         </Blob>
      </BlobList>
   </Drive>
</DriveManifest>
```

### <a name="sample-journal-file-xml-for-each-drive"></a>Esempio di file journal con estensione xml per ogni unità

```xml
[BeginUpdateRecord][2016/11/01 21:22:25.379][Type:ActivityRecord]
ActivityId: DriveInfo
DriveState: [BeginValue]
<?xml version="1.0" encoding="UTF-8"?>
<Drive>
   <DriveId>drive-id</DriveId>
   <BitLockerKey>*******</BitLockerKey>
   <ManifestFile>\DriveManifest.xml</ManifestFile>
   <ManifestHash>D863FE44F861AE0DA4DCEAEEFFCCCE68</ManifestHash> </Drive>
[EndValue]
SaveCommandOutput: Completed
[EndUpdateRecord]
```

### <a name="sample-journal-file-jrn-for-session-that-records-hello-trail-of-sessions"></a>File journal di esempio (JRN) per sessione che registra il riepilogo di hello di sessioni

```
[BeginUpdateRecord][2016/11/02 18:24:14.735][Type:NewJournalFile]
VocabularyVersion: 2013-02-01
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.749][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
LogDirectory: F:\logs
[EndUpdateRecord]
[BeginUpdateRecord][2016/11/02 18:24:14.754][Type:ActivityRecord]
ActivityId: PrepImportDriveCommandContext
StorageAccountKey: *******
[EndUpdateRecord]
```

## <a name="faq"></a>domande frequenti

### <a name="general"></a>Generale

#### <a name="what-is-waimportexport-tool"></a>Che cos'è lo strumento WAImportExport?

lo strumento WAImportExport Hello è hello unità strumento di preparazione e che è possibile utilizzare con il servizio di importazione/esportazione di Microsoft Azure hello. È possibile utilizzare questo strumento toocopy dati toohello unità disco rigido verrà tooship tooan data center di Azure. Al termine di un processo di importazione, è possibile utilizzare questo toorepair strumento tutti i blob che sono stati danneggiati, mancano o in conflitto con altri BLOB. Dopo aver ricevuto hello unità da un processo di esportazione completato, è possibile utilizzare questo strumento toorepair tutti i file danneggiati o mancanti nelle unità hello.

#### <a name="how-does-hello-waimportexport-tool-work-on-multiple-source-dir-and-disks"></a>Funzionamento fa hello strumento WAImportExport in più directory di origine e i dischi?

Se la dimensione dei dati hello è maggiore di dimensioni del disco hello, lo strumento WAImportExport hello distribuirà dati hello nei dischi hello in modo ottimizzato. toomultiple di copiare i dati Hello dischi può essere eseguite in parallelo o in sequenza. Vi è alcun limite per il numero di hello dei dati di hello dischi non può essere scritti toosimultaneously. strumento Hello distribuisce i dati in base alle dimensioni del disco e le dimensioni della cartella. Selezionerà disco hello più hello oggetto-dimensioni ottimizzate. Hello dati si caricano toohello account di archiviazione verrà essere convergente nuovamente toohello specificato struttura di directory.

#### <a name="where-can-i-find-previous-version-of-waimportexport-tool"></a>Dove è reperibile la versione precedente dello strumento WAImportExport?

WAImportExport include tutte le funzionalità dello strumento WAImportExport V1. Strumento WAImportExport consente agli utenti toospecify più origini e le unità toomultiple scrittura. Uno è inoltre possibile gestire con facilità più percorsi di origine da cui i dati di hello devono toobe copiati in un singolo file CSV. Tuttavia, nel caso è necessario SAS supporta o desidera toocopy unica origine toosingle su disco, è possibile [scaricare lo strumento di WAImportExport V1] (http://go.microsoft.com/fwlink/? LinkID = 301900&amp;clcid = 0x409) e fare riferimento troppo[WAImportExport V1 riferimento](storage-import-export-tool-how-to-v1.md) per informazioni sull'utilizzo di WAImportExport V1.

#### <a name="what-is-a-session-id"></a>Che cos'è l'ID sessione?

Hello è prevista la sessione di copia hello (o id) toobe parametro hello stesso se finalità hello toospread hello dati tra più dischi. Gestione di hello stesso nome di sessione di copia hello consentirà di dati toocopy utente da uno o più percorsi di origine in una o più dischi/directory di destinazione. Mantenendo lo stesso id di sessione consente hello strumento toopick copia hello dei file dal punto in cui è stato hello ora dell'ultimo backup.

Tuttavia, stessa sessione di copia non può essere account di archiviazione utilizzato tooimport dati toodifferent.

Quando il nome di sessione di copia sia uguale in più esecuzioni dello strumento hello, hello del file di registro (/ logdir) e chiave dell'account di archiviazione (o sk) è inoltre previsto toobe hello stesso.

L'ID sessione può essere costituito da lettere, numeri da 0 a 9, caratteri di sottolineatura (\_), trattini (-) o hash (#) e la relativa lunghezza deve essere compresa tra 3 e 30 caratteri.

Esempio: session-1 oppure session#1 oppure session\_1

#### <a name="what-is-a-journal-file"></a>Che cos'è un file journal?

Ogni volta che si esegue WAImportExport strumento toocopy file toohello unità disco rigido, hello strumento hello crea una sessione di copia. stato di Hello della sessione di copia hello viene scritto il file di registro toohello. Se una sessione di copia viene interrotta (ad esempio, a causa di interruzione dell'alimentazione del sistema tooa), può essere ripreso eseguire di nuovo lo strumento hello e specificando il file journal hello nella riga di comando hello.

Per ogni disco rigido preparato con lo strumento di importazione/esportazione di Azure hello, hello creerà un singolo file journal con nome "&lt;IDUnità&gt;. XML" in cui l'Id dell'unità è il numero di serie hello associato unità toohello hello strumento legge da disco Hello. Sono necessari file journal hello da tutto il processo di importazione hello toocreate unità. file journal Hello può essere utilizzato tooresume preparazione dell'unità se lo strumento hello viene interrotta.

#### <a name="what-is-a-log-directory"></a>Che cos'è una directory dei log?

directory log Hello specifica che una directory toobe utilizzato log dettagliati toostore, nonché i file manifesti temporanei. Se non specificato, la directory corrente hello da utilizzare come directory dei log hello. i registri di Hello sono log dettagliati.

### <a name="prerequisites"></a>Prerequisiti

#### <a name="what-are-hello-specifications-of-my-disk"></a>Quali sono specifiche di hello del mio disco?

Uno o più SATAII 2,5 o 3,5 vuoto o III o disco SSD unità connessa toohello computer di copia.

#### <a name="how-can-i-enable-bitlocker-on-my-machine"></a>Come è possibile abilitare BitLocker nel computer?

In modo semplice toocheck è facendo clic sull'unità di sistema. Verrà visualizzate opzioni per Bitlocker se è attivata la funzionalità di hello. Se è disattivata, le opzioni non sono visibili.

![Verificare BitLocker](./media/storage-import-export-tool-preparing-hard-drives-import/BitLocker.png)

Questo è un articolo su [come tooenable BitLocker](https://technet.microsoft.com/library/cc766295.aspx)

È possibile che nel computer non sia presente un chip TPM. Se non viene visualizzato un output mediante tpm.msc, esaminare hello domande frequenti.

#### <a name="how-toodisable-trusted-platform-module-tpm-in-bitlocker"></a>Come toodisable Trusted Platform Module (TPM) di BitLocker?
> [!NOTE]
> Solo se non è disponibile alcun TPM nei server in uso, è necessario criteri TPM toodisable. Non è necessario toodisable TPM se è presente un TPM attendibile nel server dell'utente. 
> 

In ordine toodisable TPM di BitLocker, esaminate hello alla procedura seguente:<br/>
1. Avviare **Group Policy Editor** (Editor Criteri di gruppo) digitando gpedit.msc in un prompt dei comandi. Se **Editor criteri di gruppo** toobe non è disponibile, per attivare BitLocker prima. vedere la domanda precedente.
2. Aprire **Criteri del computer locale &gt; Configurazione computer &gt; Modelli amministrativi &gt; Componenti di Windows&gt; Crittografia unità BitLocker &gt; Unità del sistema operativo**.
3. Modificare il criterio **Richiedi autenticazione aggiuntiva all'avvio**.
4. Impostare i criteri di hello troppo**abilitato** e assicurarsi che **Consenti BitLocker senza un TPM compatibile** è selezionata.

####  <a name="how-toocheck-if-net-4-or-higher-version-is-installed-on-my-machine"></a>Come toocheck se .NET 4 o versione successiva è installata nel computer?

Tutte le versioni di Microsoft .NET Framework sono installate nella directory seguente: %windir%\Microsoft.NET\Framework\

Passare toohello sopra menzionate parte nel computer di destinazione in cui lo strumento hello deve toorun. Cercare il nome di cartella che inizia con "v4". Se non è presente una directory di questo tipo, .NET 4 non è installato nel computer in uso. È possibile scaricare .Net 4 nel computer dalla pagina [Microsoft .NET Framework 4 (programma di installazione Web)](https://www.microsoft.com/download/details.aspx?id=17851).

### <a name="limits"></a>Limiti

#### <a name="how-many-drives-can-i-preparesend-at-hello-same-time"></a>Il numero di unità è preparare/invio hello contemporaneamente?

È non possibile preparare alcun limite per il numero di hello di dischi che hello dello strumento. Tuttavia, lo strumento hello prevede le lettere di unità come input. Che limita la preparazione di disco simultanei too25. Un singolo processo può gestire al massimo 10 dischi alla volta. Quando si preparano i dischi da più di 10 come destinazione hello stesso account di archiviazione, i dischi hello possono essere distribuiti tra più processi.

#### <a name="can-i-target-more-than-one-storage-account"></a>È possibile impostare più account di archiviazione come destinazione?

È possibile inviare un solo account di archiviazione per ogni processo e in ogni singola sessione di copia.

### <a name="capabilities"></a>Capabilities

#### <a name="does-waimportexportexe-encrypt-my-data"></a>WAImportExport.exe esegue la crittografia dei dati?

Sì. La crittografia di BitLocker è abilitata ed è obbligatoria per questo processo.

#### <a name="what-will-be-hello-hierarchy-of-my-data-when-it-appears-in-hello-storage-account"></a>Che cosa saranno gerarchia hello i dati quando viene visualizzato nell'account di archiviazione hello?

Anche se i dati vengono distribuiti nei dischi, hello al caricamento di dati verrà eseguito la convergenza di account di archiviazione toohello toohello struttura di directory specificato nel file CSV di hello set di dati.

#### <a name="how-many-of-hello-input-disks-will-have-active-io-in-parallel-when-copy-is-in-progress"></a>Il numero di hello input dischi avrà IO active in parallelo, quando si copia è in corso?

strumento Hello distribuisce i dati in dischi di input hello in base alle dimensioni di hello hello dei file di input. Ciò premesso, il numero di hello di attivi dischi in parallelo delends completamente natura hello hello di dati di input. A seconda delle dimensioni di hello dei singoli file nel set di dati input hello, uno o più dischi potrebbero mostrare IO active in parallelo. Per informazioni più dettagliate, vedere la prossima domanda.

#### <a name="how-does-hello-tool-distribute-hello-files-across-hello-disks"></a>Come strumento hello distribuire file hello nei dischi hello?

Lo strumento WAImportExport legge e scrive i file un batch alla volta e un batch contiene al massimo 100.000 file. È pertanto possibile scrivere al massimo 100.000 file in parallelo. Vengono scritte più dischi toosimultaneously se questi 100000 file sono distribuiti toomulti unità. Tuttavia se lo strumento hello scrive toomultiple dischi contemporaneamente o un singolo disco dipende dalla dimensione cumulativa di hello del batch di hello. Ad esempio, in caso di file più piccoli, se tutti i file 10,0000 sono in grado di toofit in una singola unità, lo strumento scriverà disco tooonly uno durante l'elaborazione di hello del batch.

### <a name="waimportexport-output"></a>Output di WAImportExport

#### <a name="there-are-two-journal-files-which-one-should-i-upload-tooazure-portal"></a>Sono disponibili due file journal, quale deve caricare tooAzure portale?

**file con estensione XML** -per ciascuna unità disco rigido preparato con lo strumento WAImportExport hello, hello creerà un singolo file journal con nome `<DriveID>.xml` dove IDUnità è il numero di serie hello associato unità toohello hello strumento legge dal disco hello. Sono necessari file journal hello da tutto il processo di importazione unità toocreate hello in hello portale di Azure. Questo file journal essere preparazione dell'unità tooresume utilizzati anche se lo strumento hello viene interrotta.

**.jrn** -file journal hello con suffisso `.jrn` contiene lo stato di hello per tutte le sessioni di copia per un disco rigido. Sono inoltre contenute informazioni di hello necessari toocreate hello importare il processo. È sempre necessario specificare un file journal quando lo strumento di WAImportExport hello in esecuzione, nonché una sessione di copia ID.

## <a name="next-steps"></a>Passaggi successivi

* [Impostazione hello strumento di importazione/esportazione di Azure](storage-import-export-tool-setup.md)
* [Impostazione delle proprietà e metadati hello durante il processo di importazione](storage-import-export-tool-setting-properties-metadata-import.md)
* [Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
* [Quick reference for frequently used commands](storage-import-export-tool-quick-reference.md) (Riferimento rapido per i comandi usati più di frequente) 
* [Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)
* [Riparazione di un processo di importazione](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)
* [Risoluzione dei problemi hello strumento di importazione/esportazione di Azure](storage-import-export-tool-troubleshooting-v1.md)
