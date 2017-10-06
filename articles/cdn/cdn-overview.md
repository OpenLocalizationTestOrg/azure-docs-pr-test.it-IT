---
title: Panoramica della rete CDN aaaAzure | Documenti Microsoft
description: "Informazioni su quali hello è rete recapito contenuti (CDN) di Azure e come toouse è toodeliver contenuto di larghezza di banda elevata memorizzando nella cache BLOB e il contenuto statico."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Panoramica di hello Azure rete CDN (Content Delivery)
> [!NOTE]
> Questo documento descrive quali hello Azure rete CDN (Content Delivery) è il funzionamento e le funzionalità di hello di ogni prodotto rete CDN di Azure.  Se si desidera che queste informazioni tooskip e passare tooa retta esercitazione su come toocreate un endpoint rete CDN, vedere [utilizzo della rete CDN di Azure](cdn-create-new-endpoint.md).  Se si desidera un elenco delle posizioni correnti del nodo CDN toosee, vedere [posizioni POP CDN di Azure](cdn-pop-locations.md).
> 
> 

Hello rete recapito contenuti (CDN) di Azure vengono memorizzati nella cache di contenuti web statici in percorsi strategici tooprovide massima velocità effettiva per il recapito toousers contenuto.  Hello CDN offre agli sviluppatori una soluzione globale per recapitare contenuti di larghezza di banda elevata memorizzando nella cache il contenuto di hello in nodi fisici tra HelloWorld. 

i vantaggi dell'utilizzo di risorse del sito web di hello CDN toocache Hello includono:

* Prestazioni ed esperienza utente migliorate per gli utenti finali, soprattutto quando utilizzano applicazioni a più round trip necessari contenuto tooload.
* Grande scala toobetter handle carico elevato istantaneo, ad esempio all'inizio di hello di un prodotto lancio.
* Per distribuire le richieste utente e del contenuto dai server edge, minore quantità di traffico viene inviato toohello origine.

## <a name="how-it-works"></a>Funzionamento
![Panoramica della rete CDN](./media/cdn-overview/cdn-overview.png)

1. Un utente (Alice) richiede un file, detto anche asset, usando un URL con un nome di dominio particolare, ad esempio `<endpointname>.azureedge.net`.  Il percorso Point of Presence (POP) migliori prestazioni di hello richiesta toohello instrada il DNS.  In genere si tratta di hello POP utente toohello geograficamente più vicino.
2. Se il server edge hello in hello POP non dispone di file hello nella cache, file hello server perimetrale hello richieste dall'origine hello.  origine Hello può essere un'App Web di Azure, servizio Cloud di Azure, account di archiviazione Azure o qualsiasi altro server web accessibile pubblicamente.
3. origine Hello restituisce hello file toohello lato server, incluse intestazioni HTTP, la descrizione Time-to-Live del file hello (TTL).
4. server perimetrale Hello memorizza nella cache file hello e restituisce richiedente originale di toohello file hello (Alice).  file Hello rimane memorizzata nella cache nel server perimetrale hello fino alla scadenza di TTL hello.  Se l'origine di hello non sono state specificate una durata (TTL), durata TTL predefinita hello è sette giorni.
5. Altri utenti possono quindi hello richiesta stessa utilizzando tale stesso URL di file e può anche essere diretto toothat POP stesso.
6. Se non è scaduto hello durata (TTL) per il file hello, server perimetrale hello restituisce file hello dalla cache di hello.  offrendo quindi un'esperienza utente più veloce ed efficiente.

