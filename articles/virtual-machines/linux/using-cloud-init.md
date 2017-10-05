---
title: Usare cloud-init per personalizzare una macchina virtuale Linux | Documentazione Microsoft
description: Come usare cloud-init per personalizzare una VM Linux durante la creazione con l'interfaccia della riga di comando di Azure 2.0
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="1cac7-103">Usare cloud-init per personalizzare una VM Linux durante la creazione</span><span class="sxs-lookup"><span data-stu-id="1cac7-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="1cac7-104">Questo articolo illustra come creare script cloud-init per impostare il nome host, aggiornare i pacchetti installati e gestire gli account utente con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="1cac7-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="1cac7-105">Gli script cloud-init vengono richiamati durante la creazione di una macchina virtuale (VM) dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cac7-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="1cac7-106">Per una panoramica più approfondita sull'installazione di applicazioni, la scrittura di file di configurazione e l'inserimento di chiavi da Key Vault, vedere [questa esercitazione](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1cac7-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="1cac7-107">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1cac7-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1cac7-108">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="1cac7-108">Quick commands</span></span>
<span data-ttu-id="1cac7-109">Creare uno script cloud-init.txt che consente di impostare il nome host, aggiornare tutti i pacchetti e aggiungere un utente sudo per Linux.</span><span class="sxs-lookup"><span data-stu-id="1cac7-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="1cac7-110">Creare un gruppo di risorse per avviare le macchine virtuali con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1cac7-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1cac7-111">L'esempio seguente crea il gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1cac7-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="1cac7-112">Creare una VM Linux con [az vm create](/cli/azure/vm#create) usando cloud-init per configurarla durante l'avvio con il parametro `--custom-data`.</span><span class="sxs-lookup"><span data-stu-id="1cac7-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1cac7-113">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="1cac7-113">Detailed walkthrough</span></span>
<span data-ttu-id="1cac7-114">Quando si avvia una nuova VM Linux si ottiene un VM Linux standard senza alcuna personalizzazione né alcun adattamento.</span><span class="sxs-lookup"><span data-stu-id="1cac7-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="1cac7-115">[Cloud-init](https://cloudinit.readthedocs.org) è un metodo standard che consente di inserire uno script o alcune impostazioni di configurazione in una VM Linux quando viene avviata per la prima volta.</span><span class="sxs-lookup"><span data-stu-id="1cac7-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="1cac7-116">In Azure è possibile apportare modifiche a una VM Linux in fase di distribuzione o avvio in vari modi.</span><span class="sxs-lookup"><span data-stu-id="1cac7-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="1cac7-117">Inserire gli script che usano cloud-init.</span><span class="sxs-lookup"><span data-stu-id="1cac7-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="1cac7-118">Inserire gli script che usano l' [estensione VMAccess](using-vmaccess-extension.md)di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cac7-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="1cac7-119">Un modello di Azure che usa cloud-init.</span><span class="sxs-lookup"><span data-stu-id="1cac7-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="1cac7-120">Un modello di Azure che usa [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="1cac7-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="1cac7-121">Per inserire script in qualsiasi momento dopo l'avvio:</span><span class="sxs-lookup"><span data-stu-id="1cac7-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="1cac7-122">Esecuzione diretta di comandi tramite SSH</span><span class="sxs-lookup"><span data-stu-id="1cac7-122">SSH to run commands directly</span></span>
* <span data-ttu-id="1cac7-123">Inserire gli script usando l' [estensione VMAccess](using-vmaccess-extension.md)di Azure, in modo imperativo o in un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="1cac7-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="1cac7-124">Strumenti per la gestione della configurazione come Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="1cac7-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="1cac7-125">L'estensione VMAccess esegue uno script come radice nello stesso modo di SSH.</span><span class="sxs-lookup"><span data-stu-id="1cac7-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="1cac7-126">Tuttavia, l'utilizzo dell'estensione della VM consente di abilitare diverse funzionalità di da Azure potenzialmente utili a seconda dello scenario.</span><span class="sxs-lookup"><span data-stu-id="1cac7-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="1cac7-127">Disponibilità di cloud-init negli alias delle immagini a creazione rapida della VM di Azure:</span><span class="sxs-lookup"><span data-stu-id="1cac7-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="1cac7-128">Alias</span><span class="sxs-lookup"><span data-stu-id="1cac7-128">Alias</span></span> | <span data-ttu-id="1cac7-129">Autore</span><span class="sxs-lookup"><span data-stu-id="1cac7-129">Publisher</span></span> | <span data-ttu-id="1cac7-130">Offerta</span><span class="sxs-lookup"><span data-stu-id="1cac7-130">Offer</span></span> | <span data-ttu-id="1cac7-131">SKU</span><span class="sxs-lookup"><span data-stu-id="1cac7-131">SKU</span></span> | <span data-ttu-id="1cac7-132">Versione</span><span class="sxs-lookup"><span data-stu-id="1cac7-132">Version</span></span> | <span data-ttu-id="1cac7-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="1cac7-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="1cac7-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="1cac7-134">CentOS</span></span> |<span data-ttu-id="1cac7-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1cac7-135">OpenLogic</span></span> |<span data-ttu-id="1cac7-136">Centos</span><span class="sxs-lookup"><span data-stu-id="1cac7-136">Centos</span></span> |<span data-ttu-id="1cac7-137">7,2</span><span class="sxs-lookup"><span data-stu-id="1cac7-137">7.2</span></span> |<span data-ttu-id="1cac7-138">più recenti</span><span class="sxs-lookup"><span data-stu-id="1cac7-138">latest</span></span> |<span data-ttu-id="1cac7-139">no</span><span class="sxs-lookup"><span data-stu-id="1cac7-139">no</span></span> |
| <span data-ttu-id="1cac7-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1cac7-140">CoreOS</span></span> |<span data-ttu-id="1cac7-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1cac7-141">CoreOS</span></span> |<span data-ttu-id="1cac7-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="1cac7-142">CoreOS</span></span> |<span data-ttu-id="1cac7-143">Stabile</span><span class="sxs-lookup"><span data-stu-id="1cac7-143">Stable</span></span> |<span data-ttu-id="1cac7-144">più recenti</span><span class="sxs-lookup"><span data-stu-id="1cac7-144">latest</span></span> |<span data-ttu-id="1cac7-145">sì</span><span class="sxs-lookup"><span data-stu-id="1cac7-145">yes</span></span> |
| <span data-ttu-id="1cac7-146">Debian</span><span class="sxs-lookup"><span data-stu-id="1cac7-146">Debian</span></span> |<span data-ttu-id="1cac7-147">credativ</span><span class="sxs-lookup"><span data-stu-id="1cac7-147">credativ</span></span> |<span data-ttu-id="1cac7-148">Debian</span><span class="sxs-lookup"><span data-stu-id="1cac7-148">Debian</span></span> |<span data-ttu-id="1cac7-149">8</span><span class="sxs-lookup"><span data-stu-id="1cac7-149">8</span></span> |<span data-ttu-id="1cac7-150">più recenti</span><span class="sxs-lookup"><span data-stu-id="1cac7-150">latest</span></span> |<span data-ttu-id="1cac7-151">no</span><span class="sxs-lookup"><span data-stu-id="1cac7-151">no</span></span> |
| <span data-ttu-id="1cac7-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="1cac7-152">openSUSE</span></span> |<span data-ttu-id="1cac7-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="1cac7-153">SUSE</span></span> |<span data-ttu-id="1cac7-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="1cac7-154">openSUSE</span></span> |<span data-ttu-id="1cac7-155">13.2</span><span class="sxs-lookup"><span data-stu-id="1cac7-155">13.2</span></span> |<span data-ttu-id="1cac7-156">più recenti</span><span class="sxs-lookup"><span data-stu-id="1cac7-156">latest</span></span> |<span data-ttu-id="1cac7-157">no</span><span class="sxs-lookup"><span data-stu-id="1cac7-157">no</span></span> |
| <span data-ttu-id="1cac7-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="1cac7-158">RHEL</span></span> |<span data-ttu-id="1cac7-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="1cac7-159">Redhat</span></span> |<span data-ttu-id="1cac7-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="1cac7-160">RHEL</span></span> |<span data-ttu-id="1cac7-161">7,2</span><span class="sxs-lookup"><span data-stu-id="1cac7-161">7.2</span></span> |<span data-ttu-id="1cac7-162">più recenti</span><span class="sxs-lookup"><span data-stu-id="1cac7-162">latest</span></span> |<span data-ttu-id="1cac7-163">no</span><span class="sxs-lookup"><span data-stu-id="1cac7-163">no</span></span> |
| <span data-ttu-id="1cac7-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="1cac7-164">UbuntuLTS</span></span> |<span data-ttu-id="1cac7-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="1cac7-165">Canonical</span></span> |<span data-ttu-id="1cac7-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1cac7-166">UbuntuServer</span></span> |<span data-ttu-id="1cac7-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="1cac7-167">14.04.4-LTS</span></span> |<span data-ttu-id="1cac7-168">più recenti</span><span class="sxs-lookup"><span data-stu-id="1cac7-168">latest</span></span> |<span data-ttu-id="1cac7-169">sì</span><span class="sxs-lookup"><span data-stu-id="1cac7-169">yes</span></span> |

<span data-ttu-id="1cac7-170">Microsoft collabora con i partner per promuovere l'inclusione e il funzionamento di cloud-init con le immagini da essi fornite per Azure.</span><span class="sxs-lookup"><span data-stu-id="1cac7-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="1cac7-171">Aggiungere uno script cloud-init per la creazione della VM con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="1cac7-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="1cac7-172">Per avviare uno script cloud-init durante la creazione di una VM in Azure, specificare il file cloud-init tramite l'opzione `--custom-data` dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cac7-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="1cac7-173">Creare un gruppo di risorse per avviare le macchine virtuali con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="1cac7-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="1cac7-174">L'esempio seguente crea il gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1cac7-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="1cac7-175">Creare una VM Linux con [az vm create](/cli/azure/vm#create) usando cloud-init per configurarla durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="1cac7-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="1cac7-176">Creare uno script cloud-init per impostare il nome host di una VM Linux</span><span class="sxs-lookup"><span data-stu-id="1cac7-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="1cac7-177">Una delle impostazioni più semplici e più importanti per qualsiasi VM Linux è il nome host.</span><span class="sxs-lookup"><span data-stu-id="1cac7-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="1cac7-178">È possibile definire facilmente tale impostazione tramite cloud-init con questo script.</span><span class="sxs-lookup"><span data-stu-id="1cac7-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="1cac7-179">Script cloud-init di esempio denominato `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="1cac7-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="1cac7-180">Durante l'avvio iniziale della VM questo script cloud-init imposta il nome host su *myservername*.</span><span class="sxs-lookup"><span data-stu-id="1cac7-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="1cac7-181">Creare una VM Linux con [az vm create](/cli/azure/vm#create) usando cloud-init per configurarla durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="1cac7-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="1cac7-182">Accedere e verificare il nome host della nuova VM.</span><span class="sxs-lookup"><span data-stu-id="1cac7-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="1cac7-183">Creare uno script cloud-init</span><span class="sxs-lookup"><span data-stu-id="1cac7-183">Create a cloud-init script</span></span>
<span data-ttu-id="1cac7-184">Per motivi di sicurezza, è consigliabile aggiornare la VM Ubuntu al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="1cac7-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="1cac7-185">Con cloud-init è possibile eseguire questa operazione tramite lo script seguente, a seconda della distribuzione Linux in uso.</span><span class="sxs-lookup"><span data-stu-id="1cac7-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="1cac7-186">Script cloud-init `cloud_config_apt_upgrade.txt` di esempio per la famiglia Debian</span><span class="sxs-lookup"><span data-stu-id="1cac7-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="1cac7-187">Dopo l'avvio di Linux, tutti i pacchetti installati vengono aggiornati tramite **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="1cac7-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="1cac7-188">Creare una VM Linux con [az vm create](/cli/azure/vm#create) usando cloud-init per configurarla durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="1cac7-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="1cac7-189">Accedere e verificare che tutti i pacchetti siano aggiornati.</span><span class="sxs-lookup"><span data-stu-id="1cac7-189">Login and verify all packages are updated.</span></span>

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

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="1cac7-190">Creare uno script cloud-init per aggiungere un utente a Linux</span><span class="sxs-lookup"><span data-stu-id="1cac7-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="1cac7-191">Una delle prime attività eseguite in qualsiasi nuova VM Linux è l'aggiunta di un utente distinto da *root* o per evitare di usare quest'ultimo.</span><span class="sxs-lookup"><span data-stu-id="1cac7-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="1cac7-192">Le chiavi SSH rappresentano la procedura consigliata per la sicurezza e l'usabilità e vengono aggiunte al file *~/.ssh/authorized_keys* con questo script cloud-init.</span><span class="sxs-lookup"><span data-stu-id="1cac7-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="1cac7-193">Script cloud-init `cloud_config_add_users.txt` di esempio per la famiglia Debian</span><span class="sxs-lookup"><span data-stu-id="1cac7-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="1cac7-194">Una volta avviato Linux, tutti gli utenti elencati vengono creati e aggiunti al gruppo sudo.</span><span class="sxs-lookup"><span data-stu-id="1cac7-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="1cac7-195">Creare una VM Linux con [az vm create](/cli/azure/vm#create) usando cloud-init per configurarla durante l'avvio.</span><span class="sxs-lookup"><span data-stu-id="1cac7-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="1cac7-196">Accedere e verificare l'utente appena creato.</span><span class="sxs-lookup"><span data-stu-id="1cac7-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="1cac7-197">Output</span><span class="sxs-lookup"><span data-stu-id="1cac7-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="1cac7-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1cac7-198">Next steps</span></span>
<span data-ttu-id="1cac7-199">Cloud-init si sta affermando come metodo standard per modificare la VM Linux in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="1cac7-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="1cac7-200">Azure offre inoltre estensioni VM che consentono di modificare la VM Linux in fase di avvio o durante l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1cac7-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="1cac7-201">Ad esempio, è possibile usare VMAccessExtension di Azure per reimpostare le informazioni SSH o dell'utente mentre la VM è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1cac7-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="1cac7-202">Con cloud-init, per reimpostare la password è necessario riavviare il computer.</span><span class="sxs-lookup"><span data-stu-id="1cac7-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="1cac7-203">Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1cac7-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="1cac7-204">Gestire utenti, SSH e dischi di controllo o di ripristino in VM Linux di Azure tramite l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="1cac7-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)