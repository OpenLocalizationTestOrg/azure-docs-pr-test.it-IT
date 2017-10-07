---
title: "velocità Gestisci aaa e la concorrenza della codifica con servizi multimediali di Azure | Documenti Microsoft"
description: "Questo articolo illustra brevemente la procedura per gestire la velocità e la concorrenza delle attività o dei processi di codifica con Servizi multimediali di Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a>Gestire la velocità e la concorrenza della codifica

Questo articolo illustra brevemente la procedura per gestire la velocità e la concorrenza delle attività o dei processi di codifica.

## <a name="overview"></a>Panoramica

In servizi multimediali un **il tipo di unità riservate** determina hello velocità con cui vengono elaborati i file multimediali l'elaborazione delle attività. È possibile scegliere tra segue hello i tipi di unità riservata: **S1**, **S2**, o **S3**. Ad esempio, hello stesso processo di codifica viene eseguito più velocemente quando si utilizza hello **S2** toohello di confronto del tipo di unità riservata **S1** tipo. Hello [scalabilità unità di codifica](media-services-scale-media-processing-overview.md) argomento viene illustrata una tabella che consente di decidere quando si sceglie tra diverse velocità di codifica.

Inoltre toospecifying hello riservati di tipo di unità, è possibile specificare l'account con tooprovision **unità riservate**. numero di Hello di unità riservate sottoposte a provisioning determina il numero di hello delle attività multimediali che possono essere elaborate contemporaneamente in un determinato account. Ad esempio, se l'account dispone di 5 unità riservate, quindi verrà eseguita contemporaneamente a condizione attività cinque multimediali sono pari al numero di attività toobe elaborati. le attività rimanenti Hello rimarranno in attesa nella coda di hello e saranno prelevate per l'elaborazione in sequenza al termine di un'attività in esecuzione. Se per un account non sono state fornite unità riservate, le attività verranno prelevate in sequenza. In questo caso, hello tempo di attesa tra un completamento di attività e hello avvio della successiva dipenderà disponibilità hello delle risorse di sistema hello.

Per informazioni dettagliate ed esempi che mostrano come unità di codifica tooscale, vedere [questo](media-services-scale-media-processing-overview.md) argomento.

## <a name="next-step"></a>Passaggio successivo

[Ridimensionare le unità di codifica](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

