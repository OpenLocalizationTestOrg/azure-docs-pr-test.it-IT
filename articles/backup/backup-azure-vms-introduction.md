---
title: aaaPlanning l'infrastruttura di backup di VM in Azure | Documenti Microsoft
description: Importanti considerazioni relative alla pianificazione di tooback backup di macchine virtuali in Azure
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: backup di vm, backup di macchine virtuali
ms.assetid: 19d2cf82-1f60-43e1-b089-9238042887a9
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: markgal;trinadhk
ms.openlocfilehash: d11982431610000293038ee6aa7df8e7bc2d8b70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-your-vm-backup-infrastructure-in-azure"></a>Pianificare l'infrastruttura di backup delle VM in Azure
In questo articolo fornisce prestazioni e risorsa suggerimenti toohelp si pianifica l'infrastruttura di backup di VM. Definisce inoltre gli aspetti chiave del servizio di Backup hello. questi aspetti possono essere fondamentali nella determinazione dell'architettura, la pianificazione della capacità e la pianificazione. Se è stata [preparato l'ambiente](backup-azure-vms-prepare.md), la pianificazione è successivo hello prima di iniziare [tooback le VM](backup-azure-vms.md). Se sono necessarie ulteriori informazioni sulle macchine virtuali di Azure, vedere hello [macchine virtuali-documentazione](https://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="how-does-azure-back-up-virtual-machines"></a>In che modo Azure esegue il backup delle macchine virtuali?
Quando hello servizio Backup di Azure avvia un processo di backup in fase di hello pianificata, attiva hello estensione backup tootake uno snapshot del punto nel tempo. Hello servizio Azure Backup utilizza hello _VMSnapshot_ estensione in Windows e hello _VMSnapshotLinux_ estensione in Linux. estensione Hello viene installato durante il backup di VM prima hello. estensione di hello tooinstall, hello VM deve essere in esecuzione. Se hello VM non è in esecuzione, il servizio di Backup hello crea uno snapshot di hello archiviazione sottostante (poiché non scritte dall'applicazione si verificano durante hello che macchina virtuale è stato arrestato).

Quando si acquisisce uno snapshot delle macchine virtuali di Windows, il servizio di Backup hello interagisce con hello del servizio Copia Shadow del Volume (VSS) tooget uno snapshot coerenza dei dischi della macchina virtuale hello. Se esegue il backup di macchine virtuali Linux, è possibile scrivere la propria coerenza tooensure script personalizzati quando si acquisisce uno snapshot macchina virtuale. Dettagli su come richiamare gli script sono forniti più avanti in questo articolo.

Una volta hello servizio Azure Backup istantanea hello, dati hello sono toohello trasferite insieme di credenziali. l'efficienza toomaximize servizio hello identifica e i trasferimenti di dati che sono stati modificati dal backup precedente hello solo i blocchi hello.

![Architettura del backup delle macchine virtuali di Azure](./media/backup-azure-vms-introduction/vmbackup-architecture.png)

Una volta completato il trasferimento dei dati di hello, snapshot hello viene rimosso e viene creato un punto di ripristino.

> [!NOTE]
> 1. Durante il processo di backup hello Azure Backup non include macchina virtuale toohello di hello disco temporaneo associato. Per ulteriori informazioni, vedere il blog di hello in [archiviazione temporanea](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/).
> 2. Poiché Azure Backup ha uno snapshot a livello di archiviazione e trasferimento di snapshot toovault, non modificare chiavi dell'account di archiviazione hello fino al completamento del processo di backup hello.
> 3. Per le macchine virtuali premium, copiamo account toostorage di hello snapshot. Si tratta di verificare che il servizio di Backup di Azure Ottiene IOPS sufficienti per il trasferimento di dati toovault toomake. Questa copia aggiuntiva dell'archiviazione viene addebitata in base alle hello VM dimensione allocata. 
>

### <a name="data-consistency"></a>Coerenza dei dati
Backup e ripristino dei dati aziendali critici è complicata dal fatto di hello che dati aziendali critici devono eseguire il backup durante le applicazioni di hello che producono hello dati sono in esecuzione. tooaddress, Backup di Azure supporta i backup coerenti con l'applicazione per Windows e le macchine virtuali Linux
#### <a name="windows-vm"></a>Macchina virtuale Windows
Backup di Azure esegue backup VSS completi nelle macchine virtuali di Windows (altre informazioni su [backup VSS completi](http://blogs.technet.com/b/filecab/archive/2008/05/21/what-is-the-difference-between-vss-full-backup-and-vss-copy-backup-in-windows-server-2008.aspx)). tooenable VSS i backup di copia, seguire i set di toobe esigenze chiave del Registro di sistema di hello VM hello.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT]
"USEVSSCOPYBACKUP"="TRUE"
```

#### <a name="linux-vms"></a>Macchine virtuali di Linux
Backup di Azure fornisce un framework di scripting. la coerenza delle applicazioni tooensure durante il backup di macchine virtuali Linux, creare pre- script personalizzati di e post script che controllano il flusso di lavoro backup hello e ambiente. Backup di Azure richiama pre-script di hello prima di creare snapshot VM hello e richiama post-script hello termine del processo di snapshot VM hello. Per altri dettagli, vedere l'articolo relativo a [backup di macchine con coerenza delle applicazioni usando script di pre-backup e di post-backup](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).
> [!NOTE]
> Backup di Azure solo richiama hello scritto cliente pre- e post script. Se gli post- script di e pre-script di hello eseguito correttamente, Backup di Azure contrassegna il punto di ripristino hello come applicazione coerente. Tuttavia, hello cliente è responsabile della coerenza con l'applicazione hello quando si utilizzano script personalizzati.
>


Questa tabella vengono illustrati tipi di hello di coerenza e hello condizioni che si verificano in durante il backup di macchina virtuale di Azure e procedure di ripristino.

| Coerenza | Basato su VSS | Spiegazione e dettagli |
| --- | --- | --- |
| Coerenza con l'applicazione |Sì per Windows|La coerenza dell'applicazione è ideale per i carichi di lavoro perché garantisce:<ol><li> Hello VM *avvio*. <li>L' *assenza di qualsiasi danneggiamento*. <li>L'*assenza di perdite di dati*.<li> dati Hello sono coerente toohello applicazione che utilizza dati hello, che include un'applicazione hello in fase di hello del backup, utilizzando uno script pre o post-backup o di VSS.</ol> <li>*Macchine virtuali Windows*-carichi di lavoro di Microsoft più con il writer VSS che eseguono azioni specifiche di un carico di lavoro correlati toodata coerenza. Ad esempio, Microsoft SQL Server ha un VSS writer che assicura che i file di log delle transazioni toohello scritture hello e database hello vengono eseguite correttamente. Per i backup di macchina virtuale Windows Azure, un punto di ripristino coerenti con l'applicazione, toocreate estensione backup hello deve richiamare hello VSS flusso di lavoro e completarla prima di creare snapshot VM hello. Per hello Azure VM snapshot toobe accurato, il writer VSS hello di tutte le applicazioni Azure VM deve essere completata anche. (Ulteriori hello [nozioni di base di VSS](http://blogs.technet.com/b/josebda/archive/2007/10/10/the-basics-of-the-volume-shadow-copy-service-vss.aspx) e approfondimenti dettagli hello di [funzionamento](https://technet.microsoft.com/library/cc785914%28v=ws.10%29.aspx)). </li> <li> *Le macchine virtuali Linux*-i clienti possono eseguire [la coerenza delle applicazioni personalizzata tooensure pre- script di e post-](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent). </li> |
| Coerenza del file system |Sì, per i computer basati su Windows |Esistono due scenari in cui può essere il punto di ripristino hello *coerente del file system*:<ul><li>Backup di macchine virtuali Linux in Azure, senza script di pre-/post-backup o se lo script di pre-/post-backup non è stato eseguito correttamente. <li>Errore VSS durante il backup di macchine virtuali di Windows in Azure.</li></ul> In entrambi i casi, hello migliore che può essere eseguita è tooensure che: <ol><li> Hello VM *avvio*. <li>L' *assenza di qualsiasi danneggiamento*.<li>L'*assenza di perdite di dati*.</ol> Le applicazioni devono meccanismo tooimplement i propri "correzione" dati hello ripristinato. |
| Coerenza dei dati |No |Questa situazione è una macchina virtuale tooa equivalente segnalano un "blocco" (tramite reset software o hardware). La coerenza di arresto anomalo del sistema accade solitamente quando hello macchina virtuale di Azure viene arrestato al momento di hello del backup. Un punto di ripristino coerenti con l'arresto anomalo del sistema non fornisce alcuna garanzia di coerenza hello dei dati di hello intorno a sul supporto di archiviazione - hello dalla prospettiva di hello del sistema operativo hello o un'applicazione hello. Solo i dati hello esistono già in fase di hello del backup su disco hello acquisiti e il backup. <br/> <br/> Avvio del sistema operativo, seguito dal controllo del disco di hello mentre non esistono garanzie di alcun tipo, in genere, procedure, come chkdsk, toofix eventuali errori di danneggiamento. Tutti i dati in memoria e scrive che non sono stati trasferiti toohello disco vengono perse. un'applicazione Hello segue in genere con un proprio meccanismo di verifica nel caso in cui il rollback di dati deve toobe eseguita. <br><br>Ad esempio, se il log delle transazioni hello dispone di voci che non sono presenti nel database di hello, quindi hello database software esegue un'operazione di rollback fino a quando non sono coerenti dati hello. Quando i dati viene distribuiti tra più dischi virtuali (ad esempio i volumi con spanning), un punto di ripristino coerenti con l'arresto anomalo del sistema non fornisce alcuna garanzia di correttezza hello dei dati di hello. |

## <a name="performance-and-resource-utilization"></a>Prestazioni e utilizzo delle risorse
Analogamente al software distribuito in locale, è necessario pianificare le esigenze di utilizzo di capacità e risorse durante il backup delle macchine virtuali in Azure. Hello [limiti di archiviazione Azure](../azure-subscription-service-limits.md#storage-limits) definire l'impatto di carichi di lavoro toorunning toostructure VM distribuzioni tooget le massime prestazioni con minimo.

Prestare attenzione toohello limiti di spazio di archiviazione di Azure seguente durante la pianificazione delle prestazioni di backup:

* Numero massimo in uscita per account di archiviazione
* Frequenza delle richieste totale per account di archiviazione

### <a name="storage-account-limits"></a>Limiti dell'account di archiviazione
Dati di backup copiati da un account di archiviazione, aggiunge toohello operazioni di input/output al secondo (IOPS) e in uscita (o una velocità effettiva) metriche hello dell'account di archiviazione. AT hello stesso macchine virtuali, ora anche utilizzano IOPS e la velocità effettiva. obiettivo di Hello è tooensure Backup e il traffico delle macchine virtuali non superino i limiti dell'account di archiviazione.

### <a name="number-of-disks"></a>Numero di dischi
processo di backup Hello tenta toocomplete un processo di backup più rapidamente possibile. utilizzando quindi la quantità più elevata possibile di risorse. Tuttavia, tutte le operazioni dei / o sono limitate da hello *velocità effettiva da raggiungere per Blob singolo*, che ha un limite di 60 MB al secondo. Processo di backup hello in toomaximize un tentativo di velocità, Cerca tooback backup ognuno dei dischi della macchina virtuale di hello *in parallelo*. Se una macchina virtuale è disponibili quattro dischi, hello tooback tentativi servizio backup di tutti e quattro i dischi in parallelo. Hello **numero di dischi** viene eseguito il backup, è importante fattore, hello nella determinazione di traffico di backup di account di archiviazione.

### <a name="backup-schedule"></a>Pianificazione dei backup
Un altro fattore che influisce sulle prestazioni è hello **pianificazione del backup**. Se si configurare criteri hello in modo tutte le macchine virtuali vengono eseguito il backup in hello stesso tempo, è stato pianificato un bloccati il traffico. processo di backup Hello tenta tooback backup di tutti i dischi in parallelo. tooreduce hello backup il traffico proveniente da un account di archiviazione, eseguire il backup diverse macchine virtuali in un momento diverso del giorno hello, senza sovrapposizioni.

## <a name="capacity-planning"></a>Pianificazione della capacità
Combinazione di fattori di hello precedente, è necessario tooplan per esigenze di utilizzo di account di archiviazione hello. Scaricare hello [VM backup la pianificazione della capacità del foglio di calcolo di Excel](https://gallery.technet.microsoft.com/Azure-Backup-Storage-a46d7e33) impatto hello toosee del disco e le opzioni di pianificazione di backup.

### <a name="backup-throughput"></a>Velocità effettiva del backup
Per ogni disco viene eseguito il backup, Backup di Azure legge blocchi hello sul disco hello e archivi hello solo i dati modificati (backup incrementali). Hello nella tabella seguente mostra valori medi della velocità effettiva del servizio di Backup in hello. Utilizza hello dati seguenti, è possibile stimare quanti hello necessari tooback backup di un disco di una determinata dimensione.

| Operazione di backup | Velocità effettiva ottimale |
| --- | --- |
| Backup iniziale |160 Mbps |
| Backup incrementale (ripristino di emergenza) |640 Mbps  <br><br> Velocità effettiva Elimina in modo significativo se hello modificati i dati (che devono toobe backup) è diverse tra dischi hello.|

## <a name="total-vm-backup-time"></a>Tempo totale di backup della macchina virtuale
Mentre la maggior parte del tempo di backup hello viene impiegato per la lettura e la copia dei dati, le altre operazioni contribuiscono toohello tempo totale necessario tooback una macchina virtuale:

* Necessario troppo tempo[installare o aggiornare l'estensione del backup hello](backup-azure-vms.md).
* Ora dello snapshot, ovvero hello scattato tootrigger uno snapshot. Gli snapshot sono attivate toohello chiusura pianificata ora del backup.
* Tempo di attesa di coda. Poiché il servizio di Backup hello elabora i backup di più clienti, la copia di dati di backup da backup di snapshot toohello o servizi di ripristino dell'insieme di credenziali non venga avviata immediatamente. Negli orari di punta, attesa hello consente di estendere le ore tooeight scadenza toohello numero di backup in corso di elaborazione. Tuttavia, ora backup VM totale hello è inferiore a 24 ore per i criteri di backup giornalieri.
* Tempo di trasferimento di dati, tempo necessario per il backup le modifiche incrementali toocompute hello dal backup precedente del servizio e trasferire tali archiviazione toovault le modifiche.

### <a name="why-am-i-observing-longer12-hours-backup-time"></a>Perché si registrano tempi di backup superiori alle 12 ore?
Backup è costituito da due fasi: esecuzione di snapshot e il trasferimento di hello snapshot toohello insieme di credenziali. Consente di ottimizzare Hello servizio di Backup per l'archiviazione. Durante il trasferimento di insieme di credenziali tooa dati snapshot hello, servizio hello trasferisce solo le modifiche incrementali da snapshot precedente hello.  modifiche incrementali hello toodetermine, servizio hello calcola checksum hello di blocchi di hello. Se viene modificato un blocco, blocco hello viene identificato come un blocco di toobe inviati toohello insieme di credenziali. Esercitazioni di servizio hello ulteriormente in ognuna delle hello identificati blocchi, cercando le opportunità toominimize hello dati tootransfer. Dopo aver valutato i blocchi modificati tutti, il servizio di hello assegna modifiche hello e li invia insieme di credenziali toohello. In alcune applicazioni legacy, le scritture frammentate e di piccole dimensioni non sono ottimali per l'archiviazione. Se snapshot hello contiene molte operazioni di scrittura di piccole dimensioni, frammentati, servizio hello impiega più tempo di elaborazione dati hello scritti dalle applicazioni hello. Hello consigliato di blocco di scrittura di applicazioni da Azure, per le applicazioni in esecuzione all'interno di hello macchina virtuale, è un minimo di 8 KB. Se l'applicazione usa un blocco più piccolo degli 8 KB, le prestazioni del backup ne risentono. Per informazioni sull'ottimizzazione delle prestazioni di backup tooimprove applicazione, vedere [ottimizzazione di applicazioni per ottenere prestazioni ottimali con l'archiviazione di Azure](../storage/common/storage-premium-storage-performance.md). Se l'articolo di hello sulle prestazioni del backup viene utilizzato negli esempi di archiviazione Premium, materiale sussidiario hello è applicabile per i dischi di archiviazione Standard.

## <a name="total-restore-time"></a>Tempo totale di ripristino
Un'operazione di ripristino è costituita da due attività principali sub: copia i dati nuovamente dall'account di archiviazione di hello insieme di credenziali toohello scelto cliente e creazione della macchina virtuale hello. La copia dei dati dallo stesso insieme di credenziali hello dipende in cui i backup hello vengono archiviati internamente in Azure e in cui è memorizzato l'account di archiviazione hello cliente. Dipende dal tempo impiegato toocopy dati:
* -Tempo di attesa in coda perché i processi del servizio hello processi di ripristino da più clienti in hello stesso tempo, le richieste di ripristino sono inseriti in una coda.
* Tempo - copia dei dati dei dati viene copiati dall'account di archiviazione cliente toohello hello insieme di credenziali. Ripristinare tempo dipende dal valore di IOPS e velocità effettiva del servizio di Backup di Azure Ottiene account di archiviazione cliente hello selezionato. tooreduce hello la copia di tempo durante il processo di ripristino di hello, selezionare un account di archiviazione non è stato caricato con altri di lettura e scrittura di applicazioni.

## <a name="best-practices"></a>Procedure consigliate
È consigliabile seguire queste procedure durante la configurazione del backup per le macchine virtuali:

* Non pianificare le macchine virtuali classiche più di 10 da hello stesso cloud tooback servizio in hello contemporaneamente. Se si desidera tooback di più macchine virtuali nello stesso servizio cloud, sfalsare gli orari di inizio backup di hello di un'ora.
* Non pianificare più di 40 tooback macchine virtuali di hello contemporaneamente.
* Pianificare i backup di macchine Virtuali durante le ore non di punta. Questo servizio di Backup di hello modo utilizza IOPS per il trasferimento dei dati dall'insieme di credenziali toohello hello cliente storage account.
* Assicurarsi che un criterio faccia riferimento a VM in più account di archiviazione. Si consiglia di non più di 20 totali dischi da un singolo account di archiviazione protetta da hello pianificazione del backup stesso. Se dispone di maggiore di 20 dischi in un account di archiviazione, distribuire tali macchine virtuali tra più criteri tooget hello IOPS richiesto durante la fase di trasferimento hello del processo di backup hello.
* Non ripristinare una macchina virtuale in esecuzione in account di archiviazione toosame archiviazione Premium. Se il processo di operazione di ripristino hello coincide con l'operazione di backup hello, riduce hello IOPS disponibile per il backup.
* Per il backup di VM Premium, verificare che l'account di archiviazione che ospita i dischi premium abbia almeno il 50% di spazio disponibile per la gestione temporanea degli snapshot perché il backup sia completato correttamente. 
* Verificare che la versione di python nelle macchine virtuali Linux abilitate per il backup sia la 2.7

## <a name="data-encryption"></a>Crittografia dei dati
Backup di Azure crittografa i dati come parte del processo di backup hello. Tuttavia, è possibile crittografare i dati all'interno di hello VM e backup hello i dati protetti senza problemi (ulteriori informazioni su [backup dei dati crittografati](backup-azure-vms-encryption.md)).

## <a name="calculating-hello-cost-of-protected-instances"></a>Il calcolo del costo di hello di istanze protette
Macchine virtuali di Azure che vengono sottoposti a backup tramite Backup di Azure sono soggette a troppo[dei prezzi di Azure Backup](https://azure.microsoft.com/pricing/details/backup/). calcolo di istanze protette Hello è basato su hello *effettivo* dimensioni di macchina virtuale di hello è hello somma di tutti i dati di hello nella macchina virtuale hello - escludendo hello "risorsa disco."

Prezzi per il backup delle macchine virtuali è *non* in base alle dimensioni di hello massima supportata per ogni macchina virtuale di dati su disco toohello associata. Piano tariffario è in base hello dati effettivi archiviati nel disco dati hello. Analogamente, i costi di archiviazione di backup hello sono in base hello quantità di dati archiviati in Azure Backup, ovvero la somma hello di dati effettivo hello in ogni punto di ripristino.

Si prenda ad esempio una macchina virtuale di dimensioni A2-Standard dotata di due dischi dati aggiuntivi con capacità massima di 1 TB ciascuno. Hello nella tabella seguente fornisce i dati di effettivo hello archiviati in ognuno di questi dischi:

| Tipo di disco | Dimensioni massime | Dati effettivi presenti |
| --- | --- | --- |
| Disco del sistema operativo |1023 GB |17 GB |
| Disco locale/Disco risorse |135 GB |5 GB (non incluso per il backup) |
| Disco dati 1 |1023 GB |30 GB |
| Disco dati 2 |1023 GB |0 GB |

Hello *effettivo* dimensioni di macchina virtuale hello in questo caso sono 17 GB + 30 GB + 0 GB = 47 GB. Questa dimensione di istanza protetta (47 GB) diventa base hello per fattura mensile hello. Come hello quantità di dati nella macchina virtuale hello cresce, dimensioni di istanza protetta hello utilizzata per le informazioni di fatturazione, di conseguenza.

La fatturazione non viene avviato fino al completamento di backup riuscito prima hello. A questo punto, inizia la fatturazione hello per le istanze protetti sia all'archiviazione. La fatturazione continua finché è *qualsiasi backup dei dati archiviati in un insieme di credenziali* per la macchina virtuale hello. Se si arresta la protezione nella macchina virtuale hello, ma esistono dati di backup di macchina virtuale in un insieme di credenziali, la fatturazione continua.

La fatturazione per una macchina virtuale specificata si arresta solo se la protezione di hello viene interrotta *e* tutti i dati di backup viene eliminato. Quando si arresta protezione dati e non sono disponibili processi di backup attivi, dimensioni hello dell'ultimo backup VM riuscito hello diventa dimensioni di istanza protetta hello utilizzate per la fattura mensile hello.

## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Passaggi successivi
* [Eseguire il backup di macchine virtuali](backup-azure-vms.md)
* [Gestire i backup delle macchine virtuali](backup-azure-manage-vms.md)
* [Ripristino di macchine virtuali](backup-azure-restore-vms.md)
* [Risolvere i problemi relativi al backup delle macchine virtuali di Azure](backup-azure-vms-troubleshoot.md)
