---
title: pianificazione per la ricerca di Azure aaaCapacity | Documenti Microsoft
description: "Regolare le risorse di calcolo, ovvero partizioni e repliche, dove il prezzo di ogni risorsa è definito in unità di ricerca fatturabili, in Ricerca di Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Ridimensionare i livelli di risorse per i carichi di lavoro di indicizzazione e query in Ricerca di Azure
Dopo aver [scegliere un piano tariffario](search-sku-tier.md) e [il provisioning di un servizio di ricerca](search-create-service-portal.md), hello sarà toooptionally aumento hello più repliche o partizioni utilizzate dal servizio. Ogni livello offre un numero fisso di unità di fatturazione. Questo articolo viene illustrato come tooallocate tali tooachieve unità una configurazione ottimale che consente di bilanciare i requisiti per l'esecuzione di query, indicizzazione e l'archiviazione.

Configurazione di risorsa è disponibile quando si configura un servizio in hello [livello Basic](http://aka.ms/azuresearchbasic) o uno dei hello [livelli Standard](search-limits-quotas-capacity.md). Per tutti i servizi fatturabili di questi livelli è possibile acquistare capacità a incrementi di *unità di ricerca* (SU). Le singole partizioni e repliche vengono considerate come una unità di ricerca. 

Usando un numero minore di risultati SU in una fattura proporzionalmente inferiore. La fatturazione è attiva per purché hello servizio sia configurato. Se è temporaneamente non si utilizza un servizio, l'unico modo hello tooavoid fatturazione consiste nell'eliminazione del servizio hello e quindi ricrearlo quando è necessario.

> [!Note]
> Eliminando un servizio si elimina tutto il suo contenuto. Non sono disponibili funzionalità all'interno di Ricerca di Azure per eseguire il backup e il ripristino dei dati di ricerca permanenti. tooredeploy un indice esistente in un nuovo servizio, eseguire toocreate programma utilizzato hello e caricarlo in origine. 

## <a name="terminology-partitions-and-replicas"></a>Terminologia: partizioni e repliche
Partizioni e repliche sono risorse hello primaria eseguire il backup di un servizio di ricerca.

| Risorsa | Definizione |
|----------|------------|
|*Partizioni* | Offre l'archiviazione degli indici e l'I/O per le operazioni di lettura e scrittura, ad esempio durante la compilazione o l'aggiornamento di un indice.|
|*Repliche* | Le istanze del servizio di ricerca hello, utilizzate principalmente tooload bilanciare le operazioni di query. Ogni replica ospita sempre una copia di un indice. Se si dispongono di 12 repliche, sarà necessario 12 copie di ogni indice caricati nel servizio hello.|

> [!NOTE]
> Non è possibile modificare o gestire gli indici che eseguito su una replica di toodirectly. Una copia di ogni indice in ogni replica è parte dell'architettura del servizio hello.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Come tooallocate partizioni e repliche
In Ricerca di Azure viene allocato inizialmente a un servizio un livello minimo di risorse costituito da una partizione e una replica. Per i livelli che lo supportano, è possibile regolare in modo incrementale le risorse di elaborazione aumentando le partizioni se si ha bisogno di maggiore spazio di archiviazione e I/O o aggiungendo più repliche per volumi di query maggiori o migliori prestazioni. Un singolo servizio deve avere sufficiente risorse toohandle tutti i carichi di lavoro (l'indicizzazione e query). Non è possibile suddividere i carichi di lavoro tra più servizi.

allocazione di hello tooincrease o modifica di partizioni e repliche, è consigliabile utilizzare hello portale di Azure. portale Hello impone limiti di combinazioni consentite che rimangono i limiti massimi di seguito:

1. Accedi toohello [portale di Azure](https://portal.azure.com/) e selezionare il servizio di ricerca di hello.
2. In **impostazioni**aprire hello **scala** pannello e utilizzare hello tooincrease dispositivi di scorrimento o ridurre il numero di hello di partizioni e repliche.

Se si richiede un approccio di provisioning basato su codice o script, hello [API REST di gestione](https://msdn.microsoft.com/library/azure/dn832687.aspx) è un portale toohello alternativo.

In genere, le applicazioni di ricerca richiede più repliche che partizioni, in particolare quando le operazioni del servizio hello sono sbilanciate verso i carichi di lavoro di query. Hello sezione su [la disponibilità elevata](#HA) spiega il motivo.

> [!NOTE]
> Dopo il provisioning di un servizio, non può essere aggiornato tooa SKU superiore. Sarà anche necessario toocreate un servizio di ricerca a livello di nuovo hello e ricaricare gli indici. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per assistenza con il provisioning del servizio.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Disponibilità elevata
Poiché è semplice e rapido relativamente tooscale backup, è consigliabile in genere si inizia con una partizione e uno o due repliche e quindi scalabilità verticale come volumi di query di compilazione. Per molti servizi in livelli di base o S1 hello, una partizione fornisce l'archiviazione e i/o sufficienti (in 15 milioni di documenti per partizione).

I carichi di lavoro di query vengono eseguiti principalmente nelle repliche. Se è necessaria maggiore velocità effettiva o una disponibilità elevata, probabilmente saranno necessarie repliche aggiuntive.

Le indicazioni generali per la disponibilità elevata sono:

* Due repliche per la disponibilità elevata di carichi di lavoro di sola lettura, vale a dire query.
* Tre o più repliche per la disponibilità elevata dei carichi di lavoro di lettura e scrittura, vale a dire query e indicizzazione man mano che singoli documenti vengono aggiunti, aggiornati o eliminati.

I contratti di servizio per Ricerca di Azure sono associati a operazioni di query e aggiornamenti di indici che consistono nell'aggiunta, l'aggiornamento o l'eliminazione di documenti.

### <a name="index-availability-during-a-rebuild"></a>Disponibilità degli indici durante la ricompilazione

Disponibilità elevata per la ricerca di Azure relativo aggiornamenti tooqueries e indice che non comportano la ricompilazione dell'indice. Se si elimina un campo, modificare il tipo di dati o rinominare un campo, è necessario indice hello toorebuild. indice di hello toorebuild, è necessario eliminare hello di indice, ricreare l'indice di hello e ricaricare i dati di hello.

> [!NOTE]
> È possibile aggiungere nuovo indice di ricerca di Azure tooan campi senza ricompilare l'indice di hello. il valore di Hello del nuovo campo hello sarà null per tutti i documenti già nell'indice hello.

disponibilità di indice toomaintain durante un'operazione di ricompilazione, è necessario disporre una copia dell'indice hello con un nome diverso in hello stesso servizio oppure una copia di hello indice con hello stesso nome in un altro servizio e quindi fornire la logica di reindirizzamento o di failover nel codice.

## <a name="disaster-recovery"></a>Ripristino di emergenza
Attualmente, non esiste alcun meccanismo incorporato per il ripristino di emergenza. Aggiunta di partizioni o repliche sarebbe strategia errato di hello per soddisfare gli obiettivi di ripristino di emergenza. approccio più comune di Hello è tooadd ridondanza a livello di servizio hello configurando un secondo servizio di ricerca in un'altra area. Come con la disponibilità durante la ricompilazione di un indice, il reindirizzamento di hello o logica di failover deve provenire dal codice.

## <a name="increase-query-performance-with-replicas"></a>Aumentare le prestazioni delle query con le repliche
La latenza delle query indica che sono necessarie repliche aggiuntive. In genere, un primo passo per migliorare le prestazioni delle query è tooadd più tale risorsa. Quando si aggiungono repliche, copie aggiuntive dell'indice hello vengono attivata la modalità online toosupport più grande carichi di lavoro di query e hello saldo tooload le richieste attraverso hello più repliche.

Non è possibile fornire le stime di disco rigide per le query al secondo (query al secondo): query prestazioni dipendono dalla complessità di hello di hello query e carichi di lavoro concorrenti. In media, una replica agli SKU Basic o S1 può soddisfare circa 15 QPS, ma la velocità effettiva sarà leggermente superiore o inferiore a seconda della complessità della query (le query con facet sono più complesse) e della latenza di rete. Inoltre, è importante toorecognize che anche se l'aggiunta di repliche comporti indubbiamente un aumento scalabilità e prestazioni, hello risultato non è perfettamente lineare: aggiunta di tre repliche non garantisce triplo della velocità effettiva.

toolearn sulla query al secondo, tra cui gli approcci per la stima delle query al secondo per i carichi di lavoro, vedere [gestire il servizio di ricerca](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>Aumentare le prestazioni dell'indicizzazione con le partizioni
Le applicazioni di ricerca che richiedono l'aggiornamento dei dati quasi in tempo reale avranno bisogno in proporzione di più partizioni che repliche. L'aggiunta di partizioni distribuisce le operazioni di lettura/scrittura su un numero più ampio di risorse di calcolo. Offre inoltre più spazio su disco per l'archiviazione di documenti e indici aggiuntivi.

Gli indici di dimensioni maggiori hanno tooquery più lungo. Di conseguenza, si noterà che ogni aumento incrementale delle partizioni richiede un aumento delle repliche proporzionale ma più limitato. complessità Hello delle query e il volume di query è necessario tenere conto rapidità con cui l'esecuzione di query è attivato.

## <a name="basic-tier-partition-and-replica-combinations"></a>Livello Basic: combinazioni di partizioni e repliche
Un servizio di base può avere esattamente una partizione e configurare le repliche toothree, per un massimo di tre SUs. risorsa solo regolabile Hello è repliche. Per la disponibilità elevata relativa alle query è necessario un minimo di due repliche.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Livello Standard: combinazioni di partizioni e repliche
Questa tabella mostra le combinazioni di hello SUs toosupport necessario di repliche e partizioni, limite di 36 SU toohello soggetto, per tutti i livelli Standard.

|   | **1 partizione** | **2 partizioni** | **3 partizioni** | **4 partizioni** | **6 partizioni** | **12 partizioni** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 replica.** |1 unità di ricerca |2 unità di ricerca |3 unità di ricerca |4 unità di ricerca |6 unità di ricerca |12 unità di ricerca |
| **2 repliche** |2 unità di ricerca |4 unità di ricerca |6 unità di ricerca |8 unità di ricerca |12 unità di ricerca |24 unità di ricerca |
| **3 repliche** |3 unità di ricerca |6 unità di ricerca |9 unità di ricerca |12 unità di ricerca |18 unità di ricerca |36 unità di ricerca |
| **4 repliche** |4 unità di ricerca |8 unità di ricerca |12 unità di ricerca |16 unità di ricerca |24 unità di ricerca |N/D |
| **5 repliche** |5 unità di ricerca |10 unità di ricerca |15 unità di ricerca |20 unità di ricerca |30 unità di ricerca |N/D |
| **6 repliche** |6 unità di ricerca |12 unità di ricerca |18 unità di ricerca |24 unità di ricerca |36 unità di ricerca |N/D |
| **12 repliche** |12 unità di ricerca |24 unità di ricerca |36 unità di ricerca |N/D |N/D |N/D |

SUs, prezzi e capacità sono illustrati in dettaglio nel sito Web di Azure hello. Per altre informazioni, vedere i [dettagli sui prezzi](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> numero di Hello di partizioni e repliche divide in modo uniforme in 12 (in particolare, 1, 2, 3, 4, 6, 12). In questo modo Ricerca di Azure divide preventivamente ogni indice in 12 partizioni in modo che possa essere distribuito ugualmente tra tutte le partizioni. Ad esempio, se il servizio dispone di tre partizioni e si crea un indice, ogni partizione conterrà quattro partizioni dell'indice hello. La modalità di partizionamento di ricerca di Azure un indice è un dettaglio di implementazione, soggetto toochange nelle versioni future. Anche se il numero di hello è 12, tuttavia aspettarsi che numero tooalways essere 12 in hello future.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>Formula di fatturazione per le risorse di replica e partizione
formula Hello per calcolare il numero di SUs vengono utilizzati per combinazioni specifiche è prodotto hello, partizioni e repliche o (P X R = SU). Ad esempio, tre repliche moltiplicate per tre partizioni vengono fatturate come nove unità di ricerca.

Costo SU è determinato dal livello di hello, con una tariffa di fatturazione per unità inferiore per Basic a Standard. Le tariffe per ogni livello sono disponibili in [Prezzi di Ricerca](https://azure.microsoft.com/pricing/details/search/).
