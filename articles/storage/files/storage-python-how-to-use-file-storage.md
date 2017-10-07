---
title: aaaDevelop per l'archiviazione di File di Azure con Python | Documenti Microsoft
description: Informazioni su come toodevelop Python applicazioni e servizi che utilizzano i File di Azure storage toostore dati dei file.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 2adc5aac2765b98a8022ab1f706c1fcdbca1b43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Eseguire lo sviluppo per Archiviazione file di Azure con Python
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
Questa esercitazione verrà illustrato l'utilizzo di Python toodevelop applicazioni o servizi che utilizzano i File di Azure storage toostore file dati di base di hello. In questa esercitazione verrà creata una semplice applicazione console e Mostra come tooperform azioni di base con l'archiviazione di Python e File di Azure:

* Creare condivisioni file di Azure
* Creare directory
* Enumerare file e directory in una condivisione file di Azure
* Caricare, scaricare ed eliminare un file

> [!Note]  
> Poiché la memorizzazione dei File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a condivisione di File di Azure hello utilizzando le funzioni e classi dei / o Python standard hello. In questo articolo descrive come le applicazioni che usano toowrite hello Python Azure Storage SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurare l'archiviazione di File di Azure di toouse applicazione
Aggiungere il seguente hello superiore hello di qualsiasi file di origine di Python in cui si desidera tooprogrammatically accesso di archiviazione di Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Impostare un tooAzure connessione archiviazione File 
Hello `FileService` oggetto consente di lavorare con file, directory e condivisioni. Hello codice seguente viene creata una `FileService` oggetto utilizzando hello chiave account di archiviazione nome e all'account. Sostituire `<myaccount>` e `<mykey>` con il nome e la chiave dell'account.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Creare una condivisione file di Azure
Nell'esempio di codice seguente di hello, è possibile utilizzare un `FileService` condivisione di hello toocreate oggetto se non esiste.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Creare una directory
È anche possibile organizzare archiviazione inserendo i file all'interno di sottodirectory, anziché tutti gli elementi nella directory radice hello. Archiviazione di File di Azure consente toocreate come consentire molte directory come l'account. codice Hello seguente verrà creata una sottodirectory denominata **sampledir** nella directory radice hello.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerare file e directory in una condivisione file di Azure
toolist hello file e directory in una condivisione, utilizzare hello **elenco\_directory\_e\_file** metodo. Questo metodo restituisce un generatore. il codice seguente Hello restituisce hello **nome** di ogni file e directory in una console toohello condivisione.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Caricare un file 
File di Azure condivisione contiene in hello molto meno, una directory radice in cui i file possono trovarsi. In questa sezione si apprenderà come tooupload un file dall'archiviazione locale su hello radice della directory di una condivisione.

toocreate un file e caricare i dati, utilizzare hello `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` o `create_file_from_text` metodi. Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.

`create_file_from_path`caricamenti hello contenuto di un file dal percorso specificato hello, e `create_file_from_stream` caricamenti hello contenuto dal flusso file già aperto. `create_file_from_bytes`Carica una matrice di byte, e `create_file_from_text` caricamenti hello specificato il valore di testo utilizzando hello codifica (impostazioni predefinite tooUTF-8).

esempio Hello carica il contenuto di hello di hello **sunset.png** file hello **myfile** file.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Scaricare un file
toodownload dati da un file, utilizzare `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, o `get_file_to_text`. Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.

Hello seguente viene illustrato l'utilizzo `get_file_to_path` contenuto hello toodownload di hello **myfile** file e archiviarlo toohello **out sunset.png** file.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Eliminare un file
Chiamare infine toodelete un file, `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso come toomanipulate archiviazione di File di Azure con Python, seguire questi ulteriori toolearn di collegamenti.

* [Centro per sviluppatori di Python](/develop/python/)
* [API REST dei servizi di archiviazione di Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Microsoft Azure Storage SDK per Python](https://github.com/Azure/azure-storage-python)