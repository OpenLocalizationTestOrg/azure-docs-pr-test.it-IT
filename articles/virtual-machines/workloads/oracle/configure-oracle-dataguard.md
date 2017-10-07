---
title: aaaImplement Oracle Data Guard in una macchina virtuale Linux di Azure | Documenti Microsoft
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
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="1bbc1-103">Implementare Oracle Data Guard su una macchina virtuale Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="1bbc1-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="1bbc1-104">CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="1bbc1-105">Questo articolo descrive come toouse CLI di Azure toodeploy un Oracle Database 12C database dall'immagine di hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="1bbc1-106">Questo articolo quindi illustra le fasi, come tooinstall e configurare Data Guard in una macchina virtuale di Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="1bbc1-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="1bbc1-107">Prima di iniziare, assicurarsi che l'interfaccia della riga di comando di Azure sia installata.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="1bbc1-108">Per ulteriori informazioni, vedere hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1bbc1-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="1bbc1-109">Preparare l'ambiente hello</span><span class="sxs-lookup"><span data-stu-id="1bbc1-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="1bbc1-110">Presupposti</span><span class="sxs-lookup"><span data-stu-id="1bbc1-110">Assumptions</span></span>

<span data-ttu-id="1bbc1-111">tooinstall Oracle Data Guard, è necessario toocreate due macchine virtuali di Azure su hello stesso set di disponibilità:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="1bbc1-112">Hello macchina virtuale primaria (myVM1) è un'istanza di Oracle in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="1bbc1-113">Hello che nella macchina virtuale standby (myVM2) è installato solo il software Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="1bbc1-114">immagine del Marketplace utilizzare toocreate hello macchine virtuali Hello è Oracle: Oracle-Database-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="1bbc1-115">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="1bbc1-115">Sign in tooAzure</span></span> 

