---
title: Panoramica di servizi multimediali aaaAzure | Documenti Microsoft
description: Questo argomento fornisce informazioni generali su Servizi multimediali di Azure
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a>Panoramica di Servizi multimediali di Azure 

Servizi multimediali di Microsoft Azure è una piattaforma estendibile basato su cloud che consente agli sviluppatori toobuild contenuti multimediali altamente scalabili distribuzione e gestione delle applicazioni. Servizi multimediali è basato sulle API REST che consentono di caricamento toosecurely, archiviare, codificare e creare il pacchetto di contenuto video o audio per su richiesta e live streaming toovarious client di recapito (ad esempio, TV, PC e dispositivi mobili).

È possibile creare flussi di lavoro end-to-end usando unicamente Servizi multimediali. È anche possibile scegliere toouse componenti di terze parti per alcune parti del flusso di lavoro. ad esempio, la codifica con un codificatore di terze parti. Inoltre, sono possibili operazioni di caricamento, protezione, creazione di pacchetti e invio tramite Servizi multimediali.

È possibile scegliere toostream il contenuto in tempo reale o fornire contenuto su richiesta. argomento Hello è anche possibile collegare tooother relativi argomenti.

## <a name="media-services-learning-paths"></a>Percorsi di apprendimento di Servizi multimediali
È possibile visualizzare i percorsi di apprendimento AMS qui:

* [Flusso di lavoro AMS Live Streaming](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [Flusso di lavoro dello streaming on demand di AMS](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a>Prerequisiti

toostart tramite servizi multimediali di Azure, è necessario seguente hello:

* Un account Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com).
* Un account di Servizi multimediali di Azure. Per altre informazioni, vedere [Creare un account](media-services-portal-create-account.md).
* (Facoltativo) Configurare l'ambiente di sviluppo. Scegliere .NET o API REST per l'ambiente di sviluppo. Per altre informazioni, vedere [Configurare l'ambiente](media-services-dotnet-how-to-use.md).

    Inoltre, informazioni su come troppo[connettersi a livello di programmazione tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).
* Un endpoint di streaming Standard o Premium con stato avviato.  Per altre informazioni, vedere [Gestione degli endpoint di streaming](media-services-portal-manage-streaming-endpoints.md).

## <a name="sdks-and-tools"></a>SDK e strumenti

soluzioni di servizi multimediali toobuild, è possibile utilizzare:

* [API REST di Servizi multimediali](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* Uno dei client disponibili hello SDK:
    * [Azure Media Services SDK per .NET](https://github.com/Azure/azure-sdk-for-media-services)
    * [Azure SDK per Java](https://github.com/Azure/azure-sdk-for-java),
    * [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),
    * [Servizi multimediali di Azure per Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js). Questa è una versione non Microsoft di Node.js SDK. Viene mantenuto da una community e non sono attualmente una copertura del 100% di hello AMS APIs).
* Strumenti esistenti:
    * [Portale di Azure](https://portal.azure.com/)
    * [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) è un'applicazione Winforms/C# per Windows)

## <a name="concepts-and-overview"></a>Panoramica e concetti
Per i concetti relativi ai Servizi multimediali di Azure, vedere [Concetti su Servizi multimediali di Azure](media-services-concepts.md).

Per una procedura-tooseries che presentano le componenti principali di hello tooall di servizi multimediali di Azure, vedere [esercitazioni di Azure Media Services dettagliata](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series). Questa serie contiene una panoramica dei concetti e utilizza le attività di hello AMSE strumento toodemonstrate AMS. AMSE è uno strumento Windows. Questo strumento supporta la maggior parte delle attività hello è possibile ottenere a livello di codice con [AMS SDK per .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK per Java](https://github.com/Azure/azure-sdk-for-java), o [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a>Scenari supportati e disponibilità di Servizi multimediali nei data center

Per informazioni dettagliate, vedere [Scenari supportati e disponibilità di Servizi multimediali nei data center](scenarios-and-availability.md).

## <a name="service-level-agreement-sla"></a>Contratto di servizio (SLA)

* Per il servizio di codifica di Servizi multimediali, è garantita una disponibilità al 99,9% delle transazioni delle API REST.
* Con l'acquisto di un endpoint di streaming Standard o Premium, per il servizio di streaming, è garantita una disponibilità al 99,9% per i contenuti multimediali esistenti.
* Per i canali Live, si garantisce che l'esecuzione di canali connettività esterna almeno il 99,9% del tempo di hello.
* Per la protezione del contenuto, è garantito che è verrà correttamente soddisfare richieste di chiavi almeno il 99,9% del tempo di hello.
* Per un indicizzatore, è, il servizio indicizzatore attività elaborata con una codifica di riservato unità 99,9% del tempo di hello.

Per altre informazioni, vedere [Contratto di servizio di Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).

Per informazioni sulla disponibilità in Data Center, vedere hello [Avaiability](scenarios-and-availability.md#availability) sezione.

## <a name="support"></a>Supporto

[supporto tecnico di Azure](https://azure.microsoft.com/support/options/) fornisce opzioni di supporto per Azure, compreso Servizi multimediali.

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
