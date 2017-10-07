---
title: aaaUse cloud init toocustomize una VM Linux | Documenti Microsoft
description: Come toocustomize di cloud init toouse una VM Linux durante la creazione hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="6b4bd-103">Usare cloud init toocustomize una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="6b4bd-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="6b4bd-104">Questo articolo illustra come toomake un tooset script cloud init hello nome host, aggiornare i pacchetti installati e gestire gli account utente con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="6b4bd-105">gli script di cloud init Hello vengono chiamati quando si crea una macchina virtuale (VM) da CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="6b4bd-106">Per una panoramica più approfondita sull'installazione di applicazioni, la scrittura di file di configurazione e l'inserimento di chiavi da Key Vault, vedere [questa esercitazione](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6b4bd-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="6b4bd-107">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6b4bd-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="6b4bd-108">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="6b4bd-108">Quick commands</span></span>
<span data-ttu-id="6b4bd-109">Creare uno script di cloud init.txt che imposta il nome host hello, Aggiorna tutti i pacchetti e aggiunge un tooLinux utente sudo.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

<span data-ttu-id="6b4bd-110">Creare un toolaunch gruppo di risorse di macchine virtuali in con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6b4bd-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6b4bd-111">esempio Hello Crea gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6b4bd-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="6b4bd-112">Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio con hello `--custom-data` parametro.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="6b4bd-113">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="6b4bd-113">Detailed walkthrough</span></span>
<span data-ttu-id="6b4bd-114">Quando si avvia una nuova VM Linux si ottiene un VM Linux standard senza alcuna personalizzazione né alcun adattamento.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="6b4bd-115">[Cloud init](https://cloudinit.readthedocs.org) è tooinject un metodo standard per le impostazioni di configurazione o script in tale VM Linux che è stato avviato per hello prima volta.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="6b4bd-116">In Azure, esistono alcuni modi toomake modifiche in una VM Linux come viene distribuito o avviato.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="6b4bd-117">Inserire gli script che usano cloud-init.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="6b4bd-118">Inserire gli script utilizzando hello Azure [estensione VMAccess](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6b4bd-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="6b4bd-119">Un modello di Azure che usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="6b4bd-120">Un modello di Azure che usa [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="6b4bd-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="6b4bd-121">script tooinject in qualsiasi momento dopo l'avvio:</span><span class="sxs-lookup"><span data-stu-id="6b4bd-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="6b4bd-122">Direttamente i comandi toorun SSH</span><span class="sxs-lookup"><span data-stu-id="6b4bd-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="6b4bd-123">Inserire gli script utilizzando hello Azure [estensione VMAccess](using-vmaccess-extension.md), in modo imperativo o in un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="6b4bd-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="6b4bd-124">Strumenti per la gestione della configurazione come Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="6b4bd-125">Estensione VMAccess esegue uno script come radice in hello stesso tramite SSH possibile.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="6b4bd-126">Tuttavia, utilizzando l'estensione della macchina virtuale hello consente diverse funzionalità offerti da Azure che possono essere utili a seconda dello scenario.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="6b4bd-127">Disponibilità di cloud-init negli alias delle immagini a creazione rapida della VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="6b4bd-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="6b4bd-128">Alias</span><span class="sxs-lookup"><span data-stu-id="6b4bd-128">Alias</span></span> | <span data-ttu-id="6b4bd-129">Autore</span><span class="sxs-lookup"><span data-stu-id="6b4bd-129">Publisher</span></span> | <span data-ttu-id="6b4bd-130">Offerta</span><span class="sxs-lookup"><span data-stu-id="6b4bd-130">Offer</span></span> | <span data-ttu-id="6b4bd-131">SKU</span><span class="sxs-lookup"><span data-stu-id="6b4bd-131">SKU</span></span> | <span data-ttu-id="6b4bd-132">Versione</span><span class="sxs-lookup"><span data-stu-id="6b4bd-132">Version</span></span> | <span data-ttu-id="6b4bd-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="6b4bd-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="6b4bd-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="6b4bd-134">CentOS</span></span> |<span data-ttu-id="6b4bd-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="6b4bd-135">OpenLogic</span></span> |<span data-ttu-id="6b4bd-136">Centos</span><span class="sxs-lookup"><span data-stu-id="6b4bd-136">Centos</span></span> |<span data-ttu-id="6b4bd-137">7,2</span><span class="sxs-lookup"><span data-stu-id="6b4bd-137">7.2</span></span> |<span data-ttu-id="6b4bd-138">più recenti</span><span class="sxs-lookup"><span data-stu-id="6b4bd-138">latest</span></span> |<span data-ttu-id="6b4bd-139">no</span><span class="sxs-lookup"><span data-stu-id="6b4bd-139">no</span></span> |
| <span data-ttu-id="6b4bd-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6b4bd-140">CoreOS</span></span> |<span data-ttu-id="6b4bd-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6b4bd-141">CoreOS</span></span> |<span data-ttu-id="6b4bd-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6b4bd-142">CoreOS</span></span> |<span data-ttu-id="6b4bd-143">Stabile</span><span class="sxs-lookup"><span data-stu-id="6b4bd-143">Stable</span></span> |<span data-ttu-id="6b4bd-144">più recenti</span><span class="sxs-lookup"><span data-stu-id="6b4bd-144">latest</span></span> |<span data-ttu-id="6b4bd-145">sì</span><span class="sxs-lookup"><span data-stu-id="6b4bd-145">yes</span></span> |
| <span data-ttu-id="6b4bd-146">Debian</span><span class="sxs-lookup"><span data-stu-id="6b4bd-146">Debian</span></span> |<span data-ttu-id="6b4bd-147">credativ</span><span class="sxs-lookup"><span data-stu-id="6b4bd-147">credativ</span></span> |<span data-ttu-id="6b4bd-148">Debian</span><span class="sxs-lookup"><span data-stu-id="6b4bd-148">Debian</span></span> |<span data-ttu-id="6b4bd-149">8</span><span class="sxs-lookup"><span data-stu-id="6b4bd-149">8</span></span> |<span data-ttu-id="6b4bd-150">più recenti</span><span class="sxs-lookup"><span data-stu-id="6b4bd-150">latest</span></span> |<span data-ttu-id="6b4bd-151">no</span><span class="sxs-lookup"><span data-stu-id="6b4bd-151">no</span></span> |
| <span data-ttu-id="6b4bd-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6b4bd-152">openSUSE</span></span> |<span data-ttu-id="6b4bd-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="6b4bd-153">SUSE</span></span> |<span data-ttu-id="6b4bd-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6b4bd-154">openSUSE</span></span> |<span data-ttu-id="6b4bd-155">13.2</span><span class="sxs-lookup"><span data-stu-id="6b4bd-155">13.2</span></span> |<span data-ttu-id="6b4bd-156">più recenti</span><span class="sxs-lookup"><span data-stu-id="6b4bd-156">latest</span></span> |<span data-ttu-id="6b4bd-157">no</span><span class="sxs-lookup"><span data-stu-id="6b4bd-157">no</span></span> |
| <span data-ttu-id="6b4bd-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="6b4bd-158">RHEL</span></span> |<span data-ttu-id="6b4bd-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="6b4bd-159">Redhat</span></span> |<span data-ttu-id="6b4bd-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="6b4bd-160">RHEL</span></span> |<span data-ttu-id="6b4bd-161">7,2</span><span class="sxs-lookup"><span data-stu-id="6b4bd-161">7.2</span></span> |<span data-ttu-id="6b4bd-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="6b4bd-162">latest</span></span> |<span data-ttu-id="6b4bd-163">no</span><span class="sxs-lookup"><span data-stu-id="6b4bd-163">no</span></span> |
| <span data-ttu-id="6b4bd-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="6b4bd-164">UbuntuLTS</span></span> |<span data-ttu-id="6b4bd-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="6b4bd-165">Canonical</span></span> |<span data-ttu-id="6b4bd-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="6b4bd-166">UbuntuServer</span></span> |<span data-ttu-id="6b4bd-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="6b4bd-167">14.04.4-LTS</span></span> |<span data-ttu-id="6b4bd-168">più recenti</span><span class="sxs-lookup"><span data-stu-id="6b4bd-168">latest</span></span> |<span data-ttu-id="6b4bd-169">sì</span><span class="sxs-lookup"><span data-stu-id="6b4bd-169">yes</span></span> |

<span data-ttu-id="6b4bd-170">È in uso di nostri partner tooget cloud-init inclusi e l'utilizzo delle immagini hello che forniscono tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="6b4bd-171">Aggiungere una creazione di VM cloud init script toohello con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="6b4bd-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="6b4bd-172">toolaunch uno script di inizializzazione di cloud durante la creazione di una macchina virtuale in Azure, specificare il file di cloud init hello mediante Azure CLI hello `--custom-data` passare.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="6b4bd-173">Creare un toolaunch gruppo di risorse di macchine virtuali in con [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6b4bd-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6b4bd-174">esempio Hello Crea gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6b4bd-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="6b4bd-175">Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="6b4bd-176">Creare un nome di cloud init script tooset hello host di una VM Linux</span><span class="sxs-lookup"><span data-stu-id="6b4bd-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="6b4bd-177">Uno dei hello più semplice e più importanti impostazioni per tutte le VM Linux sarà hostname hello.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="6b4bd-178">È possibile definire facilmente tale impostazione tramite cloud-init con questo script.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="6b4bd-179">Script cloud-init di esempio denominato `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="6b4bd-180">Durante l'avvio iniziale di hello di hello macchina virtuale, questo script cloud init imposta hello hostname troppo*nomeserver*.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="6b4bd-181">Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="6b4bd-182">Account di accesso e verificare il nome host hello di hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="6b4bd-183">Creare uno script cloud-init</span><span class="sxs-lookup"><span data-stu-id="6b4bd-183">Create a cloud-init script</span></span>
<span data-ttu-id="6b4bd-184">Per la sicurezza, si desidera il tooupdate Ubuntu VM al primo avvio hello.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="6b4bd-185">Con cloud init possiamo che con hello seguire script, a seconda della distribuzione di Linux hello in uso.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="6b4bd-186">Script di esempio cloud init `cloud_config_apt_upgrade.txt` per hello Debian famiglia</span><span class="sxs-lookup"><span data-stu-id="6b4bd-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="6b4bd-187">Dopo che è stato avviato Linux, tutti i pacchetti hello installato vengono aggiornati tramite **apt get**.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="6b4bd-188">Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="6b4bd-189">Accedere e verificare che tutti i pacchetti siano aggiornati.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="6b4bd-190">Creare un tooadd script cloud init tooLinux un utente</span><span class="sxs-lookup"><span data-stu-id="6b4bd-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="6b4bd-191">Una delle attività di primo hello in qualsiasi nuova VM Linux è un utente per se stessi o tooavoid utilizzando tooadd *radice*.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="6b4bd-192">Le chiavi SSH sono consigliata per la sicurezza e ai fini dell'usabilità e vengono aggiunti toohello *~/.ssh/authorized_keys* file con questo script di inizializzazione di cloud.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="6b4bd-193">Script cloud-init `cloud_config_add_users.txt` di esempio per la famiglia Debian</span><span class="sxs-lookup"><span data-stu-id="6b4bd-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="6b4bd-194">Dopo che è stato avviato Linux, tutti gli utenti di hello elencato sono il gruppo di sudo toohello creato e aggiunto.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="6b4bd-195">Creare una VM Linux con [creare vm az](/cli/azure/vm#create) tramite cloud init tooconfigure durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="6b4bd-196">Account di accesso e verificare utente hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="6b4bd-197">Output</span><span class="sxs-lookup"><span data-stu-id="6b4bd-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="6b4bd-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b4bd-198">Next steps</span></span>
<span data-ttu-id="6b4bd-199">Cloud init sta diventando un modo standard toomodify VM Linux all'avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="6b4bd-200">Azure offre inoltre estensioni VM, che consentono di toomodify il LinuxVM all'avvio del sistema o in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="6b4bd-201">Ad esempio, è possibile utilizzare hello Azure VMAccessExtension tooreset SSH o informazioni utente durante l'esecuzione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="6b4bd-202">Con cloud-init, occorre una password di hello tooreset riavvio.</span><span class="sxs-lookup"><span data-stu-id="6b4bd-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="6b4bd-203">Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="6b4bd-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="6b4bd-204">Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="6b4bd-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
