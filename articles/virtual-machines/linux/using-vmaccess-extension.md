---
title: Reimpostare l'accesso a una macchina virtuale Linux di Azure | Microsoft Docs
description: Come gestire gli utenti e ripristinare l'accesso in VM Linux mediante l'estensione VMAccess e l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: 587c73278a9a92776276a811c5c4c8d3db773de3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a><span data-ttu-id="6990e-103">Gestire utenti, SSH e dischi di controllo o di ripristino in VM Linux mediante l'estensione VMAccess con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6990e-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span></span>
<span data-ttu-id="6990e-104">Il disco della VM Linux genera errori.</span><span class="sxs-lookup"><span data-stu-id="6990e-104">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="6990e-105">In qualche modo la password radice della VM Linux è stata reimpostata o la chiave privata SSH è stata eliminata accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="6990e-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="6990e-106">In passato, quando nel data center si verificava questa situazione, era necessario accedere all'unità e quindi aprire il KVM per raggiungere la console del server.</span><span class="sxs-lookup"><span data-stu-id="6990e-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="6990e-107">L'estensione VMAccess di Azure può essere concepita come il commutatore tastiera, video e mouse che consente di accedere alla console per reimpostare l'accesso a Linux o eseguire la manutenzione a livello di disco.</span><span class="sxs-lookup"><span data-stu-id="6990e-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="6990e-108">Questo articolo illustra come usare l'estensione VMAccess di Azure per controllare o ripristinare un disco, reimpostare l'accesso utente, gestire gli account utente o reimpostare la configurazione dei dischi SSH in Linux.</span><span class="sxs-lookup"><span data-stu-id="6990e-108">This article shows you how to use the Azure VMAccess Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSH configuration on Linux.</span></span> <span data-ttu-id="6990e-109">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6990e-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-to-use-the-vmaccess-extension"></a><span data-ttu-id="6990e-110">Modi di usare l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="6990e-110">Ways to use the VMAccess Extension</span></span>
<span data-ttu-id="6990e-111">Esistono due modi per usare l'estensione VMAccess nelle VM Linux:</span><span class="sxs-lookup"><span data-stu-id="6990e-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="6990e-112">Usare l'interfaccia della riga di comando di Azure 2.0 e i parametri richiesti.</span><span class="sxs-lookup"><span data-stu-id="6990e-112">Use the Azure CLI 2.0 and the required parameters.</span></span>
* <span data-ttu-id="6990e-113">[Usare file JSON non elaborati che l'estensione VMAccess elaborerà](#use-json-files-and-the-vmaccess-extension) e su cui baserà le sue operazioni.</span><span class="sxs-lookup"><span data-stu-id="6990e-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="6990e-114">L'esempio seguente usa i comandi [az vm user](/cli/azure/vm/user).</span><span class="sxs-lookup"><span data-stu-id="6990e-114">The following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="6990e-115">Per eseguire questi passaggi è necessario aver installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e aver effettuato l'accesso a un account Azure con il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6990e-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="6990e-116">Ripristinare la chiave SSH</span><span class="sxs-lookup"><span data-stu-id="6990e-116">Reset SSH key</span></span>
<span data-ttu-id="6990e-117">L'esempio seguente ripristina la chiave SSH per l'utente `azureuser` nella VM denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6990e-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="6990e-118">Reimpostazione delle password</span><span class="sxs-lookup"><span data-stu-id="6990e-118">Reset password</span></span>
<span data-ttu-id="6990e-119">L'esempio seguente ripristina la password per l'utente `azureuser` nella VM denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6990e-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="6990e-120">Riavviare SSH</span><span class="sxs-lookup"><span data-stu-id="6990e-120">Restart SSH</span></span>
<span data-ttu-id="6990e-121">L'esempio seguente riavvia il daemon SSH e reimposta la configurazione SSH sui valori predefiniti in una macchina virtuale denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6990e-121">The following example restarts the SSH daemon and resets the SSH configuration to default values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="6990e-122">Creare un utente</span><span class="sxs-lookup"><span data-stu-id="6990e-122">Create a user</span></span>
<span data-ttu-id="6990e-123">L'esempio seguente crea un utente denominato `myNewUser` usando una chiave SSH per l'autenticazione nella VM denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6990e-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="6990e-124">Eliminare un utente</span><span class="sxs-lookup"><span data-stu-id="6990e-124">Delete a user</span></span>
<span data-ttu-id="6990e-125">L'esempio seguente elimina un utente denominato `myNewUser` nella VM denominata `myVM`:</span><span class="sxs-lookup"><span data-stu-id="6990e-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a><span data-ttu-id="6990e-126">Usare file JSON e l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="6990e-126">Use JSON files and the VMAccess Extension</span></span>
<span data-ttu-id="6990e-127">Gli esempi seguenti usano file JSON non elaborati.</span><span class="sxs-lookup"><span data-stu-id="6990e-127">The following examples use raw JSON files.</span></span> <span data-ttu-id="6990e-128">Usare [az vm extension set](/cli/azure/vm/extension#set) per chiamare in seguito i file JSON.</span><span class="sxs-lookup"><span data-stu-id="6990e-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span></span> <span data-ttu-id="6990e-129">Questi file JSON possono essere chiamati anche dai modelli di Azure.</span><span class="sxs-lookup"><span data-stu-id="6990e-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="6990e-130">Ripristinare l'accesso utente</span><span class="sxs-lookup"><span data-stu-id="6990e-130">Reset user access</span></span>
<span data-ttu-id="6990e-131">Se si è perso l'accesso alla radice della VM Linux è possibile avviare uno script VMAccess per reimpostare la chiave SSH o la password di un utente.</span><span class="sxs-lookup"><span data-stu-id="6990e-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user's SSH key or password.</span></span>

<span data-ttu-id="6990e-132">Per reimpostare la chiave pubblica SSH di un utente, creare un file denominato `reset_ssh_key.json` e aggiungere le impostazioni nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="6990e-132">To reset the SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in the following format.</span></span> <span data-ttu-id="6990e-133">Usare valori personalizzati per i parametri `username` e `ssh_key`:</span><span class="sxs-lookup"><span data-stu-id="6990e-133">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="6990e-134">Eseguire lo script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="6990e-134">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="6990e-135">Per reimpostare la password di un utente, creare un file denominato `reset_user_password.json` e aggiungere le impostazioni nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="6990e-135">To reset a user password, create a file named `reset_user_password.json` and add settings in the following format.</span></span> <span data-ttu-id="6990e-136">Usare valori personalizzati per i parametri `username` e `password`:</span><span class="sxs-lookup"><span data-stu-id="6990e-136">Substitute your own values for the `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="6990e-137">Eseguire lo script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="6990e-137">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="6990e-138">Riavviare SSH</span><span class="sxs-lookup"><span data-stu-id="6990e-138">Restart SSH</span></span>
<span data-ttu-id="6990e-139">Per riavviare il daemon SSH e reimpostare la configurazione SSH sui valori predefiniti, creare un file denominato `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="6990e-139">To restart the SSH daemon and reset the SSH configuration to default values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="6990e-140">Aggiungere il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="6990e-140">Add the following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="6990e-141">Eseguire lo script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="6990e-141">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="6990e-142">Gestire gli utenti</span><span class="sxs-lookup"><span data-stu-id="6990e-142">Manage users</span></span>

<span data-ttu-id="6990e-143">Per creare un utente che esegua l'autenticazione con una chiave SSH, creare un file denominato `create_new_user.json` e aggiungere impostazioni nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="6990e-143">To create a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in the following format.</span></span> <span data-ttu-id="6990e-144">Usare valori personalizzati per i parametri `username` e `ssh_key`:</span><span class="sxs-lookup"><span data-stu-id="6990e-144">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="6990e-145">Eseguire lo script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="6990e-145">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="6990e-146">Per eliminare un utente, creare un file denominato `delete_user.json` e aggiungere il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="6990e-146">To delete a user, create a file named `delete_user.json` and add the following content.</span></span> <span data-ttu-id="6990e-147">Usare un valore personalizzato per il parametro `remove_user`:</span><span class="sxs-lookup"><span data-stu-id="6990e-147">Substitute your own value for the `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="6990e-148">Eseguire lo script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="6990e-148">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a><span data-ttu-id="6990e-149">Controllare o riparare il disco</span><span class="sxs-lookup"><span data-stu-id="6990e-149">Check or repair the disk</span></span>
<span data-ttu-id="6990e-150">Tramite VMAccess è anche possibile controllare e riparare un disco aggiunto alla macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="6990e-150">Using VMAccess you can also check and repair a disk that you added to the Linux VM.</span></span>

<span data-ttu-id="6990e-151">Per controllare e quindi riparare il disco, creare un file denominato `disk_check_repair.json` e aggiungere impostazioni nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="6990e-151">To check and then repair the disk, create a file named `disk_check_repair.json` and add settings in the following format.</span></span> <span data-ttu-id="6990e-152">Usare un valore personalizzato per il nome di `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="6990e-152">Substitute your own value for the name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="6990e-153">Eseguire lo script VMAccess con:</span><span class="sxs-lookup"><span data-stu-id="6990e-153">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="6990e-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6990e-154">Next steps</span></span>
<span data-ttu-id="6990e-155">L'aggiornamento di Linux mediante l'estensione VMAccess di Azure è un metodo per apportare modifiche a una VM Linux in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6990e-155">Updating Linux using the Azure VMAccess Extension is one method to make changes on a running Linux VM.</span></span> <span data-ttu-id="6990e-156">È inoltre possibile usare strumenti come cloud-init e modelli di Azure Resource Manager per modificare la VM Linux in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="6990e-156">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="6990e-157">Estensioni e funzionalità delle macchine virtuali per Linux</span><span class="sxs-lookup"><span data-stu-id="6990e-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="6990e-158">Creazione di modelli di Azure Resource Manager con le estensioni di VM Linux</span><span class="sxs-lookup"><span data-stu-id="6990e-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="6990e-159">Uso di cloud-init per personalizzare una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="6990e-159">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md)

