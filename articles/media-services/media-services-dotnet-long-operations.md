---
title: Operazioni con esecuzione prolungata aaaPolling | Documenti Microsoft
description: Questo argomento viene illustrato come toopoll operazioni a esecuzione prolungata.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a>Distribuzione di Live Streaming con Servizi multimediali di Azure

## <a name="overview"></a>Panoramica

Servizi multimediali di Microsoft Azure offre API che inviano richieste di operazioni di toostart tooMedia Services (ad esempio: creare, avviare, arrestare o eliminare un canale). Queste operazioni hanno un'esecuzione prolungata.

Hello Media Services .NET SDK fornisce le API che inviano la richiesta hello e attendere hello operazione toocomplete (internamente, Buongiorno API eseguono il polling dell'avanzamento dell'operazione a intervalli definiti). Ad esempio, quando si chiama canale. Start (), il metodo hello restituisce dopo l'avvio del canale hello. È inoltre possibile utilizzare la versione asincrona di hello: attesa del canale. StartAsync() (per informazioni sul modello asincrono basato su attività, vedere [toccare](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). Le API che inviano una richiesta di operazione e quindi eseguire il polling per lo stato di hello fino al completamento dell'operazione hello vengono definite "metodi di polling". Questi metodi (in particolare versione asincrona di hello) sono consigliati per le applicazioni rich client e/o i servizi con stato.

Esistono scenari in cui un'applicazione non può attendere una richiesta http a esecuzione prolungata e desidera toopoll hello dell'avanzamento dell'operazione manualmente. Un esempio tipico sarebbe un browser che interagisce con un servizio web senza stato: quando il browser di hello richiede toocreate un canale, servizio web hello avvia un'operazione a esecuzione prolungata e restituisce hello browser toohello ID di operazione. browser Hello potrebbe quindi chiedere di hello web servizio tooget hello stato dell'operazione basato sull'ID di hello. Hello Media Services .NET SDK fornisce le API che sono utili per questo scenario. definite "metodi di non polling",
"metodi di non polling" Hello hanno hello seguente modello di denominazione: inviare*OperationName*operazione (ad esempio, SendCreateOperation). Inviare*OperationName*operazione restituiscono hello **IOperation** oggetto; hello oggetto restituito contiene le informazioni che possono essere utilizzati tootrack hello operazione. Hello trasmissione*OperationName*OperationAsync restituiscono **attività<IOperation>**.

Attualmente, hello dei seguenti metodi di non polling supporto classi: **canale**, **StreamingEndpoint**, e **programma**.

toopoll hello dello stato dell'operazione, utilizzare hello **GetOperation** metodo hello **OperationBaseCollection** classe. Utilizzare hello seguente lo stato dell'operazione intervalli toocheck hello: per **canale** e **StreamingEndpoint** operazioni, usare 30 secondi; per **programma** operazioni, utilizzare 10 secondi.

## <a name="create-and-configure-a-visual-studio-project"></a>Creare e configurare un progetto di Visual Studio

Configurare l'ambiente di sviluppo e di popolare il file app. config hello con informazioni di connessione, come descritto in [lo sviluppo di servizi multimediali con .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Esempio

esempio Hello definisce una classe denominata **ChannelOperations**. Questa definizione di classe può essere un punto di partenza per la definizione di classe del servizio Web. Per semplicità, hello negli esempi seguenti utilizzano versioni non asincrone hello dei metodi.

esempio Hello Mostra anche come client hello possibile utilizzare questa classe.

### <a name="channeloperations-class-definition"></a>Definizione della classe ChannelOperations

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a>codice client Hello
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

