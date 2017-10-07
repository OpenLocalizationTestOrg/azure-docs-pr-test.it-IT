---
title: aaaHow toouse archiviazione tabelle di Azure da Ruby | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a>Come toouse archiviazione tabelle di Azure da Ruby
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Panoramica
Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello del servizio tabelle di Azure. esempi di Hello vengono scritti utilizzando hello API Ruby. Hello scenari trattati includono **creazione e l'eliminazione di una tabella, inserimento e una query sulle entità in una tabella**.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Creare un'applicazione Ruby
Per istruzioni toocreate un'applicazione Ruby, vedere [Ruby in un'applicazione Web di guide in una macchina virtuale Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurare l'archiviazione di tooaccess di applicazione
toouse archiviazione di Azure, è necessario toodownload e utilizzare hello Ruby pacchetto azure che include un set di librerie di praticità che comunicano con servizi di archiviazione REST hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain RubyGems
1. Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Tipo **azure installazione indicatore** indicatore di hello comando finestra tooinstall hello e delle dipendenze.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Utilizzare un editor di testo, aggiungere hello toohello cima hello Ruby file in cui si intende toouse archiviazione seguente:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
Hello modulo azure verrà lette le variabili di ambiente hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_accesso\_chiave**per le informazioni necessarie tooconnect tooyour account di archiviazione Azure. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello prima di utilizzare **Azure::TableService** con hello seguente codice:

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

## <a name="create-a-table"></a>Creare una tabella
Hello **Azure::TableService** oggetto consente di utilizzare tabelle ed entità. toocreate una tabella, utilizzare hello **creare\_table()** metodo. esempio Hello crea una tabella o stampa hello errore eventuale.

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a>Aggiungere una tabella tooa entità
tooadd un'entità, creare innanzitutto un oggetto hash che definisce le proprietà dell'entità. Si noti che per ogni entità è necessario specificare un oggetto **PartitionKey** e un oggetto **RowKey**. Questi sono identificatori univoci delle entità di hello e sono valori che è possono eseguire una query più velocemente rispetto alle altre proprietà. Archiviazione di Azure Usa **PartitionKey** tooautomatically distribuire entità della tabella hello su molti nodi di archiviazione. Le entità con hello stesso **PartitionKey** vengono archiviati in hello stesso nodo. Hello **RowKey** hello ID univoco dell'entità hello all'interno della partizione hello a cui appartiene.

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a>Aggiornare un'entità
Esistono più tooupdate disponibili di metodi un'entità esistente:

* **update\_entity():** aggiorna un'entità esistente sostituendola.
* **unione\_entity():** aggiorna un'entità esistente unendo nuovi valori della proprietà di entità esistente hello.
* **insert\_or\_merge\_entity():** aggiorna un'entità esistente sostituendola. Se non esiste alcuna entità, ne verrà inserita una nuova:
* **Inserisci\_o\_sostituire\_entity():** aggiorna un'entità esistente unendo nuovi valori della proprietà di entità esistente hello. Se non esiste alcuna entità, ne verrà inserita una nuova.

Hello esempio seguente viene illustrato l'aggiornamento di un'entità mediante **aggiornare\_entity()**:

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

Con **aggiornare\_entity()** e **unione\_entity()**, se non esiste entità hello che si sta aggiornando l'operazione di aggiornamento hello avrà esito negativo. Pertanto se si desidera toostore un'entità indipendentemente dal fatto se esiste già, è invece necessario utilizzare **inserire\_o\_sostituire\_entity()** o **inserire\_o \_unione\_entity()**.

## <a name="work-with-groups-of-entities"></a>Usare i gruppi di entità
A volte risulta più toosubmit senso più operazioni contemporaneamente in un batch tooensure atomica elaborazione dal server hello. tooaccomplish, creare innanzitutto un **Batch** oggetto, quindi utilizzare hello **eseguire\_batch()** metodo **TableService**. Hello esempio seguente viene illustrato l'invio di due entità con RowKey 2 e 3 in un batch. Si noti che solo funziona per le entità con hello PartitionKey stesso.

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a>Eseguire una query su un'entità
un'entità in una tabella, utilizzare hello tooquery **ottenere\_entity()** (metodo), passando il nome di tabella hello **PartitionKey** e **RowKey**.

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a>Eseguire query su un set di entità
tooquery un set di entità in una tabella, creare un oggetto hash di query e utilizzare hello **query\_entities()** metodo. Hello esempio seguente viene illustrato come ottenere tutte le entità di hello con hello stesso **PartitionKey**:

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> Se il set di risultati hello è troppo grande per tooreturn una singola query, un token di continuazione verrà restituito che è possibile utilizzare le pagine successive tooretrieve.
>
>

## <a name="query-a-subset-of-entity-properties"></a>Eseguire query su un subset di proprietà di entità
Una tabella di tooa query è possibile recuperare solo alcune proprietà di un'entità. Questa tecnica, denominata "proiezione", consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni. Clausola select hello di utilizzo e i nomi di hello passaggio di hello proprietà toobring su toohello client.

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a>Eliminare un'entità
toodelete un'entità, utilizzare hello **eliminare\_entity()** metodo. È necessario toopass nel nome hello della tabella hello che contiene entità hello, hello PartitionKey e RowKey di hello entità.

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a>Eliminare una tabella
toodelete una tabella, utilizzare hello **eliminare\_table()** (metodo) e passare il nome di hello di hello tabella desiderata toodelete.

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a>Passaggi successivi

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.
* [Azure SDK per Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub

