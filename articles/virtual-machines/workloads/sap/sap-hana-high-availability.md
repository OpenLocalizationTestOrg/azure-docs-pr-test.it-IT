---
title: "Disponibilità di SAP HANA in macchine virtuali di Azure (VM) aaaHigh | Documenti Microsoft"
description: "Configurare la disponibilità elevata di SAP HANA in Macchine virtuali di Azure (VM)."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a>Disponibilità elevata di SAP HANA in Macchine virtuali di Azure (VM)

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

In locale, è possibile usare la replica di sistema HANA o archiviazione condivisa tooestablish la disponibilità elevata per SAP HANA.
Attualmente è supportata solo l'impostazione della replica di sistema HANA in Azure. La replica SAP HANA è costituita da un nodo master e almeno un nodo slave. Modifiche toohello dati sul nodo principale hello vengono replicati nodi slave toohello in modo sincrono o asincrono.

In questo articolo viene descritto come toodeploy hello macchine virtuali, configurare le macchine virtuali di hello, installare framework cluster hello, installare e configurare la replica di sistema di SAP HANA.
Nelle configurazioni di esempio hello, del numero di istanza e così via 03 i comandi di installazione e HANA sistema ID HDB viene utilizzata.

Leggere hello seguenti prima di note su SAP e documenti

* Nota SAP [1928533], contenente:
  * Elenco di dimensioni di macchina virtuale di Azure sono supportati per la distribuzione del software SAP hello
  * Importanti informazioni sulla capacità per le dimensioni delle VM di Azure
  * Software SAP e combinazioni di sistemi operativi e database supportati
  * Versione del kernel SAP richiesta per Windows e Linux in Microsoft Azure
* La nota SAP [2015553] elenca i prerequisiti per le distribuzioni di software SAP supportate da SAP in Azure.
* La nota SAP [2205917] contiene le impostazioni consigliate del sistema operativo per SUSE Linux Enterprise Server for SAP Applications
* La nota SAP [1944799] contiene linee guida per SAP HANA per SUSE Linux Enterprise Server for SAP Applications
* La nota SAP [2178632] contiene informazioni dettagliate su tutte le metriche di monitoraggio segnalate per SAP in Azure.
* Nota SAP [2191498] hello necessario versione dell'agente Host SAP per Linux in Azure.
* La nota SAP [2243692] contiene informazioni sulle licenze SAP in Linux in Azure.
* La nota SAP [1984787] contiene informazioni generali su SUSE Linux Enterprise Server 12.
* Nota SAP [1999351] contiene altre informazioni sulla risoluzione dei problemi per hello Azure Enhanced Monitoring Extension per SAP.
* [Community WIKI SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) contiene tutte le note su SAP necessarie per Linux.
* [Pianificazione e implementazione di Macchine virtuali di Azure per SAP in Linux][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP in Linux (questo articolo)][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP in Linux][dbms-guide]
* [SAP HANA SR prestazioni ottimizzate Scenario] [ suse-hana-ha-guide] Guida hello contiene tutte le informazioni necessarie tooset di SAP HANA sistema replica locale. Usare la guida per le indicazioni di base.

## <a name="deploying-linux"></a>Distribuzione di Linux

agente di risorsa Hello per SAP HANA è incluso in SUSE Linux Enterprise Server per le applicazioni SAP.
Hello Azure Marketplace contiene un'immagine per SUSE Linux Enterprise Server per SAP applicazioni 12 con BYOS (portare il propria sottoscrizione) che è possibile utilizzare toodeploy nuove macchine virtuali.

### <a name="manual-deployment"></a>Distribuzione manuale

1. Creare un gruppo di risorse
1. Creare una rete virtuale
1. Creare due account di archiviazione
1. Creare un set di disponibilità  
   Impostare il numero massimo di domini di aggiornamento
1. Creare un servizio di bilanciamento del carico (interno)  
   Selezionare la rete virtuale del passaggio precedente
1. Creare la macchina virtuale 1  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   Selezionare l'account di archiviazione 1  
   Selezionare il set di disponibilità  
1. Creare la macchina virtuale 2  
   https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1  
   SLES For SAP Applications 12 SP1 (BYOS)  
   Selezionare l'account di archiviazione 2   
   Selezionare il set di disponibilità  
