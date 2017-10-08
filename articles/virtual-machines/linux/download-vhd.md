---
title: aaaDownload un VHD Linux di Azure | Documenti Microsoft
description: Scaricare un VHD Linux utilizzando hello Azure CLI e hello portale di Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a><span data-ttu-id="3a7cb-103">Scaricare un disco rigido virtuale Linux da Azure</span><span class="sxs-lookup"><span data-stu-id="3a7cb-103">Download a Linux VHD from Azure</span></span>

<span data-ttu-id="3a7cb-104">In questo articolo viene illustrato come toodownload un [Linux disco rigido virtuale (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file da Azure tramite hello Azure CLI e portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-104">In this article, you learn how toodownload a [Linux virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) file from Azure using hello Azure CLI and Azure portal.</span></span> 

<span data-ttu-id="3a7cb-105">Macchine virtuali (VM) in uso Azure [dischi](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) come un toostore sul posto del sistema operativo, applicazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-105">Virtual machines (VMs) in Azure use [disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="3a7cb-106">Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="3a7cb-107">disco del sistema operativo Hello viene inizialmente creato da un'immagine e il disco di sistema operativo hello e immagine hello sono dischi rigidi virtuali archiviati in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="3a7cb-108">Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

<span data-ttu-id="3a7cb-109">Installare l'[interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2), se non è già installata.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-109">If you haven't already done so, install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="3a7cb-110">Arrestare VM hello</span><span class="sxs-lookup"><span data-stu-id="3a7cb-110">Stop hello VM</span></span>

<span data-ttu-id="3a7cb-111">Un disco rigido virtuale non può essere scaricato da Azure se è collegato tooa in esecuzione sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-111">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="3a7cb-112">È necessario toodownload VM hello toostop un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-112">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="3a7cb-113">Se si desidera toouse un disco rigido virtuale come un [immagine](tutorial-custom-images.md) toocreate altre macchine virtuali con nuovi dischi, è necessario toodeprovision e generalizzare sistema operativo hello contenuto in hello arrestare VM hello e file.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-113">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you need toodeprovision and generalize hello operating system contained in hello file and stop hello VM.</span></span> <span data-ttu-id="3a7cb-114">hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, solo necessario toostop e deallocare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-114">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="3a7cb-115">toouse hello VHD come toocreate un'immagine con altre macchine virtuali, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3a7cb-115">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1. <span data-ttu-id="3a7cb-116">Usare SSH, nome dell'account hello e indirizzo IP pubblico hello di hello VM tooconnect tooit e deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-116">Use SSH, hello account name, and hello public IP address of hello VM tooconnect tooit and deprovision it.</span></span> <span data-ttu-id="3a7cb-117">salve + utente parametro anche rimuove l'ultimo account di provisioning utente hello.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-117">hello +user parameter also removes hello last provisioned user account.</span></span> <span data-ttu-id="3a7cb-118">Se si sono salvare le credenziali dell'account in toohello VM, omettere questo parametro utente +.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-118">If you are baking account credentials in toohello VM, leave out this +user parameter.</span></span> <span data-ttu-id="3a7cb-119">Hello esempio seguente viene rimosso ultimo account di provisioning utente hello:</span><span class="sxs-lookup"><span data-stu-id="3a7cb-119">hello following example removes hello last provisioned user account:</span></span>

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. <span data-ttu-id="3a7cb-120">Accedi tooyour account Azure con [accesso az](https://docs.microsoft.com/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3a7cb-120">Sign in tooyour Azure account with [az login](https://docs.microsoft.com/cli/azure/#login).</span></span>
3. <span data-ttu-id="3a7cb-121">Arrestare e deallocare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-121">Stop and deallocate hello VM.</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="3a7cb-122">Generalizzare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-122">Generalize hello VM.</span></span> 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

<span data-ttu-id="3a7cb-123">hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="3a7cb-123">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="3a7cb-124">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3a7cb-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="3a7cb-125">Nel menu Hub hello, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-125">On hello Hub menu, click **Virtual Machines**.</span></span>
3.  <span data-ttu-id="3a7cb-126">Selezionare hello VM hello elenco.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-126">Select hello VM from hello list.</span></span>
4.  <span data-ttu-id="3a7cb-127">Nel Pannello di hello per hello VM, fare clic su **arrestare**.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-127">On hello blade for hello VM, click **Stop**.</span></span>

    ![Arrestare la macchina virtuale](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="3a7cb-129">Generare l'URL SAS</span><span class="sxs-lookup"><span data-stu-id="3a7cb-129">Generate SAS URL</span></span>

<span data-ttu-id="3a7cb-130">file di disco rigido virtuale hello toodownload, è necessario toogenerate un [firma di accesso condiviso (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-130">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="3a7cb-131">Quando viene generato l'URL di hello, un'ora di scadenza viene assegnata toohello URL.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-131">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="3a7cb-132">Dal menu hello del pannello hello hello VM, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-132">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="3a7cb-133">Selezionare il disco del sistema operativo hello per hello macchina virtuale e quindi fare clic su **esportare**.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-133">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="3a7cb-134">Fare clic su **Genera URL**.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-134">Click **Generate URL**.</span></span>

    ![Generare l'URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a><span data-ttu-id="3a7cb-136">Scaricare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="3a7cb-136">Download VHD</span></span>

1.  <span data-ttu-id="3a7cb-137">In URL hello che è stato generato, fare clic su file VHD hello di Download.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-137">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Scaricare il disco rigido virtuale](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="3a7cb-139">Potrebbe essere necessario tooclick **salvare** nel download di hello browser toostart hello.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-139">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="3a7cb-140">il nome predefinito Hello per file di disco rigido virtuale hello è *abcd*.</span><span class="sxs-lookup"><span data-stu-id="3a7cb-140">hello default name for hello VHD file is *abcd*.</span></span>

    ![Fare clic su Salva nel browser hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="3a7cb-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3a7cb-142">Next steps</span></span>

- <span data-ttu-id="3a7cb-143">Informazioni su come troppo[caricare e creare una VM Linux da disco personalizzato con hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a7cb-143">Learn how too[upload and create a Linux VM from custom disk with hello Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
- <span data-ttu-id="3a7cb-144">[Gestire i dischi Azure hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3a7cb-144">[Manage Azure disks hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

