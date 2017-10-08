---
title: aaaMigrate un tooSQL database Server SQL Server in una macchina virtuale | Documenti Microsoft
description: Informazioni su come un utente locale toomigrate database tooSQL Server in una macchina virtuale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Eseguire la migrazione di un tooSQL database Server SQL Server in una macchina virtuale di Azure

Esistono diversi metodi toomigrate un tooSQL di database utente di SQL Server on-premise Server in una macchina virtuale di Azure. In questo articolo verrà descrivere brevemente vari metodi e consigliabile migliore hello per vari scenari.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Quali sono i metodi di migrazione primario hello?
metodi di migrazione primario Hello sono:

* Eseguire il backup in locale utilizzando la compressione e manualmente file di backup di copia hello in hello macchina virtuale di Azure
* Eseguire un backup tooURL e il ripristino nella macchina virtuale di Azure dall'URL hello hello
* Scollegare e quindi copiare hello dati e log file tooAzure archiviazione blob e quindi ricollegare tooSQL Server nella macchina virtuale di Azure dall'URL
* Convertire fisico locale computer VHD tooHyper-V, caricare tooAzure nell'archiviazione Blob e quindi distribuire come nuova macchina virtuale con caricamento VHD
* Spedizione del disco rigido tramite il servizio di Importazione/Esportazione di Windows
* Se dispone di una distribuzione di AlwaysOn locale, utilizzare hello [Aggiungi Replica Azure](../classic/sql-onprem-availability.md) toocreate una replica in Azure e quindi il failover, verso l'istanza del database Azure toohello utenti
* Utilizzo di SQL Server [la replica transazionale](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server come server di sottoscrizione dell'istanza e quindi disabilitare la replica, scegliendo l'istanza del database Azure toohello utenti

> [!TIP]
> È inoltre possibile utilizzare questi stessi database toomove tecniche tra macchine virtuali di SQL Server in Azure. Non è ad esempio, una macchina virtuale immagine della raccolta di SQL Server da una versione o edizione tooanother di tooupgrade metodo supportato. In questo caso, si deve creare una nuova macchina virtuale di SQL Server con hello/edizione della nuova versione e quindi usare una delle tecniche di migrazione hello in questo articolo di toomove dei database. 

## <a name="choosing-your-migration-method"></a>Scelta del metodo di migrazione
Prestazioni di trasferimento ottimale, eseguire la migrazione di file di database hello in hello macchina virtuale di Azure utilizzando un file di backup compresso.

tempo di inattività toominimize durante il processo di migrazione di database hello, utilizzare l'opzione AlwaysOn hello o hello la replica transazionale.

Se non è possibile toouse hello sopra metodi, eseguire manualmente la migrazione del database. In questo modo, verranno in genere iniziano con un backup del database seguito da una copia di backup del database hello in Azure e quindi eseguire un ripristino del database. È possibile anche copiare i file di database hello stessi in Azure e quindi collegarli. Esistono diversi metodi che consentono di eseguire questo processo di migrazione manuale di un database in una macchina virtuale di Azure.

> [!NOTE]
> Quando si esegue l'aggiornamento da versioni precedenti di SQL Server tooSQL Server 2014 o SQL Server 2016, è necessario considerare se sono necessarie modifiche. È consigliabile indirizzare tutte le dipendenze sulle funzionalità non supportate dalla nuova versione di hello di SQL Server come parte del progetto di migrazione. Per ulteriori informazioni sulle edizioni supportata di hello e sugli scenari, vedere [aggiornamento tooSQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

Hello nella tabella seguente elenca ogni metodo di migrazione primario hello e viene descritto quando utilizzare hello di ogni metodo è più appropriato.

| Metodo | Versione del database di origine | Versione del database di destinazione | Vincolo di dimensioni del backup del database di origine | Note |
| --- | --- | --- | --- | --- |
| [Eseguire il backup in locale utilizzando la compressione e manualmente file di backup di copia hello in hello macchina virtuale di Azure](#backup-and-restore) |SQL Server 2005 o versione successiva |SQL Server 2005 o versione successiva |[Limite di archiviazione della macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | È una tecnica molto semplice e ben collaudata per spostare i database tra più computer. |
| [Eseguire un backup tooURL e il ripristino nella macchina virtuale di Azure dall'URL hello hello](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 o versione successiva |SQL Server 2012 SP1 CU2 o versione successiva |< 12.8 TB per SQL Server 2016, in caso contrario < 1 TB | Questo metodo è solo un altro modo toomove hello file di backup toohello VM utilizzando l'archiviazione di Azure. |
| [Scollegare e quindi copiare hello dati e log file tooAzure archiviazione blob e quindi ricollegare tooSQL Server nella macchina virtuale di Azure dall'URL](#detach-and-attach-from-url) |SQL Server 2005 o versione successiva |SQL Server 2014 o versione successiva |[Limite di archiviazione della macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilizzare questo metodo quando si pianifica troppo[archiviare questi file tramite il servizio di archiviazione Blob di Azure hello](https://msdn.microsoft.com/library/dn385720.aspx) e collegarli tooSQL Server in esecuzione in una macchina virtuale di Azure, in particolare con i database di dimensioni molto grandi |
| [Converti locale computer i dischi rigidi virtuali tooHyper-V, caricare tooAzure nell'archiviazione Blob e quindi distribuire una nuova macchina virtuale con disco rigido virtuale caricato](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 o versione successiva |SQL Server 2005 o versione successiva |[Limite di archiviazione della macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Quando utilizzare [riportare la propria licenza di SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), durante la migrazione di un database a cui verrà eseguita in una versione precedente di SQL Server o quando la migrazione dei database di sistema e utente come parte di hello migrazione del database dipende da altri i database utente e/o i database di sistema. |
| [Spedizione del disco rigido tramite il servizio di Importazione/Esportazione di Windows](#ship-hard-drive) |SQL Server 2005 o versione successiva |SQL Server 2005 o versione successiva |[Limite di archiviazione della macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Hello utilizzare [Windows servizio di importazione/esportazione](../../../storage/common/storage-import-export-service.md) quando il metodo di copia manuale è troppo lento, ad esempio con i database di dimensioni molto grandi |
| [Utilizzare hello Aggiungi Replica Azure](../classic/sql-onprem-availability.md) |SQL Server 2012 o versione successiva |SQL Server 2012 o versione successiva |[Limite di archiviazione della macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Riduce al minimo il tempo di inattività; da usare quando si ha una distribuzione locale di AlwaysOn |
| [Uso della replica transazionale di SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 o versione successiva |SQL Server 2005 o versione successiva |[Limite di archiviazione della macchina virtuale di Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilizzare questa opzione quando è necessario toominimize i tempi di inattività e non dispone di una distribuzione locale di AlwaysOn |

## <a name="backup-and-restore"></a>Backup e ripristino
Eseguire il backup del database con la compressione, copiare hello backup toohello macchina virtuale e quindi ripristinare il database di hello. Se il file di backup è maggiore di 1 TB, è necessario eseguire lo striping perché hello la dimensione massima di un disco di macchina virtuale è di 1 TB. Utilizzare hello seguendo i passaggi generali toomigrate un database utente utilizzando il metodo manuale:

1. Eseguire un percorso locale di tooan backup completo del database.
2. Creare o caricare una macchina virtuale con la versione di hello di SQL Server desiderato.
3. Configurare la connettività in base ai requisiti specifici. Vedere [connessione macchina virtuale di SQL Server in Azure (gestione delle risorse) tooa](virtual-machines-windows-sql-connect.md).
4. Copiare il tooyour di file di backup VM comando remote desktop, in Esplora risorse o hello copia da un prompt dei comandi.

## <a name="backup-toourl-and-restore"></a>TooURL backup e ripristino
Invece il backup dei file locale tooa, è possibile usare hello [tooURL backup](https://msdn.microsoft.com/library/dn435916.aspx) e quindi ripristinare dall'URL toohello macchina virtuale. Con SQL Server 2016, il set di backup con striping è supportato, è consigliato per le prestazioni e necessari limiti delle dimensioni hello tooexceed per ogni blob. Per i database di dimensioni molto grandi, hello l'uso di hello [Windows servizio di importazione/esportazione](../../../storage/common/storage-import-export-service.md) è consigliato.

## <a name="detach-and-attach-from-url"></a>Rimuovere e allegare dall'URL
I file di database e log di scollegamento e li trasferiscono troppo[archiviazione Blob di Azure](https://msdn.microsoft.com/library/dn385720.aspx). Quindi, collegare il database di hello dall'URL hello nella macchina virtuale di Azure. Utilizzare questo metodo se si desidera tooreside i file di database fisico hello nell'archiviazione Blob. Ciò può risultare utile per i database di dimensioni molto grandi. Utilizzare hello seguendo i passaggi generali toomigrate un database utente utilizzando il metodo manuale:

1. Scollegare il file di database hello dall'istanza del database locale hello.
2. Copiare i file del database scollegato hello nell'archiviazione blob di Azure utilizzando hello [utilità della riga di comando di AZCopy](../../../storage/common/storage-use-azcopy.md).
3. Collegare i file del database hello dall'istanza di SQL Server hello Azure URL toohello in hello macchina virtuale di Azure.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>Convertire tooVM e tooURL di caricare e distribuire come nuova macchina virtuale
Utilizzare questo toomigrate metodo tutti i database utente e di sistema in una macchina virtuale di tooAzure istanza di SQL Server di on-premise. Utilizzare hello seguendo i passaggi generali toomigrate un'intera istanza di SQL Server utilizzando il metodo manuale:

1. Converti fisico o virtuale macchine dischi rigidi virtuali tooHyper-V utilizzando [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Caricare il file di disco rigido virtuale tooAzure archiviazione usando hello [cmdlet Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Distribuire una nuova macchina virtuale tramite hello caricato disco rigido virtuale.

> [!NOTE]
> toomigrate un'intera applicazione, è consigliabile utilizzare [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Spedizione del disco rigido
Hello utilizzare [metodo del servizio di importazione/esportazione Windows](../../../storage/common/storage-import-export-service.md) tootransfer grandi quantità di dati di file tooAzure nell'archiviazione Blob in situazioni in cui caricamento hello rete viene impedito perché costoso o difficile da effettuare. Con questo servizio, si invia uno o più unità disco rigido contenente tale dati tooan data center di Azure, in cui i dati verranno caricati tooyour account di archiviazione.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'esecuzione di SQL Server in Macchine virtuali di Azure, vedere [Panoramica di SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Per istruzioni sulla creazione di una macchina virtuale di Azure SQL Server da un'immagine acquisita, vedere [suggerimenti sulla clonazione macchine virtuali di SQL Azure da immagini acquisite](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) sul blog di ingegneri di SQL Server hello.

