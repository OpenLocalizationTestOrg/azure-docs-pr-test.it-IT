---
title: aaaHow toouse Blob archiviazione (oggetto) da Ruby | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>Come toouse archiviazione Blob da Ruby
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

Questa guida viene illustrato come tooperform scenari comuni di utilizzo dell'archiviazione Blob. esempi di Hello vengono scritti utilizzando hello API Ruby. Hello scenari trattati includono **caricamento, visualizzazione di elenchi, download,** e **eliminazione** BLOB.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Creare un'applicazione Ruby
Creare un'applicazione Ruby. Per istruzioni, vedere l'articolo relativo all'[applicazione Web Ruby on Rails in una VM di Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurare l'archiviazione di tooaccess di applicazione
toouse archiviazione di Azure, è necessario toodownload e utilizzare hello Ruby pacchetto di azure, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain RubyGems
1. Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Digitare "indicatore installa azure" dipendenze e l'indicatore di hello comando finestra tooinstall hello.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Utilizzando un editor di testo, aggiungere hello toohello cima hello Ruby file in cui si intende toouse archiviazione seguente:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di Archiviazione di Azure
modulo Hello azure verrà lette le variabili di ambiente hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_ACCESS_KEY** per le informazioni richieste tooconnect tooyour account di archiviazione Azure. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello prima di utilizzare **Azure::Blob::BlobService** con hello seguente codice:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain questi valori da un classico o Gestione risorse di archiviazione di account nel portale di Azure hello:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Passare l'account di archiviazione toohello da toouse.
3. Nel pannello delle impostazioni hello in hello destra, fare clic su **chiavi di accesso**.
4. Nel pannello chiavi accesso hello che viene visualizzato, si noterà la chiave di accesso hello 1 e 2 di chiave di accesso. È possibile usare una di queste indifferentemente.
5. Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.

## <a name="create-a-container"></a>Creare un contenitore
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Hello **Azure::Blob::BlobService** oggetto consente di collaborare con i contenitori e BLOB. toocreate un contenitore, utilizzare hello **creare\_container()** metodo.

Hello esempio di codice seguente crea un contenitore o Visualizza errore hello eventuale.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Se si desidera file hello toomake nel contenitore hello pubblico, è possibile impostare le autorizzazioni del contenitore hello.

È possibile modificare solo hello <strong>creare\_container()</strong> chiamata toopass hello **: pubblica\_accesso\_livello** opzione:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

I valori validi per hello **: pubblica\_accesso\_livello** opzione sono:

* **blob:** specifica l'accesso in lettura pubblico per i BLOB. I dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili. I client non è possibile enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima.
* **container:** specifica l'accesso in lettura pubblico completo per i dati di contenitori e BLOB. I client possono enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.

In alternativa, è possibile modificare il livello di accesso pubblico hello di un contenitore utilizzando **impostare\_contenitore\_acl()** a livello di metodo toospecify hello accesso pubblico.

Hello modifiche hello livello di accesso pubblico troppo di esempio di codice seguente**contenitore**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
blob tooa contenuto tooupload, utilizzare hello **creare\_blocco\_blob()** blob hello toocreate di metodo, utilizzare un file o stringa come contenuto di hello del blob hello.

esempio di codice Hello Carica file hello **test.png** come un nuovo blob denominato "image-" blob nel contenitore hello.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
utilizzare contenitori hello toolist **list_containers()** metodo.
toolist hello BLOB all'interno di un contenitore, usare **elenco\_blobs()** metodo.

Restituisce gli URL di hello di tutti i BLOB hello in tutti i contenitori di hello per conto di hello.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Scaricare BLOB
BLOB toodownload, utilizzare hello **ottenere\_blob()** contenuto hello tooretrieve di metodo.

Hello esempio di codice seguente viene illustrato come utilizzare **ottenere\_blob()** toodownload contenuto di "immagine blob" hello e scriverlo tooa file locale.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Eliminare un BLOB
Infine, toodelete un blob, utilizzare hello **eliminare\_blob()** metodo. Hello esempio di codice riportato di seguito viene illustrato come toodelete un blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Passaggi successivi
toolearn sulle attività di archiviazione più complesse, vedere i collegamenti seguenti:

* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Azure SDK per Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub
* [Trasferimento dati con l'utilità della riga di comando di AzCopy hello](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

