---
title: aaaBackup e ripristino per SQL Server | Documenti Microsoft
description: Vengono descritte considerazioni sul backup e sul ripristino per i database di SQL Server in esecuzione in macchine virtuali di Azure.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Backup e ripristino per SQL Server in Macchine virtuali di Azure
## <a name="overview"></a>Panoramica
Archiviazione di Azure mantiene 3 copie di ogni macchina virtuale di Azure disco tooguarantee contro la perdita di dati o il danneggiamento dei dati fisica. A differenza di on-premise, di conseguenza, tooworry su questi non è necessario. Tuttavia, è comunque consigliabile eseguire backup del tooprotect di database di SQL Server dagli errori di applicazione o un utente (ad esempio, l'inserimento di dati errato o l'eliminazione di una tabella) e toorestore in grado di corso tooa punto nel tempo.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Per SQL Server in esecuzione in macchine virtuali di Azure, è possibile utilizzare backup nativo e ripristinare tecniche utilizzando dischi collegati per la destinazione di hello hello dei file di backup. Tuttavia, è una limitazione del numero di dischi che è possibile collegare tooan macchina virtuale di Azure, in base a hello toohello [dimensioni della macchina virtuale hello](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). È inoltre disponibile sovraccarico hello tooconsider Gestione disco.

A partire da SQL Server 2014, è possibile eseguire il backup e ripristino tooMicrosoft nell'archiviazione Blob di Azure. In SQL Server 2016 sono disponibili miglioramenti per questa opzione. Inoltre, per i file di database memorizzati nell'archiviazione BLOB di Microsoft Azure, SQL Server 2016 fornisce un'opzione per eseguire backup quasi istantanei e ripristini rapidi tramite gli snapshot di Azure. Questo articolo offre una panoramica di queste opzioni, mentre le informazioni aggiuntive sono disponibili in [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Per una descrizione delle opzioni di hello di backup dei database di dimensioni molto grandi, vedere [strategie di Backup del Database Server SQL a più Terabyte macchine virtuali di Azure](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

Hello nelle sezioni seguenti vengono includono versioni diverse di informazioni toohello specifiche di SQL Server supportate in una macchina virtuale di Azure.

## <a name="sql-server-virtual-machines"></a>Macchine virtuali di SQL Server
Quando l'istanza di SQL Server è in esecuzione in una macchina virtuale di Azure, i file di database si trovano già su dischi di dati in Azure. Questi dischi risiedono nell'archivio BLOB di Azure. Pertanto hello motivi del backup di approcci del database e hello che eseguire modifica leggermente. Prendere in considerazione i seguenti hello. 

