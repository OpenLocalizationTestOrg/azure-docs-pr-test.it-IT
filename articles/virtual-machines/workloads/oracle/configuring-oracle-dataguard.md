---
title: aaaImplement Oracle Data Guard sulla macchina virtuale Linux di Azure | Documenti Microsoft
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="5b76c-103">Implementare Oracle Data Guard nella VM Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="5b76c-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="5b76c-104">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="5b76c-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="5b76c-105">Questa guida descrive con hello Azure CLI toodeploy Oracle 12C Database dall'immagine della raccolta hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5b76c-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="5b76c-106">Una volta creato il database di Oracle hello, questo documento viene illustrata la procedura dettagliata tooinstall e configurare Data Guard sulla macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b76c-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="5b76c-107">Prima di iniziare, verificare che tale hello che CLI di Azure è stato installato.</span><span class="sxs-lookup"><span data-stu-id="5b76c-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="5b76c-108">Per altre informazioni, vedere [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Guida all'installazione dell'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="5b76c-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="5b76c-109">Preparare l'ambiente hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="5b76c-110">Presupposti</span><span class="sxs-lookup"><span data-stu-id="5b76c-110">Assumptions</span></span>

<span data-ttu-id="5b76c-111">hello tooperform installare Oracle Data Guard, è necessario toocreate due macchine virtuali di Azure su hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5b76c-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="5b76c-112">immagine del Marketplace Hello è utilizzare toocreate hello macchine virtuali è "Oracle: Oracle-Database-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="5b76c-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="5b76c-113">Hello macchina virtuale primaria (myVM1) è un'istanza di Oracle in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5b76c-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="5b76c-114">Hello che nella macchina virtuale standby (myVM2) è installato solo il software Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="5b76c-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5b76c-115">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="5b76c-115">Log in tooAzure</span></span> 

<span data-ttu-id="5b76c-116">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="5b76c-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="5b76c-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5b76c-117">Create a resource group</span></span>

<span data-ttu-id="5b76c-118">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5b76c-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5b76c-119">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="5b76c-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5b76c-120">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso.</span><span class="sxs-lookup"><span data-stu-id="5b76c-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="5b76c-121">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="5b76c-121">Create availability set</span></span>

<span data-ttu-id="5b76c-122">Questo passaggio è facoltativo, ma consigliabile.</span><span class="sxs-lookup"><span data-stu-id="5b76c-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="5b76c-123">Per altre informazioni, vedere le informazioni sui [set di disponibilità di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="5b76c-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="5b76c-124">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5b76c-124">Create virtual machine</span></span>

