---
title: dischi aaaExclude dalla protezione dati con Azure Site Recovery | Documenti Microsoft
description: "Viene descritto come e perché tooexclude VM dischi dalla replica per gli scenari di VMware tooAzure e tooAzure Hyper-V."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Escludere dischi dalla replica
In questo articolo viene descritto come tooexclude dischi dalla replica. Questa esclusione può ottimizzare la larghezza di banda replica hello utilizzato o ottimizzare le risorse sul lato destinazione hello che utilizzano tali dischi. funzionalità di Hello è supportato per scenari di VMware tooAzure e tooAzure Hyper-V.

## <a name="prerequisites"></a>Prerequisiti

Per impostazione predefinita, vengono replicati tutti i dischi presenti in un computer. tooexclude un disco dalla replica, è necessario installare manualmente hello servizio di mobilità nel computer di hello prima di abilitare la replica se si esegue la replica da tooAzure VMware.


## <a name="why-exclude-disks-from-replication"></a>Perché escludere dischi dalla replica
Spesso è necessario escludere dischi dalla replica per i motivi riportati di seguito:

- dati Hello sono variati sul disco hello escluso non siano importanti o non è necessario toobe replicati.

- Si desidera le risorse di archiviazione e rete toosave replicando non questa varianza.

## <a name="what-are-hello-typical-scenarios"></a>Quali sono gli scenari tipici di hello?
È possibile identificare alcuni esempi specifici di varianza dei dati particolarmente adatti all'esclusione, Esempi possono essere scrive file di paging tooa (pagefile.sys) e file di tempdb toohello di Microsoft SQL Server. A seconda del carico di lavoro hello e sottosistema di archiviazione hello, file di paging hello può registrare una quantità significativa di varianza. Tuttavia, la replica di dati da hello sito primario tooAzure sarebbe molte risorse. Di conseguenza, è possibile utilizzare hello replica toooptimize passaggi di una macchina virtuale con un solo disco virtuale che dispone sia del sistema operativo hello e file di paging hello seguenti:

1. Divisione hello singolo disco virtuale in due dischi virtuali. Un disco virtuale con sistema operativo hello hello altri è il file di paging hello.
2. Escludere il disco del file di paging hello dalla replica.

Analogamente, è possibile utilizzare i seguenti passaggi toooptimize un disco con entrambi tempdb di Microsoft SQL Server hello file hello e hello file di database di sistema:

1. Mantenere il database di sistema hello e di tempdb in dischi diversi due.
2. Escludere il disco di tempdb hello dalla replica.

## <a name="how-tooexclude-disks-from-replication"></a>Come tooexclude dischi dalla replica?

### <a name="vmware-tooazure"></a>VMware tooAzure
Seguire hello [abilitare la replica](site-recovery-vmware-to-azure.md) tooprotect del flusso di lavoro una macchina virtuale dal portale di Azure Site Recovery hello. In hello quarto passaggio del flusso di lavoro hello utilizzare hello **tooREPLICATE disco** dischi tooexclude colonna dalla replica. Per impostazione predefinita, tutti i dischi sono selezionati per la replica. Deselezionare la casella di controllo hello di dischi che si desidera tooexclude dalla replica e quindi completa hello passaggi tooenable.

