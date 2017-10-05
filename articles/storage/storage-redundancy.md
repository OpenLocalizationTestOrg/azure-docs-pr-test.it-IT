---
title: Replica dei dati in Archiviazione di Azure | Documentazione Microsoft
description: "I dati nell'account di archiviazione di Microsoft Azure vengono replicati per durabilità e disponibilità elevata. Le opzioni di replica includono archiviazione con ridondanza locale (LRS), archiviazione con ridondanza della zona (ZRS), archiviazione con ridondanza geografica (GRS) e archiviazione con ridondanza geografica e accesso in lettura (RA-GRS)."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: b9354484ff5b81e2561d017d039bf2c07a21a423
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-replication"></a>Replica di Archiviazione di Azure

I dati nell'account di archiviazione di Microsoft Azure vengono sempre replicati per assicurarne la durabilità e la disponibilità elevata. La replica copia i dati nello stesso data center o in uno secondario, a seconda dell'opzione di replica scelta. Consente di proteggere i dati e mantiene operativa l'applicazione in caso di errori hardware temporanei. Se i dati vengono replicati in un secondo data center, la replica li protegge da un errore irreversibile nella posizione primaria.

Garantisce infine che l'account di archiviazione soddisfi il [Contratto di servizio per Archiviazione](https://azure.microsoft.com/support/legal/sla/storage/) anche in caso di errori. Altre informazioni sulla garanzia di durabilità e disponibilità di Archiviazione di Azure sono reperibili nel Contratto di servizio.

Quando si crea un account di archiviazione, è possibile selezionare una delle opzioni di replica seguenti:

