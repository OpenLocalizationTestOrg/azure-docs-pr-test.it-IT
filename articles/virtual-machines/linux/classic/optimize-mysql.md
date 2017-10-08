---
title: prestazioni di MySQL in Linux aaaOptimize | Documenti Microsoft
description: Informazioni su come toooptimize MySQL in esecuzione in una macchina virtuale di Azure (VM) in esecuzione Linux.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a>Ottimizzare le prestazioni di MySQL in macchine virtuali Linux di Azure
Esistono molti fattori che influiscono sulle prestazioni di MySQL in Azure, sia nella selezione dell'hardware virtuale sia nella configurazione software. Questo articolo è incentrato sull'ottimizzazione delle prestazioni tramite la configurazione dell'archiviazione, del sistema e del database.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica. In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni sull'ottimizzazione di VM Linux con il modello di gestione risorse hello, vedere [ottimizzare le VM Linux in Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="utilize-raid-on-an-azure-virtual-machine"></a>Usare RAID in una macchina virtuale di Azure
L'archiviazione è fattore chiave hello che influisce sulle prestazioni di database in ambienti di cloud. Singolo disco tooa confrontati, RAID possono accedere più rapidamente tramite la concorrenza. Per altre informazioni, vedere la pagina [Livelli RAID standard](http://en.wikipedia.org/wiki/Standard_RAID_levels).   

Tramite RAID è possibile migliorare la velocità effettiva di I/O del disco e il tempo di risposta di I/O in Azure. I lab di test indicano che può raddoppiare la velocità effettiva dei / o disco e il tempo di risposta dei / o può essere ridotto metà medio quando hello numero di dischi RAID è raddoppiato (da toofour due, quattro tooeight e così via). Per informazioni dettagliate, vedere [Appendice A](#AppendixA) .  

Inoltre i/o toodisk, le prestazioni di MySQL migliorano quando si aumenta il livello RAID hello.  Per informazioni dettagliate, vedere [Appendice B](#AppendixB) .  

È inoltre possibile dimensioni del blocco tooconsider hello. In generale, con blocchi di dimensioni maggiori si ha un sovraccarico ridotto, soprattutto per le scritture di grandi dimensioni. Tuttavia, quando una dimensione blocco hello è troppo grande, potrebbe aggiungere overhead aggiuntivo che consente di sfruttare i vantaggi di RAID. dimensione predefinita corrente Hello è 512 KB, che viene dimostrata toobe ottimale per ambienti di produzione più generali. Per informazioni dettagliate, vedere [Appendice C](#AppendixC) .   

Esistono limiti al numero di dischi che è possibile aggiungere per i diversi tipi di macchine virtuali. Questi limiti sono descritti in dettaglio in [Dimensioni delle macchine virtuali e dei servizi cloud per Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Sarà necessario quattro dati collegati dischi toofollow hello RAID riportato in questo articolo, sebbene sia possibile tooset backup RAID con un minor numero di dischi.  

In questo articolo si presuppone che l'utente abbia già creato una macchina virtuale Linux e che MYSQL sia già stato installato e configurato. Per ulteriori informazioni sui concetti introduttivi, vedere come tooinstall MySQL in Azure.  

### <a name="set-up-raid-on-azure"></a>Configurare RAID in Azure
Hello passaggi seguenti mostrano come toocreate RAID in Azure utilizzando hello portale di Azure. È inoltre possibile configurare RAID usando gli script di Windows PowerShell.
In questo esempio verrà configurato RAID 0 con quattro dischi.  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a>Aggiungere una macchina virtuale tooyour di dati su disco
Nel portale di Azure hello, toohello dashboard scegliere hello toowhich di macchina virtuale si desidera tooadd un disco dati. In questo esempio, macchina virtuale hello è mysqlnode1.  

<!--![Virtual machines][1]-->

Fare clic su **Dischi** e quindi su **Collega nuovo**.

![Aggiunta di dischi nelle macchine virtuali](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

Creare un nuovo disco da 500 GB. Assicurarsi che **preferenze Cache dell'Host** è troppo**Nessuno**.  Al termine, fare clic su **OK**.

![Attach Empty Disk](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


Verrà aggiunto un disco vuoto nella macchina virtuale. Ripetere questo passaggio tre volte in modo da disporre di quattro dischi dati per RAID.  

È possibile visualizzare hello aggiunto unità nella macchina virtuale di hello esaminando i log dei messaggi hello del kernel. Ad esempio, toosee sull'Ubuntu, utilizzare hello comando seguente:  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a>Creare RAID con hello dischi aggiuntivi
Hello passaggi seguenti viene descritto come troppo[configurare software RAID su Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Se si utilizza hello XFS file system, eseguire hello seguendo i passaggi dopo aver creato RAID.
>
>

tooinstall XFS in Debian o Ubuntu Linux menta, hello utilizzare comando seguente:  

    apt-get -y install xfsprogs  

tooinstall XFS su Fedora, CentOS o RHEL, hello utilizzare comando seguente:  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a>Impostare un nuovo percorso di archiviazione
Utilizzare hello tooset comando backup di un nuovo percorso di archiviazione seguenti:  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a>Copia hello dati toohello nuovo percorso di archiviazione originale
Utilizzare hello comando toocopy dati toohello nuovo percorso di archiviazione seguenti:  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a>Modificare le autorizzazioni, pertanto può accedere a MySQL (lettura e scrittura) disco dati hello
Utilizzare queste autorizzazioni toomodify comando hello:  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a>Regolare i/o disco hello algoritmo di pianificazione
Linux implementa quattro tipi di algoritmi di pianificazione di I/O:  

* Algoritmo NOOP (Nessuna operazione)
* Algoritmo di scadenza (Scadenza)
* Algoritmo di accodamento pienamente equo (CFQ, Completely fair queuing)
* Algoritmo del periodo di budget (Anticipatorio)  

È possibile selezionare diversi i/o le utilità di pianificazione in prestazioni toooptimize scenari diversi. In un ambiente ad accesso casuale completamente, non c'è una differenza significativa tra hello CFQ e gli algoritmi di data di scadenza per le prestazioni. È consigliabile impostare hello tooDeadline ambiente database di MySQL per la stabilità. Se è presente un I/O sequenziale considerevole, l'algoritmo CFQ potrebbe ridurre le prestazioni di I/O del disco.   

Per unità SSD e altri dispositivi, è possibile ottenere prestazioni migliori rispetto a utilità di pianificazione predefinita hello NOOP o data di scadenza.   

Toohello precedente kernel 2.5, i/o predefinito hello algoritmo di pianificazione è scadenza. A partire da kernel hello 2.6.18, CFQ è diventato algoritmo di pianificazione di hello predefinito i/o.  È possibile specificare questa impostazione in fase di avvio del kernel o modificare dinamicamente questa impostazione quando è in esecuzione il sistema hello.  

Hello di esempio seguente viene illustrato come toocheck e set hello dell'utilità di pianificazione toohello NOOP predefinito nella famiglia di distribuzione Debian hello.  

### <a name="view-hello-current-io-scheduler"></a>Visualizzazione hello correnti i/o dell'utilità di pianificazione
utilità di pianificazione hello tooview eseguire hello comando seguente:  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

Verrà visualizzato dopo l'output, che indica l'utilità di pianificazione corrente hello:  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a>Modifica dispositivo corrente hello (dev/sda) dell'algoritmo di pianificazione hello i/o
Eseguire hello dispositivo corrente di comandi toochange hello seguenti:  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> Impostare questa opzione solo per /dev/sda è inutile. Deve essere impostato su tutti i dischi di dati in cui risiede il database di hello.  
>
>

È necessario visualizzare hello seguendo l'output, che indica che grub.cfg è stato ricompilato correttamente e che l'utilità di pianificazione predefinita hello è stato aggiornato tooNOOP:  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

Per hello famiglia distribuzione Red Hat, è necessario solo hello comando seguente:

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a>Configurare le impostazioni per le operazioni del file system
Una procedura consigliata è hello toodisable *per volta* funzionalità di registrazione nel file system di hello. Per volta è hello ora ultimo accesso file. Ogni volta che si accede a un file, i record di sistema di hello file hello timestamp nel log di hello. Tuttavia, queste informazioni vengono usate raramente. Se non è necessaria, è possibile disabilitare questa opzione, riducendo così il tempo complessivo di accesso al disco.  

per volta toodisable registrazione, è necessario toomodify hello file system configuration file /etc/ fstab e aggiungere hello **noatime** opzione.  

Ad esempio, modificare hello vim /etc/fstab. file aggiungendo noatime hello, come mostrato nel seguente esempio hello:  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

Quindi, è possibile rimontare hello file system con hello comando seguente:  

    mount -o remount /RAID0

Hello test modificato risultato. Quando si modifica il file di test hello, hello ora di accesso non viene aggiornata. Hello seguenti esempi viene illustrato il codice hello aspetto prima e dopo la modifica.

Prima:        

![Codice prima delle modifiche di accesso][5]

Dopo:

![Codice dopo le modifiche di accesso][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a>Aumentare hello il numero massimo di handle del sistema per la concorrenza elevata
MySQL è un database a concorrenza elevata. numero di handle simultanei di Hello predefinito è 1024 per Linux, che non è sempre sufficiente. Utilizzare hello seguendo i passaggi tooincrease hello massimo simultanee gli handle di concorrenza elevata hello sistema toosupport di MySQL.

### <a name="modify-hello-limitsconf-file"></a>Modificare il file di limits.conf hello
hello tooincrease massimo consentiti handle simultanei, aggiungere hello seguenti quattro righe nel file /etc/security/limits.conf hello. Si noti che numero massimo di hello in grado di supportare sistema hello è 65536.   

    * soft nofile 65536
    * hard nofile 65536
    * soft nproc 65536
    * hard nproc 65536

### <a name="update-hello-system-for-hello-new-limits"></a>Aggiornare il sistema di hello nuovi limiti hello
sistema di hello tooupdate, eseguire hello seguenti comandi:  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a>Assicurarsi che i limiti di hello vengano aggiornati in fase di avvio
Inserire i seguenti comandi di avvio nel file /etc/rc.local hello in modo ha effetto in fase di avvio hello.  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a>Ottimizzare il database MySQL
tooconfigure MySQL in Azure, è possibile utilizzare hello stessa strategia di ottimizzazione delle prestazioni si utilizza un computer locale.  

regole di ottimizzazione i/o principale Hello sono:   

* Aumentare la dimensione della cache di hello.
* Ridurre il tempo di risposta di I/O.  

impostazioni di server MySQL toooptimize, è possibile aggiornare il file my.cnf hello, ovvero file di configurazione hello predefinito per i computer client e server.  

Hello elementi di configurazione seguenti sono i fattori principali hello che influiscono sulle prestazioni di MySQL:  

* **innodb_buffer_pool_size**: pool di buffer hello contiene dati memorizzati nel buffer e indice hello. È in genere impostato too70 percento della memoria fisica.
* **innodb_log_file_size**: si tratta di dimensioni del log rollforward hello. Utilizzare tooensure i log di rollforward che le operazioni di scrittura sono veloce, affidabile e ripristinabile dopo un arresto anomalo. Viene impostato too512 MB, che consentono una notevole quantità di spazio per la registrazione di operazioni di scrittura.
* **max_connections**: in alcuni casi le applicazioni non chiudono correttamente le connessioni. Un valore più grande server avrà a disposizione hello più tempo toorecycle reso inattivo connessioni. Hello il numero massimo di connessioni è 10.000, ma consigliato di hello valore massimo è 5000.
* **Innodb_file_per_table**: questa impostazione Abilita o disabilita il possibilità hello InnoDB toostore tabelle in file distinti. Attivare tooensure opzione hello che diverse operazioni di amministrazione avanzata possono essere applicate in modo efficiente. Dal punto di vista delle prestazioni, può velocizzare la trasmissione di spazio di tabella hello e ottimizzare le prestazioni di Gestione frammenti di hello. Hello consigliata l'impostazione per questa opzione è impostata su ON.</br></br>
Da MySQL 5.6, impostazione predefinita hello è impostata su ON, pertanto è necessaria alcuna azione. Per le versioni precedenti, impostazione predefinita hello è impostata su OFF. impostazione di Hello deve essere modificate prima di caricare dati, perché sono interessate solo tabelle appena create.
* **innodb_flush_log_at_trx_commit**: valore predefinito di hello è 1, con hello ambito impostato too0 ~ 2. valore predefinito di Hello è hello più adatto per il database MySQL. 2 abilita l'impostazione Hello hello la maggior parte dell'integrità dei dati ed è adatto per cluster MySQL Master. impostazione di Hello pari a 0 consente la perdita di dati, che può influenzare l'affidabilità (in alcuni casi con prestazioni migliori) ed è adatto per l'istanza Slave in MySQL Cluster.
* **Innodb_log_buffer_size**: buffer del log hello consente transazioni toorun senza tooflush hello log toodisk prima del commit di transazioni hello. Tuttavia, se è presente il campo di testo o oggetto binario di grandi dimensioni, verranno utilizzate le cache di hello rapidamente e i/o disco frequenti verrà attivato. È meglio aumentare la dimensione del buffer hello se la variabile di stato Innodb_log_waits non è 0.
* **query_cache_size**: opzione migliore hello è toodisable dall'inizio hello. Impostare too0 query_cache_size (si tratta di impostazione hello di MySQL 5.6) e utilizzare altri metodi toospeed delle query.  

Vedere [appendice D](#AppendixD) per un confronto tra le prestazioni prima e dopo l'ottimizzazione di hello.

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a>Attivare i log di query lente hello MySQL per l'analisi dei colli di bottiglia delle prestazioni hello
log query lente di MySQL Hello consentono di identificare query lente hello per MySQL. Dopo aver abilitato i log di query lente hello MySQL, è possibile usare strumenti di MySQL come **mysqldumpslow** tooidentify hello collo di bottiglia.  

Per impostazione log non è abilitato. Accensione di log query lente hello può comportare l'utilizzo di alcune risorse di CPU. È consigliabile abilitarlo temporaneamente per la risoluzione dei colli di bottiglia delle prestazioni. tooturn nel log query lente hello:

1. Modificare file my.cnf hello aggiungendo hello fine toohello le righe seguenti:

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. Riavviare il server di MySQL hello.

        service  mysql  restart

3. Controllare se l'impostazione hello è diventino effettive tramite hello **Mostra** comando.

![Slow-query-log ON][7]   

![Slow-query-log results][8]

In questo esempio, è possibile visualizzare che tale funzionalità di query lente hello è stata attivata. È quindi possibile utilizzare hello **mysqldumpslow** strumento toodetermine i colli di bottiglia delle prestazioni e ottimizzare le prestazioni, ad esempio l'aggiunta di indici.

## <a name="appendices"></a>Appendici
di seguito Hello sono dati di test delle prestazioni di esempio prodotti in un ambiente di laboratorio di destinazione. Forniscono informazioni generali sulla tendenza dei dati delle prestazioni di hello con approcci di ottimizzazione delle prestazioni diversi. Hello risultati potrebbero variare in versioni diverse di ambiente o il prodotto.

### <a name="AppendixA"></a>Appendice A  
**Prestazioni del disco (IOPS) con livelli RAID diversi**

![Prestazioni del disco (IOPS) con livelli RAID diversi][9]

**Comandi di test**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> carico di lavoro Hello di questo test Usa 64 thread, durante il tentativo limite hello tooreach di RAID.
>
>

### <a name="AppendixB"></a>Appendice B  
**Confronto delle prestazioni (velocità effettiva) di MySQL con livelli RAID diversi**   
(XFS file system)

![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][10]  
![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][11]

**Comandi di test**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

**Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi**  
![Confronto delle prestazioni (OLTP) di MySQL con livelli RAID diversi][12]

**Comandi di test**

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <a name="AppendixC"></a>Appendice C   
**Confronto delle prestazioni (IOPS) del disco per dimensioni del blocco diverse**  
(XFS file system)

![][13]

**Comandi di test**  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

utilizzato per la verifica delle dimensioni del file Hello 30 GB e 1 GB, rispettivamente, con RAID 0 (4 dischi) XFS file system.

### <a name="AppendixD"></a>Appendice D  
**Confronto delle prestazioni (velocità effettiva) di MySQL prima e dopo l'ottimizzazione**  
(XFS file system)

![Confronto delle prestazioni (velocità effettiva) di MySQL prima e dopo l'ottimizzazione][14]

**Comandi di test**

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

**impostazione di configurazione Hello per impostazione predefinita e l'ottimizzazione è il seguente:**

| parameters | Default | Ottimizzazione |
| --- | --- | --- |
| **innodb_buffer_pool_size** |Nessuna |7 GB |
| **innodb_log_file_size** |5 MB |512 MB |
| **max_connections** |100 |5000 |
| **innodb_file_per_table** |0 |1 |
| **innodb_flush_log_at_trx_commit** |1 |2 |
| **innodb_log_buffer_size** |8 MB |128 MB |
| **query_cache_size** |16 MB |0 |

Per più dettagliate [i parametri di configurazione di ottimizzazione](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), fare riferimento toohello [istruzioni ufficiale MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).  

  **Ambiente di test**  

| Hardware | Dettagli |
| --- | --- |
| CPU |AMD Opteron(tm) Processore 4171 HE/4 core |
| Memoria |14 GB |
| Disco |10 GB/disco |
| OS |Ubuntu 14.04.1 LTS |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

