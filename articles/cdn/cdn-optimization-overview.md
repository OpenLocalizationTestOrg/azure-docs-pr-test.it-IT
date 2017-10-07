---
title: distribuzione di contenuti di Azure per lo scenario aaaOptimize
description: Come toooptimize recapito del contenuto per scenari specifici
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Ottimizzare la distribuzione del contenuto di Azure per lo scenario in uso

Quando si consegna tooa contenuto pubblico globale, si tratta di importanti tooensure hello con ottimizzazione per la consegna del contenuto. Hello Azure Content Delivery Network possibile ottimizzare l'esperienza di recapito hello in base al tipo di hello del contenuto di cui che si dispone. Il contenuto può essere un sito Web, uno streaming live, un video o un file di grandi dimensioni per il download. Quando si crea un endpoint di distribuzione di contenuti (CDN) di rete, si specifica un scenario in hello **ottimizzato per** opzione. La scelta determina quali ottimizzazione è applicato toohello contenuto recapitato dall'endpoint rete CDN hello.

Opzioni di ottimizzazione sono progettate toouse comportamenti di procedure consigliate tooimprove contenuti prestazioni e offload origine migliori. Le scelte di scenario influire sulle prestazioni modificando le configurazioni per la memorizzazione nella cache parziale, la suddivisione in blocchi di oggetti e criteri di ripetizione di hello origine errore. 

Questo articolo offre una panoramica delle varie funzionalità di ottimizzazione e dello scenario in cui usarle. Per ulteriori informazioni sulle funzionalità e limitazioni, vedere articoli hello in ogni tipo di ottimizzazione singoli.

> [!NOTE]
> Il **ottimizzato per** opzioni possono variare in base ai provider di hello selezionato. Provider CDN disponibili miglioramento applicano in modi diversi, a seconda dello scenario di hello. 

## <a name="provider-options"></a>Opzioni del provider

Hello rete CDN di Azure da Akamai supporta:

* Distribuzione Web generale 

* Streaming multimediale generale

* Streaming multimediale di video on demand

* Download di file di grandi dimensioni

* Accelerazione sito dinamico 

Hello Azure Content Delivery Network da Verizon supporta solo il recapito di web generali. Può essere usata per scaricare video on demand e file di grandi dimensioni. Tooselect non è un tipo di ottimizzazione.

Si consiglia di testare le variazioni delle prestazioni tra provider ottimale hello tooselect di provider diversi per il recapito.

## <a name="select-and-configure-optimization-types"></a>Selezionare e configurare i tipi di ottimizzazione

toocreate un nuovo endpoint, selezionare un tipo di ottimizzazione che corrisponde maggiormente scenario hello e tipo di contenuto che si desidera hello toodeliver endpoint. **Recapito web generali** è l'opzione predefinita di hello. È possibile aggiornare l'opzione di ottimizzazione hello per qualsiasi endpoint Akamai esistente in qualsiasi momento. Questa modifica non interrompa il recapito da hello CDN. 

