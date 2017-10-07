---
title: un servizio di ricerca di Azure nel portale di hello aaaCreate | Documenti Microsoft
description: Eseguire il provisioning di un servizio di ricerca di Azure nel portale di hello.
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a>Creare un servizio di ricerca di Azure nel portale di hello

Questo articolo spiega come toocreate o fornire una ricerca di Azure del servizio nel portale di hello. Per istruzioni su PowerShell vedere [Gestire il servizio Ricerca di Azure con PowerShell](search-manage-powershell.md).

## <a name="subscribe-free-or-paid"></a>Sottoscrizione gratuita o a pagamento

[Aprire un account gratuito di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) e usare i crediti tootry out a pagamento di servizi di Azure. Dopo crediti, tenere conto di hello e continuare toouse libero servizi di Azure, ad esempio siti Web. Carta di credito non viene addebitata mai a meno che non modificare le impostazioni in modo esplicito e chiedere toobe addebitati.

In alternativa, [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Con la sottoscrizione MSDN ogni mese si accumulano crediti che è possibile usare per i servizi di Azure a pagamento. 

## <a name="find-azure-search"></a>Trovare Ricerca di Azure
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Fare clic su hello sul segno più ("+") hello nell'angolo superiore sinistro.
3. Selezionare **Web e dispositivi mobili** > **Ricerca di Azure**.

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a>Servizio hello nome e l'URL endpoint

Un nome di servizio fa parte di endpoint dell'URL hello in cui vengono eseguite chiamate API. Digitare il nome di servizio in hello **URL** campo. 

Requisiti per i nomi di servizio:
   * lunghezza compresa tra 2 e 60 caratteri
   * uso di lettere minuscole, cifre o trattini ("-")
   * senza trattino ("-") come hello primi 2 caratteri o ultimo carattere singolo
   * nessun trattino consecutivo ("--")

## <a name="select-a-subscription"></a>Selezionare una sottoscrizione
Se sono disponibili più sottoscrizioni, sceglierne una che includa anche i servizi di archiviazione file o dati. Ricerca di Azure può automatico tabelle di Azure e l'archiviazione Blob e Database SQL Azure Cosmos DB per l'indicizzazione tramite *indicizzatori*, ma solo per i servizi in hello stessa sottoscrizione.

## <a name="select-a-resource-group"></a>Selezionare un gruppo di risorse
Un gruppo di risorse è una raccolta di servizi e risorse di Azure usati insieme. Ad esempio, se si utilizza una ricerca di Azure tooindex un database SQL, entrambi i servizi devono essere parte di hello stesso gruppo di risorse.

> [!TIP]
> L'eliminazione di un gruppo di risorse elimina anche i servizi di hello in esso contenuti. Per i progetti di prototipo che utilizzano più servizi, l'inserimento di tutti gli elementi in hello stesso gruppo di risorse semplifica la pulizia al termine del progetto hello. 

## <a name="select-a-hosting-location"></a>Selezionare un percorso di hosting 
Come servizio di Azure, ricerca di Azure possono essere ospitato nei Data Center in tutto il mondo hello. Tenere presente che i [prezzi possono variare](https://azure.microsoft.com/pricing/details/search/) in funzione dell'area geografica.

## <a name="select-a-pricing-tier-sku"></a>Selezionare un piano tariffario (SKU)
[Ricerca di Azure attualmente è disponibile con vari piani tariffari](https://azure.microsoft.com/pricing/details/search/): Gratuito, Basic o Standard. Ogni piano tariffario prevede una specifica [capacità e limiti](search-limits-quotas-capacity.md). Per indicazioni, vedere [Scegliere uno SKU o un piano tariffario per Ricerca di Azure](search-sku-tier.md) .

In questa procedura dettagliata, abbiamo scelto livello Standard hello per il servizio.

## <a name="create-your-service"></a>Creare il servizio

Tenere presente toopin dashboard toohello servizi per semplificare l'accesso ogni volta che accedi.

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a>Ridimensionare il servizio
Può richiedere alcuni minuti toocreate un servizio (15 minuti o più in base al livello hello). Dopo il provisioning del servizio, è possibile applicarvi la scalabilità toomeet le proprie esigenze. Poiché si è scelto di livello Standard hello per il servizio di ricerca di Azure, è possibile scalare il servizio in due dimensioni: partizioni e repliche. Si è scelto livello Basic hello, è possibile aggiungere solo le repliche. Se è stato eseguito il provisioning servizio gratuito hello, la scala non è disponibile.

***Partizioni*** consentire il servizio toostore e ricerca in più documenti.

***Repliche*** consentire toohandle il servizio di un carico superiore delle query di ricerca.

> [!Important]
> Un servizio deve disporre di [2 repliche per ogni contratto di servizio di sola lettura e 3 repliche per ogni contratto di servizio di lettura/scrittura](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

1. Andare a pannello di servizio di ricerca tooyour nel portale di Azure hello.
2. Nel riquadro di navigazione a sinistra di hello, selezionare **impostazioni** > **scala**.
3. Utilizzare hello slidebar tooadd repliche o partizioni.

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> Ogni livello presenta diversi [limiti](search-limits-quotas-capacity.md) al numero totale di hello di unità di ricerca è consentito in un singolo servizio (repliche * partizioni = totale delle unità di ricerca).

## <a name="when-tooadd-a-second-service"></a>Quando un secondo servizio tooadd

Maggioranza dei clienti di utilizzare un solo servizio eseguito il provisioning a un livello che fornisce hello [destro bilanciamento delle risorse](search-sku-tier.md). Un servizio può ospitare più indici, soggetto toohello [i limiti massimi di livello hello selezionate](search-capacity-planning.md), con ogni indice isolate una da altra. In ricerca di Azure, le richieste possono solo essere indice tooone diretto, riducendo al minimo il possibilità hello del recupero di dati accidentali o intenzionali dagli altri indici in hello stesso servizio.

Sebbene la maggior parte dei clienti utilizzano solo un servizio, ridondanza di servizio potrebbe essere necessaria se i requisiti operativi includono i seguenti di hello:

+ Ripristino di emergenza (interruzione del data center). Ricerca di Azure non fornisce il failover immediato in caso di hello di interruzione. Per consigli e informazioni aggiuntive, vedere [Amministrazione del servizio](search-manage.md).
+ L'analisi di modellazione di multi-tenancy ha determinato che servizi aggiuntivi progettazione ottimale hello. Per altre informazioni, vedere [Progettazione per multi-tenancy](search-modeling-multitenant-saas-applications.md).
+ Per le applicazioni distribuite globalmente, potrebbero essere necessari più latenza toominimize di aree del traffico internazionale dell'applicazione di un'istanza di ricerca di Azure.

> [!NOTE]
> In Ricerca di Azure, non è possibile isolare i carichi di lavoro di indicizzazione ed esecuzione di query, pertanto, non è possibile creare più servizi per i carichi di lavoro isolati. Un indice viene sempre eseguita una query sul servizio hello in cui è stata creata (è possibile creare un indice in un servizio e copiarlo tooanother).
>

Non è necessario un secondo servizio per la disponibilità elevata. Disponibilità elevata per le query avviene quando si utilizza 2 o più repliche in hello stesso servizio. Gli aggiornamenti di replica sono sequenziali, il che significa che almeno uno è operativo quando viene implementato un aggiornamento del servizio. Per altre informazioni sul tempo di attività, vedere i [Contratti di servizio](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

## <a name="next-steps"></a>Passaggi successivi
Dopo il provisioning di un servizio di ricerca di Azure, si è pronti troppo[definire un indice](search-what-is-an-index.md) in modo è possibile caricare e cercare i dati.

servizio hello tooaccess dal codice o script, specificare l'URL di hello (*-nome del servizio*. diventano <nome>.Search.Windows.NET) e una chiave. Le chiavi di amministrazione concedono l'accesso completo; le chiavi di query concedono l'accesso in sola lettura. Vedere [come toouse ricerca di Azure in .NET](search-howto-dotnet-sdk.md) tooget avviato.

Vedere [Compilare ed eseguire una query del primo indice](search-get-started-portal.md) per una rapida esercitazione basata sul portale.

