---
title: "supporto aaaScale elaborazione mediante l'aggiunta di unità di codifica - Azure |  Documenti Microsoft"
description: "Informazioni su come unità di codifica tooadd toohow con .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a>Come tooscale codifica con .NET SDK
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Panoramica
> [!IMPORTANT]
> Verificare che hello tooreview [Panoramica](media-services-scale-media-processing-overview.md) tooget argomento ulteriori informazioni sulla scalabilità supporti l'elaborazione di argomento.
> 
> 

hello toochange hello riservato hello tipo e il numero di unità mediante .NET SDK, di unità riservate di codifica seguenti:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Apertura di un ticket di supporto
Per impostazione predefinita, ogni account di servizi multimediali possono essere ridimensionati tooup too25 5 e codifica su richiesta unità riservate di Streaming. È possibile richiedere l'applicazione di un limite superiore mediante l'apertura di un ticket di supporto.

### <a name="open-a-support-ticket"></a>Aprire un ticket di supporto
hello tooopen un ticket di supporto seguenti:

1. Fare clic su [Ottieni supporto](https://manage.windowsazure.com/?getsupport=true). Se non si è connessi, è necessario essere tooenter richieste le credenziali.
2. Selezionare la propria sottoscrizione.
3. Come tipo di supporto, selezionare "Tecnico".
4. Fare clic su "Create Ticket".
5. Selezionare "Servizi multimediali di Azure" nell'elenco di prodotti hello presentate nella pagina successiva di hello.
6. Selezionare un tipo di problema appropriato per la situazione specifica.
7. Fare clic su Continue.
8. Seguire le istruzioni nella pagina successiva e quindi immettere i dettagli relativi al problema.
9. Fare clic su Invia il ticket hello tooopen.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

