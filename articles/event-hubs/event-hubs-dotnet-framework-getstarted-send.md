---
title: gli hub di eventi di aaaSend tooAzure eventi usando hello .NET Framework | Documenti Microsoft
description: Iniziare l'invio di eventi tooEvent hub utilizzando hello .NET Framework
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Inviare gli eventi di hub di eventi tooAzure utilizzando hello .NET Framework

## <a name="introduction"></a>Introduzione

Hub eventi è un servizio che consente di elaborare grandi quantità di dati di telemetria sugli eventi da applicazioni e dispositivi connessi. Dopo aver raccolto i dati in hub eventi, è possibile archiviare i dati di hello utilizzando un cluster di archiviazione o trasformare tramite un provider analitica in tempo reale. Questa funzionalità di raccolta e l'elaborazione di eventi su larga scala è un componente fondamentale di architetture di applicazioni moderne inclusi hello Internet delle cose (IoT).

Questa esercitazione viene illustrato come hello toouse [portale di Azure](https://portal.azure.com) toocreate un hub eventi. Viene inoltre illustrato come hub eventi tooan eventi toosend utilizzando un'applicazione console scritta in c# tramite hello .NET Framework. gli eventi di tooreceive utilizzando hello .NET Framework, vedere hello [ricevere gli eventi utilizzando .NET Framework hello](event-hubs-dotnet-framework-getstarted-receive-eph.md) articolo oppure fare clic sulla lingua ricevente hello appropriata nella tabella a sinistra di hello del contenuto.

toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:

* [Microsoft Visual Studio 2015 o versione successiva](http://visualstudio.com). le schermate di Hello in questa esercitazione usare Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno gratuito in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Creare uno spazio dei nomi di Hub eventi e un hub eventi

primo passaggio Hello è hello toouse [portale di Azure](https://portal.azure.com) toocreate spazio dei nomi di tipo hub eventi e ottenere hello le credenziali di gestione, l'applicazione deve toocommunicate con hub eventi hello. toocreate uno spazio dei nomi e hub eventi, attenersi alla procedura hello in [questo articolo](event-hubs-create.md), quindi procedere con hello seguendo i passaggi in questa esercitazione.

## <a name="create-a-sender-console-application"></a>Creare un'applicazione console per il mittente

In questa sezione verrà scritto un'applicazione console di Windows che invia l'hub di eventi tooyour di eventi.

1. In Visual Studio, creare un nuovo progetto di App Desktop Visual c# utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **mittente**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. In Esplora soluzioni fare doppio clic su hello **mittente** del progetto e quindi fare clic su **Gestisci pacchetti NuGet per la soluzione**. 
3. Fare clic su hello **Sfoglia** tab, quindi cercare `Microsoft Azure Service Bus`. Fare clic su **installare**e accettare le condizioni di hello d'uso. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio Scarica, installa e aggiunge un riferimento toohello [pacchetto NuGet della libreria di Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Aggiungere i seguenti campi toohello hello **programma** classe, sostituendo i valori segnaposto hello con nome hello dell'hub eventi hello creato nella sezione precedente hello e stringa di connessione dello spazio dei nomi a livello di hello è stato salvato in precedenza.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Aggiungere hello seguente metodo toohello **programma** classe:
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  Questo metodo invia in modo continuo hub di eventi eventi tooyour con un ritardo di 200 ms.
7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Eseguire il programma hello e assicurarsi che non siano presenti errori.
  
Congratulazioni. Hub di eventi tooan messaggi inviati a questo punto.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un'applicazione funzionante che crea un hub eventi e invia i dati, è possibile passare toohello seguenti scenari:

* [Ricezione di eventi utilizzando hello Host processore di eventi](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Event Processor Host reference](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) (Informazioni di riferimento sull'host processore di eventi)
* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

