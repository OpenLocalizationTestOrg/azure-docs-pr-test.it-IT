---
title: Creare una VM Linux usando l'interfaccia della riga di comando di Azure 1.0 |Microsoft Docs
description: Creare una VM Linux in Azure tramite l'interfaccia della riga di comando 1.0
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="af8e8-103">Creare una VM Linux usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="af8e8-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="af8e8-104">Questo articolo illustra come distribuire rapidamente una macchina virtuale (VM) Linux in Azure usando il comando `azure vm quick-create` nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="af8e8-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="af8e8-105">Il comando `quick-create` distribuisce una VM all'interno di un'infrastruttura di base protetta, che può essere usata per creare un prototipo o testare un concetto rapidamente.</span><span class="sxs-lookup"><span data-stu-id="af8e8-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="af8e8-106">Per creare una VM usando l'interfaccia della riga di comando di Azure 2.0, vedere [Creare una VM con l'interfaccia della riga di comando di Azure](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af8e8-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="af8e8-107">È anche possibile distribuire rapidamente una VM Linux usando il [portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af8e8-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="af8e8-108">L'articolo richiede [file di chiave pubblica e privata SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af8e8-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="af8e8-109">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="af8e8-109">Quick commands</span></span>

<span data-ttu-id="af8e8-110">L'esempio seguente mostra come distribuire una VM CoreOS e collegare la chiave SSH (Secure Shell). Gli argomenti possono variare:</span><span class="sxs-lookup"><span data-stu-id="af8e8-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="af8e8-111">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="af8e8-111">Detailed walkthrough</span></span>

<span data-ttu-id="af8e8-112">La seguente procedura riguarda la distribuzione di una VM UbuntuLTS, passo passo, con spiegazioni su ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="af8e8-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="af8e8-113">Alias del comando VM quick-create</span><span class="sxs-lookup"><span data-stu-id="af8e8-113">VM quick-create aliases</span></span>

<span data-ttu-id="af8e8-114">Per scegliere rapidamente una distribuzione è possibile usare gli alias dell'interfaccia della riga di comando di Azure con mapping alle distribuzioni di sistemi operativi più diffuse.</span><span class="sxs-lookup"><span data-stu-id="af8e8-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="af8e8-115">La tabella seguente elenca gli alias, a partire dall'interfaccia della riga di comando di Azure versione 0.10.</span><span class="sxs-lookup"><span data-stu-id="af8e8-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="af8e8-116">Per impostazione predefinita, tutte le distribuzioni che usano `quick-create` fanno uso di macchine virtuali con risorse di archiviazione basate su unità SSD, che garantiscono un provisioning più veloce e accesso al disco a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="af8e8-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="af8e8-117">Questi alias rappresentano una minima parte delle distribuzioni disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="af8e8-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="af8e8-118">Per trovare altre immagini in Azure Marketplace, è possibile [cercare un'immagine in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [sul Web](https://azure.microsoft.com/marketplace/virtual-machines/) o [caricare un'immagine personalizzata](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="af8e8-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="af8e8-119">Alias</span><span class="sxs-lookup"><span data-stu-id="af8e8-119">Alias</span></span> | <span data-ttu-id="af8e8-120">Autore</span><span class="sxs-lookup"><span data-stu-id="af8e8-120">Publisher</span></span> | <span data-ttu-id="af8e8-121">Offerta</span><span class="sxs-lookup"><span data-stu-id="af8e8-121">Offer</span></span> | <span data-ttu-id="af8e8-122">SKU</span><span class="sxs-lookup"><span data-stu-id="af8e8-122">SKU</span></span> | <span data-ttu-id="af8e8-123">Versione</span><span class="sxs-lookup"><span data-stu-id="af8e8-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="af8e8-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="af8e8-124">CentOS</span></span> |<span data-ttu-id="af8e8-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="af8e8-125">OpenLogic</span></span> |<span data-ttu-id="af8e8-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="af8e8-126">CentOS</span></span> |<span data-ttu-id="af8e8-127">7,2</span><span class="sxs-lookup"><span data-stu-id="af8e8-127">7.2</span></span> |<span data-ttu-id="af8e8-128">più recenti</span><span class="sxs-lookup"><span data-stu-id="af8e8-128">latest</span></span> |
| <span data-ttu-id="af8e8-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="af8e8-129">CoreOS</span></span> |<span data-ttu-id="af8e8-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="af8e8-130">CoreOS</span></span> |<span data-ttu-id="af8e8-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="af8e8-131">CoreOS</span></span> |<span data-ttu-id="af8e8-132">Stabile</span><span class="sxs-lookup"><span data-stu-id="af8e8-132">Stable</span></span> |<span data-ttu-id="af8e8-133">più recenti</span><span class="sxs-lookup"><span data-stu-id="af8e8-133">latest</span></span> |
| <span data-ttu-id="af8e8-134">Debian</span><span class="sxs-lookup"><span data-stu-id="af8e8-134">Debian</span></span> |<span data-ttu-id="af8e8-135">credativ</span><span class="sxs-lookup"><span data-stu-id="af8e8-135">credativ</span></span> |<span data-ttu-id="af8e8-136">Debian</span><span class="sxs-lookup"><span data-stu-id="af8e8-136">Debian</span></span> |<span data-ttu-id="af8e8-137">8</span><span class="sxs-lookup"><span data-stu-id="af8e8-137">8</span></span> |<span data-ttu-id="af8e8-138">più recenti</span><span class="sxs-lookup"><span data-stu-id="af8e8-138">latest</span></span> |
| <span data-ttu-id="af8e8-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="af8e8-139">openSUSE</span></span> |<span data-ttu-id="af8e8-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="af8e8-140">SUSE</span></span> |<span data-ttu-id="af8e8-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="af8e8-141">openSUSE</span></span> |<span data-ttu-id="af8e8-142">13.2</span><span class="sxs-lookup"><span data-stu-id="af8e8-142">13.2</span></span> |<span data-ttu-id="af8e8-143">più recenti</span><span class="sxs-lookup"><span data-stu-id="af8e8-143">latest</span></span> |
| <span data-ttu-id="af8e8-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="af8e8-144">RHEL</span></span> |<span data-ttu-id="af8e8-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="af8e8-145">Red Hat</span></span> |<span data-ttu-id="af8e8-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="af8e8-146">RHEL</span></span> |<span data-ttu-id="af8e8-147">7,2</span><span class="sxs-lookup"><span data-stu-id="af8e8-147">7.2</span></span> |<span data-ttu-id="af8e8-148">più recenti</span><span class="sxs-lookup"><span data-stu-id="af8e8-148">latest</span></span> |
| <span data-ttu-id="af8e8-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="af8e8-149">UbuntuLTS</span></span> |<span data-ttu-id="af8e8-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="af8e8-150">Canonical</span></span> |<span data-ttu-id="af8e8-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="af8e8-151">Ubuntu Server</span></span> |<span data-ttu-id="af8e8-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="af8e8-152">14.04.4-LTS</span></span> |<span data-ttu-id="af8e8-153">più recenti</span><span class="sxs-lookup"><span data-stu-id="af8e8-153">latest</span></span> |

