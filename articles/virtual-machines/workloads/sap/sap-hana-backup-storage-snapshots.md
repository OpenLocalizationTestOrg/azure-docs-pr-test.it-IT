---
title: backup di Azure HANA aaaSAP basato su snapshot di archiviazione | Documenti Microsoft
description: "Esistono due possibilità principali per il backup di SAP HANA su macchine virtuali di Azure e questo articolo descrive il backup di SAP HANA basato su snapshot di archiviazione"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Backup di SAP HANA basato su snapshot di archiviazione

## <a name="introduction"></a>Introduzione

Questo articolo fa parte di una serie di tre articoli correlati dedicati al backup di SAP HANA. [Guida al backup per SAP HANA in macchine virtuali di Azure](sap-hana-backup-guide.md) fornisce una panoramica e informazioni sulle attività iniziali e [SAP HANA Azure Backup a livello di file](sap-hana-backup-file-level.md) copre hello opzione di backup basato su file.

Quando si utilizza una funzionalità di backup di macchine Virtuali per un sistema a istanza singola all-in-one demo, uno consigliabile eseguire un backup della macchina virtuale anziché gestire backup HANA hello livello del sistema operativo. In alternativa, è tootake blob di Azure degli snapshot toocreate copie dei singoli dischi virtuali, che sono macchina virtuale tooa collegato e mantenere i file di dati HANA hello. Ma un punto critico è coerenza app durante la creazione di uno snapshot di backup o il disco di macchina virtuale mentre hello sistema sia attivo e in esecuzione. Vedere _la coerenza dei dati SAP HANA quando l'esecuzione di snapshot di archiviazione_ nell'articolo correlato hello [Guida di Backup per SAP HANA in macchine virtuali di Azure](sap-hana-backup-guide.md). SAP HANA dispone di una funzionalità che supporta questi tipi di snapshot di archiviazione.

## <a name="sap-hana-snapshots"></a>Snapshot di SAP HANA

