---
title: accesso aaaReset sull'uso di macchine virtuali Linux di Azure hello estensione VMAccess | Documenti Microsoft
description: Reimpostare l'accesso in macchine virtuali Linux di Azure utilizzando hello estensione VMAccess.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="06627-103">Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="06627-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="06627-104">Questo articolo illustra come toouse hello Azure VMAcesss estensione toocheck o ripristinare un disco, reimpostare l'accesso utente, gestire gli account utente o reimpostare configurazione SSHD hello in Linux.</span><span class="sxs-lookup"><span data-stu-id="06627-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="06627-105">articolo Hello richiede:</span><span class="sxs-lookup"><span data-stu-id="06627-105">hello article requires:</span></span>

* <span data-ttu-id="06627-106">Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06627-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="06627-107">Hello [CLI di Azure](../../cli-install-nodejs.md) accesso `azure login`.</span><span class="sxs-lookup"><span data-stu-id="06627-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="06627-108">Hello Azure CLI *deve essere* modalità Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="06627-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="06627-109">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="06627-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="06627-110">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="06627-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="06627-111">[Azure CLI 1.0](#quick-commands): l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="06627-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="06627-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="06627-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="06627-113">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="06627-113">Quick commands</span></span>
<span data-ttu-id="06627-114">Esistono due modi toouse VMAccess in macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="06627-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="06627-115">Utilizzo di hello Azure CLI 1.0 e hello parametri obbligatori.</span><span class="sxs-lookup"><span data-stu-id="06627-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="06627-116">Usare file JSON non elaborati che VMAccess elabora e su cui basa le sue operazioni.</span><span class="sxs-lookup"><span data-stu-id="06627-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="06627-117">Per la sezione comando rapido hello, verrà toouse hello Azure CLI 1.0 `azure vm reset-access` metodo.</span><span class="sxs-lookup"><span data-stu-id="06627-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="06627-118">In hello esempi di comando seguente, sostituire i valori di hello che contengono "esempio" con i valori hello dal proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="06627-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="06627-119">Creare un gruppo di risorse e una VM Linux</span><span class="sxs-lookup"><span data-stu-id="06627-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="06627-120">Creare una VM Debian</span><span class="sxs-lookup"><span data-stu-id="06627-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="06627-121">Reimpostare la password radice</span><span class="sxs-lookup"><span data-stu-id="06627-121">Reset root password</span></span>
<span data-ttu-id="06627-122">password di tooreset hello radice:</span><span class="sxs-lookup"><span data-stu-id="06627-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="06627-123">Reimpostazione della chiave SSH</span><span class="sxs-lookup"><span data-stu-id="06627-123">SSH key reset</span></span>
<span data-ttu-id="06627-124">chiave SSH di hello tooreset di un utente non radice:</span><span class="sxs-lookup"><span data-stu-id="06627-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="06627-125">Creare un utente</span><span class="sxs-lookup"><span data-stu-id="06627-125">Create a user</span></span>
<span data-ttu-id="06627-126">toocreate un utente:</span><span class="sxs-lookup"><span data-stu-id="06627-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="06627-127">Rimuovere un utente</span><span class="sxs-lookup"><span data-stu-id="06627-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="06627-128">Reimpostare un disco SSHD</span><span class="sxs-lookup"><span data-stu-id="06627-128">Reset SSHD</span></span>
<span data-ttu-id="06627-129">configurazione di SSHD tooreset hello:</span><span class="sxs-lookup"><span data-stu-id="06627-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="06627-130">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="06627-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="06627-131">Estensione VMAccess definita:</span><span class="sxs-lookup"><span data-stu-id="06627-131">VMAccess defined:</span></span>
<span data-ttu-id="06627-132">disco Hello nella VM Linux verrà visualizzati errori.</span><span class="sxs-lookup"><span data-stu-id="06627-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="06627-133">È in qualche modo reimpostare la password radice hello per le VM Linux o eliminato la chiave privata SSH.</span><span class="sxs-lookup"><span data-stu-id="06627-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="06627-134">In tal caso, in giorni hello del Data Center di hello, si sarebbe necessario toodrive non esiste e quindi aprire hello KVM tooget alla console di server hello.</span><span class="sxs-lookup"><span data-stu-id="06627-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="06627-135">Hello estensione VMAccess Azure può essere paragonato a tale commutatore KVM consente tooaccess hello console tooreset accesso tooLinux o eseguire la manutenzione a livello di disco.</span><span class="sxs-lookup"><span data-stu-id="06627-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="06627-136">Per hello dettagliate procedura dettagliata, verrà esteso hello toouse di VMAccess, che utilizza il file JSON non elaborati.</span><span class="sxs-lookup"><span data-stu-id="06627-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="06627-137">Questi file JSON di VMAccess possono essere chiamati anche dai modelli di Azure.</span><span class="sxs-lookup"><span data-stu-id="06627-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="06627-138">Utilizzo di VMAccess toocheck o Ripristina hello disco di una VM Linux</span><span class="sxs-lookup"><span data-stu-id="06627-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="06627-139">Uso di VMAccess è possibile eseguire un sfck eseguire nel disco hello nella VM Linux.</span><span class="sxs-lookup"><span data-stu-id="06627-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="06627-140">È inoltre possibile eseguire una verifica del disco e ripristinarlo utilizzando un VMAccess.</span><span class="sxs-lookup"><span data-stu-id="06627-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="06627-141">toocheck quindi hello disco usare questo script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="06627-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="06627-142">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="06627-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="06627-143">Utilizzo di VMAccess tooreset utente accesso tooLinux</span><span class="sxs-lookup"><span data-stu-id="06627-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="06627-144">Se si smarrisce accesso tooroot nella VM Linux, è possibile avviare una password di VMAccess script tooreset hello radice.</span><span class="sxs-lookup"><span data-stu-id="06627-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="06627-145">la password radice hello tooreset, utilizzare questo script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="06627-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="06627-146">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="06627-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="06627-147">la chiave SSH hello tooreset di un utente non radice, utilizzare questo script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="06627-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="06627-148">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="06627-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="06627-149">Tramite gli account utente di VMAccess toomanage in Linux</span><span class="sxs-lookup"><span data-stu-id="06627-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="06627-150">VMAccess è uno script Python che può essere utenti toomanage utilizzati nella VM Linux senza accesso e l'utilizzo di sudo o hello account radice.</span><span class="sxs-lookup"><span data-stu-id="06627-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="06627-151">toocreate un utente, utilizzare questo script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="06627-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="06627-152">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="06627-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="06627-153">toodelete un utente, utilizzare questo script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="06627-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="06627-154">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="06627-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="06627-155">Utilizzando la configurazione di VMAccess tooreset hello SSHD</span><span class="sxs-lookup"><span data-stu-id="06627-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="06627-156">Se si apportano configurazione SSHD macchine virtuali Linux toohello di modifiche e connessione SSH hello chiudere prima la verifica delle modifiche di hello, può essere impedito SSH'ing nuovamente.</span><span class="sxs-lookup"><span data-stu-id="06627-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="06627-157">VMAccess può essere utilizzato tooreset hello SSHD configurazione tooa indietro configurazione valida senza accedere su SSH.</span><span class="sxs-lookup"><span data-stu-id="06627-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="06627-158">configurazione di SSHD hello tooreset utilizzare questo script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="06627-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="06627-159">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="06627-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="06627-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06627-160">Next steps</span></span>
<span data-ttu-id="06627-161">L'aggiornamento di Linux, utilizzando le estensioni di VMAccess di Azure è un metodo toomake viene modificato in una VM Linux in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="06627-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="06627-162">È anche possibile utilizzare strumenti come cloud init e modelli di Azure toomodify VM Linux all'avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="06627-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="06627-163">Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="06627-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="06627-164">Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux</span><span class="sxs-lookup"><span data-stu-id="06627-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="06627-165">Utilizzo di cloud init toocustomize una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="06627-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