1. Selezionare un endpoint all'interno di un profilo Akamai Standard.

    ![Selezione dell'endpoint ](./media/cdn-optimization-overview/01_Akamai.png)

2. In **IMPOSTAZIONI** selezionare **Ottimizzazione**. Selezionare un tipo hello **ottimizzato per** elenco a discesa.

    ![Selezione dell'ottimizzazione e del tipo](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Ottimizzazione per scenari specifici

È possibile ottimizzare l'endpoint rete CDN hello per uno dei seguenti scenari hello. 

### <a name="general-web-delivery"></a>Distribuzione Web generale

Recapito web generale è opzione di ottimizzazione hello più comuni. È mirata per l'ottimizzazione di contenuto Web generale, ad esempio pagine Web e applicazioni Web. Può essere usata anche per i download di file e video.

Un sito Web tipico contiene contenuto statico e dinamico. Contenuto statico include immagini, le librerie JavaScript e fogli di stile che possono essere memorizzati nella cache e recapitati toodifferent utenti. Contenuto dinamico personalizzato per un singolo utente, ad esempio notizie che sono specifici del profilo utente tooa. Contenuto dinamico non è memorizzato nella cache perché è univoco tooeach utente, ad esempio shopping cart contenuto. La distribuzione Web generale consente di ottimizzare l'intero sito Web. 

> [!NOTE]
> Se si utilizza Azure Content Delivery Network da Akamai hello, è consigliabile toouse questa ottimizzazione se le dimensioni medie dei file sono inferiori a 10 MB. Se le dimensioni medie dei file sono maggiori di 10 MB, selezionare **download di file di grandi dimensioni** da hello **ottimizzato per** elenco a discesa.

### <a name="general-media-streaming"></a>Streaming multimediale generale

Se è necessario endpoint hello toouse per lo streaming live e lo streaming video on Demand, è consigliabile supporto generale di ottimizzazione del flusso.

Flussi multimediali è ora sensibile, poiché i pacchetti che arrivano in ritardo sul client hello possono causare un'esperienza di visualizzazione ridotte, ad esempio il buffer frequenti di contenuti video. Ottimizzazione dei flussi multimediali riducono la latenza di hello di recapito contenuti multimediali e offre un'esperienza di smooth streaming per gli utenti. 

Si tratta di uno scenario comune per i clienti di servizi multimediali di Azure. Quando si usano i servizi multimediali di Azure, si otterrà un endpoint di streaming che può essere usato per lo streaming live e on demand. Con questo scenario, i clienti non devono tooswitch tooanother endpoint quando vengono modificate da streaming in tempo reale tooon richiesta. L'ottimizzazione dello streaming multimediale generale supporta questo tipo di scenario.

Hello Azure Content Delivery Network da Verizon utilizza hello web generali recapito ottimizzazione tipo toodeliver contenuti multimediali.

vedere toolearn ulteriori informazioni sull'ottimizzazione, i flussi multimediali [ottimizzazione dei flussi multimediali](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Streaming multimediale di video on demand

L'ottimizzazione dello streaming multimediale di video on demand migliora il contenuto dello streaming di video on demand. Se si utilizza un endpoint di streaming video on Demand, è possibile toouse questa opzione.

Hello Azure Content Delivery Network da Verizon utilizza hello web generali recapito ottimizzazione tipo toodeliver contenuti multimediali.

vedere toolearn ulteriori informazioni sull'ottimizzazione, i flussi multimediali [ottimizzazione dei flussi multimediali](cdn-media-streaming-optimization.md).

> [!NOTE]
> Endpoint hello viene principalmente utilizzata contenuto video on Demand, è possibile utilizzare questo tipo di ottimizzazione. Hello principale differenza tra questa ottimizzazione e l'ottimizzazione del flusso di supporto generali hello è timeout del tentativo di connessione hello. timeout di Hello è molto più breve toowork con scenari di streaming live.

### <a name="large-file-download"></a>Download di file di grandi dimensioni

Se si utilizza Azure Content Delivery Network da Akamai hello, è necessario utilizzare il file toodeliver di download file di grandi dimensioni è maggiore di 1,8 GB. Hello Azure Content Delivery Network da Verizon non dispone di una limitazione nei file di dimensioni nell'ottimizzazione di recapito web generali del download.

Se si utilizza Azure Content Delivery Network da Akamai hello, download di file di grandi dimensioni sono ottimizzati per il contenuto di dimensioni maggiore di 10 MB. Se le dimensioni medie dei file sono inferiori a 10 MB, si consiglia di recapito web generali toouse. Se le dimensioni di file medio sono sempre maggiori di 10 MB, potrebbe essere più efficiente toocreate un endpoint separato per i file di grandi dimensioni. Ad esempio, gli aggiornamenti firmware o software sono in genere file di grandi dimensioni.

Hello Azure Content Delivery Network da Verizon utilizza hello web generali recapito ottimizzazione tipo toodeliver contenuti multimediali.

toolearn ulteriori informazioni sull'ottimizzazione del file di grandi dimensioni, vedere [ottimizzazione di file di grandi dimensioni](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Accelerazione sito dinamico

 L'accelerazione del sito dinamico è disponibile dai profili di rete per la distribuzione di contenuti di Akamai e Verizon. Questa ottimizzazione è necessario un toouse addizionale. Per ulteriori informazioni, vedere hello pagina dei prezzi.

Accelerazione di sito dinamico include diverse tecniche che traggono vantaggio latenza hello e le prestazioni di contenuto dinamico. Le tecniche includono l'ottimizzazione di route e rete, l'ottimizzazione TCP e molto altro. 

È possibile utilizzare questo tooaccelerate ottimizzazione un'app web che include numerose risposte non memorizzabile nella cache. I risultati di ricerca, le transazioni di checkout o i dati in tempo reale sono degli esempi. È possibile continuare toouse CDN memorizzazione nella cache le funzionalità di base per i dati statici. 



