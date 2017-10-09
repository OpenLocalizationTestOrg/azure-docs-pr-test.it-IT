---
title: aaaMove tooand di dati dall'archiviazione Blob di Azure usando Python | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure Usa Python
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Spostare dati tooand dall'archiviazione Blob di Azure Usa Python
In questo argomento viene descritto come toolist, caricare e scaricare BLOB utilizzando hello API Python. Con hello API Python fornito in Azure SDK, è possibile:

* Creare un contenitore
* Caricare un BLOB in un contenitore
* Scaricare BLOB
* Elenco di BLOB hello in un contenitore
* Eliminare un BLOB

Per ulteriori informazioni sull'utilizzo di hello Python API, vedere [come tooUse hello servizio di archiviazione Blob da Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Se si utilizza macchina virtuale che è stato configurato con gli script hello disponibili in [macchine virtuali di analisi scientifica dei dati in Azure](machine-learning-data-science-virtual-machines.md), quindi AzCopy è già installata nella macchina virtuale hello.
> 
> [!NOTE]
> Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questo documento si presuppone la presenza di una sottoscrizione di Azure, un account di archiviazione e chiave di archiviazione per l'account corrispondente hello. Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.

* tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Caricare dati tooBlob
Aggiungere hello seguente frammento di codice superiore hello del codice Python in cui si desidera tooprogrammatically accesso di archiviazione di Azure:

    from azure.storage.blob import BlobService

Hello **BlobService** oggetto consente di collaborare con i contenitori e BLOB. Hello di codice seguente crea un oggetto di BlobService tramite hello archiviazione nome account e la chiave dell'account. Sostituire nome e chiave dell'account con la chiave e l'account effettivi.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Utilizzare hello blob tooa di metodi tooupload dati seguenti:

1. inserire\_blocco\_blob\_da\_percorso (carica il contenuto di hello di un file dal percorso specificato hello)
2. inserire\_block_blob\_da\_file (carica il contenuto di hello dal flusso file già aperto)
3. put\_block\_blob\_from\_bytes (consente di caricare una matrice di byte)
4. inserire\_blocco\_blob\_da\_testo (Carica hello specificato il valore di testo utilizzando hello specificato codifica)

Hello seguente codice di esempio carica un contenitore di tooa file locale:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello codice di esempio seguente consente di caricare tutti i file hello (escluse le directory) in un archivio tooblob directory locale:

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Download dei dati dal BLOB
Utilizzare hello seguente dati toodownload metodi da un blob:

1. get\_blob\_to\_path
2. get\_blob\_to\_file
3. get\_blob\_to\_bytes
4. get\_blob\_to\_text

Questi metodi che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.

Hello codice di esempio seguente consente di scaricare contenuto hello di un blob in un file locale tooa di contenitore:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Hello codice di esempio seguente Scarica tutti i BLOB da un contenitore. Usa elenco\_BLOB elenco hello tooget di BLOB disponibili nel contenitore hello e li scarica tooa directory locale.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
