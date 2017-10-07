---
title: toodo aaaWhat nell'evento hello di un'interruzione del servizio di archiviazione di Azure | Documenti Microsoft
description: Quali toodo nell'evento hello di un'interruzione del servizio di archiviazione di Azure
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: ee7eb71311c6e453dc078ec3566267ee0c2f444a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Quali toodo se si verifica un'interruzione del servizio di archiviazione di Azure
Microsoft, collaboriamo toomake disco che i servizi siano sempre disponibili. A volte si verificano eventi al di fuori del controllo di Microsoft, che causano interruzioni non pianificate dei servizi in una o più aree. toohelp gestire queste occorrenze rare, forniamo hello seguendo le indicazioni di alto livello per servizi di archiviazione di Azure.

## <a name="how-tooprepare"></a>Come tooprepare
È essenziale per ogni cliente tooprepare proprio piano di ripristino di emergenza. Hello sforzo toorecover da un'interruzione dell'archiviazione in genere prevede personale e procedure automatizzate in ordine tooreactivate le applicazioni in uno stato funziona. Consultare la documentazione di Azure seguito toobuild toohello proprio piano di ripristino di emergenza:

* [Ripristino di emergenza e disponibilità elevata per le applicazioni Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Indicazioni tecniche sulla resilienza di Azure](../resiliency/resiliency-technical-guidance.md)
* [Servizio Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Replica di Archiviazione di Azure](storage-redundancy.md)
* [Servizio Backup di Azure](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Come toodetect
Hello consigliata hello toodetermine modo lo stato del servizio di Azure è toosubscribe toohello [Dashboard di integrità del servizio di Azure](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Quali toodo se si verifica un'interruzione dell'archiviazione
Se uno o più servizi di archiviazione sono temporaneamente non disponibili in una o più aree, sono disponibili due opzioni per si tooconsider. Se si desiderano dati tooyour accesso immediato, è consigliabile opzione 2.

### <a name="option-1-wait-for-recovery"></a>Opzione 1: Attendere il ripristino
In tal caso, non è necessaria alcuna azione da parte dell'utente. Stiamo lavorando attentamente la disponibilità del servizio Azure toorestore hello. È possibile monitorare lo stato del servizio hello in hello [Dashboard di integrità del servizio di Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Opzione 2: Copiare i dati dall'area secondaria
Se si sceglie [archiviazione con ridondanza geografica e accesso in lettura (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (scelta consigliata) per gli account di archiviazione, si disporrà di accesso in lettura tooyour dati dall'area secondaria hello. È possibile utilizzare strumenti come [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), hello e [libreria lo spostamento dei dati di Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy dati dall'area secondaria di hello in un altro account di archiviazione in un'area unimpacted e scegliere account di archiviazione di applicazioni toothat per entrambe lettura e scrittura di disponibilità.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Quali tooexpect se si verifica un failover di archiviazione
Se si è scelta l'opzione [Archiviazione con ridondanza geografica](storage-redundancy.md#geo-redundant-storage) o [Archiviazione con ridondanza geografica e accesso in lettura](storage-redundancy.md#read-access-geo-redundant-storage) (consigliato), Archiviazione di Azure manterrà i dati persistenti in due aree (primaria e secondaria). In entrambe le aree Archiviazione di Azure mantiene costantemente più repliche dei dati.

Quando un'emergenza locale interessa l'area primaria, si tenterà innanzitutto servizio hello toorestore in tale area. Dipende dalla natura hello di emergenza hello e relativi effetti, in alcuni rari casi potrebbe non essere in grado di toorestore area primaria di hello. A quel punto, verrà eseguito un failover geografico. la replica dei dati tra aree Hello è un processo asincrono che può implicare un ritardo, pertanto è possibile che le modifiche che non sono ancora stato replicato area secondaria toohello potrebbe andare perso. È possibile eseguire query hello ["Ora dell'ultima sincronizzazione" dell'account di archiviazione](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget dettagli sullo stato di replica hello.

Alcuni punti failover geo riguardo hello archiviazione:

* Archiviazione failover geo verranno attivati solo dal team di archiviazione di Azure hello: non è richiesta alcuna azione di cliente.
* Il servizio di archiviazione esistente endpoint per BLOB, tabelle, code e i file rimangono uguali hello dopo il failover hello; Hello voce DNS sarà necessario tooswitch toobe aggiornato dall'area secondaria toohello di hello area primaria.
* Prima e durante il failover geo hello, si avrà accesso in scrittura tooyour account di archiviazione a causa di impatto toohello di emergenza hello ma è comunque possibile leggere da hello secondario se l'account di archiviazione è stato configurato come RA-GRS.
* Accesso in lettura e scrittura account di archiviazione tooyour verrà ripresa quando failover geo hello è stato completato e le modifiche DNS propagate hello, toobe toowhat utilizzato fa riferimento l'endpoint secondario. 
* Si noti che se si dispone di GRS o RA-GRS è configurato per l'account di archiviazione hello sarà necessario l'accesso in scrittura. 
* È possibile eseguire query ["Ultimo geografica tempo di Failover" dell'account di archiviazione](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget ulteriori informazioni, vedere.
* Dopo il failover hello, l'account di archiviazione sarà completamente funzionante, ma in uno stato "danneggiato", perché è in realtà ospitato in un'area autonomo con è possibile eseguire alcuna replica geografica. toomitigate questo rischio, sarà ripristinato area primaria originale hello e quindi lo stato originale di eseguire un failback geo-toorestore hello. Se l'area primaria originale hello è irreversibile, si dovrà allocare un'altra area secondaria.
  Per ulteriori informazioni sull'infrastruttura hello di replica geografica di archiviazione di Azure, consultare toohello articolo sul blog del team di archiviazione hello su [opzioni di ridondanza e RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Procedure consigliate per la protezione dei dati
Esistono alcuni tooback gli approcci consigliati backup dei dati di archiviazione a intervalli regolari.

* Dischi di macchina virtuale: hello utilizzare [servizio Azure Backup](https://azure.microsoft.com/services/backup/) tooback dei dischi VM hello utilizzati dalle macchine virtuali di Azure.
* BLOB in blocchi-crea un [snapshot](https://msdn.microsoft.com/library/azure/hh488361.aspx) di ogni blocco blob o copiare account di archiviazione tooanother hello BLOB in un'altra area tramite [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), o hello [ Libreria di Azure lo spostamento dei dati](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Utilizzare tabelle: [AzCopy](storage-use-azcopy.md) tooexport dati della tabella hello in un altro account di archiviazione in un'altra area.
* Utilizzare file- [AzCopy](storage-use-azcopy.md) o [Azure PowerShell](storage-powershell-guide-full.md) toocopy dell'account di archiviazione di file tooanother in un'altra area.

Per informazioni sulla creazione di applicazioni che sfruttano le funzionalità di hello RA-GRS, estrarre [progettazione altamente disponibile di applicazioni mediante spazio di memorizzazione RA-GRS](storage-designing-ha-apps-with-ragrs.md)

