---
title: Eseguire backup e ripristino di un database Oracle Database 12c in una macchina virtuale Linux di Azure | Microsoft Docs
description: Informazioni su come eseguire rapidamente backup e ripristino di un database Oracle Database 12c nell'ambiente Azure.
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
ms.openlocfilehash: 9a2293f13b90e9a4cb11b4169fad969dd622a9a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="3dd26-103">Eseguire backup e ripristino di un database Oracle Database 12c in una macchina virtuale Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="3dd26-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="3dd26-104">È possibile usare l'interfaccia della riga di comando di Azure per creare e gestire risorse di Azure a un prompt dei comandi o per creare script.</span><span class="sxs-lookup"><span data-stu-id="3dd26-104">You can use Azure CLI to create and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="3dd26-105">In questo articolo vengono usati script dell'interfaccia della riga di comando di Azure per distribuire un database Oracle Database 12c da un'immagine della raccolta di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3dd26-105">In this article, we use Azure CLI scripts to deploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="3dd26-106">Prima di iniziare, assicurarsi che l'interfaccia della riga di comando di Azure sia installata.</span><span class="sxs-lookup"><span data-stu-id="3dd26-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="3dd26-107">Per altre informazioni, consultare la [guida all'installazione dell'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3dd26-107">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="3dd26-108">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="3dd26-108">Prepare the environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="3dd26-109">Passaggio 1: Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3dd26-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="3dd26-110">Per eseguire il processo di backup e ripristino, è necessario innanzitutto creare una macchina virtuale Linux con un'istanza installata di Oracle Database 12c.</span><span class="sxs-lookup"><span data-stu-id="3dd26-110">To perform the backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="3dd26-111">L'immagine di Marketplace usata per creare la macchina virtuale viene denominata *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="3dd26-111">The Marketplace image you use to create the VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="3dd26-112">Per informazioni su come creare un database Oracle, vedere [Creare un database Oracle Database](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="3dd26-112">To learn how to create an Oracle database, see the [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-to-the-vm"></a><span data-ttu-id="3dd26-113">Passaggio 2: Eseguire la connessione alla VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-113">Step 2: Connect to the VM</span></span>

*   <span data-ttu-id="3dd26-114">Per creare una sessione Secure Shell, SSH con la macchina virtuale, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="3dd26-114">To create a Secure Shell (SSH) session with the VM, use the following command.</span></span> <span data-ttu-id="3dd26-115">Sostituire l'indirizzo IP e la combinazione di nome host con il valore `publicIpAddress` per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3dd26-115">Replace the IP address and the host name combination with the `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-the-database"></a><span data-ttu-id="3dd26-116">Passaggio 3: Preparare il database</span><span class="sxs-lookup"><span data-stu-id="3dd26-116">Step 3: Prepare the database</span></span>

1.  <span data-ttu-id="3dd26-117">Questo passaggio presuppone che si abbia un'istanza di Oracle, cdb1, in esecuzione in una macchina virtuale denominata *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3dd26-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="3dd26-118">Usare la radice del superuser *oracle* e inizializzare il listener:</span><span class="sxs-lookup"><span data-stu-id="3dd26-118">Run the *oracle* superuser root, and then initialize the listener:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="3dd26-119">Assicurarsi che il database sia in modalità di log di archiviazione (facoltativo):</span><span class="sxs-lookup"><span data-stu-id="3dd26-119">(Optional) Make sure the database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="3dd26-120">Creare una tabella per testare il commit (facoltativo):</span><span class="sxs-lookup"><span data-stu-id="3dd26-120">(Optional) Create a table to test the commit:</span></span>

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session to scott;
    Grant succeeded.
    SQL> grant create table to scott;
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
4.  <span data-ttu-id="3dd26-121">Verificare o modificare il percorso e le dimensioni del file di backup:</span><span class="sxs-lookup"><span data-stu-id="3dd26-121">Verify or change the backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="3dd26-122">Usare Oracle Recovery Manager (RMAN) per il backup del database:</span><span class="sxs-lookup"><span data-stu-id="3dd26-122">Use Oracle Recovery Manager (RMAN) to back up the database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="3dd26-123">Passaggio 4: Backup coerente con l'applicazione per le macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="3dd26-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="3dd26-124">I backup coerenti con l'applicazione sono una nuova funzionalità di Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd26-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="3dd26-125">È possibile creare e selezionare gli script da eseguire prima e dopo lo snapshot della macchina virtuale, ovvero pre-snapshot e post-snapshot.</span><span class="sxs-lookup"><span data-stu-id="3dd26-125">You can create and select scripts to execute before and after the VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="3dd26-126">Scaricare il file JSON.</span><span class="sxs-lookup"><span data-stu-id="3dd26-126">Download the JSON file.</span></span>

    <span data-ttu-id="3dd26-127">Scaricare VMSnapshotScriptPluginConfig.json da https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="3dd26-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="3dd26-128">Il contenuto del file dovrebbe essere simile a quello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3dd26-128">The file contents look similar to the following:</span></span>

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

