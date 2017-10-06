---
title: criteri di memorizzazione nella cache della rete CDN di Azure in servizi multimediali di Azure aaaManage | Documenti Microsoft
description: Informazioni su come toomanage criteri di memorizzazione nella cache della rete CDN di Azure in servizi multimediali di Azure.
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Gestire i criteri di memorizzazione nella cache della rete CDN di Azure in Servizi multimediali di Azure
Servizi multimediali di Azure fornisce lo streaming adattivo e il download progressivo basati su HTTP. Lo streaming basato su HTTP è altamente scalabile con i vantaggi della cache nei livelli proxy e di rete CDN, nonché della cache sul lato client. Gli endpoint di streaming forniscono funzionalità di streaming generale e configurazione per le intestazioni di cache HTTP. Gli endpoint di streaming impostano le intestazioni HTTP Cache-Control: max-age ed Expires. È possibile ottenere ulteriori informazioni per le intestazioni della cache HTTP da [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>Intestazioni di memorizzazione nella cache predefinite
Per impostazione predefinita, gli endpoint di streaming applicano intestazioni di cache di 3 giorni per i dati di streaming on demand (frammenti multimediali effettivi/blocchi) e manifest(playlist). Per lo streaming live, gli endpoint di streaming applicano intestazioni di cache di 3 giorni per i dati (frammenti multimediali effettivi/blocchi) e intestazioni di cache di 2 secondi per le richieste manifest(playlist). Quando si programma in diretta attiva richiesta tooon (archivio in tempo reale) quindi applicano le intestazioni della cache di streaming su richiesta.

## <a name="azure-cdn-integration"></a>Integrazione della rete CDN di Azure
Servizi multimediali di Azure fornisce [la rete CDN integrata](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) per gli endpoint di streaming. Intestazioni cache-control applica in hello stesso modo in streaming tooCDN endpoint abilitato l'endpoint di streaming. Azure CDN vengono utilizzati flussi endpoint configurato cache valori toodefine hello durata di hello internamente memorizzati nella cache gli oggetti e Usa anche le intestazioni di cache questo valore tooset hello recapito. Quando gli endpoint di streaming abilitato l'utilizzo della rete CDN non è consigliabile tooset i valori della cache è ridotta. Impostazione dei valori di piccole dimensioni verrà ridurre le prestazioni di hello e ridurre il vantaggio di hello della rete CDN. Non è consentito intestazioni cache tooset minore di 600 secondi per la rete CDN abilitato l'endpoint di streaming.

> [!IMPORTANT]
>Servizi multimediali di Azure assicura una perfetta integrazione con la rete CDN di Azure. È possibile integrare tutti hello disponibili rete CDN di Azure provider (Akamai e Verizon) tooyour endpoint, compresi i prodotti della rete CDN Standard e Premium di streaming con un solo clic. Per altre informazioni, vedere questo [annuncio](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Gli addebiti di dati dal flusso endpoint tooCDN Ottiene disabilitata solo se hello CDN è abilitata tramite le API di endpoint di streaming o utilizzando una sezione di endpoint di streaming del portale di gestione di Azure. Integrazione manuale o direttamente la creazione di un endpoint rete CDN utilizzando le API di rete CDN o sezione portale gli addebiti di hello dati non verrà disabilitato.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Configurazione delle intestazioni della cache con Servizi multimediali di Azure
È possibile utilizzare il portale di gestione di Azure o i valori dell'intestazione cache tooconfigure le API di servizi multimediali di Azure.

1. le intestazioni di cache tooconfigure tramite Gestione portale consultare troppo[come endpoint di Streaming tooManage](../media-services/media-services-portal-manage-streaming-endpoints.md) hello di sezione Configurazione Endpoint di Streaming.
2. API REST di Servizi multimediali di Azure, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. SDK .NET di Servizi multimediali di Azure, [Proprietà StreamingEndpointCacheControl](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Ordine di precedenza di configurazione della cache
1. Il valore della cache configurato di Servizi multimediali di Azure sostituisce il valore predefinito.
2. Se non è presente alcuna configurazione manuale, vengono applicati i valori predefiniti.
3. 2 secondi si applica intestazioni cache toolive streaming manifest(playlist) indipendentemente dalla configurazione di archiviazione di Azure o del supporto di Azure e si esegue l'override di questo valore non è disponibile per impostazione predefinita.

