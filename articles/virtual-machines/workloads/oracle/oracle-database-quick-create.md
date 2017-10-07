---
title: aaaCreate un database Oracle in una macchina virtuale di Azure | Documenti Microsoft
description: Ottenere rapidamente un database Oracle 12c operativo nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="cab19-103">Creare un database Oracle in una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="cab19-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="cab19-104">Questa guida descrive con hello Azure CLI toodeploy una macchina virtuale di Azure da hello [immagine della raccolta marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in un database Oracle 12C ordine toocreate.</span><span class="sxs-lookup"><span data-stu-id="cab19-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="cab19-105">Dopo aver distribuito il server di hello, verrà effettuata la connessione via SSH nel database di Oracle hello tooconfigure ordine.</span><span class="sxs-lookup"><span data-stu-id="cab19-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="cab19-106">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="cab19-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cab19-107">Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="cab19-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cab19-108">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="cab19-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cab19-109">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cab19-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="cab19-110">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="cab19-110">Create a resource group</span></span>

<span data-ttu-id="cab19-111">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cab19-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="cab19-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="cab19-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="cab19-113">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="cab19-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="cab19-114">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="cab19-114">Create virtual machine</span></span>

<span data-ttu-id="cab19-115">toocreate una macchina virtuale (VM), utilizzare hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cab19-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="cab19-116">esempio Hello crea una macchina virtuale denominata `myVM`.</span><span class="sxs-lookup"><span data-stu-id="cab19-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="cab19-117">Crea anche le chiavi SSH se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="cab19-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="cab19-118">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="cab19-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="cab19-119">Dopo aver creato una macchina virtuale hello, CLI di Azure consente di visualizzare informazioni toohello simile esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="cab19-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="cab19-120">Si noti il valore di hello per `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="cab19-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="cab19-121">Utilizzare questo hello tooaccess indirizzo macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cab19-121">You use this address tooaccess hello VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a><span data-ttu-id="cab19-122">Connettersi toohello VM</span><span class="sxs-lookup"><span data-stu-id="cab19-122">Connect toohello VM</span></span>

<span data-ttu-id="cab19-123">toocreate una sessione SSH con hello macchina virtuale, utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="cab19-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="cab19-124">Sostituire l'indirizzo IP hello con hello `publicIpAddress` valore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cab19-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="cab19-125">Creare database hello</span><span class="sxs-lookup"><span data-stu-id="cab19-125">Create hello database</span></span>

<span data-ttu-id="cab19-126">il software Oracle Hello è già installato in un'immagine del Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="cab19-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="cab19-127">Creare un database di esempio come segue.</span><span class="sxs-lookup"><span data-stu-id="cab19-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="cab19-128">Passare toohello *oracle* utente avanzato, quindi inizializzare hello listener per la registrazione:</span><span class="sxs-lookup"><span data-stu-id="cab19-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="cab19-129">output di Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cab19-129">hello output is similar toohello following:</span></span>

    ```bash
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

2.  <span data-ttu-id="cab19-130">Crea database hello:</span><span class="sxs-lookup"><span data-stu-id="cab19-130">Create hello database:</span></span>

    ```bash
    dbca -silent \
           -createDatabase \
           -templateName General_Purpose.dbc \
           -gdbname cdb1 \
           -sid cdb1 \
           -responseFile NO_VALUE \
           -characterSet AL32UTF8 \
           -sysPassword OraPasswd1 \
           -systemPassword OraPasswd1 \
           -createAsContainerDatabase true \
           -numberOfPDBs 1 \
           -pdbName pdb1 \
           -pdbAdminPassword OraPasswd1 \
           -databaseType MULTIPURPOSE \
           -automaticMemoryManagement false \
           -storageType FS \
           -ignorePreReqs
    ```

    <span data-ttu-id="cab19-131">Accetta alcuni database di hello toocreate minuti.</span><span class="sxs-lookup"><span data-stu-id="cab19-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="cab19-132">Impostare le variabili Oracle</span><span class="sxs-lookup"><span data-stu-id="cab19-132">Set Oracle variables</span></span>

