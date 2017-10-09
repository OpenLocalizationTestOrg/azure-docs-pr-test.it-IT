---
title: "aaaMoving grandi quantità di dati in o dall'archiviazione cloud in Azure | Documenti Microsoft"
description: Panoramica dei metodi diversi per lo spostamento dati tooand hello da archiviazione di Azure.
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 8f7105fea7c2d28ba9954898743070d338f46a37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Lo spostamento di dati tooand da archiviazione di Azure
Se si desidera toomove locale dati tooAzure archiviazione (o viceversa), esistono numerosi modi toodo questo. approccio Hello che funziona meglio per l'utente dipenderà dal proprio scenario. Questo articolo offre informazioni generali su diversi scenari e la soluzione appropriata per ciascuno.

## <a name="building-applications"></a>Compilazione di applicazioni
Se si sta creando un'applicazione, lo sviluppo in hello API REST o uno dei nostri numerose librerie client è un tooand di dati ideale toomove da archiviazione di Azure.

In Archiviazione di Azure sono disponibili librerie client complete per .NET, iOS, Java, Android, piattaforma UWP, Xamarin, C++, Node.JS, PHP, Ruby e Python. le librerie client Hello offrono funzionalità avanzate come la logica di riesecuzione, registrazione e Caricamenti paralleli. È inoltre possibile sviluppare direttamente su hello API REST, che può essere chiamato da qualsiasi linguaggio che effettua le richieste HTTP/HTTPS.

Vedere [Introduzione all'archiviazione Blob di Azure](storage-dotnet-how-to-use-blobs.md) toolearn altre.

Inoltre, offre hello [libreria lo spostamento dei dati di archiviazione Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) una libreria progettata per prestazioni elevate copia dei dati tooand da Azure. Consultare tooour raccolta lo spostamento dei dati [documentazione](https://github.com/Azure/azure-storage-net-data-movement) toolearn altre. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Visualizzazione e interazione rapida dei dati
Se si desiderano tooview un modo semplice i dati di archiviazione di Azure contempo tooupload possibilità hello e scaricano i dati, quindi utilizzare uno strumento di esplorazione di archiviazione di Azure.

Estrarre l'elenco delle [Esplora archivi Azure](storage-explorers.md) toolearn altre.

## <a name="system-administration"></a>System Administration
Se si richiedono o maggiore familiarità con un'utilità della riga di comando (ad esempio, gli amministratori di sistema), di seguito sono riportate alcune opzioni per tooconsider è:

### <a name="azcopy"></a>AzCopy
AzCopy è un'utilità della riga di comando di Windows progettata per prestazioni elevate copia dei dati tooand da archiviazione di Azure. È inoltre possibile copiare i dati all'interno di un account di archiviazione o tra account di archiviazione diversi.

Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md) toolearn altre.

### <a name="azure-powershell"></a>Azure PowerShell
Azure PowerShell è un modulo che offre cmdlet per la gestione dei servizi in Azure. Si tratta di una shell da riga di comando basata su attività e di un linguaggio di scripting progettato appositamente per gli amministratori di sistema.

Vedere [tramite Azure PowerShell con l'archiviazione di Azure](storage-powershell-guide-full.md) toolearn altre.

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
L'interfaccia della riga di comando di Azure offre un insieme di comandi open source e multipiattaforma per usare i servizi di Azure. L’interfaccia della riga di comando di Azure è disponibile in Windows, OSX e Linux.

Vedere [Using hello CLI di Azure con l'archiviazione di Azure](storage-azure-cli.md) toolearn altre.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Spostamento di molti dati tramite una rete lenta
Una delle maggiori sfide hello associate allo spostamento di grandi quantità di dati è il tempo di trasferimento hello. Se si desiderano tooget dati a/da archiviazione di Azure senza doversi preoccupare dei costi di reti o la scrittura di codice, importazione/esportazione di Azure è una soluzione adeguata.

Vedere [importazione/esportazione di Azure](storage-import-export-service.md) toolearn altre.

## <a name="backing-up-your-data"></a>Backup dei dati
Se è semplicemente necessario toobackup il tooAzure di dati, archiviazione, Backup di Azure è toogo modo hello. Si tratta di una soluzione potente per il backup di dati locali e macchine virtuali di Azure.

Vedere [Azure Backup](../backup/backup-introduction-to-azure-backup.md) toolearn altre.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>L'accesso a dati locali e dal cloud hello
Se è necessaria una soluzione per l'accesso ai dati locali e dal cloud hello, quindi è consigliabile usare soluzione di archiviazione cloud ibrida di Azure, StorSimple. Questa soluzione è costituita da un dispositivo StorSimple fisico che, in modo intelligente, archivia i dati utilizzati di frequente in unità SSD, i dati utilizzati occasionalmente in unità HDD e i dati inattivi, di backup e di archiviazione in Archiviazione di Azure.

Vedere [StorSimple](../storsimple/storsimple-overview.md) toolearn altre.

## <a name="recovering-your-data"></a>Ripristino dei dati
Quando si dispone di applicazioni e carichi di lavoro locale, è necessario una soluzione che consenta il toocontinue di business in esecuzione nell'evento hello un'emergenza. Azure Site Recovery coordina la replica, il failover e il ripristino di macchine virtuali e server fisici. Dati replicati vengono archiviati in archiviazione di Azure, consentendo tooeliminate hello necessario per un data center locale secondario.

Vedere [Azure Site Recovery](../site-recovery/site-recovery-overview.md) toolearn altre.
### <a name="moving-data-faq"></a>Domande frequenti sullo spostamento di dati:
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>È possibile migrare i dischi rigidi virtuali da una regione tooanother senza copiare?
Hello solo modo toocopy dischi rigidi virtuali tra area è toocopy hello dati tra gli account di archiviazione di ogni area. A questo scopo è possibile usare AZCopy. Trasferimento dati con hello utilità della riga di comando di AzCopy toolearn altre, vedere. Per grandi quantità di dati è possibile anche usare il servizio Importazione/Esportazione di Azure. Vedere [importazione/esportazione di Azure](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn altre.
