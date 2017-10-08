---
title: "processo - v1 di importazione aaaPreparing unità disco rigido per un'importazione/esportazione di Azure | Documenti Microsoft"
description: "Informazioni su come tooprepare unità disco rigido utilizzando hello WAImportExport v1 strumento toocreate un processo di importazione per il servizio di importazione/esportazione di Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 3d818245-8b1b-4435-a41f-8e5ec1f194b2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 1eb0c3c51e984e2869b5268254f468d4b43e9d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-hard-drives-for-an-import-job"></a>Preparazione dei dischi rigidi per un processo di importazione
tooprepare uno o più dischi rigidi per un processo di importazione, seguire questi passaggi:

-   Identificare tooimport dati hello in hello servizio Blob

-   Identificare le directory virtuali di destinazione e i BLOB nel servizio Blob hello

-   determinare il numero di unità necessarie

-   Copiare hello dati tooeach le unità disco rigido

 Per un flusso di lavoro di esempio, vedere [tooPrepare del flusso di lavoro di esempio unità disco rigido per un processo di importazione](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md).

## <a name="identify-hello-data-toobe-imported"></a>Identificare hello toobe di dati importati
 è toodetermine quali directory Hello primo passaggio toocreating un processo di importazione e file si stanno tooimport. Può trattarsi di un elenco di directory, di un elenco di file univoci o di una combinazione di entrambi gli elementi. Quando viene inclusa una directory, tutti i file nella directory hello e nelle relative sottodirectory faranno parte del processo di importazione hello.

> [!NOTE]
>  Poiché le sottodirectory sono incluse in modo ricorsivo quando è inclusa in una directory padre, specificare solo directory padre di hello. Non è necessario specificare anche le relative sottodirectory.
>
>  Attualmente, hello dello strumento di importazione/esportazione di Microsoft Azure ha hello seguente limitazione: se una directory contiene più dati di un disco rigido può contenere, directory hello deve quindi toobe suddivisa in directory di dimensioni minori. Ad esempio, se una directory contiene 2,5 TB di dati e hello capacità del disco rigido è pari a 2TB, quindi è necessario directory da 2,5 TB di toobreak hello in directory più piccole. Questa limitazione verrà risolta in una versione successiva dello strumento hello.

## <a name="identify-hello-destination-locations-in-hello-blob-service"></a>Identificare le posizioni di destinazione hello nel servizio blob hello
 Per ogni directory o file che verrà importati, è necessario tooidentify una directory virtuale di destinazione o blob nel servizio Blob di Azure hello. Si utilizzerà queste destinazioni come input toohello strumento di importazione/esportazione di Azure. Si noti che le directory devono essere delimitate con il carattere di barra rovesciata hello "/".

 Hello nella tabella seguente vengono illustrati alcuni esempi di destinazioni blob:

|File o directory di origine|BLOB o directory virtuale di destinazione|
|------------------------------|-------------------------------------------|
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|
|K:\Temp\FavoriteVideo.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO|
|\\\myshare\john\music|https://mystorageaccount.blob.core.windows.net/music|

## <a name="determine-how-many-drives-are-needed"></a>Determinare il numero di unità necessarie
 Successivamente, è necessario toodetermine:

-   numero di Hello di dischi rigidi necessari dati hello toostore.

-   Directory Hello e/o i file autonomi che saranno copiato tooeach del disco rigido.

 Assicurarsi di avere hello numero di dischi rigidi che sono necessari dati hello toostore da trasferire.

## <a name="copy-data-tooyour-hard-drive"></a>Copiare l'unità disco rigido di dati tooyour
 In questa sezione viene descritto come toocall hello toocopy strumento di importazione/esportazione di Azure tooone i dati o più dischi rigidi. Ogni volta che si chiama hello strumento di importazione/esportazione di Azure, si crea un nuovo *copiare sessione*. Creare almeno una sessione di copia per ogni unità toowhich si copiano dati; In alcuni casi, potrebbe essere necessario più di una copia della sessione toocopy tutte le unità toosingle di dati. Ecco alcuni motivi per cui potrebbero essere necessarie più sessioni di copia:

