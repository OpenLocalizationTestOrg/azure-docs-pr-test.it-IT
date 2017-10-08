---
title: aaaUsing hello Azure CLI 1.0 con archiviazione di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello interfaccia della riga di comando di Azure (Azure CLI) 1.0 con toocreate di archiviazione di Azure e gestire gli account di archiviazione e utilizzo di BLOB di Azure e i file. Hello CLI di Azure è uno strumento multipiattaforma"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>Utilizzo di hello Azure CLI 1.0 con archiviazione di Azure

## <a name="overview"></a>Panoramica

Hello CLI di Azure fornisce un set di open source, multipiattaforma comandi per l'utilizzo con hello piattaforma Azure. Fornisce gran parte delle stesse funzionalità, vedere hello hello [portale di Azure](https://portal.azure.com) funzionalità di accesso ai dati e avanzati.

In questa Guida, si esamineranno come toouse [interfaccia della riga di comando di Azure (Azure CLI)](../../cli-install-nodejs.md) tooperform un'ampia gamma di attività di sviluppo e amministrazione con l'archiviazione di Azure. È consigliabile scaricare e installare o aggiornare toohello CLI di Azure più recenti prima di usare questa Guida.

Questa guida presuppone la conoscenza dei concetti di base hello dell'archiviazione di Azure. Guida di Hello fornisce un numero di script utilizzo hello toodemonstrate di hello CLI di Azure con l'archiviazione di Azure. Essere tooupdate che le variabili dello script hello in base alla configurazione prima di eseguire ogni script.

> [!NOTE]
> Guida di Hello fornisce esempi di script e comando CLI di Azure di hello per gli account di archiviazione classico. Vedere [Using hello CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) per i comandi CLI di Azure per gli account di archiviazione di gestione risorse.
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Introduzione all'archiviazione di Azure e hello CLI di Azure in 5 minuti
In questa guida utilizza Ubuntu per gli esempi, ma altre piattaforme del sistema operativo devono eseguire in modo analogo.

