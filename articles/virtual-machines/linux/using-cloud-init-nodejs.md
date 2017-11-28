---
title: Uso di cloud-init per personalizzare una VM Linux durante la creazione in Azure | Documentazione Microsoft
description: Come usare cloud-init per personalizzare una VM Linux durante la creazione con l'interfaccia della riga di comando di Azure 1.0
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
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="36b4b-103">Usare cloud-init per personalizzare una VM Linux durante la creazione con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="36b4b-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="36b4b-104">Questo articolo illustra come creare script cloud-init per impostare il nome host, aggiornare i pacchetti installati e gestire gli account utente.</span><span class="sxs-lookup"><span data-stu-id="36b4b-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="36b4b-105">Gli script cloud-init vengono richiamati durante la creazione della VM dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="36b4b-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="36b4b-106">L'articolo richiede:</span><span class="sxs-lookup"><span data-stu-id="36b4b-106">The article requires:</span></span>

* <span data-ttu-id="36b4b-107">Un account Azure. È possibile [ottenere una versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36b4b-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="36b4b-108">Accesso tramite `azure login` per l'[interfaccia della riga di comando di Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="36b4b-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="36b4b-109">L'interfaccia della riga di comando di Azure *deve essere impostata obbligatoriamente* sulla modalità Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="36b4b-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="36b4b-110">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="36b4b-110">CLI versions to complete the task</span></span>
<span data-ttu-id="36b4b-111">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="36b4b-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="36b4b-112">[Interfaccia della riga di comando di Azure 1.0](#quick-commands): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="36b4b-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="36b4b-113">[Interfaccia della riga di comando di Azure 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="36b4b-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="36b4b-114">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="36b4b-114">Quick Commands</span></span>
<span data-ttu-id="36b4b-115">Creare uno script cloud-init.txt che consente di impostare il nome host, aggiornare tutti i pacchetti e aggiungere un utente sudo per Linux.</span><span class="sxs-lookup"><span data-stu-id="36b4b-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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
<span data-ttu-id="36b4b-116">Creare un gruppo di risorse in cui avviare le VM.</span><span class="sxs-lookup"><span data-stu-id="36b4b-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="36b4b-117">Creare una VM Linux che utilizza cloud-init per configurarla durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="36b4b-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="36b4b-118">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="36b4b-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="36b4b-119">Introduzione</span><span class="sxs-lookup"><span data-stu-id="36b4b-119">Introduction</span></span>
<span data-ttu-id="36b4b-120">Quando si avvia una nuova VM Linux si ottiene un VM Linux standard senza alcuna personalizzazione né alcun adattamento.</span><span class="sxs-lookup"><span data-stu-id="36b4b-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="36b4b-121">[Cloud-init](https://cloudinit.readthedocs.org) è un metodo standard che consente di inserire uno script o alcune impostazioni di configurazione in una VM Linux quando viene avviata per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="36b4b-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="36b4b-122">In Azure è possibile apportare modifiche a una VM Linux in fase di distribuzione o avvio in tre modi diversi.</span><span class="sxs-lookup"><span data-stu-id="36b4b-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="36b4b-123">Inserire gli script che usano cloud-init.</span><span class="sxs-lookup"><span data-stu-id="36b4b-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="36b4b-124">Inserire gli script che usano l' [estensione VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)di Azure.</span><span class="sxs-lookup"><span data-stu-id="36b4b-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="36b4b-125">Un modello di Azure che usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="36b4b-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="36b4b-126">Un modello di Azure che usa [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36b4b-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="36b4b-127">Per inserire script in qualsiasi momento dopo l'avvio:</span><span class="sxs-lookup"><span data-stu-id="36b4b-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="36b4b-128">Esecuzione diretta di comandi tramite SSH</span><span class="sxs-lookup"><span data-stu-id="36b4b-128">SSH to run commands directly</span></span>
* <span data-ttu-id="36b4b-129">Inserire gli script usando l' [estensione VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)di Azure, in modo imperativo o in un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="36b4b-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="36b4b-130">Strumenti per la gestione della configurazione come Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="36b4b-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="36b4b-131">: l'estensione VMAccess esegue uno script come radice nello stesso modo di SSH.</span><span class="sxs-lookup"><span data-stu-id="36b4b-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="36b4b-132">Tuttavia, l'utilizzo dell'estensione della VM consente di abilitare diverse funzionalità di da Azure potenzialmente utili a seconda dello scenario.</span><span class="sxs-lookup"><span data-stu-id="36b4b-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="36b4b-133">Disponibilità di cloud-init negli alias delle immagini a creazione rapida della VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="36b4b-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="36b4b-134">Alias</span><span class="sxs-lookup"><span data-stu-id="36b4b-134">Alias</span></span> | <span data-ttu-id="36b4b-135">Autore</span><span class="sxs-lookup"><span data-stu-id="36b4b-135">Publisher</span></span> | <span data-ttu-id="36b4b-136">Offerta</span><span class="sxs-lookup"><span data-stu-id="36b4b-136">Offer</span></span> | <span data-ttu-id="36b4b-137">SKU</span><span class="sxs-lookup"><span data-stu-id="36b4b-137">SKU</span></span> | <span data-ttu-id="36b4b-138">Versione</span><span class="sxs-lookup"><span data-stu-id="36b4b-138">Version</span></span> | <span data-ttu-id="36b4b-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="36b4b-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="36b4b-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="36b4b-140">CentOS</span></span> |<span data-ttu-id="36b4b-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="36b4b-141">OpenLogic</span></span> |<span data-ttu-id="36b4b-142">Centos</span><span class="sxs-lookup"><span data-stu-id="36b4b-142">Centos</span></span> |<span data-ttu-id="36b4b-143">7,2</span><span class="sxs-lookup"><span data-stu-id="36b4b-143">7.2</span></span> |<span data-ttu-id="36b4b-144">più recenti</span><span class="sxs-lookup"><span data-stu-id="36b4b-144">latest</span></span> |<span data-ttu-id="36b4b-145">no</span><span class="sxs-lookup"><span data-stu-id="36b4b-145">no</span></span> |
| <span data-ttu-id="36b4b-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="36b4b-146">CoreOS</span></span> |<span data-ttu-id="36b4b-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="36b4b-147">CoreOS</span></span> |<span data-ttu-id="36b4b-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="36b4b-148">CoreOS</span></span> |<span data-ttu-id="36b4b-149">Stabile</span><span class="sxs-lookup"><span data-stu-id="36b4b-149">Stable</span></span> |<span data-ttu-id="36b4b-150">più recenti</span><span class="sxs-lookup"><span data-stu-id="36b4b-150">latest</span></span> |<span data-ttu-id="36b4b-151">sì</span><span class="sxs-lookup"><span data-stu-id="36b4b-151">yes</span></span> |
| <span data-ttu-id="36b4b-152">Debian</span><span class="sxs-lookup"><span data-stu-id="36b4b-152">Debian</span></span> |<span data-ttu-id="36b4b-153">credativ</span><span class="sxs-lookup"><span data-stu-id="36b4b-153">credativ</span></span> |<span data-ttu-id="36b4b-154">Debian</span><span class="sxs-lookup"><span data-stu-id="36b4b-154">Debian</span></span> |<span data-ttu-id="36b4b-155">8</span><span class="sxs-lookup"><span data-stu-id="36b4b-155">8</span></span> |<span data-ttu-id="36b4b-156">più recenti</span><span class="sxs-lookup"><span data-stu-id="36b4b-156">latest</span></span> |<span data-ttu-id="36b4b-157">no</span><span class="sxs-lookup"><span data-stu-id="36b4b-157">no</span></span> |
| <span data-ttu-id="36b4b-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="36b4b-158">openSUSE</span></span> |<span data-ttu-id="36b4b-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="36b4b-159">SUSE</span></span> |<span data-ttu-id="36b4b-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="36b4b-160">openSUSE</span></span> |<span data-ttu-id="36b4b-161">13.2</span><span class="sxs-lookup"><span data-stu-id="36b4b-161">13.2</span></span> |<span data-ttu-id="36b4b-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="36b4b-162">latest</span></span> |<span data-ttu-id="36b4b-163">no</span><span class="sxs-lookup"><span data-stu-id="36b4b-163">no</span></span> |
| <span data-ttu-id="36b4b-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="36b4b-164">RHEL</span></span> |<span data-ttu-id="36b4b-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="36b4b-165">Redhat</span></span> |<span data-ttu-id="36b4b-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="36b4b-166">RHEL</span></span> |<span data-ttu-id="36b4b-167">7,2</span><span class="sxs-lookup"><span data-stu-id="36b4b-167">7.2</span></span> |<span data-ttu-id="36b4b-168">più recenti</span><span class="sxs-lookup"><span data-stu-id="36b4b-168">latest</span></span> |<span data-ttu-id="36b4b-169">no</span><span class="sxs-lookup"><span data-stu-id="36b4b-169">no</span></span> |
| <span data-ttu-id="36b4b-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="36b4b-170">UbuntuLTS</span></span> |<span data-ttu-id="36b4b-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="36b4b-171">Canonical</span></span> |<span data-ttu-id="36b4b-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="36b4b-172">UbuntuServer</span></span> |<span data-ttu-id="36b4b-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="36b4b-173">14.04.4-LTS</span></span> |<span data-ttu-id="36b4b-174">più recenti</span><span class="sxs-lookup"><span data-stu-id="36b4b-174">latest</span></span> |<span data-ttu-id="36b4b-175">sì</span><span class="sxs-lookup"><span data-stu-id="36b4b-175">yes</span></span> |

<span data-ttu-id="36b4b-176">Microsoft collabora con i partner per promuovere l'inclusione di cloud-init e utilizza le immagini da essi fornite per Azure.</span><span class="sxs-lookup"><span data-stu-id="36b4b-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="36b4b-177">Aggiunta di uno script cloud-init per la creazione della VM con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="36b4b-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="36b4b-178">Per avviare uno script cloud-init durante la creazione di una VM in Azure, specificare il file cloud-init tramite l'opzione `--custom-data` dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="36b4b-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="36b4b-179">Creare un gruppo di risorse in cui avviare le VM.</span><span class="sxs-lookup"><span data-stu-id="36b4b-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="36b4b-180">Creare una VM Linux che utilizza cloud-init per configurarla durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="36b4b-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="36b4b-181">Creazione di uno script cloud-init per impostare il nome host di una VM Linux</span><span class="sxs-lookup"><span data-stu-id="36b4b-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="36b4b-182">Una delle impostazioni più semplici e più importanti per qualsiasi VM Linux è il nome host.</span><span class="sxs-lookup"><span data-stu-id="36b4b-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="36b4b-183">È possibile definire facilmente tale impostazione tramite cloud-init con questo script.</span><span class="sxs-lookup"><span data-stu-id="36b4b-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="36b4b-184">Script cloud-init di esempio denominato `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="36b4b-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="36b4b-185">Durante l'avvio iniziale della VM questo script cloud-init imposta il nome host su `myservername`.</span><span class="sxs-lookup"><span data-stu-id="36b4b-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

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

<span data-ttu-id="36b4b-186">Accedere e verificare il nome host della nuova VM.</span><span class="sxs-lookup"><span data-stu-id="36b4b-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="36b4b-187">Creazione di uno script cloud-init per aggiornare Linux</span><span class="sxs-lookup"><span data-stu-id="36b4b-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="36b4b-188">Per motivi di sicurezza, è consigliabile aggiornare la VM Ubuntu al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="36b4b-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="36b4b-189">Con cloud-init è possibile eseguire questa operazione tramite lo script seguente, a seconda della distribuzione Linux in uso.</span><span class="sxs-lookup"><span data-stu-id="36b4b-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="36b4b-190">Script cloud-init `cloud_config_apt_upgrade.txt` di esempio per la famiglia Debian</span><span class="sxs-lookup"><span data-stu-id="36b4b-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="36b4b-191">Una volta avviato Linux, tutti i pacchetti installati vengono aggiornati tramite `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="36b4b-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="36b4b-192">Accedere e verificare che tutti i pacchetti siano aggiornati.</span><span class="sxs-lookup"><span data-stu-id="36b4b-192">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="36b4b-193">Creazione di uno script cloud-init per aggiungere un utente a Linux</span><span class="sxs-lookup"><span data-stu-id="36b4b-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="36b4b-194">Una delle prime attività eseguite in qualsiasi nuova VM Linux è l'aggiunta di un utente distinto da `root`, per evitare di usare quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="36b4b-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="36b4b-195">Le chiavi SSH rappresentano la procedura consigliata per la protezione e l'usabilità e vengono aggiunte al file `~/.ssh/authorized_keys` con questo script cloud-init.</span><span class="sxs-lookup"><span data-stu-id="36b4b-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="36b4b-196">Script cloud-init `cloud_config_add_users.txt` di esempio per la famiglia Debian</span><span class="sxs-lookup"><span data-stu-id="36b4b-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="36b4b-197">Una volta avviato Linux, tutti gli utenti elencati vengono creati e aggiunti al gruppo sudo.</span><span class="sxs-lookup"><span data-stu-id="36b4b-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

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

<span data-ttu-id="36b4b-198">Accedere e verificare l'utente appena creato.</span><span class="sxs-lookup"><span data-stu-id="36b4b-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="36b4b-199">Output</span><span class="sxs-lookup"><span data-stu-id="36b4b-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="36b4b-200">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36b4b-200">Next Steps</span></span>
<span data-ttu-id="36b4b-201">Cloud-init si sta affermando come metodo standard per modificare la VM Linux in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="36b4b-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="36b4b-202">Azure offre inoltre estensioni VM che consentono di modificare la VM Linux in fase di avvio o durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="36b4b-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="36b4b-203">Ad esempio, è possibile usare VMAccessExtension di Azure per reimpostare le informazioni SSH o dell'utente mentre la VM è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="36b4b-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="36b4b-204">Con cloud-init, per reimpostare la password è necessario riavviare il computer.</span><span class="sxs-lookup"><span data-stu-id="36b4b-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="36b4b-205">Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="36b4b-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="36b4b-206">Gestire utenti, SSH e dischi di controllo o di ripristino in VM Linux di Azure tramite l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="36b4b-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

