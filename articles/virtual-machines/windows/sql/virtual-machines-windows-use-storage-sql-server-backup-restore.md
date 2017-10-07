---
title: aaaHow toouse archiviazione di Azure per SQL Server backup e ripristino | Documenti Microsoft
description: Informazioni su come tooback di SQL Server tooAzure archiviazione. Illustra i vantaggi di hello del backup dei database SQL tooAzure archiviazione.
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Usare Archiviazione di Azure per il backup e il ripristino di SQL Server
## <a name="overview"></a>Panoramica
A partire da SQL Server 2012 SP1 CU2, ora è possibile scrivere backup di SQL Server direttamente toohello il servizio di archiviazione Blob di Azure. È possibile utilizzare questo tooback funzionalità di ripristino tooand dal servizio Blob di Azure hello con un database di SQL Server locale o un database di SQL Server in una macchina virtuale di Azure. Backup toocloud offre i vantaggi della disponibilità, replica geografica di archiviazione esterne illimitate e facilità di migrazione dei dati tooand dal cloud hello. È possibile eseguire istruzioni BACKUP o RESTORE usando T-SQL o SMO.

SQL Server 2016 introduce nuove funzionalità; è possibile utilizzare [backup snapshot di file](http://msdn.microsoft.com/library/mt169363.aspx) tooperform backup quasi istantanei e ripristini estremamente rapido.

Questo argomento illustra i motivi per cui si potrebbe scegliere toouse archiviazione di Azure per i backup di SQL e quindi descrive i componenti di hello coinvolti. È possibile utilizzare risorse hello fornite alla fine hello hello articolo tooaccess dettagliate e informazioni aggiuntive toostart utilizzando questo servizio con i backup di SQL Server.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Vantaggi dell'utilizzo hello servizio Blob di Azure per i backup di SQL Server
Quando si eseguono backup di SQL Server, è necessario affrontare diverse problematiche, Queste sfide includono la gestione di archiviazione, rischio di errori di archiviazione, accesso archiviazione toooff sito e configurazione hardware. Molti di questi problemi vengono indirizzate mediante il servizio di archiviazione Blob di Azure hello per i backup di SQL Server. Prendere in considerazione hello seguenti vantaggi:

* **Semplicità d'uso**: l'archiviazione dei backup in BLOB di Azure può essere un'opzione esterna tooaccess utile, flessibile e semplice. Creazione di archiviazione esterne per i backup di SQL Server possono essere semplici quanto la modifica esistente degli script o processi hello toouse **BACKUP tooURL** sintassi. Capacità di archiviazione esterne deve essere sufficientemente lontana dalla posizione tooprevent di hello produzione database una singola situazione di emergenza possa influire sia hello fuori sede e percorsi di database di produzione. Scegliendo troppo[BLOB di Azure di replica geografica](../../../storage/common/storage-redundancy.md), si dispone di un ulteriore livello di protezione in caso di hello un'emergenza che potrebbe influire sull'intera area hello.
* **Archivio di backup**: hello servizio di archiviazione Blob di Azure offre un migliore nastro toohello alternativo usato spesso backup tooarchive opzione. L'archiviazione su nastro potrebbe richiedere trasporto fisico tooan esterna struttura e misure tooprotect hello media. L'archiviazione dei backup nell'archiviazione BLOB di Azure rappresenta un'opzione di archiviazione istantanea, estremamente disponibile e durevole.
* **Hardware gestito**: con i servizi di Azure non viene addebitato alcun sovraccarico per la gestione dell'hardware. Servizi di Azure gestire hardware hello e forniscono la replica geografica per garantire ridondanza e protezione da eventuali errori hardware.
* **Archiviazione illimitata**: abilitando un BLOB tooAzure backup diretto, si dispone di accesso toovirtually archiviazione illimitata. In alternativa, eseguire il backup di un disco di macchina virtuale di Azure tooan presenta limiti in base alle dimensioni della macchina. È un toohello limita il numero di dischi è possibile collegare tooan macchina virtuale di Azure per i backup. Tale limite è di 16 dischi per un'istanza molto grande e un numero di dischi inferiore per istanze più piccole.
* **Disponibilità di backup**: backup archiviati nel BLOB di Azure sono disponibili da qualsiasi luogo e in qualsiasi momento e possono essere facilmente accessibili per tooeither ripristini un Server SQL locale o un altro Server SQL in esecuzione in una macchina di virtuale di Azure, senza hello necessario Per collegare/scollegare il database o scaricare e collegare hello disco rigido virtuale.
* **Costo**: si paga solo hello servizio utilizzato. Può rivelarsi una soluzione economica per il backup e l'archiviazione fuori sede. Vedere hello [calcolatore dei costi Azure](http://go.microsoft.com/fwlink/?LinkId=277060 "calcolatore dei costi"), hello e [dei prezzi di Azure articolo](http://go.microsoft.com/fwlink/?LinkId=277059 "prezzi articolo") per ulteriori informazioni informazioni.
* **Snapshot di archiviazione**: quando i file di database sono archiviati in un blob di Azure e si utilizza SQL Server 2016, è possibile utilizzare [backup snapshot di file](http://msdn.microsoft.com/library/mt169363.aspx) tooperform backup quasi istantanei e ripristini estremamente rapido.

Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Azure](http://go.microsoft.com/fwlink/?LinkId=271617).

nelle due sezioni che seguono Hello introdurre servizio di archiviazione Blob di Azure hello, inclusi i componenti di SQL Server necessarie hello. È importante toounderstand hello e componenti i backup per utilizzo interazione toosuccessfully e il ripristino dal servizio di archiviazione Blob di Azure hello.

## <a name="azure-blob-storage-service-components"></a>Componenti del servizio di archiviazione BLOB di Azure
componenti di Azure seguenti Hello vengono utilizzati per eseguire il backup toohello servizio di archiviazione Blob di Azure.

| Componente | Descrizione |
| --- | --- |
| **Storage Account** |account di archiviazione Hello è hello punto di partenza per tutti i servizi di archiviazione. tooaccess un servizio di archiviazione Blob di Azure, creare innanzitutto un account di archiviazione di Azure. Per ulteriori informazioni sul servizio di archiviazione Blob di Azure, vedere [come toouse hello servizio di archiviazione Blob di Azure](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Contenitore** |Un contenitore fornisce il raggruppamento di un set di BLOB ed è in grado di archiviare un numero di BLOB illimitato. toowrite un tooan backup di SQL Server il servizio Blob di Azure, è necessario disporre almeno contenitore radice hello creato. |
| **BLOB** |file di qualsiasi tipo o dimensione. I BLOB sono indirizzabili utilizzando hello seguendo il formato di URL: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Per altre informazioni sui BLOB di pagine, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>Componenti di SQL Server
componenti di SQL Server seguenti Hello vengono utilizzati per eseguire il backup toohello servizio di archiviazione Blob di Azure.

| Componente | Descrizione |
| --- | --- |
| **URL** |Un URL specifica un file di backup univoco tooa di identificatore URI (Uniform Resource). URL di Hello è usato tooprovide hello percorso e il nome del file di backup di SQL Server hello. Hello URL deve puntare tooan blob effettivo, non solo un contenitore. Se il blob hello non esiste, viene creato. Se viene specificato un blob esistente, BACKUP non riesce, a meno che non hello > è specificata l'opzione WITH FORMAT. Hello seguito è riportato un esempio di URL hello specificate nel comando BACKUP hello: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS non è obbligatorio ma è consigliato. |
| **Credenziali** |informazioni Hello tooconnect richiesto e l'autenticazione tooAzure servizio di archiviazione Blob viene archiviate come credenziale.  In ordine per SQL Server toowrite backup tooan Blob di Azure o il ripristino da esso, è necessario creare una credenziale di SQL Server. Per altre informazioni, vedere [Credenziali di SQL Server](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Se si sceglie toocopy e carica un servizio di archiviazione Blob di Azure di toohello file di backup, è necessario utilizzare un tipo di blob di pagina come opzione di archiviazione, se si intende toouse questo file per operazioni di ripristino. Il comando RESTORE da un tipo di BLOB in blocchi non riuscirà e restituirà un errore.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
1. Se non se ne possiede già uno, creare un account di Azure. Se si sta valutando Azure, è consigliabile hello [versione di valutazione gratuita](https://azure.microsoft.com/free/).
2. Quindi passare a uno dei seguenti esercitazioni che illustrano la creazione di un account di archiviazione e l'esecuzione di un ripristino hello.
   
   * **SQL Server 2014**: [esercitazione: Backup di SQL Server 2014 e ripristino tooMicrosoft servizio di archiviazione Blob di Azure](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [esercitazione: uso il servizio di archiviazione Blob di Microsoft Azure hello con i database di SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)
3. Esaminare la documentazione aggiuntiva, a partire da [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

Se si verificano problemi, consultare l'argomento di hello [tooURL di Backup di SQL Server Best Practices and Troubleshooting](https://msdn.microsoft.com/library/jj919149.aspx).

Per una descrizione delle altre opzioni di backup e ripristino, vedere [Backup e ripristino per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-backup-recovery.md).

