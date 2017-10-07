---
title: Panoramica di Endpoint di Streaming di servizi multimediali aaaAzure | Documenti Microsoft
description: Questo argomento offre una panoramica degli endpoint di streaming dei Servizi multimediali di Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 097ab5e5-24e1-4e8e-b112-be74172c2701
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: f27f590175dcc945d1d3299fc0cae5a68cfbf4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-endpoints-overview"></a>Panoramica degli endpoint di streaming 

##<a name="overview"></a>Panoramica

In Microsoft Azure Media Services (AMS), un **Endpoint di Streaming** rappresenta un servizio di streaming in grado di fornire contenuto direttamente applicazione di lettore client tooa o tooa rete di contenuti (CDN) per ulteriore distribuzione. Servizi multimediali fornisce inoltre un'integrazione completa della rete CDN di Azure. flusso in uscita di Hello da un servizio StreamingEndpoint può essere un flusso in tempo reale, un video su richiesta o il download progressivo dell'asset nell'account di servizi multimediali. Ogni account di Servizi multimediali di Azure include un servizio StreamingEndpoint predefinito. È possibile creare le entità Streamingendpoint ulteriori account hello. Esistono due versioni di servizi StreamingEndpoint, ovvero 1.0 e 2.0. A partire dal 10 gennaio 2017, ogni account di AMS appena creato includerà lo StreamingEndpoint **predefinito** della versione 2.0. Aggiungere account toothis endpoint di streaming aggiuntive saranno anche versione 2.0. Questa modifica non avrà impatto sulle account esistenti hello; le entità Streamingendpoint esistente sarà la versione 1.0 e può essere aggiornato tooversion 2.0. Con questa modifica verrà esserci modifiche di comportamento, fatturazione e funzionalità (per ulteriori informazioni, vedere hello **Streaming tipi e le versioni** sezione documentati di seguito).

