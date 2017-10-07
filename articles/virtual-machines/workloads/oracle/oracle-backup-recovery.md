---
title: aaaBack backup e ripristinare un Database Oracle 12C database in una macchina virtuale Linux di Azure | Documenti Microsoft
description: Informazioni su database tooback backup e ripristinare un Database Oracle 12C nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Eseguire backup e ripristino di un database Oracle Database 12c in una macchina virtuale Linux di Azure

Si può utilizzare toocreate CLI di Azure e gestire risorse di Azure a un prompt dei comandi o utilizzare gli script. In questo articolo, si usa Azure CLI script toodeploy un database di Oracle Database 12C da un'immagine della raccolta di Azure Marketplace.

Prima di iniziare, assicurarsi che l'interfaccia della riga di comando di Azure sia installata. Per ulteriori informazioni, vedere hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Preparare l'ambiente hello

### <a name="step-1-prerequisites"></a>Passaggio 1: Prerequisiti

*   processo di backup e ripristino di hello tooperform, è innanzitutto necessario creare una VM Linux con un'istanza installata di Oracle Database 12C. immagine del Marketplace Hello è utilizzare hello toocreate VM è denominato *Oracle: Oracle-Database-Ee:12.1.0.2:latest*.

    toolearn toocreate un database Oracle, vedere hello [Oracle creare avvio rapido database](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Passaggio 2: Connettere toohello VM

*   toocreate una sessione di Secure Shell (SSH) con hello macchina virtuale, utilizzare hello comando seguente. Sostituire l'indirizzo IP hello e combinazione di nome host hello con hello `publicIpAddress` valore per la macchina virtuale.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Passaggio 3: Preparare i database di hello

1.  Questo passaggio presuppone che si abbia un'istanza di Oracle, cdb1, in esecuzione in una macchina virtuale denominata *myVM*.

    Eseguire hello *oracle* radice utente avanzato e inizializzare listener di hello:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  (Facoltativo) Verificare che il database di hello sia in modalità di archiviazione del log:

    ```bash
    $ sqlplus / as sysdba
    SQL> SELECT log_mode FROM v$database;

    LOG_MODE
    ------------
    NOARCHIVELOG

    SQL> SHUTDOWN IMMEDIATE;
    SQL> STARTUP MOUNT;
    SQL> ALTER DATABASE ARCHIVELOG;
    SQL> ALTER DATABASE OPEN;
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  (Facoltativo) Creare un commit hello tootest di tabella:

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  Verificare o modificare le dimensioni e posizione di file di backup hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Utilizzare Oracle gestione del ripristino (RMAN) tooback backup database hello:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Passaggio 4: Backup coerente con l'applicazione per le macchine virtuali Linux

I backup coerenti con l'applicazione sono una nuova funzionalità di Backup di Azure. È possibile creare e selezionare tooexecute script prima e dopo snapshot di macchina virtuale hello (pre-snapshot e post-snapshot).

1. Scaricare il file JSON hello.

    Scaricare VMSnapshotScriptPluginConfig.json da https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. contenuto del file Hello un aspetto simile toohello seguenti:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. Crea cartella /etc/azure hello in hello VM:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Copiare i file JSON hello.

    Copia VMSnapshotScriptPluginConfig.json toohello /etc/azure cartella.

4. Modificare il file JSON hello.

    Modifica hello di hello VMSnapshotScriptPluginConfig.json file tooinclude `PreScriptLocation` e `PostScriptlocation` parametri. ad esempio:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. Creare hello file script di pre-snapshot e post-snapshot.

    Ecco un esempio di script di pre-snapshot e post-snapshot per un "backup a freddo", un backup offline, con arresto e riavvio:

    Per /etc/azure/pre_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Per /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Ecco un esempio di script di pre-snapshot e post-snapshot per un "backup a caldo", un backup online:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Per /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Per /etc/azure/pre_script.sql, modificare il contenuto di hello del file hello base alle esigenze:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    Per /etc/azure/post_script.sql, modificare il contenuto di hello del file hello base alle esigenze:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Modificare le autorizzazioni del file:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Hello script di test.

    script di hello tootest, prima di tutto, Accedi come radice. Assicurarsi quindi che non ci siano errori:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Per altre informazioni, vedere [Backup coerente delle applicazioni per le macchine virtuali Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Passaggio 5: Utilizzare servizi di ripristino di Azure insiemi di credenziali tooback backup hello VM

1.  Nel portale di Azure hello, cercare **insiemi di credenziali di servizi di ripristino**.

    ![Pagina degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_01.png)

2.  In hello **insiemi di credenziali di servizi di ripristino** pannello tooadd un nuovo insieme di credenziali, fare clic su **Aggiungi**.

    ![Pagina di aggiunta degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, fare clic su **myVault**.

    ![Pagina di dettaglio degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_03.png)

4.  In hello **myVault** pannello, fare clic su **Backup**.

    ![Pagina di backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_04.png)

5.  In hello **Backup obiettivo** valori predefiniti di hello uso del pannello **Azure** e **macchina virtuale**. Fare clic su **OK**.

    ![Pagina di dettaglio degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Per **Criterio di backup** usare **DefaultPolicy** o selezionare **Crea un nuovo criterio**. Fare clic su **OK**.

    ![Pagina di dettaglio dei criteri di backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_06.png)

7.  In hello **selezionare le macchine virtuali** blade, seleziona hello **myVM1** casella di controllo e quindi fare clic su **OK**. Fare clic su hello **Abilita backup** pulsante.

    ![Pagina dei dettagli backup toohello ripristino Services insiemi di credenziali per gli elementi](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Dopo aver fatto clic **Abilita backup**, processo di backup hello non viene avviato finché non scade hello ora pianificata. tooset di un backup immediato completo hello passaggio successivo.

8.  In hello **myVault - elementi di Backup** pannello, in **Conteggio elementi di BACKUP**, selezionare il numero di backup dell'elemento hello.

    ![Pagina di dettaglio degli insiemi di credenziali myVault dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_08.png)

9.  In hello **gli elementi di Backup (macchina virtuale di Azure)** pannello hello destra della pagina di hello, fare clic sui puntini di sospensione hello (**...** ) pulsante e quindi fare clic su **Backup ora**.

    ![Comando Backup now (Esegui il backup ora) degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_09.png)

10. Fare clic su hello **Backup** pulsante. Attendere hello toofinish di processo di backup. Quindi, passare troppo[passaggio 6: rimuovere i file di database hello](#step-6-remove-the-database-files).

    stato hello tooview hello del processo di backup, fare clic su **processi**.

    ![Pagina dei processi degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_10.png)

    stato di Hello hello del processo di backup viene visualizzato nella seguente immagine hello:

    ![Pagina dei processi degli insiemi di credenziali dei servizi di ripristino con stato](./media/oracle-backup-recovery/recovery_service_11.png)

11. Per un backup coerente con l'applicazione, risolvere gli eventuali errori nel file di log hello. file di log di Hello si trova in /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Passaggio 6: Rimuovere i file di database hello 
Più avanti in questo articolo si apprenderà come tootest hello il processo di ripristino. Prima di testare il processo di ripristino di hello, si dispone di file di database tooremove hello.

1.  Rimuovere i file di backup e spazio tabelle hello:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Facoltativo) Arrestare l'istanza di Oracle hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Ripristinare file eliminato hello da hello che insiemi di credenziali di servizi di ripristino
hello toorestore eliminato file, hello completo alla procedura seguente:

1. Nel portale di Azure hello, cercare hello *myVault* elemento insiemi di credenziali di servizi di ripristino. In hello **Panoramica** pannello, in **Backup elementi**, selezionare hello numero di elementi.

    ![Elementi di backup myVault degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_12.png)

2. In **Conteggio elementi di BACKUP**, selezionare hello numero di elementi.

    ![Numero di elementi di backup di macchine virtuali di Azure in insiemi di credenziali di servizi di ripristino](./media/oracle-backup-recovery/recovery_service_13.png)

3. In hello **myvm1** pannello, fare clic su **il ripristino di File (anteprima)**.

    ![Schermata di hello servizi di ripristino di insiemi di credenziali di pagina di ripristino di file](./media/oracle-backup-recovery/recovery_service_14.png)

4. In hello **il ripristino di File (anteprima)** riquadro, fare clic su **Download Script**. Quindi, è possibile salvare cartella tooa file di download (SH) hello in computer client hello.

    ![Opzioni di salvataggio e download del file di script](./media/oracle-backup-recovery/recovery_service_15.png)

5. Copiare hello sh file toohello macchina virtuale.

    Hello di esempio seguente viene illustrato come si toouse un toomove di comando di copia sicuro (scp) hello toohello file macchina virtuale. È inoltre possibile copiare negli Appunti di toohello contenuto hello e quindi incollare hello contenuto in un nuovo file in cui è installato nella macchina virtuale hello.

    > [!IMPORTANT]
    > Nell'esempio seguente di hello, assicurarsi di aggiornare i valori di indirizzo e la cartella IP hello. i valori Hello devono eseguire il mapping toohello cartella in cui è salvato il file hello.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Modificare il file di hello, in modo che appartiene a una radice di hello.

    Nell'esempio seguente di hello, modificare il file di hello in modo che appartiene a una radice di hello. Modificare quindi le autorizzazioni.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Hello esempio seguente viene illustrato ciò che viene visualizzato dopo aver eseguito hello script precedente. Quando viene chiesto di toocontinue, immettere **Y**.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. Accedere a volumi montato toohello viene confermata.

    tooexit, immettere **q**e quindi cercare volumi montato hello. aggiunta di un elenco di hello volumi, al prompt dei comandi, immettere toocreate **df -k**.

    ![comando di Hello df -k](./media/oracle-backup-recovery/recovery_service_16.png)

8. Hello utilizzare seguenti script toocopy hello mancante file toohello indietro cartelle:

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. In hello lo script seguente, è possibile utilizzare database di hello toorecover RMAN:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Smontare il disco di hello.

    Nel portale di Azure su hello hello **il ripristino di File (anteprima)** pannello, fare clic su **smontare dischi**.

    ![Comando Unmount disks](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Ripristinare hello intera macchina virtuale

Anziché ripristinare file eliminato hello dagli archivi di hello servizi di ripristino, è possibile ripristinare hello intera macchina virtuale.

### <a name="step-1-delete-myvm"></a>Passaggio 1: Eliminare myVM

*   Nel portale di Azure hello, passare toohello **myVM1** insieme di credenziali e quindi selezionare **eliminare**.

    ![Comando Elimina insieme di credenziali](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Passaggio 2: Recuperare hello VM

1.  Andare troppo**insiemi di credenziali di servizi di ripristino**, quindi selezionare **myVault**.

    ![voce myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  In hello **Panoramica** pannello, in **Backup elementi**, selezionare hello numero di elementi.

    ![elementi di backup myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  In hello **gli elementi di Backup (macchina virtuale di Azure)** pannello seleziona **myvm1**.

    ![Pagina di ripristino della macchina virtuale](./media/oracle-backup-recovery/recover_vm_04.png)

4.  In hello **myvm1** pannello, fare clic sui puntini di sospensione hello (**...** ) pulsante e quindi fare clic su **ripristinare VM**.

    ![Comando Ripristina macchina virtuale](./media/oracle-backup-recovery/recover_vm_05.png)

5.  In hello **punto di ripristino selezionare** blade, elemento selezionare hello che desidera toorestore e quindi fare clic su **OK**.

    ![Punto di ripristino selezionare hello](./media/oracle-backup-recovery/recover_vm_06.png)

    Se è stato abilitato il backup coerente con l'applicazione, viene visualizzata una barra verticale di colore blu.

6.  In hello **ripristino configurazione** pannello, nome della macchina virtuale selezionare hello, selezionare il gruppo di risorse hello e quindi fare clic su **OK**.

    ![Valori di configurazione del ripristino](./media/oracle-backup-recovery/recover_vm_07.png)

7.  hello toorestore macchina virtuale, fare clic su hello **ripristinare** pulsante.

8.  stato hello tooview hello del processo di ripristino, fare clic su **processi**, quindi fare clic su **i processi di Backup**.

    ![Comando dello stato dei processi di backup](./media/oracle-backup-recovery/recover_vm_08.png)

    Hello figura riportata di seguito viene illustrato hello stato del processo di ripristino hello:

    ![Stato del processo di ripristino hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Passaggio 3: Impostare l'indirizzo IP pubblico hello
Dopo aver hello che VM viene ripristinato, impostare l'indirizzo IP pubblico hello.

1.  Nella casella di ricerca hello, immettere **indirizzo IP pubblico**.

    ![Elenco degli indirizzi IP pubblici](./media/oracle-backup-recovery/create_ip_00.png)

2.  In hello **gli indirizzi IP pubblici** pannello, fare clic su **Aggiungi**. In hello **creare l'indirizzo IP pubblico** pannello per **nome**, selezionare il nome IP pubblico di hello. Per **Gruppo di risorse** selezionare **Usa esistente**. Fare quindi clic su **Crea**.

    ![Creare un indirizzo IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate hello indirizzo IP pubblico con l'interfaccia di rete hello per hello macchina virtuale, eseguire la ricerca per e selezionare **myVMip**. Quindi fare clic su **Associa**.

    ![Associare l'indirizzo IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  Per **Tipo di risorsa** selezionare **Interfaccia di rete**. Selezionare l'interfaccia di rete hello utilizzato dall'istanza di macchina virtuale myVM hello e quindi fare clic su **OK**.

    ![Selezionare i valori Tipo di risorsa e Interfaccia di rete](./media/oracle-backup-recovery/create_ip_03.png)

5.  Cercare e aprire l'istanza hello myVM che viene trasferita dal portale hello. Hello indirizzo IP associato hello VM è presente nella macchina virtuale myVM hello **Panoramica** blade.

    ![Valore dell'indirizzo IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Passaggio 4: Connettere toohello VM

*   tooconnect toohello macchina virtuale, utilizzare hello lo script seguente:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Passaggio 5: Verificare se il database hello è accessibile
*   accessibilità tootest, hello utilizzare lo script seguente:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Se hello database **avvio** comando genera un errore, il database di hello toorecover, vedere [passaggio 6: database di hello usare RMAN toorecover](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Passaggio 6: Database (facoltativo) usare RMAN toorecover hello
*   database di hello toorecover, hello utilizzare lo script seguente:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

Hello backup e ripristino dei database 12C Database Oracle di hello in una macchina virtuale Linux di Azure è ora completato.

## <a name="delete-hello-vm"></a>Eliminare hello VM

Quando si non è più necessario hello VM, è possibile utilizzare hello seguente gruppo di risorse di comando tooremove hello, hello VM e tutte le relative risorse:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

[Esercitazione: Creare VM a disponibilità elevata](../../linux/create-cli-complete.md)

[Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM](../../linux/cli-samples.md)



