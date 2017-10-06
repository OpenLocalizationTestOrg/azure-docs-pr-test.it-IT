---
title: i livelli nel database di Azure Cosmos aaaConsistency | Documenti Microsoft
description: "DB Cosmos Azure dispone di cinque coerenza livelli toohelp saldo finale coerenza, disponibilità e latenza compromessi."
keywords: coerenza finale, azure cosmos db, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Livelli di coerenza dei dati ottimizzabili in Azure Cosmos DB
È progettato Azure DB Cosmos hello messa a terra con la distribuzione globale presente per ogni modello di dati. È progettato toooffer stimabile a bassa latenza garanzie, un contratto di servizio disponibilità 99,99%, e ben definite più ridotti i modelli di coerenza. Azure Cosmos DB offre attualmente cinque livelli di coerenza: assoluta, decadimento ristretto, sessione, prefisso coerente e finale. 

Oltre ai modelli di **coerenza assoluta** e **finale** offerti in genere dai database distribuiti, Azure Cosmos DB offre altri tre modelli di coerenza attentamente codificati e operativi e ha convalidato la loro utilità in casi reali. Si tratta di hello **delimitata obsolescenza**, **sessione**, e **prefisso coerenza** livelli di coerenza. Collettivamente questi livelli di cinque coerenza consentono toomake ben motivata compromessi tra la coerenza, disponibilità e latenza. 

## <a name="distributed-databases-and-consistency"></a>Coerenza e database distribuiti
I database distribuiti a livello commerciale rientrano in due categorie: database che non offrono opzioni di coerenza comprovabili e ben definite e database che offrono due opzioni di programmabilità estreme (coerenza assoluta e coerenza finale). 

gli sviluppatori di applicazioni gli oneri precedente con minutia i protocolli di replica di Hello e non prevede li toomake difficile compromessi coerenza, disponibilità, latenza e velocità effettiva. quest'ultimo Hello inserisce un toochoose pressione uno dei due estremi hello. Nonostante hello moltissimi ricerca e proposte per i modelli di coerenza più di 50, hello community di database distribuita non è stato in grado di toocommercialize livelli di coerenza oltre la coerenza eventuale e sicuro. COSMOS DB consente agli sviluppatori toochoose tra i modelli di coerenza ben definiti cinque lungo spettro di coerenza hello – sicuro, delimitata obsolescenza, [sessione](http://dl.acm.org/citation.cfm?id=383631), prefisso coerenza e finale. 

![DB Cosmos Azure offre più ben definita (Media) coerenza modelli toochoose da](./media/consistency-levels/five-consistency-levels.png)

Hello nella tabella seguente vengono illustrate le garanzie specifiche hello che fornisce a ogni livello di coerenza.
 
**Livelli di coerenza e garanzie**

| Livello di coerenza | Garanzie |
| --- | --- |
| Assoluta | Linearità |
| Obsolescenza associata | Prefisso coerente. Ritardo delle letture rispetto alle scritture in base a prefissi k o intervallo t |
| sessione   | Prefisso coerente. Letture costanti, scritture costanti, lettura delle proprie scritture, scrittura basata sulle letture |
| Prefisso coerente | Gli aggiornamenti restituiti sono un prefisso di tutti gli aggiornamenti di hello, senza interruzioni |
| Finale  | Letture non in ordine |

È possibile configurare livello di coerenza predefinita hello sull'account DB Cosmos (e successivamente eseguire l'override della coerenza hello in una specifica richiesta di lettura). Internamente, livello di coerenza predefinita hello applica toodata all'interno di set di partizioni hello che può estendersi su aree. Circa il 73% dei tenant di Microsoft usa il livello di coerenza sessione e il 20% il livello decadimento ristretto. È stato notato che circa il 3% dei clienti sperimenta i vari livelli di coerenza inizialmente prima di decidere quale sia il livello di coerenza specifico più adatto alla propria applicazione. È stato osservato anche che solo il 2% dei tenant eseguono l'override dei livelli di coerenza per ogni richiesta. 

