---
title: aaaHow toouse archiviazione delle code da Ruby | Documenti Microsoft
description: Informazioni su come toouse hello Azure coda servizio toocreate e le code di delete e insert, ottenere ed eliminare i messaggi. Gli esempi sono scritti in Ruby.
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a>Come l'archiviazione delle code da Ruby toouse
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello del servizio di archiviazione di Accodamento di Microsoft Azure. esempi di Hello vengono scritti utilizzando hello Ruby API di Azure.
Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Creare un'applicazione Ruby
Creare un'applicazione Ruby. Per istruzioni, vedere l'articolo relativo all' [applicazione Web Ruby on Rails in una macchina virtuale di Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).

## <a name="configure-your-application-tooaccess-storage"></a>Configurare l'applicazione tooAccess archiviazione
toouse archiviazione di Azure, è necessario toodownload e utilizzare hello Ruby pacchetto di azure, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Utilizzare un pacchetto di hello tooobtain RubyGems
1. Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).
2. Digitare "indicatore installa azure" dipendenze e l'indicatore di hello comando finestra tooinstall hello.

### <a name="import-hello-package"></a>Importa pacchetto di hello
Utilizzare un editor di testo, aggiungere hello toohello cima hello Ruby file in cui si intende toouse archiviazione seguente:

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
modulo Hello azure verrà lette le variabili di ambiente hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_ACCESS_KEY** per le informazioni richieste tooconnect tooyour account di archiviazione Azure. Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello prima di utilizzare **Azure::QueueService** con hello seguente codice:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

tooobtain questi valori da un classico o Gestione risorse di archiviazione di account nel portale di Azure hello:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Passare l'account di archiviazione toohello da toouse.
3. Nel pannello delle impostazioni hello in hello destra, fare clic su **chiavi di accesso**.
4. Nel pannello chiavi accesso hello che viene visualizzato, si noterà la chiave di accesso hello 1 e 2 di chiave di accesso. È possibile usare una di queste indifferentemente. 
5. Fare clic su hello Copia icona toocopy hello toohello chiave Appunti. 

tooobtain questi valori da un'archiviazione classico account nel portale di Azure classico hello:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Passare l'account di archiviazione toohello da toouse.
3. Fare clic su **GESTISCI CHIAVI di accesso** nella parte inferiore di hello del riquadro di spostamento hello.
4. Nella finestra di dialogo a comparsa hello, si noterà nome account di archiviazione hello, chiave di accesso primaria e chiave di accesso secondaria. Per la chiave di accesso, è possibile utilizzare hello primario o quello secondario hello. 
5. Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.

## <a name="how-to-create-a-queue"></a>Procedura: creare una coda
Hello codice seguente viene creata una **Azure::QueueService** oggetto, che consente di toowork con le code.

```ruby
azure_queue_service = Azure::QueueService.new
```

Hello utilizzare **create_queue()** toocreate metodo una coda con hello nome specificato.

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedura: inserire un messaggio in una coda
un messaggio in una coda, utilizzare hello tooinsert **create_message()** metodo toocreate un nuovo messaggio e aggiungerla toohello coda.

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a>Procedura: Leggere hello messaggio successivo
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peek\_messages()** metodo. Per impostazione predefinita, **peek\_messages()** visualizza un singolo messaggio. È inoltre possibile specificare il numero di messaggi desiderato toopeek.

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a>Procedura: Rimozione dalla coda hello messaggio successivo
È possibile rimuovere un messaggio da una coda in due passaggi.

1. Quando si chiama **elenco\_messages()**, si messaggio hello successivo in una coda per impostazione predefinita. È inoltre possibile specificare il numero di messaggi desiderato tooget. i messaggi restituiti da Hello **elenco\_messages()** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. Passare nel timeout di visibilità hello in secondi come parametro.
2. toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **delete_message()**.

Questo processo in due passaggi della rimozione di un messaggio assicura che quando il tooprocess ha esito negativo di codice un messaggio a causa di un errore toohardware o software, un'altra istanza del codice è possibile ottenere hello stesso messaggio e provare nuovamente. Il codice chiama **eliminare\_message()** subito dopo il messaggio hello è stato elaborato.

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedura: Modificare il contenuto di hello di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello. codice Hello riportato di seguito utilizza hello **update_message()** metodo tooupdate un messaggio. metodo Hello restituirà una tupla che contiene di ricezione pop del messaggio della coda di hello hello e un valore di tempo data UTC che rappresenta quando il messaggio hello sarà visibile nella coda di hello.

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a>Procedura: opzioni aggiuntive per rimuovere i messaggi dalla coda
È possibile personalizzare il recupero di messaggi da una coda in due modi.

1. È possibile recuperare un batch di messaggi.
2. È possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio.

esempio di codice seguente Hello utilizza hello **elenco\_messages()** messaggi tooget 15 metodo in un'unica chiamata. Quindi, ogni messaggio viene stampato ed eliminato. Imposta inoltre hello invisibilità timeout toofive in minuti per ogni messaggio.

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a>Procedura: Recuperare hello lunghezza coda
È possibile ottenere una stima del numero di hello di messaggi nella coda di hello. Hello **ottenere\_coda\_metadata()** metodo chiede hello coda conteggio approssimativo dei messaggi di servizio tooreturn hello e i metadati sulla coda hello.

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a>Procedura: eliminare una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, chiamata hello **eliminare\_Queue** metodo hello dell'oggetto di coda.

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* Visitare hello [blog del Team di archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Visitare hello [Azure SDK per Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository in GitHub

Per un confronto tra hello servizio di Accodamento Azure descritti in questo articolo e code di Azure Service Bus descritti in hello [come toouse code di Service Bus](/develop/ruby/how-to-guides/service-bus-queues/) articolo, vedere [code di Azure e code di Service Bus: confronto e Differenza](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)