2. <span data-ttu-id="3dd26-129">Creare la cartella /etc/azure nella macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="3dd26-129">Create the /etc/azure folder on the VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="3dd26-130">Copiare il file JSON.</span><span class="sxs-lookup"><span data-stu-id="3dd26-130">Copy the JSON file.</span></span>

    <span data-ttu-id="3dd26-131">Copiare il file VMSnapshotScriptPluginConfig.json nella cartella /etc/azure.</span><span class="sxs-lookup"><span data-stu-id="3dd26-131">Copy VMSnapshotScriptPluginConfig.json to the /etc/azure folder.</span></span>

4. <span data-ttu-id="3dd26-132">Modificare il file JSON.</span><span class="sxs-lookup"><span data-stu-id="3dd26-132">Edit the JSON file.</span></span>

    <span data-ttu-id="3dd26-133">Modificare il file VMSnapshotScriptPluginConfig.json per includere i parametri `PreScriptLocation` e `PostScriptlocation`.</span><span class="sxs-lookup"><span data-stu-id="3dd26-133">Edit the VMSnapshotScriptPluginConfig.json file to include the `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="3dd26-134">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="3dd26-134">For example:</span></span>

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

5. <span data-ttu-id="3dd26-135">Creare file di script di pre-snapshot e post-snapshot.</span><span class="sxs-lookup"><span data-stu-id="3dd26-135">Create the pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="3dd26-136">Ecco un esempio di script di pre-snapshot e post-snapshot per un "backup a freddo", un backup offline, con arresto e riavvio:</span><span class="sxs-lookup"><span data-stu-id="3dd26-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="3dd26-137">Per /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="3dd26-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="3dd26-138">Per /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="3dd26-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="3dd26-139">Ecco un esempio di script di pre-snapshot e post-snapshot per un "backup a caldo", un backup online:</span><span class="sxs-lookup"><span data-stu-id="3dd26-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="3dd26-140">Per /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="3dd26-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="3dd26-141">Per /etc/azure/pre_script.sql, è necessario modificare il contenuto del file in base ai requisiti:</span><span class="sxs-lookup"><span data-stu-id="3dd26-141">For /etc/azure/pre_script.sql, modify the contents of the file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="3dd26-142">Per /etc/azure/post_script.sql, è necessario modificare il contenuto del file in base ai requisiti:</span><span class="sxs-lookup"><span data-stu-id="3dd26-142">For /etc/azure/post_script.sql, modify the contents of the file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="3dd26-143">Modificare le autorizzazioni del file:</span><span class="sxs-lookup"><span data-stu-id="3dd26-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="3dd26-144">Testare gli script.</span><span class="sxs-lookup"><span data-stu-id="3dd26-144">Test the scripts.</span></span>

    <span data-ttu-id="3dd26-145">Per testare gli script accedere innanzitutto come radice.</span><span class="sxs-lookup"><span data-stu-id="3dd26-145">To test the scripts, first, sign in as root.</span></span> <span data-ttu-id="3dd26-146">Assicurarsi quindi che non ci siano errori:</span><span class="sxs-lookup"><span data-stu-id="3dd26-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="3dd26-147">Per altre informazioni, vedere [Backup coerente delle applicazioni per le macchine virtuali Linux](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="3dd26-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-to-back-up-the-vm"></a><span data-ttu-id="3dd26-148">Passaggio 5: Usare gli insiemi di credenziali dei servizi di ripristino di Azure per eseguire il backup della VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-148">Step 5: Use Azure Recovery Services vaults to back up the VM</span></span>

1.  <span data-ttu-id="3dd26-149">Nel portale di Azure cercare gli **insiemi di credenziali di Servizi di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-149">In the Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Pagina degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="3dd26-151">Nel pannello **Insiemi di credenziali dei servizi di ripristino** fare clic su **Aggiungi** per aggiungere un nuovo insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="3dd26-151">On the **Recovery Services vaults** blade, to add a new vault, click **Add**.</span></span>

    ![Pagina di aggiunta degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="3dd26-153">Per continuare, fare clic su **myVault**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-153">To continue, click **myVault**.</span></span>

    ![Pagina di dettaglio degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="3dd26-155">Nel pannello **myVault** fare clic su **Backup**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-155">On the **myVault** blade, click **Backup**.</span></span>

    ![Pagina di backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="3dd26-157">Nel pannello **Obiettivo del backup** usare i valori predefiniti **Azure** e **Macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-157">On the **Backup Goal** blade, use the default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="3dd26-158">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-158">Click **OK**.</span></span>

    ![Pagina di dettaglio degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="3dd26-160">Per **Criterio di backup** usare **DefaultPolicy** o selezionare **Crea un nuovo criterio**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="3dd26-161">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-161">Click **OK**.</span></span>

    ![Pagina di dettaglio dei criteri di backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="3dd26-163">Nel pannello **Seleziona macchine virtuali** selezionare la casella di controllo **myVM1** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-163">On the **Select virtual machines** blade, select the **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="3dd26-164">Fare clic sul pulsante **Abilita backup**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-164">Click the **Enable backup** button.</span></span>

    ![Pagina di dettaglio degli elementi per il backup degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="3dd26-166">Dopo aver fatto clic su **Abilita backup**, il processo di backup non viene avviato fino all'orario pianificato.</span><span class="sxs-lookup"><span data-stu-id="3dd26-166">After you click **Enable backup**, the backup process doesn't start until the scheduled time expires.</span></span> <span data-ttu-id="3dd26-167">Per configurare un backup immediato, completare il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="3dd26-167">To set up an immediate backup, complete the next step.</span></span>

8.  <span data-ttu-id="3dd26-168">Nel pannello **myVault - Elementi di backup** in **CONTEGGIO DEGLI ELEMENTI DI BACKUP** selezionare il numero di backup degli elementi.</span><span class="sxs-lookup"><span data-stu-id="3dd26-168">On the **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select the backup item count.</span></span>

    ![Pagina di dettaglio degli insiemi di credenziali myVault dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="3dd26-170">Nel pannello **Backup Items (Azure Virtual Machine)** (Elementi di backup: macchina virtuale di Azure), sul lato destro della pagina, fare clic sui puntini di sospensione (**...**) e su **Backup now** (Esegui il backup ora).</span><span class="sxs-lookup"><span data-stu-id="3dd26-170">On the **Backup Items (Azure Virtual Machine)** blade, on the right side of the page, click the ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Comando Backup now (Esegui il backup ora) degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="3dd26-172">Fare clic sul pulsante **Backup**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-172">Click the **Backup** button.</span></span> <span data-ttu-id="3dd26-173">Attendere il completamento del processo di backup.</span><span class="sxs-lookup"><span data-stu-id="3dd26-173">Wait for the backup process to finish.</span></span> <span data-ttu-id="3dd26-174">Quindi passare al [passaggio 6: Rimuovere i file di database](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="3dd26-174">Then, go to [Step 6: Remove the database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="3dd26-175">Per visualizzare lo stato del processo di backup, fare clic su **Processi**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-175">To view the status of the backup job, click **Jobs**.</span></span>

    ![Pagina dei processi degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="3dd26-177">Lo stato del processo di backup viene visualizzato nella figura seguente:</span><span class="sxs-lookup"><span data-stu-id="3dd26-177">The status of the backup job appears in the following image:</span></span>

    ![Pagina dei processi degli insiemi di credenziali dei servizi di ripristino con stato](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="3dd26-179">Per un backup coerente con l'applicazione, risolvere gli eventuali errori nel file di log.</span><span class="sxs-lookup"><span data-stu-id="3dd26-179">For an application-consistent backup, address any errors in the log file.</span></span> <span data-ttu-id="3dd26-180">Il file di log si trova in /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="3dd26-180">The log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-the-database-files"></a><span data-ttu-id="3dd26-181">Passaggio 6: Rimuovere i file di database</span><span class="sxs-lookup"><span data-stu-id="3dd26-181">Step 6: Remove the database files</span></span> 
<span data-ttu-id="3dd26-182">Più avanti in questo articolo verrà illustrato come testare il processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3dd26-182">Later in this article, you'll learn how to test the recovery process.</span></span> <span data-ttu-id="3dd26-183">Prima di testare il processo di ripristino, è necessario rimuovere i file di database.</span><span class="sxs-lookup"><span data-stu-id="3dd26-183">Before you can test the recovery process, you have to remove the database files.</span></span>

1.  <span data-ttu-id="3dd26-184">Rimuovere lo spazio di tabella e i file di backup:</span><span class="sxs-lookup"><span data-stu-id="3dd26-184">Remove the tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="3dd26-185">Arrestare l'istanza di Oracle (facoltativo):</span><span class="sxs-lookup"><span data-stu-id="3dd26-185">(Optional) Shut down the Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-the-deleted-files-from-the-recovery-services-vaults"></a><span data-ttu-id="3dd26-186">Ripristinare i file eliminati dagli insiemi di credenziali dei servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="3dd26-186">Restore the deleted files from the Recovery Services vaults</span></span>
<span data-ttu-id="3dd26-187">Per ripristinare i file eliminati, completare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3dd26-187">To restore the deleted files, complete the following steps:</span></span>

1. <span data-ttu-id="3dd26-188">Nel portale di Azure e cercare l'elemento degli insiemi di credenziali dei servizi di ripristino *myVault*.</span><span class="sxs-lookup"><span data-stu-id="3dd26-188">In the Azure portal, search for the *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="3dd26-189">Nel pannello **Panoramica** in **Elementi di backup** selezionare il numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="3dd26-189">On the **Overview** blade, under **Backup items**, select the number of items.</span></span>

    ![Elementi di backup myVault degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="3dd26-191">In **CONTEGGIO DEGLI ELEMENTI DI BACKUP** fare clic sul numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="3dd26-191">Under **BACKUP ITEM COUNT**, select the number of items.</span></span>

    ![Numero di elementi di backup di macchine virtuali di Azure in insiemi di credenziali di servizi di ripristino](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="3dd26-193">Nel pannello **myvm1** fare clic su **Ripristino di file (anteprima)**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-193">On the **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Schermata della pagina di ripristino dei file degli insiemi di credenziali dei servizi di ripristino](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="3dd26-195">Nel riquadro **Ripristino di file (anteprima)** fare clic su **Scarica script**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-195">On the **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="3dd26-196">Quindi, salvare il file di download con estensione SH in una cartella nel computer client.</span><span class="sxs-lookup"><span data-stu-id="3dd26-196">Then, save the download (.sh) file to a folder on the client computer.</span></span>

    ![Opzioni di salvataggio e download del file di script](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="3dd26-198">Copiare il file con estensione sh nella VM.</span><span class="sxs-lookup"><span data-stu-id="3dd26-198">Copy the .sh file to the VM.</span></span>

    <span data-ttu-id="3dd26-199">Nell'esempio seguente viene illustrato come usare un comando di copia di sicurezza (scp) per spostare il file nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3dd26-199">The following example shows how you to use a secure copy (scp) command to move the file to the VM.</span></span> <span data-ttu-id="3dd26-200">È possibile anche copiare il contenuto negli Appunti e incollarlo in un nuovo file configurato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3dd26-200">You also can copy the contents to the clipboard, and then paste the contents in a new file that is set up on the VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3dd26-201">Nell'esempio seguente assicurarsi di aggiornare i valori dell'indirizzo IP e della cartella.</span><span class="sxs-lookup"><span data-stu-id="3dd26-201">In the following example, ensure that you update the IP address and folder values.</span></span> <span data-ttu-id="3dd26-202">I valori devono corrispondere a quelli della cartella in cui è stato salvato il file.</span><span class="sxs-lookup"><span data-stu-id="3dd26-202">The values must map to the folder where the file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="3dd26-203">Modificare il file in modo che appartenga alla radice.</span><span class="sxs-lookup"><span data-stu-id="3dd26-203">Change the file, so that it's owned by the root.</span></span>

    <span data-ttu-id="3dd26-204">Nell'esempio seguente modificare il file in modo che appartenga a una radice.</span><span class="sxs-lookup"><span data-stu-id="3dd26-204">In the following example, change the file so that it's owned by the root.</span></span> <span data-ttu-id="3dd26-205">Modificare quindi le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="3dd26-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="3dd26-206">L'esempio seguente illustra ciò che dovrebbe venire visualizzato dopo aver eseguito lo script precedente.</span><span class="sxs-lookup"><span data-stu-id="3dd26-206">The following example shows what you should see after you run the preceding script.</span></span> <span data-ttu-id="3dd26-207">Quando viene chiesto di continuare, immettere **Y**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-207">When you're prompted to continue, enter **Y**.</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    The script requires 'open-iscsi' and 'lshw' to run.
    Do you want us to install 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' to continue with installation, 'N' to abort the operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting to recovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of the recovery point to this machine...

    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

7. <span data-ttu-id="3dd26-208">L'accesso ai volumi montati è stato confermato.</span><span class="sxs-lookup"><span data-stu-id="3dd26-208">Access to the mounted volumes is confirmed.</span></span>

    <span data-ttu-id="3dd26-209">Per uscire, immettere **q** e cercare i volumi montati.</span><span class="sxs-lookup"><span data-stu-id="3dd26-209">To exit, enter **q**, and then search for the mounted volumes.</span></span> <span data-ttu-id="3dd26-210">Per creare un elenco dei volumi aggiunti, a un prompt dei comandi, immettere **df -k**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-210">To create a list of the added volumes, at a command prompt, enter **df -k**.</span></span>

    ![Comando df-k](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="3dd26-212">Usare lo script seguente per copiare nuovamente i file mancanti nelle cartelle:</span><span class="sxs-lookup"><span data-stu-id="3dd26-212">Use the following script to copy the missing files back to the folders:</span></span>

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
9. <span data-ttu-id="3dd26-213">Nello script seguente usare RMAN per ripristinare il database:</span><span class="sxs-lookup"><span data-stu-id="3dd26-213">In the following script, use RMAN to recover the database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="3dd26-214">Smontare il disco.</span><span class="sxs-lookup"><span data-stu-id="3dd26-214">Unmount the disk.</span></span>

    <span data-ttu-id="3dd26-215">Nel portale di Azure, nel pannello **Ripristino file (anteprima)** fare clic su **Unmount Disks** (Smonta dischi).</span><span class="sxs-lookup"><span data-stu-id="3dd26-215">In the Azure portal, on the **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Comando Unmount disks](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-the-entire-vm"></a><span data-ttu-id="3dd26-217">Ripristinare l'intera VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-217">Restore the entire VM</span></span>

<span data-ttu-id="3dd26-218">Anziché ripristinare i file eliminati dagli insiemi di credenziali dei servizi di ripristino, è possibile ripristinare l'intera macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3dd26-218">Instead of restoring the deleted files from the Recovery Services vaults, you can restore the entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="3dd26-219">Passaggio 1: Eliminare myVM</span><span class="sxs-lookup"><span data-stu-id="3dd26-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="3dd26-220">Nel portale di Azure passare all'insieme di credenziali **myVM1** e selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-220">In the Azure portal, go to the **myVM1** vault, and then select **Delete**.</span></span>

    ![Comando Elimina insieme di credenziali](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-the-vm"></a><span data-ttu-id="3dd26-222">Passaggio 2: Ripristinare la VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-222">Step 2: Recover the VM</span></span>

1.  <span data-ttu-id="3dd26-223">Passare a **Insiemi di credenziali dei servizi di ripristino** e selezionare **myVault**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-223">Go to **Recovery Services vaults**, and then select **myVault**.</span></span>

    ![voce myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="3dd26-225">Nel pannello **Panoramica** in **Elementi di backup** selezionare il numero di elementi.</span><span class="sxs-lookup"><span data-stu-id="3dd26-225">On the **Overview** blade, under **Backup items**, select the number of items.</span></span>

    ![elementi di backup myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="3dd26-227">Nel pannello **Backup Items (Azure Virtual Machine)** (Elementi di backup: macchina virtuale di Azure) selezionare **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-227">On the **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Pagina di ripristino della macchina virtuale](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="3dd26-229">Nel pannello **myvm1** fare clic sui puntini di sospensione (**...**) e su **Ripristina macchina virtuale**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-229">On the **myvm1** blade, click the ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Comando Ripristina macchina virtuale](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="3dd26-231">Nel pannello **Seleziona punto di ripristino** selezionare l'elemento che si vuole ripristinare e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-231">On the **Select restore point** blade, select the item that you want to restore, and then click **OK**.</span></span>

    ![Selezionare il punto di ripristino](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="3dd26-233">Se è stato abilitato il backup coerente con l'applicazione, viene visualizzata una barra verticale di colore blu.</span><span class="sxs-lookup"><span data-stu-id="3dd26-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="3dd26-234">Nel pannello **Configurazione di ripristino** selezionare il nome della macchina virtuale, il gruppo di risorse e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-234">On the **Restore configuration** blade, select the virtual machine name, select the resource group, and then click **OK**.</span></span>

    ![Valori di configurazione del ripristino](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="3dd26-236">Per ripristinare la macchina virtuale, fare clic sul pulsante **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-236">To restore the VM, click the **Restore** button.</span></span>

8.  <span data-ttu-id="3dd26-237">Per visualizzare lo stato del processo di ripristino, fare clic su **Processi** e quindi su **Processi di backup**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-237">To view the status of the restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Comando dello stato dei processi di backup](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="3dd26-239">L'immagine seguente mostra lo stato del processo di ripristino:</span><span class="sxs-lookup"><span data-stu-id="3dd26-239">The following figure shows the status of the restore process:</span></span>

    ![Stato del processo di ripristino](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-the-public-ip-address"></a><span data-ttu-id="3dd26-241">Passaggio 3: Impostare l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="3dd26-241">Step 3: Set the public IP address</span></span>
<span data-ttu-id="3dd26-242">Dopo il ripristino della macchina virtuale, configurare l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3dd26-242">After the VM is restored, set up the public IP address.</span></span>

1.  <span data-ttu-id="3dd26-243">Nella casella di ricerca inserire l'**indirizzo IP pubblico**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-243">In the search box, enter **public IP address**.</span></span>

    ![Elenco degli indirizzi IP pubblici](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="3dd26-245">Nel pannello**Indirizzi IP pubblici** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-245">On the **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="3dd26-246">Nel pannello **Crea indirizzo IP pubblico** per **Nome** selezionare il nome dell'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3dd26-246">On the **Create public IP address** blade, for **Name**, select the public IP name.</span></span> <span data-ttu-id="3dd26-247">Per **Gruppo di risorse** selezionare **Usa esistente**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="3dd26-248">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-248">Then, click **Create**.</span></span>

    ![Creare un indirizzo IP](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="3dd26-250">Per associare l'indirizzo IP pubblico all'interfaccia di rete per la macchina virtuale, cercare e selezionare **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-250">To associate the public IP address with the network interface for the VM, search for and select **myVMip**.</span></span> <span data-ttu-id="3dd26-251">Quindi fare clic su **Associa**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-251">Then, click **Associate**.</span></span>

    ![Associare l'indirizzo IP](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="3dd26-253">Per **Tipo di risorsa** selezionare **Interfaccia di rete**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="3dd26-254">Selezionare l'interfaccia di rete usata dall'istanza di myVM e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3dd26-254">Select the network interface that is used by the myVM instance, and then click **OK**.</span></span>

    ![Selezionare i valori Tipo di risorsa e Interfaccia di rete](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="3dd26-256">Cercare e aprire l'istanza di myVM che viene trasferita dal portale.</span><span class="sxs-lookup"><span data-stu-id="3dd26-256">Search for and open the instance of myVM that is ported from the portal.</span></span> <span data-ttu-id="3dd26-257">L'indirizzo IP associato alla macchina virtuale viene visualizzato nel pannello **Panoramica** di myVM.</span><span class="sxs-lookup"><span data-stu-id="3dd26-257">The IP address that is associated with the VM appears on the myVM **Overview** blade.</span></span>

    ![Valore dell'indirizzo IP](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-to-the-vm"></a><span data-ttu-id="3dd26-259">Passaggio 4: Eseguire la connessione alla VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-259">Step 4: Connect to the VM</span></span>

*   <span data-ttu-id="3dd26-260">Per eseguire la connessione alla macchina virtuale, usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="3dd26-260">To connect to the VM, use the following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-the-database-is-accessible"></a><span data-ttu-id="3dd26-261">Passaggio 5: Verificare se il database è accessibile</span><span class="sxs-lookup"><span data-stu-id="3dd26-261">Step 5: Test whether the database is accessible</span></span>
*   <span data-ttu-id="3dd26-262">Per testare l'accessibilità, usare lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="3dd26-262">To test accessibility, use the following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="3dd26-263">Se il comando **startup** del database genera un errore, per ripristinare il database, vedere [Passaggio 6: Usare RMAN per ripristinare il database (facoltativo)](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="3dd26-263">If the database **startup** command generates an error, to recover the database, see [Step 6: Use RMAN to recover the database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-to-recover-the-database"></a><span data-ttu-id="3dd26-264">Passaggio 6: Usare RMAN per ripristinare il database (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="3dd26-264">Step 6: (Optional) Use RMAN to recover the database</span></span>
*   <span data-ttu-id="3dd26-265">Usare lo script seguente per ripristinare il database:</span><span class="sxs-lookup"><span data-stu-id="3dd26-265">To recover the database, use the following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="3dd26-266">L'esecuzione di backup e ripristino del database Oracle Database 12c su una macchina virtuale Linux di Azure è stata completata.</span><span class="sxs-lookup"><span data-stu-id="3dd26-266">The backup and recovery of the Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="3dd26-267">Eliminare la VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-267">Delete the VM</span></span>

<span data-ttu-id="3dd26-268">Quando la macchina virtuale non è più necessaria, è possibile usare il comando seguente per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate:</span><span class="sxs-lookup"><span data-stu-id="3dd26-268">When you no longer need the VM, you can use the following command to remove the resource group, the VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="3dd26-269">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3dd26-269">Next steps</span></span>

[<span data-ttu-id="3dd26-270">Esercitazione: Creare VM a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="3dd26-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="3dd26-271">Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="3dd26-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



