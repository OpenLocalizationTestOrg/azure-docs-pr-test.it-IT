---
title: Inviare eventi a Hub eventi di Azure usando Java | Microsoft Docs
description: Guida introduttiva all'invio a Hub di eventi con Java
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
ms.openlocfilehash: b31771001989e20b88bc8d7bca1afceb58ec197c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="4159f-103">Inviare eventi a Hub eventi di Azure usando Java</span><span class="sxs-lookup"><span data-stu-id="4159f-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="4159f-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="4159f-104">Introduction</span></span>
<span data-ttu-id="4159f-105">Hub eventi è un sistema di inserimento a scalabilità elevata, in grado di inserire milioni di eventi al secondo, che permette a un'applicazione di elaborare e analizzare le elevate quantità di dati prodotti dalle applicazioni e dai dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="4159f-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="4159f-106">Dopo la raccolta in un hub eventi, è possibile trasformare e archiviare i dati usando qualsiasi provider di analisi in tempo reale o un cluster di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4159f-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="4159f-107">Per altre informazioni, vedere [Panoramica di Hub eventi][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="4159f-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="4159f-108">Questa esercitazione illustra come inviare eventi a un hub eventi usando un'applicazione console in Java.</span><span class="sxs-lookup"><span data-stu-id="4159f-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="4159f-109">Per ricevere eventi usando la libreria host del processore di eventi di Java, vedere [questo articolo](event-hubs-java-get-started-receive-eph.md) o fare clic sul linguaggio di ricezione appropriato nel sommario a sinistra.</span><span class="sxs-lookup"><span data-stu-id="4159f-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="4159f-110">Per completare questa esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4159f-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="4159f-111">Ambiente di sviluppo in Java.</span><span class="sxs-lookup"><span data-stu-id="4159f-111">A Java development environment.</span></span> <span data-ttu-id="4159f-112">Per questa esercitazione si presuppone l'uso di [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="4159f-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="4159f-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4159f-113">An active Azure account.</span></span> <br/><span data-ttu-id="4159f-114">Se non si ha un account, è possibile creare un account gratuito in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="4159f-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="4159f-115">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="4159f-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="4159f-116">Inviare messaggi all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="4159f-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="4159f-117">La libreria client Java per Hub eventi è disponibile per l'uso in progetti Maven dal [repository centrale di Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="4159f-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="4159f-118">Per fare riferimento a questa libreria è possibile usare questa dichiarazione di dipendenza all'interno del file di progetto di Maven:</span><span class="sxs-lookup"><span data-stu-id="4159f-118">You can reference this library using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="4159f-119">Per diversi tipi di ambienti di compilazione è possibile ottenere in modo esplicito i file JAR rilasciati più recenti dal [repository centrale di Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="4159f-119">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="4159f-120">Per un autore di eventi semplice, importare il pacchetto *com.microsoft.azure.eventhubs* per le classi di client di hub eventi e il pacchetto *com.microsoft.azure.servicebus* per le classi di utilità, ad esempio eccezioni comuni condivise con il client di messaggistica del bus di servizio di Azure.</span><span class="sxs-lookup"><span data-stu-id="4159f-120">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="4159f-121">Per l'esempio seguente, creare prima un nuovo progetto Maven per un'applicazione console/shell nell'ambiente di sviluppo Java preferito.</span><span class="sxs-lookup"><span data-stu-id="4159f-121">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="4159f-122">Denominare la classe `Send`.</span><span class="sxs-lookup"><span data-stu-id="4159f-122">Name the class `Send`.</span></span>     

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

<span data-ttu-id="4159f-123">Sostituire lo spazio dei nomi e i nomi dell'hub eventi con i valori utilizzati durante la creazione dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="4159f-123">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="4159f-124">A questo punto, creare un evento singolare trasformando una stringa nel relativo corrispettivo con codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="4159f-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="4159f-125">Creare infine una nuova istanza del client di Hub eventi dalla stringa di connessione e inviare il messaggio.</span><span class="sxs-lookup"><span data-stu-id="4159f-125">Then, create a new Event Hubs client instance from the connection string and send the message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="4159f-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4159f-126">Next steps</span></span>
<span data-ttu-id="4159f-127">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4159f-127">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="4159f-128">[Receive events using the EventProcessorHost](event-hubs-java-get-started-receive-eph.md) (Ricevere eventi usando EventProcessorHost)</span><span class="sxs-lookup"><span data-stu-id="4159f-128">[Receive events using the EventProcessorHost](event-hubs-java-get-started-receive-eph.md)</span></span>
* <span data-ttu-id="4159f-129">[Panoramica di Hub eventi][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="4159f-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="4159f-130">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="4159f-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="4159f-131">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="4159f-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md