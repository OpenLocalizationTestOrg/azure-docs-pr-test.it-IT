---
title: aaaSend eventi tooAzure hub eventi utilizzando C | Documenti Microsoft
description: Inviare gli eventi di hub di eventi tooAzure utilizzando C
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
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="7ac34-103">Inviare gli eventi di hub di eventi tooAzure utilizzando C</span><span class="sxs-lookup"><span data-stu-id="7ac34-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="7ac34-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7ac34-104">Introduction</span></span>
<span data-ttu-id="7ac34-105">Hub eventi è un sistema di inserimento estremamente scalabile in grado di milioni di eventi al secondo, abilitazione tooprocess un'applicazione di inserimento e analizzare hello enormi quantità di dati generati per i dispositivi connessi e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7ac34-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="7ac34-106">Dopo la raccolta in un hub eventi, è possibile trasformare e archiviare i dati usando qualsiasi provider di analisi in tempo reale o un cluster di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="7ac34-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="7ac34-107">Per ulteriori informazioni, vedere hello [Panoramica di hub eventi] [Panoramica di hub eventi].</span><span class="sxs-lookup"><span data-stu-id="7ac34-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="7ac34-108">In questa esercitazione si apprenderà come hub eventi tooan eventi toosend usando un'applicazione console in c. tooreceive eventi, fare clic su lingua ricevente hello appropriata nella tabella a sinistra di hello del contenuto.</span><span class="sxs-lookup"><span data-stu-id="7ac34-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="7ac34-109">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7ac34-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="7ac34-110">Ambiente di sviluppo in C.</span><span class="sxs-lookup"><span data-stu-id="7ac34-110">A C development environment.</span></span> <span data-ttu-id="7ac34-111">Per questa esercitazione, si suppone stack gcc hello in una macchina virtuale Linux di Azure con Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="7ac34-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="7ac34-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="7ac34-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="7ac34-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="7ac34-113">An active Azure account.</span></span> <span data-ttu-id="7ac34-114">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="7ac34-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7ac34-115">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ac34-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="7ac34-116">Invio di messaggi tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="7ac34-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="7ac34-117">In questa sezione è scrivere un hub di eventi tooyour C app toosend eventi.</span><span class="sxs-lookup"><span data-stu-id="7ac34-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="7ac34-118">codice Hello Usa libreria Proton AMQP hello da hello [progetto Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="7ac34-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="7ac34-119">Questo è analoga toousing code del Bus di servizio e gli argomenti con AMQP da C, come illustrato [qui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="7ac34-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="7ac34-120">Per altre informazioni, vedere la [documentazione di Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="7ac34-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="7ac34-121">Da hello [pagina Messenger AMQP Qpid](https://qpid.apache.org/proton/messenger.html), seguire le istruzioni di hello tooinstall Qpid Proton, a seconda dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="7ac34-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="7ac34-122">toocompile hello libreria Proton, installare i seguenti pacchetti hello:</span><span class="sxs-lookup"><span data-stu-id="7ac34-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="7ac34-123">Scaricare hello [libreria Qpid Proton](http://qpid.apache.org/proton/index.html)ed estrarre i file, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7ac34-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="7ac34-124">Creare una directory di compilazione, compilare e installare:</span><span class="sxs-lookup"><span data-stu-id="7ac34-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="7ac34-125">Nella directory di lavoro, creare un nuovo file denominato **sender.c** con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="7ac34-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="7ac34-126">Tenere presente il valore hello toosubstitute per il nome dell'hub eventi e il nome dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="7ac34-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="7ac34-127">È inoltre necessario sostituire una versione con codifica URL della chiave di hello per hello **SendRule** creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="7ac34-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="7ac34-128">È possibile creare la versione codificata con URL [qui](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="7ac34-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
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
        printf("Press Ctrl-C toostop hello sender process\n");
   
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
6. <span data-ttu-id="7ac34-129">Compilare il file hello, presupponendo che **gcc**:</span><span class="sxs-lookup"><span data-stu-id="7ac34-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="7ac34-130">In questo codice, si usa una finestra in uscita dei messaggi di hello tooforce 1 out appena possibile.</span><span class="sxs-lookup"><span data-stu-id="7ac34-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="7ac34-131">In generale, l'applicazione deve tentare di velocità effettiva di tooincrease messaggi toobatch.</span><span class="sxs-lookup"><span data-stu-id="7ac34-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="7ac34-132">Vedere hello [pagina Messenger AMQP Qpid](https://qpid.apache.org/proton/messenger.html) per informazioni su come toouse hello libreria Qpid Proton in questo e altri ambienti e da piattaforme per il quale vengono fornite le associazioni (attualmente Perl, PHP, Python e Ruby).</span><span class="sxs-lookup"><span data-stu-id="7ac34-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ac34-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ac34-133">Next steps</span></span>
<span data-ttu-id="7ac34-134">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="7ac34-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="7ac34-135">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="7ac34-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="7ac34-136">Creare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="7ac34-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="7ac34-137">Domande frequenti su Hub eventi</span><span class="sxs-lookup"><span data-stu-id="7ac34-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
