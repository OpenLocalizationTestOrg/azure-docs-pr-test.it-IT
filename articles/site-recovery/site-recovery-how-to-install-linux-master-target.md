---
title: aaaHow tooinstall un server di destinazione master Linux per il failover da locale tooon Azure | Documenti Microsoft
description: "Prima di eseguire la riprotezione di una macchina virtuale Linux, è necessario dotarsi di un server di destinazione master Linux. Informazioni su come tooinstall uno."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a>Installare un server di destinazione master Linux
Dopo aver eseguito il failover delle macchine virtuali, è possibile eseguire il backup hello macchine virtuali toohello nel sito locale. toofail nuovamente, è necessario tooreprotect hello macchina virtuale Azure toohello nel sito locale. Per questo processo, è necessario un traffico di hello tooreceive del server di destinazione master di on-premise. 

Se quella protetta è una macchina virtuale Windows, è necessario un server di destinazione master Windows. Per una macchina virtuale Linux è necessario un server di destinazione master Linux. Lettura hello seguenti passaggi viene toolearn come toocreate e installare Linux master destinazione.

> [!IMPORTANT]
> A partire dalla versione del server di destinazione master hello 9.10.0, hello più recente destinazione master server può essere installato solo su un server Ubuntu 16.04. Le nuove installazioni non sono consentite nei server CentOS6.6. Tuttavia, è possibile continuare tooupgrade i server di destinazione master precedente utilizzando la versione di hello 9.10.0.

## <a name="overview"></a>Panoramica
In questo articolo vengono fornite istruzioni per la modalità tooinstall Linux master di destinazione.

Registrare commenti o domande alla fine di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Prerequisiti

* host di hello toochoose in quale destinazione master hello toodeploy, determinare se il failback hello verrà toobe tooan locali esistenti tooa nuova macchina virtuale o macchina virtuale. 
    * Per una macchina virtuale esistente, hello host di destinazione master hello deve disporre di accesso toohello di archivi di dati della macchina virtuale hello.
    * Se non esiste una macchina virtuale locale di hello, macchina virtuale di failback hello viene creato in hello stesso host di destinazione master hello. È possibile scegliere qualsiasi host ESXi di destinazione master di tooinstall hello.
* la destinazione master Hello deve trovarsi in una rete in grado di comunicare con il server di elaborazione hello e il server di configurazione di hello.
* versione di Hello della destinazione master hello deve essere tooor uguale precedenza rispetto alle versioni hello del server di elaborazione hello e il server di configurazione di hello. Ad esempio, se versione hello hello del server di configurazione di 9.4, può essere versione hello della destinazione master hello 9.4 o 9.3 ma non di 9,5.
* la destinazione master Hello può essere solo una macchina virtuale VMware e non un server fisico.

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a>Creare la destinazione master di hello in base a toohello linee guida di ridimensionamento

Creare la destinazione master di hello in base alle indicazioni di ridimensionamento hello:
- **RAM**: almeno 6 GB
- **Dimensioni del disco del sistema operativo**: 100 GB o più (tooinstall CentOS6.6)
- **Dimensioni disco aggiuntive per l'unità di conservazione**: 1 TB
- **Core CPU**: almeno 4 core

esempio Hello supportato Ubuntu kernel sono supportati.


|Serie di kernel  |Supporto troppo alto |
|---------|---------|
|4.4      |4.4.0-81-generico         |
|4.8      |4.8.0-56-generico         |
|4.10     |4.10.0-24-generico        |


## <a name="deploy-hello-master-target-server"></a>Distribuire il server di destinazione master hello

### <a name="install-ubuntu-16042-minimal"></a>Installare Ubuntu 16.04.2 Minimal

Richiedere hello seguenti del sistema operativo a 64 bit di hello passaggi tooinstall hello Ubuntu 16.04.2.

**Passaggio 1:** passare toohello [collegamento per il download](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) scegliere mirror di hello più vicino da cui scaricare un file ISO di Ubuntu 16.04.2 minimo a 64 bit.

Mantenere un'immagine ISO a 64 bit minimo di Ubuntu 16.04.2 nell'unità DVD hello e avviare hello del sistema.

**Passaggio 2:** selezionare **English** (Inglese) come lingua preferita e premere **Invio**.

