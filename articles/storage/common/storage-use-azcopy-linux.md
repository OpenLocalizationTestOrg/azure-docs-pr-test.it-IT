---
title: aaaCopy o lo spostamento dati tooAzure archiviazione con AzCopy in Linux | Documenti Microsoft
description: "Usare AzCopy hello in Linux utilità toomove o copia dati tooor dal contenuto di blob e file. Copiare i dati tooAzure archiviazione da file locali, o copiare dati in o tra gli account di archiviazione. Migrare facilmente l'archiviazione di tooAzure di dati."
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
ms.date: 05/11/2017
ms.author: seguler
ms.openlocfilehash: ee39c311d996a046999b7fd4a4eb873f25b4eb86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-azcopy-on-linux"></a>Trasferire dati con AzCopy in Linux
AzCopy in Linux è un'utilità della riga di comando progettata per la copia di dati tooand dall'archiviazione Blob di Microsoft Azure e i File utilizzando i comandi semplici con prestazioni ottimali. È possibile copiare dati da un oggetto tooanother all'interno dell'account di archiviazione o tra gli account di archiviazione.

Esistono due versioni di AzCopy che è possibile scaricare. AzCopy in Linux viene compilato con .NET Core Framework per le piattaforme Linux e offre opzioni della riga di comando in stile POSIX. [AzCopy in Windows](../storage-use-azcopy.md) viene compilato con .NET Framework e offre opzioni della riga di comando in stile Windows. Questo articolo descrive AzCopy in Linux.

## <a name="download-and-install-azcopy"></a>Scaricare e installare AzCopy
### <a name="installation-on-linux"></a>Installazione in Linux

