---
title: aaaRun un MariaDB (MySQL) del cluster in Azure | Documenti Microsoft
description: Creare un cluster MariaDB + Galera MySQL in macchine virtuali di Azure
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a>Cluster MariaDB (MySQL) - Esercitazione su Azure
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica. Questo articolo descrive il modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse di Azure hello più nuove distribuzioni.

> [!NOTE]
> Cluster MariaDB Enterprise è ora disponibile in hello Azure Marketplace. nuova offerta di Hello distribuirà automaticamente un cluster di MariaDB Galera in Gestione risorse di Azure. È consigliabile utilizzare una nuova offerta di hello da [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).
>
>

In questo articolo illustra come un multimaster toocreate [Galera](http://galeracluster.com/products/) cluster di [MariaDBs](https://mariadb.org/en/about/) (una sostituzione più solida, scalabile e affidabile per MySQL) toowork in un ambiente a disponibilità elevata in Azure macchine virtuali.

## <a name="architecture-overview"></a>Panoramica dell'architettura
Questo articolo viene descritto come hello toocomplete seguenti passaggi:

- Creare un cluster a tre nodi.
- Dischi dati hello separato dal disco del sistema operativo hello.
- Creare dischi dati hello in tooincrease RAID 0/striping impostazione IOPS.
- Utilizzare carico hello toobalance di bilanciamento del carico di Azure per i nodi di hello tre.
- toominimize ricorrenti di lavoro, creare un'immagine di macchina virtuale che contiene MariaDB + Galera e utilizzarlo toocreate hello altre macchine virtuali del cluster.

![Architettura di sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> In questo argomento utilizza hello [CLI di Azure](../../../cli-install-nodejs.md) strumenti, quindi è opportuno assicurarsi che toodownload li e connettere le istruzioni in base toohello di tooyour sottoscrizione di Azure. Se è necessario un comandi toohello di riferimento disponibili in hello CLI di Azure, vedere hello [riferimento sui comandi CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2). È inoltre necessario troppo[creare una chiave SSH per l'autenticazione] e prendere nota del percorso del file con estensione PEM hello.
>
>

## <a name="create-hello-template"></a>Creare il modello di hello
### <a name="infrastructure"></a>Infrastruttura
1. Creare un gruppo di affinità di toohold hello risorse insieme.

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. Creare una rete virtuale.

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. Creare un toohost di account di archiviazione di tutti i dischi. Non inserire più di 40 dischi utilizzati molto frequentemente su hello stesso tooavoid di account di archiviazione raggiunge limite dell'account di archiviazione IOPS hello 20.000. In questo caso, è molto di sotto di tale limite, in modo che conterrà tutti gli elementi in hello stesso account per semplicità.

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. Trovare il nome di hello dell'immagine di macchina virtuale CentOS 7 hello.

        azure vm image list | findstr CentOS
   output di Hello sarà simile al seguente `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.

   Utilizzare il nome nel hello riportata dopo il passaggio.
5. Creare il modello di macchina virtuale hello e sostituire /path/to/key.pem con percorso hello in cui è archiviata la chiave SSH PEM hello generato.

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. Collegare i quattro 500 GB di dati dischi toohello macchina virtuale per l'utilizzo in una configurazione RAID hello.

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. Usare SSH toosign toohello modello macchina virtuale creata in mariadbhatemplate.cloudapp.net:22 e connettersi usando la chiave privata.

### <a name="software"></a>Software
1. Ottenere la radice hello.

        sudo su

2. Installare il supporto RAID:

    a. Installare mdadm.

              yum install mdadm

    b. Creare una configurazione RAID0/stripe hello con un file system EXT4.

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    c. Creare una directory del punto di montaggio hello.

              mkdir /mnt/data
    d. Recuperare hello UUID del dispositivo RAID hello appena creato.

              blkid | grep /dev/md0
    e. Modificare /etc/fstab.

              vi /etc/fstab
    f. Aggiunta automatica di tooenable dispositivo hello montaggio riavvio, sostituendo hello UUID con valore hello ottenuto dal precedente hello **ID blocco** comando.

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    g. Installare una nuova partizione hello.

              mount /mnt/data

3. Installare MariaDB.

    a. Creare file MariaDB.repo hello.

                vi /etc/yum.repos.d/MariaDB.repo

    b. Riempire i file di repository hello con hello seguente contenuto:

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    c. tooavoid conflitti, rimuovere il suffisso esistente e mariadb librerie.

           yum remove postfix mariadb-libs-*
    d. Installare MariaDB con Galera.

           yum install MariaDB-Galera-server MariaDB-client galera

4. Spostare hello MySQL directory toohello RAID blocco il dispositivo di dati.

    a. Copiare directory MySQL corrente hello nella nuova posizione e rimuovere la directory di hello precedente.

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    b. Impostare le autorizzazioni per una nuova directory hello di conseguenza.

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    c. Creare un collegamento simbolico che punta hello precedente toohello nuovo percorso della directory in hello partizione RAID.

           ln -s /mnt/data/mysql /var/lib/mysql

5. Poiché [SELinux interferisce con le operazioni del cluster di hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), è necessario toodisable per hello sessione corrente. Modifica `/etc/selinux/config` toodisable per successivi riavvii.

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. Convalidare le esecuzioni di MySQL.

   a. Avviare MySQL.

           service mysql start
   b. Proteggere l'installazione di MySQL hello, impostare la password radice hello, rimuovere account di accesso di utenti anonimi toodisable radice remota e rimuovere i database di prova hello.

           mysql_secure_installation
   c. Creare un utente nel database di hello per le operazioni del cluster e, facoltativamente, per le applicazioni.

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   d. Arrestare MySQL.

            service mysql stop
7. Creare un segnaposto di configurazione.

   a. Modificare hello MySQL configurazione toocreate un segnaposto per le impostazioni del cluster hello. Non sostituire hello  **`<Variables>`**  o rimuovere il commento ora. L'operazione va eseguita dopo la creazione di una macchina virtuale dal modello.

            vi /etc/my.cnf.d/server.cnf
   b. Modifica hello  **[galera]**  sezione e deselezionarla.

   c. Modifica hello **[mariadb]** sezione.

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. Aprire le porte necessarie sul firewall hello utilizzando FirewallD in CentOS 7.

   * MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
   * GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`
   * GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`
   * RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`
   * Ricarica hello firewall:`firewall-cmd --reload`

9. Ottimizzare il sistema hello per le prestazioni. Per altre informazioni, vedere la [strategia di ottimizzazione delle prestazioni](optimize-mysql.md).

   a. Modificare di nuovo il file di configurazione di hello MySQL.

            vi /etc/my.cnf.d/server.cnf
   b. Modifica hello **[mariadb]** sezione e accodare hello seguente contenuto:

   > [!NOTE]
   > innodb\_buffer\_pool_size dovrebbe essere il 70% della memoria della macchina virtuale. In questo esempio è stata impostata 2,45 GB per Media hello macchina virtuale di Azure con 3,5 GB di RAM.
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. Arrestare MySQL, disabilitare il servizio MySQL esecuzione avvio tooavoid interrompere cluster hello quando si aggiunge un nodo e deprovisioning macchina hello.

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. Acquisire hello VM tramite il portale di hello. (Attualmente [emettere &#1268; negli strumenti di Azure CLI hello](https://github.com/Azure/azure-xplat-cli/issues/1268) vengono descritti i fatti hello che le immagini acquisite dagli strumenti di Azure CLI hello si acquisiscono i dischi dati collegato hello.)

    a. Spegnere la macchina hello tramite il portale di hello.

    b. Fare clic su **acquisire** e specificare il nome immagine hello come **mariadb-galera-immagine**. Fornire una descrizione e selezionare "Il comando waagent è stato eseguito."
      
      ![Acquisire una macchina virtuale hello](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a>Creare il cluster hello
Creare tre macchine virtuali con il modello di hello creato, quindi configurare e avviare hello cluster.

1. Creare hello prima CentOS 7 VM da hello mariadb-galera-immagine immagine è creata, fornendo hello le seguenti informazioni:

 - Nome rete virtuale: mariadbvnet
 - Subnet: mariadb
 - Dimensioni della macchina: medie
 - Nome del servizio cloud: mariadbha (o qualsiasi nome con cui si desidera accedere tramite mariadbha.cloudapp.net toobe)
 - Nome del computer: mariadb1
 - Nome utente: azureuser
 - Accesso SSH: abilitato
 - Il passaggio di file con estensione PEM del certificato SSH hello e sostituendo /path/to/key.pem con percorso hello in cui è archiviata la chiave SSH PEM hello generato.

   > [!NOTE]
   > Hello comandi riportati di seguito sono suddivisi in più righe per maggiore chiarezza, ma è necessario immettere ogni una sola riga.
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. Creare due altre macchine virtuali mediante la connessione del servizio cloud di toohello mariadbha. Nome della macchina virtuale modifica hello e hello porta tooa univoca porta SSH non è in conflitto con altre macchine virtuali in hello nello stesso servizio cloud.

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  Per MariaDB3:

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. È necessario per il passaggio successivo hello tooget hello indirizzo IP interno di ognuna delle macchine virtuali hello tre:

    ![Recupero dell'indirizzo IP virtuale](./media/mariadb-mysql-cluster/IP.png)
4. Nelle macchine virtuali toohello tre toosign SSH e modificare il file di configurazione hello in ognuna di esse.

        sudo vi /etc/my.cnf.d/server.cnf

    Rimuovere il commento  **`wsrep_cluster_name`**  e  **`wsrep_cluster_address`**  rimuovendo hello  **#**  all'inizio di hello della riga hello.
    Inoltre, sostituire  **`<ServerIP>`**  in  **`wsrep_node_address`**  e  **`<NodeName>`**  in  **`wsrep_node_name`**  con hello IP della VM indirizzo e il nome, rispettivamente, e rimuovere il commento le righe di codice.
5. Avviare il cluster hello su MariaDB1 e consentire l'esecuzione all'avvio.

        sudo service mysql bootstrap
        chkconfig mysql on
6. Avviare MySQL in MariaDB2 e MariaDB3 e lasciare che venga eseguito all'avvio.

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a>Cluster di bilanciamento carico di hello
Durante la creazione di macchine virtuali hello in cluster, sono stati aggiunti in un set di disponibilità denominato clusteravset tooensure e che sono stati inseriti in diversi domini di errore e di aggiornamento e che Azure mai non manutenzione in tutti i computer in una sola volta. Questa configurazione soddisfa i requisiti di hello toobe supportati dal contratto di servizio di Azure (SLA) hello.

Utilizzare le richieste di bilanciamento del carico di Azure toobalance tra tre nodi hello.

Eseguire hello seguenti comandi nel computer in uso tramite hello CLI di Azure.

struttura di parametri di comando Hello è:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

Hello CLI imposta hello carico bilanciamento probe intervallo too15 (secondi), che potrebbero essere un po' troppo lunghi. Modificare le impostazioni in portale hello in **endpoint** per le macchine virtuali hello.

![Modificare l'endpoint](./media/mariadb-mysql-cluster/Endpoint.PNG)

Selezionare **hello Reconfigure Load-Balanced impostare**.

![Riconfigurare hello con bilanciamento del carico Set](./media/mariadb-mysql-cluster/Endpoint2.PNG)

Modifica **intervallo Probe** too5 secondi e salvare le modifiche.

![Modificare l'intervallo di probe](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a>Convalida cluster hello
Hello rigido lavoro. cluster Hello dovrebbe ora essere accessibili nel `mariadbha.cloudapp.net:3306`, quale riscontri di bilanciamento del carico hello e indirizzare le richieste tra hello tre macchine virtuali lineare ed efficiente.

Utilizzare i Preferiti tooconnect client MySQL, oppure da uno dei hello tooverify di macchine virtuali che il cluster sia in esecuzione.

     mysql -u cluster -h mariadbha.cloudapp.net -p

Creare quindi un nuovo database e popolarlo con una serie di dati.

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

database Hello creato restituisce hello nella tabella seguente:

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato creato un cluster a disponibilità elevata MariaDB + Galera a tre nodi in macchine virtuali di Azure con CentOS 7. macchine virtuali Hello sono con carico bilanciato con bilanciamento del carico di Azure.

Potrebbe essere necessario toolook in [un altro modo toocluster MySQL in Linux](mysql-cluster.md) e modalità troppo[ottimizzare e testare le prestazioni di MySQL in macchine virtuali Linux di Azure](optimize-mysql.md).

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[creare una chiave SSH per l'autenticazione]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
