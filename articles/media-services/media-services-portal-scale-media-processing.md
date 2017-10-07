---
title: supporto aaaScale elaborazione utilizzando hello portale di Azure | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di scala media elaborazione utilizzando hello portale di Azure.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a>Tipo di unità di modifica hello riservato
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encoding-units.md)
> * [Portale](media-services-portal-scale-media-processing.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a>Panoramica

Un account di servizi multimediali è associato a un tipo di unità riservate, che determina la velocità di hello con cui vengono elaborati i file multimediali l'elaborazione delle attività. È possibile scegliere tra segue hello i tipi di unità riservata: **S1**, **S2**, o **S3**. Ad esempio, hello stesso processo di codifica viene eseguito più velocemente quando si utilizza hello **S2** toohello di confronto del tipo di unità riservata **S1** tipo.

Inoltre toospecifying hello riservati di tipo di unità, è possibile specificare l'account con tooprovision **unità riservate** (RUs). numero di Hello di provisioning RUs determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account.

>[!NOTE]
>UR di lavoro per la parallelizzazione di tutta l'elaborazione di supporti di memorizzazione, tra cui l'indicizzazione di processi tramite Azure Media Indexer. Tuttavia, a differenza della codifica, l'indicizzazione di processi non viene elaborata più velocemente con unità riservate più veloci.

> [!IMPORTANT]
> Verificare che hello tooreview [Panoramica](media-services-scale-media-processing-overview.md) tooget argomento ulteriori informazioni sulla scalabilità supporti l'elaborazione di argomento.
> 
> 

## <a name="scale-media-processing"></a>Ridimensionare l'elaborazione di contenuti multimediali
toochange hello riservato unità hello tipo e il numero di unità riservate, hello seguenti:

1. In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali di Azure.
2. In hello **impostazioni** selezionare **supporto di unità riservate**.
   
    numero di hello toochange di unità riservate per hello selezionato il tipo di unità riservata, utilizzare hello **Media servita unità** dispositivo di scorrimento.
   
    hello toochange **il tipo di unità riservate**, premere S1, S2 o S3.
   
    ![Pagina relativa ai processori](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. Hello premere salvare toosave pulsante le modifiche.
   
    Quando si preme di salvataggio, vengono allocate nuove unità riservate di Hello.

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