AzCopy in Linux richiede il framework .NET Core su piattaforma hello. Vedere le istruzioni di installazione di hello sulla hello [.NET Core](https://www.microsoft.com/net/core#linuxubuntu) pagina.

Ecco un esempio di installazione di .NET Core in Ubuntu 16.10. Hello più recente della Guida all'installazione, visitare [.NET Core su Linux](https://www.microsoft.com/net/core#linuxubuntu) pagina di installazione.


```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
sudo apt-get update
sudo apt-get install dotnet-dev-1.0.3
```

Dopo aver installato .NET Core, scaricare e installare AzCopy.

```bash
wget -O azcopy.tar.gz https://aka.ms/downloadazcopyprlinux
tar -xf azcopy.tar.gz
sudo ./install.sh
```

Dopo aver installato AzCopy in Linux, è possibile rimuovere file hello estratto. In alternativa se non si dispone di privilegi avanzati, è possibile anche eseguire tramite script della shell hello AzCopy 'azcopy' nella cartella di estrazione hello. 

### <a name="alternative-installation-on-ubuntu"></a>Installazione alternativa in Ubuntu

**Ubuntu 14.04**

Aggiungere un'origine apt per .Net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.04**

Aggiungere un'origine apt per .Net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

**Ubuntu 16.10**

Aggiungere un'origine apt per .Net Core:

```bash
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list' 
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
```

Aggiungere un'origine apt per il repository di prodotti Linux di Microsoft e installare AzCopy:

```bash
curl https://packages.microsoft.com/config/ubuntu/16.10/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

```bash
sudo apt-get update
sudo apt-get install azcopy
```

## <a name="writing-your-first-azcopy-command"></a>Scrittura del primo comando AzCopy 
sintassi di base per i comandi AzCopy Hello è:

```azcopy
azcopy --source <source> --destination <destination> [Options]
```

Hello seguenti esempi illustrano vari scenari per la copia dei dati tooand da file e i BLOB di Microsoft Azure. Fare riferimento toohello `azcopy --help` menu per una spiegazione dettagliata dei parametri di hello utilizzata in ogni esempio.

## <a name="blob-download"></a>BLOB: scaricare
### <a name="download-single-blob"></a>Scaricare un singolo BLOB

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Se la cartella hello `/mnt/myfiles` non esiste, AzCopy crea e ne scarica `abc.txt ` nella nuova cartella hello.

### <a name="download-single-blob-from-secondary-region"></a>Scaricare un singolo BLOB da un'area secondaria

```azcopy
azcopy \
    --source https://myaccount-secondary.blob.core.windows.net/mynewcontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.

### <a name="download-all-blobs"></a>Scaricare tutti BLOB

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Si supponga che segue hello BLOB si trovano nel contenitore specificato hello:  

```
abc.txt
abc1.txt
abc2.txt
vd1/a.txt
vd1/abcd.txt
```

Dopo un'operazione di download hello hello directory `/mnt/myfiles` include hello i seguenti file:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/vd1/a.txt
/mnt/myfiles/vd1/abcd.txt
```

Se non si specifica l'opzione `--recursive`, non verrà scaricato alcun BLOB.

### <a name="download-blobs-with-specified-prefix"></a>Scaricare i BLOB con il prefisso specificato

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "a" \
    --recursive
```

Si supponga che segue hello BLOB si trovano nel contenitore specificato hello. Tutti i blob che iniziano con il prefisso hello `a` vengono scaricati.

```
abc.txt
abc1.txt
abc2.txt
xyz.txt
vd1\a.txt
vd1\abcd.txt
```

Dopo un'operazione di download hello hello cartella `/mnt/myfiles` include hello i seguenti file:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
```

prefisso Hello applica toohello directory virtuale, che costituisce hello prima parte del nome blob hello. Nell'esempio hello illustrato in precedenza, la directory virtuale hello non corrisponde prefisso specificato hello, non viene scaricato alcun blob. Inoltre, se hello opzione `--recursive` non viene specificato, AzCopy non scarica tutti i BLOB.

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a>Impostare l'ora dell'ultima modifica hello dei file esportati toobe stesso hello BLOB di origine

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination "/mnt/myfiles" \
    --source-key <key> \
    --preserve-last-modified-time
```

È anche possibile escludere i BLOB da un'operazione di download hello in base all'ora ultima modifica. Ad esempio, se si desidera tooexclude BLOB la cui ultima modifica è hello uguale o più file di destinazione hello recente, aggiungere hello `--exclude-newer` opzione:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-newer
```

O se si desidera tooexclude BLOB la cui ultima modifica è hello stesso o meno i file di destinazione hello, aggiungere hello `--exclude-older` opzione:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer \
    --destination /mnt/myfiles \
    --source-key <key> \
    --preserve-last-modified-time \
    --exclude-older
```

## <a name="blob-upload"></a>BLOB: caricare
### <a name="upload-single-file"></a>Caricare un singolo file

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Se il contenitore di destinazione specificato hello non esiste, AzCopy crea e ne caricamenti hello file al suo interno.

### <a name="upload-single-file-toovirtual-directory"></a>Caricare file singoli toovirtual directory

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "abc.txt"
```

Se hello specificato una directory virtuale non esiste, AzCopy carica hello file tooinclude hello directory virtuale nel nome di blob hello (*ad esempio*, `vd/abc.txt` nell'esempio hello sopra).

### <a name="upload-all-files"></a>Caricare tutti i file

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --recursive
```

Specifica l'opzione `--recursive` contenuto hello caricamenti di hello specificato directory tooBlob archiviazione in modo ricorsivo, vale a dire che tutte le sottocartelle e i file vengono caricati anche. Ad esempio, si supponga che segue hello file si trovano nella cartella `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Dopo un'operazione di caricamento hello contenitore hello include hello i seguenti file:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Hello quando l'opzione `--recursive` non viene specificato, solo hello tre vengono caricati file seguenti:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="upload-files-matching-specified-pattern"></a>Caricare i file corrispondenti ai criteri specificati

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --include "a*" \
    --recursive
```

Si supponga che segue hello file si trovano nella cartella `/mnt/myfiles`:

```
/mnt/myfiles/abc.txt
/mnt/myfiles/abc1.txt
/mnt/myfiles/abc2.txt
/mnt/myfiles/xyz.txt
/mnt/myfiles/subfolder/a.txt
/mnt/myfiles/subfolder/abcd.txt
```

Dopo un'operazione di caricamento hello contenitore hello include hello i seguenti file:

```
abc.txt
abc1.txt
abc2.txt
subfolder/a.txt
subfolder/abcd.txt
```

Hello quando l'opzione `--recursive` non viene specificato, AzCopy Ignora file presenti nella sottodirectory:

```
abc.txt
abc1.txt
abc2.txt
```

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a>Specificare hello tipo di contenuto MIME di un blob di destinazione
Per impostazione predefinita, AzCopy Imposta tipo di contenuto di un blob di destinazione hello troppo`application/octet-stream`. Tuttavia, è possibile specificare in modo esplicito tipo di contenuto tramite l'opzione hello hello `--set-content-type [content-type]`. Questa sintassi Imposta tipo di contenuto hello per tutti i BLOB in un'operazione di caricamento.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type "video/mp4"
```

Se hello opzione `--set-content-type` viene specificata senza un valore, quindi AzCopy imposta ogni blob o il file del tipo di contenuto in base tooits estensione di file.

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/myContainer/ \
    --dest-key <key> \
    --include "ab" \
    --set-content-type
```

## <a name="blob-copy"></a>BLOB: copiare
### <a name="copy-single-blob-within-storage-account"></a>Copiare un BLOB all'interno di un account di archiviazione

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key> \
    --dest-key <key> \
    --include "abc.txt"
```

Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-across-storage-accounts"></a>Copiare un singolo BLOB tra account di archiviazione

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

Quando si copia un BLOB senza l'opzione --sync-copy, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a>Copiare blob singolo dall'area tooprimary area secondaria

```azcopy
azcopy \
    --source https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 \
    --destination https://myaccount2.blob.core.windows.net/mynewcontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt"
```

È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a>Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione

```azcopy
azcopy \
    --source https://sourceaccount.blob.core.windows.net/mycontainer1 \
    --destination https://destaccount.blob.core.windows.net/mycontainer2 \
    --source-key <key1> \
    --dest-key <key2> \
    --include "abc.txt" \
    --include-snapshot
```

Dopo un'operazione di copia hello contenitore di destinazione hello include blob hello e i relativi snapshot. contenitore Hello include hello segue blob e i relativi snapshot:

```
abc.txt
abc (2013-02-25 080757).txt
abc (2014-02-21 150331).txt
```

### <a name="synchronously-copy-blobs-across-storage-accounts"></a>Copiare in modo sincrono i BLOB tra account di archiviazione
Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono. Pertanto, hello copia operazione viene eseguita in background hello usando la capacità della larghezza di banda di riserva che non dispone di alcun contratto di servizio in termini di velocità con cui un blob viene copiato. 

Hello `--sync-copy` opzione assicura che l'operazione di copia hello Ottiene velocità coerente. AzCopy esegue copia sincrono hello scaricando BLOB hello toocopy da hello specificato memoria toolocal di origine e quindi caricarli toohello destinazione di archiviazione Blob.

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/myContainer/ \
    --destination https://myaccount2.blob.core.windows.net/myContainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --include "ab" \
    --sync-copy
```

`--sync-copy`potrebbe generare uscita ulteriori costi rispetto tooasynchronous copia. Hello approccio consigliato è toouse questa opzione in una macchina virtuale di Azure, che è in hello stessa area del costo di uscita origine tooavoid account di archiviazione.

## <a name="file-download"></a>File: scaricare
### <a name="download-single-file"></a>Scaricare un singolo file

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/myfolder1/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --include "abc.txt"
```

Se è specificato l'origine è una condivisione di file di Azure, quindi è necessario specificare il nome di file esatto hello, hello (*ad esempio* `abc.txt`) toodownload un singolo file, oppure specificare l'opzione `--recursive` toodownload tutti i file nella condivisione di hello in modo ricorsivo. Il tentativo di toospecify un modello di file e l'opzione `--recursive` contemporaneamente provoca un errore.

### <a name="download-all-files"></a>Scaricare tutti i file

```azcopy
azcopy \
    --source https://myaccount.file.core.windows.net/myfileshare/ \
    --destination /mnt/myfiles \
    --source-key <key> \
    --recursive
```

Le cartelle vuote non vengono scaricate.

## <a name="file-upload"></a>File: caricare
### <a name="upload-single-file"></a>Caricare un singolo file

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include abc.txt
```

### <a name="upload-all-files"></a>Caricare tutti i file

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --recursive
```

Le cartelle vuote non vengono caricate.

### <a name="upload-files-matching-specified-pattern"></a>Caricare i file corrispondenti ai criteri specificati

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.file.core.windows.net/myfileshare/ \
    --dest-key <key> \
    --include "ab*" \
    --recursive
```

## <a name="file-copy"></a>File: copia
### <a name="copy-across-file-shares"></a>Copiare tra condivisioni file

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).

### <a name="copy-from-file-share-tooblob"></a>Copiare da tooblob condivisione file

```azcopy
azcopy \ 
    --source https://myaccount1.file.core.windows.net/myfileshare/ \
    --destination https://myaccount2.blob.core.windows.net/mycontainer/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando si copia un file da tooblob di condivisione file, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.

### <a name="copy-from-blob-toofile-share"></a>Copiare da blob toofile condivisione

```azcopy
azcopy \
    --source https://myaccount1.blob.core.windows.net/mycontainer/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive
```
Quando si copia un file dalla condivisione toofile blob, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.

### <a name="synchronously-copy-files"></a>Copiare file in modo sincrono
È possibile specificare hello `--sync-copy` opzione toocopy dati da archiviazione di File tooFile archiviazione da archiviazione di File tooBlob, archiviazione e, dall'archiviazione Blob tooFile archiviazione in modo sincrono. AzCopy viene eseguita questa operazione per il download di memoria di toolocal hello origine dati e quindi caricarli toodestination. In questo caso, vengono applicati i costi in uscita standard.

```azcopy
azcopy \
    --source https://myaccount1.file.core.windows.net/myfileshare1/ \
    --destination https://myaccount2.file.core.windows.net/myfileshare2/ \
    --source-key <key1> \
    --dest-key <key2> \
    --recursive \
    --sync-copy
```

Durante la copia da archiviazione di File tooBlob archiviazione, è di tipo di blob predefinito hello blob in blocchi, l'utente può specificare l'opzione `/BlobType:page` toochange hello tipo di blob di destinazione.

Si noti che `--sync-copy` potrebbe generare uscita ulteriore costi Copia tooasynchronous il confronto. Hello approccio consigliato è toouse questa opzione in una macchina virtuale di Azure, che è in hello stessa area del costo di uscita origine tooavoid account di archiviazione.

## <a name="other-azcopy-features"></a>Altre funzionalità di AzCopy
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a>Copia solo i dati che non esistono nella destinazione hello
Hello `--exclude-older` e `--exclude-newer` parametri consentono tooexclude le risorse dell'origine o meno recente viene copiato, rispettivamente. Se si desidera solo le risorse dell'origine toocopy che non sono presenti nella destinazione hello, è possibile specificare entrambi i parametri nel comando AzCopy hello:

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --exclude-older --exclude-newer

    --source /mnt/myfiles --destination http://myaccount.file.core.windows.net/myfileshare --dest-key <destkey> --recursive --exclude-older --exclude-newer

    --source http://myaccount.blob.core.windows.net/mycontainer --destination http://myaccount.blob.core.windows.net/mycontainer1 --source-key <sourcekey> --dest-key <destkey> --recursive --exclude-older --exclude-newer

### <a name="use-a-configuration-file-toospecify-command-line-parameters"></a>Utilizzare i parametri della riga di comando toospecify file configurazione

```azcopy
azcopy --config-file "azcopy-config.ini"
```

È possibile includere i parametri della riga di comando di AzCopy in un file di configurazione. I processi di AzCopy hello parametri nel file hello come se fossero stati specificati nella riga di comando hello, eseguire una sostituzione diretta con contenuto hello del file hello.

Si supponga che un file di configurazione denominato `copyoperation`, che contiene hello seguenti righe. Ogni parametro di AzCopy può essere specificato su una singola riga

    --source http://myaccount.blob.core.windows.net/mycontainer --destination /mnt/myfiles --source-key <sourcekey> --recursive --quiet

o su righe separate:

    --source http://myaccount.blob.core.windows.net/mycontainer
    --destination /mnt/myfiles
    --source-key<sourcekey>
    --recursive
    --quiet

AzCopy ha esito negativo se il parametro hello si divide in due righe, come illustrato di seguito per hello `--source-key` parametro:

    http://myaccount.blob.core.windows.net/mycontainer
    /mnt/myfiles
    --sourcekey
    <sourcekey>
    --recursive
    --quiet

### <a name="specify-a-shared-access-signature-sas"></a>Specificare una firma di accesso condiviso

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1 \
    --destination https://myaccount.blob.core.windows.net/mycontainer2 \
    --source-sas <SAS1> \
    --dest-sas <SAS2> \
    --include abc.txt
```

È inoltre possibile specificare una firma di accesso condiviso nel contenitore hello URI:

```azcopy
azcopy \
    --source https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken \
    --destination /mnt/myfiles \
    --recursive
```

Si noti che AzCopy supporta attualmente solo hello [SAS Account](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-shared-access-signature-part-1).

### <a name="journal-file-folder"></a>Cartella del file journal
Ogni volta che si esegue un comando tooAzCopy, controlla se è presente un file journal nella cartella predefinita hello o se esiste in una cartella specificata tramite questa opzione. Se non esiste alcun file journal hello in entrambe le posizioni, AzCopy considera nuova operazione hello e genera un nuovo file journal.

Se esistono file journal hello, AzCopy controlla se hello riga di comando che l'input corrisponde hello riga di comando nel file journal hello. Se due righe di comando hello corrispondono, AzCopy riprende hello incompleti. Se non corrispondono, AzCopy richiede all'utente tooeither sovrascrittura hello journal file toostart una nuova operazione o l'operazione corrente di toocancel hello.

Se si desidera toouse hello percorso predefinito file journal hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --resume
```

Se si omette l'opzione `--resume`, oppure specificare l'opzione `--resume` senza percorso della cartella hello, come illustrato in precedenza, AzCopy crea file journal hello nel percorso predefinito di hello, ovvero `~\Microsoft\Azure\AzCopy`. Se il file journal di hello esiste già, quindi AzCopy riprende l'operazione di hello basato su file journal hello.

Se si desidera toospecify un percorso personalizzato per il file journal hello:

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key key \
    --resume "/mnt/myjournal"
```

Questo esempio crea file journal hello se non esiste già. Se esiste, quindi AzCopy riprende l'operazione di hello basato su file journal hello.

Se si desidera tooresume un'operazione AzCopy, ripetere hello stesso comando. AzCopy in Linux richiederà la conferma:

```azcopy
Incomplete operation with same command line detected at hello journal directory "/home/myaccount/Microsoft/Azure/AzCopy", do you want tooresume hello operation? Choose Yes tooresume, choose No toooverwrite hello journal toostart a new operation. (Yes/No)
```

### <a name="output-verbose-logs"></a>Output di log dettagliati

```azcopy
azcopy \
    --source /mnt/myfiles \
    --destination https://myaccount.blob.core.windows.net/mycontainer \
    --dest-key <key> \
    --verbose
```

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a>Specificare il numero di hello di operazioni simultanee toostart
Opzione `--parallel-level` specifica hello numero di operazioni di copia simultanea. Per impostazione predefinita, AzCopy inizia un certo numero di velocità effettiva di trasferimento dei dati di operazioni simultanee tooincrease hello. numero di Hello di operazioni simultanee è uguale otto volte hello numero di processori disponibili. Se si esegue AzCopy attraverso una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per - parallelo livello tooavoid errore di concorrenza di risorse.

[!TIP]
>elenco completo di hello tooview dei parametri di AzCopy, estrarre "azcopy - help" dal menu.

## <a name="known-issues-and-best-practices"></a>Problemi noti e procedure consigliate
### <a name="error-net-core-is-not-found-in-hello-system"></a>Errore: .NET Core non è stato trovato nel sistema hello.
Se si verifica un errore che informa che .NET Core non è installato nel sistema hello, hello binario di .NET Core toohello percorso `dotnet` potrebbe essere mancante.

In ordine tooaddress questo problema, trovare il file binario di .NET Core hello nel sistema hello:
```bash
sudo find / -name dotnet
```

Vengono restituite hello percorso toohello dotnet binario. 

    /opt/rh/rh-dotnetcore11/root/usr/bin/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/dotnet
    /opt/rh/rh-dotnetcore11/root/usr/lib64/dotnetcore/shared/Microsoft.NETCore.App/1.1.2/dotnet

Aggiungere quindi questa variabile di percorso toohello percorso. Per sudo, modifica secure_path toocontain hello percorso toohello dotnet binario:
```bash 
sudo visudo
### Append hello path found in hello preceding example too'secure_path' variable
```

In questo esempio, la variabile secure_path è:

```
secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/opt/rh/rh-dotnetcore11/root/usr/bin/
```

Per l'utente corrente di hello, modificare.bash_profile/.profile tooinclude hello percorso toohello dotnet binario nella variabile PATH 
```bash
vi ~/.bash_profile
### Append hello path found in hello preceding example too'PATH' variable
```

Verificare che .NET Core sia ora presente in PATH:
```bash
which dotnet
sudo which dotnet
```

### <a name="error-installing-azcopy"></a>Errore durante l'installazione di AzCopy
Se si verificano problemi con l'installazione di AzCopy, è possibile provare toorun AzCopy utilizzando script bash hello in hello estratti `azcopy` cartella.

```bash
cd azcopy
./azcopy
```

### <a name="limit-concurrent-writes-while-copying-data"></a>Limitare le scritture simultanee durante la copia dei dati
Quando si copiano BLOB o i file con AzCopy, tenere presente che un'altra applicazione può modificare dati hello mentre si copiano. Se possibile, verificare che i dati di hello che si copia non viene modificati durante l'operazione di copia hello. Ad esempio, quando si copia un disco rigido virtuale associato a una macchina virtuale di Azure, assicurarsi che altre applicazioni non sono attualmente scrivendo toohello disco rigido virtuale. Toodo un modo efficace questa caratteristica è leasing hello risorsa toobe copiati. In alternativa, è possibile creare uno snapshot del disco rigido virtuale hello prima e quindi copiare hello snapshot.

Se non è possibile impedire o la scrittura tooblobs file mentre vengono copiate, quindi tenere presente che, dal processo di hello hello tempo al termine di altre applicazioni, hello copiate risorse possono non avere completa parità con le risorse dell'origine hello.

### <a name="run-one-azcopy-instance-on-one-machine"></a>Eseguire un'istanza di AzCopy su un computer.
AzCopy è progettato toomaximize hello utilizzo del computer risorse tooaccelerate hello di trasferimento dei dati, è consigliabile eseguire solo un'istanza di AzCopy in un computer e specificare l'opzione hello `--parallel-level` se è necessario simultanea di più operazioni. Per ulteriori informazioni, digitare `AzCopy --help parallel-level` nella riga di comando hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sull'archiviazione di Azure e AzCopy, vedere hello seguenti risorse:

### <a name="azure-storage-documentation"></a>Documentazione di Archiviazione di Azure
* [Introduzione tooAzure archiviazione](../storage-introduction.md)
* [Creare un account di archiviazione](../storage-create-storage-account.md)
* [Gestire BLOB con Storage Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-explorer-blobs)
* [Utilizzo di hello Azure CLI 2.0 con archiviazione di Azure](../storage-azure-cli.md)
* [Come toouse archiviazione Blob da C++](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Come toouse archiviazione Blob da Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Come toouse archiviazione Blob da Node.js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Come toouse archiviazione Blob da Python](../blobs/storage-python-how-to-use-blob-storage.md)

### <a name="azure-storage-blog-posts"></a>Post del blog di Archiviazione di Azure:
* [Annuncio della versione di anteprima di AzCopy in Linux](https://azure.microsoft.com/en-in/blog/announcing-azcopy-on-linux-preview/)
* [Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [AzCopy: ottimizzazione per gli scenari di copia su larga scala](http://go.microsoft.com/fwlink/?LinkId=507682)
* [AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [AzCopy: uso del comando di copia dei BLOB tra account](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [AzCopy: Caricamento e download di file per BLOB di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

