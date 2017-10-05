---
title: Implementare Oracle Golden Gate in una VM Linux di Azure | Microsoft Docs
description: Implementare rapidamente Oracle Golden Gate nell'ambiente Azure.
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="26904-103">Implementare Oracle Golden Gate in una VM Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="26904-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="26904-104">L'interfaccia della riga di comando di Azure viene usata per creare e gestire le risorse di Azure dalla riga di comando o negli script.</span><span class="sxs-lookup"><span data-stu-id="26904-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="26904-105">Questa guida descrive nei dettagli come usare l'interfaccia della riga di comando di Azure per distribuire un database Oracle 12c dall'immagine della raccolta di Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="26904-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="26904-106">Questo documento descrive dettagliatamente come creare, installare e configurare Oracle Golden Gate in una VM Azure.</span><span class="sxs-lookup"><span data-stu-id="26904-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="26904-107">Prima di iniziare, verificare che l'interfaccia della riga di comando di Azure sia stata installata.</span><span class="sxs-lookup"><span data-stu-id="26904-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="26904-108">Per altre informazioni, vedere [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Guida all'installazione dell'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="26904-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="26904-109">Preparare l'ambiente</span><span class="sxs-lookup"><span data-stu-id="26904-109">Prepare the environment</span></span>

<span data-ttu-id="26904-110">Per installare Oracle Golden Gate è necessario creare due VM Azure nello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="26904-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="26904-111">L'immagine del Marketplace usata per creare le VM è **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="26904-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="26904-112">È anche necessario avere familiarità con l'editor Unix e nozioni di base di x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="26904-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="26904-113">Di seguito è riportato un riepilogo della configurazione dell'ambiente:</span><span class="sxs-lookup"><span data-stu-id="26904-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="26904-114">**Sito primario**</span><span class="sxs-lookup"><span data-stu-id="26904-114">**Primary site**</span></span> | <span data-ttu-id="26904-115">**Sito di replica**</span><span class="sxs-lookup"><span data-stu-id="26904-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="26904-116">**Versione di Oracle**</span><span class="sxs-lookup"><span data-stu-id="26904-116">**Oracle release**</span></span> |<span data-ttu-id="26904-117">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="26904-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="26904-118">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="26904-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="26904-119">**Nome computer**</span><span class="sxs-lookup"><span data-stu-id="26904-119">**Machine name**</span></span> |<span data-ttu-id="26904-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="26904-120">myVM1</span></span> |<span data-ttu-id="26904-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="26904-121">myVM2</span></span> |
> | <span data-ttu-id="26904-122">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="26904-122">**Operating system**</span></span> |<span data-ttu-id="26904-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="26904-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="26904-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="26904-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="26904-125">**SID Oracle**</span><span class="sxs-lookup"><span data-stu-id="26904-125">**Oracle SID**</span></span> |<span data-ttu-id="26904-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="26904-126">CDB1</span></span> |<span data-ttu-id="26904-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="26904-127">CDB1</span></span> |
> | <span data-ttu-id="26904-128">**Schema di replica**</span><span class="sxs-lookup"><span data-stu-id="26904-128">**Replication schema**</span></span> |<span data-ttu-id="26904-129">TEST</span><span class="sxs-lookup"><span data-stu-id="26904-129">TEST</span></span>|<span data-ttu-id="26904-130">TEST</span><span class="sxs-lookup"><span data-stu-id="26904-130">TEST</span></span> |
> | <span data-ttu-id="26904-131">**Proprietario/replica Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="26904-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="26904-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="26904-132">C##GGADMIN</span></span> |<span data-ttu-id="26904-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="26904-133">REPUSER</span></span> |
> | <span data-ttu-id="26904-134">**Processo Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="26904-134">**Golden Gate process**</span></span> |<span data-ttu-id="26904-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="26904-135">EXTORA</span></span> |<span data-ttu-id="26904-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="26904-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="26904-137">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="26904-137">Sign in to Azure</span></span> 

<span data-ttu-id="26904-138">Accedere alla sottoscrizione di Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="26904-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="26904-139">Seguire quindi le istruzioni visualizzate sullo schermo.</span><span class="sxs-lookup"><span data-stu-id="26904-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="26904-140">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="26904-140">Create a resource group</span></span>