<span data-ttu-id="1bbc1-116">Accedi tooyour sottoscrizione di Azure tramite hello [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="1bbc1-117">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="1bbc1-117">Create a resource group</span></span>

<span data-ttu-id="1bbc1-118">Creare un gruppo di risorse utilizzando hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1bbc1-119">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="1bbc1-120">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="1bbc1-121">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="1bbc1-121">Create an availability set</span></span>

<span data-ttu-id="1bbc1-122">Creare un set di disponibilità è un'operazione facoltativa, ma consigliata.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="1bbc1-123">Per altre informazioni, vedere [Linee guida per i set di disponibilità di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="1bbc1-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="1bbc1-124">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1bbc1-124">Create a virtual machine</span></span>

<span data-ttu-id="1bbc1-125">Creare una macchina virtuale utilizzando hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="1bbc1-126">esempio Hello crea due macchine virtuali denominate `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="1bbc1-127">Crea anche le chiavi SSH se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="1bbc1-128">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="1bbc1-129">Creare myVM1 (primaria):</span><span class="sxs-lookup"><span data-stu-id="1bbc1-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="1bbc1-130">Dopo aver creato hello macchina virtuale, Azure CLI Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="1bbc1-131">Si noti il valore di hello di `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="1bbc1-132">Utilizzare questo hello tooaccess indirizzo macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="1bbc1-133">Creare myVM2 (standby):</span><span class="sxs-lookup"><span data-stu-id="1bbc1-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="1bbc1-134">Si noti il valore di hello di `publicIpAddress` dopo aver creato myVM2.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="1bbc1-135">Aprire la porta TCP hello per la connettività</span><span class="sxs-lookup"><span data-stu-id="1bbc1-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="1bbc1-136">Questo passaggio consente di configurare gli endpoint esterni, quali database Oracle toohello di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="1bbc1-137">Aprire la porta hello per myVM1:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="1bbc1-138">risultato Hello dovrebbe essere simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="1bbc1-139">Aprire la porta hello per myVM2:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="1bbc1-140">Connettere la macchina virtuale di toohello</span><span class="sxs-lookup"><span data-stu-id="1bbc1-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="1bbc1-141">Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="1bbc1-142">Sostituire l'indirizzo IP hello con hello `publicIpAddress` valore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="1bbc1-143">Creare il database di hello in myVM1 (primario)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="1bbc1-144">Hello software Oracle è già installato in un'immagine del Marketplace hello, pertanto la fase successiva hello database hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="1bbc1-145">L'opzione utente avanzato Oracle toohello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="1bbc1-146">Crea database hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-146">Create hello database:</span></span>

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
<span data-ttu-id="1bbc1-147">Output dovrebbe essere simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="1bbc1-148">Impostare le variabili ORACLE_SID e ORACLE_HOME hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="1bbc1-149">Facoltativamente, è possibile aggiungere ORACLE_HOME e ORACLE_SID file /home/oracle/.bashrc toohello, in modo che queste impostazioni vengono salvate per gli account di accesso futuro:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="1bbc1-150">Configurare Data Guard</span><span class="sxs-lookup"><span data-stu-id="1bbc1-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="1bbc1-151">Abilitare la modalità archivelog in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="1bbc1-152">Abilitare la registrazione forzata e verificare che esista almeno un file di log:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="1bbc1-153">Creare i log di ripristino di standby:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="1bbc1-154">Accendere il Flashback (che rende molto più facile ripristino) e impostare STANDBY\_FILE\_tooauto di gestione.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="1bbc1-155">Chiudere quindi il comando SQL * Plus.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="1bbc1-156">Configurare il servizio in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="1bbc1-157">Modificare o creare il file tnsnames.ora hello, che si trova nella cartella di hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="1bbc1-158">Aggiungere hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-158">Add hello following entries:</span></span>

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

<span data-ttu-id="1bbc1-159">Modificare o creare il file listener.ora hello, che si trova nella cartella di hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="1bbc1-160">Aggiungere hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-160">Add hello following entries:</span></span>

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

<span data-ttu-id="1bbc1-161">Abilitare Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="1bbc1-162">Avviare il listener di hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="1bbc1-163">Configurare il servizio in myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="1bbc1-164">ToomyVM2 SSH:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="1bbc1-165">Accedere come Oracle:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="1bbc1-166">Modificare o creare il file tnsnames.ora hello, che si trova nella cartella di hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="1bbc1-167">Aggiungere hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-167">Add hello following entries:</span></span>

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

<span data-ttu-id="1bbc1-168">Modificare o creare il file listener.ora hello, che si trova nella cartella di hello $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="1bbc1-169">Aggiungere hello seguenti voci:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-169">Add hello following entries:</span></span>

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

<span data-ttu-id="1bbc1-170">Avviare il listener di hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="1bbc1-171">Ripristinare hello database toomyVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="1bbc1-172">Creare hello parametro file /tmp/initcdb1_stby.ora con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="1bbc1-173">Creare le cartelle:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="1bbc1-174">Creare un file di password:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="1bbc1-175">Avviare il database di hello myVM2:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="1bbc1-176">Ripristinare il database di hello utilizzando lo strumento RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="1bbc1-177">Eseguire i seguenti comandi in RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="1bbc1-178">Viene visualizzata messaggi simili toohello quando hello comando viene completato.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="1bbc1-179">Uscire da RMAN.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="1bbc1-180">Facoltativamente, è possibile aggiungere ORACLE_HOME e ORACLE_SID file /home/oracle/.bashrc toohello, in modo che queste impostazioni vengono salvate per gli account di accesso futuro:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="1bbc1-181">Abilitare Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="1bbc1-182">Configurare Data Guard Broker su myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="1bbc1-183">Avviare Data Guard Manage e accedere usando SYS e una password.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="1bbc1-184">Non usare l'autenticazione del sistema operativo. Eseguire l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="1bbc1-185">Verificare la configurazione: hello</span><span class="sxs-lookup"><span data-stu-id="1bbc1-185">Review hello configuration:</span></span>
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

<span data-ttu-id="1bbc1-186">È stata completata l'installazione di Oracle Data Guard hello.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="1bbc1-187">Nella sezione successiva Hello Mostra come tootest hello connettività e passare.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="1bbc1-188">La connessione a database hello da computer client hello</span><span class="sxs-lookup"><span data-stu-id="1bbc1-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="1bbc1-189">Aggiornare o creare il file tnsnames.ora hello nel computer client.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="1bbc1-190">Questo file si trova solitamente in $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="1bbc1-191">Sostituire gli indirizzi IP hello con il `publicIpAddress` valori per myVM1 e myVM2:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="1bbc1-192">Avviare il comando SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="1bbc1-193">Configurazione di test hello Data Guard</span><span class="sxs-lookup"><span data-stu-id="1bbc1-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="1bbc1-194">Passare database hello myVM1 (primario)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="1bbc1-195">tooswitch da toostandby primario (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="1bbc1-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="1bbc1-196">È ora possibile connettersi a database standby toohello.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="1bbc1-197">Avviare il comando SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="1bbc1-198">Passare database hello myVM2 (standby)</span><span class="sxs-lookup"><span data-stu-id="1bbc1-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="1bbc1-199">tooswitch, eseguire l'istruzione seguente hello su myVM2:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="1bbc1-200">In questo caso, dovrebbe ora essere in grado di tooconnect toohello primario database.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="1bbc1-201">Avviare il comando SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="1bbc1-202">Aver hello installazione e configurazione della protezione dati in Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbc1-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="1bbc1-203">Eliminare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="1bbc1-203">Delete hello virtual machine</span></span>

<span data-ttu-id="1bbc1-204">Quando si non è più necessario hello VM, è possibile utilizzare hello seguente gruppo di risorse di comando tooremove hello, macchina virtuale e tutte le relative risorse:</span><span class="sxs-lookup"><span data-stu-id="1bbc1-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1bbc1-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1bbc1-205">Next steps</span></span>

[<span data-ttu-id="1bbc1-206">Esercitazione: creare macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="1bbc1-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="1bbc1-207">Esplorare gli esempi dell'interfaccia della riga di comando di Azure per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="1bbc1-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
