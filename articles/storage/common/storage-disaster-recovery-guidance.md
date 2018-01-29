---
title: Cosa fare in caso di interruzione di Archiviazione di Azure | Microsoft Docs
description: Cosa fare in caso di interruzione di Archiviazione di Azure
services: storage
documentationcenter: .net
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: tamram
ms.openlocfilehash: c768bdbb8e1ce2aae3eb5b6db0e48977366c83fb
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="what-to-do-if-an-azure-storage-outage-occurs"></a>Cosa fare se si verifica un'interruzione di Archiviazione di Azure
Microsoft si impegna costantemente per verificare che i servizi siano sempre disponibili. A volte si verificano eventi al di fuori del controllo di Microsoft, che causano interruzioni non pianificate dei servizi in una o più aree. Per riuscire a gestire questi sporadici avvenimenti, viene fornita la guida generale seguente per i servizi di Archiviazione di Azure.

## <a name="how-to-prepare"></a>Come prepararsi
È fondamentale che ogni cliente prepari il proprio piano di ripristino di emergenza. Il processo per eseguire il ripristino dopo un'interruzione dell'archiviazione comporta in genere sia il coinvolgimento del personale addetto alle attività operative che procedure automatizzate per riattivare le applicazioni in uno stato funzionante. Per creare un piano di ripristino di emergenza, vedere la documentazione di Azure seguente:

* [Ripristino di emergenza e disponibilità elevata per le applicazioni Azure](/azure/architecture/resiliency/disaster-recovery-high-availability-azure-applications.md)
* [Indicazioni tecniche sulla resilienza di Azure](/azure/architecture/resiliency.md)
* [Servizio Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Replica di Archiviazione di Azure](storage-redundancy.md)
* [Servizio Backup di Azure](https://azure.microsoft.com/services/backup/)

## <a name="how-to-detect"></a>Come rilevare il problema
Il modo consigliato per determinare lo stato dei servizi di Azure consiste nel sottoscrivere il [Dashboard per l'integrità dei servizi di Azure](https://azure.microsoft.com/status/).

## <a name="what-to-do-if-a-storage-outage-occurs"></a>Cosa fare se si verifica un'interruzione dell'archiviazione
Se uno o più servizi di archiviazione sono temporaneamente non disponibili in una o più aree, è possibile prendere considerazione due opzioni. Per accedere immediatamente ai dati, prendere in considerazione l'opzione 2.

### <a name="option-1-wait-for-recovery"></a>Opzione 1: Attendere il ripristino
In tal caso, non è necessaria alcuna azione da parte dell'utente. Si sta lavorando per ripristinare la disponibilità dei servizi di Azure. È possibile monitorare lo stato dei servizi nel [Dashboard per l'integrità dei servizi di Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Opzione 2: Copiare i dati dall'area secondaria
Se si è scelto [Archiviazione con ridondanza geografica e accesso in lettura](storage-redundancy.md#read-access-geo-redundant-storage) (consigliato) per gli account di archiviazione, si avrà l'accesso in lettura ai dati dall'area secondaria. È possibile usare strumenti come [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md) e la [libreria di spostamento dei dati di Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) per copiare i dati dall'area secondaria in un altro account di archiviazione in un'area non interessata e quindi indirizzare le applicazioni a tale account di archiviazione per la disponibilità sia in lettura che in scrittura.

## <a name="what-to-expect-if-a-storage-failover-occurs"></a>Cosa aspettarsi se si verifica un failover dell'archiviazione
Se si è scelta l'opzione [Archiviazione con ridondanza geografica](storage-redundancy.md#geo-redundant-storage) o [Archiviazione con ridondanza geografica e accesso in lettura](storage-redundancy.md#read-access-geo-redundant-storage) (consigliato), Archiviazione di Azure manterrà i dati persistenti in due aree (primaria e secondaria). In entrambe le aree Archiviazione di Azure mantiene costantemente più repliche dei dati.

Quando un'emergenza locale colpisce l'area primaria, per prima cosa si cercherà di ripristinare il servizio in tale area. A seconda della natura e delle conseguenze dell'emergenza, in alcuni rari casi potrebbe non essere possibile ripristinare l'area primaria. A quel punto, verrà eseguito un failover geografico. La replica dei dati tra aree è un processo asincrono che può comportare un ritardo, quindi è possibile che le modifiche non ancora replicate nell'area secondaria vadano perse. È possibile effettuare una query del valore ["Ora ultima sincronizzazione" dell'account di archiviazione](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) per ottenere i dettagli sullo stato di replica.

È necessario tenere presenti alcuni aspetti relativi all'esperienza di failover geografico di archiviazione:

* Il failover geografico di archiviazione verrà attivato solo dal team di Archiviazione di Azure. Non è necessaria alcuna azione da parte del cliente.
* Gli endpoint di servizio di archiviazione esistenti per BLOB, tabelle, code e file resteranno inalterati dopo il failover. La voce DNS fornita da Microsoft dovrà essere aggiornata per passare dall'area primaria all'area secondaria.  Microsoft eseguirà questo aggiornamento automaticamente nell'ambito del processo di failover geografico.
* Prima e durante il failover geografico, in conseguenza dell'emergenza non si avrà accesso in scrittura all'account di archiviazione, ma sarà possibile leggere dall'area secondaria se l'account di archiviazione è stato configurato come RA-GRS.
* Dopo il completamento del failover geografico e la propagazione delle modifiche DNS, verrà ripristinato l'accesso in lettura e scrittura all'account di archiviazione, che punterà a quello che in precedenza era l'endpoint secondario. 
* L'accesso in scrittura sarà disponibile se per l'account di archiviazione è configurata l'archiviazione con ridondanza geografica oppure l'archiviazione con ridondanza geografica e accesso in lettura (RA-GRS). 
* Per informazioni più dettagliate, è possibile cercare l'[ora dell'ultimo failover replica geografica dell'account di archiviazione](https://msdn.microsoft.com/library/azure/ee460802.aspx).
* Dopo il failover, l'account di archiviazione sarà completamente funzionante, ma in uno stato "danneggiato", perché in realtà è ospitato in un'area autonoma senza possibilità di replica geografica. Per ridurre questo rischio, verrà ripristinata l'area primaria originale e quindi verrà eseguito un failback geografico per ripristinare lo stato originale. Se l'area primaria originale non è recuperabile, verrà allocata un'altra area secondaria.
  Per altri dettagli sull'infrastruttura della replica geografica di Archiviazione di Azure, vedere l'articolo nel blog del team di archiviazione sulle [opzioni di ridondanza e RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Procedure consigliate per la protezione dei dati
Esistono alcuni approcci consigliati per il backup periodico dei dati di archiviazione.

* Disk di VM: usare il [servizio Backup di Azure](https://azure.microsoft.com/services/backup/) per eseguire il backup dei dischi delle VM usati dalle macchine virtuali di Azure.
* BLOB in blocchi: creare uno [snapshot](https://msdn.microsoft.com/library/azure/hh488361.aspx) di ogni BLOB in blocchi o copiare i BLOB in un altro account di archiviazione in un'altra area usando [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md) o la [libreria di spostamento dei dati di Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Tabelle: usare [AzCopy](storage-use-azcopy.md) per esportare i dati delle tabelle in un altro account di archiviazione in un'altra area.
* File: usare [AzCopy](storage-use-azcopy.md) o [Azure PowerShell](storage-powershell-guide-full.md) per copiare i file in un altro account di archiviazione in un'altra area.

Per informazioni sulla creazione di applicazioni che sfruttano al meglio la funzionalità RA-GRS, vedere l'articolo relativo alla [progettazione di applicazioni a disponibilità elevata con archiviazione RA-GRS](../storage-designing-ha-apps-with-ragrs.md)

