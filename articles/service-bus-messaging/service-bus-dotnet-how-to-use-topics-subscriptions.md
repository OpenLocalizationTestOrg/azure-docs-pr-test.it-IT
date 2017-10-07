---
title: aaaGet avviato con gli argomenti del Bus di servizio di Azure e le sottoscrizioni | Documenti Microsoft
description: Scrivere un'applicazione console C# che usa gli argomenti e le sottoscrizioni di messaggistica del bus di servizio.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Introduzione agli argomenti del bus di servizio

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Contenuto dell'esercitazione

Questa esercitazione sono trattati hello alla procedura seguente:

1. Creare uno spazio dei nomi Service Bus, utilizzando hello portale di Azure.
2. Creare un argomento del Bus di servizio, utilizzando hello portale di Azure.
3. Creare un argomento di toothat sottoscrizione Bus di servizio, utilizzando hello portale di Azure.
4. Scrivere un toosend di applicazione console come un argomento di toohello di messaggio.
5. Scrivere un tooreceive di applicazione console che il messaggio dalla sottoscrizione hello.

## <a name="prerequisites"></a>Prerequisiti

1. [Visual Studio 2015 o versione successiva](http://www.visualstudio.com). esempi di Hello in questa esercitazione usano Visual Studio 2017.
2. Una sottoscrizione di Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Creare uno spazio dei nomi utilizzando hello portale di Azure

Se è già stato creato uno spazio dei nomi di messaggistica del Bus di servizio, passare toohello [creare un argomento tramite il portale di Azure hello](#2-create-a-topic-using-the-azure-portal) sezione.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Creazione di un argomento tramite hello portale di Azure

1. Accesso toohello [portale di Azure][azure-portal].
2. Nel riquadro di spostamento a sinistra di hello del portale di hello, fare clic su **Bus di servizio** (se non viene visualizzato **Bus di servizio**, fare clic su **più servizi**).
3. Fare clic su spazio dei nomi hello in cui si desidera argomento hello toocreate. pannello della panoramica Hello dello spazio dei nomi viene visualizzato:
   
    ![Creare un argomento][createtopic1]
4. In hello **dello spazio dei nomi Service Bus** pannello, fare clic su **argomenti**, quindi fare clic su **Aggiungi argomento**.
   
    ![Selezionare gli argomenti][createtopic2]
5. Immettere un nome per l'argomento hello e deselezionare hello **abilitare il partizionamento** opzione. Lasciare hello altre opzioni con valori predefiniti.
   
    ![Selezionare Nuovo][createtopic3]
6. Nella parte inferiore di hello del pannello hello, fare clic su **crea**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Creazione di un argomento toohello sottoscrizione

1. Nel riquadro risorse portale hello, fare clic su spazio dei nomi hello creato nel passaggio 1, quindi fare clic sul nome di argomento hello creato nel passaggio 2.
2. Top hello del riquadro Panoramica hello, fare clic su hello segno più accanto troppo**sottoscrizione** tooadd un argomento toothis di sottoscrizione.

    ![Creare la sottoscrizione][createtopic4]

3. Immettere un nome per la sottoscrizione di hello. Lasciare hello altre opzioni con valori predefiniti.

## <a name="4-send-messages-toohello-topic"></a>4. Inviare l'argomento toohello messaggi

argomento toohello messaggi toosend è scrivere un'applicazione console c# con Visual Studio.

### <a name="create-a-console-application"></a>Creare un'applicazione console

Avviare Visual Studio e creare un nuovo progetto **App console (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Aggiungere il pacchetto NuGet di Service Bus hello

1. Fare clic sul progetto hello appena creato e selezionare **Gestisci pacchetti NuGet**.
2. Fare clic su hello **Sfoglia** scheda, cercare **Microsoft Azure Service Bus**, quindi selezionare hello **Windowsazure** elemento. Fare clic su **installare** toocomplete hello installazione, quindi chiudere questa finestra di dialogo.
   
    ![Selezionare un pacchetto NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Scrivere alcuni toosend codice un argomento toohello messaggio

1. Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Aggiungere i seguenti toohello codice hello `Main` metodo. Set hello `connectionString` connessione toohello variabile stringa ottenuto durante la creazione dello spazio dei nomi hello e impostare `topicName` toohello nome utilizzato per la creazione di hello argomento.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Esegui programma hello e verifica hello portale di Azure: fare clic sul nome dell'argomento nello spazio dei nomi hello hello **Panoramica** blade. argomento Hello **Essentials** pannello viene visualizzato. In hello delle sottoscrizioni elencate nella parte inferiore di hello della pannello hello, si noti che hello **numero messaggi** valore per ogni sottoscrizione deve essere 1. Ogni volta che si esegue l'applicazione mittente hello senza recuperare messaggi hello (come descritto nella sezione successiva hello), questo valore incrementato di 1. Si noti inoltre che dimensioni correnti di hello di hello incrementi di argomento hello **corrente** valore hello **Essentials** pannello ogni volta che l'applicazione hello aggiunge una messaggio toohello argomento o sottoscrizione.
   
      ![Dimensioni dei messaggi][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Ricevere messaggi dalla sottoscrizione hello

1. tooreceive hello o messaggi appena inviato, creare una nuova applicazione console e aggiungere un pacchetto NuGet di Service Bus toohello riferimento, applicazione mittente precedente toohello simile.
2. Aggiungere il seguente hello `using` top toohello istruzione del file Program.cs hello.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Aggiungere i seguenti toohello codice hello `Main` metodo. Set hello `connectionString` connessione toohello variabile stringa ottenuto durante la creazione dello spazio dei nomi hello e impostare `topicName` toohello nome utilizzato per la creazione di hello argomento.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Eseguire il programma hello e controllare di nuovo portale hello. Si noti che hello **numero messaggi** e **corrente** ora sono valori 0.
   
    ![Lunghezza argomento][topic-message-receive]

Congratulazioni. Sono stati creati un argomento e una sottoscrizione ed è stato inviato un messaggio che è stato quindi ricevuto.

## <a name="next-steps"></a>Passaggi successivi

Estrarre il nostro [repository GitHub con campioni](https://github.com/Azure/azure-service-bus/tree/master/samples) che illustrano alcune delle più avanzate funzionalità di messaggistica del Bus di servizio hello.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
