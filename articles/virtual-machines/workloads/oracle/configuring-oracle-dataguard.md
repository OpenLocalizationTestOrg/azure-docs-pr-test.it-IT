---
title: Implementare Oracle Data Guard nella VM Linux di Azure | Microsoft Docs
description: Attivare e mettere in funzione rapidamente Oracle Data Guard nell'ambiente Azure.
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="0c599-103">Implementare Oracle Data Guard nella VM Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="0c599-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="0c599-104">L'interfaccia della riga di comando di Azure viene usata per creare e gestire le risorse di Azure dalla riga di comando o negli script.</span><span class="sxs-lookup"><span data-stu-id="0c599-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="0c599-105">Questa guida descrive nei dettagli l'uso dell'interfaccia della riga di comando di Azure per distribuire un database Oracle 12c dall'immagine della raccolta Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0c599-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="0c599-106">Dopo la creazione del database Oracle questo documento descrive in modo dettagliato come installare e configurare Data Guard nella VM Azure.</span><span class="sxs-lookup"><span data-stu-id="0c599-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="0c599-107">Prima di iniziare, verificare che l'interfaccia della riga di comando di Azure sia stata installata.</span><span class="sxs-lookup"><span data-stu-id="0c599-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="0c599-108">Per altre informazioni, vedere [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Guida all'installazione dell'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="0c599-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="0c599-109">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="0c599-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="0c599-110">Presupposti</span><span class="sxs-lookup"><span data-stu-id="0c599-110">Assumptions</span></span>

<span data-ttu-id="0c599-111">Per installare Oracle Data Guard, è necessario creare due VM Azure nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="0c599-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="0c599-112">L'immagine di Marketplace usata per creare le VM è "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="0c599-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="0c599-113">Nella VM primaria (myVM1) è installata un'istanza di Oracle in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0c599-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="0c599-114">Nella VM di standby (myVM2) è installato solo il software Oracle.</span><span class="sxs-lookup"><span data-stu-id="0c599-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="0c599-115">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="0c599-115">Log in to Azure</span></span> 

<span data-ttu-id="0c599-116">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login) e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="0c599-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="0c599-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="0c599-117">Create a resource group</span></span>

<span data-ttu-id="0c599-118">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0c599-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="0c599-119">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="0c599-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="0c599-120">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella posizione `westus`.</span><span class="sxs-lookup"><span data-stu-id="0c599-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="0c599-121">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="0c599-121">Create availability set</span></span>

<span data-ttu-id="0c599-122">Questo passaggio è facoltativo, ma consigliabile.</span><span class="sxs-lookup"><span data-stu-id="0c599-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="0c599-123">Per altre informazioni, vedere le informazioni sui [set di disponibilità di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="0c599-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="0c599-124">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c599-124">Create virtual machine</span></span>

<span data-ttu-id="0c599-125">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0c599-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="0c599-126">Nell'esempio seguente vengono create due VM denominate `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="0c599-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="0c599-127">Crea le chiavi SSH, se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0c599-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="0c599-128">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="0c599-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="0c599-129">Creare myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="0c599-129">Create myVM1 (primary)</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="0c599-130">Dopo che la VM è stata creata, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente. Prendere nota del valore `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="0c599-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="0c599-131">Questo indirizzo viene usato per accedere alla VM.</span><span class="sxs-lookup"><span data-stu-id="0c599-131">This address is used to access the VM.</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="0c599-132">Creare myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="0c599-132">Create myVM2 (standby)</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="0c599-133">Annotare il valore `publicIpAddress` dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="0c599-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="0c599-134">Aprire la porta TCP per la connettività</span><span class="sxs-lookup"><span data-stu-id="0c599-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="0c599-135">Il passaggio consiste nel configurare endpoint esterni consentendo l'accesso in remoto al DB Oracle; eseguire il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="0c599-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="0c599-136">Aprire la porta per myVM1</span><span class="sxs-lookup"><span data-stu-id="0c599-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="0c599-137">Il risultato sarà simile alla seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="0c599-137">Result should look similar to the following response:</span></span>

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

