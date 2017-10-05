---
title: Scaricare un disco rigido virtuale (VHD) Windows da Azure | Microsoft Docs
description: Scaricare un disco rigido virtuale Windows tramite il portale di Azure.
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
ms.openlocfilehash: d8bf89a4b7c2a158302f9ba09a182a3d8d062adc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="download-a-windows-vhd-from-azure"></a><span data-ttu-id="eadc9-103">Scaricare un disco rigido virtuale Linux da Azure</span><span class="sxs-lookup"><span data-stu-id="eadc9-103">Download a Windows VHD from Azure</span></span>

<span data-ttu-id="eadc9-104">Questo articolo illustra come scaricare un file di [disco rigido virtuale (VHD) Windows](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) da Azure usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eadc9-104">In this article, you learn how to download a [Windows virtual hard disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) file from Azure using the Azure portal.</span></span> 

<span data-ttu-id="eadc9-105">Le macchine virtuali (VM) in Azure usano i [dischi](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) come spazi in cui memorizzare un sistema operativo, le applicazioni e i dati.</span><span class="sxs-lookup"><span data-stu-id="eadc9-105">Virtual machines (VMs) in Azure use [disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) as a place to store an operating system, applications, and data.</span></span> <span data-ttu-id="eadc9-106">Tutte le macchine virtuali di Azure dispongono di almeno due dischi: un disco del sistema operativo Windows e un disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="eadc9-106">All Azure VMs have at least two disks – a Windows operating system disk and a temporary disk.</span></span> <span data-ttu-id="eadc9-107">Il disco del sistema operativo viene inizialmente creato da un'immagine e sia il disco del sistema operativo sia l'immagine sono costituiti da dischi rigidi virtuali archiviati in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eadc9-107">The operating system disk is initially created from an image, and both the operating system disk and the image are VHDs stored in an Azure storage account.</span></span> <span data-ttu-id="eadc9-108">Anche le macchine virtuali possono disporre di uno o più dischi dati archiviati in dischi rigidi virtuali.</span><span class="sxs-lookup"><span data-stu-id="eadc9-108">Virtual machines also can have one or more data disks, that are also stored as VHDs.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="eadc9-109">Arrestare la VM</span><span class="sxs-lookup"><span data-stu-id="eadc9-109">Stop the VM</span></span>

<span data-ttu-id="eadc9-110">Un disco rigido virtuale non può essere scaricato da Azure se è collegato a una macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="eadc9-110">A VHD can’t be downloaded from Azure if it's attached to a running VM.</span></span> <span data-ttu-id="eadc9-111">Per scaricare un disco rigido virtuale è quindi necessario arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="eadc9-111">You need to stop the VM to download a VHD.</span></span> <span data-ttu-id="eadc9-112">Se si vuole usare un disco rigido virtuale come [immagine](tutorial-custom-images.md) per la creazione di altre macchine virtuali con nuovi dischi, è necessario usare [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) per generalizzare il sistema operativo contenuto nel file e successivamente arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="eadc9-112">If you want to use a VHD as an [image](tutorial-custom-images.md) to create other VMs with new disks, you use [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) to generalize the operating system contained in the file and then stop the VM.</span></span> <span data-ttu-id="eadc9-113">Per usare il disco rigido virtuale come disco in cui creare una nuova istanza di un disco dati o di una macchina virtuale esistente, è sufficiente arrestare e deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="eadc9-113">To use the VHD as a disk for a new instance of an existing VM or data disk, you only need to stop and deallocate the VM.</span></span>

<span data-ttu-id="eadc9-114">Per usare il disco rigido virtuale come immagine per la creazione di altre macchine virtuali, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eadc9-114">To use the VHD as an image to create other VMs, complete these steps:</span></span>

