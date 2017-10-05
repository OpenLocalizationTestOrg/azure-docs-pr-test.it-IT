---
title: Espandere il disco del sistema operativo in una macchina virtuale Linux con l'interfaccia della riga di comando 1.0 di Azure | Microsoft Docs
description: Informazioni su come espandere il disco virtuale del sistema operativo di una macchina virtuale Linux tramite l'interfaccia della riga di comando 1.0 di Azure e il modello di distribuzione di Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0aedcd70b54c2ed47ec327ccf0529a48351353c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="61ca2-103">Espandere il disco del sistema operativo in una macchina virtuale Linux con l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="61ca2-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="61ca2-104">Le dimensioni predefinite del disco rigido virtuale per il sistema operativo sono in genere di 30 GB in una VM Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="61ca2-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="61ca2-105">È possibile [aggiungere dischi dati](add-disk.md) per aumentare lo spazio di archiviazione, ma è anche possibile espandere il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="61ca2-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="61ca2-106">Questo articolo illustra come espandere il disco del sistema operativo di una macchina virtuale Linux usando i dischi non gestiti con l'interfaccia della riga di comando 1.0 di Azure.</span><span class="sxs-lookup"><span data-stu-id="61ca2-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="61ca2-107">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="61ca2-107">CLI versions to complete the task</span></span>
<span data-ttu-id="61ca2-108">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="61ca2-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="61ca2-109">[Interfaccia della riga di comando di Azure 1.0](#prerequisites): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="61ca2-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="61ca2-110">[Interfaccia della riga di comando di Azure 2.0](expand-disks.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="61ca2-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61ca2-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="61ca2-111">Prerequisites</span></span>
<span data-ttu-id="61ca2-112">È necessario installare l'[interfaccia della riga di comando 1.0 di Azure più recente](../../cli-install-nodejs.md) e accedere a un [account di Azure](https://azure.microsoft.com/pricing/free-trial/) usando la modalità di Resource Manager nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="61ca2-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="61ca2-113">Negli esempi seguenti sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="61ca2-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="61ca2-114">I nomi dei parametri di esempio includono *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="61ca2-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="61ca2-115">Espandere il disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="61ca2-115">Expand OS disk</span></span>

1. <span data-ttu-id="61ca2-116">Non è possibile eseguire operazioni sui dischi rigidi virtuali quando la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="61ca2-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="61ca2-117">L'esempio seguente arresta e dealloca la macchina virtuale denominata *myVM* nel gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="61ca2-117">The following example stops and deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="61ca2-118">`azure vm stop` non rilascia le risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="61ca2-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="61ca2-119">Per rilasciare le risorse di calcolo, usare `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="61ca2-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="61ca2-120">Per espandere il disco rigido virtuale è necessario deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="61ca2-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="61ca2-121">Aggiornare le dimensioni del disco non gestito del sistema operativo con il comando `azure vm set`.</span><span class="sxs-lookup"><span data-stu-id="61ca2-121">Update the size of the unmanaged OS disk using the `azure vm set` command.</span></span> <span data-ttu-id="61ca2-122">L'esempio seguente aggiorna la macchina virtuale denominata *myVM* nel gruppo di risorse *myResourceGroup* per portarla a *50* GB:</span><span class="sxs-lookup"><span data-stu-id="61ca2-122">The following example updates the VM named *myVM* in the resource group named *myResourceGroup* to be *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="61ca2-123">Avviare la macchina virtuale come segue:</span><span class="sxs-lookup"><span data-stu-id="61ca2-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="61ca2-124">Eseguire SSH nella macchina virtuale con le credenziali appropriate.</span><span class="sxs-lookup"><span data-stu-id="61ca2-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="61ca2-125">Per verificare che il disco del sistema operativo sia stato ridimensionato, usare `df -h`.</span><span class="sxs-lookup"><span data-stu-id="61ca2-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="61ca2-126">L'output di esempio seguente mostra che la partizione primaria (*/dev/sda1*) ha ora una dimensione di 50 GB:</span><span class="sxs-lookup"><span data-stu-id="61ca2-126">The following example output shows the primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="61ca2-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61ca2-127">Next steps</span></span>
<span data-ttu-id="61ca2-128">Se è necessario altro spazio di archiviazione, è possibile [aggiungere dischi dati a una VM Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="61ca2-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="61ca2-129">Per altre informazioni sulla crittografia del disco, vedere [Crittografare i dischi di una VM Linux usando l'interfaccia della riga di comando di Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="61ca2-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
