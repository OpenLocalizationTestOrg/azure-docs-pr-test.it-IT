---
title: aaaUsing hello Azure CLI 2.0 con l'archiviazione di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello interfaccia della riga di comando di Azure (Azure CLI) 2.0 con toocreate di archiviazione di Azure e gestire gli account di archiviazione e utilizzo di BLOB di Azure e i file. Hello Azure CLI 2.0 è uno strumento di multipiattaforma scritto in Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Utilizzo di hello Azure CLI 2.0 con archiviazione di Azure

Hello open source, multipiattaforma Azure CLI versione 2.0 fornisce un set di comandi per l'utilizzo di hello piattaforma Azure. Fornisce gran parte delle stesse funzionalità, vedere hello hello [portale di Azure](https://portal.azure.com), incluso l'accesso a dati complessi.

In questa Guida, verrà illustrato come hello toouse [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform diverse attività di utilizzo delle risorse nell'account di archiviazione di Azure. È consigliabile scaricare e installare o aggiornare toohello la versione più recente di hello CLI 2.0 prima di utilizzare questa Guida.

esempi di Hello in hello Guida prevedono l'uso di hello di hello shell Bash in Ubuntu, ma altre piattaforme devono eseguire in modo analogo. 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Prerequisiti
Questa guida presuppone la conoscenza dei concetti di base hello dell'archiviazione di Azure. Si presuppone inoltre che si è in grado di toosatisfy hello creazione requisiti dell'account specificate di seguito per Azure e hello servizio di archiviazione.

### <a name="accounts"></a>Account
* **Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito](https://azure.microsoft.com/free/).
* **Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Installare hello Azure CLI 2.0

Scaricare e installare hello Azure CLI 2.0 seguendo le istruzioni di hello fornite in [installare Azure CLI 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Se si verificano problemi con l'installazione di hello, estrarre hello [la risoluzione dei problemi di installazione](/cli/azure/install-az-cli2#installation-troubleshooting) sezione dell'articolo hello e hello [la risoluzione dei problemi di installazione](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) Guida su GitHub.
>

## <a name="working-with-hello-cli"></a>Utilizzo di hello CLI

Dopo aver installato hello CLI, è possibile utilizzare hello `az` comando nei comandi CLI di Azure hello tooaccess interfaccia della riga di comando (Bash, Terminal, il prompt dei comandi). Hello tipo `az` comando toosee un elenco completo dei comandi di base hello (hello output di esempio seguente è stata troncata):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

Nell'interfaccia della riga di comando, eseguire il comando hello `az storage --help` hello toolist `storage` comando sottogruppi. le descrizioni di Hello dei sottogruppi di hello viene fornita una panoramica di hello funzionalità hello che CLI di Azure fornisce per lavorare con le risorse di archiviazione.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Connettersi hello CLI tooyour sottoscrizione di Azure

toowork con risorse hello nella sottoscrizione di Azure, è necessario innanzitutto accedere tooyour account Azure con `az login`. È possibile eseguire l'accesso in diversi modi:

* **Accesso interattivo**: `az login`
* **Accesso con nome utente e password**: `az login -u johndoe@contoso.com -p VerySecret`
  * Questo non funziona con gli account Microsoft o gli account che usano Multi-Factor Authentication.
* **Accesso con un'entità servizio**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Script di esempio dell'interfaccia della riga di comando di Azure 2.0

Successivamente, è necessario utilizzare uno script della shell di piccole dimensioni che emette qualche toointeract di comandi CLI di Azure 2.0 base con le risorse di archiviazione di Azure. script Hello prima crea un nuovo contenitore nell'account di archiviazione, quindi carica un contenitore di toothat file (come un blob) esistente. Vengono quindi elencati tutti i BLOB nel contenitore hello e infine Scarica la destinazione nel computer locale che specificano tooa file hello.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Configurare ed eseguire script hello**

1. Aprire un editor di testo, quindi copiare e incollare hello precedente script nell'editor di hello.

2. Aggiornare quindi tooreflect variabili dello script hello le impostazioni di configurazione. Sostituire hello valori, come specificato di seguito:

   * **\<storage_account_name\>**  nome hello dell'account di archiviazione.
   * **\<storage_account_key\>**  chiave di accesso primaria o secondaria hello per l'account di archiviazione.
   * **\<container_name\>**  un nome hello toocreate di nuovo contenitore, ad esempio "azure-cli-esempio-container".
   * **\<blob_name\>**  un nome per il blob di destinazione hello nel contenitore hello.
   * **\<file_to_upload\>**  hello percorso toosmall file nel computer locale, ad esempio "~ / images/HelloWorld.png".
   * **\<destination_file\>**  hello percorso file di destinazione, ad esempio "~ / downloadedImage.png".

3. Dopo aver aggiornato le variabili necessarie hello, salvare script hello e chiudere l'editor. passaggi successivi Hello si supponga che è stato denominato script **my_storage_sample.sh**.

4. Contrassegna script hello come eseguibile, se necessario:`chmod +x my_storage_sample.sh`

5. Eseguire script hello. Ad esempio, in Bash: `./my_storage_sample.sh`

Dovrebbe vedere seguenti toohello simili di output e hello  **\<destination_file\>**  specificato nel hello script devono essere visualizzate sul computer locale.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Hello precedente l'output è in **tabella** formato. È possibile specificare quale output formato toouse specificando hello `--output` argomento nei comandi CLI, o impostare il valore a livello globale tramite `az configure`.
>

## <a name="manage-storage-accounts"></a>Gestire gli account di archiviazione

### <a name="create-a-new-storage-account"></a>Creare un nuovo account di archiviazione.
toouse archiviazione di Azure, è necessario un account di archiviazione. È possibile creare un nuovo account di archiviazione di Azure dopo aver configurato il computer troppo[connettere sottoscrizione tooyour](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location` [Richiesto]: posizione. Ad esempio "Stati Uniti occidentali".
* `--name`[Obbligatorio]: nome account di archiviazione hello. nome Hello deve essere di lunghezza 3 caratteri too24 e utilizzare solo caratteri alfanumerici minuscoli.
* `--resource-group`[Richiesto]: il nome del gruppo di risorse.
* `--sku`[Obbligatorio]: hello SKU di account di archiviazione. Valori consentiti:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Impostare le variabili di ambiente predefinite dell'account di archiviazione di Azure
È possibile avere più account di archiviazione nella sottoscrizione di Azure. tooselect uno di questi comandi toouse per tutti gli archivi successive, è possibile impostare queste variabili di ambiente:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Un altro modo tooset un account di archiviazione predefinito consiste nell'utilizzare una stringa di connessione. Innanzitutto, ottenere la stringa di connessione hello con hello `show-connection-string` comando:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Quindi hello copia stringa di connessione di output e impostare hello `AZURE_STORAGE_CONNECTION_STRING` variabile di ambiente (potrebbe essere necessario tooenclose stringa di connessione hello racchiuso tra virgolette):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Tutti gli esempi di hello le sezioni seguenti di questo articolo si presuppongono di aver impostato hello `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` le variabili di ambiente.
>

## <a name="create-and-manage-blobs"></a>Creare e gestire gli account di accesso
Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS. Questa sezione presuppone la conoscenza dei concetti relativi al servizio di archiviazione BLOB di Azure. Per informazioni dettagliate, vedere [Introduzione all'archiviazione BLOB di Azure con .NET](storage-dotnet-how-to-use-blobs.md) e [Concetti relativi al servizio BLOB](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Creare un contenitore
Ogni BLOB nell'archiviazione di Azure deve risiedere in un contenitore. È possibile creare un contenitore utilizzando hello `az storage container create` comando:

```azurecli
az storage container create --name <container_name>
```

È possibile impostare uno dei tre livelli di accesso in lettura per un nuovo contenitore specificando hello facoltativo `--public-access` argomento:

* `off`(impostazione predefinita): dati del contenitore sono privato toohello proprietario dell'account.
* `blob`: Accesso in lettura pubblico per i BLOB.
* `container`: Lettura ed elenco accesso toohello intero contenitore pubblico.

Per ulteriori informazioni, vedere [gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Caricare un contenitore di blob tooa
Archiviazione BLOB di Azure supporta BLOB in blocchi, BLOB di accodamento e BLOB di pagine. Caricamento BLOB tooa contenitore usando hello `blob upload` comando:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Per impostazione predefinita, hello `blob upload` comando Carica BLOB toopage di file VHD o BLOB in blocchi in caso contrario. toospecify un altro tipo quando si carica un blob, è possibile usare hello `--type` argomento, ovvero i valori consentito sono `append`, `block`, e `page`.

 Per ulteriori informazioni sui tipi di blob diversi hello, vedere [informazioni sui BLOB in blocchi, BLOB di accodamento e BLOB di pagine](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Scaricare un BLOB da un contenitore
Questo esempio viene illustrato come toodownload un blob da un contenitore:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore

Elencare i BLOB hello in un contenitore con hello [elenco blob di archiviazione az](/cli/azure/storage/blob#list) comando.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Copiare i BLOB
È possibile copiare i BLOB tra aree e account di archiviazione in modo asincrono.

Hello esempio seguente viene illustrato come toocopy BLOB da un archivio account tooanother. È necessario creare un contenitore nell'account di archiviazione di origine hello, specificando l'accesso in lettura pubblico per il BLOB. Successivamente, si carica un contenitore toohello file e infine copia hello blob dal contenitore in un contenitore nell'account di archiviazione di destinazione hello.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

In hello esempio precedente, il contenitore di destinazione hello deve esistere già nell'account di archiviazione di destinazione hello per toosucceed operazione di copia hello. Inoltre, i blob origine hello specificato in hello `--source-uri` argomento deve includere un token di firma di accesso condiviso oppure essere accessibile pubblicamente, come nel seguente esempio.

### <a name="delete-a-blob"></a>Eliminare un BLOB
toodelete un blob, utilizzare hello `blob delete` comando:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Creare e gestire condivisioni di file
Archiviazione di File di Azure offre archiviazione condivisa per le applicazioni mediante protocollo Server Message Block (SMB) hello. Macchine virtuali di Microsoft Azure e servizi cloud, nonché applicazioni locali, possono condividere i dati di file tra condivisioni montate. È possibile gestire condivisioni file e dati di file tramite hello CLI di Azure. Per ulteriori informazioni sull'archiviazione di File di Azure, vedere [Introduzione all'archiviazione di File di Azure in Windows](storage-dotnet-how-to-use-files.md) o [come archiviazione di File di Azure con Linux toouse](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Creare una condivisione file
Una condivisione di archiviazione file è una condivisione file SMB di Azure. Tutte le directory e i file devono essere creati in una condivisione padre. Un account può contenere un numero illimitato di condivisioni e una condivisione può archiviare un numero illimitato di file, i limiti di capacità toohello hello dell'account di archiviazione. esempio Hello crea una condivisione file denominata **myshare**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Creare una directory
Una directory fornisce una struttura gerarchica in una condivisione di file di Azure. esempio Hello crea una directory denominata **myDir** nella condivisione di file hello.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Un percorso di directory può includere più livelli, ad esempio **dir1/dir2**. Tuttavia, prima di creare una sottodirectory, è necessario assicurarsi che tutte le directory padre esistano. Ad esempio, per il percorso **dir1/dir2**, è necessario creare prima la directory **dir1** e poi la directory **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Caricare una condivisione di file locale tooa
esempio Hello carica un file da **~/temp/samplefile.txt** tooroot di hello **myshare** condivisione file. Hello `--source` argomento specifica tooupload file locale esistente hello.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Come per la creazione della directory, è possibile specificare un percorso di directory all'interno di hello condivisione tooupload hello tooan esistente directory del file nella condivisione di hello:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Un file nella condivisione di hello può essere backup too1 TB nella dimensione.

### <a name="list-hello-files-in-a-share"></a>Elencare i file hello in una condivisione
È possibile elencare i file e directory in una condivisione con hello `az storage file list` comando:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Copiare i file      
È possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa. Ad esempio, una directory tooa del file in una condivisione diversa toocopy:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Passaggi successivi
Ecco alcune risorse aggiuntive per ottenere ulteriori informazioni sull'utilizzo di hello CLI di Azure 2.0.

* [Introduzione all'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Riferimento ai comandi dell'interfaccia della riga di comando di Azure 2.0](/cli/azure)
* [Interfaccia della riga di comando di Azure 2.0 su GitHub](https://github.com/Azure/azure-cli)
