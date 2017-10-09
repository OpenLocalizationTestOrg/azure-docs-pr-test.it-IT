---
title: un disco rigido virtuale di Windows da Azure aaaDownload | Documenti Microsoft
description: Scaricare un disco rigido virtuale di Windows utilizzando hello portale di Azure.
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="2735c-103">Scaricare un disco rigido virtuale Linux da Azure</span><span class="sxs-lookup"><span data-stu-id="2735c-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="2735c-104">In questo articolo viene illustrato come toodownload un [Windows disco rigido virtuale (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello di file da Azure tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2735c-104">In this article, you learn how toodownload a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using hello Azure portal.</span></span> 

<span data-ttu-id="2735c-105">Macchine virtuali (VM) in uso Azure [dischi](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) come un toostore sul posto del sistema operativo, applicazioni e dati.</span><span class="sxs-lookup"><span data-stu-id="2735c-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place toostore an operating system, applications, and data.</span></span> <span data-ttu-id="2735c-106">Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="2735c-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="2735c-107">disco del sistema operativo Hello viene inizialmente creato da un'immagine e il disco di sistema operativo hello e immagine hello sono dischi rigidi virtuali archiviati in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2735c-107">hello operating system disk is initially created from an image, and both hello operating system disk and hello image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="2735c-108">Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="2735c-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-hello-vm"></a><span data-ttu-id="2735c-109">Arrestare VM hello</span><span class="sxs-lookup"><span data-stu-id="2735c-109">Stop hello VM</span></span>

<span data-ttu-id="2735c-110">Un disco rigido virtuale non può essere scaricato da Azure se è collegato tooa in esecuzione sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2735c-110">A VHD can’t be downloaded from Azure if it's attached tooa running VM.</span></span> <span data-ttu-id="2735c-111">È necessario toodownload VM hello toostop un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="2735c-111">You need toostop hello VM toodownload a VHD.</span></span> <span data-ttu-id="2735c-112">Se si desidera toouse un disco rigido virtuale come un [immagine](tutorial-custom-images.md) toocreate altre macchine virtuali con nuovi dischi, utilizzare [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello contenuto nel file hello del sistema operativo e quindi arrestare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2735c-112">If you want toouse a VHD as an [image](tutorial-custom-images.md) toocreate other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello operating system contained in hello file and then stop hello VM.</span></span> <span data-ttu-id="2735c-113">hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, solo necessario toostop e deallocare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2735c-113">toouse hello VHD as a disk for a new instance of an existing VM or data disk, you only need toostop and deallocate hello VM.</span></span>