-   È necessario creare una sessione di copia separata per ogni unità su cui si copia.

-   Una sessione di copia è possibile copiare una singola directory o un'unità toohello singolo blob. Se si copia una combinazione di entrambi, più BLOB o più directory, è necessario toocreate più sessioni di copia.

-   È possibile specificare le proprietà e i metadati che verranno impostati nei blob hello importati come parte di un processo di importazione. proprietà Hello o i metadati specificati per una sessione di copia verranno applicati BLOB tooall specificati in tale sessione. Se si desidera toospecify proprietà o metadati diversi per alcuni BLOB, è necessario toocreate sessione di copia un oggetto separato. Vedere [impostazione delle proprietà e metadati durante il processo di importazione hello](storage-import-export-tool-setting-properties-metadata-import-v1.md)per ulteriori informazioni.

> [!NOTE]
>  Se si dispone di più computer che soddisfino i requisiti di hello descritti [impostazione hello strumento di importazione/esportazione di Azure](storage-import-export-tool-setup-v1.md), è possibile copiare i dischi rigidi toomultiple di dati in parallelo tramite l'esecuzione di un'istanza di questo strumento in ogni computer.

 Per ogni disco rigido preparato con lo strumento di importazione/esportazione di Azure hello, hello creerà un singolo file journal. Sono necessari file journal hello da tutto il processo di importazione hello toocreate unità. file journal Hello può essere utilizzato tooresume preparazione dell'unità se lo strumento hello viene interrotta.