Inoltre, a partire dalla versione di hello 2.15 (rilasciato nel gennaio January 2017), servizi multimediali di Azure aggiunti hello seguenti entità Endpoint di Streaming di proprietà toohello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Per una panoramica dettagliata di queste proprietà, vedere [questo articolo](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

Quando si crea un account di servizi multimediali di Azure predefinito endpoint di streaming standard viene creato in hello **arrestato** stato. È possibile eliminare l'endpoint di streaming predefinito di hello. A seconda della disponibilità di rete CDN di Azure nell'area di destinazione hello hello, per impostazione predefinita predefinito appena creato endpoint di streaming include anche "StandardVerizon" CDN integrazione provider. 

>[!NOTE]
>Integrazione della rete CDN di Azure può essere disabilitato prima di avviare l'endpoint di streaming hello.

In questo argomento fornisce una panoramica delle funzionalità principali di hello forniti dall'endpoint di streaming.

## <a name="streaming-types-and-versions"></a>Tipologie e versioni di streaming

### <a name="standardpremium-types-version-20"></a>Tipologia standard o Premium (versione 2.0)

A partire dalla versione di gennaio January 2017 hello di servizi multimediali, sono presenti due tipi di flusso: **Standard** e **Premium**. Questi tipi sono parte di una versione di endpoint di Streaming hello "2.0".

Tipo|Descrizione
---|---
**Standard**|Si tratta di opzione predefinito hello utilizzabili per la maggior parte di hello degli scenari di hello.<br/>Con questa opzione, si ottiene contratto di servizio predefinito/limitata, primi 15 giorni dopo l'avvio di hello endpoint di streaming è disponibile.<br/>Se si crea più di un endpoint di streaming, solo hello prima uno è gratuito per hello 15 giorni prima, altri vengono fatturati non appena si avvia li hello. <br/>Si noti che versione di valutazione gratuita si applica solo toonewly creato gli account di servizi multimediali e di endpoint di streaming predefinito. Gli endpoint di streaming esistenti e inoltre creati gli endpoint di streaming non include versione di valutazione gratuita periodo anche siano aggiornati tooversion 2.0 oppure vengono creati come versione 2.0.
**Premium**|Questa opzione è adatta ai professionisti che hanno bisogno di una maggiore scalabilità o di maggior controllo.<br/>Diversi tipi di contratto di servizio in base alla capacità dell'unità di streaming (SU) premium acquistata, endpoint di streaming live dedicati in un ambiente isolato e nessuna competizione per le risorse.

Per ulteriori informazioni, vedere hello **Streaming confrontare tipi** seguente sezione.

### <a name="classic-type-version-10"></a>Tipologia classica (versione 1.0)

Per gli utenti che ha creato gli account di sistema AMS toohello precedente versione di gennaio January 2017 10, è necessario un **classico** tipo di un endpoint di streaming. Questo tipo è parte di hello streaming endpoint versione "1.0".

Se il **versione "1.0"** endpoint di streaming è > = 1 premium (SU), unità di streaming sarà l'endpoint di streaming premium e fornirà tutte le funzionalità di sistema AMS (analogamente hello **Standard o Premium** tipo) senza ulteriori passaggi di configurazione.

>[!NOTE]
>Gli endpoint di streaming **classici** (versione "1.0" e 0 SU), offrono funzionalità limitate e non includono un contratto di servizio. È consigliabile toomigrate**Standard** digitare tooget una migliore esperienza toouse funzionalità come la crittografia o creazione dinamica dei pacchetti e altre funzionalità fornite con hello **Standard** tipo. toomigrate toohello **Standard** digitare, visitare toohello [portale di Azure](https://portal.azure.com/) e selezionare **prevede il consenso esplicito tooStandard**. Per ulteriori informazioni sulla migrazione, vedere hello [migrazione](#migration-between-types) sezione.
>
>Tenere presente che questa operazione non può essere sottoposta a rollback e influisce sul prezzo.
>
 
## <a name="comparing-streaming-types"></a>Confronto tra le tipologie di streaming

### <a name="versions"></a>Versioni

|Tipo|StreamingEndpointVersion|ScaleUnits|RETE CDN|Fatturazione|Contratto di servizio| 
|--------------|----------|-----------------|-----------------|-----------------|-----------------|    
|Classico|1.0|0|ND|Free|ND|
|Endpoint di streaming Standard|2.0|0|Sì|A pagamento|Sì|
|Unità di streaming Premium|1.0|>0|Sì|A pagamento|Sì|
|Unità di streaming Premium|2.0|>0|Sì|A pagamento|Sì|

### <a name="features"></a>Funzionalità

Funzionalità|Standard|Premium
---|---|---
Gratis per i primi 15 giorni| Sì |No
Velocità effettiva |Backup too600 Mbps quando non viene utilizzata la rete CDN Azure. Scalabilità con la rete CDN.|200 Mbps per unità di streaming (SU). Scalabilità con la rete CDN.
Contratto di servizio | 99,9|99,9 (200 Mbps per SU).
RETE CDN|Rete CDN di Azure, rete CDN di terze parti o nessuna rete CDN.|Rete CDN di Azure, rete CDN di terze parti o nessuna rete CDN.
Fatturazione con ripartizione proporzionale| Giornaliera|Giornaliera
Crittografia dinamica|Sì|Sì
creazione dinamica dei pacchetti|Sì|Sì
Scalabilità|Velocità effettiva toohello destinata passa automaticamente.|Unità di streaming aggiuntive
Host con filtro IP/G20/personalizzato|Sì|Sì
Download progressivo|Sì|Sì
Uso consigliato |Consigliato per hello gran parte gli scenari di flusso.|Uso professionale.<br/>Per esigenze superiori alle funzionalità offerte dalla tipologia Standard. Se si prevede un numero di destinatari simultanei superiore a 50.000 visualizzatori, contattare Microsoft (amsstreaming all'indirizzo microsoft.com).


## <a name="migration-between-types"></a>Migrazione tra le tipologie

Da | Anche| Azione
---|---|---
Classico|Standard|È necessario tooopt-in
Classico|Premium| Scalabilità (unità di streaming aggiuntive)
Standard/Premium|Classico|Non disponibile (se la versione dell'endpoint di streaming è 1.0. È consentito tooclassic toochange con l'impostazione di proprietà scaleunits troppo "0")
Standard (con/senza la rete CDN)|Premium con hello stesse configurazioni|È consentito in hello **avviato** stato. (tramite il Portale di Azure)
Premium (con/senza la rete CDN)|Standard con hello stesse configurazioni|È consentito in hello **avviato** stato (tramite il portale di Azure)
Standard (con/senza la rete CDN)|Premium con diverse configurazioni|È consentito in hello **arrestato** stato (tramite il portale di Azure). Non è consentito in hello dello stato di esecuzione.
Premium (con/senza la rete CDN)|Standard con diverse configurazioni|È consentito in hello **arrestato** stato (tramite il portale di Azure). Non è consentito in hello dello stato di esecuzione.
Versione 1.0 con SU >=1 con la rete CDN|Standard/Premium con nessuna rete CDN|È consentito in hello **arrestato** stato. Non è consentito in hello **avviato** stato.
Versione 1.0 con SU >=1 con la rete CDN|Standard con/senza la rete CDN|È consentito in hello **arrestato** stato. Non è consentito in hello **avviato** stato. Verrà eliminata la rete CDN della versione 1.0 e ne verrà creata e avviata una nuova.
Versione 1.0 con SU >=1 con la rete CDN|Premium con/senza la rete CDN|È consentito in hello **arrestato** stato. Non è consentito in hello **avviato** stato. Verrà eliminata la rete CDN della tipologia classica e ne verrà creata e avviata una nuova.

## <a name="next-steps"></a>Passaggi successivi
Analizzare i percorsi di apprendimento di Servizi multimediali.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