In Cosmos DB le operazioni di lettura servite con coerenza di sessione, prefisso coerente e finale sono due volte più economici delle operazioni di lettura con coerenza assoluta o decadimento ristretto. Il 99,99% dei contratti di servizi di Cosmos DB riguarda complessivamente aziende leader nel settore. Tali contratti includono garanzie di coerenza per quanto riguarda disponibilità, velocità effettiva e latenza. Viene impiegata una [controllo linearizability](http://dl.acm.org/citation.cfm?id=1806634), che funziona in modo continuo tramite i dati di telemetria di servizio e apertamente segnala eventuali tooyou le violazioni di verifica coerenza. Per delimitata obsolescenza, monitorare e segnalare eventuali violazioni impiegate i limiti di t. Per tutti i cinque livelli di coerenza flessibile, è inoltre segnalare hello [metrica probabilistica con obsolescenza associata](http://dl.acm.org/citation.cfm?id=2212359) tooyou direttamente.  

## <a name="scope-of-consistency"></a>Ambito di coerenza
granularità di Hello di verifica di coerenza è richiesta utente singolo tooa con ambito. Una richiesta di scrittura può corrispondono tooan insert, replace, inserire o eliminare la transazione. Come per le scritture, una transazione di lettura o alla query è anche richiesta utente singolo tooa con ambito. utente Hello potrebbe essere necessario toopaginate su una grande set di risultati, che si estende su più partizioni, ma ogni lettura transazione è con ambito tooa singola pagina e servito da all'interno di una singola partizione.

## <a name="consistency-levels"></a>Livelli di coerenza
È possibile configurare un livello di coerenza predefinita per l'account di database che si applica a raccolte tooall (e database) con il proprio account DB Cosmos. Per impostazione predefinita, tutte le letture e le query eseguite su hello risorse definito dall'utente, utilizzare livello di coerenza hello predefinito specificato nell'account di database hello. È possibile ridurre il livello di coerenza hello di lettura o una query specifica richiesta mediante in ognuna delle hello API supportate. Esistono cinque tipi di livelli di coerenza supportati dal protocollo di replica di Azure Cosmos DB hello che forniscono un chiaro compromesso tra garanzie di coerenza specifico e le prestazioni, come descritto in questa sezione.

**Assoluta**: 

* Coerenza assoluta offre un [linearizability](https://aphyr.com/posts/313-strong-consistency-models) con hello legge tooreturn garantita hello più recente di un elemento. 
* Coerenza assoluta garantisce che un'operazione di scrittura è visibile solo dopo che eseguito il commit in modo durevole quorum maggioranza dei hello delle repliche. Un'operazione di scrittura sia in modo sincrono eseguito il commit in modo durevole hello primario sia quorum hello dei database secondari, o che sia interrotto. Un'operazione di lettura è sempre riconosciuta leggere quorum maggioranza hello, un client non può vedere mai una scrittura uncommitted o parziale ed è sempre garantito tooread hello più recente riconosciuto scrittura. 
* Gli account Cosmos DB Azure coerenza assoluta toouse configurato non è possibile associare più di una regione di Azure con il proprio account Azure Cosmos DB. 
* costo di un'operazione di lettura Hello (in termini di [unità richieste](request-units.md) utilizzata) con coerenza assoluta è superiore alla sessione e finale, ma hello stesso come con obsolescenza associata.

**Decadimento ristretto**: 

* Coerenza con obsolescenza associata garantisce che le letture hello potrebbero rimanere indietro scritture da al massimo *K* versioni o prefissi di un elemento o *t* intervallo di tempo. 
* Pertanto, quando sceglie delimitata obsolescenza, hello "obsolescenza" può essere configurata in due modi: numero di versioni *K* dell'elemento hello mediante il quale hello letture un ritardo scritture hello e intervallo di tempo hello *t* 
* Delimitata obsolescenza offerte totale ordine globali, ad eccezione all'interno di hello "obsolescenza finestra." Hello monotonico leggere garanzie esiste all'interno di un'area all'interno e all'esterno di hello "obsolescenza finestra." 
* Il decadimento ristretto offre una maggiore garanzia di coerenza rispetto alla coerenza di sessione o finale. Per le applicazioni distribuite a livello globale, è consigliabile che utilizzare con obsolescenza associata per gli scenari in cui la coerenza assoluta toohave ma si desidera inoltre 99,99% di disponibilità e a bassa latenza. 
* Gli account Azure Cosmos DB configurati con la coerenza con decadimento ristretto possono associare qualsiasi numero di aree di Azure con il proprio account Azure Cosmos DB. 
* Hello costo di un'operazione di lettura (in termini di RUs utilizzata) con obsolescenza associata è superiore alla sessione e la coerenza eventuale ma hello stesso come coerenza assoluta.

**Sessione**: 

* A differenza dei modelli di coerenza globale hello offerti dai livelli di coerenza obsolescenza sicuro e limitata, la coerenza di sessione è tooa con ambito sessione. 
* La coerenza di sessione è ideale per tutti gli scenari in cui è coinvolto un dispositivo o una sessione utente poiché garantisce letture monotone, scritture monotone e garanzie di lettura di ciò che si scrive (RYW). 
* La coerenza della sessione fornisce coerenza prevedibile per una sessione e velocità effettiva di lettura massima offrendo letture e scritture di latenza più basse hello. 
* Gli account Azure Cosmos DB configurati con la coerenza sessione possono associare qualsiasi numero di aree di Azure con il proprio account Azure Cosmos DB. 
* Hello costo di un'operazione di lettura (in termini di RUs utilizzata) con livello di coerenza è minore di obsolescenza sicuro e limitata, ma la coerenza eventuale più di sessione

<a id="consistent-prefix"></a>
**Prefisso coerente**: 

* Prefisso coerenza garantisce che in assenza di altre scritture, hello repliche all'interno di gruppo hello finiranno per convergere. 
* Il prefisso coerente garantisce che le operazioni di lettura non vedano mai il fuori sequenza delle operazioni di scrittura. Se sono state eseguite operazioni di scrittura in ordine di hello `A, B, C`, quindi un client riconosce una `A`, `A,B`, o `A,B,C`, ma mai ordine come `A,C` o `B,A,C`.
* Gli account Azure Cosmos DB configurati con la coerenza con prefisso coerente possono associare qualsiasi numero di aree di Azure con il proprio account Azure Cosmos DB. 

**Finale**: 

* La coerenza eventuale garantisce che in assenza di altre scritture, hello repliche all'interno di gruppo hello finiranno per convergere. 
* La coerenza eventuale costituisce hello più debole di coerenza in cui un client può ottenere i valori di hello antecedenti hello quelli che aveva prima.
* La coerenza eventuale offre la consistenza in lettura più debole hello ma offerte hello latenza più bassa per le operazioni di lettura e scrittura.
* Gli account Azure Cosmos DB configurati con la coerenza finale possono associare qualsiasi numero di aree di Azure con il proprio account Azure Cosmos DB. 
* Hello costo di un'operazione di lettura (in termini di RUs utilizzata) con la coerenza eventuale hello livello è minore di tutti i livelli di coerenza hello Azure Cosmos DB hello.

## <a name="configuring-hello-default-consistency-level"></a>Configurazione del livello di coerenza predefinita hello
1. In hello [portale di Azure](https://portal.azure.com/)in hello Jumpbar, fare clic su **Azure Cosmos DB**.
2. In hello **Azure Cosmos DB** blade, hello selezionare database account toomodify.
3. Nel Pannello di hello account, fare clic su **predefinito coerenza**.
4. In hello **uniformità predefinita** pannello, il nuovo livello di coerenza selezionare hello e fare clic su **salvare**.
   
    ![Cattura di schermata evidenziazione icona Impostazioni hello e voce uniformità predefinita](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Livelli di coerenza per le query
Per impostazione predefinita, per le risorse definite dall'utente, il livello di coerenza hello per le query è hello stesso come il livello di coerenza hello per legge. Per impostazione predefinita, l'indice di hello viene aggiornato in modo sincrono in ogni istruzione insert, sostituire o eliminazione di un contenitore di DB Cosmos toohello dell'elemento. In questo modo le query hello toohonor hello stesso livello di coerenza del punto di letture. Anche se Azure Cosmos DB è con ottimizzazione per la scrittura e supporta volumi prolungati di operazioni di scrittura, la manutenzione degli indici sincrono e la gestione delle query coerenti, è possibile configurare determinate tooupdate raccolte relativo indice in modo differito. Questo tipo di indicizzazione ulteriormente migliora le prestazioni di scrittura hello ed è ideale per gli scenari di inserimento bulk quando un carico di lavoro è principalmente con intensa attività di lettura.  

| Modalità di indicizzazione | Letture | Query |
| --- | --- | --- |
| Coerente (impostazione predefinita) |Selezionare tra assoluta, con decadimento ristretto, sessione, prefisso coerente o finale |Selezionare tra assoluta, con obsolescenza associata, sessione o finale |
| Differita |Selezionare tra assoluta, con decadimento ristretto, sessione, prefisso coerente o finale |Finale |
| Nessuno |Selezionare tra assoluta, con decadimento ristretto, sessione, prefisso coerente o finale |Non applicabile |

Come con le richieste di lettura, è possibile abbassare il livello di coerenza hello di una richiesta di query specifico in ogni API.

## <a name="next-steps"></a>Passaggi successivi
Se si desidera toodo più le operazioni di lettura sui livelli di coerenza e compromessi, è consigliabile hello seguenti risorse:

* Doug Terry. Video: Replicated Data Consistency explained through baseball (La coerenza dei dati replicati illustrata attraverso il baseball).   
  [https://www.youtube.com/watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Doug Terry. Replicated Data Consistency explained through baseball.   
  [http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Doug Terry. Session Guarantees for Weakly Consistent Replicated Data.   
  [http://dl.acm.org/citation.cfm?id=383631](http://dl.acm.org/citation.cfm?id=383631)
* Daniel Abadi. Gli svantaggi di coerenza di Distributed Database sistemi Design moderno: perno è solo una parte della storia hello ".   
  [http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica. Probabilistic Bounded Staleness (PBS) for Practical Partial Quorums.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Coerente Finale - Revisited.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.html](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* MONI Naor, Avishai grezzo, hello carico, capacità e disponibilità di Quorum sistemi SIAM Journal in elaborazione, v.27 n.2, 447 p.423, aprile 1998.
  [http://epubs.siam.org/doi/abs/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Sebastian Burckhardt, Chris Dern, Macanal Musuvathi, Tan Roy, line-up: un linearizability completo e automatico correttore, procedimenti della conferenza ACM SIGPLAN 2010 di hello sulla lingua progettazione e implementazione, 05-10 giugno 2010, Roma, Ontario, programmazione Canada [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peter Bailis, Shivaram Venkataraman, Michael J. Franklin, Joseph M. Hellerstein, Ion Stoica, probabilisticamente delimitata obsolescenza per pratiche quorum parziale, svolgimento di hello VLDB dotazione, n.8 v. 5, 787 p.776, aprile 2012 [http:// DL.ACM.org/Citation.cfm?ID=2212359](http://dl.acm.org/citation.cfm?id=2212359)