**Nuovo tooAzure:** ottenere una sottoscrizione di Microsoft Azure e un account Microsoft associato a tale sottoscrizione. Per informazioni sulle opzioni di acquisto di Azure, vedere la [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/), le [opzioni di acquisto](https://azure.microsoft.com/pricing/purchase-options/) e le [offerte per i membri](https://azure.microsoft.com/pricing/member-offers/) (per i membri di MSDN, Microsoft Partner Network, BizSpark e altri programmi Microsoft).

Per altre informazioni sulle sottoscrizioni di Azure, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .

**Dopo aver creato una sottoscrizione e un account di Microsoft Azure:**

1. Scaricare e installare hello Azure CLI hello alle istruzioni descritte nella [installazione hello Azure CLI](../../cli-install-nodejs.md).
2. Una volta hello CLI di Azure è stato installato, sarà in grado di toouse hello azure comando i comandi di Azure CLI hello tooaccess interfaccia della riga di comando (Bash, Terminal, prompt dei comandi). Hello tipo _azure_ comando e si dovrebbe essere hello output seguente.

    ![Output del comando di esempio:](./media/storage-azure-cli/azure_command.png)   
3. Nell'interfaccia della riga di comando hello, digitare `azure storage` toolist tutte hello i comandi di archiviazione di azure e ottenere una visione prima di hello funzionalità hello CLI di Azure fornisce. È possibile digitare il nome di comando con **-h** parametro (ad esempio, `azure storage share create -h`) toosee dettagli della sintassi del comando.
4. A questo punto, verrà fornita è un semplice script che mostra tooaccess di comandi CLI di Azure basic di archiviazione di Azure. script Hello verrà innanzitutto richiesto tooset due variabili per l'account di archiviazione e la chiave. Quindi, hello script creare un nuovo contenitore in questo nuovo account di archiviazione e caricare un contenitore toothat (blob) di file di immagine esistente. Dopo aver hello script permette di elencare tutti i BLOB nel contenitore, verrà scaricato hello immagine toohello destinazione directory del file esistente sul computer locale hello.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. Nel computer locale, aprire l'editor di testo preferito (vim ad esempio). Digitare hello sopra script nell'editor di testo.
6. A questo punto, è necessario tooupdate hello scripting di variabili in base alle impostazioni di configurazione.

   * **< Storage_account_name >** utilizzare hello dato nome nello script hello o immettere un nuovo nome per l'account di archiviazione. **Importante:** nome hello hello dell'account di archiviazione deve essere univoco in Azure. Utilizzare caratteri minuscoli.
   * **< storage_account_key >** chiave di accesso hello dell'account di archiviazione.
   * **< Container_name >** utilizzare hello dato nome nello script hello o immettere un nuovo nome per il contenitore.
   * **< Image_to_upload >** immettere un'immagine di tooa percorso sul computer locale, ad esempio: "~ / images/HelloWorld.png".
   * **< Destination_folder >** immettere un percorso tooa directory locale toostore scaricare i file dall'archiviazione di Azure, ad esempio: "~/downloadImages".
7. Dopo aver aggiornato le variabili necessarie hello in vim, premere le combinazioni di tasti `ESC`, `:`, `wq!` script hello toosave.
8. toorun questo script, semplicemente tipo hello nome del file script nella console di hello bash. Quando si esegue questo script, è una cartella di destinazione locale che include i file di immagine scaricato hello. Hello seguente schermata mostra un esempio dell'output:

Dopo l'esecuzione di script hello è una cartella di destinazione locale che include i file di immagine scaricato hello.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Gestire gli account di archiviazione con hello CLI di Azure
### <a name="connect-tooyour-azure-subscription"></a>Connettersi tooyour sottoscrizione di Azure
Anche se la maggior parte dei comandi di archiviazione hello funzionerà senza una sottoscrizione di Azure, è consigliabile tooconnect tooyour sottoscrizione hello CLI di Azure. tooconfigure hello Azure CLI toowork con la sottoscrizione, seguire i passaggi hello [connettersi tooan sottoscrizione di Azure da hello Azure CLI](../../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Creare un nuovo account di archiviazione.
toouse archiviazione di Azure, è necessario un account di archiviazione. Dopo aver configurato la sottoscrizione di tooyour tooconnect computer, è possibile creare un nuovo account di archiviazione di Azure.

```azurecli
azure storage account create <account_name>
```

nome di Hello dell'account di archiviazione deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare i numeri e lettere minuscole solo.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Impostare un account di archiviazione Azure predefinito nelle variabili di ambiente
È possibile avere più account di archiviazione nella sottoscrizione. È possibile scegliere uno di essi e impostate nel hello le variabili di ambiente per l'archiviazione hello tutti i comandi hello stessa sessione. Ciò consente l'archiviazione di Azure CLI hello toorun comandi senza specificare archiviazione hello account e la chiave in modo esplicito.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Stringa di connessione utilizza un altro modo tooset un account di archiviazione predefinito. Prima di tutto ottenere la stringa di connessione hello dal comando:

```azurecli
azure storage account connectionstring show <account_name>
```

Copiare la stringa di connessione di output di hello e impostarlo tooenvironment variabile:

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Creare e gestire gli account di accesso
Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS. In questa sezione si presuppone che si ha già familiarità con i concetti di archiviazione Blob di Azure hello. Per informazioni dettagliate, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Concetti relativi al servizio BLOB](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Creare un contenitore
Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore. È possibile creare un contenitore privato utilizzando hello `azure storage container create` comando:

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Esistono tre livelli di accesso in lettura anonimo: **Off**, **BLOB** e **contenitore**. tooprevent anonimo accesso troppo accedere tooblobs, il parametro di autorizzazione del set di hello**Off**. Per impostazione predefinita, hello nuovo contenitore è privato e accessibile solo dal proprietario dell'account hello. in lettura pubblico anonimo tooallow tooblob di accedere alle risorse, ma non toocontainer metadati o toohello elenco di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**Blob**. in lettura pubblico completo tooallow tooblob di accedere alle risorse e i metadati del contenitore elenco hello di BLOB nel contenitore di hello, impostare il parametro di autorizzazione hello troppo**contenitore**. Per ulteriori informazioni, vedere [gestire BLOB e accesso in lettura anonimo toocontainers](../blobs/storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
Nell'archivio BLOB di Azure sono supportati BLOB in blocchi e BLOB di pagine. Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).

i BLOB nel contenitore tooa tooupload, è possibile utilizzare hello `azure storage blob upload`. Per impostazione predefinita, questo comando Carica blob in blocchi tooa hello file locali. tipo di hello toospecify per blob hello, è possibile utilizzare hello `--blobtype` parametro.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Come scaricare i BLOB da un contenitore
Hello di esempio seguente viene illustrato come toodownload BLOB da un contenitore.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Copiare i BLOB
È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.

Hello esempio seguente viene illustrato come toocopy BLOB da un archivio account tooanother. In questo esempio è possibile creare un contenitore in cui i BLOB sono pubblicamente, accessibile in forma anonima.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

Nell'esempio viene eseguita una copia asincrona. È possibile monitorare lo stato di hello di ogni operazione di copia eseguendo hello `azure storage blob copy show` operazione.

Si noti che hello origine URL fornito per l'operazione di copia hello deve essere accessibile pubblicamente o includono un token di firma di accesso condiviso (firma di accesso condiviso).

### <a name="delete-a-blob"></a>Eliminare un BLOB
toodelete un blob, utilizzare hello comando seguente:

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Creare e gestire condivisioni di file
Archiviazione di File di Azure offre archiviazione condivisa per applicazioni che utilizzano il protocollo SMB standard di hello. Macchine virtuali di Microsoft Azure e servizi cloud, nonché applicazioni locali, possono condividere i dati di file tra condivisioni montate. È possibile gestire condivisioni file e dati di file tramite hello CLI di Azure. Per ulteriori informazioni sull'archiviazione di File di Azure, vedere [Introduzione all'archiviazione di File di Azure in Windows](../storage-dotnet-how-to-use-files.md) o [come archiviazione di File di Azure con Linux toouse](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Creare una condivisione file
Una condivisione di archiviazione file è una condivisione file SMB di Azure. Tutte le directory e i file devono essere creati in una condivisione padre. Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, i limiti di capacità toohello hello dell'account di archiviazione. esempio Hello crea una condivisione file denominata **myshare**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Creare una directory
Una directory fornisce una struttura gerarchica facoltativa per una condivisione di file di Azure. esempio Hello crea una directory denominata **myDir** nella condivisione di file hello.

```azurecli
azure storage directory create myshare myDir
```

Si noti che tale percorso di directory può includere più livelli, *ad esempio*, **un / b**. Tuttavia è necessario assicurarsi che tutte le directory padre esistano. Ad esempio, per il percorso **a/b**, è necessario creare prima la directory **a** e poi la directory **b**.

### <a name="upload-a-local-file-toodirectory"></a>Caricare un file locale di toodirectory
esempio Hello carica un file da **~/temp/samplefile.txt** toohello **myDir** directory. Modificare il percorso del file hello in modo che punti tooa file valido sul computer locale:

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Si noti che può essere un file nella condivisione di hello backup too1 TB nella dimensione.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Elencare i file hello nella radice di hello condivisione o directory
È possibile elencare i file hello e le sottodirectory in una radice di condivisione o una directory tramite hello comando seguente:

```azurecli
azure storage file list myshare myDir
```

Si noti che il nome directory hello sia facoltativo per l'operazione di elenco hello. Se omesso, il comando hello Elenca il contenuto di hello della directory radice hello della condivisione hello.

### <a name="copy-files"></a>Copiare i file
A partire dalla versione 0.9.8 di CLI di Azure, è possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa. Di seguito viene illustrato come questi tooperform copiare operazioni utilizzando i comandi CLI. toocopy una nuova directory toohello di file:

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

una directory del file blob tooa toocopy:

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Passaggi successivi

È possibile trovare riferimenti ai comandi dell'interfaccia della riga di comando 1.0 di Azure da usare con le risorse di Archiviazione qui:

* [Comandi dell'interfaccia della riga di comando Azure in modalità Resource Manager](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Comandi dell'interfaccia della riga di comando di Azure in modalità Gestione servizi di Azure](../../cli-install-nodejs.md)

Anche desiderato hello tootry [CLI di Azure 2.0](../storage-azure-cli.md), la CLI di prossima generazione scritti in Python, per l'utilizzo con modello di distribuzione di gestione risorse di hello.