### <a name="azure-importexport-tool-syntax-for-an-import-job"></a>Sintassi dello strumento Importazione/Esportazione di Azure per il processo di importazione
 unità tooprepare per un processo di importazione, chiamare hello strumento di importazione/esportazione di Azure con hello **PrepImport** comando. I parametri da includere varia a seconda se questo è hello prima sessione di copia o di una sessione di copia successive.

 prima sessione di copia per un'unità Hello richiede alcuni parametri aggiuntivi toospecify hello chiave account di archiviazione; lettera di unità di destinazione Hello. Se è necessario formattare l'unità di hello; Se l'unità di hello devono essere crittografati e in tal caso, hello chiave BitLocker. e la directory di log hello. Ecco sintassi hello per un toocopy di sessione di copia iniziale, una directory o un singolo file:

 **Copiare prima sessione toocopy una singola directory**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Copiare prima sessione toocopy un singolo file**

 `WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 Nelle sessioni di copia successive, non è necessario toospecify parametri iniziali di hello. Ecco un toocopy di sessione di copia successive sintassi hello una directory o un singolo file:

 **Le sessioni di copia successive toocopy una singola directory**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

 **Le sessioni di copia successive toocopy un singolo file**

 `WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /srcfile:<SourceFile> /dstblob:<DestinationBlobPath> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]`

### <a name="parameters-for-hello-first-copy-session-for-a-hard-drive"></a>Parametri per hello copiare prima sessione per un'unità disco rigida
 A ogni esecuzione dei file hello dello strumento di importazione/esportazione di Azure toocopy toohello disco rigido, lo strumento hello crea una sessione di copia. Ogni sessione viene copiata una singola directory o un singolo file tooa disco rigido. stato di Hello della sessione di copia hello viene scritto il file di registro toohello. Se una sessione di copia viene interrotta (ad esempio, a causa di interruzione dell'alimentazione del sistema tooa), può essere ripreso eseguire di nuovo lo strumento hello e specificando il file journal hello nella riga di comando hello.

> [!WARNING]
>  Se si specifica hello **formato** parametro per hello prima sessione di copia, hello unità verrà formattata e tutti i dati nell'unità hello verranno cancellati. È consigliabile usare unità vuote solo per la sessione di copia.

 comando Hello utilizzata per hello prima sessione di copia per ogni unità richiede parametri diversi comandi hello per le sessioni di copia successive. Hello nella tabella seguente elenca i parametri aggiuntivi hello che sono disponibili per hello prima sessione di copia:

|Parametro della riga di comando|Descrizione|
|-----------------------------|-----------------|
|**/sk:**&lt;ChiaveAccountArchiviazione\>|`Optional.`chiave dell'account di archiviazione per i dati hello hello storage account toowhich Hello verrà importati. È necessario includere **/sk:**< StorageAccountKey\> o **/csas:**< ContainerSas\> nel comando hello.|
|**/csas:**&lt;ContainerSas\>|`Optional`. contenitore Hello account di archiviazione toohello dati tooimport toouse SAS. È necessario includere **/sk:**< StorageAccountKey\> o **/csas:**< ContainerSas\> nel comando hello.<br /><br /> il valore di Hello per questo parametro deve iniziare con il nome di contenitore hello, seguito da un punto interrogativo (?) e un token SAS hello. ad esempio:<br /><br /> `mycontainer?sv=2014-02-14&sr=c&si=abcde&sig=LiqEmV%2Fs1LF4loC%2FJs9ZM91%2FkqfqHKhnz0JM6bqIqN0%3D&se=2014-11-20T23%3A54%3A14Z&sp=rwdl`<br /><br /> le autorizzazioni di Hello, se specificato nell'URL hello o in un criterio di accesso archiviati, devono includere lettura, scrittura ed eliminazione per i processi di importazione e lettura, scrittura ed elenco per i processi di esportazione.<br /><br /> Quando viene specificato questo parametro, tutti i BLOB toobe, importato o esportato deve essere all'interno del contenitore di hello specificato nella firma di accesso condiviso hello.|
|**/t:**<TargetDriveLetter\>|`Required.`lettera di unità disco di destinazione hello hello copia sessione corrente, senza i due punti finali hello unità Hello.|
|**/format**|`Optional.`Specificare questo parametro quando l'unità hello deve toobe formattata; in caso contrario, ometterlo. Prima di formattare unità hello hello, verrà chiesta una conferma dalla console. toosuppress hello conferma, specificare il parametro /silentmode. hello.|
|**/silentmode**|`Optional.`Specificare questo parametro toosuppress hello di conferma per la formattazione dell'unità di hello.|
|**/encrypt**|`Optional.`Specificare questo parametro se l'unità di hello non è ancora stata crittografata con BitLocker ed esigenze toobe crittografati dallo strumento hello. Se l'unità di hello è già stato crittografato con BitLocker, omettere questo parametro e specificare hello `/bk` parametro, fornendo chiave BitLocker esistente hello.<br /><br /> Se si specifica hello `/format` parametro, quindi è necessario specificare anche hello `/encrypt` parametro.|
|**/bk:**&lt;BitLockerKey\>|`Optional.`Se `/encrypt` viene specificato, omettere questo parametro. Se `/encrypt` viene omesso, è necessario toohave già crittografato unità hello con BitLocker. Utilizzare questa chiave del parametro toospecify hello BitLocker. La crittografia di BitLocker è necessaria per tutti i dischi rigidi destinati ai processi di importazione.|
|**/logdir:**&lt;LogDirectory\>|`Optional.`directory log Hello specifica che una directory toobe utilizzato log dettagliati toostore, nonché i file manifesti temporanei. Se non specificato, la directory corrente hello da utilizzare come directory dei log hello.|

### <a name="parameters-required-for-all-copy-sessions"></a>Parametri necessari per tutte le sessioni di copia
 file journal Hello contiene lo stato di hello per tutte le sessioni di copia per un disco rigido. Sono inoltre contenute informazioni di hello necessari toocreate hello importare il processo. È sempre necessario specificare un file journal quando è in esecuzione hello strumento di importazione/esportazione di Azure, nonché un ID di sessione di copia:

|||
|-|-|
|Parametro della riga di comando|Descrizione|
|**/j:**&lt;JournalFile\>|`Required.`file journal di Hello percorso toohello. Ogni unità deve contenere esattamente un file journal. Si noti che file journal hello non deve trovarsi nell'unità di destinazione hello. estensione del file journal Hello è `.jrn`.|
|**/id:**&lt;SessionId\>|`Required.`ID di sessione Hello identifica una sessione di copia. È utilizzato tooensure accurata del recupero di una sessione di copia interrotta. I file vengono copiati in una sessione di copia vengono archiviati in una directory denominata hello ID di sessione nell'unità di destinazione hello dopo.|

### <a name="parameters-for-copying-a-single-directory"></a>Parametri per copiare una singola directory
 Quando si copia una singola directory, si applicano seguente hello necessarie e i parametri facoltativi:

|Parametro della riga di comando|Descrizione|
|----------------------------|-----------------|
|**/srcdir:**<SourceDirectory\>|`Required.`directory di origine Hello che contiene i file toobe copiati toohello unità di destinazione. percorso della directory Hello deve essere un percorso assoluto (non un percorso relativo).|
|**/dstdir:**<DestinationBlobVirtualDirectory\>|`Required.`Hello percorso toohello directory virtuale di destinazione nell'account di archiviazione Windows Azure. la directory virtuale Hello può o non esiste già.<br /><br /> È possibile specificare un contenitore o un prefisso di BLOB come `music/70s/`. Hello directory di destinazione deve iniziare con il nome di contenitore hello, seguito da una barra rovesciata "/" e può includere una directory di blob virtuale che termina con "/".<br /><br /> Quando il contenitore di destinazione di hello è contenitore radice hello, è necessario specificare in modo esplicito contenitore radice hello, inclusa la barra hello, come `$root/`. Poiché i BLOB nel contenitore radice hello non può includere "/" nei relativi nomi, le eventuali sottodirectory nella directory di origine hello non verrà copiata quando directory di destinazione hello contenitore radice hello.<br /><br /> Essere toouse che i nomi di contenitore valido quando si specificano BLOB o directory virtuale di destinazione. Tenere presente che i nomi di contenitore devono essere costituiti da lettere minuscole. Per le regole sulla denominazione dei contenitori, vedere [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata) (Assegnazione di nome e riferimento a contenitori, BLOB e metadati).|
|**/Disposition:**&lt;rename&amp;#124;no-overwrite&amp;#124;overwrite&gt;|`Optional.`Specifica il comportamento di hello quando un blob con hello specificato l'indirizzo esiste già. I valori validi per questo parametro sono: `rename`, `no-overwrite` e `overwrite`. Si noti che questi valori distinguono tra maiuscole e minuscole. Se viene specificato alcun valore, valore predefinito di hello è `rename`.<br /><br /> valore specificato per questo parametro influisce su tutti i file nella directory hello specificata da hello hello Hello `/srcdir` parametro.|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`Specifica il tipo di blob hello dei blob di destinazione hello. I valori validi sono: `BlockBlob` e `PageBlob`. Si noti che questi valori distinguono tra maiuscole e minuscole. Se viene specificato alcun valore, valore predefinito di hello è `BlockBlob`.<br /><br /> Nella maggior parte dei casi, è consigliato `BlockBlob`. Se si specifica `PageBlob`, hello lunghezza di ogni file nella directory hello deve essere un multiplo delle dimensioni di hello 512, di una pagina per i BLOB di pagine.|
|**/PropertyFile:**<PropertyFile\>|`Optional.`Percorso file di proprietà toohello per i BLOB di destinazione hello. Per altre informazioni, vedere [Import/Export service Metadata and Properties File Format](../storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione).|
|**/MetadataFile:**<MetadataFile\>|`Optional.`Percorso file di metadati toohello dei blob di destinazione hello. Per altre informazioni, vedere [Import/Export service Metadata and Properties File Format](../storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione).|