<span data-ttu-id="0c599-138">Aprire la porta per myVM2</span><span class="sxs-lookup"><span data-stu-id="0c599-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="0c599-139">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c599-139">Connect to virtual machine</span></span>

<span data-ttu-id="0c599-140">Usare il comando seguente per creare una sessione SSH con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c599-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="0c599-141">Sostituire l'indirizzo IP con `publicIpAddress` della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0c599-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="0c599-142">Creare il database su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="0c599-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="0c599-143">Il software Oracle è già installato nell'immagine di Marketplace, pertanto il passaggio successivo è installare il database.</span><span class="sxs-lookup"><span data-stu-id="0c599-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="0c599-144">il primo passaggio viene eseguito come utente avanzato 'oracle'.</span><span class="sxs-lookup"><span data-stu-id="0c599-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="0c599-145">creare il database:</span><span class="sxs-lookup"><span data-stu-id="0c599-145">create the database:</span></span>

```bash
$ dbca -silent \
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
<span data-ttu-id="0c599-146">Gli output saranno simili alla risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="0c599-146">Outputs should look similar to the following response:</span></span>

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="0c599-147">Impostare le variabili ORACLE_SID e ORACLE_HOME</span><span class="sxs-lookup"><span data-stu-id="0c599-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="0c599-148">Se lo si vuole, è possibile aggiungere le variabili ORACLE_HOME e ORACLE_SID al file con estensione bashrc, in modo da salvare queste impostazioni per un accesso futuro.</span><span class="sxs-lookup"><span data-stu-id="0c599-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="0c599-149">Configurazioni di Data Guard</span><span class="sxs-lookup"><span data-stu-id="0c599-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="0c599-150">Abilitare la modalità archivelog su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="0c599-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
```
<span data-ttu-id="0c599-151">Abilitare la registrazione forzata e verificare che sia presente almeno un file di registro.</span><span class="sxs-lookup"><span data-stu-id="0c599-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="0c599-152">Creare i log di ripristino di standby</span><span class="sxs-lookup"><span data-stu-id="0c599-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="0c599-153">Attivare il flashback che consente il ripristino in notevole anticipo e impostare STANDBY_FILE_MANAGEMENT su auto</span><span class="sxs-lookup"><span data-stu-id="0c599-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="0c599-154">Configurazione del servizio su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="0c599-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="0c599-155">Modificare o creare il file tnsnames.ora presente nella cartella $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="0c599-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="0c599-156">Aggiungere le voci seguenti</span><span class="sxs-lookup"><span data-stu-id="0c599-156">Add the following entries</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="0c599-157">Modificare o creare il file listener.ora presente nella cartella $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="0c599-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="0c599-158">Aggiungere le voci seguenti</span><span class="sxs-lookup"><span data-stu-id="0c599-158">Add the following entries</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="0c599-159">Avviare il listener</span><span class="sxs-lookup"><span data-stu-id="0c599-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="0c599-160">Configurazione del servizio su myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="0c599-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="0c599-161">Modificare o creare il file tnsnames.ora presente nella cartella $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="0c599-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="0c599-162">Aggiungere le voci seguenti</span><span class="sxs-lookup"><span data-stu-id="0c599-162">Add the following entries</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="0c599-163">Modificare o creare il file listener.ora presente nella cartella $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="0c599-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="0c599-164">Aggiungere le voci seguenti</span><span class="sxs-lookup"><span data-stu-id="0c599-164">Add the following entries</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="0c599-165">Avviare il listener</span><span class="sxs-lookup"><span data-stu-id="0c599-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="0c599-166">Abilitare il broker Data Guard</span><span class="sxs-lookup"><span data-stu-id="0c599-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="0c599-167">Ripristinare il database su myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="0c599-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="0c599-168">Creare un file di parametri '/tmp/initcdb1_stby.ora' con il contenuto seguente</span><span class="sxs-lookup"><span data-stu-id="0c599-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="0c599-169">Creare cartelle</span><span class="sxs-lookup"><span data-stu-id="0c599-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="0c599-170">Creare il file di password</span><span class="sxs-lookup"><span data-stu-id="0c599-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="0c599-171">Avviare il database su myVM2</span><span class="sxs-lookup"><span data-stu-id="0c599-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="0c599-172">Ripristinare il database usando l'utilità RMAN</span><span class="sxs-lookup"><span data-stu-id="0c599-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="0c599-173">Eseguire i comandi seguenti in RMAN</span><span class="sxs-lookup"><span data-stu-id="0c599-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="0c599-174">Abilitare il broker Data Guard</span><span class="sxs-lookup"><span data-stu-id="0c599-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="0c599-175">Configurare il broker Data Guard su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="0c599-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="0c599-176">Avviare il manager Data Guard e accedere usando SYS e password (non l'autenticazione del sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="0c599-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="0c599-177">Eseguire le operazioni seguenti</span><span class="sxs-lookup"><span data-stu-id="0c599-177">Perform the followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="0c599-178">Esaminare la configurazione</span><span class="sxs-lookup"><span data-stu-id="0c599-178">Review the configuration</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="0c599-179">Questa operazione completa l'installazione di Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="0c599-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="0c599-180">La sezione successiva illustra come testare la connettività e il passaggio</span><span class="sxs-lookup"><span data-stu-id="0c599-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="0c599-181">Connettere il database dal computer client</span><span class="sxs-lookup"><span data-stu-id="0c599-181">Connect database from client machine</span></span>

