---
title: aaaGet avviato con le code di Service Bus di Azure | Documenti Microsoft
description: Scrivere un'applicazione console C# che usa le code di messaggistica del bus di servizio.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Introduzione alle code del bus di servizio
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Contenuto dell'esercitazione
Questa esercitazione sono trattati hello alla procedura seguente:

1. Creare uno spazio dei nomi Service Bus, utilizzando hello portale di Azure.
2. Creare una coda di Service Bus, utilizzando hello portale di Azure.
3. Scrivere un messaggio a un toosend di applicazione console.
4. Scrivere un hello tooreceive di applicazione console messaggi inviati nel passaggio precedente hello.

## <a name="prerequisites"></a>Prerequisiti
1. [Visual Studio 2015 o versione successiva](http://www.visualstudio.com). esempi di Hello in questa esercitazione usano Visual Studio 2017.
2. Una sottoscrizione di Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Creare uno spazio dei nomi utilizzando hello portale di Azure
Se è già stato creato uno spazio dei nomi di messaggistica del Bus di servizio, passare toohello [creare una coda utilizzando il portale di Azure hello](#2-create-a-queue-using-the-azure-portal) sezione.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Creare una coda utilizzando hello portale di Azure
Se è stato già creato una coda del Bus di servizio, passare toohello [coda di invio messaggi toohello](#3-send-messages-to-the-queue) sezione.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Messaggi toohello coda di invio
coda di toohello toosend messaggi, è scrivere un'applicazione console c# con Visual Studio.

### <a name="create-a-console-application"></a>Creare un'applicazione console

Avviare Visual Studio e creare un nuovo progetto **App console (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Aggiungere il pacchetto NuGet di Service Bus hello
1. Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.
2. Fare clic su hello **Sfoglia** scheda, cercare **Microsoft Azure Service Bus**, quindi selezionare hello **Windowsazure** elemento. Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.
   
    ![Selezionare un pacchetto NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Scrittura di una coda di messaggi toohello alcuni toosend di codice
1. Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Aggiungere i seguenti toohello codice hello `Main` metodo. Set hello `connectionString` connessione toohello variabile stringa ottenuto durante la creazione dello spazio dei nomi hello e impostare `queueName` toohello della coda utilizzata durante la creazione della coda di hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Ecco l'aspetto che avrà il file Program.cs.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Esegui programma hello e verifica hello portale di Azure: fare clic sul nome della coda nello spazio dei nomi hello hello **Panoramica** blade. coda Hello **Essentials** pannello viene visualizzato. Si noti che hello **il numero di messaggi attivi** valore dovrebbe essere 1. Ogni volta che si esegue l'applicazione mittente hello senza recuperare i messaggi hello, questo valore incrementato di 1. Si noti che dimensioni correnti di hello della coda di hello viene incrementato a ogni applicazione hello ora aggiunge inoltre una coda di messaggi toohello.
   
      ![Dimensioni dei messaggi][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Ricevere messaggi dalla coda hello

1. messaggi hello tooreceive appena inviato, creare una nuova applicazione console e aggiungere un pacchetto NuGet di Service Bus toohello riferimento, applicazione mittente precedente toohello simile.
2. Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Aggiungere i seguenti toohello codice hello `Main` metodo. Set hello `connectionString` toohello variabile stringa di connessione è stato ottenuto durante la creazione dello spazio dei nomi hello e impostare `queueName` toohello della coda utilizzata durante la creazione della coda di hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Ecco l'aspetto che avrà il file Program.cs:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Eseguire il programma hello e controllare di nuovo portale hello. Si noti che hello **il numero di messaggi attivi** e **corrente** ora sono valori 0.
   
    ![Lunghezza coda][queue-message-receive]

Congratulazioni. È stata creata una coda ed è stato inviato e ricevuto un messaggio.

## <a name="next-steps"></a>Passaggi successivi

Estrarre il nostro [repository GitHub con campioni](https://github.com/Azure/azure-service-bus/tree/master/samples) che illustrano alcune delle più avanzate funzionalità di messaggistica del Bus di servizio hello.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
