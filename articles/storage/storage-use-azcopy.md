---
title: aaaCopy o lo spostamento dati tooAzure archiviazione con AzCopy in Windows | Documenti Microsoft
description: "Utilizzare hello AzCopy Windows utilità toomove o copia dati tooor dal blob, tabelle e contenuto del file. Copiare i dati tooAzure archiviazione da file locali, o copiare dati in o tra gli account di archiviazione. Migrare facilmente l'archiviazione di tooAzure di dati."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a>Trasferimento dati con hello AzCopy in Windows
AzCopy è un'utilità della riga di comando progettata per la copia di dati tooand dall'archiviazione Blob di Microsoft Azure, File e tabella utilizzando i comandi semplici con prestazioni ottimali. È possibile copiare dati da un oggetto tooanother all'interno dell'account di archiviazione o tra gli account di archiviazione.

Esistono due versioni di AzCopy che è possibile scaricare. AzCopy in Windows viene compilato con .NET Framework e offre opzioni della riga di comando in stile Windows. [AzCopy in Linux](storage-use-azcopy-linux.md) viene compilato con .NET Framework per le piattaforme Linux e offre opzioni della riga di comando in stile POSIX. Questo articolo descrive AzCopy in Windows.

## <a name="download-and-install-azcopy"></a>Scaricare e installare AzCopy
### <a name="azcopy-on-windows"></a>AzCopy in Windows
Scaricare hello [versione più recente di AzCopy in Windows](http://aka.ms/downloadazcopy).

#### <a name="installation-on-windows"></a>Installazione in Windows
Dopo l'installazione di AzCopy in Windows tramite installazione guidata di hello, aprire una finestra di comando e passare toohello AzCopy directory di installazione nel computer in uso - dove hello `AzCopy.exe` eseguibile si trova. Se si desidera, è possibile aggiungere hello AzCopy tooyour sistema percorso di installazione. Per impostazione predefinita, AzCopy è installato troppo`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` o `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.

## <a name="writing-your-first-azcopy-command"></a>Scrittura del primo comando AzCopy 
sintassi di base per i comandi AzCopy Hello è:

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

Hello seguenti esempi illustrano una varietà di scenari per la copia di dati tooand da BLOB di Microsoft Azure, file e tabelle. Fare riferimento toohello [AzCopy parametri](#azcopy-parameters) sezione per una spiegazione dettagliata dei parametri di hello utilizzata in ogni esempio.

## <a name="blob-download"></a>BLOB: scaricare
### <a name="download-single-blob"></a>Scaricare un singolo BLOB

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

Si noti che se la cartella hello `C:\myfolder` non esiste, AzCopy la creerà e scaricare `abc.txt ` nella nuova cartella hello.

### <a name="download-single-blob-from-secondary-region"></a>Scaricare un singolo BLOB da un'area secondaria

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.

### <a name="download-all-blobs"></a>Scaricare tutti BLOB

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

Si supponga che segue hello BLOB si trovano nel contenitore specificato hello:  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

Dopo un'operazione di download hello hello directory `C:\myfolder` includerà hello i seguenti file:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

Se non si specifica l'opzione `/S`, non verrà scaricato alcun BLOB.

### <a name="download-blobs-with-specified-prefix"></a>Scaricare i BLOB con il prefisso specificato

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

Si supponga che segue hello BLOB si trovano nel contenitore specificato hello. Tutti i blob che iniziano con il prefisso hello `a` verranno scaricati:

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

Dopo un'operazione di download hello hello cartella `C:\myfolder` includerà hello i seguenti file:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

prefisso Hello applica toohello directory virtuale, che costituisce hello prima parte del nome blob hello. Nell'esempio hello illustrato in precedenza, la directory virtuale hello non corrisponde prefisso specificato hello, in modo che non è stato scaricato. Inoltre, se hello opzione `\S` non viene specificato, AzCopy non verranno scaricati tutti i BLOB.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Impostare l'ora dell'ultima modifica hello dei file esportati toobe stesso hello BLOB di origine

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

È anche possibile escludere i BLOB da un'operazione di download hello in base all'ora ultima modifica. Ad esempio, se si desidera tooexclude BLOB la cui ultima modifica è hello uguale o più file di destinazione hello recente, aggiungere hello `/XN` opzione:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

O se si desidera tooexclude BLOB la cui ultima modifica è hello stesso o meno i file di destinazione hello, aggiungere hello `/XO` opzione:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a>BLOB: caricare
### <a name="upload-single-file"></a>Caricare un singolo file

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

Se hello contenitore di destinazione specificato non esiste, AzCopy verrà creato e caricare file hello al suo interno.

### <a name="upload-single-file-toovirtual-directory"></a>Caricare file singoli toovirtual directory

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

Se hello specificato una directory virtuale non esiste, AzCopy caricherà hello file tooinclude hello directory virtuale nel nome (*ad esempio*, `vd/abc.txt` nell'esempio hello sopra).

### <a name="upload-all-files"></a>Caricare tutti i file

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

Specifica l'opzione `/S` contenuto hello caricamenti di hello specificato directory tooBlob archiviazione in modo ricorsivo, vale a dire che tutte le sottocartelle e i relativi file verranno caricati anche. Ad esempio, si supponga che segue hello file si trovano nella cartella `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Dopo un'operazione di caricamento hello contenitore hello includerà hello i seguenti file:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Se non si specifica l'opzione `/S`, AzCopy non caricherà i file in modo ricorsivo. Dopo un'operazione di caricamento hello contenitore hello includerà hello i seguenti file:

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a>Caricare i file corrispondenti ai criteri specificati

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

Si supponga che segue hello file si trovano nella cartella `C:\myfolder`:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

Dopo un'operazione di caricamento hello contenitore hello includerà hello i seguenti file:

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

Se non si specifica l'opzione `/S`, AzCopy caricherà solo i BLOB che non si trovano in una directory virtuale:

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Specificare hello tipo di contenuto MIME di un blob di destinazione
Per impostazione predefinita, AzCopy Imposta tipo di contenuto di un blob di destinazione hello troppo`application/octet-stream`. A partire dalla versione 3.1.0, è possibile specificare in modo esplicito tipo di contenuto tramite l'opzione hello hello `/SetContentType:[content-type]`. Questa sintassi Imposta tipo di contenuto hello per tutti i BLOB in un'operazione di caricamento.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

Se si specifica `/SetContentType` senza un valore, quindi AzCopy imposterà ogni blob o il tipo di contenuto del file in base a tooits estensione di file.

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a>BLOB: copiare
### <a name="copy-single-blob-within-storage-account"></a>Copiare un BLOB all'interno di un account di archiviazione

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

Quando si copia un BLOB all'interno di un account di archiviazione, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-single-blob-across-storage-accounts"></a>Copiare un singolo BLOB tra account di archiviazione

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

Quando si copia un BLOB tra account di archiviazione, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiare blob singolo dall'area tooprimary area secondaria

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

Dopo un'operazione di copia hello contenitore di destinazione hello includerà blob hello e i relativi snapshot. Se il blob di hello esempio hello precedente contiene due snapshot, il contenitore di hello includerà seguente hello blob e snapshot:

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copiare in modo sincrono i BLOB tra account di archiviazione
Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono. Pertanto, operazione di copia hello verrà eseguito in background hello usando la capacità della larghezza di banda di riserva che non dispone di alcun contratto di servizio in termini di velocità con cui verrà copiato un blob e AzCopy verificherà periodicamente lo stato di copia hello fino a quando non hello copia viene completata o non è riuscita.

Hello `/SyncCopy` opzione assicura che l'operazione di copia hello otterranno velocità coerente. AzCopy esegue copia sincrono hello scaricando BLOB hello toocopy da hello specificato memoria toolocal di origine e quindi caricarli toohello destinazione di archiviazione Blob.

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

`/SyncCopy`potrebbe generare ulteriore uscita costo copia tooasynchronous confrontati, hello approccio consigliato è toouse questa opzione in una macchina virtuale di Azure in hello stessa area del costo di uscita origine tooavoid account di archiviazione.

## <a name="file-download"></a>File: scaricare
### <a name="download-single-file"></a>Scaricare un singolo file

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

Se è specificato l'origine è una condivisione di file di Azure, quindi è necessario specificare il nome di file esatto hello, hello (*ad esempio* `abc.txt`) toodownload un singolo file, oppure specificare l'opzione `/S` toodownload tutti i file nella condivisione di hello in modo ricorsivo. Il tentativo di toospecify un modello di file e l'opzione `/S` insieme si verificherà un errore.

### <a name="download-all-files"></a>Scaricare tutti i file

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

Le cartelle vuote non verranno scaricate.

## <a name="file-upload"></a>File: caricare
### <a name="upload-single-file"></a>Caricare un singolo file

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a>Caricare tutti i file

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

Le cartelle vuote non verranno caricate.

### <a name="upload-files-matching-specified-pattern"></a>Caricare i file corrispondenti ai criteri specificati

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a>File: copia
### <a name="copy-across-file-shares"></a>Copiare tra condivisioni file

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Copiare da tooblob condivisione file

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
Quando si copia un file da tooblob di condivisione file, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.


### <a name="copy-from-blob-toofile-share"></a>Copiare da blob toofile condivisione

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
Quando si copia un file dalla condivisione toofile blob, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.

### <a name="synchronously-copy-files"></a>Copiare file in modo sincrono
È possibile specificare hello `/SyncCopy` opzione toocopy dati da archiviazione di File tooFile, archiviazione, dall'archiviazione di File tooBlob, archiviazione e dall'archiviazione Blob tooFile archiviazione in modo sincrono, AzCopy esegue questa operazione di download di memoria di toolocal hello origine dati e di caricarlo toodestination nuovamente. Verranno applicati i costi in uscita standard.

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

Durante la copia da archiviazione di File tooBlob archiviazione, è di tipo di blob predefinito hello blob in blocchi, l'utente può specificare l'opzione `/BlobType:page` toochange hello tipo di blob di destinazione.

Si noti che `/SyncCopy` potrebbe generare uscita ulteriore costi confronto tooasynchronous copia, l'approccio consigliato hello è toouse hello di questa opzione nella macchina virtuale di Azure in hello stessa area del costo di uscita origine tooavoid account di archiviazione.

## <a name="table-export"></a>Tabella: esportare
### <a name="export-table"></a>Esportare una tabella

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

AzCopy scrive una cartella di destinazione specificato toohello file manifesto. file manifesto Hello viene usato nei file di dati necessari hello hello importazione processo toolocate ed eseguire la convalida dei dati. file manifesto Hello utilizza hello convenzione di denominazione seguente per impostazione predefinita:

    <account name>_<table name>_<timestamp>.manifest

È inoltre possibile specificare opzione hello `/Manifest:<manifest file name>` tooset nome del file manifesto hello.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a>Dividere l'esportazione in più file

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

AzCopy utilizza un *l'indice di volume* in hello suddividere i dati di nomi di file toodistinguish più file. indice di volume Hello è costituito da due parti, un *indice intervalli di chiavi di partizione* e *split file indice*. Entrambi gli indici sono in base zero.

indice di intervalli di chiavi di partizione Hello sarà pari a 0 se l'utente non specifica l'opzione `/PKRS`.

Si supponga, ad esempio, AzCopy genera due file di dati dopo che l'utente hello specifica l'opzione `/SplitSize`. potrebbe essere Hello risultante i nomi di file di dati:

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

Si noti che hello valore minimo possibile per l'opzione `/SplitSize` 32 MB. Se hello specificato di destinazione è l'archiviazione Blob, AzCopy verrà dividere il file di dati hello una volta la dimensioni raggiunge hello blob dimensione massima consentita (200GB), indipendentemente dall'opzione se `/SplitSize` è stato specificato dall'utente hello.

### <a name="export-table-toojson-or-csv-data-file-format"></a>Esportare tooJSON tabella o un formato di file di dati CSV
AzCopy per impostazione predefinita consente di esportare i file di dati di tabelle tooJSON. È possibile specificare l'opzione hello `/PayloadFormat:JSON|CSV` tabelle hello tooexport come JSON o CSV.

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

Quando si specifica il formato di payload di hello CSV, AzCopy genererà inoltre un file di schema con estensione `.schema.csv` per ogni file di dati.

### <a name="export-table-entities-concurrently"></a>Esportare entità tabella simultaneamente

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

AzCopy avvierà entità tooexport operazioni simultanee all'utente di hello specifica l'opzione `/PKRS`. Ogni operazione esporta un intervallo di chiavi di partizione.

Si noti che il numero di hello di operazioni simultanee anche viene controllato dall'opzione `/NC`. AzCopy utilizza il numero di hello di processori core come valore predefinito hello `/NC` quando si copiano le entità tabella, anche se `/NC` non è stato specificato. Quando utente hello specifica l'opzione `/PKRS`, AzCopy utilizza hello minore del numero di hello due valori - partizione intervalli di chiavi e operazioni simultanee in modo implicito o esplicito specificate - toodetermine hello di toostart operazioni simultanee. Per ulteriori informazioni, digitare `AzCopy /?:NC` nella riga di comando hello.

### <a name="export-table-tooblob"></a>Esportazione tabella tooblob

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

AzCopy genererà un file di dati JSON in un contenitore blob hello con convenzione di denominazione seguente:

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

file di dati JSON Hello generato segue il formato di payload hello per metadati minimi. Per i dettagli su questo formato di payload, vedere [Formato di payload per le operazioni del servizio tabelle](http://msdn.microsoft.com/library/azure/dn535600.aspx).

Si noti che quando si esportano tabelle tooblobs, AzCopy sarà di scaricare i file di dati temporanei toolocal entità tabella hello e quindi caricare tali blob toohello entità. Questi file di dati temporanei vengono inseriti nella cartella di file hello giornale di registrazione con il percorso predefinito di hello "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", è possibile specificare l'opzione/toochange [cartella di file journal] z: hello percorso della cartella file journal e pertanto modificare percorso dei file di dati temporanei hello. dati temporanei, le dimensioni dei file viene stabilita delle entità di tabella dimensioni e hello che è specificato con /SplitSize opzione hello, anche se il file di dati temporanei hello nel disco locale verrà eliminato immediatamente dopo che è stato Hello caricate toohello blob, assicurarsi che si disporre di sufficiente toostore di spazio su disco locale questi file di dati temporanei vengono eliminati.

## <a name="table-import"></a>Tabella: importare
### <a name="import-table"></a>Importare una tabella

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

opzione Hello `/EntityOperation` indica come entità tooinsert in hello tabella. I valori possibili sono:

* `InsertOrSkip`: Ignora un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.
* `InsertOrMerge`: Unisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.
* `InsertOrReplace`: Sostituisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.

Si noti che non è possibile specificare l'opzione `/PKRS` in uno scenario di importazione hello. Diversamente dallo scenario di esportazione hello, in cui è necessario specificare l'opzione `/PKRS` toostart operazioni simultanee, AzCopy per impostazione predefinita avvia operazioni simultanee quando si importa una tabella. numero di operazioni simultanee di avvio predefinito di Hello è uguale toohello numero di processori core; Tuttavia, è possibile specificare un numero diverso di simultanee con l'opzione `/NC`. Per ulteriori informazioni, digitare `AzCopy /?:NC` nella riga di comando hello.

Si noti che AzCopy supporta solo l'importazione per JSON, non per CSV. AzCopy non supporta l'importazione di tabelle da file JSON e file manifesto creati dall'utente. Entrambi questi file devono provenire da un'esportazione di tabella di AzCopy. tooavoid errori, non modificare hello esportata JSON o un file manifesto.

### <a name="import-entities-tootable-using-blobs"></a>Importazione di entità tootable tramite i BLOB
Si supponga che un contenitore Blob contenuto seguente hello: file oggetto JSON che rappresenta una tabella di Azure e il relativo file manifesto.

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

È possibile eseguire hello seguenti entità tooimport comando in una tabella utilizzando il file manifesto di hello in tale contenitore blob:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a>Altre funzionalità di AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Copia solo i dati che non esistono nella destinazione hello
Hello `/XO` e `/XN` parametri consentono tooexclude le risorse dell'origine o meno recente viene copiato, rispettivamente. Se si desidera solo le risorse dell'origine toocopy che non sono presenti nella destinazione hello, è possibile specificare entrambi i parametri nel comando AzCopy hello:

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

Si noti che questo non è supportato quando hello origine o destinazione è una tabella.

### <a name="use-a-response-file-toospecify-command-line-parameters"></a>Utilizzare un parametri della riga di comando toospecify del file di risposta

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

È possibile includere i parametri della riga di comando di AzCopy in un file di risposta. I processi di AzCopy hello parametri nel file hello come se fossero stati specificati nella riga di comando hello, eseguire una sostituzione diretta con contenuto hello del file hello.

Si supponga che un file di risposta denominato `copyoperation.txt`, che contiene hello seguenti righe. Ogni parametro di AzCopy può essere specificato su una singola riga

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

o su righe separate:

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

AzCopy non riuscirà se il parametro hello si divide in due righe, come illustrato di seguito per hello `/sourcekey` parametro:

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a>Utilizzare più risposta file toospecify parametri della riga di comando
Si supponga che siano presenti un file di risposta denominato `source.txt` , che specifica un contenitore di origine:

    /Source:http://myaccount.blob.core.windows.net/mycontainer

E un file di risposta denominato `dest.txt` che specifica una cartella di destinazione nel file system di hello:

    /Dest:C:\myfolder

E un file di risposta denominato `options.txt` , che specifica le opzioni per AzCopy:

    /S /Y

toocall AzCopy con questi file di risposta, di cui si trovano tutti in una directory `C:\responsefiles`, utilizzare questo comando:

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

AzCopy elabora questo comando esattamente come se si è incluso tutti hello singoli parametri della riga di comando hello:

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a>Specificare una firma di accesso condiviso

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

È inoltre possibile specificare una firma di accesso condiviso nel contenitore hello URI:

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a>Cartella del file journal
Ogni volta che si esegue un comando tooAzCopy, controlla se è presente un file journal nella cartella predefinita hello o se esiste in una cartella specificata tramite questa opzione. Se non esiste alcun file journal hello in entrambe le posizioni, AzCopy considera nuova operazione hello e genera un nuovo file journal.

Se esistono file journal hello, AzCopy controllerà se riga di comando hello immesso corrisponde a riga di comando hello in file journal hello. Se due righe di comando hello corrispondono, AzCopy riprende hello incompleti. Se non corrispondono, si tooeither richiesta sovrascrittura hello journal file toostart una nuova operazione o toocancel hello operazione corrente.

Se si desidera toouse hello percorso predefinito file journal hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

Se si omette l'opzione `/Z`, oppure specificare l'opzione `/Z` senza percorso della cartella hello, come illustrato in precedenza, AzCopy crea file journal hello nel percorso predefinito di hello, ovvero `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`. Se il file journal di hello esiste già, quindi AzCopy riprende l'operazione di hello basato su file journal hello.

Se si desidera toospecify un percorso personalizzato per il file journal hello:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

Questo esempio crea file journal hello se non esiste già. Se esiste, quindi AzCopy riprende l'operazione di hello basato su file journal hello.

Se si desidera tooresume un'operazione di AzCopy:

```azcopy
AzCopy /Z:C:\journalfolder\
```

In questo esempio riprende hello ultima operazione, che potrebbe non essere stata toocomplete.

### <a name="generate-a-log-file"></a>Generare un file di log

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

Se si specifica l'opzione `/V` senza fornire un log dettagliato di percorso toohello file, quindi AzCopy crea hello file di log nel percorso predefinito di hello, ovvero `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.

In caso contrario, è possibile creare un file di log in un percorso personalizzato:

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

Si noti che se si specifica un percorso relativo seguente opzione `/V`, ad esempio `/V:test/azcopy1.log`, log dettagliato hello viene creato nella directory di lavoro corrente di hello all'interno di una sottocartella denominata `test`.

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Specificare il numero di hello di operazioni simultanee toostart
Opzione `/NC` specifica hello numero di operazioni di copia simultanea. Per impostazione predefinita, AzCopy inizia un certo numero di velocità effettiva di trasferimento dei dati di operazioni simultanee tooincrease hello. Per le operazioni di tabella, il numero di hello di operazioni simultanee è uguale toohello numero di processori che disponibili. Per operazioni di Blob e File, il numero di hello di operazioni simultanee è uguale a numero hello 8 volte di processori che disponibili. Se si esegue AzCopy attraverso una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per /NC tooavoid errore di concorrenza di risorse.

### <a name="run-azcopy-against-azure-storage-emulator"></a>Eseguire AzCopy nell'Emulatore di archiviazione di Azure
È possibile eseguire AzCopy hello [emulatore di archiviazione Azure](storage-use-emulator.md) per i BLOB:

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

e le tabelle:

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a>Parametri di AzCopy
I parametri per AzCopy sono descritti nella tabella seguente. È anche possibile digitare uno dei seguenti comandi dalla riga di comando hello per informazioni sull'utilizzo di AzCopy hello:

* Per assistenza dettagliata della riga di comando per AzCopy: `AzCopy /?`
* Per assistenza dettagliata con un parametro di AzCopy: `AzCopy /?:SourceKey`
* Per esempi della riga di comando: `AzCopy /?:Samples`

### <a name="sourcesource"></a>/Source: "source"
Specifica i dati di origine hello da cui toocopy. Hello origine può essere una directory del file system, un contenitore blob, una directory virtuale di blob, una condivisione di file di archiviazione, una directory di archiviazione di file o una tabella di Azure.

**Applicabile a:** BLOB, file, tabelle

### <a name="destdestination"></a>/Dest:"destination"
Specifica hello destinazione toocopy per. Hello destinazione può essere una directory del file system, un contenitore blob, una directory virtuale di blob, una condivisione di file di archiviazione, una directory di archiviazione di file o una tabella di Azure.

**Applicabile a:** BLOB, file, tabelle

### <a name="patternfile-pattern"></a>/Pattern:"file-pattern"
Specifica uno schema di file che indica quale toocopy file. comportamento di Hello del parametro /Pattern hello è determinato dal percorso hello hello dei dati di origine e la presenza di hello di opzione della modalità ricorsiva hello. È possibile specificare la modalità ricorsiva tramite l'opzione /S.

Se l'origine specificata hello è una directory nel file system di hello, caratteri jolly standard vengono in effetti, e quindi il modello di file hello fornito viene confrontato con i file nella directory hello. Se l'opzione che /s è specificata, quindi AzCopy corrisponde anche modello specificato di hello in tutti i file nelle sottocartelle nella directory hello.

Se l'origine specificata hello è un contenitore blob o directory virtuale, i caratteri jolly non vengono applicate. Se l'opzione che /s è specificata, quindi AzCopy interpreta il criterio di file specificato hello come prefisso blob. Se opzione che /s non viene specificato, quindi AzCopy corrisponde allo schema di file di hello e i nomi dei blob esatto.

Se hello specificato origine è una condivisione di file di Azure, è necessario specificare hello nome esatto del file, (ad esempio, ABC) toocopy un singolo file, oppure specificare opzione /S toocopy tutti i file in modo ricorsivo condivisione hello. Il tentativo toospecify un modello di file e l'opzione /S insieme genererà un errore.

AzCopy Usa la corrispondenza tra maiuscole e minuscole quando hello /Source è un contenitore blob o directory virtuale di blob e utilizza distinzione corrispondenti in tutti gli altri casi di hello.

Hello file criterio predefinito utilizzato quando non è specificato alcun modello di file è *.* per un percorso del file system o un prefisso vuoto per un percorso di Archiviazione di Azure. Non è consentito specificare più criteri file.

**Applicabile a:** BLOB, file

### <a name="destkeystorage-key"></a>/DestKey:"storage-key"
Specifica una chiave dell'account di archiviazione per la risorsa di destinazione hello hello.

**Applicabile a:** BLOB, file, tabelle

### <a name="destsassas-token"></a>/DestSAS:"sas-token"
Specifica una firma di accesso condiviso (SAS) con autorizzazioni di lettura e scrittura per la destinazione di hello (se applicabile). Consente di racchiudere hello SAS tra virgolette doppie, in quanto potrebbe contiene i caratteri speciali della riga di comando.

Se risorsa di destinazione hello è un contenitore blob, condivisione file o una tabella, è possibile specificare questa opzione, seguita dal token di firma di accesso condiviso hello oppure è possibile specificare hello firma di accesso condiviso come parte del contenitore blob di destinazione hello, condivisione file o l'URI della tabella, senza questa opzione.

Se hello origine e destinazione siano entrambi i BLOB, quindi il blob di destinazione hello deve risiedere all'interno di hello stesso account di archiviazione blob di origine hello.

**Applicabile a:** BLOB, file, tabelle

### <a name="sourcekeystorage-key"></a>/SourceKey:"storage-key"
Specifica una chiave dell'account di archiviazione per la risorsa di origine hello hello.

**Applicabile a:** BLOB, file, tabelle

### <a name="sourcesassas-token"></a>/SourceSAS:"sas-token"
Specifica una firma di accesso condiviso con le autorizzazioni di lettura ed elenco per hello origine (se applicabile). Consente di racchiudere hello SAS tra virgolette doppie, in quanto potrebbe contiene i caratteri speciali della riga di comando.

Se hello origine risorsa è un contenitore di blob e viene fornita una chiave né una firma di accesso condiviso, il contenitore di blob hello verrà letta tramite l'accesso anonimo.

Se l'origine di hello è una condivisione file o una tabella, è necessario specificare una chiave o una firma di accesso condiviso.

**Applicabile a:** BLOB, file, tabelle

### <a name="s"></a>/S
Specifica la modalità ricorsiva per le operazioni di copia. In modalità ricorsiva, AzCopy verranno copiati tutti i BLOB o i file che corrispondono a hello criterio di file specificato, inclusi quelli nelle sottocartelle.

**Applicabile a:** BLOB, file

### <a name="blobtypeblock--page--append"></a>/BlobType:"block" | "page" | "append"
Specifica se il blob di destinazione hello è un blob in blocchi, un blob di pagine o un blob di aggiunta. Questa opzione è applicabile solo per l'upload di un BLOB. In caso contrario, viene generato un errore. Se la destinazione hello è un blob e questa opzione non è specificata, per impostazione predefinita, AzCopy crea un blob in blocchi.

**Applicabile a:** BLOB

### <a name="checkmd5"></a>/CheckMD5
Calcola un hash MD5 per i dati scaricati e verifica che l'hash MD5 hello archiviati nel blob hello o hash calcolato hello corrisponde a proprietà Content-MD5 del file. controllo Hello MD5 è disattivata per impostazione predefinita, pertanto è necessario specificare questo controllo di MD5 hello tooperform opzione quando il download dei dati.

Si noti che di archiviazione di Azure non garantisce che hello hash MD5 archiviato per il blob hello o file sia aggiornato. È hello tooupdate di responsabilità del client MD5 ogni volta che viene modificato hello blob o file.

AzCopy sempre impostata hello Content-MD5 per un blob di Azure o il file dopo averlo caricato toohello servizio.  

**Applicabile a:** BLOB, file

### <a name="snapshot"></a>/Snapshot
Indica se gli snapshot tootransfer. Questa opzione è valida solo quando l'origine hello è un blob.

Hello snapshot blob trasferiti vengono rinominati in questo formato:. Extension blob-name (ora dello snapshot)

Per impostazione predefinita, gli snapshot non vengono copiati.

**Applicabile a:** BLOB

### <a name="vverbose-log-file"></a>/V:[verbose-log-file]
Esegue l'output dei messaggi di stato dettagliati in un file di log.

Per impostazione predefinita, il file di log dettagliato hello denominato AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`. Se si specifica un percorso del file esistente per questa opzione, log dettagliato hello sarà toothat aggiunto file.  

**Applicabile a:** BLOB, file, tabelle

### <a name="zjournal-file-folder"></a>/Z:[journal-file-folder]
Specifica la cartella del file journal per la ripresa di un'operazione.

AzCopy supporta sempre la ripresa di un'operazione interrotta.

Se questa opzione non è specificata o viene specificato senza un percorso di cartella, AzCopy crea nel percorso predefinito di hello, ovvero % LocalAppData%\Microsoft\Azure\AzCopy file journal hello.

Ogni volta che si esegue un comando tooAzCopy, controlla se è presente un file journal nella cartella predefinita hello o se esiste in una cartella specificata tramite questa opzione. Se non esiste alcun file journal hello in entrambe le posizioni, AzCopy considera nuova operazione hello e genera un nuovo file journal.

Se esistono file journal hello, AzCopy controllerà se riga di comando hello immesso corrisponde a riga di comando hello in file journal hello. Se due righe di comando hello corrispondono, AzCopy riprende hello incompleti. Se non corrispondono, si tooeither richiesta sovrascrittura hello journal file toostart una nuova operazione o toocancel hello operazione corrente.

file journal Hello viene eliminato dopo il completamento dell'operazione di hello.

Si noti che la ripresa di un'operazione da un file journal creato da una versione precedente di AzCopy non è supportata.

**Applicabile a:** BLOB, file, tabelle

### <a name="parameter-file"></a>/@:"parameter-file"
Specifica un file contenente parametri. I processi di AzCopy hello parametri nel file hello come se fossero stati specificati nella riga di comando hello.

In un file di risposta è possibile specificare più parametri su una sola riga o specificare un parametro su ogni riga. Si noti che un singolo parametro non può estendersi su più righe.

File di risposta possono includere righe di commenti che iniziano con il simbolo # hello.

È possibile specificare più file di risposta. Tuttavia, tenere presente che AzCopy non supporta file di risposta annidati.

**Applicabile a:** BLOB, file, tabelle

### <a name="y"></a>/Y
Elimina tutte le richieste di conferma di AzCopy.

**Applicabile a:** BLOB, file, tabelle

### <a name="l"></a>/L
Specifica solo un'operazione di elenco, non viene copiato alcun dato.

AzCopy interpreterà hello utilizzo di questa opzione come una simulazione per riga di comando hello in esecuzione senza questa opzione /L e contare il numero di oggetti verrà copiato, è possibile specificare l'opzione /V in hello stesso tempo toocheck gli oggetti che verranno copiati nel log dettagliato hello.

comportamento di Hello di questa opzione è inoltre determinato dalla posizione hello hello dei dati di origine e la presenza di hello di hello ricorsiva modalità /S e file di modello opzione /Pattern.

AzCopy richiede l'autorizzazione ELENCO e LETTURA per questo percorso di origine quando si utilizza questa opzione.

**Applicabile a:** BLOB, file

### <a name="mt"></a>/MT
Imposta l'ora dell'ultima modifica del file scaricato hello toobe hello stesso come blob di origine hello o del file.

**Applicabile a:** BLOB, file

### <a name="xn"></a>/XN
Esclude una risorsa di origine più recente. risorsa Hello non verrà copiato se l'ora dell'ultima modifica dell'origine hello hello è hello uguale o più recente di destinazione.

**Applicabile a:** BLOB, file

### <a name="xo"></a>/XO
Esclude una risorsa di origine meno recente. risorsa Hello non verrà copiato se l'ora dell'ultima modifica dell'origine hello hello è hello uguale o più vecchi di destinazione.

**Applicabile a:** BLOB, file

### <a name="a"></a>/A
Carica solo i file che è sono impostato l'attributo Archive hello.

**Applicabile a:** BLOB, file

### <a name="iarashcnetoi"></a>/IA:[RASHCNETOI]
Caricamenti solo i file che dispongono di alcuna hello specificare set di attributi.

Gli attributi disponibili sono:

* R = File di sola lettura
* A = File pronti per l'archiviazione
* S = File di sistema
* H = File nascosti
* C = File compressi
* N = File normali
* E = File crittografati
* T = File temporanei
* O = File offline
* I = File non indicizzati

**Applicabile a:** BLOB, file

### <a name="xarashcnetoi"></a>/XA:[RASHCNETOI]
Esclude i file contenenti hello specificato set di attributi.

Gli attributi disponibili sono:

* R = File di sola lettura
* A = File pronti per l'archiviazione
* S = File di sistema
* H = File nascosti
* C = File compressi
* N = File normali
* E = File crittografati
* T = File temporanei
* O = File offline
* I = File non indicizzati

**Applicabile a:** BLOB, file

### <a name="delimiterdelimiter"></a>/Delimiter:"delimiter"
Indica il carattere delimitatore di hello utilizzato toodelimit le directory virtuali in un nome di blob.

Per impostazione predefinita, viene utilizzato AzCopy / come carattere di delimitazione hello. Tuttavia, a questo scopo supporta anche l'uso di caratteri comuni, ad esempio @, # o %. Se è necessario tooinclude uno di questi caratteri speciali nella riga di comando hello, racchiudere il nome file hello tra virgolette doppie.

Questa opzione si applica solo per il download di BLOB.

**Applicabile a:** BLOB

### <a name="ncnumber-of-concurrent-operations"></a>/NC:"number-of-concurrent-operations"
Specifica il numero di hello di operazioni simultanee.

AzCopy per impostazione predefinita viene avviato un determinato numero di velocità effettiva di trasferimento dei dati di operazioni simultanee tooincrease hello. Si noti che un numero elevato di operazioni simultanee in un ambiente di larghezza di banda bassa può sovraccaricare la connessione di rete hello e impedire completamente il completamento delle operazioni hello. Limitare le operazioni simultanee in base alla larghezza di banda di rete effettivamente disponibile.

limite massimo di Hello per le operazioni simultanee è 512.

**Applicabile a:** BLOB, file, tabelle

### <a name="sourcetypeblob--table"></a>/SourceType:"Blob" | "Table"
Specifica che hello `source` risorsa è un blob disponibile nell'ambiente di sviluppo locale hello, in esecuzione nell'emulatore di archiviazione hello.

**Applicabile a:** BLOB, tabelle

### <a name="desttypeblob--table"></a>/DestType:"Blob" | "Table"
Specifica che hello `destination` risorsa è un blob disponibile nell'ambiente di sviluppo locale hello, in esecuzione nell'emulatore di archiviazione hello.

**Applicabile a:** BLOB, tabelle

### <a name="pkrskey1key2key3"></a>/PKRS:"key1#key2#key3#..."
Divisioni hello tooenable di intervalli di chiavi di partizione esportazione dei dati in parallelo, il che aumenta la velocità di hello dell'operazione di esportazione hello.

Se questa opzione non è specificata, AzCopy utilizza entità della tabella tooexport un singolo thread. Ad esempio, se hello utente specifica /PKRS: "#bb aa", quindi AzCopy avvia tre operazioni simultanee.

Ogni operazione esporta uno dei tre intervalli di chiavi di partizione, nel modo seguente:

  [first-partition-key, aa)

  [aa, bb)

  [bb, last-partition-key]

**Applicabile a:** tabelle

### <a name="splitsizefile-size"></a>/SplitSize:"file-size"
Specifica hello esportato dividere dimensioni in MB, hello di valore minimo consentito è 32.

Se questa opzione non è specificata, AzCopy esporterà toosingle file di dati di tabella.

Se i dati di tabella hello esportata tooa blob, e hello esportato il file raggiunge il limite di 200 GB hello per le dimensioni del blob, AzCopy suddividerà hello file esportato, anche se questa opzione non è specificata.

**Applicabile a:** tabelle

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a>/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"
Specifica il comportamento di importazione hello tabella dati.

* InsertOrSkip - Ignora un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.
* InsertOrMerge - unisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.
* InsertOrReplace - sostituisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.

**Applicabile a:** tabelle

### <a name="manifestmanifest-file"></a>/Manifest:"manifest-file"
Specifica il file manifesto hello per tabella hello esportazione e importazione di operazione.

Questa opzione è facoltativa durante l'operazione di esportazione hello, AzCopy genererà un file manifesto con il nome predefinito se non si specifica questa opzione.

Questa opzione è necessaria durante l'operazione di importazione hello per individuare i file di dati hello.

**Applicabile a:** tabelle

### <a name="synccopy"></a>/SyncCopy
Indica se toosynchronously copiare BLOB o i file tra due endpoint di archiviazione di Azure.

Per impostazione predefinita, AzCopy esegue la copia in modo asincrono sul lato server. Specificare questa opzione tooperform sincrona copia, che scarica BLOB o i file di memoria toolocal e quindi li carica tooAzure archiviazione.

È possibile utilizzare questa opzione quando si copiano file nell'archiviazione Blob, all'interno di archiviazione di File o da Blob archiviazione tooFile archiviazione o vice versa.

**Applicabile a:** BLOB, file

### <a name="setcontenttypecontent-type"></a>/SetContentType:"content-type"
Specifica tipo di contenuto MIME hello per BLOB di destinazione o i file.

Set di AzCopy hello tipo di contenuto per un blob o il file tooapplication/octet-stream per impostazione predefinita. Specificando in modo esplicito un valore per questa opzione, è possibile impostare tipo di contenuto per tutti i BLOB o i file hello.

Se si specifica questa opzione senza un valore, AzCopy imposterà ogni blob o il tipo di contenuto del file in base a tooits estensione di file.

**Applicabile a:** BLOB, file

### <a name="payloadformatjson--csv"></a>/PayloadFormat:"JSON" | "CSV"
Specifica il formato di hello hello tabella esportata del file di dati.

Se questa opzione non è specificata, per impostazione predefinita AzCopy esporta il file di dati tabella nel formato JSON.

**Applicabile a:** tabelle

## <a name="known-issues-and-best-practices"></a>Problemi noti e procedure consigliate
### <a name="limit-concurrent-writes-while-copying-data"></a>Limitare le scritture simultanee durante la copia dei dati
Quando si copiano BLOB o i file con AzCopy, tenere presente che un'altra applicazione può modificare dati hello mentre si copiano. Se possibile, verificare che i dati di hello che si copia non viene modificati durante l'operazione di copia hello. Ad esempio, quando si copia un disco rigido virtuale associato a una macchina virtuale di Azure, assicurarsi che altre applicazioni non sono attualmente scrivendo toohello disco rigido virtuale. Toodo un modo efficace questa caratteristica è leasing hello risorsa toobe copiati. In alternativa, è possibile creare uno snapshot del disco rigido virtuale hello prima e quindi copiare hello snapshot.

Se non è possibile impedire o la scrittura tooblobs file mentre vengono copiate, quindi tenere presente che, dal processo di hello hello tempo al termine di altre applicazioni, hello copiate risorse possono non avere completa parità con le risorse dell'origine hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Eseguire un'istanza di AzCopy su un computer.
AzCopy è progettato toomaximize hello utilizzo del computer risorse tooaccelerate hello di trasferimento dei dati, è consigliabile eseguire solo un'istanza di AzCopy in un computer e specificare l'opzione hello `/NC` se è necessario simultanea di più operazioni. Per ulteriori informazioni, digitare `AzCopy /?:NC` nella riga di comando hello.

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a>Abilitare gli algoritmi MD5 conformi a FIPS per AzCopy quando si utilizzano gli algoritmi FIPS compatibili per crittografia, hash e firma.
AzCopy per impostazione predefinita utilizza hello toocalculate di implementazione .NET MD5 MD5 durante la copia di oggetti, ma esistono alcuni requisiti di sicurezza che richiedono l'impostazione MD5 compatibile di AzCopy tooenable FIPS.

È possibile creare un file app.config `AzCopy.exe.config` con la proprietà `AzureStorageUseV1MD5` e conservarlo con AzCopy.exe.

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

Per la proprietà "AzureStorageUseV1MD5" • True: valore predefinito di hello, AzCopy utilizzerà implementazione .NET MD5.
• False: AzCopy utilizzerà l'algoritmo MD5 conforme a FIPS.

Si noti che gli algoritmi conformi a FIPS sono disabilitati per impostazione predefinita nel computer Windows. Digitare secpol.msc nella finestra Esegui e selezionare questa opzione in Impostazione di sicurezza -> Criteri locali -> Opzioni di sicurezza -> Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'archiviazione di Azure e AzCopy, vedere toohello seguenti risorse.

### <a name="azure-storage-documentation"></a>Documentazione di Archiviazione di Azure
* [Introduzione tooAzure archiviazione](storage-introduction.md)
* [Come toouse archiviazione Blob da .NET](storage-dotnet-how-to-use-blobs.md)
* [Come toouse archiviazione di File da .NET](storage-dotnet-how-to-use-files.md)
* [Come toouse archiviazione tabelle da .NET](storage-dotnet-how-to-use-tables.md)
* [Come toocreate, gestire o eliminare un account di archiviazione](storage-create-storage-account.md)
* [Trasferire dati con AzCopy in Linux](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a>Post del blog di Archiviazione di Azure:
* [Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: ottimizzazione per gli scenari di copia su larga scala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: uso del comando di copia dei BLOB tra account](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Caricamento e download di file per BLOB di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