![Escludere i dischi dalla replica e abilitare la replica per il failback tooAzure VMware](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * È possibile escludere solo i dischi che sono già installato servizio di mobilità di hello. È necessario il servizio di mobilità hello installazione toomanually, perché servizio di mobilità hello viene installato solo tramite il meccanismo di push hello dopo aver abilitata la replica.
> * Solo i dischi di base possono essere esclusi dalla replica. Non è possibile escludere dischi del sistema operativo o dinamici.
> * Dopo aver abilitato la replica, non è più possibile aggiungere o rimuovere dischi da replicare. Se si desidera tooadd o esclude un disco, è necessario toodisable protezione per il computer di hello e quindi Abilita di nuovo.
> * Se si esclude un disco è sufficiente per toooperate un'applicazione, dopo il failover tooAzure, è necessario disco hello toocreate manualmente in Azure in modo che sia possibile eseguire l'applicazione hello replicato. In alternativa, è possibile integrare automazione di Azure in un disco di ripristino piano toocreate hello durante il failover della macchina hello.
> * Macchina virtuale Windows: per i dischi creati manualmente in Azure non viene eseguito il failback. Se, ad esempio, si esegue il failover di tre dischi e se ne creano due direttamente in Macchine virtuali di Azure, viene eseguito il failback solo dei tre dischi sottoposti a failover. È possibile includere i dischi che è stato creato manualmente il failback o riprotezione da tooAzure locale.
> * Macchina virtuale Linux: per i dischi creati manualmente in Azure non viene eseguito il failback. Se, ad esempio, si esegue il failover di tre dischi e se ne creano due direttamente in Macchine virtuali di Azure, viene eseguito il failback di tutti e cinque i dischi. Non è possibile escludere i dischi creati manualmente dall'operazione di failback.
>

### <a name="hyper-v-tooazure"></a>TooAzure Hyper-V
Seguire hello [abilitare la replica](site-recovery-hyper-v-site-to-azure.md) tooprotect del flusso di lavoro una macchina virtuale dal portale di Azure Site Recovery hello. In hello quarto passaggio del flusso di lavoro hello utilizzare hello **tooREPLICATE disco** dischi tooexclude colonna dalla replica. Per impostazione predefinita, tutti i dischi sono selezionati per la replica. Deselezionare la casella di controllo hello di dischi che si desidera tooexclude dalla replica e quindi completa hello passaggi tooenable.

![Escludere i dischi dalla replica e abilitare la replica per il failback tooAzure Hyper-V](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * È possibile escludere dalla replica solo dischi di base. Non è possibile escludere dischi del sistema operativo e non è consigliabile escludere dischi dinamici. Azure Site Recovery non è possibile identificare il disco rigido virtuale (VHD) è di base o dinamici nella macchina virtuale guest di hello.  Se tutti i dischi dei volumi dinamici dipendenti non vengono esclusi, disco dinamico protetto hello diventa un disco guasto in una macchina virtuale di failover e hello dati presenti sul disco non sono accessibili.
> * Dopo aver abilitato la replica, non è più possibile aggiungere o rimuovere dischi da replicare. Se si desidera tooadd o esclude un disco, è necessario toodisable protezione per la macchina virtuale hello e quindi Abilita di nuovo.
> * Se si esclude un disco è sufficiente per toooperate un'applicazione, dopo il failover tooAzure è necessario toocreate hello disco manualmente in Azure in modo che sia possibile eseguire l'applicazione hello replicato. In alternativa, è possibile integrare automazione di Azure in un disco di ripristino piano toocreate hello durante il failover della macchina hello.
> * Per i dischi creati manualmente in Azure non viene eseguito il failback. Ad esempio, se si esito negativo su tre dischi e creare due dischi direttamente in macchine virtuali di Azure, solo tre dischi che sono stati eseguiti il failover non verranno eseguiti nuovamente da Azure tooHyper-V. È possibile includere i dischi che sono stati creati manualmente la replica inversa da tooAzure Hyper-V o il failback.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Scenari end-to-end di esclusione dei dischi
Si consideri una funzione di due scenari toounderstand hello esclusioni disco:

- Disco del tempdb di SQL Server
- Disco del file di paging (pagefile.sys)

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Escludere il disco tempdb di SQL Server hello
Si prenda ad esempio una macchina virtuale di SQL Server con un tempdb che è possibile escludere.

nome di Hello del disco virtuale hello è SalesDB.

Di seguito sono riportati i dischi nella macchina virtuale di origine hello:


**Nome del disco** | **N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disk1| Disk1 | D:\ | Database di sistema SQL e Database1 dell'utente
DB-Disco2 (disco di hello escluse dalla protezione) | Disk2 | E:\ | File temporanei
DB-Disk3 (disco di hello escluse dalla protezione) | Disk3 | F:\ | Database tempdb SQL (percorso della cartella (F:\MSSQL\Data\) </br/>< / br/>, annotare il percorso di cartella hello prima del failover.
DB-Disk4 | Disk4 |G:\ |Database2 dell'utente

Poiché varianza dei dati su due dischi della macchina virtuale hello è temporanea, mentre si protegge una macchina virtuale di hello SalesDB, escludere Disco2 e Disk3 dalla replica. Azure Site Recovery non eseguirà la replica di questi dischi, In caso di failover, i dischi non sarà presenti nella macchina virtuale di failover hello in Azure.

Di seguito sono riportati i dischi nella macchina virtuale di Azure dopo il failover hello:

**N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | ---
DISK0 | C:\ | Disco del sistema operativo
Disk1 | E:\ | Archiviazione temporanea </br / >< / br / > Azure aggiunge il disco e assegna la lettera di unità disponibile prima di hello.
Disk2 | D:\ | Database di sistema SQL e Database1 dell'utente
Disk3 | G:\ | Database2 dell'utente

Poiché Disco2 e Disk3 sono stati esclusi dalla macchina virtuale di hello SalesDB, e: è hello prima lettera di unità dall'elenco disponibile hello. Azure assegna volume di archiviazione temporanea e: toohello. Per tutti i dischi hello replicato, rimangono lettere di unità di hello hello stesso.

Disk3, ovvero disco tempdb SQL hello (percorso della cartella tempdb F:\MSSQL\Data\), è stata esclusa dalla replica. disco Hello non è disponibile nella macchina virtuale di hello failover. Di conseguenza, hello servizio SQL è in stato di interruzione e richiede il percorso di F:\MSSQL\Data hello.

Esistono due modi toocreate questo percorso:

- Aggiungere un nuovo disco e assegnare il percorso della cartella del tempdb.
- Utilizzare un disco di archiviazione temporanea esistente per il percorso di cartella hello tempdb.

#### <a name="add-a-new-disk"></a>Aggiungere un nuovo disco:

1. Annotare i percorsi di hello SQL tempdb.mdf e tempdb.ldf prima del failover.
2. Dal portale di Azure hello, aggiungere una nuova macchina virtuale failover di toohello disco con hello uguale o più dimensioni del disco di tempdb hello origine SQL (Disk3).
3. Accedi toohello macchina virtuale di Azure. Dalla console di gestione (diskmgmt.msc) disco hello, inizializzare e formato hello appena aggiunti del disco.
4. Hello Assegna stessa lettera utilizzato dal disco di tempdb SQL hello (f) di unità.
5. Creare una cartella di tempdb in hello volume f: (F:\MSSQL\Data).
6. Avviare il servizio SQL hello dalla console di service hello.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Utilizzare un disco di archiviazione temporanea esistente per il percorso di cartella hello SQL tempdb:

1. Aprire un prompt dei comandi.
2. Eseguire SQL Server in modalità di ripristino dal prompt dei comandi di hello.

        Net start MSSQLSERVER /f / T3608

3. Eseguire hello seguente sqlcmd toochange hello tempdb toohello nuovo percorso.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Arrestare il servizio di Microsoft SQL Server hello.

        Net stop MSSQLSERVER
5. Avviare il servizio di Microsoft SQL Server hello.

        Net start MSSQLSERVER

Fare riferimento toohello di Azure indicazioni per il disco di archiviazione temporanea:

* [Utilizzo di SSD nelle macchine virtuali di Azure toostore TempDB di SQL Server e le estensioni del Pool di Buffer](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Performance best practices for SQL Server in Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance) (Procedure consigliate sulle prestazioni per SQL Server nelle macchine virtuali di Azure)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Failback (da Azure tooan nell'host locale)
Ora è utile comprendere dischi hello che vengono replicati quando si esegue il failover dall'host di VMware o Hyper-V locale tooyour Azure. Per i dischi creati manualmente in Azure non viene eseguita la replica. Se, ad esempio, si esegue il failover di tre dischi e se ne creano due direttamente in Macchine virtuali di Azure, viene eseguito il failback solo dei tre dischi sottoposti a failover. È possibile includere i dischi che sono stati creati manualmente il failback o riprotezione da tooAzure locale. Inoltre non replicare gli host locale tooon disco di archiviazione temporanea hello.

#### <a name="failback-toooriginal-location-recovery"></a>Ripristino nel percorso toooriginal failback

Nell'esempio precedente hello, configurazione del disco di macchina virtuale di Azure hello è come segue:

**N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | ---
DISK0 | C:\ | Disco del sistema operativo
Disk1 | E:\ | Archiviazione temporanea </br / >< / br / > Azure aggiunge il disco e assegna la lettera di unità disponibile prima di hello.
Disk2 | D:\ | Database di sistema SQL e Database1 dell'utente
Disk3 | G:\ | Database2 dell'utente


#### <a name="vmware-tooazure"></a>VMware tooAzure
Al termine il failback toohello nel percorso originale, configurazione del disco hello failback macchina virtuale non dispone di dischi esclusi. I dischi che sono stati esclusi dal tooAzure VMware non saranno disponibili nella macchina virtuale di failback hello.

Dopo il failover pianificato da Azure tooon sedi VMware, dischi nella macchina virtuale VMWare di hello (percorso originale) sono i seguenti:

**N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | ---
DISK0 | C:\ | Disco del sistema operativo
Disk1 | D:\ | Database di sistema SQL e Database1 dell'utente
Disk2 | G:\ | Database2 dell'utente

#### <a name="hyper-v-tooazure"></a>TooAzure Hyper-V
Quando il failback è toohello nel percorso originale, hello failback macchina virtuale su disco configurazione rimane hello uguale a quello della configurazione originale del disco della macchina virtuale per Hyper-V. I dischi che sono stati esclusi dal tooAzure sito Hyper-V sono disponibili nella macchina virtuale di failback hello.

Dopo un failover pianificato da Azure tooon locale Hyper-V, i dischi nella macchina virtuale Hyper-V di hello (percorso originale) sono i seguenti:

**Nome del disco** | **N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | Disco del sistema operativo
DB-Disk1 | Disk1 | D:\ | Database di sistema SQL e Database1 dell'utente
DB-Disk2 (disco escluso) | Disk2 | E:\ | File temporanei
DB-Disk3 (disco escluso) | Disk3 | F:\ | Database tempdb SQL (percorso della cartella, F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | Database2 dell'utente


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Escludere il disco (pagefile.sys) di file di paging hello

Si prenda ad esempio una macchina virtuale con un disco del file di paging che è possibile escludere.
I casi possibili sono due:

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Caso 1: file di paging hello è configurato in unità d: hello
Di seguito è riportata la configurazione disco hello:


**Nome del disco** | **N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disco1 (disco di hello escluse dalla protezione hello) | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Dati utente 1
DB-Disk3 | Disk3 | F:\ | Dati utente 2

Di seguito sono hello impostazioni del file paging nella macchina virtuale di origine hello:

![Impostazioni del file di paging nella macchina virtuale di origine](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Dopo il failover della macchina virtuale hello da VMware tooAzure o tooAzure Hyper-V, dischi su hello macchina virtuale di Azure sono i seguenti:

**Nome del disco** | **N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disk1 | Disk1 | D:\ | Archiviazione temporanea</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Dati utente 1
DB-Disk3 | Disk3 | F:\ | Dati utente 2

Poiché è stata esclusa Disco1 (d), d: è hello prima lettera di unità dall'elenco disponibile hello. Azure assegna volume di archiviazione temporanea toohello d:. Poiché l'unità d: è disponibile in hello macchina virtuale di Azure, hello file di paging di hello macchina virtuale rimane hello stesso.

Di seguito sono hello impostazioni del file paging su hello macchina virtuale di Azure:

![Impostazioni del file di paging nella macchina virtuale di Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Caso 2: file di paging hello è configurato in un'altra unità (ad eccezione di unità d)

Di seguito è la configurazione disco macchina virtuale di origine hello:

**Nome del disco** | **N. disco sistema operativo guest** | **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disco del sistema operativo
DB-Disco1 (disco di hello escluse dalla protezione) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Dati utente 1
DB-Disk3 | Disk3 | F:\ | Dati utente 2

Di seguito sono hello impostazioni del file paging nella macchina virtuale di hello locale:

![File di paging nella macchina virtuale di hello locale](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Dopo il failover della macchina virtuale hello da tooAzure VMware/Hyper-V, dischi su hello macchina virtuale di Azure sono i seguenti:

**Nome del disco**| **N. disco sistema operativo guest**| **Lettera di unità** | **Tipo di dati su disco hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |Disco del sistema operativo
DB-Disk1 | Disk1 | D:\ | Archiviazione temporanea</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Dati utente 1
DB-Disk3 | Disk3 | F:\ | Dati utente 2

Poiché l'unità d: hello prima lettera di unità dall'elenco disponibile hello, Azure assegna volume di archiviazione temporanea toohello d:. Per tutti i dischi hello replicato, rimane lettera di unità hello hello stesso. Poiché hello disco g: non è disponibile, il sistema hello utilizzerà unità c: hello hello file di paging.

Di seguito sono hello impostazioni del file paging su hello macchina virtuale di Azure:

![Impostazioni del file di paging nella macchina virtuale di Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Passaggi successivi
Dopo aver configurato correttamente la distribuzione, vedere [altre informazioni](site-recovery-failover.md) sui diversi tipi di failover.