1. Aggiungere dischi dati
1. Configurare il bilanciamento del carico hello
    1. Creare un pool di indirizzi IP front-end
        1. Aprire servizio di bilanciamento del carico hello, selezionare il pool IP front-end e fare clic su Aggiungi
        1. Immettere il nome di hello hello nuovo front-end del pool di IP (ad esempio hana-front-end)
       1. Fare clic su OK.
        1. Dopo aver creato il nuovo pool di IP front-end di hello, annotare il relativo indirizzo IP
    1. Creare un pool back-end
        1. Aprire servizio di bilanciamento del carico hello, selezionare il pool back-end e fare clic su Aggiungi
        1. Immettere il nome di hello del pool back-end nuovo hello (ad esempio hana-back-end)
        1. Fare clic su Aggiungi una macchina virtuale
        1. Selezionare i Set di disponibilità creato in precedenza hello
        1. Selezionare le macchine virtuali hello del cluster di SAP HANA hello
        1. Fare clic su OK.
    1. Creare un probe di integrità
       1. Aprire hello bilanciamento del carico, selezionare i probe di integrità e fare clic su Aggiungi
        1. Immettere il nome di hello del probe di integrità nuovo hello (ad esempio hana hp)
        1. Selezionare TCP come protocollo, la porta 625**03**, mantenere 5 per Intervallo e impostare il valore di Soglia di non integrità su 2
        1. Fare clic su OK.
    1. Creare le regole di bilanciamento del carico
        1. Aprire servizio di bilanciamento del carico hello, selezionare regole di bilanciamento del carico e fare clic su Aggiungi
        1. Immettere il nome di hello della regola di bilanciamento del carico nuovo hello (ad esempio hana-lb-3**03**15)
        1. Indirizzo IP di front-end Select hello, pool back-end e integrità probe è creato in precedenza (ad esempio hana-front-end)
        1. Mantenere il protocollo TCP, immettere la porta 3**03**15
        1. Aumentare il timeout di inattività too30 minuti
       1. **Verificare che tooenable IP mobile**
        1. Fare clic su OK.
        1. Ripetere i passaggi di hello sopra per la porta 3**03**17

### <a name="deploy-with-template"></a>Eseguire la distribuzione con un modello
È possibile utilizzare uno dei modelli di avvio rapido hello in github toodeploy tutte le risorse necessarie. Consente di distribuire il modello di Hello hello le macchine virtuali, bilanciamento del carico hello, disponibilità, set e così via. Seguire questi modelli di hello toodeploy passaggi:

1. Aprire hello [modello di database] [ template-multisid-db] o hello [convergente modello] [ template-converged] nel portale di Azure hello hello database modello solo consente di creare hello regole di bilanciamento del carico per un database mentre hello convergente modello crea anche hello regole di bilanciamento del carico per un ASCS/SCS e un'istanza di Hiamanti (solo Linux). Se si prevede un sistema basate su SAP NetWeaver tooinstall e si desidera anche hello tooinstall ASCS/SCS istanza su hello stesso computer, utilizzare hello [convergente modello][template-converged].
1. Immettere i seguenti parametri hello
    1. ID sistema SAP  
       Immettere il sistema SAP hello Id di sistema SAP si desidera tooinstall hello. Hello Id verrà considerato come prefisso per le risorse di hello che vengono distribuite.
    1. Tipo di stack (applicabile solo se si Usa modello convergente hello)  
       Selezionare tipo di stack hello SAP NetWeaver
    1. Tipo di sistema operativo  
       Selezionare una delle distribuzioni di Linux hello. Per questo esempio, selezionare SLES 12 BYOS
    1. Tipo di database  
       Selezionare HANA
    1. Dimensioni del sistema SAP  
       quantità di Hello del nuovo sistema SAP hello fornirà. Se non si conoscono quanti valori SAPS hello sistema richiederà, chiedere il Partner di tecnologia di SAP o l'integratore di sistema
    1. Disponibilità del sistema  
       Selezionare la disponibilità elevata.
    1. Nome utente e password amministratore  
       Viene creato un nuovo utente che può essere utilizzato toolog toohello computer.
    1. Subnet nuova o esistente  
       Determina se devono essere create una nuova rete virtuale e una nuova subnet o deve essere usata una subnet esistente. Se si dispone già di una rete virtuale è una rete locale tooyour connesso, selezionare esistente.
    1. ID subnet  
    ID Hello delle macchine virtuali di hello subnet toowhich hello deve essere connessa a. Selezionare hello subnet della rete VPN o Express Route rete virtuale tooconnect hello macchina virtuale tooyour locale rete. ID Hello in genere è simile /Subscriptions/<ID`<subscription id`>/ResourceGroups /`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`>

