---
title: "Ridimensionare l'elaborazione multimediale aggiungendo unità di codifica - Azure | Documentazione Microsoft"
description: "Informazioni su come aggiungere unità di codifica mediante .NET"
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
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a>Come scalare la codifica con .NET SDK
> [!div class="op_single_selector"]
> * [Portale](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Overview
> [!IMPORTANT]
> Per altre informazioni sul ridimensionamento dell'elaborazione multimediale, vedere questo argomento di [panoramica](media-services-scale-media-processing-overview.md) .
> 
> 

Per cambiare il tipo di unità riservata e il numero di unità riservate di codifica mediante l'SDK per .NET, seguire questa procedura:

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a>Apertura di un ticket di supporto
Per impostazione predefinita, ogni account di Media Services può includere fino a 25 unità di codifica riservate e cinque unità riservate di streaming on demand. È possibile richiedere l'applicazione di un limite superiore mediante l'apertura di un ticket di supporto.

### <a name="open-a-support-ticket"></a>Aprire un ticket di supporto
Per aprire un ticket di supporto, seguire questa procedura:

1. Fare clic su [Ottieni supporto](https://manage.windowsazure.com/?getsupport=true). Se non si è ancora connessi, verrà richiesto di immettere le credenziali.
2. Selezionare la propria sottoscrizione.
3. Come tipo di supporto, selezionare "Tecnico".
4. Fare clic su "Create Ticket".
5. Selezionare "Servizi multimediali di Azure" dall'elenco dei prodotti visualizzato nella pagina successiva.
6. Selezionare un tipo di problema appropriato per la situazione specifica.
7. Fare clic su Continue.
8. Seguire le istruzioni nella pagina successiva e quindi immettere i dettagli relativi al problema.
9. Fare clic su Invia per aprire il ticket.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

