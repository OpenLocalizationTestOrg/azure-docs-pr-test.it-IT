---
title: Creare un database Oracle in una VM di Azure | Microsoft Docs
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="534b9-103">Creare un database Oracle in una VM di Azure</span><span class="sxs-lookup"><span data-stu-id="534b9-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="534b9-104">Questa guida descrive nei dettagli l'uso dell'interfaccia della riga di comando di Azure per distribuire una macchina virtuale di Azure dall'[immagine della raccolta Marketplace di Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) per creare un database Oracle 12c.</span><span class="sxs-lookup"><span data-stu-id="534b9-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="534b9-105">Dopo avere distribuito il server, verrà effettuata la connessione via SSH per configurare il database Oracle.</span><span class="sxs-lookup"><span data-stu-id="534b9-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="534b9-106">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="534b9-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="534b9-107">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa guida introduttiva è necessario eseguire la versione 2.0.4 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="534b9-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="534b9-108">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="534b9-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="534b9-109">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="534b9-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="534b9-110">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="534b9-110">Create a resource group</span></span>

<span data-ttu-id="534b9-111">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="534b9-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="534b9-112">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="534b9-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="534b9-113">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="534b9-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="534b9-114">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="534b9-114">Create virtual machine</span></span>

<span data-ttu-id="534b9-115">Per crea una macchina virtuale (VM), usare il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="534b9-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="534b9-116">L'esempio seguente crea una VM denominata `myVM`.</span><span class="sxs-lookup"><span data-stu-id="534b9-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="534b9-117">Crea anche le chiavi SSH se non esistono già in un percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="534b9-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="534b9-118">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="534b9-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="534b9-119">In seguito alla creazione della VM, l'interfaccia della riga di comando di Azure visualizza informazioni simili a quelle dell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="534b9-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="534b9-120">Notare il valore di `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="534b9-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="534b9-121">Questo indirizzo verrà usato per accedere alla VM.</span><span class="sxs-lookup"><span data-stu-id="534b9-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="534b9-122">Connettersi alla VM</span><span class="sxs-lookup"><span data-stu-id="534b9-122">Connect to the VM</span></span>

<span data-ttu-id="534b9-123">Per creare una sessione SSH con la VM, usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="534b9-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="534b9-124">Sostituire l'indirizzo IP con il valore di `publicIpAddress` della VM.</span><span class="sxs-lookup"><span data-stu-id="534b9-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="534b9-125">Creare il database</span><span class="sxs-lookup"><span data-stu-id="534b9-125">Create the database</span></span>