## <a name="setting-up-linux-ha"></a>Configurazione della disponibilità elevata di Linux

Hello seguenti elementi è preceduto da uno [A] - nodi tooall applicabile, toonode applicabile solo [1] - toonode applicabile solo 1 o [2] - 2.

1. [A] SLES per SAP BYOS solo - repository hello toouse in grado di registrare SLES toobe
1. [A] Solo SLES per SAP BYOS - Aggiungere il modulo cloud pubblico
1. [A] Aggiornare SLES
    ```bash
    sudo zypper update

    ```

1. [1] Abilitare l'accesso SSH
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. [2] Abilitare l'accesso SSH
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. [1] Abilitare l'accesso SSH
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. [A] Installare l'estensione per la disponibilità elevata
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. [A] Configurare il layout dei dischi
    1. LVM  
    In genere è consigliabile toouse LVM per volumi in cui archiviare i dati e i file di log. esempio Hello riportato di seguito presuppone che le macchine virtuali hello disponga di quattro dischi dati collegati che devono essere utilizzati toocreate due volumi.
        * Creare volumi fisici per tutti i dischi che si desidera toouse.
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * Creare un gruppo di volumi per il file di dati di hello, un gruppo di volumi per il file di log hello e una directory condivisa hello SAP HANA
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * Creare hello volumi logici
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * Creare le directory di montaggio hello e copiare hello UUID di tutti i volumi logici
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * Creare le voci di fstab per hello tre volumi logici
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    Inserire questa riga troppo/ecc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * Montare i volumi di nuovo hello
    <pre><code>
    sudo mount -a
    </code></pre>
    1. Dischi normali  
       Per sistemi demo o di piccole dimensioni, è possibile inserire i dati e i file di log HANA su un disco. Hello seguenti comandi creare una partizione su /dev/sdc e formattarla con xfs.
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a>Annotare l'id di hello di /dev/sdc1
    sudo /sbin/blkid sudo vi /etc/fstab
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. [A] Configurare la risoluzione dei nomi host per tutti gli host  
    È possibile usare un server DNS o modificare /etc/hosts hello in tutti i nodi. Questo esempio mostra come toouse hello file /etc/hosts.
   Sostituire l'indirizzo IP hello e nome host hello in hello seguenti comandi
    ```bash
    sudo vi /etc/hosts
    ```
    Inserire hello seguenti righe troppo/ecc/host. Modificare l'ambiente di hello IP indirizzo e nome host toomatch    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. [1] Installare il cluster
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. [2] Aggiungi nodo toocluster
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. [A] modifica di hacluster password toohello stessa password
    ```bash
    sudo passwd hacluster
    
    ```

1. [A] configurare corosync toouse altro trasporto e aggiungere nodelist. In caso contrario, il cluster non funzionerà.
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    Aggiungere i seguenti file grassetto toohello contenuto hello.
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    Riavviare il servizio di corosync hello

    ```bash
    sudo service corosync restart
    
    ```

1. [A] Installare pacchetti HANA a disponibilità elevata  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a>Installazione di SAP HANA

Seguire il capitolo 4 di hello [SAP HANA SR prestazioni ottimizzate Scenario guide] [ suse-hana-ha-guide] tooinstall SAP HANA sistema di replica.