1.  <span data-ttu-id="eadc9-115">Accedere al [portale di Azure](https://portal.azure.com/), se questa operazione non è già stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="eadc9-115">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2.  <span data-ttu-id="eadc9-116">[Connettersi alla VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eadc9-116">[Connect to the VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
3.  <span data-ttu-id="eadc9-117">Nella VM aprire la finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="eadc9-117">On the VM, open the Command Prompt window as an administrator.</span></span>
4.  <span data-ttu-id="eadc9-118">Passare alla directory *%windir%\system32\sysprep* e quindi eseguire sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="eadc9-118">Change the directory to *%windir%\system32\sysprep* and run sysprep.exe.</span></span>
5.  <span data-ttu-id="eadc9-119">Nella finestra di dialogo Utilità preparazione sistema selezionare **Passare alla Configurazione guidata** e verificare che la casella di controllo **Generalizza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="eadc9-119">In the System Preparation Tool dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that **Generalize** is selected.</span></span>
6.  <span data-ttu-id="eadc9-120">In Opzioni di arresto selezionare **Arresta il sistema** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eadc9-120">In Shutdown Options, select **Shutdown**, and then click **OK**.</span></span> 

<span data-ttu-id="eadc9-121">Per usare il disco rigido virtuale come disco in cui creare una nuova istanza di un disco dati o di una macchina virtuale esistente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="eadc9-121">To use the VHD as a disk for a new instance of an existing VM or data disk, complete these steps:</span></span>

1.  <span data-ttu-id="eadc9-122">Nel menu Hub del portale di Azure fare clic su **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="eadc9-122">On the Hub menu in the Azure portal, click **Virtual Machines**.</span></span>
2.  <span data-ttu-id="eadc9-123">Selezionare la VM dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="eadc9-123">Select the VM from the list.</span></span>
3.  <span data-ttu-id="eadc9-124">Nel pannello della VM fare clic su **Interrompi**.</span><span class="sxs-lookup"><span data-stu-id="eadc9-124">On the blade for the VM, click **Stop**.</span></span>

    ![Arrestare la macchina virtuale](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a><span data-ttu-id="eadc9-126">Generare l'URL SAS</span><span class="sxs-lookup"><span data-stu-id="eadc9-126">Generate SAS URL</span></span>

<span data-ttu-id="eadc9-127">Per scaricare il file VHD, è necessario generare un URL di [firma di accesso condiviso (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eadc9-127">To download the VHD file, you need to generate a [shared access signature (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL.</span></span> <span data-ttu-id="eadc9-128">Quando viene generato, all'URL viene assegnata una scadenza.</span><span class="sxs-lookup"><span data-stu-id="eadc9-128">When the URL is generated, an expiration time is assigned to the URL.</span></span>

1.  <span data-ttu-id="eadc9-129">Nel menu del pannello della macchina virtuale fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="eadc9-129">On the menu of the blade for the VM, click **Disks**.</span></span>
2.  <span data-ttu-id="eadc9-130">Selezionare il disco del sistema operativo per la VM e quindi fare clic su **Esporta**.</span><span class="sxs-lookup"><span data-stu-id="eadc9-130">Select the operating system disk for the VM, and then click **Export**.</span></span>
3.  <span data-ttu-id="eadc9-131">Impostare la scadenza dell'URL su *36000*.</span><span class="sxs-lookup"><span data-stu-id="eadc9-131">Set the expiration time of the URL to *36000*.</span></span>
4.  <span data-ttu-id="eadc9-132">Fare clic su **Genera URL**.</span><span class="sxs-lookup"><span data-stu-id="eadc9-132">Click **Generate URL**.</span></span>

    ![Generare l'URL](./media/download-vhd/export-generate.png)

> [!NOTE]
> <span data-ttu-id="eadc9-134">La scadenza viene aumentata rispetto all'impostazione predefinita per fornire un tempo sufficiente a scaricare il file VHD di grandi dimensioni di un sistema operativo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="eadc9-134">The expiration time is increased from the default to provide enough time to download the large VHD file for a Windows Server operating system.</span></span> <span data-ttu-id="eadc9-135">A seconda della connessione, il download di un file VHD che contiene il sistema operativo Windows Server può richiedere alcune ore.</span><span class="sxs-lookup"><span data-stu-id="eadc9-135">You can expect a VHD file that contains the Windows Server operating system to take several hours to download depending on your connection.</span></span> <span data-ttu-id="eadc9-136">Se si scarica un disco rigido virtuale per un disco dati, il tempo predefinito è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="eadc9-136">If you are downloading a VHD for a data disk, the default time is sufficient.</span></span> 
> 
> 

## <a name="download-vhd"></a><span data-ttu-id="eadc9-137">Scaricare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="eadc9-137">Download VHD</span></span>

1.  <span data-ttu-id="eadc9-138">Nell'URL appena generato fare clic su Scarica il file VHD.</span><span class="sxs-lookup"><span data-stu-id="eadc9-138">Under the URL that was generated, click Download the VHD file.</span></span>

    ![Scaricare il disco rigido virtuale](./media/download-vhd/export-download.png)

2.  <span data-ttu-id="eadc9-140">Potrebbe essere necessario fare clic su **Salva** nel browser per avviare il download.</span><span class="sxs-lookup"><span data-stu-id="eadc9-140">You may need to click **Save** in the browser to start the download.</span></span> <span data-ttu-id="eadc9-141">Il nome predefinito per il file VHD è *abcd*.</span><span class="sxs-lookup"><span data-stu-id="eadc9-141">The default name for the VHD file is *abcd*.</span></span>

    ![Fare clic su Salva nel browser.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a><span data-ttu-id="eadc9-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eadc9-143">Next steps</span></span>

- <span data-ttu-id="eadc9-144">Informazioni su come [caricare un file VHD in Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eadc9-144">Learn how to [upload a VHD file to Azure](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 
- <span data-ttu-id="eadc9-145">[Creare dischi gestiti da dischi non gestiti in un account di archiviazione](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eadc9-145">[Create managed disks from unmanaged disks in a storage account](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
- <span data-ttu-id="eadc9-146">[Gestire i dischi di Azure con PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eadc9-146">[Manage Azure disks with PowerShell](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

