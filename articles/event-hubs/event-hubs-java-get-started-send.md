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
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="43e92-103">Inviare gli eventi di hub di eventi tooAzure Usa Java</span><span class="sxs-lookup"><span data-stu-id="43e92-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="43e92-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="43e92-104">Introduction</span></span>
<span data-ttu-id="43e92-105">Hub eventi è un sistema di inserimento estremamente scalabile in grado di milioni di eventi al secondo, abilitazione tooprocess un'applicazione di inserimento e analizzare hello enormi quantità di dati generati per i dispositivi connessi e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="43e92-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="43e92-106">Dopo la raccolta in un hub eventi, è possibile trasformare e archiviare i dati usando qualsiasi provider di analisi in tempo reale o un cluster di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="43e92-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="43e92-107">Per ulteriori informazioni, vedere hello [Panoramica di hub eventi][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="43e92-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="43e92-108">Questa esercitazione viene illustrato come hub di eventi tooan eventi toosend tramite un'applicazione console in Java.</span><span class="sxs-lookup"><span data-stu-id="43e92-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="43e92-109">eventi tooreceive utilizza hello Host processore di eventi di linguaggio libreria, vedere [questo articolo](event-hubs-java-get-started-receive-eph.md), oppure fare clic su lingua ricevente hello appropriata nella tabella a sinistra di hello del contenuto.</span><span class="sxs-lookup"><span data-stu-id="43e92-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="43e92-110">In ordine toocomplete questa esercitazione, sarà necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="43e92-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="43e92-111">Ambiente di sviluppo in Java.</span><span class="sxs-lookup"><span data-stu-id="43e92-111">A Java development environment.</span></span> <span data-ttu-id="43e92-112">Per questa esercitazione si presuppone l'uso di [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="43e92-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="43e92-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="43e92-113">An active Azure account.</span></span> <br/><span data-ttu-id="43e92-114">Se non si ha un account, è possibile creare un account gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="43e92-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="43e92-115">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="43e92-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="43e92-116">Invio di messaggi tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="43e92-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="43e92-117">Hello Java libreria client per gli hub eventi è disponibile per l'utilizzo nei progetti Maven da hello [Repository centrale Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="43e92-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="43e92-118">È possibile fare riferimento a questa raccolta usando hello segue la dichiarazione di dipendenza all'interno del file di progetto di Maven:</span><span class="sxs-lookup"><span data-stu-id="43e92-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="43e92-119">Per diversi tipi di ambienti di compilazione, è possibile ottenere in modo esplicito i file JAR hello più recenti rilasciato da hello [Repository centrale Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="43e92-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="43e92-120">Per un server di pubblicazione di un evento semplice, importare hello *com.microsoft.azure.eventhubs* pacchetto per le classi del client hello hub eventi e hello *com.microsoft.azure.servicebus* dal pacchetto per le classi di utilità ad come eccezioni più comuni che vengono condivisi con client di messaggistica di hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="43e92-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="43e92-121">Per hello nel seguente esempio, creare un nuovo progetto di Maven per un'applicazione console/shell nell'ambiente di sviluppo preferita di Java.</span><span class="sxs-lookup"><span data-stu-id="43e92-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="43e92-122">Nome classe hello `Send`.</span><span class="sxs-lookup"><span data-stu-id="43e92-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="43e92-123">Sostituire hello dello spazio dei nomi e hub nomi di evento con i valori hello utilizzati durante la creazione di hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="43e92-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="43e92-124">A questo punto, creare un evento singolare trasformando una stringa nel relativo corrispettivo con codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="43e92-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="43e92-125">Quindi, creare una nuova istanza di hub eventi client dalla stringa di connessione hello e inviare il messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="43e92-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="43e92-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43e92-126">Next steps</span></span>
<span data-ttu-id="43e92-127">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="43e92-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="43e92-128">Ricezione di eventi utilizzando hello EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="43e92-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="43e92-129">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="43e92-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="43e92-130">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="43e92-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="43e92-131">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="43e92-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md