## <a name="azure-cdn-features"></a>Funzionalità della rete CDN di Azure
Per la rete CDN di Azure sono disponibili tre prodotti: **rete CDN Standard di Azure fornita da Akamai**, **rete CDN Standard di Azure fornita da Verizon** e **rete CDN Premium di Azure fornita da Verizon**.  Hello nella tabella seguente sono elencate le funzionalità di hello disponibili con ogni prodotto.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Funzionalità prestazioni e ottimizzazioni__ |
| [Accelerazione sito dinamico](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&amp;#x2713;** | **&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  [Accelerazione sito dinamico - Compressione di immagini adattiva](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&amp;#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Accelerazione sito dinamico - Prelettura degli oggetti](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&amp;#x2713;**  |  |  |
| [Ottimizzazione dello streaming video](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&amp;#x2713;**  | \* |  \* |
| [Ottimizzazione di file di grandi dimensioni](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Bilanciamento del carico del server globale](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Eliminazione veloce](cdn-purge-endpoint.md) |**&#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Precaricamento Asset](cdn-preload-endpoint.md) | |**&amp;#x2713;** |**&amp;#x2713;** |
| [Memorizzazione nella cache della stringa di query](cdn-query-string.md) |**&#x2713;** |**&amp;#x2713;** |**&#x2713;** |
| IPv4/IPv6 dual stack |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Supporto HTTP/2](cdn-http2.md) |**&#x2713;** |**&amp;#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Sicurezza__ |
| Supporto per HTTPS con endpoint della rete CDN |**&#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [HTTPS dominio personalizzato](cdn-custom-ssl.md) | |**&amp;#x2713;** |**&#x2713;** |
| [Supporto del nome di dominio personalizzato.](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Filtro geografico](cdn-restrict-access-by-country.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Autenticazione tramite token](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [Protezione DDoS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Analisi e creazione di report__ |
| [Analisi del core](cdn-analyze-usage-patterns.md) | **&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Report HTTP avanzati](cdn-advanced-http-reports.md) | | |**&amp;#x2713;** |
| [Statistiche in tempo reale](cdn-real-time-stats.md) | | |**&amp;#x2713;** |
| [Avvisi in tempo reale](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Semplicità d'uso__ |
| Semplice integrazione con i servizi di Azure, ad esempio [Archiviazione](cdn-create-a-storage-account-with-cdn.md), [Servizi cloud](cdn-cloud-service-with-cdn.md), [App Web](../app-service-web/app-service-web-tutorial-content-delivery-network.md) e [Servizi multimediali](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&#x2713;** |
| Gestione tramite [API REST](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) oppure [PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&amp;#x2713;** |**&#x2713;** |
| [Motore di distribuzione di contenuti personalizzabile, basato su regole](cdn-rules-engine.md) | | |**&#x2713;** |
| Impostazioni cache/intestazioni (con il [motore regole](cdn-rules-engine.md)) | | |**&amp;#x2713;** |
| Riscrittura/reindirizzamento URL (con il [motore regole](cdn-rules-engine.md)) | | |**&amp;#x2713;** |
| Regole per dispositivi mobili (con il [motore regole](cdn-rules-engine.md)) | | |**&#x2713;** |

\* Verizon supporta la distribuzione di file di grandi dimensioni e di file multimediali direttamente tramite la distribuzione Web generale.


> [!TIP]
> È una funzionalità che si desidera toosee nella rete CDN di Azure?  [Commenti e suggerimenti](https://feedback.azure.com/forums/169397-cdn) 
> 
> 

## <a name="next-steps"></a>Passaggi successivi
tooget avviato con una rete CDN, vedere [utilizzo della rete CDN di Azure](cdn-create-new-endpoint.md).

Nel caso di un cliente della rete CDN esistente, è ora possibile gestire gli endpoint rete CDN tramite hello [portale Microsoft Azure](https://portal.azure.com) o con [PowerShell](cdn-manage-powershell.md).

toosee hello CDN in azione, estrarre hello [video della sessione compilazione 2016](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Informazioni su come tooautomate rete CDN di Azure con [.NET](cdn-app-dev-net.md) o [Node.js](cdn-app-dev-node.md).

Per informazioni sui prezzi, vedere [Prezzi del servizio Rete di distribuzione dei contenuti (rete CDN)](https://azure.microsoft.com/pricing/details/cdn/).