![Selezionare una lingua](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

**Passaggio 3:** selezionare **Install Ubuntu Server** (Installa server Ubuntu) e premere **Invio**.

![Selezionare Installa server Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

**Passaggio 4:** selezionare **English** (Inglese) come lingua preferita e premere **Invio**.

![Selezionare English (Inglese) come lingua preferita](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

**Passaggio 5:** selezionare hello opzione appropriata hello **fuso orario** elenco di opzioni e quindi selezionare **invio**.

![Selezionare il fuso orario corretti di hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

**Passaggio 6:** selezionare **n** (hello. opzione predefinita), quindi selezionare **invio**.


![Configurare hello tastiera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

**Passaggio 7:** selezionare **inglese (Stati Uniti)** come hello paese di origine per la tastiera hello e quindi selezionare **invio**.

![Selezionare Usa come paese hello di origine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

**Passaggio 8:** selezionare **inglese (Stati Uniti)** come layout di tastiera hello, quindi selezionare **invio**.

![Selezionare l'inglese come layout di tastiera hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

**Passaggio 9:** immettere nome host di hello del server in hello **Hostname** e quindi selezionare **continua**.

![Immettere nome host di hello del server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

**Passaggio 10:** toocreate un account utente, immettere nome utente hello e quindi selezionare **continua**.

![Crea un account utente](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

**Passaggio 11:** immettere hello password per account utente nuovo hello e quindi selezionare **continua**.

![Immettere la password di hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

**Passaggio 12:** Conferma password hello hello nuovo utente e quindi selezionare **continua**.

![Conferma password hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

**Passaggio 13:** selezionare **n** (hello. opzione predefinita), quindi selezionare **invio**.

![Configurare utenti e password](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

**Passaggio 14:** se hello fuso orario visualizzato sia corretto, selezionare **Sì** (hello. opzione predefinita), quindi selezionare **invio**.

tooreconfigure il fuso orario **n**.

![Configurare orologio hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

**Passaggio 15:** hello metodo opzioni di partizionamento, selezionare **interattiva - utilizzare l'intero disco**, quindi selezionare **invio**.

![Selezionare l'opzione metodo di partizionamento hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

**Passaggio 16:** selezionare hello disco appropriato da hello **selezionare disco toopartition** opzioni e quindi selezionare **invio**.


![Selezionare il disco hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

**Passaggio 17:** selezionare **Sì** toowrite hello toodisk modifiche e quindi selezionare **invio**.

![Scrivere hello modifiche toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

**Passaggio 18:** selezionare l'opzione predefinita di hello, selezionare **continua**, quindi selezionare **invio**.

![Selezionare l'opzione predefinita hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

**Passaggio 19:** selezionare hello opzione appropriata per la gestione degli aggiornamenti del sistema e quindi selezionare **invio**.

![Selezionare la modalità di aggiornamento toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> Poiché il server di destinazione master hello Azure Site Recovery richiede una versione di hello Ubuntu molto specifica, è necessario tooensure tale kernel hello gli aggiornamenti sono disabilitati per la macchina virtuale hello. Se sono abilitati, eventuali aggiornamenti regolari causano toomalfunction server di destinazione master hello. Assicurarsi di selezionare hello **alcun aggiornamento automatico** opzione.


**Passaggio 20:** selezionare le opzioni predefinite. Se si desidera openSSH per la connessione SSH, selezionare hello **server OpenSSH** opzione e quindi selezionare **continua**.

![Selezionare il software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

**Passaggio 21:** selezionare **Sì** e quindi **Invio**.

![Caricatore di avvio installazione hello GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

**Passaggio 22:** selezionare hello dispositivi appropriati per l'installazione del caricatore di avvio hello (preferibilmente **dev/sda**), quindi selezionare **invio**.

![Selezionare un dispositivo per l'installazione del caricatore di avvio](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

**Passaggio 23:** selezionare **continua**, quindi selezionare **invio** installazione hello toofinish.

![Completare l'installazione di hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

Al termine dell'installazione di hello, accedi toohello VM con le nuove credenziali utente hello. (Vedere troppo**passaggio 10** per ulteriori informazioni.)

Eseguire i passaggi di hello descritti nella seguente schermata tooset hello radice hello password utente. Quindi, accedere come utente ROOT.

![Password dell'utente ROOT hello set](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a>Preparare il computer di hello per la configurazione come server di destinazione master
Successivamente, preparare il computer di hello per la configurazione come server di destinazione master.

ID di hello tooget per ogni disco rigido SCSI in una macchina virtuale Linux, abilitare hello **disco. EnableUUID = TRUE** parametro.

tooenable questo parametro, hello take seguendo i passaggi:

1. Arrestare la macchina virtuale.

2. Voce hello per la macchina virtuale hello nel riquadro di sinistra hello e quindi scegliere **Modifica impostazioni**.

3. Seleziona hello **opzioni** scheda.

4. Nel riquadro sinistro hello selezionare **avanzate** > **generale**, quindi selezionare hello **parametri di configurazione** pulsante nella parte inferiore destra hello della schermata di hello.

    ![Scheda Opzioni](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    Hello **parametri di configurazione** opzione non è disponibile quando hello macchina è in esecuzione. toomake questa scheda è attiva, spegnere la macchina virtuale hello.

5. Controllare se esiste già una riga con il valore **disk.EnableUUID**.

    - Se il valore di hello esiste e viene impostato troppo**False**, modificare il valore di hello troppo**True**. (valori hello non sono distinzione maiuscole/minuscole).

    - Se il valore di hello esiste e viene impostato troppo**True**selezionare **Annulla**.

    - Se il valore di hello non esiste, selezionare **Aggiungi riga**.

    - Nella colonna nome hello, aggiungere **disco. EnableUUID**, quindi impostare il valore di hello troppo**TRUE**.

    ![Controllare se esiste già una riga con il valore disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a>Disabilitare gli aggiornamenti del kernel

Server di destinazione master di Azure Site Recovery richiede una versione molto specifica di hello Ubuntu, verificare che gli aggiornamenti kernel hello sono disabilitati per la macchina virtuale hello.

Se sono abilitati gli aggiornamenti del kernel, eventuali aggiornamenti regolari causano toomalfunction server di destinazione master hello.

#### <a name="download-and-install-additional-packages"></a>Scaricare e installare i pacchetti aggiuntivi

> [!NOTE]
> Assicurarsi di aver toodownload connettività Internet e installare pacchetti aggiuntivi. Se non si dispone di connettività Internet, è necessario toomanually trovare questi pacchetti RPM e installarli.

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a>Ottenere installer hello per il programma di installazione

Se la destinazione master disponga della connettività Internet, è possibile utilizzare hello seguente programma di installazione di passaggi toodownload hello. In caso contrario, è possibile copiare installer hello dal server di elaborazione hello e quindi installarlo.

#### <a name="download-hello-master-target-installation-packages"></a>Scaricare i pacchetti di installazione di destinazione master hello

[Scaricare i bit di hello più recente Linux destinazione master installazione](https://aka.ms/latestlinuxmobsvc).

toodownload usando Linux, tipo:

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

Assicurarsi di scaricare e decomprimere installer hello nella home directory. Se decomprimere troppo**usr/Local**, installazione hello ha esito negativo.


#### <a name="access-hello-installer-from-hello-process-server"></a>Programma di installazione di accesso hello dal server di elaborazione hello

1. Nel server di elaborazione hello, andare troppo**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.

2. Copiare il file di programma di installazione necessari hello dal server di elaborazione hello e salvarlo come **latestlinuxmobsvc.tar.gz** nella home directory.


### <a name="apply-custom-configuration-changes"></a>Applicare le modifiche di configurazione personalizzate

modifiche di configurazione personalizzata tooapply, utilizzare hello alla procedura seguente:


1. Eseguire hello binario hello toountar di comando seguente.
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Schermata di hello comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. Comando che segue di esecuzione hello toogive autorizzazione.
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. Eseguire lo script di comando toorun hello seguente hello.
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> Eseguire script hello una sola volta nel server di hello. Arrestare il server di hello. Quindi riavviare hello server dopo aver aggiunto un disco, come descritto nella sezione successiva hello.

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a>Aggiungere una macchina virtuale destinazione master Linux di memorizzazione disco toohello

Utilizzare hello seguendo i passaggi toocreate un disco di conservazione:

1. Collegare una nuova disco 1 TB toohello Linux destinazione master macchina virtuale e quindi avviare hello macchina.

2. Hello utilizzare **a percorsi multipli -ll** toolearn ID con percorsi multipli hello del disco di conservazione hello di comando.

    ```
    multipath -ll
    ```
    ![ID di multipath Hello del disco di conservazione di hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. Formattare l'unità di hello e quindi creare un file system hello nuova unità.

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Creazione di un file system nell'unità hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. Dopo aver creato il sistema di file hello, montare il disco di conservazione hello.
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco di conservazione di montaggio hello](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. Creare hello **fstab** voce toomount hello unità di conservazione ogni volta che viene avviato il sistema hello.
    ```
    vi /etc/fstab
    ```
    Selezionare **inserire** toobegin modifica file hello. Creare una nuova riga e quindi inserire dopo testo hello. Modificare multipath ID disco hello in base all'ID di multipath hello evidenziata dal comando precedente hello.

    **/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**

    Selezionare **Esc**, quindi digitare **: wq** (scrivere e chiudere) finestra dell'editor tooclose hello.

### <a name="install-hello-master-target"></a>Installare la destinazione master hello

> [!IMPORTANT]
> versione di Hello del server di destinazione master hello deve essere tooor uguale precedenza rispetto alle versioni hello del server di elaborazione hello e il server di configurazione di hello. Se la versione del server master di destinazione è superiore, la riprotezione avrà esito positivo, ma la replica avrà esito negativo.


> [!NOTE]
> Prima di installare il server di destinazione master hello, verificare che hello **/e così via/host** file nella macchina virtuale hello contiene voci che mappa gli indirizzi IP toohello di nome host locale hello che sono associati a tutte le schede di rete.

1. Copiare la passphrase hello da **C:\ProgramData\Microsoft Azure sito Recovery\private\connection.passphrase** nel server di configurazione hello. Quindi salvarlo come **passphrase.txt** in hello stessa directory locale eseguendo hello comando seguente:

    ```
    echo <passphrase> >passphrase.txt
    ```
    Esempio: 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. Nota l'indirizzo IP del server di configurazione hello. È necessario nel passaggio successivo hello.

3. Eseguire hello seguente server di destinazione master comando tooinstall hello e registrare server hello con il server di configurazione di hello.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    Esempio: 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    Attendere il completamento dello script hello. Se la destinazione master hello registra correttamente, la destinazione master hello è elencata in hello **infrastruttura di Site Recovery** pagina del portale hello.


#### <a name="install-hello-master-target-by-using-interactive-installation"></a>Installare la destinazione master hello utilizzando Installazione interattiva

1. Eseguire hello seguente destinazione di comando tooinstall hello master. Per il ruolo dell'agente hello scegliere **destinazione Master**.

    ```
    ./install
    ```

2. Selezionare il percorso predefinito hello per l'installazione e quindi selezionare **invio** toocontinue.

    ![Scelta di un percorso predefinito per l'installazione del server di destinazione master](./media/site-recovery-how-to-install-linux-master-target/image17.png)

Al termine dell'installazione di hello, registrare il server di configurazione di hello dalla riga di comando hello.

1. Nota l'indirizzo IP hello hello del server di configurazione. È necessario nel passaggio successivo hello.

2. Eseguire hello seguente server di destinazione master comando tooinstall hello e registrare server hello con il server di configurazione di hello.

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    Esempio: 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   Attendere il completamento dello script hello. Se la destinazione master hello è registrato correttamente, la destinazione master hello è elencata in hello **infrastruttura di Site Recovery** pagina del portale hello.


### <a name="upgrade-hello-master-target"></a>Aggiornare la destinazione master hello

Eseguire l'installazione guidata di hello. Rileva automaticamente che l'agente di hello è installato nella destinazione master hello. tooupgrade, selezionare **Y**.  Al termine dell'installazione di hello, controllare la versione hello della destinazione master di hello installato utilizzando hello comando seguente.

    ```
    cat /usr/local/.vx_version
    ```

È possibile visualizzare tale hello **versione** campo fornisce il numero di versione hello della destinazione master hello.

### <a name="install-vmware-tools-on-hello-master-target-server"></a>Installare gli strumenti VMware nel server di destinazione master hello

È necessario tooinstall VMware tools nella destinazione master hello in modo che è possibile rilevare gli archivi dati hello. Se non sono installati gli strumenti di hello, schermata di riprotezione hello non elencato in archivi dati hello. Dopo l'installazione di strumenti di VMware hello, è necessario toorestart.

## <a name="next-steps"></a>Passaggi successivi
Dopo l'installazione hello e la registrazione della destinazione master hello è finsihed, è possibile visualizzare la destinazione master hello vengono visualizzati nel hello **destinazione Master** sezione **infrastruttura di Site Recovery**, in hello Panoramica di server di configurazione.

È ora possibile procedere con la [riprotezione](site-recovery-how-to-reprotect.md), seguita dal failback.

## <a name="common-issues"></a>Problemi comuni

* Verificare che Storage vMotion non sia abilitato in alcun componente di gestione, ad esempio il server di destinazione master. Se la destinazione master hello Sposta dopo un riprotezione ha esito positivo, non è possibile scollegare i dischi di macchina virtuale di hello (VMDK). In questo caso, il failback avrà esito negativo.

* la destinazione master Hello non deve avere uno snapshot nella macchina virtuale hello. Se sono presenti snapshot, il failback avrà esito negativo.

* A causa di toosome NIC le configurazioni personalizzate in alcuni clienti, l'interfaccia di rete hello è disabilitato durante l'avvio e non è possibile inizializzare l'agente di destinazione master hello. Verificare che tale hello le proprietà seguenti sono state impostate correttamente. Controllare queste proprietà in hello Ethernet /etc/sysconfig/network-scripts/ifcfg del file di scheda-eth *.
    * BOOTPROTO=dhcp
    * ONBOOT=yes
