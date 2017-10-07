---
title: aaaHow toouse (archiviazione di oggetti) di archiviazione Blob di Azure da Python | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Come toouse archiviazione Blob di Azure da Python
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

In questo articolo viene illustrato come tooperform scenari comuni di utilizzo dell'archiviazione Blob. esempi di Hello sono scritti in Python e utilizzare hello [Microsoft Azure Storage SDK per Python]. scenari di Hello trattati includono il caricamento, elenco, il download e l'eliminazione dei BLOB.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Creare un contenitore
In base al tipo di hello del blob desideri toouse, creare un **BlockBlobService**, **AppendBlobService**, o **PageBlobService** oggetto. codice Hello seguente viene utilizzato un **BlockBlobService** oggetto. Aggiungere il seguente hello superiore hello di qualsiasi file Python in cui si desidera tooprogrammatically accesso Azure archivio Blob in blocchi.

```python
from azure.storage.blob import BlockBlobService
```

Hello codice seguente viene creata una **BlockBlobService** oggetto utilizzando hello chiave account di archiviazione nome e all'account.  Sostituire 'myaccount' e 'mykey' con l'account e la chiave da usare.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Nell'esempio di codice seguente di hello, è possibile utilizzare un **BlockBlobService** toocreate hello contenitore di oggetti di se non esiste.

```python
block_blob_service.create_container('mycontainer')
```

Per impostazione predefinita, hello nuovo contenitore è privato, è necessario specificare la chiave di accesso di archiviazione (come descritto in precedenza) BLOB toodownload da questo contenitore. Se si desidera BLOB hello toomake all'interno di hello contenitore disponibili tooeveryone, è possibile creare il contenitore di hello e passare il livello di accesso pubblico hello utilizzando il seguente codice hello.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

In alternativa, è possibile modificare un contenitore dopo aver creato tramite hello seguente codice.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Dopo questa modifica, chiunque in Internet hello può visualizzare i BLOB in un contenitore pubblico, ma solo è possibile modificarli o eliminarli.

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
toocreate un blob in blocchi e caricare i dati, utilizzare hello **creare\_blob\_da\_percorso**, **creare\_blob\_da\_flusso**, **creare\_blob\_da\_byte** o **creare\_blob\_da\_testo** metodi. Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.

**creare\_blob\_da\_percorso** caricamenti hello contenuto di un file dal percorso specificato hello, e **creare\_blob\_da\_flusso** caricamenti hello contenuto dal flusso file già aperto. **creare\_blob\_da\_byte** carica una matrice di byte, e **creare\_blob\_da\_testo** carica hello specificato il valore di testo utilizzando hello specificato codifica (impostazioni predefinite tooUTF-8).

esempio Hello carica il contenuto di hello di hello **sunset.png** file hello **myblob** blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, usare hello **elenco\_BLOB** metodo. Questo metodo restituisce un generatore. il codice seguente Hello restituisce hello **nome** di ogni blob in una console toohello contenitore.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Scaricare BLOB
toodownload dei dati da un blob, utilizzare **ottenere\_blob\_a\_percorso**, **ottenere\_blob\_a\_flusso**, **ottenere\_blob\_a\_byte**, o **ottenere\_blob\_a\_testo**. Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.

Hello seguente viene illustrato l'utilizzo **ottenere\_blob\_a\_percorso** contenuto hello toodownload di hello **myblob** blob e di archiviarlo toohello **out sunset.png** file.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Eliminare un BLOB
Chiamare infine toodelete un blob, **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Scrittura tooan aggiungere blob
Un blob di accodamento è ottimizzato per le operazioni di accodamento, ad esempio la registrazione. Come un blob in blocchi, un blob di aggiunta è costituito da blocchi, ma quando si aggiunge un nuovo blob in blocchi tooan accodamento, è sempre aggiunte toohello fine del blob hello. È possibile aggiornare o eliminare un blocco esistente in un blob di Accodamento. ID blocco Hello per un blob di aggiunta non vengono esposte come se fossero per un blob in blocchi.

Ogni blocco di un blob di aggiunta può avere dimensioni diverse, backup tooa massimo 4 MB, e un blob di aggiunta può includere un massimo di 50.000 blocchi. dimensione massima di Hello di un blob di aggiunta è pertanto leggermente superiore a 195 GB (4 MB X 50.000 blocchi).

esempio Hello seguente crea un nuovo blob di aggiunta e accoda tooit alcuni dati, simulazione di un'operazione di registrazione semplice.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello dell'archiviazione Blob, seguire questi ulteriori toolearn di collegamenti.

* [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/)
* [API REST dei servizi di archiviazione di Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog del team di Archiviazione di Azure]
* [Microsoft Azure Storage SDK per Python]

[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK per Python]: https://github.com/Azure/azure-storage-python
