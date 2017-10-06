---
title: replica aaaData in archiviazione di Azure | Documenti Microsoft
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
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Replica di Archiviazione di Azure

dati Hello in di Microsoft Azure è sempre l'account di archiviazione replicata tooensure durabilità e disponibilità elevata. Copia la replica dei dati, all'interno hello stesso data center o tooa secondo data center, a seconda dell'opzione di replica scelto. Replica protegge i dati e mantiene l'applicazione tempo nell'evento hello di errori hardware temporanei. Se i dati vengono replicati tooa secondo data center, è protetto da un errore irreversibile nel percorso primario hello.

La replica garantisce che l'account di archiviazione soddisfi hello [contratto a livello di servizio (SLA) per l'archiviazione](https://azure.microsoft.com/support/legal/sla/storage/) anche in faccia hello di errori. Vedere hello contratto di servizio per informazioni sull'archiviazione di Azure garantisce la durabilità e la disponibilità.

Quando si crea un account di archiviazione, è possibile selezionare una delle seguenti opzioni di replica hello:

* [Archiviazione con ridondanza locale (LRS)](#locally-redundant-storage)
* [Archiviazione con ridondanza della zona (ZRS).](#zone-redundant-storage)
* [Archiviazione con ridondanza geografica (GRS)](#geo-redundant-storage)
* [Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS).](#read-access-geo-redundant-storage)

Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) è l'opzione predefinita di hello quando si crea un account di archiviazione.

Hello nella tabella seguente fornisce una rapida panoramica delle differenze di hello tra LRS, ZRS, GRS e RA-GRS, mentre ogni tipo di replica in modo più dettagliato nelle sezioni successive.

| Strategia di replica | Archiviazione con ridondanza locale | ZRS | Archiviazione con ridondanza geografica | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| I dati vengono replicati in più data center. |No |Sì |Sì |Sì |
| Dati possono essere letti da una posizione secondaria, nonché la posizione primaria hello. |No |No |No |Sì |
| Numero di copie di dati mantenute in nodi distinti |3 |3 |6 |6 |

Vedere [prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/) per informazioni sui prezzi per le opzioni di ridondanza diversi hello.

> [!NOTE]
> Archiviazione Premium supporta solo l'archiviazione con ridondanza locale. Per informazioni su Archiviazione Premium, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Archiviazione con ridondanza locale
Archiviazione localmente ridondante (LRS) consente di replicare i dati tre volte all'interno di un'unità di scala di archiviazione, che è ospitato in un Data Center nell'area di hello in cui viene creato l'account di archiviazione. Una richiesta di scrittura viene restituita correttamente solo dopo che è stato scritto tooall tre repliche. Queste tre repliche risiedono ognuna in domini di errore e domini di aggiornamento distinti all'interno di un'unità di scala di archiviazione.

Un'unità di scala di archiviazione è una raccolta di rack di nodi di archiviazione. Un dominio di errore (FD) è un gruppo di nodi che rappresentano un'unità fisica di errore e possono essere considerati come nodi appartenenti toohello stesso rack fisico. Un dominio di aggiornamento (UD) è un gruppo di nodi che vengono aggiornati contemporaneamente durante il processo di hello di un aggiornamento del servizio (implementazione). Hello tre repliche vengono distribuite tra domini di aggiornamento e domini di errore all'interno di un archivio scala unità tooensure che i dati sono disponibili anche se un errore hardware influisce su un singolo rack o quando i nodi vengono aggiornati durante un'implementazione.

Ridondanza locale è più economica hello e offre opzioni di tooother di durabilità confrontate minimi. Nell'evento hello di una Data Center di emergenza (incendi, inondazioni e così via) tutte e tre le repliche potrebbero essere perse o irreversibili. Archiviazione con ridondanza geografica (GRS) toomitigate questo rischio, è consigliabile per la maggior parte delle applicazioni.

L'archiviazione con ridondanza locale potrebbe comunque essere utile in determinati scenari:

* Fornisce la larghezza di banda massima più alta delle opzioni di replica di Archiviazione di Azure.
* Se l'applicazione archivia dati che possono essere ricostruiti facilmente, è consigliabile scegliere l'archiviazione con ridondanza locale.
* Alcune applicazioni sono dati tooreplicating limitato solo all'interno di un paese a causa di requisiti di governance toodata. Un'area abbinata può trovarsi in un altro paese. Per altre informazioni sulle coppie di aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Archiviazione con ridondanza della zona
Archiviazione con ridondanza della zona (ZRS), i dati vengono replicati in modo asincrono tra più Data Center all'interno di uno o due aree in aggiunta simile repliche toostoring tre del tooLRS, fornendo una durabilità maggiore rispetto a ridondanza locale. Dati archiviati in una zona sono durevoli, anche se i data center principale hello è disponibile o è irreversibile.
I clienti che pianificano toouse ZRS tenere presente che:

* L'archiviazione con ridondanza della zona è disponibile solo per i BLOB in blocchi negli account di archiviazione di uso generale e supportata esclusivamente nelle versioni del servizio di archiviazione 2014-02-14 e successive.
* Poiché la replica asincrona implica un ritardo, in caso di hello un'emergenza locale che è possibile che le modifiche che non sono ancora stato replicato toohello secondario andranno perse se non è possibile recuperare dati hello da hello primario.
* replica Hello potrebbe non essere disponibile fino a quando non Microsoft Avvia failover toohello secondario.
* Impossibile convertire l'account ZRS successive tooLRS o archiviazione con ridondanza geografica. Analogamente, un account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica è non può essere convertito di account ZRS tooa.
* Gli account di archiviazione con ridondanza della zona non dispongono di metriche o funzionalità di registrazione.

## <a name="geo-redundant-storage"></a>Archiviazione con ridondanza geografica
Archiviazione con ridondanza geografica (GRS) consente di replicare i dati tooa area secondaria a centinaia di miglia di distanza area primaria hello. Se l'account di archiviazione con ridondanza geografica abilitata, i dati sono durevoli anche in caso di hello di una completa interruzione dell'alimentazione locale o di emergenza in cui hello area primaria non è recuperabile.

Per un account di archiviazione con ridondanza geografica abilitata, l'area primaria toohello eseguito il commit prima, dove viene replicato per tre volte è un aggiornamento. Quindi l'aggiornamento di hello viene replicato in modo asincrono toohello area secondaria, in cui viene replicato anche tre volte.

Con l'archiviazione con ridondanza geografica, entrambe le aree primarie e secondarie hello gestire repliche tra domini di errore e l'aggiornamento di domini all'interno di un'unità di scala di archiviazione come descritto con ridondanza locale.

Considerazioni:

* Poiché la replica asincrona implica un ritardo, in caso di hello di situazioni di emergenza che è possibile che le modifiche apportate non sono ancora state replicate area secondaria toohello andranno persa se non è possibile recuperare dati hello dall'area primaria hello.
* replica Hello è disponibile solo se Microsoft avvia area secondaria toohello di failover. Se Microsoft ha avviato un'area secondaria toohello di failover, si avrà accesso in lettura e scrittura dati toothat dopo il failover hello è stata completata. Per altre informazioni, vedere le [indicazioni sul ripristino di emergenza](../storage-disaster-recovery-guidance.md). 
* Se un'applicazione desidera tooread dall'area secondaria hello, utente hello debba abilitare RA-GRS.

Quando si crea un account di archiviazione, selezionare l'area primaria hello account hello. area secondaria Hello viene determinato in base area primaria hello e non può essere modificato. Hello nella tabella seguente mostra hello associazioni di aree primarie e secondarie.

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
> L'area secondaria di US Gov Virginia è US Gov Texas. In precedenza, US Gov Virginia usava come area secondaria US Gov Iowa. Gli account di archiviazione ancora sfruttando ci Gov Iowa come un'area secondaria vengono migrati Texas Gov tooUS come area secondaria. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Archiviazione con ridondanza geografica e accesso in lettura
Archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) ottimizza la disponibilità dell'account di archiviazione, fornendo i dati di accesso in sola lettura toohello nella posizione secondaria hello, inoltre toohello replica tra due aree fornito dalla funzionalità GRS.

Quando si abilita dati di accesso in sola lettura tooyour nell'area secondaria hello, i dati sono disponibili in un endpoint secondario, nell'endpoint primario toohello di aggiunta dell'account di archiviazione. endpoint secondario Hello è endpoint primario a toohello simile, ma aggiunge il suffisso hello `–secondary` toohello nome dell'account. Ad esempio, se l'endpoint primario per il servizio Blob di hello è `myaccount.blob.core.windows.net`, l'endpoint secondario è `myaccount-secondary.blob.core.windows.net`. Hello i tasti di scelta per l'account di archiviazione sono hello stesso per entrambi hello endpoint primario e secondario.

Considerazioni:

* L'applicazione ha toomanage endpoint a cui interagisce con quando si utilizza RA-GRS.
* Poiché la replica asincrona implica un ritardo, in caso di hello di situazioni di emergenza che è possibile che le modifiche apportate non sono ancora state replicate area secondaria toohello andranno persa se non è possibile recuperare dati hello dall'area primaria hello.
* Se Microsoft avvia area secondaria toohello di failover, si avrà accesso in lettura e scrittura dati toothat dopo il failover hello è stata completata. Per altre informazioni, vedere le [indicazioni sul ripristino di emergenza](../storage-disaster-recovery-guidance.md). 
* L'archiviazione con ridondanza geografica e accesso in lettura è pensata per rispondere a requisiti di disponibilità elevata. Per materiale sussidiario per la scalabilità, vedere l'articolo hello [elenco di controllo delle prestazioni](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Domande frequenti

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Come è possibile modificare tipo di replica geografica hello personale dell'account di archiviazione?

   È possibile modificare tipo di replica geografica hello dell'account di archiviazione tra ridondanza locale, l'archiviazione con ridondanza geografica, e RA-GRS utilizzando hello [portale di Azure](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) o a livello di programmazione utilizzando uno dei nostri molti Client di archiviazione Librerie. Si noti che gli account di archiviazione con ridondanza della zona non possono essere convertiti in account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica. Analogamente, un account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica è non può essere convertito di account ZRS tooa.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Vi sarà qualsiasi tempo di inattività se si cambia il tipo di replica hello personale dell'account di archiviazione?

   No, non si verificheranno tempi di inattività.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Vi sarà alcun costo aggiuntivo se si cambia il tipo di replica hello personale dell'account di archiviazione?

   Sì. Se si passa dall'archiviazione con ridondanza locale tooGRS (o RA-GRS) dell'account di archiviazione, è necessario comporta un costo aggiuntivo coinvolti nella copia di dati esistenti dal percorso secondario di posizione primaria toohello in uscita. Una volta la copia di dati iniziale hello è senza ulteriori costi aggiuntivi in uscita per la replica dei dati di hello dalla posizione primaria toosecondary hello geografica. i dettagli di Hello per i costi di larghezza di banda sono reperibile in hello [pagina prezzi di archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/blobs/). Se passa dall'archiviazione con ridondanza geografica tooLRS, non sono previsti costi aggiuntivi, ma i dati verranno eliminati dal percorso secondario hello.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Qual è l'utilità di RA-GRS?
   
   Archiviazione di archiviazione con ridondanza geografica fornisce la replica dei dati da un'area secondaria tooa primario centinaia di miglia di distanza area primaria hello. In tal caso, i dati sono durevoli anche in caso di hello di una completa interruzione dell'alimentazione locale o di emergenza in cui hello area primaria non è recuperabile. Archiviazione RA-GRS include questo oltre ad aggiungere dati hello tooread possibilità di hello dalla posizione secondaria hello. Per alcune idee su come tooleverage questa capacità, consultare troppo[progettazione altamente disponibile di applicazioni mediante spazio di memorizzazione RA-GRS](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Esiste un modo per me toofigure out quanto tempo servirebbe tooreplicate dei dati dall'area secondaria di hello toohello primaria?
   
   Se si utilizza l'archiviazione RA-GRS, è possibile controllare hello ora dell'ultima sincronizzazione dell'account di archiviazione. Ora dell'ultima sincronizzazione è un valore di data/ora GMT. tutte le scritture primarie prima di hello ora dell'ultima sincronizzazione sono stati scritti correttamente toohello posizione secondaria, che significa che sono disponibili toobe leggere dal percorso secondario hello. Le scritture primarie dopo hello ora dell'ultima sincronizzazione può o non sia disponibile per le letture ancora. È possibile eseguire query di questo valore utilizzando hello [portale di Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), o livello di programmazione tramite hello API REST o una delle librerie Client di archiviazione hello. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Come è possibile passare area secondaria toohello se è presente un'interruzione del servizio nell'area primaria hello?
   
   Consultare l'articolo toohello [quali toodo se si verifica un'interruzione di servizio di archiviazione Azure](../storage-disaster-recovery-guidance.md) per altri dettagli.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. Che cos'è hello RPO e RTO con archiviazione con ridondanza geografica?
   
   Obiettivo del punto di ripristino (RPO): GRS e RA-GRS, archiviazione hello servizio in modo asincrono dati hello geografica replica dal percorso secondario di hello toohello primario. Se è presente un errore grave internazionale e toobe eseguita dispone di un failover, le modifiche delta recenti non sono stati replicati geograficamente vadano perse. numero di Hello di minuti della potenziali perdita di dati è tooas cui hello RPO (ovvero punto hello nei dati toowhich temporale può essere ripristinato). In genere il nostro RPO è inferiore a 15 minuti, anche se attualmente non è previsto alcun contratto di servizio sulla durata della replica geografica.

   Obiettivo tempo di ripristino (RTO): Questa è una misura di tempo impiegato ci toodo hello failover e tornare account di archiviazione hello online se si dispone di un failover toodo. Hello ora toodo hello failover include seguente hello:
    * tempo di Hello ci ha tooinvestigate e determinare se è possibile ripristinare i dati di hello nella posizione primaria hello o se è necessario toodo un failover.
    * Account di failover hello modificando hello primario DNS voci toopoint toohello posizione secondaria.

   È responsabilità del hello di mantenere i dati molto grave, pertanto se è presente qualsiasi possibilità di ripristino dei dati di hello, verrà consigliabile evitare di effettuare il failover hello e concentrare l'attenzione sul ripristino di dati hello nella posizione primaria hello. In futuro hello, contiamo tooallow tooprovide un'API si tootrigger un failover a un livello di account, che quindi consentirebbe toocontrol hello RTO personalmente, ma questo non è ancora disponibile.
   
## <a name="next-steps"></a>Passaggi successivi
* [Progettazione di applicazioni a disponibilità elevata con archiviazione RA-GRS](../storage-designing-ha-apps-with-ragrs.md)
* [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Informazioni sugli account di archiviazione di Azure](../storage-create-storage-account.md)
* [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](storage-scalability-targets.md)
* [Opzioni di ridondanza di Archiviazione di Microsoft Azure e archiviazione con ridondanza geografica e accesso in lettura ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [Paper SOSP - Archiviazione di Azure: un servizio di archiviazione cloud a elevata disponibilità con coerenza assoluta](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