1. [A] eseguire hdblcm da hello HANA DVD
    * Scegliere l'installazione -> 1
    * Selezionare i componenti aggiuntivi per l'installazione -> 1
    * Immettere il percorso di installazione [/hana/shared]: -> INVIO
    * Immettere il nome host locale [..]: -> INVIO
    * Sistema di toohello tooadd ulteriori host si desidera? (y/n) [n]: -> INVIO
    * Immettere l'ID di sistema SAP HANA: <SID of HANA e.g. HDB>
    * Immettere il numero di istanza [00]:   
  Numero di istanza di HANA. Utilizzare 03 se è utilizzato il modello di Azure hello o esempio hello sopra riportato di seguito
    * Selezionare la modalità di database/immettere l'indice [1]: -> INVIO
    * Selezionare l'utilizzo del sistema/immettere l'indice [4]:  
  Selezionare il sistema di hello utilizzo
    * Immettere il percorso dei volumi di dati [/hana/data/HDB]: -> INVIO
    * Immettere il percorso dei volumi di log [/hana/log/HDB]: -> INVIO
    * Limitare l'allocazione massima della memoria? [n]: -> INVIO
    * Immettere nome Host del certificato per l'Host '...' […]: -> Invio
    * Immettere la password dell'utente agente host SAP (sapadm):
    * Confermare la password dell'utente agente host SAP (sapadm):
    * Immettere la password dell'amministratore di sistema (hdbadm):
    * Confermare la password dell'amministratore di sistema (hdbadm):
    * Immettere la home directory dell'amministratore di sistema [/usr/sap/HDB/home]: -> INVIO
    * Immettere la shell di accesso dell'amministratore di sistema [/bin/sh]: -> INVIO
    * Immettere l'ID utente dell'amministratore di sistema [1001]: -> INVIO
    * Immettere l'ID del gruppo di utenti (sapsys) [79]: -> INVIO
    * Immettere la password dell'utente del database (SYSTEM):
    * Confermare la password dell'utente del database (SYSTEM):
    * Riavviare il sistema dopo il riavvio della macchina? [n]: -> INVIO
    * Si desidera toocontinue? (y/n):  
  Convalidare hello riepilogo e immettere y toocontinue
1. [A] Aggiornare l'agente host SAP  
  Scaricare l'archivio agente Host SAP più recente hello da hello [SAP Softwarecenter] [ sap-swcenter] ed eseguiti hello seguenti comando tooupgrade hello agente. Sostituire hello percorso toohello archivio toopoint toohello file scaricato.
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. [1] Creare la replica HANA (come radice)  
    Eseguire hello comando seguente. Verificare che tooreplace grassetto stringhe (HANA sistema ID HDB e numero di istanza 03) con valori di hello dell'installazione di SAP HANA.
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. [A] Creare una voce di archivio chiavi (come radice)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. [1] Eseguire il backup del database (come radice)
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. [1] passare toohello sapsid utente (ad esempio hdbadm) e creare il sito primario di hello.
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. [2] passare toohello sapsid utente (ad esempio hdbadm) e creare il sito secondario di hello.
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a>Configurare il framework del cluster

Modificare le impostazioni predefinite di hello

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>ora di caricare cluster toohello di file hello
sudo crm configure load update crm-defaults.txt
</pre>

### <a name="create-stonith-device"></a>Creare il dispositivo STONITH

dispositivo STONITH Hello utilizza un tooauthorize dell'entità servizio in Microsoft Azure. Seguire questi toocreate passaggi un'entità servizio.

1. Andare troppo<https://portal.azure.com>
1. Pannello di Azure Active Directory aprire hello  
   Passare tooProperties e annotare hello ID di Directory. Si tratta di hello **id tenant**.
