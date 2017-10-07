---
title: aaaSend eventi tooAzure hub eventi Usa Java | Documenti Microsoft
description: Iniziare l'invio a hub tooEvent Usa Java
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a>Inviare gli eventi di hub di eventi tooAzure Usa Java

## <a name="introduction"></a>Introduzione
Hub eventi è un sistema di inserimento estremamente scalabile in grado di milioni di eventi al secondo, abilitazione tooprocess un'applicazione di inserimento e analizzare hello enormi quantità di dati generati per i dispositivi connessi e le applicazioni. Dopo la raccolta in un hub eventi, è possibile trasformare e archiviare i dati usando qualsiasi provider di analisi in tempo reale o un cluster di archiviazione.

Per ulteriori informazioni, vedere hello [Panoramica di hub eventi][Event Hubs overview].

Questa esercitazione viene illustrato come hub di eventi tooan eventi toosend tramite un'applicazione console in Java. eventi tooreceive utilizza hello Host processore di eventi di linguaggio libreria, vedere [questo articolo](event-hubs-java-get-started-receive-eph.md), oppure fare clic su lingua ricevente hello appropriata nella tabella a sinistra di hello del contenuto.

In ordine toocomplete questa esercitazione, sarà necessario hello seguenti:

* Ambiente di sviluppo in Java. Per questa esercitazione si presuppone l'uso di [Eclipse](https://www.eclipse.org/).
* Un account Azure attivo. <br/>Se non si ha un account, è possibile creare un account gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">versione di valutazione gratuita di Azure</a>.

## <a name="send-messages-tooevent-hubs"></a>Invio di messaggi tooEvent hub
Hello Java libreria client per gli hub eventi è disponibile per l'utilizzo nei progetti Maven da hello [Repository centrale Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). È possibile fare riferimento a questa raccolta usando hello segue la dichiarazione di dipendenza all'interno del file di progetto di Maven:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Per diversi tipi di ambienti di compilazione, è possibile ottenere in modo esplicito i file JAR hello più recenti rilasciato da hello [Repository centrale Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Per un server di pubblicazione di un evento semplice, importare hello *com.microsoft.azure.eventhubs* pacchetto per le classi del client hello hub eventi e hello *com.microsoft.azure.servicebus* dal pacchetto per le classi di utilità ad come eccezioni più comuni che vengono condivisi con client di messaggistica di hello Azure Service Bus. 

Per hello nel seguente esempio, creare un nuovo progetto di Maven per un'applicazione console/shell nell'ambiente di sviluppo preferita di Java. Nome classe hello `Send`.     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

Sostituire hello dello spazio dei nomi e hub nomi di evento con i valori hello utilizzati durante la creazione di hub eventi hello.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

A questo punto, creare un evento singolare trasformando una stringa nel relativo corrispettivo con codifica UTF-8. Quindi, creare una nuova istanza di hub eventi client dalla stringa di connessione hello e inviare il messaggio hello.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Ricezione di eventi utilizzando hello EventProcessorHost](event-hubs-java-get-started-receive-eph.md)
* [Panoramica di Hub eventi][Event Hubs overview]
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md