<span data-ttu-id="cab19-133">Prima di connettersi, è necessario tooset due variabili di ambiente: *ORACLE_HOME* e *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="cab19-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="cab19-134">È anche possibile aggiungere ORACLE_HOME e ORACLE_SID file .bashrc toohello di variabili.</span><span class="sxs-lookup"><span data-stu-id="cab19-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="cab19-135">Le variabili di ambiente hello futuri accessi salvati. Verificare i seguenti hello istruzioni sono state aggiunte toohello `~/.bashrc` file utilizzando l'editor di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="cab19-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="cab19-136">Connettività a Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="cab19-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="cab19-137">Strumento di gestione interfaccia utente grafica che è possibile utilizzare database hello tooexplore, configurare Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="cab19-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="cab19-138">tooconnect tooOracle EM Express, è necessario innanzitutto impostare porta hello in Oracle.</span><span class="sxs-lookup"><span data-stu-id="cab19-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="cab19-139">La connessione a database tooyour sqlplus utilizzando:</span><span class="sxs-lookup"><span data-stu-id="cab19-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="cab19-140">Una volta connessi, impostare la porta hello 5502 per Express EM</span><span class="sxs-lookup"><span data-stu-id="cab19-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="cab19-141">Contenitore hello aprire PDB1 se non è già aperto, ma prima controllare hello lo stato di:</span><span class="sxs-lookup"><span data-stu-id="cab19-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="cab19-142">output di Hello è simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="cab19-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="cab19-143">Se hello OPEN_MODE per `PDB1` non è di lettura e scrittura, quindi eseguire hello seguenti comandi tooopen PDB1:</span><span class="sxs-lookup"><span data-stu-id="cab19-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="cab19-144">È necessario tootype `quit` tooend hello sqlplus sessione e il tipo `exit` toologout dell'utente oracle hello.</span><span class="sxs-lookup"><span data-stu-id="cab19-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="cab19-145">Automatizzare l'avvio e l'arresto del database</span><span class="sxs-lookup"><span data-stu-id="cab19-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="cab19-146">database Oracle Hello per impostazione predefinita non viene avviato automaticamente quando si riavvia hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cab19-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="cab19-147">tooset backup hello Oracle database toostart automaticamente, prima di tutto Accedi come radice.</span><span class="sxs-lookup"><span data-stu-id="cab19-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="cab19-148">Quindi creare e aggiornare alcuni file di sistema.</span><span class="sxs-lookup"><span data-stu-id="cab19-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="cab19-149">Accedere come utente ROOT</span><span class="sxs-lookup"><span data-stu-id="cab19-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="cab19-150">Utilizzando l'editor preferito, modificare il file di hello `/etc/oratab` e modificare l'impostazione predefinita hello `N` troppo`Y`:</span><span class="sxs-lookup"><span data-stu-id="cab19-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="cab19-151">Creare un file denominato `/etc/init.d/dbora` e Incolla hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="cab19-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="cab19-152">Modificare le autorizzazioni nei file con *chmod* come segue:</span><span class="sxs-lookup"><span data-stu-id="cab19-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="cab19-153">Creare collegamenti simbolici per l'avvio e l'arresto come segue:</span><span class="sxs-lookup"><span data-stu-id="cab19-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="cab19-154">tootest le modifiche, riavviare hello VM:</span><span class="sxs-lookup"><span data-stu-id="cab19-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="cab19-155">Aprire le porte per la connettività</span><span class="sxs-lookup"><span data-stu-id="cab19-155">Open ports for connectivity</span></span>

<span data-ttu-id="cab19-156">attività finale Hello è tooconfigure alcuni endpoint esterno.</span><span class="sxs-lookup"><span data-stu-id="cab19-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="cab19-157">tooset backup hello Azure gruppo di sicurezza di rete che protegge hello VM, terminare la sessione SSH in hello VM (deve avere stato espulso dalla SSH durante il riavvio nel passaggio precedente).</span><span class="sxs-lookup"><span data-stu-id="cab19-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="cab19-158">endpoint di hello tooopen che si utilizzi tooaccess hello Oracle database in modalità remota, creare una regola gruppo di sicurezza di rete con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cab19-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="cab19-159">endpoint di hello tooopen utilizzare tooaccess Express EM Oracle in modalità remota, creare una regola gruppo di sicurezza di rete con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cab19-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="cab19-160">Se è necessario ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show) come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cab19-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="cab19-161">Connettersi a EM Express dal browser.</span><span class="sxs-lookup"><span data-stu-id="cab19-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="cab19-162">Verificare che il browser sia compatibile con EM Express. È necessario installare Flash.</span><span class="sxs-lookup"><span data-stu-id="cab19-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="cab19-163">È possibile accedere tramite hello **SYS** account e controllare hello **come sysdba** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="cab19-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="cab19-164">Utilizzare password hello **OraPasswd1** che impostato durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="cab19-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Schermata della pagina di accesso Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="cab19-166">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="cab19-166">Clean up resources</span></span>

<span data-ttu-id="cab19-167">Dopo aver esplorazione di un database Oracle in Azure e hello VM non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="cab19-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cab19-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cab19-168">Next steps</span></span>

<span data-ttu-id="cab19-169">Informazioni su altre [soluzioni Oracle in Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="cab19-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="cab19-170">Provare a hello [installazione e configurazione di gestione di archiviazione automatica di Oracle](configure-oracle-asm.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="cab19-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