1. Fare clic su Registrazioni per l'app
1. Fare clic su Aggiungi.
1. Immettere un nome, selezionare il tipo di applicazione "App Web/API", immettere un URL di accesso (ad esempio http://localhost) e fare clic su Crea
1. URL Hello-sign-on non viene utilizzato e può essere un URL valido
1. Selezionare hello nuova App e fare clic su chiavi nella scheda Impostazioni hello
1. Immettere una descrizione per una nuova chiave, selezionare "Non scade mai" e fare clic su Salva
1. Annotare hello valore. Viene utilizzato come hello **password** per hello dell'entità servizio
1. Annotare hello ID dell'applicazione. Viene utilizzato come nome utente di hello (**id di accesso** in seguito hello) di hello dell'entità servizio

Hello dell'entità servizio non dispone delle autorizzazioni tooaccess le risorse di Azure per impostazione predefinita. È necessario toogive hello dell'entità servizio autorizzazioni toostart e l'arresto (deallocazione) tutte le macchine virtuali del cluster di hello.

1. Passare toohttps://portal.azure.com
1. Apri hello tutti pannello risorse
1. Selezionare la macchina virtuale di hello
1. Fare clic su Controllo di accesso (IAM)
1. Fare clic su Aggiungi.
1. Selezionare il ruolo di hello proprietario
1. Immettere il nome di hello dell'applicazione hello creato in precedenza
1. Fare clic su OK.

Dopo le autorizzazioni di hello per le macchine virtuali hello modificato, è possibile configurare i dispositivi STONITH hello cluster hello.

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>ora di caricare cluster toohello di file hello
sudo crm configure load update crm-fencing.txt
</pre>

### <a name="create-sap-hana-resources"></a>Creare risorse SAP HANA

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>ora di caricare cluster toohello di file hello
sudo crm configure load update crm-saphanatop.txt
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a>ora di caricare cluster toohello di file hello
sudo crm configure load update crm-saphana.txt
</pre>

### <a name="test-cluster-setup"></a>Testare la configurazione del cluster
Hello seguente capitolo viene descritto come è possibile testare il programma di installazione. Ogni test si presuppone che sono radice e master di SAP HANA hello è in esecuzione in hello saphanavm1 di macchina virtuale.

#### <a name="fencing-test"></a>Test di isolamento

È possibile verificare l'installazione di hello dell'agente fencing hello disabilitando l'interfaccia di rete hello saphanavm1 nodo.

<pre><code>
sudo ifdown eth0
</code></pre>

macchina virtuale Hello deve ora ottenere riavviato o arrestato a seconda della configurazione del cluster.
Se si imposta toooff stonith azione hello, macchina virtuale hello verrà arrestato e risorse hello toohello migrato in esecuzione sulla macchina virtuale.

Quando si avvia macchina virtuale hello nuovamente, hello risorse SAP HANA avrà esito negativo toostart come database secondario se si imposta AUTOMATED_REGISTER = "false". In questo caso, è necessario tooconfigure hello HANA istanza secondaria eseguendo hello comando seguente:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a>Test di un failover manuale

È possibile testare un failover manuale per l'arresto del servizio di pacemaker hello nel nodo saphanavm1.
<pre><code>
service pacemaker stop
</code></pre>

Dopo il failover hello, è possibile avviare il servizio hello nuovamente. Hello risorse SAP HANA in saphanavm1 avrà esito negativo toostart come database secondario se si imposta AUTOMATED_REGISTER = "false". In questo caso, è necessario tooconfigure hello HANA istanza secondaria eseguendo hello comando seguente:

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a>Test di una migrazione

È possibile eseguire la migrazione di nodo principale di SAP HANA hello eseguendo hello comando seguente
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

Si deve eseguire la migrazione di nodo principale di SAP HANA hello e gruppo hello contenente toosaphanavm2 di indirizzo IP virtuale hello.
Hello risorse SAP HANA in saphanavm1 avrà esito negativo toostart come database secondario se si imposta AUTOMATED_REGISTER = "false". In questo caso, è necessario tooconfigure hello HANA istanza secondaria eseguendo hello comando seguente:

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

la migrazione di Hello crea vincoli di percorso che è necessario toobe nuovamente.

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

È inoltre necessario stato hello toocleanup della risorsa di hello nodo secondario

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a>Passaggi successivi
* [Pianificazione e implementazione di Macchine virtuali di Azure per SAP][planning-guide]
* [Distribuzione di Macchine virtuali di Azure per SAP][deployment-guide]
* [Distribuzione DBMS di Macchine virtuali di Azure per SAP][dbms-guide]
* toolearn tooestablish la disponibilità elevata e piano di ripristino di emergenza di SAP HANA in Azure (istanze di grandi dimensioni), vedere [SAP HANA (istanze di grandi dimensioni) ad alto disponibilità e ripristino di emergenza in Azure](hana-overview-high-availability-disaster-recovery.md). 
