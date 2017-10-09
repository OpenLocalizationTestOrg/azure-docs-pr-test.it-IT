---
title: aaaUsing cloud init toocustomize una VM Linux durante la creazione di Azure | Documenti Microsoft
description: Come toocustomize di cloud init toouse una VM Linux durante la creazione hello Azure CLI 1.0
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="cca5f-103">Utilizzare cloud init toocustomize una VM Linux durante la creazione hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cca5f-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="cca5f-104">Questo articolo illustra come toomake un tooset script cloud init hello nome host, aggiornare i pacchetti installati e gestire gli account utente.</span><span class="sxs-lookup"><span data-stu-id="cca5f-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="cca5f-105">script cloud init Hello vengono chiamati durante la creazione di VM da Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="cca5f-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="cca5f-106">articolo Hello richiede:</span><span class="sxs-lookup"><span data-stu-id="cca5f-106">hello article requires:</span></span>

* <span data-ttu-id="cca5f-107">Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cca5f-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="cca5f-108">Hello [CLI di Azure](../../cli-install-nodejs.md) accesso `azure login`.</span><span class="sxs-lookup"><span data-stu-id="cca5f-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="cca5f-109">Hello Azure CLI *deve essere* modalità Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="cca5f-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cca5f-110">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="cca5f-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="cca5f-111">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="cca5f-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="cca5f-112">[Azure CLI 1.0](#quick-commands) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="cca5f-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cca5f-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="cca5f-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="cca5f-114">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="cca5f-114">Quick Commands</span></span>
<span data-ttu-id="cca5f-115">Creare uno script di cloud init.txt che imposta il nome host hello, Aggiorna tutti i pacchetti e aggiunge un tooLinux utente sudo.</span><span class="sxs-lookup"><span data-stu-id="cca5f-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```sh
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
<span data-ttu-id="cca5f-116">Creazione di macchine virtuali in un toolaunch gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cca5f-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="cca5f-117">Creare una VM Linux di cloud init tooconfigure durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="cca5f-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="cca5f-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="cca5f-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="cca5f-119">Introduzione</span><span class="sxs-lookup"><span data-stu-id="cca5f-119">Introduction</span></span>
<span data-ttu-id="cca5f-120">Quando si avvia una nuova VM Linux si ottiene un VM Linux standard senza alcuna personalizzazione né alcun adattamento.</span><span class="sxs-lookup"><span data-stu-id="cca5f-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="cca5f-121">[Cloud init](https://cloudinit.readthedocs.org) è tooinject un metodo standard per le impostazioni di configurazione o script in tale VM Linux che è stato avviato per hello prima volta.</span><span class="sxs-lookup"><span data-stu-id="cca5f-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="cca5f-122">In Azure, sono disponibili un tre modi diversi toomake modifiche in una VM Linux mentre viene distribuito o avviato.</span><span class="sxs-lookup"><span data-stu-id="cca5f-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="cca5f-123">Inserire gli script che usano cloud-init.</span><span class="sxs-lookup"><span data-stu-id="cca5f-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="cca5f-124">Inserire gli script utilizzando hello Azure [estensione VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cca5f-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="cca5f-125">Un modello di Azure che usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="cca5f-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="cca5f-126">Un modello di Azure che usa [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cca5f-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="cca5f-127">script tooinject in qualsiasi momento dopo l'avvio:</span><span class="sxs-lookup"><span data-stu-id="cca5f-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="cca5f-128">Direttamente i comandi toorun SSH</span><span class="sxs-lookup"><span data-stu-id="cca5f-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="cca5f-129">Inserire gli script utilizzando hello Azure [estensione VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), in modo imperativo o in un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="cca5f-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="cca5f-130">Strumenti per la gestione della configurazione come Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="cca5f-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="cca5f-131">: Estensione VMAccess esegue uno script come radice in hello stesso tramite SSH possibile.</span><span class="sxs-lookup"><span data-stu-id="cca5f-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="cca5f-132">Tuttavia, utilizzando l'estensione della macchina virtuale hello consente diverse funzionalità offerti da Azure che possono essere utili a seconda dello scenario.</span><span class="sxs-lookup"><span data-stu-id="cca5f-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="cca5f-133">Disponibilità di cloud-init negli alias delle immagini a creazione rapida della VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="cca5f-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="cca5f-134">Alias</span><span class="sxs-lookup"><span data-stu-id="cca5f-134">Alias</span></span> | <span data-ttu-id="cca5f-135">Autore</span><span class="sxs-lookup"><span data-stu-id="cca5f-135">Publisher</span></span> | <span data-ttu-id="cca5f-136">Offerta</span><span class="sxs-lookup"><span data-stu-id="cca5f-136">Offer</span></span> | <span data-ttu-id="cca5f-137">SKU</span><span class="sxs-lookup"><span data-stu-id="cca5f-137">SKU</span></span> | <span data-ttu-id="cca5f-138">Versione</span><span class="sxs-lookup"><span data-stu-id="cca5f-138">Version</span></span> | <span data-ttu-id="cca5f-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="cca5f-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="cca5f-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="cca5f-140">CentOS</span></span> |<span data-ttu-id="cca5f-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="cca5f-141">OpenLogic</span></span> |<span data-ttu-id="cca5f-142">Centos</span><span class="sxs-lookup"><span data-stu-id="cca5f-142">Centos</span></span> |<span data-ttu-id="cca5f-143">7,2</span><span class="sxs-lookup"><span data-stu-id="cca5f-143">7.2</span></span> |<span data-ttu-id="cca5f-144">più recenti</span><span class="sxs-lookup"><span data-stu-id="cca5f-144">latest</span></span> |<span data-ttu-id="cca5f-145">no</span><span class="sxs-lookup"><span data-stu-id="cca5f-145">no</span></span> |
| <span data-ttu-id="cca5f-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cca5f-146">CoreOS</span></span> |<span data-ttu-id="cca5f-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cca5f-147">CoreOS</span></span> |<span data-ttu-id="cca5f-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cca5f-148">CoreOS</span></span> |<span data-ttu-id="cca5f-149">Stabile</span><span class="sxs-lookup"><span data-stu-id="cca5f-149">Stable</span></span> |<span data-ttu-id="cca5f-150">più recenti</span><span class="sxs-lookup"><span data-stu-id="cca5f-150">latest</span></span> |<span data-ttu-id="cca5f-151">sì</span><span class="sxs-lookup"><span data-stu-id="cca5f-151">yes</span></span> |
| <span data-ttu-id="cca5f-152">Debian</span><span class="sxs-lookup"><span data-stu-id="cca5f-152">Debian</span></span> |<span data-ttu-id="cca5f-153">credativ</span><span class="sxs-lookup"><span data-stu-id="cca5f-153">credativ</span></span> |<span data-ttu-id="cca5f-154">Debian</span><span class="sxs-lookup"><span data-stu-id="cca5f-154">Debian</span></span> |<span data-ttu-id="cca5f-155">8</span><span class="sxs-lookup"><span data-stu-id="cca5f-155">8</span></span> |<span data-ttu-id="cca5f-156">più recenti</span><span class="sxs-lookup"><span data-stu-id="cca5f-156">latest</span></span> |<span data-ttu-id="cca5f-157">no</span><span class="sxs-lookup"><span data-stu-id="cca5f-157">no</span></span> |
| <span data-ttu-id="cca5f-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="cca5f-158">openSUSE</span></span> |<span data-ttu-id="cca5f-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="cca5f-159">SUSE</span></span> |<span data-ttu-id="cca5f-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="cca5f-160">openSUSE</span></span> |<span data-ttu-id="cca5f-161">13.2</span><span class="sxs-lookup"><span data-stu-id="cca5f-161">13.2</span></span> |<span data-ttu-id="cca5f-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="cca5f-162">latest</span></span> |<span data-ttu-id="cca5f-163">no</span><span class="sxs-lookup"><span data-stu-id="cca5f-163">no</span></span> |
| <span data-ttu-id="cca5f-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="cca5f-164">RHEL</span></span> |<span data-ttu-id="cca5f-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="cca5f-165">Redhat</span></span> |<span data-ttu-id="cca5f-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="cca5f-166">RHEL</span></span> |<span data-ttu-id="cca5f-167">7,2</span><span class="sxs-lookup"><span data-stu-id="cca5f-167">7.2</span></span> |<span data-ttu-id="cca5f-168">più recenti</span><span class="sxs-lookup"><span data-stu-id="cca5f-168">latest</span></span> |<span data-ttu-id="cca5f-169">no</span><span class="sxs-lookup"><span data-stu-id="cca5f-169">no</span></span> |
| <span data-ttu-id="cca5f-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="cca5f-170">UbuntuLTS</span></span> |<span data-ttu-id="cca5f-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="cca5f-171">Canonical</span></span> |<span data-ttu-id="cca5f-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="cca5f-172">UbuntuServer</span></span> |<span data-ttu-id="cca5f-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="cca5f-173">14.04.4-LTS</span></span> |<span data-ttu-id="cca5f-174">più recenti</span><span class="sxs-lookup"><span data-stu-id="cca5f-174">latest</span></span> |<span data-ttu-id="cca5f-175">sì</span><span class="sxs-lookup"><span data-stu-id="cca5f-175">yes</span></span> |

<span data-ttu-id="cca5f-176">Microsoft è l'uso con i partner tooget cloud-init inclusi e utilizzo delle immagini hello che forniscono tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cca5f-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="cca5f-177">Aggiunta di una creazione di VM cloud init script toohello con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="cca5f-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="cca5f-178">toolaunch uno script di inizializzazione di cloud durante la creazione di una macchina virtuale in Azure, specificare il file di cloud init hello mediante Azure CLI hello `--custom-data` passare.</span><span class="sxs-lookup"><span data-stu-id="cca5f-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="cca5f-179">Creazione di macchine virtuali in un toolaunch gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cca5f-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="cca5f-180">Creare una VM Linux di cloud init tooconfigure durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="cca5f-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="cca5f-181">Creazione di un nome di cloud init script tooset hello host di una VM Linux</span><span class="sxs-lookup"><span data-stu-id="cca5f-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="cca5f-182">Uno dei hello più semplice e più importanti impostazioni per tutte le VM Linux sarà hostname hello.</span><span class="sxs-lookup"><span data-stu-id="cca5f-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="cca5f-183">È possibile definire facilmente tale impostazione tramite cloud-init con questo script.</span><span class="sxs-lookup"><span data-stu-id="cca5f-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="cca5f-184">Script cloud-init di esempio denominato `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="cca5f-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="cca5f-185">Durante l'avvio iniziale di hello di hello macchina virtuale, questo script cloud init imposta hello hostname troppo`myservername`.</span><span class="sxs-lookup"><span data-stu-id="cca5f-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="cca5f-186">Account di accesso e verificare il nome host hello di hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cca5f-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="cca5f-187">Creazione di un tooupdate script cloud init Linux</span><span class="sxs-lookup"><span data-stu-id="cca5f-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="cca5f-188">Per la sicurezza, si desidera il tooupdate Ubuntu VM al primo avvio hello.</span><span class="sxs-lookup"><span data-stu-id="cca5f-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="cca5f-189">Con cloud init possiamo che con hello seguire script, a seconda della distribuzione di Linux hello in uso.</span><span class="sxs-lookup"><span data-stu-id="cca5f-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="cca5f-190">Script di esempio cloud init `cloud_config_apt_upgrade.txt` per hello Debian famiglia</span><span class="sxs-lookup"><span data-stu-id="cca5f-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="cca5f-191">Dopo che è stato avviato Linux, tutti i pacchetti hello installato vengono aggiornati tramite `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="cca5f-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="cca5f-192">Accedere e verificare che tutti i pacchetti siano aggiornati.</span><span class="sxs-lookup"><span data-stu-id="cca5f-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="cca5f-193">Creazione di un tooadd script cloud init tooLinux un utente</span><span class="sxs-lookup"><span data-stu-id="cca5f-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="cca5f-194">Una delle attività di primo hello in qualsiasi nuova VM Linux è un utente per se stessi o tooavoid utilizzando tooadd `root`.</span><span class="sxs-lookup"><span data-stu-id="cca5f-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="cca5f-195">Le chiavi SSH sono consigliata per la sicurezza e ai fini dell'usabilità e vengono aggiunti toohello `~/.ssh/authorized_keys` file con questo script di inizializzazione di cloud.</span><span class="sxs-lookup"><span data-stu-id="cca5f-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="cca5f-196">Script cloud-init `cloud_config_add_users.txt` di esempio per la famiglia Debian</span><span class="sxs-lookup"><span data-stu-id="cca5f-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="cca5f-197">Dopo che è stato avviato Linux, tutti gli utenti di hello elencato sono il gruppo di sudo toohello creato e aggiunto.</span><span class="sxs-lookup"><span data-stu-id="cca5f-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="cca5f-198">Account di accesso e verificare utente hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="cca5f-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="cca5f-199">Output</span><span class="sxs-lookup"><span data-stu-id="cca5f-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="cca5f-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cca5f-200">Next Steps</span></span>
<span data-ttu-id="cca5f-201">Cloud init sta diventando un modo standard toomodify VM Linux all'avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="cca5f-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="cca5f-202">Azure offre inoltre estensioni VM, che consentono di toomodify il LinuxVM all'avvio del sistema o in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cca5f-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="cca5f-203">Ad esempio, è possibile utilizzare hello Azure VMAccessExtension tooreset SSH o informazioni utente durante l'esecuzione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cca5f-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="cca5f-204">Con cloud-init, occorre una password di hello tooreset riavvio.</span><span class="sxs-lookup"><span data-stu-id="cca5f-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="cca5f-205">Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="cca5f-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="cca5f-206">Gestire utenti, SSH e controllo o i dischi di ripristino di macchine virtuali Linux di Azure utilizzando hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="cca5f-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

