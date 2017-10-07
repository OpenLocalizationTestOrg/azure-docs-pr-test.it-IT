---
title: aaaHow toouse l'archiviazione delle code da Python | Documenti Microsoft
description: Informazioni come toouse hello servizio di Accodamento di Azure da toocreate Python ed eliminare le code e inserire, ottenere ed eliminare messaggi.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a>Come toouse l'archiviazione delle code da Python
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello servizio di archiviazione code di Azure. esempi di Hello sono scritti in Python e utilizzare hello [Microsoft Azure Storage SDK per Python]. Hello scenari trattati includono **inserimento**, **visualizzazione**, **recupero**, e **eliminazione** coda di messaggi, nonché  **Creazione ed eliminazione di code**. Per ulteriori informazioni sulle code, vedere sezione toohello [passaggi successivi].

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a>Procedura: creare una coda
Hello **QueueService** oggetto consente di lavorare con le code. Hello codice seguente viene creata una **QueueService** oggetto. Aggiungere il seguente hello superiore hello di qualsiasi file Python in cui si desidera tooprogrammatically accesso di archiviazione di Azure:

```python
from azure.storage.queue import QueueService
```

Hello codice seguente viene creata una **QueueService** oggetto utilizzando hello chiave account di archiviazione nome e all'account. Sostituire 'myaccount' e 'mykey' con l'account e la chiave da usare.

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Procedura: inserire un messaggio in una coda
un messaggio in una coda, utilizzare hello tooinsert **inserire\_messaggio** per creare un nuovo messaggio e aggiungerlo toohello coda.

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a>Procedura: Leggere hello messaggio successivo
È possibile anche visualizzare il messaggio hello nella parte anteriore hello di una coda senza rimuoverlo dalla coda hello dal chiamante hello **peek\_messaggi** metodo. Per impostazione predefinita, **peek\_messages** visualizza un singolo messaggio.

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a>Procedura: Rimuovere messaggi dalla coda
Il codice consente di rimuovere un messaggio da una coda in due passaggi. Quando si chiama **ottenere\_messaggi**, si messaggio hello successivo in una coda per impostazione predefinita. Un messaggio restituito da **ottenere\_messaggi** diventa invisibile tooany altro codice la lettura dei messaggi dalla coda. Per impostazione predefinita, il messaggio rimane invisibile per 30 secondi. toofinish messaggio hello rimozione dalla coda di hello, è necessario chiamare anche **eliminare\_messaggio**. Questo processo in due passaggi della rimozione di un messaggio garantisce che quando il codice ha esito negativo tooprocess un messaggio a causa di un errore hardware o software, un'altra istanza del codice può ottenere lo stesso messaggio e riprovare. Il codice chiama **eliminare\_messaggio** subito dopo il messaggio hello è stato elaborato.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

È possibile personalizzare il recupero di messaggi da una coda in due modi.
In primo luogo, è possibile ottenere un batch di messaggi (in alto too32). In secondo luogo, è possibile impostare un timeout di invisibilità superiori o inferiori, consentendo al codice più o meno toofully ora elaborare ogni messaggio. codice Hello seguente viene utilizzata la **ottenere\_messaggi** messaggi tooget 16 metodo in un'unica chiamata. Quindi, ogni messaggio viene elaborato con un ciclo for. Imposta inoltre il timeout di invisibilità hello a cinque minuti per ogni messaggio.

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Procedura: Modificare il contenuto di hello di un messaggio in coda
È possibile modificare il contenuto di hello di un messaggio sul posto nella coda di hello. Se il messaggio rappresenta un'attività di lavoro, è possibile utilizzare questo tooupdate funzionalità lo stato dell'attività di lavoro hello. codice Hello riportato di seguito utilizza hello **aggiornare\_messaggio** metodo tooupdate un messaggio. timeout di visibilità Hello è impostato too0, vale a dire viene immediatamente visualizzato il messaggio e contenuto hello viene aggiornato.

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a>Procedura: Recuperare hello lunghezza coda
È possibile ottenere una stima del numero di hello dei messaggi in una coda. Il **ottenere\_coda\_metadati** metodo richiede i metadati della coda del servizio tooreturn sulla coda hello hello e hello **approximate_message_count**. risultato Hello è solo approssimativo perché i messaggi possono essere aggiunti o rimossi dopo che il servizio di Accodamento risponde tooyour richiesta.

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a>Procedura: eliminare una coda
toodelete una coda e tutti i messaggi hello in esso contenuti, chiamare il **eliminare\_coda** metodo.

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione delle code, seguire questi ulteriori toolearn di collegamenti.

* [Centro per sviluppatori di Python](/develop/python/)
* [API REST dei servizi di archiviazione di Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog del team di Archiviazione di Azure]
* [Microsoft Azure Storage SDK per Python]

[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK per Python]: https://github.com/Azure/azure-storage-python