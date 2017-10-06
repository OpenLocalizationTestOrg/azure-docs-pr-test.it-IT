---
title: aaaClusterize MySQL con set con carico bilanciato | Documenti Microsoft
description: "Impostare una bilanciamento del carico, la disponibilità elevata cluster Linux MySQL creato con il modello di distribuzione classica hello in Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a>Utilizzare set con carico bilanciato tooclusterize MySQL in Linux
> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica. In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Oggetto [modello Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) è disponibile se è necessario toodeploy un cluster di MySQL.

In questo articolo viene esaminata e illustra hello diversi approcci disponibili toodeploy servizi a disponibilità elevata basate su Linux in Microsoft Azure, l'esplorazione di MySQL Server a elevata disponibilità come nozioni di base. Su [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)è disponibile un video che illustra questo approccio.

Sarà descritta una soluzione con disponibilità elevata MySQL a master singolo, con due nodi e nessuna condivisione, basata su DRBD, Corosync e Pacemaker. MySQL viene eseguito solo su un nodo alla volta. Lettura e scrittura da risorse DRBD hello è anche un nodo tooonly limitato alla volta.

Non è necessario per una soluzione VIP come LVS, poiché verrà utilizzato il set di bilanciamento del carico nella possibilità di recupero di hello VIP, il rilevamento di funzionalità e l'endpoint round-robin tooprovide e la rimozione di Microsoft Azure. Hello VIP è un indirizzo IPv4 instradabile assegnato da Microsoft Azure al momento della creazione del servizio cloud hello.

