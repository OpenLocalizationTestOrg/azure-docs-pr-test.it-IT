---
title: aaaImplement Gate d'oro Oracle in una macchina virtuale Linux di Azure | Documenti Microsoft
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
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="aaacb-103">Implementare Oracle Golden Gate in una VM Linux di Azure</span><span class="sxs-lookup"><span data-stu-id="aaacb-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="aaacb-104">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="aaacb-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="aaacb-105">Questa guida descrive come toouse hello Azure CLI toodeploy Oracle 12C del database di immagine della raccolta hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="aaacb-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="aaacb-106">Questo documento viene illustrata la procedura dettagliata come toocreate, installare e configurare il controllo d'oro Oracle in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aaacb-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="aaacb-107">Prima di iniziare, verificare che tale hello che CLI di Azure è stato installato.</span><span class="sxs-lookup"><span data-stu-id="aaacb-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="aaacb-108">Per altre informazioni, vedere [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Guida all'installazione dell'interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="aaacb-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="aaacb-109">Preparare l'ambiente hello</span><span class="sxs-lookup"><span data-stu-id="aaacb-109">Prepare hello environment</span></span>

<span data-ttu-id="aaacb-110">installazione di Oracle d'oro Gate hello tooperform, è necessario toocreate due macchine virtuali di Azure su hello stesso set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="aaacb-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="aaacb-111">immagine del Marketplace Hello è utilizzare toocreate hello macchine virtuali è **Oracle: Oracle-Database-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="aaacb-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="aaacb-112">Inoltre necessario toobe familiarità con Unix editor vi e avere una conoscenza di base di x11 (Windows X).</span><span class="sxs-lookup"><span data-stu-id="aaacb-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="aaacb-113">di seguito Hello è un riepilogo della configurazione dell'ambiente hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="aaacb-114">**Sito primario**</span><span class="sxs-lookup"><span data-stu-id="aaacb-114">**Primary site**</span></span> | <span data-ttu-id="aaacb-115">**Sito di replica**</span><span class="sxs-lookup"><span data-stu-id="aaacb-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="aaacb-116">**Versione di Oracle**</span><span class="sxs-lookup"><span data-stu-id="aaacb-116">**Oracle release**</span></span> |<span data-ttu-id="aaacb-117">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="aaacb-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="aaacb-118">Oracle 12c Release 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="aaacb-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="aaacb-119">**Nome computer**</span><span class="sxs-lookup"><span data-stu-id="aaacb-119">**Machine name**</span></span> |<span data-ttu-id="aaacb-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="aaacb-120">myVM1</span></span> |<span data-ttu-id="aaacb-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="aaacb-121">myVM2</span></span> |
> | <span data-ttu-id="aaacb-122">**Sistema operativo**</span><span class="sxs-lookup"><span data-stu-id="aaacb-122">**Operating system**</span></span> |<span data-ttu-id="aaacb-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="aaacb-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="aaacb-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="aaacb-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="aaacb-125">**SID Oracle**</span><span class="sxs-lookup"><span data-stu-id="aaacb-125">**Oracle SID**</span></span> |<span data-ttu-id="aaacb-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="aaacb-126">CDB1</span></span> |<span data-ttu-id="aaacb-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="aaacb-127">CDB1</span></span> |
> | <span data-ttu-id="aaacb-128">**Schema di replica**</span><span class="sxs-lookup"><span data-stu-id="aaacb-128">**Replication schema**</span></span> |<span data-ttu-id="aaacb-129">TEST</span><span class="sxs-lookup"><span data-stu-id="aaacb-129">TEST</span></span>|<span data-ttu-id="aaacb-130">TEST</span><span class="sxs-lookup"><span data-stu-id="aaacb-130">TEST</span></span> |
> | <span data-ttu-id="aaacb-131">**Proprietario/replica Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="aaacb-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="aaacb-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="aaacb-132">C##GGADMIN</span></span> |<span data-ttu-id="aaacb-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="aaacb-133">REPUSER</span></span> |
> | <span data-ttu-id="aaacb-134">**Processo Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="aaacb-134">**Golden Gate process**</span></span> |<span data-ttu-id="aaacb-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="aaacb-135">EXTORA</span></span> |<span data-ttu-id="aaacb-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="aaacb-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="aaacb-137">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="aaacb-137">Sign in tooAzure</span></span> 

<span data-ttu-id="aaacb-138">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando.</span><span class="sxs-lookup"><span data-stu-id="aaacb-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="aaacb-139">Quindi seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="aaacb-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="aaacb-140">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="aaacb-140">Create a resource group</span></span>

<span data-ttu-id="aaacb-141">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="aaacb-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="aaacb-142">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="aaacb-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="aaacb-143">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso.</span><span class="sxs-lookup"><span data-stu-id="aaacb-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="aaacb-144">Creare un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="aaacb-144">Create an availability set</span></span>

<span data-ttu-id="aaacb-145">Hello riportata dopo il passaggio è facoltativo ma consigliato.</span><span class="sxs-lookup"><span data-stu-id="aaacb-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="aaacb-146">Per altre informazioni, vedere [Linee guida per i set di disponibilità di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="aaacb-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="aaacb-147">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="aaacb-147">Create a virtual machine</span></span>

<span data-ttu-id="aaacb-148">Creare una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="aaacb-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="aaacb-149">esempio Hello crea due macchine virtuali denominate `myVM1` e `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="aaacb-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="aaacb-150">Creare le chiavi SSH, se non esistono già in una posizione predefinita.</span><span class="sxs-lookup"><span data-stu-id="aaacb-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="aaacb-151">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="aaacb-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="aaacb-152">Creare myVM1 (primaria):</span><span class="sxs-lookup"><span data-stu-id="aaacb-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="aaacb-153">Dopo l'hello che macchina virtuale è stata creata, hello CLI di Azure Visualizza informazioni toohello simile esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="aaacb-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="aaacb-154">(Prendere nota di hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="aaacb-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="aaacb-155">Questo indirizzo è utilizzato tooaccess hello VM).</span><span class="sxs-lookup"><span data-stu-id="aaacb-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="aaacb-156">Creare myVM2 (replica):</span><span class="sxs-lookup"><span data-stu-id="aaacb-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="aaacb-157">Prendere nota di hello `publicIpAddress` anche dopo che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="aaacb-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="aaacb-158">Aprire la porta TCP hello per la connettività</span><span class="sxs-lookup"><span data-stu-id="aaacb-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="aaacb-159">passaggio successivo Hello è tooconfigure endpoint esterni, che consentono di database di Oracle tooaccess hello in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="aaacb-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="aaacb-160">tooconfigure hello endpoint esterni, eseguire hello i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="aaacb-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="aaacb-161">Aprire la porta hello per myVM1:</span><span class="sxs-lookup"><span data-stu-id="aaacb-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="aaacb-162">risultati Hello dovrebbero essere simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="aaacb-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="aaacb-163">Aprire la porta hello per myVM2:</span><span class="sxs-lookup"><span data-stu-id="aaacb-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="aaacb-164">Connettere la macchina virtuale di toohello</span><span class="sxs-lookup"><span data-stu-id="aaacb-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="aaacb-165">Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="aaacb-166">Sostituire l'indirizzo IP hello con hello `publicIpAddress` della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="aaacb-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="aaacb-167">Creare il database di hello in myVM1 (primario)</span><span class="sxs-lookup"><span data-stu-id="aaacb-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="aaacb-168">Hello software Oracle è già installato in un'immagine del Marketplace hello, pertanto la fase successiva hello database hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="aaacb-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="aaacb-169">Eseguire software hello come utente avanzato 'oracle' hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="aaacb-170">Crea database hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-170">Create hello database:</span></span>

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
<span data-ttu-id="aaacb-171">Output dovrebbe essere simile toohello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="aaacb-171">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="aaacb-172">Impostare le variabili ORACLE_SID e ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="aaacb-173">Facoltativamente, è possibile aggiungere file di .bashrc toohello ORACLE_HOME e ORACLE_SID, in modo che queste impostazioni vengono salvate per accessi futuri:</span><span class="sxs-lookup"><span data-stu-id="aaacb-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="aaacb-174">Avviare il listener Oracle</span><span class="sxs-lookup"><span data-stu-id="aaacb-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="aaacb-175">Creare database hello in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="aaacb-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="aaacb-176">Crea database hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-176">Create hello database:</span></span>

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
<span data-ttu-id="aaacb-177">Impostare le variabili ORACLE_SID e ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="aaacb-178">Facoltativamente, è possibile ORACLE_HOME e ORACLE_SID toohello .bashrc file aggiunto, in modo che queste impostazioni vengono salvate per accessi futuri.</span><span class="sxs-lookup"><span data-stu-id="aaacb-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="aaacb-179">Avviare il listener Oracle</span><span class="sxs-lookup"><span data-stu-id="aaacb-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="aaacb-180">Configurare Golden Gate</span><span class="sxs-lookup"><span data-stu-id="aaacb-180">Configure Golden Gate</span></span> 
<span data-ttu-id="aaacb-181">tooconfigure Gate d'oro, eseguire i passaggi di hello in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="aaacb-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="aaacb-182">Abilitare la modalità archivelog in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="aaacb-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="aaacb-183">Abilitare la registrazione forzata e verificare che sia presente almeno un file di registro.</span><span class="sxs-lookup"><span data-stu-id="aaacb-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="aaacb-184">Scaricare il software Golden Gate</span><span class="sxs-lookup"><span data-stu-id="aaacb-184">Download Golden Gate software</span></span>
<span data-ttu-id="aaacb-185">toodownload e preparare il software Oracle d'oro Gate hello, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="aaacb-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="aaacb-186">Scaricare hello **fbo_ggs_Linux_x64_shiphome.zip** file hello [pagina di download di Oracle d'oro Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="aaacb-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="aaacb-187">In hello Scarica titolo **12.x.x.x di Oracle GoldenGate per Oracle Linux x86-64**, dovrebbe esserci un set di toodownload file con estensione zip.</span><span class="sxs-lookup"><span data-stu-id="aaacb-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="aaacb-188">Dopo aver scaricato hello ZIP file tooyour client computer, utilizzare il protocollo Secure di copia (SCP) toocopy hello file tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="aaacb-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="aaacb-189">Spostare hello ZIP file toohello **/OPT** cartella.</span><span class="sxs-lookup"><span data-stu-id="aaacb-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="aaacb-190">Modificare quindi il proprietario di hello del file hello come segue:</span><span class="sxs-lookup"><span data-stu-id="aaacb-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="aaacb-191">Decomprimere il file di hello (installazione hello Linux decomprimere utilità se non è già installato):</span><span class="sxs-lookup"><span data-stu-id="aaacb-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="aaacb-192">Modificare l'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="aaacb-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="aaacb-193">Preparare client hello e VM toorun x11 (solo client di Windows)</span><span class="sxs-lookup"><span data-stu-id="aaacb-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="aaacb-194">Si tratta di un passaggio facoltativo.</span><span class="sxs-lookup"><span data-stu-id="aaacb-194">This is an optional step.</span></span> <span data-ttu-id="aaacb-195">Può essere ignorato se si usa un client Linux o se x11 è già configurato.</span><span class="sxs-lookup"><span data-stu-id="aaacb-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="aaacb-196">Download di PuTTY e Xming computer Windows tooyour:</span><span class="sxs-lookup"><span data-stu-id="aaacb-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="aaacb-197">Scaricare PuTTY</span><span class="sxs-lookup"><span data-stu-id="aaacb-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="aaacb-198">Scaricare Xming</span><span class="sxs-lookup"><span data-stu-id="aaacb-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="aaacb-199">Dopo aver installato PuTTY, in hello PuTTY cartella (ad esempio, c:\Programmi\Microsoft Files\PuTTY), eseguire puttygen.exe (Generatore di chiavi di PuTTY).</span><span class="sxs-lookup"><span data-stu-id="aaacb-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="aaacb-200">Nel generatore di chiavi PuTTY:</span><span class="sxs-lookup"><span data-stu-id="aaacb-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="aaacb-201">toogenerate hello un chiave, seleziona **genera** pulsante.</span><span class="sxs-lookup"><span data-stu-id="aaacb-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="aaacb-202">Copiare il contenuto di hello della chiave di hello (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="aaacb-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="aaacb-203">Seleziona hello **Salva la chiave privata** pulsante.</span><span class="sxs-lookup"><span data-stu-id="aaacb-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="aaacb-204">Ignorare l'avviso hello visualizzata e quindi seleziona **OK**.</span><span class="sxs-lookup"><span data-stu-id="aaacb-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Schermata della pagina di hello PuTTY generatore di chiavi](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="aaacb-206">Nella macchina virtuale eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="aaacb-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="aaacb-207">Creare un file denominato **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="aaacb-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="aaacb-208">Incollare il contenuto di hello della chiave di hello in questo file e quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aaacb-209">chiave di Hello deve contenere la stringa hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="aaacb-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="aaacb-210">Inoltre, il contenuto di hello della chiave hello deve essere una singola riga di testo.</span><span class="sxs-lookup"><span data-stu-id="aaacb-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="aaacb-211">Avviare PuTTY.</span><span class="sxs-lookup"><span data-stu-id="aaacb-211">Start PuTTY.</span></span> <span data-ttu-id="aaacb-212">In hello **categoria** riquadro, selezionare **connessione** > **SSH** > **Auth**. In hello **file di chiave privata per l'autenticazione** passare toohello chiave generata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="aaacb-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Schermata della pagina di impostare la chiave privata hello](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="aaacb-214">In hello **categoria** riquadro, selezionare **connessione** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="aaacb-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="aaacb-215">Selezionare quindi hello **inoltro X11 Enable** casella.</span><span class="sxs-lookup"><span data-stu-id="aaacb-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Schermata della pagina attiva X11 hello](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="aaacb-217">In hello **categoria** riquadro andare troppo**sessione**.</span><span class="sxs-lookup"><span data-stu-id="aaacb-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="aaacb-218">Immettere le informazioni host hello e quindi selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="aaacb-218">Enter hello host information, and then select **Open**.</span></span>

  ![Schermata della pagina della sessione hello](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="aaacb-220">Installare il software Golden Gate</span><span class="sxs-lookup"><span data-stu-id="aaacb-220">Install Golden Gate software</span></span>

<span data-ttu-id="aaacb-221">tooinstall Oracle d'oro Gate, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="aaacb-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="aaacb-222">Accedere come oracle.</span><span class="sxs-lookup"><span data-stu-id="aaacb-222">Sign in as oracle.</span></span> <span data-ttu-id="aaacb-223">(Deve essere in grado di toosign in senza che venga richiesta una password.) Assicurarsi che Xming sia in esecuzione prima di iniziare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="aaacb-224">Selezionare 'Oracle GoldenGate for Oracle Database 12c'.</span><span class="sxs-lookup"><span data-stu-id="aaacb-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="aaacb-225">Selezionare quindi **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="aaacb-225">Then select **Next** toocontinue.</span></span>

  ![Schermata della pagina di installazione selezionare hello programma di installazione](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="aaacb-227">Modificare il percorso di software hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-227">Change hello software location.</span></span> <span data-ttu-id="aaacb-228">Selezionare quindi hello **avvia Gestione** e immettere il percorso di database hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="aaacb-229">Selezionare **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="aaacb-229">Select **Next** toocontinue.</span></span>

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="aaacb-231">Cambiare directory inventario hello e quindi selezionare **Avanti** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="aaacb-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="aaacb-233">In hello **riepilogo** selezionare **installare** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="aaacb-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Schermata della pagina di installazione selezionare hello programma di installazione](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="aaacb-235">Potrebbe essere richiesta toorun uno script come 'radice'.</span><span class="sxs-lookup"><span data-stu-id="aaacb-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="aaacb-236">In questo caso, aprire una sessione separata, ssh toohello tooroot sudo, macchina virtuale, quindi eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="aaacb-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="aaacb-237">Selezionare **OK** per continuare.</span><span class="sxs-lookup"><span data-stu-id="aaacb-237">Select **OK** continue.</span></span>

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="aaacb-239">Al termine dell'installazione di hello, selezionare **Chiudi** processo hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="aaacb-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="aaacb-241">Configurare il servizio in myVM1 (primaria)</span><span class="sxs-lookup"><span data-stu-id="aaacb-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="aaacb-242">Creare o aggiornare il file tnsnames.ora hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-242">Create or update hello tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="aaacb-243">Creare hello d'oro Gate proprietario e agli account utente.</span><span class="sxs-lookup"><span data-stu-id="aaacb-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aaacb-244">account del proprietario Hello deve contenere il prefisso di C# #.</span><span class="sxs-lookup"><span data-stu-id="aaacb-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="aaacb-245">Creare account utente di prova d'oro Gate hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="aaacb-246">Configurare hello Estrai parametro file.</span><span class="sxs-lookup"><span data-stu-id="aaacb-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="aaacb-247">Avviare l'interfaccia della riga di comando di hello gate finale (ggsci):</span><span class="sxs-lookup"><span data-stu-id="aaacb-247">Start hello Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="aaacb-248">Aggiungere hello seguente toohello Estrai file dei parametri (mediante comandi vi).</span><span class="sxs-lookup"><span data-stu-id="aaacb-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="aaacb-249">Premere il tasto Esc, ':wq!'</span><span class="sxs-lookup"><span data-stu-id="aaacb-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="aaacb-250">file toosave.</span><span class="sxs-lookup"><span data-stu-id="aaacb-250">toosave file.</span></span> 

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
6. <span data-ttu-id="aaacb-251">REGISTER EXTRACT - estrazione integrata:</span><span class="sxs-lookup"><span data-stu-id="aaacb-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="aaacb-252">Configurare i checkpoint di estrazione e avviare l'estrazione in tempo reale:</span><span class="sxs-lookup"><span data-stu-id="aaacb-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="aaacb-253">In questo passaggio si trovare hello avvio SCN, che verrà utilizzato in un secondo momento, in un'altra sezione:</span><span class="sxs-lookup"><span data-stu-id="aaacb-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="aaacb-254">Configurare il servizio in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="aaacb-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="aaacb-255">Creare o aggiornare il file tnsnames.ora hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-255">Create or update hello tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="aaacb-256">Creare un account di replica:</span><span class="sxs-lookup"><span data-stu-id="aaacb-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="aaacb-257">Creare un account dell'utente di test di Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="aaacb-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="aaacb-258">REPLICAT parametro tooreplicate le modifiche al file:</span><span class="sxs-lookup"><span data-stu-id="aaacb-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="aaacb-259">Contenuto del file dei parametri REPORA:</span><span class="sxs-lookup"><span data-stu-id="aaacb-259">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="aaacb-260">Configurare un checkpoint replicat:</span><span class="sxs-lookup"><span data-stu-id="aaacb-260">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="aaacb-261">Configurare la replica di hello (myVM1 e myVM2)</span><span class="sxs-lookup"><span data-stu-id="aaacb-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="aaacb-262">1. Configurare la replica di hello in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="aaacb-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="aaacb-263">Aggiornare il file hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="aaacb-264">Quindi riavviare il servizio di gestione hello:</span><span class="sxs-lookup"><span data-stu-id="aaacb-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="aaacb-265">2. Configurare la replica di hello in myVM1 (primario)</span><span class="sxs-lookup"><span data-stu-id="aaacb-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="aaacb-266">Avviare il caricamento iniziale hello e controllare gli errori:</span><span class="sxs-lookup"><span data-stu-id="aaacb-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="aaacb-267">3. Configurare la replica di hello in myVM2 (replica)</span><span class="sxs-lookup"><span data-stu-id="aaacb-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="aaacb-268">Modificare hello numero SCN con hello ottenuto prima di:</span><span class="sxs-lookup"><span data-stu-id="aaacb-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="aaacb-269">replica Hello è iniziata ed è possibile eseguirne il test tramite l'inserimento di nuove tabelle tooTEST di record.</span><span class="sxs-lookup"><span data-stu-id="aaacb-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="aaacb-270">Visualizzare lo stato del processo e le informazioni di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="aaacb-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="aaacb-271">Visualizzazione dei report</span><span class="sxs-lookup"><span data-stu-id="aaacb-271">View reports</span></span>
<span data-ttu-id="aaacb-272">tooview segnala myVM1, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="aaacb-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="aaacb-273">tooview segnala myVM2, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="aaacb-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="aaacb-274">Visualizzare stato e cronologia</span><span class="sxs-lookup"><span data-stu-id="aaacb-274">View status and history</span></span>
<span data-ttu-id="aaacb-275">stato tooview e cronologia myVM1, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="aaacb-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="aaacb-276">stato tooview e cronologia myVM2, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="aaacb-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="aaacb-277">Questo completa hello installazione e configurazione del controllo d'oro in Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="aaacb-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="aaacb-278">Eliminare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="aaacb-278">Delete hello virtual machine</span></span>

<span data-ttu-id="aaacb-279">Quando non è più necessario, è possibile hello comando seguente gruppo di risorse utilizzato tooremove hello VM e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="aaacb-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="aaacb-280">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aaacb-280">Next steps</span></span>

[<span data-ttu-id="aaacb-281">Creare esercitazioni per macchine virtuali a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="aaacb-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="aaacb-282">Esplorare gli esempi dell'interfaccia della riga di comando per la distribuzione della VM</span><span class="sxs-lookup"><span data-stu-id="aaacb-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
