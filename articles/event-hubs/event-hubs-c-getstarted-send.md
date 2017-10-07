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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Inviare gli eventi di hub di eventi tooAzure utilizzando C

## <a name="introduction"></a>Introduzione
Hub eventi è un sistema di inserimento estremamente scalabile in grado di milioni di eventi al secondo, abilitazione tooprocess un'applicazione di inserimento e analizzare hello enormi quantità di dati generati per i dispositivi connessi e le applicazioni. Dopo la raccolta in un hub eventi, è possibile trasformare e archiviare i dati usando qualsiasi provider di analisi in tempo reale o un cluster di archiviazione.

Per ulteriori informazioni, vedere hello [Panoramica di hub eventi] [Panoramica di hub eventi].

In questa esercitazione si apprenderà come hub eventi tooan eventi toosend usando un'applicazione console in c. tooreceive eventi, fare clic su lingua ricevente hello appropriata nella tabella a sinistra di hello del contenuto.

toocomplete questa esercitazione, è necessario hello seguenti:

* Ambiente di sviluppo in C. Per questa esercitazione, si suppone stack gcc hello in una macchina virtuale Linux di Azure con Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Un account Azure attivo. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-tooevent-hubs"></a>Invio di messaggi tooEvent hub
In questa sezione è scrivere un hub di eventi tooyour C app toosend eventi. codice Hello Usa libreria Proton AMQP hello da hello [progetto Apache Qpid](http://qpid.apache.org/). Questo è analoga toousing code del Bus di servizio e gli argomenti con AMQP da C, come illustrato [qui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Per altre informazioni, vedere la [documentazione di Qpid Proton](http://qpid.apache.org/proton/index.html).

1. Da hello [pagina Messenger AMQP Qpid](https://qpid.apache.org/proton/messenger.html), seguire le istruzioni di hello tooinstall Qpid Proton, a seconda dell'ambiente.
2. toocompile hello libreria Proton, installare i seguenti pacchetti hello:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Scaricare hello [libreria Qpid Proton](http://qpid.apache.org/proton/index.html)ed estrarre i file, ad esempio:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Creare una directory di compilazione, compilare e installare:
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. Nella directory di lavoro, creare un nuovo file denominato **sender.c** con hello seguente codice. Tenere presente il valore hello toosubstitute per il nome dell'hub eventi e il nome dello spazio dei nomi. È inoltre necessario sostituire una versione con codifica URL della chiave di hello per hello **SendRule** creato in precedenza. È possibile creare la versione codificata con URL [qui](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Compilare il file hello, presupponendo che **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > In questo codice, si usa una finestra in uscita dei messaggi di hello tooforce 1 out appena possibile. In generale, l'applicazione deve tentare di velocità effettiva di tooincrease messaggi toobatch. Vedere hello [pagina Messenger AMQP Qpid](https://qpid.apache.org/proton/messenger.html) per informazioni su come toouse hello libreria Qpid Proton in questo e altri ambienti e da piattaforme per il quale vengono fornite le associazioni (attualmente Perl, PHP, Python e Ruby).


## <a name="next-steps"></a>Passaggi successivi
Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md
)
* [Creare un hub eventi](event-hubs-create.md)
* [Domande frequenti su Hub eventi](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