<span data-ttu-id="5b76c-125">Creare una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5b76c-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="5b76c-126">esempio Hello crea 2 macchine virtuali denominate `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="5b76c-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="5b76c-127">Crea le chiavi SSH, se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5b76c-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="5b76c-128">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="5b76c-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="5b76c-129">Creare myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="5b76c-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="5b76c-130">Una volta hello macchina virtuale è stata creata, hello CLI di Azure Mostra toohello di informazioni simili seguente esempio: prendere nota di hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="5b76c-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="5b76c-131">Questo indirizzo è utilizzato tooaccess hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5b76c-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="5b76c-132">Creare myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="5b76c-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="5b76c-133">Prendere nota di hello `publicIpAddress` anche dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="5b76c-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="5b76c-134">Aprire la porta TCP hello per la connettività</span><span class="sxs-lookup"><span data-stu-id="5b76c-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="5b76c-135">Hello passaggio tooconfigure endpoint esterni, che consente di accedere in remoto hello Oracle DB, si esegue hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="5b76c-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="5b76c-136">Aprire la porta per myVM1</span><span class="sxs-lookup"><span data-stu-id="5b76c-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="5b76c-137">Risultato dovrebbe essere simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5b76c-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="5b76c-138">Aprire la porta per myVM2</span><span class="sxs-lookup"><span data-stu-id="5b76c-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="5b76c-139">Connettere la macchina toovirtual</span><span class="sxs-lookup"><span data-stu-id="5b76c-139">Connect toovirtual machine</span></span>

<span data-ttu-id="5b76c-140">Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="5b76c-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="5b76c-141">Sostituire l'indirizzo IP hello con hello `publicIpAddress` della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5b76c-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="5b76c-142">Creare il database su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="5b76c-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="5b76c-143">Hello software Oracle è già installato in un'immagine del Marketplace hello, pertanto la fase successiva hello database hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="5b76c-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="5b76c-144">primo passaggio Hello è in esecuzione come utente avanzato 'oracle' hello.</span><span class="sxs-lookup"><span data-stu-id="5b76c-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="5b76c-145">Crea database hello:</span><span class="sxs-lookup"><span data-stu-id="5b76c-145">create hello database:</span></span>

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
<span data-ttu-id="5b76c-146">Output dovrebbe essere simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="5b76c-146">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="5b76c-147">Impostare le variabili ORACLE_SID e ORACLE_HOME hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="5b76c-148">Facoltativamente, è possibile ORACLE_HOME e ORACLE_SID toohello .bashrc file aggiunto, in modo che queste impostazioni vengono salvate per gli accessi futuri.</span><span class="sxs-lookup"><span data-stu-id="5b76c-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="5b76c-149">Configurazioni di Data Guard</span><span class="sxs-lookup"><span data-stu-id="5b76c-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="5b76c-150">Abilitare la modalità archivelog su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="5b76c-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="5b76c-151">Abilitare la registrazione forzata e verificare che sia presente almeno un file di registro.</span><span class="sxs-lookup"><span data-stu-id="5b76c-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="5b76c-152">Creare i log di ripristino di standby</span><span class="sxs-lookup"><span data-stu-id="5b76c-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="5b76c-153">Accendere il Flashback (che effettuate ripristino hello molto precedenti) e impostare STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="5b76c-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="5b76c-154">Configurazione del servizio su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="5b76c-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="5b76c-155">Modificare o creare il file tnsnames.ora hello, che si trova nella cartella ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5b76c-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5b76c-156">Aggiungere hello seguenti voci</span><span class="sxs-lookup"><span data-stu-id="5b76c-156">Add hello following entries</span></span>

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

<span data-ttu-id="5b76c-157">Modificare o creare il file listener.ora hello, che si trova nella cartella ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5b76c-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5b76c-158">Aggiungere hello seguenti voci</span><span class="sxs-lookup"><span data-stu-id="5b76c-158">Add hello following entries</span></span>

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

<span data-ttu-id="5b76c-159">Avviare il listener hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="5b76c-160">Configurazione del servizio su myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="5b76c-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="5b76c-161">Modificare o creare il file tnsnames.ora hello, che si trova nella cartella ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5b76c-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5b76c-162">Aggiungere hello seguenti voci</span><span class="sxs-lookup"><span data-stu-id="5b76c-162">Add hello following entries</span></span>

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

<span data-ttu-id="5b76c-163">Modificare o creare il file listener.ora hello, che si trova nella cartella ORACLE_HOME\network\admin $</span><span class="sxs-lookup"><span data-stu-id="5b76c-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5b76c-164">Aggiungere hello seguenti voci</span><span class="sxs-lookup"><span data-stu-id="5b76c-164">Add hello following entries</span></span>

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

<span data-ttu-id="5b76c-165">Avviare il listener hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="5b76c-166">Abilitare il broker Data Guard</span><span class="sxs-lookup"><span data-stu-id="5b76c-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="5b76c-167">Ripristinare i database toomyVM2 (Standby)</span><span class="sxs-lookup"><span data-stu-id="5b76c-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="5b76c-168">Creare un file di parametro ' / tmp/initcdb1_stby.ora' con contenuto segue hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="5b76c-169">Creare cartelle</span><span class="sxs-lookup"><span data-stu-id="5b76c-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="5b76c-170">Creare il file di password</span><span class="sxs-lookup"><span data-stu-id="5b76c-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="5b76c-171">Avviare il database su myVM2</span><span class="sxs-lookup"><span data-stu-id="5b76c-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="5b76c-172">Ripristinare il database usando l'utilità RMAN</span><span class="sxs-lookup"><span data-stu-id="5b76c-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="5b76c-173">Eseguire i seguenti comandi in RMAN hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="5b76c-174">Abilitare il broker Data Guard</span><span class="sxs-lookup"><span data-stu-id="5b76c-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="5b76c-175">Configurare il broker Data Guard su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="5b76c-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="5b76c-176">Avviare Gestione di Data Guard hello e account di accesso tramite SYS e la password (do non utilizza l'autenticazione del sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="5b76c-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="5b76c-177">Eseguire i seguenti hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-177">Perform hello followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="5b76c-178">Verificare la configurazione hello</span><span class="sxs-lookup"><span data-stu-id="5b76c-178">Review hello configuration</span></span>
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

<span data-ttu-id="5b76c-179">Questa operazione completata l'installazione di Oracle Data Guard hello.</span><span class="sxs-lookup"><span data-stu-id="5b76c-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="5b76c-180">Nella sezione successiva Hello viene illustrato come tootest hello connettività e passando</span><span class="sxs-lookup"><span data-stu-id="5b76c-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="5b76c-181">Connettere il database dal computer client</span><span class="sxs-lookup"><span data-stu-id="5b76c-181">Connect database from client machine</span></span>

<span data-ttu-id="5b76c-182">Aggiornare o creare il file tnsnames.ora hello nel computer client che in genere si trova in $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="5b76c-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="5b76c-183">Sostituire l'indirizzo IP hello con il `publicIpAddress` per myVM1 e myVM2</span><span class="sxs-lookup"><span data-stu-id="5b76c-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="5b76c-184">Avviare sqlplus</span><span class="sxs-lookup"><span data-stu-id="5b76c-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="5b76c-185">Testare la configurazione di Data Guard</span><span class="sxs-lookup"><span data-stu-id="5b76c-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="5b76c-186">Passaggio di database su myVM1 (primario)</span><span class="sxs-lookup"><span data-stu-id="5b76c-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="5b76c-187">tooswitch da toostandby primario (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="5b76c-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="5b76c-188">Dovrebbe essere in grado di tooconnect toohello standby database</span><span class="sxs-lookup"><span data-stu-id="5b76c-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="5b76c-189">Avviare sqlplus</span><span class="sxs-lookup"><span data-stu-id="5b76c-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="5b76c-190">Cambio di database su myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="5b76c-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="5b76c-191">tooswitch nuovamente, eseguire i seguenti hello in myVM2</span><span class="sxs-lookup"><span data-stu-id="5b76c-191">tooswitch back, run hello followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="5b76c-192">Ancora una volta, dovrebbe essere in grado di tooconnect toohello principale database</span><span class="sxs-lookup"><span data-stu-id="5b76c-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="5b76c-193">Avviare sqlplus</span><span class="sxs-lookup"><span data-stu-id="5b76c-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="5b76c-194">Questa operazione completata hello installazione e configurazione della protezione dati in Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="5b76c-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="5b76c-195">Eliminare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="5b76c-195">Delete virtual machine</span></span>

<span data-ttu-id="5b76c-196">Quando non è più necessario, hello comando seguente può essere utilizzato tooremove hello, gruppo di risorse macchina virtuale, e tutte risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="5b76c-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5b76c-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b76c-197">Next steps</span></span>

[<span data-ttu-id="5b76c-198">Creare esercitazioni per macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="5b76c-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="5b76c-199">Esplorare gli esempi dell'interfaccia della riga di comando per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="5b76c-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
