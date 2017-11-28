---
title: aaaReset accesso tooan VM Linux di Azure | Documenti Microsoft
description: Come gli utenti toomanage e Reimposta accesso sull'uso di macchine virtuali Linux hello estensione VMAccess e hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="b17e7-103">Gestire utenti, SSH e controllo o i dischi di ripristino sull'uso di macchine virtuali Linux hello estensione VMAccess con hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b17e7-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="b17e7-104">disco Hello nella VM Linux verrà visualizzati errori.</span><span class="sxs-lookup"><span data-stu-id="b17e7-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="b17e7-105">È in qualche modo reimpostare la password radice hello per le VM Linux o eliminato la chiave privata SSH.</span><span class="sxs-lookup"><span data-stu-id="b17e7-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="b17e7-106">In tal caso, in giorni hello del Data Center di hello, si sarebbe necessario toodrive non esiste e quindi aprire hello KVM tooget alla console di server hello.</span><span class="sxs-lookup"><span data-stu-id="b17e7-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="b17e7-107">Hello estensione VMAccess Azure può essere paragonato a tale commutatore KVM consente tooaccess hello console tooreset accesso tooLinux o eseguire la manutenzione a livello di disco.</span><span class="sxs-lookup"><span data-stu-id="b17e7-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="b17e7-108">Questo articolo illustra come toouse hello toocheck estensione VMAccess Azure o ripristinare un disco, reimpostare l'accesso utente, gestire gli account utente o Reimposta configurazione SSH hello in Linux.</span><span class="sxs-lookup"><span data-stu-id="b17e7-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="b17e7-109">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b17e7-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="b17e7-110">Modi toouse hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="b17e7-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="b17e7-111">Esistono due modi, che è possibile utilizzare l'estensione VMAccess hello in macchine virtuali Linux:</span><span class="sxs-lookup"><span data-stu-id="b17e7-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="b17e7-112">Utilizzare hello Azure CLI 2.0 e i parametri di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="b17e7-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="b17e7-113">[JSON non elaborata di utilizzare i file che il processo di estensione VMAccess hello](#use-json-files-and-the-vmaccess-extension) e quindi agire su.</span><span class="sxs-lookup"><span data-stu-id="b17e7-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="b17e7-114">Dopo l'utilizzo di esempi di Hello [utente vm az](/cli/azure/vm/user) comandi.</span><span class="sxs-lookup"><span data-stu-id="b17e7-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="b17e7-115">tooperform questi passaggi, è necessario hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b17e7-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="b17e7-116">Ripristinare la chiave SSH</span><span class="sxs-lookup"><span data-stu-id="b17e7-116">Reset SSH key</span></span>
<span data-ttu-id="b17e7-117">esempio Hello Reimposta chiave SSH hello per utente hello `azureuser` nella macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b17e7-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="b17e7-118">Reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="b17e7-118">Reset password</span></span>
<span data-ttu-id="b17e7-119">esempio Hello Reimposta password hello hello utente `azureuser` nella macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b17e7-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="b17e7-120">Riavviare SSH</span><span class="sxs-lookup"><span data-stu-id="b17e7-120">Restart SSH</span></span>
<span data-ttu-id="b17e7-121">esempio Hello riavvia il daemon SSH hello e reimposta hello i valori di toodefault configurazione SSH in una macchina virtuale denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b17e7-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="b17e7-122">Creare un utente</span><span class="sxs-lookup"><span data-stu-id="b17e7-122">Create a user</span></span>
<span data-ttu-id="b17e7-123">esempio Hello crea un utente denominato `myNewUser` usando una chiave SSH per l'autenticazione nella macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b17e7-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="b17e7-124">Eliminare un utente</span><span class="sxs-lookup"><span data-stu-id="b17e7-124">Delete a user</span></span>
<span data-ttu-id="b17e7-125">esempio Hello Elimina un utente denominato `myNewUser` nella macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="b17e7-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="b17e7-126">Utilizzare i file JSON e hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="b17e7-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="b17e7-127">seguono esempi Hello utilizza file JSON non elaborati.</span><span class="sxs-lookup"><span data-stu-id="b17e7-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="b17e7-128">Utilizzare [az vm estensione set](/cli/azure/vm/extension#set) toothen chiamare i file JSON.</span><span class="sxs-lookup"><span data-stu-id="b17e7-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="b17e7-129">Questi file JSON possono essere chiamati anche dai modelli di Azure.</span><span class="sxs-lookup"><span data-stu-id="b17e7-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="b17e7-130">Ripristinare l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="b17e7-130">Reset user access</span></span>
<span data-ttu-id="b17e7-131">Se si smarrisce accesso tooroot nella VM Linux, è possibile avviare un tooreset script VMAccess chiave SSH o la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="b17e7-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="b17e7-132">chiave pubblica SSH hello di tooreset di un utente, creare un file denominato `reset_ssh_key.json` e aggiungere le impostazioni nel seguente formato hello.</span><span class="sxs-lookup"><span data-stu-id="b17e7-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="b17e7-133">Sostituire i valori per hello `username` e `ssh_key` parametri:</span><span class="sxs-lookup"><span data-stu-id="b17e7-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="b17e7-134">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="b17e7-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="b17e7-135">tooreset una password utente, creare un file denominato `reset_user_password.json` e aggiungere le impostazioni nel seguente formato hello.</span><span class="sxs-lookup"><span data-stu-id="b17e7-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="b17e7-136">Sostituire i valori per hello `username` e `password` parametri:</span><span class="sxs-lookup"><span data-stu-id="b17e7-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="b17e7-137">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="b17e7-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="b17e7-138">Riavviare SSH</span><span class="sxs-lookup"><span data-stu-id="b17e7-138">Restart SSH</span></span>
<span data-ttu-id="b17e7-139">toorestart hello daemon SSH e reimpostare i valori hello SSH configurazione toodefault, creare un file denominato `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="b17e7-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="b17e7-140">Aggiungere hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="b17e7-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="b17e7-141">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="b17e7-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="b17e7-142">Gestire gli utenti</span><span class="sxs-lookup"><span data-stu-id="b17e7-142">Manage users</span></span>

<span data-ttu-id="b17e7-143">toocreate un utente che usa una chiave SSH per l'autenticazione, creare un file denominato `create_new_user.json` e aggiungere le impostazioni nel seguente formato hello.</span><span class="sxs-lookup"><span data-stu-id="b17e7-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="b17e7-144">Sostituire i valori per hello `username` e `ssh_key` parametri:</span><span class="sxs-lookup"><span data-stu-id="b17e7-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="b17e7-145">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="b17e7-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="b17e7-146">toodelete un utente, creare un file denominato `delete_user.json` e aggiungere hello dopo contenuto.</span><span class="sxs-lookup"><span data-stu-id="b17e7-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="b17e7-147">Sostituire il valore per hello `remove_user` parametro:</span><span class="sxs-lookup"><span data-stu-id="b17e7-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="b17e7-148">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="b17e7-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="b17e7-149">Verificare o riparare hello disco</span><span class="sxs-lookup"><span data-stu-id="b17e7-149">Check or repair hello disk</span></span>
<span data-ttu-id="b17e7-150">Uso di VMAccess è anche possibile controllare e ripristinare un disco di cui sono stati aggiunti toohello VM Linux.</span><span class="sxs-lookup"><span data-stu-id="b17e7-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="b17e7-151">toocheck quindi hello disco, creare un file denominato `disk_check_repair.json` e aggiungere le impostazioni nel seguente formato hello.</span><span class="sxs-lookup"><span data-stu-id="b17e7-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="b17e7-152">Sostituire il valore per nome hello `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="b17e7-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="b17e7-153">Eseguire lo script di VMAccess hello con:</span><span class="sxs-lookup"><span data-stu-id="b17e7-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="b17e7-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b17e7-154">Next steps</span></span>
<span data-ttu-id="b17e7-155">L'aggiornamento di Linux mediante hello estensione VMAccess Azure è un metodo toomake viene modificato in una VM Linux in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b17e7-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="b17e7-156">È anche possibile usare strumenti come cloud-inizializzazione e Gestione risorse di Azure modelli toomodify VM Linux all'avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="b17e7-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="b17e7-157">Estensioni e funzionalità delle macchine virtuali per Linux</span><span class="sxs-lookup"><span data-stu-id="b17e7-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="b17e7-158">Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux</span><span class="sxs-lookup"><span data-stu-id="b17e7-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b17e7-159">Utilizzo di cloud init toocustomize una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="b17e7-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

