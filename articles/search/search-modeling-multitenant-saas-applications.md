---
title: aaaModeling multi-tenancy in ricerca di Azure | Documenti Microsoft
description: Informazioni sui modelli di progettazione comuni per le applicazioni SaaS multi-tenant quando si usa Ricerca di Azure.
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Modelli di progettazione per le applicazioni SaaS multi-tenant e Ricerca di Azure
Un'applicazione multi-tenant è uno hello fornisce la stessa funzionalità e i servizi tooany svariati tenant che non possono vedere o condividere i dati di hello di un altro tenant. Questo documento illustra le strategie di isolamento dei tenant per le applicazioni multi-tenant compilate con Ricerca di Azure.

## <a name="azure-search-concepts"></a>Concetti di Ricerca di Azure
Come soluzione ricerca-as-a-service, ricerca di Azure consente di ricerca avanzate di sviluppatori tooadd esperienze tooapplications senza gestire qualsiasi infrastruttura o diventare esperti di ricerca. Dati caricati toohello servizio e quindi archiviate nel cloud hello. Utilizza toohello semplici richieste API di ricerca di Azure, dati hello possono quindi essere modificati e la ricerca. Una panoramica del servizio hello è reperibile [questo articolo](http://aka.ms/whatisazsearch). Prima di esaminare i modelli di progettazione, è importante toounderstand alcuni concetti nella ricerca di Azure.

### <a name="search-services-indexes-fields-and-documents"></a>Servizi di ricerca, indici, campi e documenti
Quando si usa ricerca di Azure, uno sottoscrive tooa *servizio di ricerca*. Come dati caricati tooAzure ricerca, viene archiviata in un *indice* all'interno del servizio di ricerca hello. In un solo servizio possono essere presenti molti indici. toouse hello conoscere i concetti di database, il servizio di ricerca hello può essere paragonata tooa database mentre gli indici di hello all'interno di un servizio possono essere paragonate tootables all'interno di un database.

Ogni indice all'interno di un servizio di ricerca ha un proprio schema, definito da un certo numero di *campi*personalizzabili. Indice di ricerca di Azure tooan vengono aggiunti dati sotto forma di hello di singoli *documenti*. Deve essere caricato tooa particolare indice di ogni documento e deve essere contenuta dello schema di tale indice. Durante la ricerca di dati mediante ricerca di Azure, le query di ricerca full-text hello inviate a un particolare indice.  toocompare toothose questi concetti di un database, i campi possono essere paragonate toocolumns in una tabella e i documenti possono essere paragonate toorows.

### <a name="scalability"></a>Scalabilità
Qualsiasi servizio di ricerca di Azure in hello Standard [tariffario](https://azure.microsoft.com/pricing/details/search/) possibile scalare in due dimensioni: archiviazione e la disponibilità.

* *Partizioni* possono essere aggiunti archiviazione hello tooincrease di un servizio di ricerca.
* *Repliche* possono essere aggiunti tooa servizio tooincrease hello velocità di trasmissione di richieste in grado di gestire un servizio di ricerca.

Aggiunta e rimozione di partizioni e repliche a consentirà la capacità di hello di hello ricerca servizio toogrow con quantità hello di dati e il traffico di richieste dell'applicazione hello. Per consentire un tooachieve servizio di ricerca una lettura [contratto di servizio](https://azure.microsoft.com/support/legal/sla/search/v1_0/), richiede due repliche. In modo che un servizio tooachieve in lettura-scrittura [contratto di servizio](https://azure.microsoft.com/support/legal/sla/search/v1_0/), richiede tre repliche.

### <a name="service-and-index-limits-in-azure-search"></a>Limiti dei servizi e degli indici in Ricerca di Azure
Ci sono alcuni diversi [i livelli di prezzo](https://azure.microsoft.com/pricing/details/search/) in ricerca di Azure, ognuno dei livelli di hello presenta diversi [limiti e quote](search-limits-quotas-capacity.md). Alcuni di questi limiti sono hello a livello di servizio, alcune sono a livello di indice hello e alcuni sono a livello di partizione hello.

|  | Basic | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Massimo numero di repliche per servizio |3 |12 |12 |12 |12 |
| Massimo numero di partizioni per servizio |1 |12 |12 |12 |1 |
| Massimo numero di unità di ricerca (repliche * partizioni) per servizio |3 |36 |36 |36 |36 (max 3 partizioni) |
| Massimo numero di documenti per servizio |1 milione |180 milioni |720 milioni |1,4 miliardi |600 milioni |
| Massimo spazio di archiviazione per servizio |2 GB |300 GB |1,2 TB |2,4 TB |600 GB |
| Massimo numero di documenti per partizione |1 milione |15 milioni |60 milioni |120 milioni |200 milioni |
| Massimo spazio di archiviazione per partizione |2 GB |25 GB |100 GB |200 GB |200 GB |
| Massimo numero di indici per servizio |5 |50 |200 |200 |3000 (max 1000 indici/partizione) |

#### <a name="s3-high-density"></a>S3 ad alta densità
Nel livello di prezzo S3 della ricerca di Azure, è disponibile un'opzione per la modalità di densità elevata (HD) hello appositamente progettata per scenari multi-tenant. In molti casi, è necessario toosupport un numero elevato di tenant più piccoli in vantaggi di hello tooachieve un singolo servizio di semplicità e costi ridotti.

S3 HD consente hello molti indici di dimensioni toobe compressi in Gestione hello di un servizio di ricerca singola dal commerciali hello possibilità tooscale gli indici di utilizzo di partizioni per hello possibilità toohost più indici in un singolo servizio.

In concreto, un servizio S3 potrebbe essere compresi tra 1 e 200 indici che può ospitare contemporaneamente i miliardi documenti too1.4. Un HD S3 su hello invece consentirebbe singoli indici tooonly salire too1 milioni documenti, ma in grado di gestire backup too1000 indici per ogni partizione (backup too3000 per ogni servizio) con un numero di documenti totale di 200 milioni per partizione (backup too600 milioni di servizio).

## <a name="considerations-for-multitenant-applications"></a>Considerazioni per le applicazioni multi-tenant
Applicazioni multi-tenant devono distribuire efficacemente i risorse fra tenant hello mantenendo un certo livello di privacy tra hello tenant diversi. Quando si progetta l'architettura di hello per tale applicazione, esistono alcune considerazioni:

* *L'isolamento del tenant:* gli sviluppatori di applicazioni è necessario tootake le misure appropriate tooensure che nessun tenant non autorizzato o indesiderato di accedere ai dati toohello di altri tenant. Oltre a prospettiva hello della privacy dei dati, strategie di isolamento tenant richiedono efficienti di gestione delle risorse condivise e la protezione da altre istanze rumore.
* *Costi delle risorse del cloud:* come con qualsiasi altra applicazione, le soluzioni software devono rimanere competitive quando sono componenti di un'applicazione multi-tenant.
* *Facilità di operazioni:* durante lo sviluppo di un'architettura multi-tenant, hello impatto sulle operazioni dell'applicazione hello e complessità è importante tenere in considerazione. Ricerca di Azure ha un [contratto di servizio del 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Footprint globale:* applicazioni multi-tenant potrebbe essere necessario tooeffectively serve tenant che vengono distribuite tra globo hello.
* *Scalabilità:* gli sviluppatori di applicazioni è necessario tooconsider come cui risolvere le differenze tra un sufficientemente basso livello di complessità dell'applicazione di gestione e progettazione tooscale applicazione hello con numero di tenant e dimensioni dei dati dei tenant hello e carico di lavoro.

Ricerca di Azure offre alcuni limiti che possono essere utilizzati tooisolate tenant dati e il carico di lavoro.

## <a name="modeling-multitenancy-with-azure-search"></a>Modellazione del multi-tenancy con Ricerca di Azure
In caso di hello di scenario multi-tenant, sviluppatore dell'applicazione hello utilizza uno o più servizi di ricerca e dividere i tenant tra servizi, gli indici o entrambi. Ricerca di Azure dispone di alcuni modelli comuni per la modellazione di uno scenario multi-tenant:

1. *Indice per tenant:* ogni tenant dispone di un proprio indice all'interno di un servizio di ricerca che è condiviso con altri tenant.
2. *Servizio per tenant:* ogni tenant dispone di un proprio servizio Ricerca di Azure dedicato, il che offre un livello più elevato di separazione dei dati e del carico di lavoro.
3. *Combinazione di entrambi:* ai tenant più grandi e attivi vengono assegnati servizi dedicati mentre ai tenant più piccoli vengono assegnati singoli indici all'interno di servizi condivisi.

## <a name="1-index-per-tenant"></a>1. Indice per tenant
![Un'immagine del modello di indice per tenant hello](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

In un modello "indice per tenant", più tenant occupano un singolo servizio di Ricerca di Azure in cui ogni tenant dispone di un proprio indice.

I tenant ottengono l'isolamento dei dati perché tutte le richieste di ricerca e le operazioni sui documenti sono emesse a livello di indice in Ricerca di Azure. Nel livello di applicazione hello, è a conoscenza necessità hello toodirect hello degli indici corretti vari tenant traffico toohello durante anche la gestione delle risorse a livello di servizio hello tra tutti i tenant.

Un attributo chiave del modello di indice per tenant hello è il possibilità hello capacità hello applicazione developer toooversubscribe hello di un servizio di ricerca tra tenant dell'applicazione hello. Se tenant hello dispone di una distribuzione non uniforme del carico di lavoro, la combinazione ottimale di hello di tenant possono essere distribuiti in un servizio di ricerca indici tooaccommodate un numero di elevata tenant attivo, un numero di risorse durante la gestione contemporaneamente una parte più consistente di tenant meno attivi. compromesso di Hello è impossibilità hello hello modello toohandle situazioni in cui ogni tenant contemporaneamente attivi.

modello di indice per tenant Hello fornisce base hello per un modello di costo variabile, in un intero servizio di ricerca di Azure viene acquistato anticipato e successivamente riempita con i tenant. In questo modo la capacità non usata toobe designato per le versioni di valutazione e gli account gratuiti.

Per le applicazioni con un footprint globale, il modello di indice per tenant hello potrebbe non essere più efficiente hello. Se i tenant di un'applicazione vengono distribuiti in globo hello, è possibile che un servizio distinto potrebbe essere necessario per ogni area in cui è possibile duplicare i costi per ognuno di essi.

Ricerca di Azure consente di scala hello singoli indici hello sia hello totale toogrow indici. Se un piano tariffario appropriato livello scelto, partizioni e repliche è possibile aggiungere servizio di ricerca completa toohello quando un singolo indice all'interno del servizio hello diventa troppo grande in termini di archiviazione o il traffico.

Se il numero totale di hello indici diventa troppo grande per un singolo servizio, un altro servizio ha tooaccommodate toobe provisioning hello nuovi tenant. Se gli indici toobe spostati tra i servizi di ricerca con l'aggiunta di nuovi servizi, dati hello dall'indice di hello sono toobe copiati manualmente da un indice toohello altri come ricerca di Azure non consente un toobe indice spostato.

## <a name="2-service-per-tenant"></a>2. Servizio per tenant
![Un'immagine del modello di servizio per tenant hello](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

In un'architettura "servizio per tenant" ogni tenant dispone di un proprio servizio di ricerca.

In questo modello, un'applicazione hello raggiunge il livello massimo di hello di isolamento per il tenant. Ogni servizio ha risorse di archiviazione e velocità effettiva dedicate per la gestione delle richiesta di ricerca nonché chiavi API diverse.

Per le applicazioni in cui ogni tenant dispone di un footprint di grandi dimensioni o il carico di lavoro di hello è minima variabilità da tootenant tenant, il modello di servizio per tenant hello è particolarmente efficace le risorse non vengono condivise tra i carichi di lavoro diversi tenant.

Un servizio per ogni modello tenant offre inoltre il vantaggio di hello di un modello stimabile un costo fisso. Non vi è alcun investimento iniziale in un servizio di ricerca completa fino a quando non è presente un toofill tenant, tuttavia hello costo per tenant è superiore a un modello di indice per tenant.

modello di servizio per tenant Hello è particolarmente efficace per le applicazioni con un footprint globale. Con i tenant distribuiti geograficamente, è facile toohave servizio ogni tenant in paese appropriato hello.

difficoltà di Hello in questo modello di scalabilità sorgono quando i singoli tenant diventano troppo grandi per il servizio. Ricerca di Azure attualmente non supporta l'aggiornamento hello tariffario di un servizio di ricerca, in modo che tutti i dati verrebbero toobe copiati manualmente tooa nuovo servizio.

## <a name="3-mixing-both-models"></a>3. Valutazione di entrambi i modelli
Un'altra possibilità per la modellazione multi-tenancy consiste nell'unione delle due strategie "indice per tenant" e "servizio per tenant".

Da una combinazione di hello due modelli, i tenant più grande di un'applicazione possono occupare servizi dedicati mentre hello tempo parte finale del meno tenant attivo di piccole dimensioni può occupare indici in un servizio condiviso. Questo modello garantisce che i tenant più grande di hello abbiano costantemente elevato delle prestazioni dal servizio hello proteggendo tooprotect hello tenant più piccolo da eventuali altre istanze di rumore.

L'implementazione di questa strategia si basa tuttavia sulla previsione di quali tenant richiederanno un servizio dedicato e non un indice in un servizio condiviso. La complessità dell'applicazione aumenta con hello necessità toomanage entrambi questi modelli multi-tenancy.

## <a name="achieving-even-finer-granularity"></a>Raggiungimento di una granularità ancora maggiore
Hello sopra scenari multi-tenant toomodel modelli di progettazione in ricerca di Azure si presuppone un uniform ambito in cui ogni tenant è un'intera istanza di un'applicazione. Le applicazioni tuttavia possono gestire a volte numerosi ambiti più piccoli.

Se i modelli di servizio per tenant e di indice per tenant non sono sufficientemente piccoli ambiti, è possibile toomodel un tooachieve indice un livello di granularità ancora più preciso.

toohave un singolo indice si comportano in modo diverso per gli endpoint client diversi, un campo può essere aggiunto tooan indice che designa un determinato valore per ogni client possibili. Ogni volta che un client chiama tooquery di ricerca di Azure o modificare un indice, codice hello dall'applicazione client hello specifica hello appropriato valore per tale campo mediante ricerca di Azure [filtro](https://msdn.microsoft.com/library/azure/dn798921.aspx) funzionalità in fase di query.

Questo metodo può essere utilizzato tooachieve funzionalità dell'account utente separato, livelli di autorizzazione separati e applicazioni completamente separate.

> [!NOTE]
> Hello approccio descritto in precedenza tooconfigure tooserve un singolo indice più pertinenti di hello interessa tenant dei risultati della ricerca. Punteggi di pertinenza di ricerca vengono calcolati in un ambito a livello di indice, non è un ambito a livello di tenant, in modo da dati di tutti i tenant viene incorporati nelle statistiche sottostanti dei punteggi di pertinenza hello, ad esempio la frequenza di termini.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Ricerca di Azure è una soluzione interessante per molte applicazioni, [ulteriori informazioni sulla funzionalità affidabili del servizio hello](http://aka.ms/whatisazsearch). Quando la valutazione hello vari Progettazione modelli per applicazioni multi-tenant, prendere in considerazione hello [vari piani tariffari](https://azure.microsoft.com/pricing/details/search/) e rispettiva hello [i limiti del servizio](search-limits-quotas-capacity.md) toobest personalizzare toofit di ricerca di Azure architetture di tutte le dimensioni e i carichi di lavoro dell'applicazione.

È possibile indirizzare eventuali domande sulla ricerca di Azure e scenari multi-tenant tooazuresearch_contact@microsoft.com.