<span data-ttu-id="0c599-182">Aggiornare o creare il file tnsnames.ora sul computer client, in genere presente nella cartella $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="0c599-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="0c599-183">Sostituire l'indirizzo IP con `publicIpAddress` per myVM1 e myVM2</span><span class="sxs-lookup"><span data-stu-id="0c599-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="0c599-184">Avviare sqlplus</span><span class="sxs-lookup"><span data-stu-id="0c599-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="0c599-185">Testare la configurazione di Data Guard</span><span class="sxs-lookup"><span data-stu-id="0c599-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="0c599-186">Passaggio di database su myVM1 (primario)</span><span class="sxs-lookup"><span data-stu-id="0c599-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="0c599-187">Per passare dal database primario a quello di standby (da cdb1 a cdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="0c599-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="0c599-188">Ora dovrebbe essere possibile connettersi al database di standby</span><span class="sxs-lookup"><span data-stu-id="0c599-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="0c599-189">Avviare sqlplus</span><span class="sxs-lookup"><span data-stu-id="0c599-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="0c599-190">Cambio di database su myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="0c599-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="0c599-191">Per l'operazione inversa, eseguire le operazioni seguenti su myVM2</span><span class="sxs-lookup"><span data-stu-id="0c599-191">To switch back, run the followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="0c599-192">Di nuovo dovrebbe essere possibile connettersi al database primario</span><span class="sxs-lookup"><span data-stu-id="0c599-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="0c599-193">Avviare sqlplus</span><span class="sxs-lookup"><span data-stu-id="0c599-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="0c599-194">Questa operazione completa l'installazione e la configurazione di Data Guard nell'ambiente Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="0c599-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="0c599-195">Eliminare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0c599-195">Delete virtual machine</span></span>

<span data-ttu-id="0c599-196">Quando non servono più, il comando seguente consente di rimuovere il gruppo di risorse, la VM e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="0c599-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="0c599-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0c599-197">Next steps</span></span>

[<span data-ttu-id="0c599-198">Creare esercitazioni per macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="0c599-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="0c599-199">Esplorare gli esempi dell'interfaccia della riga di comando per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="0c599-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
