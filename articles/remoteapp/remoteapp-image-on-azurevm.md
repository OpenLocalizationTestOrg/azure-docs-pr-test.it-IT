---
title: Creare un'immagine di Azure RemoteApp basata su una macchina virtuale di Azure | Microsoft Docs
description: Informazioni su come creare un'immagine per Azure RemoteApp iniziando con una macchina virtuale di Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="d54af-103">Creare un'immagine di Azure RemoteApp basata su una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d54af-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d54af-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="d54af-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d54af-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="d54af-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d54af-106">È possibile creare immagini di Azure RemoteApp (che contengono le app condivise nella raccolta) da una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d54af-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="d54af-107">Inoltre, è possibile scegliere di utilizzare un’immagine della macchina virtuale che è stata aggiunta alla raccolta immagini della VM di Azure che soddisfa tutti i requisiti per le immagini di Azure RemoteApp: se si desidera, l'immagine della macchina virtuale può essere usata come punto di partenza per la propria macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d54af-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="d54af-108">È sufficiente cercare l'immagine "Host sessione Desktop remoto di Windows Server" nella libreria.</span><span class="sxs-lookup"><span data-stu-id="d54af-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="d54af-109">Sono necessari due passaggi per creare la propria immagine in base a una VM di Azure: la creazione dell'immagine e il caricamento dalla raccolta di macchine virtuali di Azure ad Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d54af-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="d54af-110">Creare un'immagine personalizzata basata su una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d54af-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="d54af-111">Usare questi passaggi per creare un'immagine basata su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d54af-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="d54af-112">Creare una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d54af-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="d54af-113">È possibile usare l'immagine "Windows Server Remote Desktop Session Host" o "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" dalla raccolta immagini per le macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="d54af-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="d54af-114">Questa immagine soddisfa tutti i requisiti dell'immagine modello di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d54af-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="d54af-115">Per i dettagli, vedere [Creare una macchina virtuale che esegue Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d54af-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="d54af-116">Connettersi alla macchina virtuale e installare e configurare le app da condividere mediante RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d54af-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="d54af-117">Assicurarsi di eseguire tutte le configurazioni aggiuntive di Windows richieste dalle app.</span><span class="sxs-lookup"><span data-stu-id="d54af-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="d54af-118">Per informazioni dettagliate, vedere [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Come accedere a una macchina virtuale che esegue Windows Server).</span><span class="sxs-lookup"><span data-stu-id="d54af-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="d54af-119">Se si usa una delle immagini Host sessione Desktop remoto di Windows Server, viene fornito uno script di valutazione che assicura che la macchina virtuale soddisfi i prerequisiti di RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d54af-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="d54af-120">Per eseguire lo script, fare doppio clic su **ValidateRemoteAppImage** nel desktop.</span><span class="sxs-lookup"><span data-stu-id="d54af-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="d54af-121">Assicurarsi di risolvere tutti gli errori rilevati dallo script prima di procedere al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="d54af-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="d54af-122">Generalizzare l'immagine con SYSPREP e acquisirla.</span><span class="sxs-lookup"><span data-stu-id="d54af-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="d54af-123">Per istruzioni, vedere [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (Come acquisire una macchina virtuale Windows da usare come modello).</span><span class="sxs-lookup"><span data-stu-id="d54af-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="d54af-124">Importare l'immagine nella raccolta immagini di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d54af-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="d54af-125">Usare questi passaggi per importare la nuova immagine Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="d54af-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="d54af-126">Nella scheda **Immagini modello** :</span><span class="sxs-lookup"><span data-stu-id="d54af-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="d54af-127">Se non sono disponibili immagini, fare clic su **Caricare o importare un'immagine modello**.</span><span class="sxs-lookup"><span data-stu-id="d54af-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="d54af-128">Se è presente almeno un'immagine, fare clic su **+** per aggiungere una nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="d54af-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="d54af-129">Selezionare **Importare un'immagine dalla raccolta di macchine virtuali** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d54af-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="d54af-130">Nella pagina successiva, selezionare l'immagine personalizzata dall'elenco e confermare che sono stati seguiti i passaggi elencati durante la creazione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="d54af-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="d54af-131">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d54af-131">Click **Next**.</span></span>
4. <span data-ttu-id="d54af-132">Immettere un nome per la nuova immagine di RemoteApp e scegliere il percorso, quindi fare clic sul segno di spunta per avviare il processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="d54af-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="d54af-133">È possibile importare le immagini da qualsiasi percorso di Azure supportato dalle macchine virtuali di Azure in qualsiasi percorso di Azure supportato da Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d54af-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="d54af-134">A seconda dei percorsi, l'importazione può richiedere fino a 25 minuti.</span><span class="sxs-lookup"><span data-stu-id="d54af-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="d54af-135">Ora è possibile creare la nuova raccolta, [cloud](remoteapp-create-cloud-deployment.md) o [ibrida](remoteapp-create-hybrid-deployment.md), in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d54af-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

