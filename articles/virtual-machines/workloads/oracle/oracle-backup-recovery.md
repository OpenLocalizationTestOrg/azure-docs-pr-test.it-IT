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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="502b7-103">Eseguire backup e ripristino di un database Oracle Database 12c in una macchina virtuale Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="502b7-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="502b7-104">Si può utilizzare toocreate CLI di Azure e gestire risorse di Azure a un prompt dei comandi o utilizzare gli script.</span><span class="sxs-lookup"><span data-stu-id="502b7-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="502b7-105">In questo articolo, si usa Azure CLI script toodeploy un database di Oracle Database 12C da un'immagine della raccolta di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="502b7-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="502b7-106">Prima di iniziare, assicurarsi che l'interfaccia della riga di comando di Azure sia installata.</span><span class="sxs-lookup"><span data-stu-id="502b7-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="502b7-107">Per ulteriori informazioni, vedere hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="502b7-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="502b7-108">Preparare l'ambiente hello</span><span class="sxs-lookup"><span data-stu-id="502b7-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="502b7-109">Passaggio 1: Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="502b7-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="502b7-110">processo di backup e ripristino di hello tooperform, è innanzitutto necessario creare una VM Linux con un'istanza installata di Oracle Database 12C.</span><span class="sxs-lookup"><span data-stu-id="502b7-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="502b7-111">immagine del Marketplace Hello è utilizzare hello toocreate VM è denominato *Oracle: Oracle-Database-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="502b7-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="502b7-112">toolearn toocreate un database Oracle, vedere hello [Oracle creare avvio rapido database](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="502b7-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="502b7-113">Passaggio 2: Connettere toohello VM</span><span class="sxs-lookup"><span data-stu-id="502b7-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="502b7-114">toocreate una sessione di Secure Shell (SSH) con hello macchina virtuale, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="502b7-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="502b7-115">Sostituire l'indirizzo IP hello e combinazione di nome host hello con hello `publicIpAddress` valore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="502b7-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="502b7-116">Passaggio 3: Preparare i database di hello</span><span class="sxs-lookup"><span data-stu-id="502b7-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="502b7-117">Questo passaggio presuppone che si abbia un'istanza di Oracle, cdb1, in esecuzione in una macchina virtuale denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="502b7-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="502b7-118">Eseguire hello *oracle* radice utente avanzato e inizializzare listener di hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

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

2.  <span data-ttu-id="502b7-119">(Facoltativo) Verificare che il database di hello sia in modalità di archiviazione del log:</span><span class="sxs-lookup"><span data-stu-id="502b7-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="502b7-120">(Facoltativo) Creare un commit hello tootest di tabella:</span><span class="sxs-lookup"><span data-stu-id="502b7-120">(Optional) Create a table tootest hello commit:</span></span>

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
4.  <span data-ttu-id="502b7-121">Verificare o modificare le dimensioni e posizione di file di backup hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="502b7-122">Utilizzare Oracle gestione del ripristino (RMAN) tooback backup database hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="502b7-123">Passaggio 4: Backup coerente con l'applicazione per le macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="502b7-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="502b7-124">I backup coerenti con l'applicazione sono una nuova funzionalità di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="502b7-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="502b7-125">È possibile creare e selezionare tooexecute script prima e dopo snapshot di macchina virtuale hello (pre-snapshot e post-snapshot).</span><span class="sxs-lookup"><span data-stu-id="502b7-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="502b7-126">Scaricare il file JSON hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-126">Download hello JSON file.</span></span>

    <span data-ttu-id="502b7-127">Scaricare VMSnapshotScriptPluginConfig.json da https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="502b7-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="502b7-128">contenuto del file Hello un aspetto simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="502b7-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="502b7-129">Crea cartella /etc/azure hello in hello VM:</span><span class="sxs-lookup"><span data-stu-id="502b7-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="502b7-130">Copiare i file JSON hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="502b7-131">Copia VMSnapshotScriptPluginConfig.json toohello /etc/azure cartella.</span><span class="sxs-lookup"><span data-stu-id="502b7-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="502b7-132">Modificare il file JSON hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="502b7-133">Modifica hello di hello VMSnapshotScriptPluginConfig.json file tooinclude `PreScriptLocation` e `PostScriptlocation` parametri.</span><span class="sxs-lookup"><span data-stu-id="502b7-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="502b7-134">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="502b7-134">For example:</span></span>

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

5. <span data-ttu-id="502b7-135">Creare hello file script di pre-snapshot e post-snapshot.</span><span class="sxs-lookup"><span data-stu-id="502b7-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="502b7-136">Ecco un esempio di script di pre-snapshot e post-snapshot per un "backup a freddo", un backup offline, con arresto e riavvio:</span><span class="sxs-lookup"><span data-stu-id="502b7-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="502b7-137">Per /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="502b7-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="502b7-138">Per /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="502b7-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="502b7-139">Ecco un esempio di script di pre-snapshot e post-snapshot per un "backup a caldo", un backup online:</span><span class="sxs-lookup"><span data-stu-id="502b7-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="502b7-140">Per /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="502b7-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="502b7-141">Per /etc/azure/pre_script.sql, modificare il contenuto di hello del file hello base alle esigenze:</span><span class="sxs-lookup"><span data-stu-id="502b7-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="502b7-142">Per /etc/azure/post_script.sql, modificare il contenuto di hello del file hello base alle esigenze:</span><span class="sxs-lookup"><span data-stu-id="502b7-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="502b7-143">Modificare le autorizzazioni del file:</span><span class="sxs-lookup"><span data-stu-id="502b7-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="502b7-144">Hello script di test.</span><span class="sxs-lookup"><span data-stu-id="502b7-144">Test hello scripts.</span></span>

    <span data-ttu-id="502b7-145">script di hello tootest, prima di tutto, Accedi come radice.</span><span class="sxs-lookup"><span data-stu-id="502b7-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="502b7-146">Assicurarsi quindi che non ci siano errori:</span><span class="sxs-lookup"><span data-stu-id="502b7-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="502b7-147">Per altre informazioni, vedere [Backup coerente delle applicazioni per le macchine virtuali Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="502b7-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="502b7-148">Passaggio 5: Utilizzare servizi di ripristino di Azure insiemi di credenziali tooback backup hello VM</span><span class="sxs-lookup"><span data-stu-id="502b7-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="502b7-149">Nel portale di Azure hello, cercare **insiemi di credenziali di servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="502b7-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Pagina degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="502b7-151">In hello **insiemi di credenziali di servizi di ripristino** pannello tooadd un nuovo insieme di credenziali, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="502b7-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Pagina di aggiunta degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="502b7-153">toocontinue, fare clic su **myVault**.</span><span class="sxs-lookup"><span data-stu-id="502b7-153">toocontinue, click **myVault**.</span></span>

    ![Pagina di dettaglio degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="502b7-155">In hello **myVault** pannello, fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="502b7-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Pagina di backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="502b7-157">In hello **Backup obiettivo** valori predefiniti di hello uso del pannello **Azure** e **macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="502b7-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="502b7-158">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="502b7-158">Click **OK**.</span></span>

    ![Pagina di dettaglio degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="502b7-160">Per **Criterio di backup** usare **DefaultPolicy** o selezionare **Crea un nuovo criterio**.</span><span class="sxs-lookup"><span data-stu-id="502b7-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="502b7-161">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="502b7-161">Click **OK**.</span></span>

    ![Pagina di dettaglio dei criteri di backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="502b7-163">In hello **selezionare le macchine virtuali** blade, seleziona hello **myVM1** casella di controllo e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="502b7-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="502b7-164">Fare clic su hello **Abilita backup** pulsante.</span><span class="sxs-lookup"><span data-stu-id="502b7-164">Click hello **Enable backup** button.</span></span>

    ![Pagina dei dettagli backup toohello ripristino Services insiemi di credenziali per gli elementi](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="502b7-166">Dopo aver fatto clic **Abilita backup**, processo di backup hello non viene avviato finché non scade hello ora pianificata.</span><span class="sxs-lookup"><span data-stu-id="502b7-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="502b7-167">tooset di un backup immediato completo hello passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="502b7-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="502b7-168">In hello **myVault - elementi di Backup** pannello, in **Conteggio elementi di BACKUP**, selezionare il numero di backup dell'elemento hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Pagina di dettaglio degli insiemi di credenziali myVault dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="502b7-170">In hello **gli elementi di Backup (macchina virtuale di Azure)** pannello hello destra della pagina di hello, fare clic sui puntini di sospensione hello (**...** ) pulsante e quindi fare clic su **Backup ora**.</span><span class="sxs-lookup"><span data-stu-id="502b7-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Comando Backup now (Esegui il backup ora) degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="502b7-172">Fare clic su hello **Backup** pulsante.</span><span class="sxs-lookup"><span data-stu-id="502b7-172">Click hello **Backup** button.</span></span> <span data-ttu-id="502b7-173">Attendere hello toofinish di processo di backup.</span><span class="sxs-lookup"><span data-stu-id="502b7-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="502b7-174">Quindi, passare troppo[passaggio 6: rimuovere i file di database hello](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="502b7-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="502b7-175">stato hello tooview hello del processo di backup, fare clic su **processi**.</span><span class="sxs-lookup"><span data-stu-id="502b7-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Pagina dei processi degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="502b7-177">stato di Hello hello del processo di backup viene visualizzato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Pagina dei processi degli insiemi di credenziali dei servizi di ripristino con stato](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="502b7-179">Per un backup coerente con l'applicazione, risolvere gli eventuali errori nel file di log hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="502b7-180">file di log di Hello si trova in /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="502b7-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="502b7-181">Passaggio 6: Rimuovere i file di database hello</span><span class="sxs-lookup"><span data-stu-id="502b7-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="502b7-182">Più avanti in questo articolo si apprenderà come tootest hello il processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="502b7-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="502b7-183">Prima di testare il processo di ripristino di hello, si dispone di file di database tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="502b7-184">Rimuovere i file di backup e spazio tabelle hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="502b7-185">(Facoltativo) Arrestare l'istanza di Oracle hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="502b7-186">Ripristinare file eliminato hello da hello che insiemi di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="502b7-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="502b7-187">hello toorestore eliminato file, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="502b7-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="502b7-188">Nel portale di Azure hello, cercare hello *myVault* elemento insiemi di credenziali di servizi di ripristino.</span><span class="sxs-lookup"><span data-stu-id="502b7-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="502b7-189">In hello **Panoramica** pannello, in **Backup elementi**, selezionare hello numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="502b7-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Elementi di backup myVault degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="502b7-191">In **Conteggio elementi di BACKUP**, selezionare hello numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="502b7-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Numero di elementi di backup di macchine virtuali di Azure in insiemi di credenziali di servizi di ripristino](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="502b7-193">In hello **myvm1** pannello, fare clic su **il ripristino di File (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="502b7-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Schermata di hello servizi di ripristino di insiemi di credenziali di pagina di ripristino di file](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="502b7-195">In hello **il ripristino di File (anteprima)** riquadro, fare clic su **Download Script**.</span><span class="sxs-lookup"><span data-stu-id="502b7-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="502b7-196">Quindi, è possibile salvare cartella tooa file di download (SH) hello in computer client hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Opzioni di salvataggio e download del file di script](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="502b7-198">Copiare hello sh file toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="502b7-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="502b7-199">Hello di esempio seguente viene illustrato come si toouse un toomove di comando di copia sicuro (scp) hello toohello file macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="502b7-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="502b7-200">È inoltre possibile copiare negli Appunti di toohello contenuto hello e quindi incollare hello contenuto in un nuovo file in cui è installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="502b7-201">Nell'esempio seguente di hello, assicurarsi di aggiornare i valori di indirizzo e la cartella IP hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="502b7-202">i valori Hello devono eseguire il mapping toohello cartella in cui è salvato il file hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="502b7-203">Modificare il file di hello, in modo che appartiene a una radice di hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="502b7-204">Nell'esempio seguente di hello, modificare il file di hello in modo che appartiene a una radice di hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="502b7-205">Modificare quindi le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="502b7-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="502b7-206">Hello esempio seguente viene illustrato ciò che viene visualizzato dopo aver eseguito hello script precedente.</span><span class="sxs-lookup"><span data-stu-id="502b7-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="502b7-207">Quando viene chiesto di toocontinue, immettere **Y**.</span><span class="sxs-lookup"><span data-stu-id="502b7-207">When you're prompted toocontinue, enter **Y**.</span></span>

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

7. <span data-ttu-id="502b7-208">Accedere a volumi montato toohello viene confermata.</span><span class="sxs-lookup"><span data-stu-id="502b7-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="502b7-209">tooexit, immettere **q**e quindi cercare volumi montato hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="502b7-210">aggiunta di un elenco di hello volumi, al prompt dei comandi, immettere toocreate **df -k**.</span><span class="sxs-lookup"><span data-stu-id="502b7-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![comando di Hello df -k](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="502b7-212">Hello utilizzare seguenti script toocopy hello mancante file toohello indietro cartelle:</span><span class="sxs-lookup"><span data-stu-id="502b7-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="502b7-213">In hello lo script seguente, è possibile utilizzare database di hello toorecover RMAN:</span><span class="sxs-lookup"><span data-stu-id="502b7-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="502b7-214">Smontare il disco di hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-214">Unmount hello disk.</span></span>

    <span data-ttu-id="502b7-215">Nel portale di Azure su hello hello **il ripristino di File (anteprima)** pannello, fare clic su **smontare dischi**.</span><span class="sxs-lookup"><span data-stu-id="502b7-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Comando Unmount disks](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="502b7-217">Ripristinare hello intera macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="502b7-217">Restore hello entire VM</span></span>

<span data-ttu-id="502b7-218">Anziché ripristinare file eliminato hello dagli archivi di hello servizi di ripristino, è possibile ripristinare hello intera macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="502b7-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="502b7-219">Passaggio 1: Eliminare myVM</span><span class="sxs-lookup"><span data-stu-id="502b7-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="502b7-220">Nel portale di Azure hello, passare toohello **myVM1** insieme di credenziali e quindi selezionare **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="502b7-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Comando Elimina insieme di credenziali](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="502b7-222">Passaggio 2: Recuperare hello VM</span><span class="sxs-lookup"><span data-stu-id="502b7-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="502b7-223">Andare troppo**insiemi di credenziali di servizi di ripristino**, quindi selezionare **myVault**.</span><span class="sxs-lookup"><span data-stu-id="502b7-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![voce myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="502b7-225">In hello **Panoramica** pannello, in **Backup elementi**, selezionare hello numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="502b7-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![elementi di backup myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="502b7-227">In hello **gli elementi di Backup (macchina virtuale di Azure)** pannello seleziona **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="502b7-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Pagina di ripristino della macchina virtuale](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="502b7-229">In hello **myvm1** pannello, fare clic sui puntini di sospensione hello (**...** ) pulsante e quindi fare clic su **ripristinare VM**.</span><span class="sxs-lookup"><span data-stu-id="502b7-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Comando Ripristina macchina virtuale](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="502b7-231">In hello **punto di ripristino selezionare** blade, elemento selezionare hello che desidera toorestore e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="502b7-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Punto di ripristino selezionare hello](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="502b7-233">Se è stato abilitato il backup coerente con l'applicazione, viene visualizzata una barra verticale di colore blu.</span><span class="sxs-lookup"><span data-stu-id="502b7-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="502b7-234">In hello **ripristino configurazione** pannello, nome della macchina virtuale selezionare hello, selezionare il gruppo di risorse hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="502b7-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Valori di configurazione del ripristino](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="502b7-236">hello toorestore macchina virtuale, fare clic su hello **ripristinare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="502b7-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="502b7-237">stato hello tooview hello del processo di ripristino, fare clic su **processi**, quindi fare clic su **i processi di Backup**.</span><span class="sxs-lookup"><span data-stu-id="502b7-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Comando dello stato dei processi di backup](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="502b7-239">Hello figura riportata di seguito viene illustrato hello stato del processo di ripristino hello:</span><span class="sxs-lookup"><span data-stu-id="502b7-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Stato del processo di ripristino hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="502b7-241">Passaggio 3: Impostare l'indirizzo IP pubblico hello</span><span class="sxs-lookup"><span data-stu-id="502b7-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="502b7-242">Dopo aver hello che VM viene ripristinato, impostare l'indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="502b7-243">Nella casella di ricerca hello, immettere **indirizzo IP pubblico**.</span><span class="sxs-lookup"><span data-stu-id="502b7-243">In hello search box, enter **public IP address**.</span></span>

    ![Elenco degli indirizzi IP pubblici](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="502b7-245">In hello **gli indirizzi IP pubblici** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="502b7-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="502b7-246">In hello **creare l'indirizzo IP pubblico** pannello per **nome**, selezionare il nome IP pubblico di hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="502b7-247">Per **Gruppo di risorse** selezionare **Usa esistente**.</span><span class="sxs-lookup"><span data-stu-id="502b7-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="502b7-248">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="502b7-248">Then, click **Create**.</span></span>

    ![Creare un indirizzo IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="502b7-250">tooassociate hello indirizzo IP pubblico con l'interfaccia di rete hello per hello macchina virtuale, eseguire la ricerca per e selezionare **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="502b7-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="502b7-251">Quindi fare clic su **Associa**.</span><span class="sxs-lookup"><span data-stu-id="502b7-251">Then, click **Associate**.</span></span>

    ![Associare l'indirizzo IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="502b7-253">Per **Tipo di risorsa** selezionare **Interfaccia di rete**.</span><span class="sxs-lookup"><span data-stu-id="502b7-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="502b7-254">Selezionare l'interfaccia di rete hello utilizzato dall'istanza di macchina virtuale myVM hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="502b7-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Selezionare i valori Tipo di risorsa e Interfaccia di rete](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="502b7-256">Cercare e aprire l'istanza hello myVM che viene trasferita dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="502b7-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="502b7-257">Hello indirizzo IP associato hello VM è presente nella macchina virtuale myVM hello **Panoramica** blade.</span><span class="sxs-lookup"><span data-stu-id="502b7-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![Valore dell'indirizzo IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="502b7-259">Passaggio 4: Connettere toohello VM</span><span class="sxs-lookup"><span data-stu-id="502b7-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="502b7-260">tooconnect toohello macchina virtuale, utilizzare hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="502b7-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="502b7-261">Passaggio 5: Verificare se il database hello è accessibile</span><span class="sxs-lookup"><span data-stu-id="502b7-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="502b7-262">accessibilità tootest, hello utilizzare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="502b7-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="502b7-263">Se hello database **avvio** comando genera un errore, il database di hello toorecover, vedere [passaggio 6: database di hello usare RMAN toorecover](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="502b7-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="502b7-264">Passaggio 6: Database (facoltativo) usare RMAN toorecover hello</span><span class="sxs-lookup"><span data-stu-id="502b7-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="502b7-265">database di hello toorecover, hello utilizzare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="502b7-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="502b7-266">Hello backup e ripristino dei database 12C Database Oracle di hello in una macchina virtuale Linux di Azure è ora completato.</span><span class="sxs-lookup"><span data-stu-id="502b7-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="502b7-267">Eliminare hello VM</span><span class="sxs-lookup"><span data-stu-id="502b7-267">Delete hello VM</span></span>

<span data-ttu-id="502b7-268">Quando si non è più necessario hello VM, è possibile utilizzare hello seguente gruppo di risorse di comando tooremove hello, hello VM e tutte le relative risorse:</span><span class="sxs-lookup"><span data-stu-id="502b7-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="502b7-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="502b7-269">Next steps</span></span>

[<span data-ttu-id="502b7-270">Esercitazione: Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="502b7-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="502b7-271">Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="502b7-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