<span data-ttu-id="26904-141">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="26904-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="26904-142">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="26904-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="26904-143">Nell'esempio seguente viene creato un gruppo di risorse denominato `myResourceGroup` nella posizione `westus`.</span><span class="sxs-lookup"><span data-stu-id="26904-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="26904-144">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="26904-144">Create an availability set</span></span>

<span data-ttu-id="26904-145">Il passaggio seguente è facoltativo ma consigliato.</span><span class="sxs-lookup"><span data-stu-id="26904-145">The following step is optional but recommended.</span></span> <span data-ttu-id="26904-146">Per altre informazioni, vedere [Linee guida per i set di disponibilità di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="26904-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="26904-147">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="26904-147">Create a virtual machine</span></span>

<span data-ttu-id="26904-148">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="26904-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="26904-149">Nell'esempio seguente vengono create due VM chiamate `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="26904-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="26904-150">Creare le chiavi SSH, se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="26904-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="26904-151">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="26904-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="26904-152">Creare myVM1 (primaria):</span><span class="sxs-lookup"><span data-stu-id="26904-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="26904-153">Dopo aver creato la VM, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="26904-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="26904-154">Prendere nota di `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="26904-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="26904-155">Questo indirizzo viene usato per accedere alla VM.</span><span class="sxs-lookup"><span data-stu-id="26904-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="26904-156">Creare myVM2 (replica):</span><span class="sxs-lookup"><span data-stu-id="26904-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="26904-157">Prendere nota anche di `publicIpAddress` dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="26904-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="26904-158">Aprire la porta TCP per la connettività</span><span class="sxs-lookup"><span data-stu-id="26904-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="26904-159">Il passaggio successivo consiste nel configurare gli endpoint esterni, che consentono di accedere al database Oracle in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="26904-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="26904-160">Per configurare gli endpoint esterni, eseguire questi comandi.</span><span class="sxs-lookup"><span data-stu-id="26904-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="26904-161">Aprire la porta per myVM1:</span><span class="sxs-lookup"><span data-stu-id="26904-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="26904-162">I risultati saranno simili alla risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="26904-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="26904-163">Aprire la porta per myVM2:</span><span class="sxs-lookup"><span data-stu-id="26904-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="26904-164">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="26904-164">Connect to the virtual machine</span></span>

<span data-ttu-id="26904-165">Usare il comando seguente per creare una sessione SSH con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="26904-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="26904-166">Sostituire l'indirizzo IP con `publicIpAddress` della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="26904-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="26904-167">Creare il database in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="26904-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="26904-168">Il software Oracle è già installato nell'immagine di Marketplace, pertanto il passaggio successivo è installare il database.</span><span class="sxs-lookup"><span data-stu-id="26904-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="26904-169">Eseguire il software come utente con privilegi avanzati 'oracle':</span><span class="sxs-lookup"><span data-stu-id="26904-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="26904-170">Creare il database:</span><span class="sxs-lookup"><span data-stu-id="26904-170">Create the database:</span></span>

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
<span data-ttu-id="26904-171">Gli output saranno simili alla risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="26904-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="26904-172">Impostare le variabili ORACLE_SID e ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="26904-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="26904-173">È anche possibile aggiungere le variabili ORACLE_HOME e ORACLE_SID al file con estensione bashrc, in modo da salvare queste impostazioni per un accesso futuro:</span><span class="sxs-lookup"><span data-stu-id="26904-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="26904-174">Avviare il listener Oracle</span><span class="sxs-lookup"><span data-stu-id="26904-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="26904-175">Creare il database in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="26904-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="26904-176">Creare il database:</span><span class="sxs-lookup"><span data-stu-id="26904-176">Create the database:</span></span>

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
<span data-ttu-id="26904-177">Impostare le variabili ORACLE_SID e ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="26904-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="26904-178">È anche possibile aggiungere le variabili ORACLE_HOME e ORACLE_SID al file con estensione bashrc, in modo da salvare queste impostazioni per un accesso futuro.</span><span class="sxs-lookup"><span data-stu-id="26904-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="26904-179">Avviare il listener Oracle</span><span class="sxs-lookup"><span data-stu-id="26904-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="26904-180">Configurare Golden Gate</span><span class="sxs-lookup"><span data-stu-id="26904-180">Configure Golden Gate</span></span> 
<span data-ttu-id="26904-181">Per configurare Golden Gate, eseguire i passaggi di questa sezione.</span><span class="sxs-lookup"><span data-stu-id="26904-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="26904-182">Abilitare la modalità archivelog in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="26904-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="26904-183">Abilitare la registrazione forzata e verificare che sia presente almeno un file di registro.</span><span class="sxs-lookup"><span data-stu-id="26904-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="26904-184">Scaricare il software Golden Gate</span><span class="sxs-lookup"><span data-stu-id="26904-184">Download Golden Gate software</span></span>
<span data-ttu-id="26904-185">Per scaricare e preparare il software Oracle Golden Gate, completare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="26904-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="26904-186">Scaricare il file **fbo_ggs_Linux_x64_shiphome.zip** dalla [pagina di download di Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="26904-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="26904-187">Sotto il titolo di download **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64** è presente un set di file ZIP da scaricare.</span><span class="sxs-lookup"><span data-stu-id="26904-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="26904-188">Dopo aver scaricato i file ZIP nel computer client, usare il protocollo per la copia di sicurezza, SCP, per copiare i file nella macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="26904-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="26904-189">Spostare i file ZIP nella cartella **/opt**.</span><span class="sxs-lookup"><span data-stu-id="26904-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="26904-190">Modificare quindi il proprietario dei file come segue:</span><span class="sxs-lookup"><span data-stu-id="26904-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="26904-191">Decomprimere i file, per farlo installare l'utilità di decompressione di Linux se non è già installata:</span><span class="sxs-lookup"><span data-stu-id="26904-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="26904-192">Modificare l'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="26904-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="26904-193">Preparare il client e la VM per l'esecuzione di x11, solo per i client di Windows</span><span class="sxs-lookup"><span data-stu-id="26904-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="26904-194">Si tratta di un passaggio facoltativo.</span><span class="sxs-lookup"><span data-stu-id="26904-194">This is an optional step.</span></span> <span data-ttu-id="26904-195">Può essere ignorato se si usa un client Linux o se x11 è già configurato.</span><span class="sxs-lookup"><span data-stu-id="26904-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="26904-196">Scaricare PuTTY e Xming sul computer Windows:</span><span class="sxs-lookup"><span data-stu-id="26904-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * [<span data-ttu-id="26904-197">Scaricare PuTTY</span><span class="sxs-lookup"><span data-stu-id="26904-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="26904-198">Scaricare Xming</span><span class="sxs-lookup"><span data-stu-id="26904-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="26904-199">Dopo aver installato PuTTY, nella cartella PuTTY, ad esempio, C:\Programmi\PuTTY, eseguire puttygen.exe, il generatore di chiavi PuTTY.</span><span class="sxs-lookup"><span data-stu-id="26904-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="26904-200">Nel generatore di chiavi PuTTY:</span><span class="sxs-lookup"><span data-stu-id="26904-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="26904-201">Per generare una chiave, selezionare il pulsante **Genera**.</span><span class="sxs-lookup"><span data-stu-id="26904-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="26904-202">Copiare il contenuto della chiave con **Ctrl+C**.</span><span class="sxs-lookup"><span data-stu-id="26904-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="26904-203">Selezionare il pulsante **Save private key** (Salva la chiave privata).</span><span class="sxs-lookup"><span data-stu-id="26904-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="26904-204">Ignorare l'avviso che viene visualizzato e quindi selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="26904-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![Schermata della pagina del generatore di chiavi PuTTY](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="26904-206">Nella macchina virtuale eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="26904-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="26904-207">Creare un file denominato **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="26904-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="26904-208">Incollare il contenuto della chiave in questo file e quindi salvare il file.</span><span class="sxs-lookup"><span data-stu-id="26904-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="26904-209">La chiave deve contenere la stringa `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="26904-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="26904-210">In aggiunta, il contenuto della chiave deve essere una singola riga di testo.</span><span class="sxs-lookup"><span data-stu-id="26904-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="26904-211">Avviare PuTTY.</span><span class="sxs-lookup"><span data-stu-id="26904-211">Start PuTTY.</span></span> <span data-ttu-id="26904-212">Nel pannello **Categoria** selezionare **Connessione** > **SSH** > **Autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="26904-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="26904-213">Nella casella **Private key file for authentication** (File della chiave privata per l'autenticazione) individuare la chiave generata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="26904-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![Schermata della pagina di impostazione della chiave privata](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="26904-215">Nel pannello **Categoria** selezionare **Connessione** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="26904-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="26904-216">Selezionare quindi la casella **Enable X11 forwarding** (Abilita l'inoltro di X11).</span><span class="sxs-lookup"><span data-stu-id="26904-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![Schermata della pagina di abilitazione di X11](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="26904-218">Nel pannello **Categoria** andare in **Sessione**.</span><span class="sxs-lookup"><span data-stu-id="26904-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="26904-219">Immettere le informazioni sull'host e quindi selezionare **Apri**.</span><span class="sxs-lookup"><span data-stu-id="26904-219">Enter the host information, and then select **Open**.</span></span>

  ![Screenshot della pagina della sessione](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="26904-221">Installare il software Golden Gate</span><span class="sxs-lookup"><span data-stu-id="26904-221">Install Golden Gate software</span></span>

<span data-ttu-id="26904-222">Per installare Oracle Golden Gate seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26904-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="26904-223">Accedere come oracle.</span><span class="sxs-lookup"><span data-stu-id="26904-223">Sign in as oracle.</span></span> <span data-ttu-id="26904-224">L'accesso non dovrebbe richiedere una password. Assicurarsi che Xming sia in esecuzione prima di iniziare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="26904-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="26904-225">Selezionare 'Oracle GoldenGate for Oracle Database 12c'.</span><span class="sxs-lookup"><span data-stu-id="26904-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="26904-226">Selezionare quindi **Next** (Avanti) per continuare.</span><span class="sxs-lookup"><span data-stu-id="26904-226">Then select **Next** to continue.</span></span>

  ![Screenshot della pagina Select Installation Option (Selezionare l'opzione di installazione) del programma di installazione](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="26904-228">Modificare il percorso del software.</span><span class="sxs-lookup"><span data-stu-id="26904-228">Change the software location.</span></span> <span data-ttu-id="26904-229">Selezionare quindi **Start Manager** (Gestione avvio) e immettere il percorso del database.</span><span class="sxs-lookup"><span data-stu-id="26904-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="26904-230">Selezionare **Avanti** per continuare.</span><span class="sxs-lookup"><span data-stu-id="26904-230">Select **Next** to continue.</span></span>

  ![Screenshot della pagina di selezione dell'installazione](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="26904-232">Modificare la directory di inventario e quindi selezionare **Next** (Avanti) per continuare.</span><span class="sxs-lookup"><span data-stu-id="26904-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![Screenshot della pagina di selezione dell'installazione](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="26904-234">Nella schermata **Summary** (Riepilogo) selezionare **Install** (Installa) per continuare.</span><span class="sxs-lookup"><span data-stu-id="26904-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![Screenshot della pagina Select Installation Option (Selezionare l'opzione di installazione) del programma di installazione](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="26904-236">Potrebbe essere richiesto di eseguire uno script come 'root'.</span><span class="sxs-lookup"><span data-stu-id="26904-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="26904-237">In questo caso aprire una sessione separata, connettersi alla VM tramite SSH, passare a root tramite sudo e quindi eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="26904-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="26904-238">Selezionare **OK** per continuare.</span><span class="sxs-lookup"><span data-stu-id="26904-238">Select **OK** continue.</span></span>

  ![Screenshot della pagina di selezione dell'installazione](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="26904-240">Al termine dell'installazione, selezionare **Close** (Chiudi) per completare il processo.</span><span class="sxs-lookup"><span data-stu-id="26904-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![Screenshot della pagina di selezione dell'installazione](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="26904-242">Configurare il servizio in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="26904-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="26904-243">Creare o aggiornare il file tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="26904-243">Create or update the tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="26904-244">Creare gli account proprietario e utente di Golden Gate.</span><span class="sxs-lookup"><span data-stu-id="26904-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="26904-245">L'account proprietario deve avere il prefisso C##.</span><span class="sxs-lookup"><span data-stu-id="26904-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="26904-246">Creare l'account dell'utente di test di Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="26904-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="26904-247">Configurare il file dei parametri EXTRACT.</span><span class="sxs-lookup"><span data-stu-id="26904-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="26904-248">Avviare l'interfaccia della riga di comando di Golden Gate (ggsci):</span><span class="sxs-lookup"><span data-stu-id="26904-248">Start the Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="26904-249">Aggiungere quanto segue al file dei parametri EXTRACT usando i comandi vi.</span><span class="sxs-lookup"><span data-stu-id="26904-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="26904-250">Premere il tasto Esc, ':wq!'</span><span class="sxs-lookup"><span data-stu-id="26904-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="26904-251">per salvare il file.</span><span class="sxs-lookup"><span data-stu-id="26904-251">to save file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="26904-252">REGISTER EXTRACT - estrazione integrata:</span><span class="sxs-lookup"><span data-stu-id="26904-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="26904-253">Configurare i checkpoint di estrazione e avviare l'estrazione in tempo reale:</span><span class="sxs-lookup"><span data-stu-id="26904-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="26904-254">In questo passaggio è presente il parametro SCN iniziale, che verrà usato in un secondo momento in un'altra sezione:</span><span class="sxs-lookup"><span data-stu-id="26904-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="26904-255">Configurare il servizio in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="26904-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="26904-256">Creare o aggiornare il file tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="26904-256">Create or update the tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="26904-257">Creare un account di replica:</span><span class="sxs-lookup"><span data-stu-id="26904-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="26904-258">Creare un account dell'utente di test di Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="26904-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="26904-259">File dei parametri REPLICAT per replicare le modifiche:</span><span class="sxs-lookup"><span data-stu-id="26904-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="26904-260">Contenuto del file dei parametri REPORA:</span><span class="sxs-lookup"><span data-stu-id="26904-260">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="26904-261">Configurare un checkpoint replicat:</span><span class="sxs-lookup"><span data-stu-id="26904-261">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="26904-262">Configurare la replica (myVM1 e myVM2)</span><span class="sxs-lookup"><span data-stu-id="26904-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="26904-263">1. Configurare la replica in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="26904-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="26904-264">Aggiornare il file con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="26904-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="26904-265">Riavviare quindi il servizio di gestione:</span><span class="sxs-lookup"><span data-stu-id="26904-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="26904-266">2. Configurare la replica in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="26904-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="26904-267">Avviare il caricamento iniziale e verificare gli errori:</span><span class="sxs-lookup"><span data-stu-id="26904-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="26904-268">3. Configurare la replica in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="26904-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="26904-269">Sostituire il numero SCN con il numero ottenuto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="26904-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="26904-270">La replica è iniziata ed è possibile testarla inserendo nuovi record nelle tabelle TEST.</span><span class="sxs-lookup"><span data-stu-id="26904-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="26904-271">Visualizzare lo stato del processo e le informazioni di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="26904-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="26904-272">Visualizzazione dei report</span><span class="sxs-lookup"><span data-stu-id="26904-272">View reports</span></span>
<span data-ttu-id="26904-273">Per visualizzare i report in myVM1, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="26904-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="26904-274">Per visualizzare i report in myVM2, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="26904-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="26904-275">Visualizzare stato e cronologia</span><span class="sxs-lookup"><span data-stu-id="26904-275">View status and history</span></span>
<span data-ttu-id="26904-276">Per visualizzare stato e cronologia in myVM1, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="26904-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="26904-277">Per visualizzare stato e cronologia in myVM2, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="26904-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="26904-278">Questa operazione completa l'installazione e la configurazione di Golden Gate nell'ambiente Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="26904-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="26904-279">Eliminare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="26904-279">Delete the virtual machine</span></span>

<span data-ttu-id="26904-280">Il comando seguente consente di rimuovere il gruppo di risorse, la VM e tutte le risorse correlate quando non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="26904-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="26904-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26904-281">Next steps</span></span>

[<span data-ttu-id="26904-282">Creare esercitazioni per macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="26904-282">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="26904-283">Esplorare gli esempi dell'interfaccia della riga di comando per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="26904-283">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