<span data-ttu-id="534b9-126">Il software Oracle è già installato nell'immagine del Marketplace.</span><span class="sxs-lookup"><span data-stu-id="534b9-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="534b9-127">Creare un database di esempio come segue.</span><span class="sxs-lookup"><span data-stu-id="534b9-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="534b9-128">Passare all'utente con privilegi avanzati *oracle*, quindi inizializzare il listener per la registrazione:</span><span class="sxs-lookup"><span data-stu-id="534b9-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="534b9-129">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="534b9-129">The output is similar to the following:</span></span>

    ```bash
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

2.  <span data-ttu-id="534b9-130">Creare il database:</span><span class="sxs-lookup"><span data-stu-id="534b9-130">Create the database:</span></span>

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

    <span data-ttu-id="534b9-131">La creazione del database richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="534b9-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="534b9-132">Impostare le variabili Oracle</span><span class="sxs-lookup"><span data-stu-id="534b9-132">Set Oracle variables</span></span>

<span data-ttu-id="534b9-133">Prima della connessione, è necessario configurare due variabili di ambiente: *ORACLE_HOME* e *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="534b9-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="534b9-134">È anche possibile aggiungere le variabili ORACLE_HOME e ORACLE_SID al file con estensione bashrc.</span><span class="sxs-lookup"><span data-stu-id="534b9-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="534b9-135">In questo modo, le variabili di ambiente verranno salvate per gli accessi successivi.</span><span class="sxs-lookup"><span data-stu-id="534b9-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="534b9-136">Verificare che le seguenti istruzioni siano state aggiunte al file `~/.bashrc` usando l'editor scelto.</span><span class="sxs-lookup"><span data-stu-id="534b9-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="534b9-137">Connettività a Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="534b9-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="534b9-138">Per ottenere uno strumento di gestione dell'interfaccia utente grafica da usare per esplorare il database, configurare Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="534b9-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="534b9-139">Per connettersi a Oracle EM Express, prima di tutto è necessario configurare la porta in Oracle.</span><span class="sxs-lookup"><span data-stu-id="534b9-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="534b9-140">Connettersi al database usando sqlplus:</span><span class="sxs-lookup"><span data-stu-id="534b9-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="534b9-141">Dopo la connessione, impostare la porta 5502 per EM Express</span><span class="sxs-lookup"><span data-stu-id="534b9-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="534b9-142">Aprire il contenitore PDB1 se non è già aperto, ma prima controllare lo stato:</span><span class="sxs-lookup"><span data-stu-id="534b9-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="534b9-143">L'output è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="534b9-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="534b9-144">Se OPEN_MODE per `PDB1` non è READ WRITE, usare i comandi seguenti per aprire PDB1:</span><span class="sxs-lookup"><span data-stu-id="534b9-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="534b9-145">È necessario digitare `quit` per terminare la sessione sqlplus e `exit` per disconnettere l'utente Oracle.</span><span class="sxs-lookup"><span data-stu-id="534b9-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="534b9-146">Automatizzare l'avvio e l'arresto del database</span><span class="sxs-lookup"><span data-stu-id="534b9-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="534b9-147">Per impostazione predefinita, il database Oracle non viene avviato automaticamente quando si riavvia la VM.</span><span class="sxs-lookup"><span data-stu-id="534b9-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="534b9-148">Per configurare il database Oracle perché venga avviato automaticamente, accedere prima di tutto come utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="534b9-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="534b9-149">Quindi creare e aggiornare alcuni file di sistema.</span><span class="sxs-lookup"><span data-stu-id="534b9-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="534b9-150">Accedere come utente ROOT</span><span class="sxs-lookup"><span data-stu-id="534b9-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="534b9-151">Usando l'editor preferito modificare il file `/etc/oratab` e il valore predefinito `N` in `Y`:</span><span class="sxs-lookup"><span data-stu-id="534b9-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="534b9-152">Creare un file denominato `/etc/init.d/dbora` e incollare i contenuti seguenti:</span><span class="sxs-lookup"><span data-stu-id="534b9-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="534b9-153">Modificare le autorizzazioni nei file con *chmod* come segue:</span><span class="sxs-lookup"><span data-stu-id="534b9-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="534b9-154">Creare collegamenti simbolici per l'avvio e l'arresto come segue:</span><span class="sxs-lookup"><span data-stu-id="534b9-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="534b9-155">Per testare le modifiche, riavviare la VM:</span><span class="sxs-lookup"><span data-stu-id="534b9-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="534b9-156">Aprire le porte per la connettività</span><span class="sxs-lookup"><span data-stu-id="534b9-156">Open ports for connectivity</span></span>

<span data-ttu-id="534b9-157">Il passaggio finale consiste nel configurare alcuni endpoint esterni.</span><span class="sxs-lookup"><span data-stu-id="534b9-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="534b9-158">Per configurare il gruppo di sicurezza di rete di Azure che protegge la VM, prima di tutto chiudere la sessione SSH nella VM, anche se la sessione dovrebbe essere stata chiusa durante il riavvio nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="534b9-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="534b9-159">Per aprire l'endpoint usato per accedere al database Oracle in modalità remota, creare una regola del gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create) come segue:</span><span class="sxs-lookup"><span data-stu-id="534b9-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="534b9-160">Per aprire l'endpoint usato per accedere a Oracle EM Express in modalità remota, creare una regola del gruppo di sicurezza di rete con [az network nsg rule create](/cli/azure/network/nsg/rule#create) come segue:</span><span class="sxs-lookup"><span data-stu-id="534b9-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="534b9-161">Se necessario, ottenere di nuovo l'indirizzo IP pubblico della VM con [az network public-ip show](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="534b9-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="534b9-162">Connettersi a EM Express dal browser.</span><span class="sxs-lookup"><span data-stu-id="534b9-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="534b9-163">Verificare che il browser sia compatibile con EM Express. È necessario installare Flash.</span><span class="sxs-lookup"><span data-stu-id="534b9-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="534b9-164">È possibile eseguire l'accesso usando l'account **SYS** e selezionare la casella di controllo **as sysdba**.</span><span class="sxs-lookup"><span data-stu-id="534b9-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="534b9-165">Usare la password **OraPasswd1** impostata durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="534b9-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Screenshot della pagina di accesso a Oracle OEM Express](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="534b9-167">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="534b9-167">Clean up resources</span></span>

<span data-ttu-id="534b9-168">Al termine dell'esplorazione di un primo database Oracle in Azure e quando la macchina virtuale non è più necessaria, è possibile usare il comando [az group delete](/cli/azure/group#delete) per rimuovere il gruppo di risorse la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="534b9-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="534b9-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="534b9-169">Next steps</span></span>

<span data-ttu-id="534b9-170">Informazioni su altre [soluzioni Oracle in Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="534b9-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="534b9-171">Provare a eseguire l'esercitazione [Installing and Configuring Oracle Automated Storage Management (Installazione e configurazione di Oracle Automated Storage Management)](configure-oracle-asm.md).</span><span class="sxs-lookup"><span data-stu-id="534b9-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>