### <a name="parameters-for-copying-a-single-file"></a>Parametri per copiare un singolo file
 Quando la copia di un singolo file, hello parametri obbligatori e facoltativi seguenti:

|Parametro della riga di comando|Descrizione|
|----------------------------|-----------------|
|**/srcfile:**<SourceFile\>|`Required.`Hello percorso completo toohello file toobe copiato. percorso della directory Hello deve essere un percorso assoluto (non un percorso relativo).|
|**/dstblob:**<DestinationBlobPath\>|`Required.`Hello percorso toohello blob di destinazione nell'account di archiviazione Windows Azure. blob Hello può o non esiste già.<br /><br /> Specificare hello blob nome che inizia con il nome di contenitore hello. nome del blob Hello non può iniziare con "/" o nome account di archiviazione hello. Per le regole sulla denominazione dei BLOB, vedere [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata) (Assegnazione di nome e riferimento a contenitori, BLOB e metadati).<br /><br /> Quando il contenitore di destinazione di hello è contenitore radice hello, è necessario specificare in modo esplicito `$root` come hello contenitore, ad esempio `$root/sample.txt`. I BLOB nel contenitore radice hello non possono includere "/" nei nomi.|
|**/Disposition:**&lt;rename&amp;#124;no-overwrite&amp;#124;overwrite&gt;|`Optional.`Specifica il comportamento di hello quando un blob con hello specificato l'indirizzo esiste già. I valori validi per questo parametro sono: `rename`, `no-overwrite` e `overwrite`. Si noti che questi valori distinguono tra maiuscole e minuscole. Se viene specificato alcun valore, valore predefinito di hello è `rename`.|
|**/BlobType:**<BlockBlob&#124;PageBlob>|`Optional.`Specifica il tipo di blob hello dei blob di destinazione hello. I valori validi sono: `BlockBlob` e `PageBlob`. Si noti che questi valori distinguono tra maiuscole e minuscole. Se viene specificato alcun valore, valore predefinito di hello è `BlockBlob`.<br /><br /> Nella maggior parte dei casi, è consigliato `BlockBlob`. Se si specifica `PageBlob`, hello lunghezza di ogni file nella directory hello deve essere un multiplo delle dimensioni di hello 512, di una pagina per i BLOB di pagine.|
|**/PropertyFile:**<PropertyFile\>|`Optional.`Percorso file di proprietà toohello per i BLOB di destinazione hello. Per altre informazioni, vedere [Import/Export service Metadata and Properties File Format](../storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione).|
|**/MetadataFile:**<MetadataFile\>|`Optional.`Percorso file di metadati toohello dei blob di destinazione hello. Per altre informazioni, vedere [Import/Export service Metadata and Properties File Format](../storage-import-export-file-format-metadata-and-properties.md) (Formato dei file di metadati e delle proprietà del servizio Importazione/Esportazione).|

