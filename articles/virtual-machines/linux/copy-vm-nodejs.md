---
title: una copia della VM Linux con hello Azure CLI 1.0 aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate una copia della macchina virtuale Linux di Azure con hello Azure CLI 1.0 nel modello di distribuzione di gestione risorse di hello
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="a7ae8-103">Creare una copia di una macchina virtuale di Linux in esecuzione in Azure con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a7ae8-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="a7ae8-104">In questo articolo viene illustrato come una copia della macchina virtuale di Azure (VM) in esecuzione Linux utilizzando toocreate hello il modello di distribuzione di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="a7ae8-105">Innanzitutto copiato hello del sistema operativo e dischi tooa nuovo contenitore di dati, quindi impostare le risorse di rete hello e creare hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="a7ae8-106">È anche possibile [caricare e creare una VM da un'immagine disco personalizzata](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7ae8-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a7ae8-107">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="a7ae8-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a7ae8-108">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="a7ae8-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a7ae8-109">CLI di Azure 1.0-nostri CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="a7ae8-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a7ae8-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="a7ae8-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7ae8-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a7ae8-111">Before you begin</span></span>
<span data-ttu-id="a7ae8-112">Verificare che siano soddisfatti i seguenti prerequisiti prima di iniziare i passaggi di hello hello:</span><span class="sxs-lookup"><span data-stu-id="a7ae8-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="a7ae8-113">Si dispone di hello [CLI di Azure](../../cli-install-nodejs.md) scaricato e installato nel computer.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="a7ae8-114">Sono anche necessarie alcune informazioni sulla VM Linux di Azure esistente:</span><span class="sxs-lookup"><span data-stu-id="a7ae8-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="a7ae8-115">Informazioni sulla VM di origine</span><span class="sxs-lookup"><span data-stu-id="a7ae8-115">Source VM information</span></span> | <span data-ttu-id="a7ae8-116">Dove tooget è</span><span class="sxs-lookup"><span data-stu-id="a7ae8-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="a7ae8-117">Nome della VM.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="a7ae8-118">Nome del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a7ae8-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="a7ae8-119">Location</span><span class="sxs-lookup"><span data-stu-id="a7ae8-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="a7ae8-120">Nome dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a7ae8-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="a7ae8-121">Nome del contenitore</span><span class="sxs-lookup"><span data-stu-id="a7ae8-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="a7ae8-122">Nome del file VHD della VM di origine</span><span class="sxs-lookup"><span data-stu-id="a7ae8-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="a7ae8-123">È necessario toomake elencate alcune scelte sulla nuova macchina virtuale:   </span><span class="sxs-lookup"><span data-stu-id="a7ae8-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="a7ae8-124">-Nome contenitore    </span><span class="sxs-lookup"><span data-stu-id="a7ae8-124">-Container name    </span></span><br> <span data-ttu-id="a7ae8-125">-Nome della VM    </span><span class="sxs-lookup"><span data-stu-id="a7ae8-125">-VM name    </span></span><br> <span data-ttu-id="a7ae8-126">-Dimensioni della VM    </span><span class="sxs-lookup"><span data-stu-id="a7ae8-126">-VM size    </span></span><br> <span data-ttu-id="a7ae8-127">-Nome della vNet    </span><span class="sxs-lookup"><span data-stu-id="a7ae8-127">-vNet name    </span></span><br> <span data-ttu-id="a7ae8-128">-Nome della SubNet    </span><span class="sxs-lookup"><span data-stu-id="a7ae8-128">-SubNet name    </span></span><br> <span data-ttu-id="a7ae8-129">-Nome dell'IP    </span><span class="sxs-lookup"><span data-stu-id="a7ae8-129">-IP Name    </span></span><br> <span data-ttu-id="a7ae8-130">-Nome NIC</span><span class="sxs-lookup"><span data-stu-id="a7ae8-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="a7ae8-131">Effettuare l'accesso e impostare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a7ae8-131">Login and set your subscription</span></span>
1. <span data-ttu-id="a7ae8-132">Account di accesso toohello CLI.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="a7ae8-133">Verificare di essere in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="a7ae8-134">Impostare la sottoscrizione corretta hello.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-134">Set hello correct subscription.</span></span> <span data-ttu-id="a7ae8-135">È possibile utilizzare 'elenco di account di azure' toosee tutte le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="a7ae8-136">Arrestare VM hello</span><span class="sxs-lookup"><span data-stu-id="a7ae8-136">Stop hello VM</span></span>
<span data-ttu-id="a7ae8-137">Arrestare e deallocare una macchina virtuale di origine hello.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="a7ae8-138">È possibile utilizzare 'elenco di macchine virtuali di azure' tooget un elenco di tutte le macchine virtuali hello nella sottoscrizione e i relativi nomi di gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="a7ae8-139">Copiare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a7ae8-139">Copy hello VHD</span></span>
<span data-ttu-id="a7ae8-140">È possibile copiare hello VHD hello origine archiviazione toohello di destinazione utilizzando hello `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="a7ae8-141">In questo esempio verrà toocopy hello VHD toohello stesso account di archiviazione, ma un contenitore diverso.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="a7ae8-142">toocopy hello VHD tooanother contenitore hello stesso account di archiviazione, digitare:</span><span class="sxs-lookup"><span data-stu-id="a7ae8-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="a7ae8-143">Configurare la rete virtuale di hello per la nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a7ae8-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="a7ae8-144">Configurare una rete virtuale e una scheda NIC per la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="a7ae8-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="a7ae8-145">Creare hello nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a7ae8-145">Create hello new VM</span></span>
<span data-ttu-id="a7ae8-146">È ora possibile creare una macchina virtuale dal disco virtuale caricato [utilizzando un modello di gestione risorse](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) o tramite hello CLI specificando hello URI tooyour disco copiato digitando:</span><span class="sxs-lookup"><span data-stu-id="a7ae8-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="a7ae8-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a7ae8-147">Next steps</span></span>
<span data-ttu-id="a7ae8-148">toolearn come toouse CLI di Azure toomanage nuova macchina virtuale, vedere [i comandi CLI di Azure per Gestione risorse di Azure hello](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="a7ae8-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