<span data-ttu-id="af8e8-154">Le sezioni seguenti illustrano come usare l'alias `UbuntuLTS` per l'opzione **ImageURN** (`-Q`) per distribuire Ubuntu Server 14.04.4 LTS.</span><span class="sxs-lookup"><span data-stu-id="af8e8-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="af8e8-155">L'esempio `quick-create` precedente ha solo chiamato il flag `-M` per identificare la chiave pubblica SSH da caricare durante la disabilitazione delle password SSH. Viene quindi chiesto di specificare gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="af8e8-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="af8e8-156">Nome del gruppo di risorse: per il primo gruppo di risorse di Azure in genere viene accettata una stringa qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="af8e8-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="af8e8-157">Nome della VM.</span><span class="sxs-lookup"><span data-stu-id="af8e8-157">VM name</span></span>
* <span data-ttu-id="af8e8-158">posizione. `westus` o `westeurope` sono valori predefiniti idonei</span><span class="sxs-lookup"><span data-stu-id="af8e8-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="af8e8-159">Linux: per indicare ad Azure quale sistema operativo viene usato.</span><span class="sxs-lookup"><span data-stu-id="af8e8-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="af8e8-160">username</span><span class="sxs-lookup"><span data-stu-id="af8e8-160">username</span></span>

<span data-ttu-id="af8e8-161">L'esempio seguente illustra come specificare tutti i valori in modo che non vengano richieste altre conferme.</span><span class="sxs-lookup"><span data-stu-id="af8e8-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="af8e8-162">Il funzionamento è garantito, purché sia disponibile un file `~/.ssh/id_rsa.pub` come file di chiave pubblica in formato ssh-rsa:</span><span class="sxs-lookup"><span data-stu-id="af8e8-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="af8e8-163">L'output dovrebbe essere simile al blocco di output seguente:</span><span class="sxs-lookup"><span data-stu-id="af8e8-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="af8e8-164">Accedere alla nuova VM</span><span class="sxs-lookup"><span data-stu-id="af8e8-164">Log in to the new VM</span></span>
<span data-ttu-id="af8e8-165">Connettersi alla macchina virtuale usando l'indirizzo IP pubblico elencato nell'output.</span><span class="sxs-lookup"><span data-stu-id="af8e8-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="af8e8-166">È anche possibile usare il nome di dominio completo (FQDN) elencato:</span><span class="sxs-lookup"><span data-stu-id="af8e8-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="af8e8-167">Il processo di accesso dovrebbe essere simile al blocco di output seguente:</span><span class="sxs-lookup"><span data-stu-id="af8e8-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="af8e8-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af8e8-168">Next steps</span></span>
<span data-ttu-id="af8e8-169">Il comando `azure vm quick-create` consente di distribuire rapidamente una macchina virtuale per poter accedere a una shell bash e iniziare a lavorare.</span><span class="sxs-lookup"><span data-stu-id="af8e8-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="af8e8-170">L'uso di `vm quick-create` , tuttavia, non consente un controllo esteso né permette di creare un ambiente più complesso.</span><span class="sxs-lookup"><span data-stu-id="af8e8-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="af8e8-171">Per informazioni su come distribuire una VM Linux personalizzata per l'infrastruttura, è possibile vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="af8e8-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="af8e8-172">Creare un ambiente Linux completo mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="af8e8-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="af8e8-173">Creare una VM Linux usando un modello di Azure</span><span class="sxs-lookup"><span data-stu-id="af8e8-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="af8e8-174">È anche possibile [usare il driver di Azure `docker-machine` con vari comandi per creare rapidamente una VM Linux come host docker](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af8e8-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
