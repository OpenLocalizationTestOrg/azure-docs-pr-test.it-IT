---
title: Inviare eventi a Hub eventi di Azure usando C | Microsoft Docs
description: Inviare eventi a Hub di eventi di Azure usando C
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a615ee39b6c3731cc7df366e9fabeed5219a71b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a><span data-ttu-id="62ea0-103">Inviare eventi a Hub di eventi di Azure usando C</span><span class="sxs-lookup"><span data-stu-id="62ea0-103">Send events to Azure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="62ea0-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="62ea0-104">Introduction</span></span>
<span data-ttu-id="62ea0-105">Hub eventi è un sistema di inserimento a scalabilità elevata, in grado di inserire milioni di eventi al secondo, che permette a un'applicazione di elaborare e analizzare le elevate quantità di dati prodotti dalle applicazioni e dai dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="62ea0-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="62ea0-106">Dopo la raccolta in un hub eventi, è possibile trasformare e archiviare i dati usando qualsiasi provider di analisi in tempo reale o un cluster di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="62ea0-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="62ea0-107">Per altre informazioni, vedere [Panoramica di Hub eventi][Panoramica di Hub eventi].</span><span class="sxs-lookup"><span data-stu-id="62ea0-107">For more information, please see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="62ea0-108">In questa esercitazione si apprenderà come inviare eventi a un hub eventi usando un'applicazione console in C. Per ricevere gli eventi, fare clic sulla lingua di destinazione appropriata nel sommario a sinistra.</span><span class="sxs-lookup"><span data-stu-id="62ea0-108">In this tutorial, you will learn how to send events to an event hub using a console application in C. To receive events, click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="62ea0-109">Per completare questa esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="62ea0-109">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="62ea0-110">Ambiente di sviluppo in C.</span><span class="sxs-lookup"><span data-stu-id="62ea0-110">A C development environment.</span></span> <span data-ttu-id="62ea0-111">Per questa esercitazione si presuppone l'uso di uno stack gcc in una VM Linux in Azure con Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="62ea0-111">For this tutorial, we will assume the gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="62ea0-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="62ea0-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="62ea0-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="62ea0-113">An active Azure account.</span></span> <span data-ttu-id="62ea0-114">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="62ea0-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="62ea0-115">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62ea0-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="62ea0-116">Inviare messaggi all'hub eventi</span><span class="sxs-lookup"><span data-stu-id="62ea0-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="62ea0-117">In questa sezione si scrive un'app C per inviare eventi all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="62ea0-117">In this section we write a C app to send events to your event hub.</span></span> <span data-ttu-id="62ea0-118">Il codice usa la libreria Proton AMQP dal [progetto Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="62ea0-118">The code uses the Proton AMQP library from the [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="62ea0-119">Il procedimento è simile a quello adottato per l'uso da C di code e argomenti del bus di servizio con AMQP, come illustrato [qui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="62ea0-119">This is analogous to using Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="62ea0-120">Per altre informazioni, vedere la [documentazione di Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="62ea0-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="62ea0-121">Dalla [pagina di Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) seguire le istruzioni per l'installazione di Qpid Proton a seconda dell'ambiente corrente.</span><span class="sxs-lookup"><span data-stu-id="62ea0-121">From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="62ea0-122">Per compilare la libreria Proton, installare i seguenti pacchetti:</span><span class="sxs-lookup"><span data-stu-id="62ea0-122">To compile the Proton library, install the following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="62ea0-123">Scaricare la [libreria Qpid Proton](http://qpid.apache.org/proton/index.html) e quindi estrarla, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="62ea0-123">Download the [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="62ea0-124">Creare una directory di compilazione, compilare e installare:</span><span class="sxs-lookup"><span data-stu-id="62ea0-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="62ea0-125">Nella directory di lavoro creare un nuovo file denominato **sender.c** con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="62ea0-125">In your work directory, create a new file called **sender.c** with the following code.</span></span> <span data-ttu-id="62ea0-126">Ricordare di sostituire i valori del nome dell'hub eventi e del nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="62ea0-126">Remember to substitute the value for your event hub name and namespace name.</span></span> <span data-ttu-id="62ea0-127">È anche necessario sostituire una versione codificata con URL della chiave per l'elemento **SendRule** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="62ea0-127">You must also substitute a URL-encoded version of the key for the **SendRule** created earlier.</span></span> <span data-ttu-id="62ea0-128">È possibile creare la versione codificata con URL [qui](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="62ea0-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C to stop the sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="62ea0-129">Compilare il file (si presuppone **gcc**):</span><span class="sxs-lookup"><span data-stu-id="62ea0-129">Compile the file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="62ea0-130">In questo codice viene usata una finestra in uscita pari a 1 per imporre un invio dei messaggi il più rapido possibile.</span><span class="sxs-lookup"><span data-stu-id="62ea0-130">In this code, we use an outgoing window of 1 to force the messages out as soon as possible.</span></span> <span data-ttu-id="62ea0-131">In generale l'applicazione dovrebbe cercare di riunire i messaggi in batch per migliorare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="62ea0-131">In general, your application should try to batch messages to increase throughput.</span></span> <span data-ttu-id="62ea0-132">Vedere la [pagina di Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) per informazioni sull'uso della libreria Qpid Proton in questo e in altri ambienti e anche nelle piattaforme per le quali sono disponibili associazioni, al momento Perl, PHP, Python e Ruby.</span><span class="sxs-lookup"><span data-stu-id="62ea0-132">See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="62ea0-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62ea0-133">Next steps</span></span>
<span data-ttu-id="62ea0-134">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="62ea0-134">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="62ea0-135">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="62ea0-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="62ea0-136">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="62ea0-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="62ea0-137">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="62ea0-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