* Non è più necessario tooperform protezione tooprovide i backup del database in caso di errore hardware o media perché Microsoft Azure offre la protezione come parte del servizio Microsoft Azure hello.
* È comunque necessario tooperform database backup tooprovide protezione contro errori dell'utente o per scopi di archiviazione, motivi normativi o per scopi amministrativi.
* È possibile archiviare i file di backup hello direttamente in Azure. Per ulteriori informazioni, vedere le sezioni che forniscono informazioni aggiuntive per hello versioni diverse di SQL Server seguenti hello.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 supporta le funzionalità di [backup e ripristino con BLOB di Azure](https://msdn.microsoft.com/library/jj919148.aspx) disponibili in SQL Server 2014. Ma include anche hello seguenti miglioramenti:

| Miglioramento nella versione 2016 | Dettagli |
| --- | --- |
| **Striping** |Per eseguire il backup tooMicrosoft archiviazione blob di Azure, SQL Server 2016 supporta il backup toomultiple BLOB tooenable il backup dei database di grandi dimensioni, backup tooa massimo pari a 12,8 TB. |
| **Backup di snapshot** |Tramite l'utilizzo di hello di snapshot di Azure, Backup di Snapshot di File di SQL Server fornisce backup quasi istantanei e ripristini rapido per i file di database archiviati usando il servizio di archiviazione Blob di Azure hello. Questa funzionalità consente di toosimplify i criteri di backup e ripristino. Backup di snapshot di file supporta anche il ripristino temporizzato. Per altre informazioni, vedere [Backup di snapshot di file di database in Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx). |
| **Pianificazione del backup gestito** |Backup gestito di SQL Server tooAzure supporta ora pianificazioni personalizzate. Per ulteriori informazioni, vedere [tooMicrosoft Backup gestito di SQL Server Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Per un'esercitazione di funzionalità hello di SQL Server 2016 quando si utilizza l'archiviazione Blob di Azure, vedere [esercitazione: uso il servizio di archiviazione Blob di Microsoft Azure hello con i database di SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 include i seguenti miglioramenti hello:

1. **Backup e ripristino tooAzure**:
   
   * *Backup di SQL Server tooURL* è incluso il supporto in SQL Server Management Studio. Hello opzione tooback backup tooAzure è ora disponibile quando si utilizza l'attività di Backup o ripristino o creazione guidata piano di manutenzione in SQL Server Management Studio. Per ulteriori informazioni, vedere [tooURL di Backup di SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *Backup gestito di SQL Server tooAzure* include nuove funzionalità che consente la gestione di backup automatizzata. Ciò è particolarmente utile per l'automazione della gestione dei backup per le istanze di SQL Server 2014 in esecuzione in una macchina di Azure. Per ulteriori informazioni, vedere [tooMicrosoft Backup gestito di SQL Server Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Backup automatizzato* fornisce l'automazione aggiuntive consentono di tooautomatically *tooAzure Backup gestito di SQL Server* in tutti i database nuovi ed esistenti per una VM SQL Server in Azure. Per altre informazioni, vedere [Backup automatizzato per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-automated-backup.md).
   * Per una panoramica di tutte le opzioni di hello per tooAzure di Backup di SQL Server 2014, vedere [SQL Server Backup e ripristino con il servizio di archiviazione Blob di Microsoft Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Crittografia**: SQL Server 2014 supporta la crittografia dei dati durante la creazione di un backup. Supporta diversi algoritmi di crittografia e hello utilizzare osf un certificato o chiave asimmetrica. Per altre informazioni, vedere [Crittografia del backup](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Per informazioni dettagliate sul backup e il ripristino di SQL Server 2012, vedere [Backup e ripristino di database SQL Server (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx).

A partire da SQL Server 2012 SP1 aggiornamento cumulativo 2, è possibile eseguire il backup tooand ripristino dal servizio di archiviazione Blob di Azure hello. Questa funzionalità avanzata può essere utilizzato tooback dei database di SQL Server in un Server SQL in esecuzione in un'istanza locale o di una macchina virtuale di Azure. Per altre informazioni, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Alcuni dei vantaggi hello utilizzando il servizio di archiviazione Blob di Azure hello includono hello possibilità toobypass hello 16 limite disco per i dischi collegati, facilità di gestione, la disponibilità diretta hello hello backup tooanother dell'istanza del file dell'istanza di SQL Server in esecuzione in un tipo di Azure macchina virtuale o un'istanza locale per scopi di ripristino di emergenza o di migrazione. Per un elenco completo dei vantaggi toousing un servizio di archiviazione blob di Azure per i backup di SQL Server, vedere hello *vantaggi* sezione [SQL Server Backup e ripristino con il servizio di archiviazione Blob di Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Per informazioni sulla risoluzione dei problemi e sulle procedure consigliate, vedere [Procedure consigliate di backup e ripristino (servizio di archiviazione BLOB di Azure)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx).

## <a name="sql-server-2008"></a>SQL Server 2008
Per il backup e ripristino in SQL Server 2008 R2, vedere [Backup e ripristino di database in SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Per il backup e ripristino in SQL Server 2008, vedere [Backup e ripristino di database in SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Passaggi successivi
Se si pianifica la distribuzione di SQL Server in una macchina virtuale di Azure, è possibile trovare indicazioni provisioning in hello segue esercitazione: [il Provisioning di una macchina virtuale di SQL Server in Azure con Azure Resource Manager](virtual-machines-windows-portal-sql-server-provision.md).

Anche se il backup e ripristino può essere utilizzati toomigrate i dati, sono potenzialmente più facile tooSQL i percorsi di migrazione dati Server in una macchina virtuale di Azure. Per una descrizione completa delle opzioni di migrazione e i suggerimenti, vedere [la migrazione di un Server in una macchina virtuale Azure di tooSQL Database](virtual-machines-windows-migrate-sql.md).

Esaminare altre [risorse per l'esecuzione di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