### <a name="resuming-an-interrupted-copy-session"></a>Ripresa di una sessione di copia interrotta
 Se una sessione di copia viene interrotta per qualsiasi motivo, è possibile ripristinarla eseguendo lo strumento hello con solo i file journal hello specificato:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession
```

 Solo hello ultima sessione di copia, se è stato terminato in modo anomalo, può essere ripresa.

> [!IMPORTANT]
>  Quando si riprende una sessione di copia, non modificare le directory e file di dati di origine hello aggiungendo o rimuovendo i file.

### <a name="aborting-an-interrupted-copy-session"></a>Abbandono di una sessione di copia interrotta
 Se una sessione di copia viene interrotta e non è possibile tooresume (ad esempio, se una directory di origine e inaccessibile), è necessario terminare hello sessione corrente in modo che è possibile eseguire il rollback precedente e le nuove sessioni di copia possono essere avviate:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession
```

 Hello solo ultima sessione di copia, se è stato terminato in modo anomalo, può essere interrotta. Si noti che non è possibile terminare hello prima sessione di copia per un'unità. È invece necessario riavviare la sessione di copia hello con un nuovo file journal.

## <a name="next-steps"></a>Passaggi successivi

* [Impostazione hello strumento di importazione/esportazione di Azure](storage-import-export-tool-setup-v1.md)
* [Impostazione delle proprietà e metadati hello durante il processo di importazione](storage-import-export-tool-setting-properties-metadata-import-v1.md)
* [Unità disco rigido tooprepare del flusso di lavoro di esempio per un processo di importazione](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
* [Quick reference for frequently used commands](storage-import-export-tool-quick-reference-v1.md) (Riferimento rapido per i comandi usati più di frequente) 
* [Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md) (Revisione dello stato dei processi con i file di log di copia)
* [Riparazione di un processo di importazione](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md) (Riparazione di un processo di esportazione)
* [Risoluzione dei problemi hello strumento di importazione/esportazione di Azure](storage-import-export-tool-troubleshooting-v1.md)
