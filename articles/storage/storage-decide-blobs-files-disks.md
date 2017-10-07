---
title: aaaDeciding quando toouse BLOB di Azure, i file di Azure o i dischi dati di Azure
description: Informazioni su hello modi toostore e accedere ai dati in Azure toohelp che si decide quale toouse tecnologia.
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: 6109affe41e98ed459616a4f91064ded0c74428d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Decidere quando toouse BLOB di Azure, file di Azure o i dischi dati di Azure

Microsoft Azure offre diverse funzionalità in archiviazione di Azure per l'archiviazione e accesso ai dati nel cloud hello. In questo articolo riguarda file di Azure, BLOB e i dischi dati e viene progettato toohelp si sceglie tra queste funzionalità.

## <a name="scenarios"></a>Scenari

Hello nella tabella seguente Confronta file, BLOB e i dischi dati e visualizza gli scenari di esempio appropriata per ognuno.

| Funzionalità | Descrizione | Quando toouse |
|--------------|-------------|-------------|
| **File di Azure** | Fornisce un'interfaccia SMB, le librerie client e un [interfaccia REST](/rest/api/storageservices/file-service-rest-api) toostored file che consente l'accesso da qualsiasi posizione. | Si desidera troppo "sollevare e spostare" un cloud toohello applicazione che usa già dati tooshare API hello file nativo del sistema tra altre applicazioni in esecuzione in Azure.<br/><br/>Si desidera toostore sviluppo e strumenti di debug che è necessario toobe accedere da molte macchine virtuali. |
| **BLOB di Azure** | Fornisce le librerie client e un [interfaccia REST](/rest/api/storageservices/blob-service-rest-api) che consente di dati non strutturati troppo archiviato e utilizzato su larga scala in BLOB in blocchi. | Si desidera lo streaming di applicazioni toosupport e scenari di accesso casuale.<br/><br/>Si desidera toobe tooaccess in grado di dati dell'applicazione da qualsiasi posizione. |
| **Dischi dati di Azure** | Fornisce le librerie client e un [interfaccia REST](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) che consente di toobe dati archiviati in modo permanente e accessibile da un disco rigido virtuale collegato. | Si desidera toolift e spostare le applicazioni che utilizzano tooread le API di file nativi del sistema e scrivere i dischi dati toopersistent.<br/><br/>Si desidera toostore i dati non necessari toobe accessibili dal disco hello toowhich della macchina virtuale all'esterno di hello sono collegati. |

## <a name="comparison-files-and-blobs"></a>Confronto: File e BLOB

Hello nella tabella seguente Confronta file di Azure e BLOB di Azure.  
  
||||  
|-|-|-|  
|**Attributo**|**BLOB di Azure**|**File di Azure**|  
|Opzioni di durabilità|LRS, ZRS, GRS (e RA-GRS per una maggiore disponibilità)|LRS, GRS|  
|Accessibilità|API REST|API REST<br /><br /> SMB 2.1 e SMB 3.0 (API del file system standard)|  
|Connettività|API REST: tutto il mondo|API REST: tutto il mondo<br /><br /> SMB 2.1: nell'area<br /><br /> SMB 3.0: tutto il mondo|  
|Endpoint|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Directory|Spazio dei nomi flat|Oggetti directory veri|  
|Distinzione tra maiuscole e minuscole nei nomi|Fa distinzione tra maiuscole e minuscole.|Non fa distinzione tra maiuscole e minuscole, ma le mantiene così come sono|  
|Capacity|I contenitori di too500 TB|Condivisioni file da 5 TB|  
|Velocità effettiva|Backup too60 MB/s per blob in blocchi|Backup too60 MB/s per condivisione|  
|Dimensioni oggetto|Backup too200 GB/blob in blocchi|Backup o il file too1TB|  
|Capacità fatturata|In base ai byte scritti|In base alle dimensioni di file|  
|Librerie client|Supporto di più lingue|Supporto di più lingue|  
  
## <a name="comparison-files-and-data-disks"></a>Confronto: File e Dischi dati

File di Azure è un complemento di Dischi dati di Azure. Un disco dati può essere solo tooone collegato macchina virtuale di Azure contemporaneamente. I dischi dati sono dischi rigidi virtuali in formato fisso archiviati come BLOB di pagine in archiviazione di Azure e vengono utilizzati da dati durevoli toostore di hello macchina virtuale. Condivisioni file in file di Azure è possibile accedere in hello stessa come disco locale hello è accessibile (usando le API del sistema di file nativi) e possono essere condivise tra molte macchine virtuali.  
 
Hello nella tabella seguente Confronta file di Azure con dischi dati di Azure.  
 
||||  
|-|-|-|  
|**Attributo**|**Dischi dati di Azure**|**File di Azure**|  
|Scope|Esclusivo tooa singola macchina virtuale|Accesso condiviso tra più macchine virtuali|  
|Snapshot e Copia|Sì|No|  
|Configurazione|Connessione all'avvio della macchina virtuale hello|Connesso dopo l'avvio di macchina virtuale hello|  
|Autenticazione|Predefinito|Impostato con comando net use|  
|Pulizia|Automatico|Manuale|  
|Accesso tramite REST|Non è possibile accedere ai file all'interno di hello disco rigido virtuale|È possibile accedere ai file archiviati in una condivisione|  
|Dimensioni massime|Disco di 1 TB|Condivisione file da 5 TB e file da 1 TB nella condivisione|  
|IOPS di 8 KB massimo|500 IOPS|1000 IOps|  
|Velocità effettiva|Backup too60 MB/s per disco|Backup too60 MB/s per condivisione File|  

## <a name="next-steps"></a>Passaggi successivi

Nel prendere decisioni sulla modalità di archiviazione e di accedere ai dati, è inoltre consigliabile costi hello coinvolti. Per altre informazioni, vedere [Prezzi di Archiviazione di Azure](https://azure.microsoft.com/pricing/details/storage/).
  
Alcune funzionalità SMB non sono applicabili toohello cloud. Per ulteriori informazioni, vedere [funzionalità non supportate dal servizio File di Azure hello](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Per ulteriori informazioni sui dischi dati, vedere [gestione dei dischi e immagini](storage-about-disks-and-vhds-linux.md) e [come tooAttach tooa un disco dati macchina virtuale Windows](../virtual-machines/windows/classic/attach-disk.md).