<span data-ttu-id="2735c-114">toouse hello VHD come toocreate un'immagine con altre macchine virtuali, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2735c-114">toouse hello VHD as an image toocreate other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="2735c-115">Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2735c-115">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="2735c-116">[Connettersi toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2735c-116">[Connect toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="2735c-117">Nella macchina virtuale hello, finestra hello prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2735c-117">On hello VM, open hello Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="2735c-118">Modificare anche le directory hello*%windir%\system32\sysprep* ed eseguire sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="2735c-118">Change hello directory too*%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="2735c-119">Nella finestra di dialogo Utilità preparazione sistema hello, selezionare **immettere sistema Out-of-Box guidata**e assicurarsi che **Generalize** è selezionata.</span><span class="sxs-lookup"><span data-stu-id="2735c-119">In hello System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="2735c-120">In Opzioni di arresto selezionare **Arresta il sistema** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2735c-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="2735c-121">hello toouse VHD come disco per una nuova istanza della macchina virtuale esistente o disco dati, completare questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="2735c-121">toouse hello VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="2735c-122">Menu hello Hub hello portale di Azure, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="2735c-122">On hello Hub menu in hello Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="2735c-123">Selezionare hello VM hello elenco.</span><span class="sxs-lookup"><span data-stu-id="2735c-123">Select hello VM from hello list.</span></span>
3.  <span data-ttu-id="2735c-124">Nel Pannello di hello per hello VM, fare clic su **arrestare**.</span><span class="sxs-lookup"><span data-stu-id="2735c-124">On hello blade for hello VM, click **Stop**.</span></span>

    ![Arrestare la macchina virtuale](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="2735c-126">Generare l'URL SAS</span><span class="sxs-lookup"><span data-stu-id="2735c-126">Generate SAS URL</span></span>

<span data-ttu-id="2735c-127">file di disco rigido virtuale hello toodownload, è necessario toogenerate un [firma di accesso condiviso (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span><span class="sxs-lookup"><span data-stu-id="2735c-127">toodownload hello VHD file, you need toogenerate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="2735c-128">Quando viene generato l'URL di hello, un'ora di scadenza viene assegnata toohello URL.</span><span class="sxs-lookup"><span data-stu-id="2735c-128">When hello URL is generated, an expiration time is assigned toohello URL.</span></span>

1.  <span data-ttu-id="2735c-129">Dal menu hello del pannello hello hello VM, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="2735c-129">On hello menu of hello blade for hello VM, click **Disks**.</span></span>
2.  <span data-ttu-id="2735c-130">Selezionare il disco del sistema operativo hello per hello macchina virtuale e quindi fare clic su **esportare**.</span><span class="sxs-lookup"><span data-stu-id="2735c-130">Select hello operating system disk for hello VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="2735c-131">Impostare l'ora di scadenza di hello dell'URL hello troppo*36000*.</span><span class="sxs-lookup"><span data-stu-id="2735c-131">Set hello expiration time of hello URL too*36000*.</span></span>
4.  <span data-ttu-id="2735c-132">Fare clic su **Genera URL**.</span><span class="sxs-lookup"><span data-stu-id="2735c-132">Click **Generate URL**.</span></span>

    ![Generare l'URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="2735c-134">Data di scadenza Hello è aumentato da hello predefinito tooprovide tempo sufficiente toodownload hello di grandi dimensioni file VHD per un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2735c-134">hello expiration time is increased from hello default tooprovide enough time toodownload hello large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="2735c-135">È possibile prevedere un file di disco rigido virtuale contenente tootake di sistema operativo Windows Server hello toodownload ore diverse a seconda della connessione.</span><span class="sxs-lookup"><span data-stu-id="2735c-135">You can expect a VHD file that contains hello Windows Server operating system tootake several hours toodownload depending on your connection.</span></span> <span data-ttu-id="2735c-136">Se si scarica un disco rigido virtuale per un disco dati, l'ora predefinita hello è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="2735c-136">If you are downloading a VHD for a data disk, hello default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="2735c-137">Scaricare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="2735c-137">Download VHD</span></span>

1.  <span data-ttu-id="2735c-138">In URL hello che è stato generato, fare clic su file VHD hello di Download.</span><span class="sxs-lookup"><span data-stu-id="2735c-138">Under hello URL that was generated, click Download hello VHD file.</span></span>

    ![Scaricare il disco rigido virtuale](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="2735c-140">Potrebbe essere necessario tooclick **salvare** nel download di hello browser toostart hello.</span><span class="sxs-lookup"><span data-stu-id="2735c-140">You may need tooclick **Save** in hello browser toostart hello download.</span></span> <span data-ttu-id="2735c-141">il nome predefinito Hello per file di disco rigido virtuale hello è *abcd*.</span><span class="sxs-lookup"><span data-stu-id="2735c-141">hello default name for hello VHD file is *abcd*.</span></span>

    ![Fare clic su Salva nel browser hello](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="2735c-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2735c-143">Next steps</span></span>

- <span data-ttu-id="2735c-144">Informazioni su come troppo[caricare un tooAzure file disco rigido virtuale](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2735c-144">Learn how too[upload a VHD file tooAzure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="2735c-145">[Creare dischi gestiti da dischi non gestiti in un account di archiviazione](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2735c-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="2735c-146">[Gestire i dischi di Azure con PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2735c-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

