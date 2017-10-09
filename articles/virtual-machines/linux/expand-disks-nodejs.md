---
title: disco del sistema operativo aaaExpand in VM Linux con hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come tooexpand hello disco virtuale del sistema operativo (sistema operativo) in una VM Linux utilizzando hello Azure CLI 1.0 e modello di distribuzione di gestione risorse di hello
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
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="dbc42-103">Espandere il disco del sistema operativo in una VM Linux con hello Azure CLI hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dbc42-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="dbc42-104">dimensioni di disco rigido virtuale Hello predefinite per il sistema operativo hello (sistema operativo) sono in genere 30 GB in una macchina virtuale Linux (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbc42-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="dbc42-105">È possibile [aggiungere dischi dati](add-disk.md) tooprovide per ulteriore spazio di archiviazione, ma è inoltre possibile del disco del sistema operativo hello tooexpand.</span><span class="sxs-lookup"><span data-stu-id="dbc42-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="dbc42-106">In questo articolo illustra in dettaglio come tooexpand hello del sistema operativo del disco per una VM Linux con dischi non gestiti hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="dbc42-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="dbc42-107">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="dbc42-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="dbc42-108">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="dbc42-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="dbc42-109">[Azure CLI 1.0](#prerequisites) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="dbc42-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="dbc42-110">[Azure CLI 2.0](expand-disks.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="dbc42-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbc42-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dbc42-111">Prerequisites</span></span>
<span data-ttu-id="dbc42-112">È necessario hello [più recente di Azure CLI 1.0](../../cli-install-nodejs.md) installato e registrato nel tooan [account Azure](https://azure.microsoft.com/pricing/free-trial/) utilizzando la modalità di gestione risorse hello nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="dbc42-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="dbc42-113">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="dbc42-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="dbc42-114">I nomi dei parametri di esempio includono *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="dbc42-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="dbc42-115">Espandere il disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="dbc42-115">Expand OS disk</span></span>

1. <span data-ttu-id="dbc42-116">Impossibile eseguire operazioni su dischi rigidi virtuali con hello macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="dbc42-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="dbc42-117">Arresta Hello riportato e dealloca hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="dbc42-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="dbc42-118">`azure vm stop`non rilasciare le risorse di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="dbc42-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="dbc42-119">toorelease le risorse di calcolo, utilizzare `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="dbc42-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="dbc42-120">Hello VM deve essere deallocata il disco rigido virtuale di tooexpand hello.</span><span class="sxs-lookup"><span data-stu-id="dbc42-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="dbc42-121">Aggiornare hello dimensioni del disco del sistema operativo hello non gestita usando hello `azure vm set` comando.</span><span class="sxs-lookup"><span data-stu-id="dbc42-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="dbc42-122">dopo gli aggiornamenti di esempio Hello hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup* toobe *50* GB:</span><span class="sxs-lookup"><span data-stu-id="dbc42-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="dbc42-123">Avviare la macchina virtuale come segue:</span><span class="sxs-lookup"><span data-stu-id="dbc42-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="dbc42-124">SSH tooyour VM con le credenziali appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="dbc42-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="dbc42-125">disco del sistema operativo hello tooverify è stato ridimensionato, utilizzare `df -h`.</span><span class="sxs-lookup"><span data-stu-id="dbc42-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="dbc42-126">Hello output di esempio seguente mostra la partizione primaria hello (*dev/sda1*) ora è di 50 GB:</span><span class="sxs-lookup"><span data-stu-id="dbc42-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="dbc42-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbc42-127">Next steps</span></span>
<span data-ttu-id="dbc42-128">Se è necessario ulteriore spazio di archiviazione, è anche [aggiungere tooa dischi dati VM Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="dbc42-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="dbc42-129">Per ulteriori informazioni sulla crittografia del disco, vedere [Encrypt dischi in una VM Linux utilizzando hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="dbc42-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