È possibile usare altre architetture per MySQL inclusi NBD Cluster, Percona, Galera e varie soluzioni middleware, di cui almeno una disponibile come VM su [VM Depot](http://vmdepot.msopentech.com). Purché queste soluzioni possono essere replicati in unicast e multicast o broadcast e non fare affidamento sull'archiviazione condivisa o più interfacce di rete, gli scenari di hello devono essere facile toodeploy in Microsoft Azure.

Queste architetture di clustering possono essere estesi tooother prodotti come PostgreSQL e OpenLDAP in modo simile. Questa procedura di bilanciamento del carico senza condivisione è stata ad esempio testata con OpenLDAP multimaster ed è possibile vederne i risultati sul blog di Channel 9.

## <a name="get-ready"></a>Preparazione
È necessario hello segue le risorse e funzionalità:

  - Account di un Microsoft Azure con una sottoscrizione valida, in grado di toocreate almeno due macchine virtuali (XS è stato utilizzato in questo esempio)
  - Una rete e una subnet
  - Un gruppo di affinità
  - Un set di disponibilità
  - Hello possibilità toocreate dischi rigidi virtuali nella stessa area del servizio cloud hello hello e allegarli le macchine virtuali Linux toohello

### <a name="tested-environment"></a>Ambiente testato
* Ubuntu 13.10
  * DRBD
  * Server MySQL
  * Corosync e Pacemaker

### <a name="affinity-group"></a>Gruppo di affinità
Creare un gruppo di affinità per la soluzione hello effettuando l'accesso al portale di Azure classico, toohello selezionando **impostazioni**e la creazione di un gruppo di affinità. Le risorse allocate create in un secondo momento verranno assegnate il gruppo di affinità toothis.

### <a name="networks"></a>Reti
Viene creata una nuova rete e una subnet viene creata all'interno di rete hello. Questo esempio usa una rete 10.10.10.0/24 contenente una sola subnet /24.

### <a name="virtual-machines"></a>Macchine virtuali
Hello prima Ubuntu 13.10 VM viene creato utilizzando un'immagine della raccolta Ubuntu Endorsed e viene chiamato `hadb01`. Nel processo di hello, denominato hadb, viene creato un nuovo servizio cloud. Questo nome viene condiviso, hello natura con bilanciamento del carico che servizio hello avrà quando vengono aggiunte più risorse. creazione di Hello `hadb01` è completata e se tramite il portale di hello. Viene creato automaticamente un endpoint per SSH e hello nuova rete sia selezionata. È ora possibile creare un set di disponibilità per le macchine virtuali hello.

Dopo aver hello prima macchina virtuale viene creato (tecnicamente, quando viene creato il servizio di cloud hello), creare hello seconda macchina virtuale, `hadb02`. Per hello secondo VM, utilizzare Ubuntu 13.10 VM da hello raccolta tramite il portale di hello, ma utilizzare un servizio cloud esistente, `hadb.cloudapp.net`, anziché crearne uno nuovo. Hello rete e set di disponibilità deve essere selezionato automaticamente. Verrà anche creato un endpoint SSH.

Dopo aver create entrambe le macchine virtuali, prendere nota della porta SSH hello per `hadb01` (TCP 22) e `hadb02` (assegnato automaticamente da Azure).

### <a name="attached-storage"></a>Archivio collegato
Collegare un nuovo tooboth disco macchine virtuali e creare i dischi di 5 GB nel processo di hello. dischi Hello sono ospitati nel contenitore di disco rigido virtuale hello in uso per i dischi del sistema operativo principale. Dopo che i dischi vengono creati e collegati, non si verifica alcun toorestart necessità Linux poiché kernel hello verrà visualizzato il nuovo dispositivo di hello. Questo dispositivo è in genere `/dev/sdc`. Controllare `dmesg` per l'output di hello.

In ogni macchina virtuale, creare una partizione utilizzando `cfdisk` (partizione principale, di Linux) e scrittura hello nuova tabella di partizione. Non creare un file system in questa partizione.

## <a name="set-up-hello-cluster"></a>Configurazione di cluster hello
Scegliere entrambe le macchine virtuali Ubuntu APT tooinstall Corosync Pacemaker e DRBD. toodo con `apt-get`, eseguire hello il codice seguente:

    sudo apt-get install corosync pacemaker drbd8-utils.

Non installare MySQL a questo punto. Debian e Ubuntu gli script di installazione verranno inizializzato una directory di dati di MySQL in `/var/lib/mysql`, ma poiché la directory hello verrà essere sostituita da un file system DRBD, è necessario tooinstall MySQL in un secondo momento.

Verificare (tramite `/sbin/ifconfig`) che entrambe le macchine virtuali utilizzano indirizzi nella subnet 10.10.10.0/24 hello e che è possibile eseguire il ping tra loro in base al nome. È inoltre possibile utilizzare `ssh-keygen` e `ssh-copy-id` toomake che entrambe le macchine virtuali possono comunicare tramite SSH senza richiedere una password.

### <a name="set-up-drbd"></a>Configurare DRBD
Creare una risorsa DRBD che utilizza hello sottostante `/dev/sdc1` tooproduce partizionare un `/dev/drbd1` risorse che possono essere formattate usando ext3 e utilizzate nei nodi primari e secondari.

1. Aprire `/etc/drbd.d/r0.res` e hello copia seguente definizione di risorsa in entrambe le macchine virtuali:

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. Inizializzare la risorsa hello usando `drbdadm` in entrambe le macchine virtuali:

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. Nella macchina virtuale primaria hello (`hadb01`), forzare la proprietà (primaria) della risorsa DRBD hello:

        sudo drbdadm primary --force r0

Se si esamina il contenuto di hello di proc/drbd (`sudo cat /proc/drbd`) su entrambe le macchine virtuali, dovrebbe essere `Primary/Secondary` su `hadb01` e `Secondary/Primary` su `hadb02`, coerente con la soluzione hello a questo punto. disco di 5 GB Hello verrà sincronizzato tramite rete 10.10.10.0/24 hello toocustomers alcun addebito.

Dopo la sincronizzazione disco hello, è possibile creare il sistema di file hello in `hadb01`. A scopo di test, abbiamo utilizzato ext2, ma hello seguente codice verrà creato un file system ext3:

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a>Montare hello DRBD risorsa
Si è ora pronto toomount risorse DRBD hello `hadb01`. Debian e i derivati usano `/var/lib/mysql` come directory dei dati di MySQL. Poiché non è stato installato MySQL, creare directory hello e montare hello DRBD risorsa. tooperform questa opzione, eseguire hello seguendo codice `hadb01`:

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a>Configurare MySQL
A questo punto è pronti tooinstall MySQL in `hadb01`:

    sudo apt-get install mysql-server

Per `hadb02`sono disponibili due opzioni. È possibile installare mysql server, che crea /var/lib/mysql, compilarlo con una nuova directory dei dati e quindi rimuovere il contenuto di hello. tooperform questa opzione, eseguire hello seguendo codice `hadb02`:

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

seconda opzione Hello è toofailover troppo`hadb02` e quindi installare mysql-server non esiste. Gli script di installazione noteranno installazione esistente di hello e non è disponibile.

Esecuzione hello il seguente codice in `hadb01`:

    sudo drbdadm secondary –force r0

Esecuzione hello il seguente codice in `hadb02`:

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

Se a questo punto non si intende toofailover DRBD, hello prima opzione è più semplice, anche se probabilmente sia meno elegante. Al termine della configurazione, è possibile iniziare a lavorare sul database MySQL. Esecuzione hello il seguente codice in `hadb02` (o qualsiasi uno dei server hello è attivo, in base tooDRBD):

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> L'ultima istruzione disabilita in modo efficace l'autenticazione per l'utente root hello in questa tabella. È consigliabile sostituirla con istruzioni GRANT di livello di produzione ed è inclusa solo per scopi esplicativi.

Se si desidera toomake query da macchine virtuali di hello esterno (ovvero scopo hello di questa Guida), è necessario anche tooenable di rete per MySQL. In entrambe le macchine virtuali, aprire `/etc/mysql/my.cnf` e andare troppo`bind-address`. Modificare indirizzo hello da 127.0.0.1 too0.0.0.0. Dopo aver salvato il file hello, emettere un `sudo service mysql restart` sul server principale corrente.

### <a name="create-hello-mysql-load-balanced-set"></a>Creare set di bilanciamento del carico di hello MySQL
Tornare indietro toohello portal, andare troppo`hadb01`e scegliere **endpoint**. toocreate un endpoint, scegliere di MySQL (porta TCP 3306) dall'elenco a discesa hello e selezionare **set con bilanciamento del carico di nuova creazione**. Endpoint con bilanciamento del carico di nome hello `lb-mysql`. Impostare **ora** too5 secondi minimi.

Dopo aver creato endpoint hello, andare troppo`hadb02`, scegliere **endpoint**e creare un endpoint. Scegliere `lb-mysql`, quindi selezionare MySQL dall'elenco a discesa hello. È inoltre possibile utilizzare hello CLI di Azure per questo passaggio.

È ora disponibile tutto il che necessario per l'operazione manuale del cluster di hello.

### <a name="test-hello-load-balanced-set"></a>Testare il set di bilanciamento del carico hello
I test possono essere eseguiti da un computer esterno usando qualsiasi client MySQL oppure con alcune applicazioni come phpMyAdmin in esecuzione come sito Web di Azure. In questo caso è stato usato lo strumento da riga di comando di MySQL su un'altra casella di Linux:

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a>Failover manuale
È possibile simulare il failover chiudendo MySQL, passando al nodo primario di DRBD e riavviando MySQL.

tooperform questa attività esegue hello seguendo hadb01 codice:

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

Quindi, in hadb02:

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

Dopo aver eseguito il failover manuale, è possibile ripetere la query remota, che dovrebbe funzionare perfettamente.

## <a name="set-up-corosync"></a>Configurare Corosync
Corosync è hello un'infrastruttura di cluster sottostante per Pacemaker toowork. Per Heartbeat (e altri metodi come Ultramonkey) Corosync è una suddivisione delle funzionalità CRM hello, mentre il Pacemaker rimane tooHeartbeat più simile nella funzionalità.

vincolo principale per Corosync Hello in Azure è che Corosync privilegia multicast broadcast unicast comunicazioni, ma la rete di Microsoft Azure supporta solo unicast.

Fortunatamente Corosync include una modalità di lavoro unicast. vincolo solo reale Hello è che, poiché tutti i nodi non comunicano tra loro, è necessario nodi hello toodefine nei file di configurazione, inclusi gli indirizzi IP. È possibile utilizzare file di esempio hello Corosync per Unicast e Modifica binding di indirizzo, elenchi di nodi e le directory di registrazione (Ubuntu Usa `/var/log/corosync` mentre utilizzato dai file di esempio hello `/var/log/cluster`) e consentire agli strumenti di quorum.

> [!NOTE]
> Utilizzare la seguente hello `transport: udpu` direttiva e hello definiti manualmente gli indirizzi IP per entrambi i nodi.

Esecuzione hello il seguente codice in `/etc/corosync/corosync.conf` per entrambi i nodi:

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

Copiare il file di configurazione in entrambe le VM e avviare Corosync in entrambi i nodi:

    sudo service start corosync

Subito dopo l'avvio del servizio di hello, è necessario stabilire cluster hello anello corrente hello e quorum deve essere costituito. Revisione dei registri o eseguendo hello seguente di codice, è possibile controllare questa funzionalità:

    sudo corosync-quorumtool –l

Si noterà toohello simili di output seguente immagine:

![output di esempio di corosync-quorumtool -l](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a>Configurare Pacemaker
Usa pacemaker hello toomonitor cluster per le risorse, definisce quando diminuisce primari e passa toosecondaries tali risorse. Le risorse possono essere definite da un set di script disponibili o da script LSB (simili all'inizializzazione), tra le altre possibilità.

Vogliamo Pacemaker risorsa DRBD hello troppo "un" punto di montaggio hello e servizio MySQL hello. Se il Pacemaker può attivare e disattivare DRBD, montare e smontare, quindi avviare e arrestare MySQL in hello destra ordine quando un'operazione non valida si verifica con hello primario, il programma di installazione è stata completata.

Quando si installa Pacemaker per la prima volta, la configurazione dovrebbe essere molto semplice, come:

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. Controllare la configurazione di hello eseguendo `sudo crm configure show`.
2. Quindi creare un file (ad esempio `/tmp/cluster.conf`) con hello seguenti risorse:

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. Caricare il file hello in configurazione hello. È necessario solo toodo questo in uno dei nodi.

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. Controllare che Pacemaker si avvii al momento giusto in entrambi i nodi:

        sudo update-rc.d pacemaker defaults

5. Utilizzando `sudo crm_mon –L`, verificare che uno dei nodi è diventato master hello per cluster hello e che è in esecuzione tutte le risorse di hello. È possibile utilizzare montaggio e ps toocheck risorse hello in esecuzione.

Hello seguente schermata mostra `crm_mon` con un solo nodo arrestato (uscita selezionando Ctrl + C):

![Nodo crm_mon arrestato](./media/mysql-cluster/image002.png)

Questa schermata mostra entrambi i nodi, uno master e uno slave:

![Master/slave operativo crm_mon](./media/mysql-cluster/image003.png)

## <a name="testing"></a>Test
Ora è possibile eseguire una simulazione del failover automatico. Esistono due modi toodo questo: software e hardware.

Hello soft viene utilizzata la funzione di arresto del cluster hello: ``crm_standby -U `uname -n` -v on``. Se si utilizza questa sul master hello, slave hello assume. Tenere presente che tooset questo toooff indietro. In caso contrario, crm_mon mostrerà un solo nodo in standby.

Hello complicata è in corso l'arresto verso il basso hello macchina virtuale primaria (hadb01) tramite il portale di hello o modificando hello /RL. su hello VM (ovvero, arresto, arresto). In questo modo Corosync e Pacemaker tramite segnalazioni corso della pagina master che hello verso il basso. È possibile testare questo (utile per le finestre di manutenzione), ma è anche possibile forzare scenario hello bloccando hello macchina virtuale.

## <a name="stonith"></a>STONITH
Dovrebbe essere possibile tooissue un arresto della macchina virtuale tramite hello CLI di Azure anziché uno script STONITH che controlla un dispositivo fisico. È possibile utilizzare `/usr/lib/stonith/plugins/external/ssh` come base e abilitare STONITH nella configurazione del cluster hello. CLI di Azure deve essere installato a livello globale e le impostazioni di pubblicazione hello e profilo deve essere caricato per l'utente del cluster hello.

È disponibile nel codice di esempio per la risorsa hello [GitHub](https://github.com/bureado/aztonith). Modificare la configurazione del cluster hello aggiungendo hello seguente troppo`sudo crm configure`:

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> script Hello non esegue controlli su/giù. risorsa SSH originale Hello aveva 15 verifica ping, ma il tempo di recupero per una macchina virtuale di Azure potrebbe essere più variabile.

## <a name="limitations"></a>Limitazioni
si applica Hello limitazioni seguenti:

* script di risorsa DRBD linbit che gestisce DRBD come risorsa in Usa Pacemaker Hello `drbdadm down` durante l'arresto di un nodo, anche se il nodo hello solo in modalità standby. Questo non è ideale perché slave hello verrà non sincronizzati risorsa DRBD hello mentre master hello Ottiene scritture. Se non viene eseguito gentilmente master hello, slave hello può richiedere più di un file system uno stato precedente. Per questo problema sono possibili due soluzioni:
  * Applicare un `drbdadm up r0` in tutti i nodi del cluster tramite un watchdog locale (non appartenente al cluster) oppure
  * Modifica di script di hello linbit DRBD, assicurandosi che `down` non viene chiamato in`/usr/lib/ocf/resource.d/linbit/drbd`
* servizio di bilanciamento del carico Hello deve toorespond almeno cinque secondi, in modo che le applicazioni devono essere compatibile con cluster e più tolleranti di timeout. Possono essere utili anche altre architetture, quali le code in-app e i middleware di query.
* Ottimizzazione di MySQL è necessario tooensure scrittura eseguita a un ritmo gestibile e memorizza nella cache è stati scaricati toodisk con una frequenza toominimize possibili perdite di memoria.
* Scrivere le prestazioni sono dipendenti in una macchina virtuale nel commutatore virtuale hello sono collegati perché questo è il meccanismo di hello utilizzato da DRBD tooreplicate hello dispositivo.