SAP HANA dispone di una funzionalità che supporta la creazione di uno snapshot di archiviazione. Tuttavia, a partire dal 2016 dicembre, vi è una restrizione sistemi toosingle contenitore. Le configurazioni con contenitore multi-tenant non supportano questo tipo di snapshot del database (vedere [Create a Storage Snapshot (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) (Creare uno snapshot di archiviazione (SAP HANA Studio))).

Il funzionamento è il seguente:

- Preparare per uno snapshot di archiviazione avviando snapshot SAP HANA hello
- Eseguire snapshot archiviazione hello (blob, ad esempio snapshot di Azure)
- Confermare di snapshot di SAP HANA hello

![La schermata mostra che è possibile creare uno snapshot dei dati di SAP HANA tramite un'istruzione SQL](media/sap-hana-backup-storage-snapshots/image011.png)

La schermata mostra che è possibile creare uno snapshot dei dati di SAP HANA tramite un'istruzione SQL.

![snapshot quindi Hello viene inoltre visualizzato nel catalogo di backup hello in Studio di SAP HANA](media/sap-hana-backup-storage-snapshots/image012.png)

Hello snapshot quindi viene visualizzato anche nel catalogo di backup hello in Studio di SAP HANA.

![Sul disco, snapshot hello viene visualizzato nella directory dei dati SAP HANA hello](media/sap-hana-backup-storage-snapshots/image013.png)

Sul disco, snapshot hello viene visualizzato nella directory dei dati SAP HANA hello.

Uno contiene tooensure che coerenza del file system hello è garantita anche prima dell'esecuzione di snapshot di archiviazione hello mentre si trova in modalità di preparazione snapshot hello SAP HANA. Vedere _la coerenza dei dati SAP HANA quando l'esecuzione di snapshot di archiviazione_ nell'articolo correlato hello [Guida di Backup per SAP HANA in macchine virtuali di Azure](sap-hana-backup-guide.md).

Al termine dello snapshot di archiviazione hello, si tratta di snapshot di SAP HANA hello tooconfirm critici. È presente un corrispondente toorun istruzione SQL: BACKUP SNAPSHOT Chiudi dei dati (vedere [la istruzione BACKUP dati Chiudi SNAPSHOT (Backup e ripristino)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Confermare snapshot HANA hello. Scadenza troppo&quot;Copy-on-Write&quot; SAP HANA potrebbe richiedere ulteriore spazio su disco in snapshot-modalità preparazione, e non è possibile toostart nuovi backup fino a quando non viene confermato snapshot SAP HANA hello.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Backup di VM HANA tramite il servizio Backup di Azure

A partire dal 2016 dicembre, l'agente di backup hello di hello servizio Azure Backup non è disponibile per le macchine virtuali Linux. utilizzo di toomake di backup di Azure a livello di file o directory hello, uno si copiano i file di backup di SAP HANA tooa macchina virtuale di Windows e quindi utilizzare l'agente di backup hello. In caso contrario, un backup completo solo VM Linux è possibile tramite servizio di Backup di Azure hello. Vedere [Panoramica di hello funzionalità in Azure Backup](../../../backup/backup-introduction-to-azure-backup.md) toofind altre.

Hello servizio Backup di Azure offre un'opzione tooback e ripristinare una macchina virtuale. Ulteriori informazioni su questo servizio e il relativo funzionamento sono reperibile nell'articolo hello [pianificare l'infrastruttura di backup di VM in Azure](../../../backup/backup-azure-vms-introduction.md).

Esistono due importanti considerazioni in base toothat articolo:

_&quot;Per le macchine virtuali Linux, solo i backup coerenti con i file sono possibili, poiché non dispone di un tooVSS equivalente piattaforma Linux.&quot;_

_&quot;Le applicazioni devono tooimplement i propri &quot;correzione&quot; meccanismo hello il ripristino dei dati.&quot;_

Pertanto, uno ha toomake assicurarsi SAP HANA in uno stato coerente su disco quando viene avviato il backup di hello. Vedere _snapshot SAP HANA_ descritto in precedenza in documento hello. Ma esiste un problema potenziale quando SAP HANA si trova in questa modalità di preparazione dello snapshot. Per altre informazioni, vedere [Create a Storage Snapshot - SAP HANA Studio](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) (Creare uno snapshot di archiviazione - SAP HANA Studio).

L'articolo afferma quanto segue:

_&quot;È consigliabile tooconfirm o abbandonare uno snapshot di archiviazione appena possibile dopo che è stato creato. Mentre snapshot di archiviazione hello viene preparato o hello creato, i dati pertinenti a snapshot sono bloccati. Mentre i dati relativi a snapshot hello rimangono bloccati, è possibile apportare modifiche nel database di hello. Tali modifiche non genererà hello bloccata toobe relativi snapshot di dati modificati. Al contrario, le modifiche di hello vengono scritte toopositions nell'area dati hello separati da snapshot archiviazione hello. Le modifiche vengono scritte anche toohello log. Tuttavia, hello più hello snapshot di dati rilevanti vengono mantenuti bloccata, hello hello ulteriori può raggiungere il volume di dati.&quot;_

Backup di Azure si occupa di coerenza del file system hello tramite estensioni VM di Azure. Queste estensioni non sono disponibili in modalità autonoma e funzionano solo in combinazione con il servizio Backup di Azure. Tuttavia, è comunque toomanage un requisito della coerenza un'app di SAP HANA snapshot tooguarantee.

Backup di Azure presenta due fasi principali:

- Creare lo snapshot
- Trasferimento dati toovault

Pertanto, una possibile confermare la snapshot SAP HANA hello dopo il completamento della fase di esecuzione di uno snapshot del servizio Azure Backup hello. Potrebbe richiedere diversi minuti toosee in hello portale di Azure.

![In questa figura mostra parte dell'elenco di hello processo di backup di un servizio di Backup di Azure](media/sap-hana-backup-storage-snapshots/image014.png)

Questa figura mostra parte dell'elenco di hello processo di backup di un servizio di Backup di Azure, che è stato utilizzato tooback di test HANA hello macchina virtuale.

![i dettagli dei processi tooshow hello, fare clic su processo di backup hello in hello portale di Azure](media/sap-hana-backup-storage-snapshots/image015.png)

i dettagli dei processi tooshow hello, fare clic su processo di backup nel portale di Azure hello hello. In questo caso, si può osservare hello due fasi. Potrebbe richiedere alcuni minuti finché non viene visualizzato fase snapshot hello come completata. La maggior parte del tempo di hello viene impiegata in fase di trasferimento dei dati hello.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Automazione del backup di VM HANA tramite il servizio Backup di Azure

Uno stato confermare snapshot SAP HANA hello manualmente dopo il completamento della fase hello Azure Backup snapshot, come descritto in precedenza, ma è utile tooconsider automazione perché un amministratore non può monitorare elenco processo di backup hello hello portale di Azure.

Di seguito è riportata una spiegazione di come si potrebbe fare questo mediante i cmdlet di Azure PowerShell.

![Un servizio di Azure Backup è stato creato con hello Nome hana-backup-insieme di credenziali](media/sap-hana-backup-storage-snapshots/image016.png)

Un servizio di Azure Backup è stato creato con il nome di hello &quot;hana-backup-insieme di credenziali.&quot; hello comando PS **AzureRmRecoveryServicesVault di Get-nome archivio di backup hana** recupera hello oggetto corrispondente. Questo oggetto è utilizzato tooset hello backup contesto come mostrato nella figura che segue hello.

![È possibile verificare hello processo di backup attualmente in corso](media/sap-hana-backup-storage-snapshots/image017.png)

Dopo il contesto corretto hello impostazione, uno può controllare hello processo di backup attualmente in corso e quindi cercare i dettagli del processo. elenco delle sottoattività Hello Mostra se fase snapshot hello di hello Azure processo di backup è già stata completata:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Valore di polling hello in un ciclo fino a quando non diventa tooCompleted](media/sap-hana-backup-storage-snapshots/image018.png)

Una volta i dettagli dei processi hello vengono archiviati in una variabile, è sufficiente PS sintassi tooget toohello primo elemento della matrice e recuperare il valore di stato hello. script di automazione toocomplete hello, valore hello sondaggio in un ciclo fino a quando diventa troppo&quot;completato.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>Chiave di licenza di HANA e ripristino di VM mediante il servizio Backup di Azure

Hello servizio Azure Backup è progettata toocreate una nuova macchina virtuale durante il ripristino. Non vi è alcun piano attualmente toodo un &quot;sul posto&quot; ripristino di una macchina virtuale di Azure esistente.

![Nella figura viene illustrata l'opzione di ripristino hello di hello servizio di Azure nel portale di Azure hello](media/sap-hana-backup-storage-snapshots/image019.png)

Questa figura mostra l'opzione di ripristino hello di hello servizio di Azure nel portale di Azure hello. È possibile scegliere tra la creazione di una macchina virtuale durante il ripristino o ripristino dei dischi hello. Dopo aver ripristinato i dischi di hello, è comunque necessario toocreate una nuova macchina virtuale su di esso. Ogni volta che in cui viene creata una nuova macchina virtuale in Azure hello VM ID univoco cambia (vedere [accesso e con ID univoco di Azure VM](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Questa figura mostra hello ID univoco di macchina virtuale di Azure prima e dopo il ripristino di hello mediante il servizio di Backup di Azure](media/sap-hana-backup-storage-snapshots/image020.png)

Questa figura mostra l'ID univoco di macchina virtuale di Azure hello prima e dopo il ripristino di hello mediante il servizio di Backup di Azure. tasto hardware SAP Hello, che viene utilizzato per la gestione delle licenze SAP, Usa questo ID univoco di macchina virtuale. Di conseguenza, una nuova licenza SAP ha toobe installato dopo un ripristino della macchina virtuale.

Una nuova funzionalità Backup di Azure è stata presentata durante la creazione di hello di questa Guida al backup in modalità di anteprima. Consente un ripristino di file livello in base a snapshot VM hello che è stato eseguito per hello VM backup. Questo modo si evita di hello necessità toodeploy una nuova macchina virtuale, pertanto rimane ID macchina virtuale univoci hello hello stesso e nessun nuovo codice di licenza di SAP HANA è obbligatorio. Altre informazioni su questa funzionalità saranno fornite dopo un completo test.

Backup di Azure verrà infine consentire il backup di singoli dischi virtuali Azure, più file e le directory all'interno di hello macchina virtuale. Dei vantaggi principale di Backup di Azure è la gestione di tutti i backup di hello, salvataggio cliente hello dalla presenza di toodo è. Se necessario, un ripristino del Backup di Azure selezionerà il toouse backup corretto hello.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>Backup di VM SAP HANA mediante snapshot manuali dei dischi

Anziché servizio di Backup di Azure hello, uno è stato possibile configurare una singola soluzione di backup mediante la creazione di snapshot di blob di dischi rigidi virtuali di Azure manualmente tramite PowerShell. Vedere [utilizzando gli snapshot di blob con PowerShell](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) per una descrizione dei passaggi di hello.

Offre una maggiore flessibilità ma non consente di risolvere i problemi di hello illustrati in precedenza in questo documento:

- È comunque necessario assicurarsi che SAP HANA sia in uno stato coerente
- disco del sistema operativo Hello non può essere sovrascritto, anche se esiste hello deallocata a causa di un errore indicante che un lease. Funziona solo dopo l'eliminazione di hello VM, che potrebbe causare tooa nuovo univoco ID macchina virtuale e hello necessità tooinstall una nuova licenza SAP.

![È possibile toorestore solo hello dischi di dati di una macchina virtuale di Azure](media/sap-hana-backup-storage-snapshots/image021.png)

È possibile toorestore solo hello dischi di dati di una macchina virtuale di Azure, come evitare il problema hello di ottenere un nuovo ID univoco di macchina virtuale e, pertanto invalidati licenza SAP hello:

- Per il test di hello, due dischi di dati di Azure sono stato collegato tooa VM e RAID software è stato definito questi 
- La coerenza di SAP HANA è stata verificata mediante la funzionalità di snapshot di SAP HANA
- Blocco del file system (vedere _la coerenza dei dati SAP HANA quando l'esecuzione di snapshot di archiviazione_ nell'articolo correlato hello [Guida di Backup per SAP HANA in macchine virtuali di Azure](sap-hana-backup-guide.md))
- Sono stati eseguiti snapshot BLOB da entrambi i dischi dati
- Sblocco del file system
- Conferma dello snapshot SAP HANA
- i dischi dati hello toorestore, hello VM è stato chiuso e scollegato da entrambi i dischi
- Dopo la disconnessione dischi hello, che sono stati sovrascritti con snapshot di blob precedente hello
- Quindi sono stati collegati dischi virtuali hello ripristinato nuovamente toohello VM
- Dopo la durata di snapshot inizia hello VM, tutto il software di hello RAID funzionava correttamente e che è stato reimpostato toohello blob
- HANA è stato reimpostato snapshot HANA toohello

Se è stato possibile tooshut verso il basso SAP HANA prima degli snapshot blob hello, procedura hello sarebbe meno complessa. Uno stato in questo caso, ignorare snapshot HANA hello e, se nient'altro sta succedendo nel sistema hello, anche ignorare hello file sistema blocca. Complessità aggiuntiva viene immagine hello quando è necessario toodo snapshot mentre tutto ciò che è online. Vedere _la coerenza dei dati SAP HANA quando l'esecuzione di snapshot di archiviazione_ nell'articolo correlato hello [Guida di Backup per SAP HANA in macchine virtuali di Azure](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Passaggi successivi
* La [Guida del backup di SAP HANA in Macchine virtuali di Azure](sap-hana-backup-guide.md) offre una panoramica e informazioni introduttive.
* [Backup di SAP HANA in base al livello di file](sap-hana-backup-file-level.md) copre hello opzione di backup basato su file.
* toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md).