* [Archiviazione con ridondanza locale (LRS)](#locally-redundant-storage)
* [Archiviazione con ridondanza della zona (ZRS).](#zone-redundant-storage)
* [Archiviazione con ridondanza geografica (GRS)](#geo-redundant-storage)
* [Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS).](#read-access-geo-redundant-storage)

L'archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) è l'opzione predefinita quando si crea un account di archiviazione.

Nella tabella seguente è riportata una breve panoramica delle differenze tra i vari tipi di archiviazione, mentre nelle sezioni successive verranno forniti altri dettagli su ogni tipo di replica.

| Strategia di replica | Archiviazione con ridondanza locale | ZRS | Archiviazione con ridondanza geografica | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| I dati vengono replicati in più data center. |No |Sì |Sì |Sì |
| I dati possono essere letti da una posizione secondaria oltre che da quella primaria. |No |No |No |Sì |
| Numero di copie di dati mantenute in nodi distinti |3 |3 |6 |6 |

Per informazioni sui prezzi delle varie opzioni di ridondanza, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) .

> [!NOTE]
> Archiviazione Premium supporta solo l'archiviazione con ridondanza locale. Per informazioni su Archiviazione Premium, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](storage-premium-storage.md).
>

> [!NOTE]
> L'archiviazione file di Azure supporta solo l'archiviazione con ridondanza locale e l'archiviazione con ridondanza geografica. Per informazioni sull'archiviazione file di Azure, vedere [Panoramica dell'archiviazione file di Azure](storage-files-introduction.md).
>

## <a name="locally-redundant-storage"></a>Archiviazione con ridondanza locale
L'archiviazione con ridondanza locale (LRS) replica i dati tre volte all'interno di un'unità di scala di archiviazione, che è ospitata in un data center nell'area in cui è stato creato l'account di archiviazione. Una richiesta di scrittura viene restituita correttamente dopo che è stata scritta in tutte e tre le repliche. Queste tre repliche risiedono ognuna in domini di errore e domini di aggiornamento distinti all'interno di un'unità di scala di archiviazione.

Un'unità di scala di archiviazione è una raccolta di rack di nodi di archiviazione. Un dominio di errore è un gruppo di nodi che rappresentano un'unità di errore fisica e possono essere considerati come nodi appartenenti allo stesso rack fisico. Un dominio di aggiornamento è un gruppo di nodi che vengono aggiornati contemporaneamente durante il processo di aggiornamento del servizio (implementazione). Le tre repliche vengono distribuite tra domini di aggiornamento e domini di errore all'interno di un'unità di scala di archiviazione per assicurare la disponibilità dei dati anche in caso di errori hardware che influiscono su un singolo rack o quando i nodi vengono aggiornati durante un'implementazione.

L'archiviazione con ridondanza locale è l'opzione più economica e offre meno durata rispetto alle altre opzioni. In caso di emergenza a livello di data center (incendio, saturazione e così via) tutte e tre le repliche potrebbero essere perse o non essere recuperabili. Per ridurre questo rischio, per la maggior parte delle applicazioni è consigliabile l'archiviazione con ridondanza geografica (GRS).

L'archiviazione con ridondanza locale potrebbe comunque essere utile in determinati scenari:

* Fornisce la larghezza di banda massima più alta delle opzioni di replica di Archiviazione di Azure.
* Se l'applicazione archivia dati che possono essere ricostruiti facilmente, è consigliabile scegliere l'archiviazione con ridondanza locale.
* Per alcune applicazioni è necessario replicare i dati solo all'interno di un paese a causa di requisiti di governance dei dati. Un'area abbinata può trovarsi in un altro paese. Per altre informazioni sulle coppie di aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Archiviazione con ridondanza della zona
L'archiviazione con ridondanza della zona (ZRS) replica i dati in modo asincrono nei data center all'interno di uno o due aree oltre a memorizzare tre repliche come nell'archiviazione con ridondanza locale, fornendo così una durabilità maggiore rispetto a quest'ultima. I dati archiviati nell'archiviazione con ridondanza della zona sono assicurati anche se il data center principale non è disponibile o recuperabile.
I clienti che intendono usare l'archiviazione con ridondanza della zona devono tenere presente che:

* L'archiviazione con ridondanza della zona è disponibile solo per i BLOB in blocchi negli account di archiviazione di uso generale e supportata esclusivamente nelle versioni del servizio di archiviazione 2014-02-14 e successive.
* Poiché la replica asincrona implica un ritardo, in caso di un'emergenza locale è possibile che le modifiche non ancora replicate nell'area secondaria vadano perse se non è possibile recuperare i dati dall'area primaria.
* La replica potrebbe non essere disponibile fino a quando Microsoft non avvia il failover all'area secondaria.
* Gli account di archiviazione con ridondanza della zona non possono essere convertiti in un secondo momento in account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica. Allo stesso modo, non è possibile convertire un account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica in un account di archiviazione con ridondanza della zona.
* Gli account di archiviazione con ridondanza della zona non dispongono di metriche o funzionalità di registrazione.

## <a name="geo-redundant-storage"></a>Archiviazione con ridondanza geografica
Con l'archiviazione con ridondanza geografica (GRS) i dati vengono replicati in un'area secondaria a centinaia di chilometri di distanza dall'area primaria. Se per l'account di archiviazione è stata abilitata l'archiviazione con ridondanza geografica, la durabilità dei dati è assicurata anche in caso di un'interruzione completa dell'alimentazione locale o in situazioni di emergenza in cui l'area primaria non è recuperabile.

Per un account di archiviazione con l'archiviazione con ridondanza geografica abilitata, il commit di un aggiornamento viene eseguito prima nell'area primaria, dove viene replicato per tre volte. Quindi l'aggiornamento viene replicato in modo asincrono nell'area secondaria, dove viene inoltre replicato tre volte.

Con l'archiviazione con ridondanza geografica, entrambe le aree primaria e secondaria gestiscono repliche tra domini di errore e domini di aggiornamento separati all'interno di un'unità di scala di archiviazione, come descritto per l'archiviazione con ridondanza locale.

Considerazioni:

* Poiché la replica asincrona implica un ritardo, in caso di un'emergenza a livello di area è possibile che le modifiche non ancora replicate nell'area secondaria vadano perse se non è possibile recuperare i dati dall'area primaria.
* La replica non è disponibile a meno che Microsoft non avvii il failover all'area secondaria. Se Microsoft avvia un failover nell'area secondaria, al termine del failover si avrà accesso in lettura e scrittura a tali dati. Per altre informazioni, vedere le [indicazioni sul ripristino di emergenza](storage-disaster-recovery-guidance.md). 
* Per consentire a un'applicazione la lettura dall'area secondaria, l'utente deve abilitare l'archiviazione con ridondanza geografica e accesso in lettura (RA-GRS).

L'area primaria viene selezionata durante la creazione di un account di archiviazione. L'area secondaria viene invece determinata in base a quella primaria e non è possibile modificarla. Nella tabella seguente vengono illustrate le associazioni di aree primarie e secondarie:

| Primario | Secondario |
| --- | --- |
| Stati Uniti centro-settentrionali |Stati Uniti centro-meridionali |
| Stati Uniti centro-meridionali |Stati Uniti centro-settentrionali |
| Stati Uniti orientali |Stati Uniti occidentali |
| Stati Uniti occidentali |Stati Uniti orientali |
| Stati Uniti orientali 2 |Stati Uniti centrali |
| Stati Uniti centrali |Stati Uniti orientali 2 |
| Europa settentrionale |Europa occidentale |
| Europa occidentale |Europa settentrionale |
| Asia sudorientale |Asia orientale |
| Asia orientale |Asia sudorientale |
| Cina orientale |Cina settentrionale |
| Cina settentrionale |Cina orientale |
| Giappone orientale |Giappone occidentale |
| Giappone occidentale |Giappone orientale |
| Brasile meridionale |Stati Uniti centro-meridionali |
| Australia orientale |Australia sudorientale |
| Australia sudorientale |Australia orientale |
| India meridionale |India centrale |
| India centrale |India meridionale |
| India occidentale |India meridionale |
| Governo degli Stati Uniti - Iowa |Governo degli Stati Uniti - Virginia |
| Governo degli Stati Uniti - Virginia |Governo degli Stati Uniti - Texas |
| Governo degli Stati Uniti - Texas |Governo degli Stati Uniti - Arizona |
| Governo degli Stati Uniti - Arizona |Governo degli Stati Uniti - Texas |
| Canada centrale |Canada orientale |
| Canada orientale |Canada centrale |
| Regno Unito occidentale |Regno Unito meridionale |
| Regno Unito meridionale |Regno Unito occidentale |
| Germania centrale |Germania nord-orientale |
| Germania nord-orientale |Germania centrale |
| Stati Uniti occidentali 2 |Stati Uniti centro-occidentali |
| Stati Uniti centro-occidentali |Stati Uniti occidentali 2 |

Per informazioni aggiornate sulle aree supportate da Azure, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

>[!NOTE]  
> L'area secondaria di US Gov Virginia è US Gov Texas. In precedenza, US Gov Virginia usava come area secondaria US Gov Iowa. È in corso la migrazione degli account di archiviazione che usano ancora US Gov Iowa all'area secondaria US Gov Texas. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Archiviazione con ridondanza geografica e accesso in lettura
L'archiviazione con ridondanza geografica e accesso in lettura(RA-GRS) massimizza la disponibilità dell'account di archiviazione fornendo l'accesso in sola lettura ai dati nella posizione secondaria, oltre alla replica tra due aree assicurata dall'archiviazione con ridondanza geografica.

Se si abilita l'accesso in sola lettura ai dati nell'area secondaria, i dati saranno disponibili in un endpoint secondario, oltre che nell'endpoint primario dell'account di archiviazione. L'endpoint secondario è simile a quello primario, ma al nome dell'account viene aggiunto il suffisso `–secondary` . Se ad esempio l'endpoint primario per il servizio BLOB è `myaccount.blob.core.windows.net`, l'endpoint secondario sarà `myaccount-secondary.blob.core.windows.net`. Le chiavi di accesso per l'account di archiviazione sono identiche per gli endpoint primario e secondario.

Considerazioni:

* L'applicazione deve gestire l'endpoint con cui interagire quando usa l'archiviazione con ridondanza geografica e accesso in lettura.
* Poiché la replica asincrona implica un ritardo, in caso di un'emergenza a livello di area è possibile che le modifiche non ancora replicate nell'area secondaria vadano perse se non è possibile recuperare i dati dall'area primaria.
* Se Microsoft avvia un failover nell'area secondaria, al termine del failover si avrà accesso in lettura e scrittura a tali dati. Per altre informazioni, vedere le [indicazioni sul ripristino di emergenza](storage-disaster-recovery-guidance.md). 
* L'archiviazione con ridondanza geografica e accesso in lettura è pensata per rispondere a requisiti di disponibilità elevata. Per linee guida sulla scalabilità, consultare l'[elenco di controllo delle prestazioni](storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Domande frequenti

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-the-geo-replication-type-of-my-storage-account"></a>1. Come si può modificare il tipo di replica geografica dell'account di archiviazione?

   Si può modificare il tipo di replica geografica dell'account di archiviazione, scegliendo tra archiviazione con ridondanza locale, archiviazione con ridondanza geografica e archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) tramite il [portale di Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md) o a livello di programmazione usando una delle numerose librerie dei client di archiviazione disponibili. Si noti che gli account di archiviazione con ridondanza della zona non possono essere convertiti in account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica. Allo stesso modo, non è possibile convertire un account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica in un account di archiviazione con ridondanza della zona.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-the-replication-type-of-my-storage-account"></a>2. Sono previsti tempi di inattività quando si cambia il tipo di replica dell'account di archiviazione?

   No, non si verificheranno tempi di inattività.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-the-replication-type-of-my-storage-account"></a>3. Sono previsti costi aggiuntivi quando si cambia il tipo di replica dell'account di archiviazione?

   Sì. Il passaggio dall'archiviazione con ridondanza locale all'archiviazione con ridondanza geografica (o con ridondanza geografica e accesso in lettura, RA-GRS) per l'account di archiviazione comporta un addebito aggiuntivo sul traffico in uscita associato alla copia dei dati esistenti dalla posizione primaria alla posizione secondaria. Dopo la copia dei dati iniziali non sono previsti ulteriori addebiti in uscita per la replica geografica dei dati dalla posizione primaria a quella secondaria. I dettagli sui costi per la larghezza di banda sono disponibili nella [pagina dei prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/blobs/). Se si passa dall'archiviazione con ridondanza geografica all'archiviazione con ridondanza locale non sono previsti costi aggiuntivi, ma i dati verranno eliminati dalla posizione secondaria.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Qual è l'utilità di RA-GRS?
   
   Con l'archiviazione con ridondanza geografica i dati vengono replicati in un'area secondaria a centinaia di chilometri di distanza dall'area primaria. In questo caso, la durabilità dei dati è assicurata anche in caso di un'interruzione completa dell'alimentazione locale o in situazioni di emergenza in cui l'area primaria non è recuperabile. L'archiviazione RA-GRS include, oltre a questo, la possibilità di leggere i dati dalla posizione secondaria. Per alcune idee su come sfruttare questa possibilità, consultare [Progettazione di applicazioni a disponibilità elevata con archiviazione RA-GRS](storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-to-figure-out-how-long-it-takes-to-replicate-my-data-from-the-primary-to-the-secondary-region"></a>5. Esiste un modo per determinare il tempo necessario per replicare i dati dall'area primaria a quella secondaria?
   
   Se si usa l'archiviazione RA-GRS, è possibile controllare l'ora dell'ultima sincronizzazione dell'account di archiviazione. Ora ultima sincronizzazione è un valore di data/ora GMT. Tutte le scritture nell'area primaria precedenti all'ora dell'ultima sincronizzazione sono state scritte correttamente nella posizione secondaria, vale a dire che sono disponibili per la lettura dalla posizione secondaria. Le scritture nell'area primaria successive all'ora dell'ultima sincronizzazione possono essere o meno già disponibili per la lettura. È possibile eseguire query su questo valore tramite il [portale di Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md) o a livello di programmazione usando l'API REST o una delle librerie dei client di archiviazione. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-to-the-secondary-region-if-there-is-an-outage-in-the-primary-region"></a>6. Come si fa a passare all'area secondaria se si verifica un'interruzione nell'area primaria?
   
   Consultare l'articolo [Cosa fare se si verifica un'interruzione di Archiviazione di Azure](storage-disaster-recovery-guidance.md) per altri dettagli.

<a id="rpo-rto"></a>
#### <a name="7-what-is-the-rpo-and-rto-with-grs"></a>7. Quali sono gli obiettivi RPO e RTO con l'archiviazione con ridondanza geografica?
   
   Obiettivo del punto di ripristino (RPO, Recovery Point Objective): nel caso dell'archiviazione con ridondanza geografica e dell'archiviazione con ridondanza geografica e accesso in lettura, il servizio di archiviazione esegue la replica geografica asincrona dalla posizione primaria a quella secondaria. Se si verifica una grave emergenza a livello locale ed è necessario eseguire il failover, le modifiche differenziali non ancora replicate geograficamente potrebbero andare perse. Il numero di minuti di potenziale perdita di dati è detto RPO e corrisponde al punto nel tempo in cui è possibile ripristinare i dati. In genere il nostro RPO è inferiore a 15 minuti, anche se attualmente non è previsto alcun contratto di servizio sulla durata della replica geografica.

   Obiettivo del punto di ripristino (RPO, Recovery Point Objective): è una misura del tempo necessario per eseguire il failover e riportare online l'account di archiviazione se si rende necessario un failover. Il tempo necessario per eseguire il failover include quanto segue:
    * Tempo necessario per svolgere analisi e determinare se è possibile recuperare i dati nella posizione primaria o se è necessario eseguire un failover.
    * Failover dell'account mediante modifica delle voci relative al DNS primario in modo che puntino alla posizione secondaria.

   Prendiamo molto seriamente la responsabilità di salvaguardare i dati degli utenti, pertanto se esiste la possibilità di recuperare i dati il failover non verrà eseguito e ci concentreremo sul recupero dei dati nella posizione primaria. In futuro, intendiamo fornire un'API che consenta agli utenti di attivare il failover a livello di account e dunque di controllare personalmente l'obiettivo RTO, ma attualmente non è disponibile.
   
## <a name="next-steps"></a>Passaggi successivi
* [Progettazione di applicazioni a disponibilità elevata con archiviazione RA-GRS](storage-designing-ha-apps-with-ragrs.md)
* [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md)
* [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md)
* [Opzioni di ridondanza di Archiviazione di Microsoft Azure e archiviazione con ridondanza geografica e accesso in lettura ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [Paper SOSP - Archiviazione di Azure: un servizio di archiviazione cloud a elevata disponibilità con coerenza assoluta](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

