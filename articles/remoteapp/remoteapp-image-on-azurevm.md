---
title: aaaCreate un'immagine di Azure RemoteApp basata su una macchina virtuale di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'immagine di Azure RemoteApp a partire da una macchina virtuale di Azure.
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
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="f94d4-103">Creare un'immagine di Azure RemoteApp basata su una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="f94d4-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f94d4-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="f94d4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f94d4-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="f94d4-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f94d4-106">È possibile creare immagini di Azure RemoteApp (che contengono hello App che condivise nella raccolta) da una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f94d4-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="f94d4-107">È anche possibile scegliere toouse un'immagine di macchina virtuale è stata aggiunta una raccolta di immagini di macchina virtuale di Azure toohello che soddisfi tutti i requisiti di immagine hello Azure RemoteApp, è possibile utilizzare l'immagine di macchina virtuale come punto di partenza per la propria macchina virtuale, se si desidera.</span><span class="sxs-lookup"><span data-stu-id="f94d4-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="f94d4-108">Cercare solo l'immagine di "Windows Server Host sessione Desktop remoto" hello nella libreria hello.</span><span class="sxs-lookup"><span data-stu-id="f94d4-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="f94d4-109">Sono disponibili due passaggi toocreate, la propria immagine basata su una macchina virtuale di Azure: creare l'immagine di hello e quindi caricare il file da tooAzure libreria di hello macchina virtuale di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f94d4-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="f94d4-110">Creare un'immagine personalizzata basata su una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="f94d4-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="f94d4-111">Utilizzare queste toocreate passaggi un'immagine basata su una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f94d4-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="f94d4-112">Creare una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f94d4-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="f94d4-113">È possibile utilizzare hello "Windows Server Host sessione Desktop remoto" o "Windows Server Remote Desktop sessione Host con Microsoft Office 365 ProPlus" immagine di hello dalla raccolta di immagini di macchina virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f94d4-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="f94d4-114">Questa immagine soddisfi tutti i requisiti di immagine hello Azure RemoteApp modello.</span><span class="sxs-lookup"><span data-stu-id="f94d4-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="f94d4-115">Per i dettagli, vedere [Creare una macchina virtuale che esegue Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f94d4-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="f94d4-116">Connettersi toohello macchina virtuale, installare e configurare App hello che si desidera tooshare tramite RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f94d4-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="f94d4-117">Verificare che tooperform eventuali configurazioni aggiuntive di Windows necessari per le app.</span><span class="sxs-lookup"><span data-stu-id="f94d4-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="f94d4-118">Per informazioni dettagliate, vedere [come tooLog nella macchina virtuale che esegue Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f94d4-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="f94d4-119">Se si utilizza una delle immagini di Windows Server Host sessione Desktop remoto hello, vi è uno script di convalida inclusi che garantirà che la macchina virtuale soddisfa hello RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="f94d4-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="f94d4-120">toorun script, fare doppio clic su **ValidateRemoteAppImage** sul desktop hello.</span><span class="sxs-lookup"><span data-stu-id="f94d4-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="f94d4-121">Verificare che tutti gli errori segnalati dallo script hello risolti prima del passaggio successivo toohello di procedere.</span><span class="sxs-lookup"><span data-stu-id="f94d4-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="f94d4-122">SYSPREP generalizzare e acquisire l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="f94d4-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="f94d4-123">Vedere [come tooCapture tooUse una macchina virtuale di Windows come modello](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="f94d4-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="f94d4-124">Importare l'immagine hello in libreria di immagini di hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="f94d4-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="f94d4-125">Utilizzare queste nuova immagine hello tooimport passaggi in Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="f94d4-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="f94d4-126">In hello **immagini modello** scheda:</span><span class="sxs-lookup"><span data-stu-id="f94d4-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="f94d4-127">Se non sono disponibili immagini, fare clic su **Caricare o importare un'immagine modello**.</span><span class="sxs-lookup"><span data-stu-id="f94d4-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="f94d4-128">Se si dispone già almeno un'immagine, fare clic su  **+**  tooadd una nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="f94d4-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="f94d4-129">Selezionare **Importare un'immagine dalla raccolta di macchine virtuali** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f94d4-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="f94d4-130">Nella pagina successiva di hello, selezionare l'immagine personalizzata hello elenco e verificare che siano seguite illustrate hello al momento della creazione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="f94d4-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="f94d4-131">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="f94d4-131">Click **Next**.</span></span>
4. <span data-ttu-id="f94d4-132">Immettere un nome per la nuova immagine di RemoteApp hello e scegliere il percorso di hello, quindi fare clic su processo di importazione hello toostart hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="f94d4-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="f94d4-133">È possibile importare immagini da qualsiasi posizione di Azure supportati da macchine virtuali di Azure tooany località di Azure supportati da Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f94d4-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="f94d4-134">A seconda delle posizioni hello importazione hello può richiedere too25 minuti.</span><span class="sxs-lookup"><span data-stu-id="f94d4-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="f94d4-135">È ora pronto toocreate la nuova raccolta, ovvero un [cloud](remoteapp-create-cloud-deployment.md) insieme o [ibrida](remoteapp-create-hybrid-deployment.md), in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="f94d4-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

