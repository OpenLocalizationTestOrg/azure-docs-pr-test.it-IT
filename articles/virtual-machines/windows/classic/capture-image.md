---
title: Acquisire un'immagine di una macchina virtuale Windows di Azure | Microsoft Docs
description: Acquisire un'immagine di una macchina virtuale Windows di Azure creata con il modello di distribuzione classico.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 6032263848c469ce2f416306e5c91c29f4cb30e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="4bc43-103">Acquisire un'immagine di una macchina virtuale Windows di Azure creata con il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="4bc43-103">Capture an image of an Azure Windows virtual machine created with the classic deployment model.</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4bc43-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4bc43-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4bc43-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="4bc43-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4bc43-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="4bc43-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4bc43-107">Per informazioni sul modello di Gestione risorse, vedere [Acquisire un'immagine gestita di una macchina virtuale generalizzata in Azure](../capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="4bc43-107">For Resource Manager model information, see [Capture a managed image of a generalized VM in Azure](../capture-image-resource.md).</span></span>

<span data-ttu-id="4bc43-108">Questo articolo illustra come acquisire una macchina virtuale Linux che esegue Windows in modo da usarla come immagine per creare altre macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4bc43-108">This article shows you how to capture an Azure virtual machine running Windows so you can use it as an image to create other virtual machines.</span></span> <span data-ttu-id="4bc43-109">Tale immagine include il disco del sistema operativo ed eventuali dischi dati collegati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4bc43-109">This image includes the operating system disk and any data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="4bc43-110">Poiché le configurazioni di rete non sono incluse, sarà necessario impostare le configurazioni di rete quando vengono create le altre macchine virtuali che usano l'immagine.</span><span class="sxs-lookup"><span data-stu-id="4bc43-110">It doesn't include networking configurations, so you'll need to set up network configurations when you create the other virtual machines that use the image.</span></span>

<span data-ttu-id="4bc43-111">Azure archivia l'immagine in **Immagini VM (classico)**, un servizio di **Calcolo** elencato quando si visualizzano tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bc43-111">Azure stores the image under **VM images (classic)**, a **Compute** service that is listed when you view all the Azure services.</span></span> <span data-ttu-id="4bc43-112">che è anche la posizione in cui vengono archiviate le immagini caricate.</span><span class="sxs-lookup"><span data-stu-id="4bc43-112">This is the same place where any images you've uploaded are stored.</span></span> <span data-ttu-id="4bc43-113">Per altre informazioni sulle immagini, vedere [Informazioni sulle immagini per le macchine virtuali Linux](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bc43-113">For details about images, see [About images for virtual machines](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4bc43-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4bc43-114">Before you begin</span></span>
<span data-ttu-id="4bc43-115">Questa procedura presuppone che sia stata creata una macchina virtuale di Azure e che sia stato configurato il sistema operativo, inclusi gli eventuali dischi dati connessi.</span><span class="sxs-lookup"><span data-stu-id="4bc43-115">These steps assume that you've already created an Azure virtual machine and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="4bc43-116">Vedere gli articoli seguenti, se non è stato già fatto, per informazioni sulla creazione e la preparazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="4bc43-116">If you haven't done this yet, see the following articles for information on creating and preparing the virtual machine:</span></span>

* [<span data-ttu-id="4bc43-117">Creare una macchina virtuale da un'immagine</span><span class="sxs-lookup"><span data-stu-id="4bc43-117">Create a virtual machine from an image</span></span>](createportal.md)
* [<span data-ttu-id="4bc43-118">Come collegare un disco dati a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4bc43-118">How to attach a data disk to a virtual machine</span></span>](attach-disk.md)
* <span data-ttu-id="4bc43-119">Assicurarsi che i ruoli server siano supportati con Sysprep.</span><span class="sxs-lookup"><span data-stu-id="4bc43-119">Make sure the server roles are supported with Sysprep.</span></span> <span data-ttu-id="4bc43-120">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="4bc43-120">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

> [!WARNING]
> <span data-ttu-id="4bc43-121">Questo processo elimina la macchina virtuale originale dopo che viene acquisita.</span><span class="sxs-lookup"><span data-stu-id="4bc43-121">This process deletes the original virtual machine after it's captured.</span></span>
>
>

<span data-ttu-id="4bc43-122">Prima dell'acquisizione dell'immagine di una macchina virtuale di Azure, si consiglia di eseguire il backup della macchina virtuale di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4bc43-122">Prior to capturing an image of an Azure virtual machine, it is recommended the target virtual machine be backed up.</span></span> <span data-ttu-id="4bc43-123">È possibile eseguire il backup delle macchine virtuali di Azure con Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="4bc43-123">Azure virtual machines can be backed up using Azure Backup.</span></span> <span data-ttu-id="4bc43-124">Per informazioni dettagliate, vedere [Backup delle macchine virtuali di Azure](../../../backup/backup-azure-vms.md).</span><span class="sxs-lookup"><span data-stu-id="4bc43-124">For details, see [Back up Azure virtual machines](../../../backup/backup-azure-vms.md).</span></span> <span data-ttu-id="4bc43-125">Altre soluzioni sono disponibili da partner certificati.</span><span class="sxs-lookup"><span data-stu-id="4bc43-125">Other solutions are available from certified partners.</span></span> <span data-ttu-id="4bc43-126">Per scoprire ciò che è attualmente disponibile, eseguire la ricerca in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4bc43-126">To find out what’s currently available, search the Azure Marketplace.</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="4bc43-127">Acquisizione della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4bc43-127">Capture the virtual machine</span></span>
1. <span data-ttu-id="4bc43-128">Nel [portale di Azure](http://portal.azure.com) **connettersi** alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="4bc43-128">In the [Azure portal](http://portal.azure.com), **Connect** to the virtual machine.</span></span> <span data-ttu-id="4bc43-129">Per istruzioni, vedere [Come accedere a una macchina virtuale che esegue Windows Server][How to sign in to a virtual machine running Windows Server].</span><span class="sxs-lookup"><span data-stu-id="4bc43-129">For instructions, see [How to sign in to a virtual machine running Windows Server][How to sign in to a virtual machine running Windows Server].</span></span>
2. <span data-ttu-id="4bc43-130">Aprire una finestra del Prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="4bc43-130">Open a Command Prompt window as an administrator.</span></span>
3. <span data-ttu-id="4bc43-131">Impostare la directory su `%windir%\system32\sysprep`, quindi eseguire sysprep.exe.</span><span class="sxs-lookup"><span data-stu-id="4bc43-131">Change the directory to `%windir%\system32\sysprep`, and then run sysprep.exe.</span></span>
4. <span data-ttu-id="4bc43-132">Verrà visualizzata la finestra di dialogo **Utilità preparazione sistema** .</span><span class="sxs-lookup"><span data-stu-id="4bc43-132">The **System Preparation Tool** dialog box appears.</span></span> <span data-ttu-id="4bc43-133">Eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="4bc43-133">Do the following:</span></span>

   * <span data-ttu-id="4bc43-134">In **Azione pulizia sistema** selezionare **Passare alla Configurazione guidata** e verificare che l'opzione **Generalizza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="4bc43-134">In **System Cleanup Action**, select **Enter System Out-of-Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span> <span data-ttu-id="4bc43-135">Per altre informazioni sull'uso di Sysprep, vedere [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction] (Introduzione all'uso di Sysprep).</span><span class="sxs-lookup"><span data-stu-id="4bc43-135">For more information about using Sysprep, see [How to Use Sysprep: An Introduction][How to Use Sysprep: An Introduction].</span></span>
   * <span data-ttu-id="4bc43-136">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-136">In **Shutdown Options**, select **Shutdown**.</span></span>
   * <span data-ttu-id="4bc43-137">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-137">Click **OK**.</span></span>

   ![Eseguire Sysprep.](./media/capture-image/SysprepGeneral.png)
5. <span data-ttu-id="4bc43-139">Sysprep arresta la macchina virtuale il cui stato nel portale di Azure diventa **Arrestato**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-139">Sysprep shuts down the virtual machine, which changes the status of the virtual machine in the Azure portal to **Stopped**.</span></span>
6. <span data-ttu-id="4bc43-140">Nel portale di Azure, fare clic su **Immagini VM (classico)** e selezionare la macchina virtuale che si desidera acquisire.</span><span class="sxs-lookup"><span data-stu-id="4bc43-140">In the Azure portal, click **Virtual Machines (classic)** and select the virtual machine you want to capture.</span></span> <span data-ttu-id="4bc43-141">Il gruppo **Immagini VM (classico)** è elencato in **Calcolo** quando si visualizza **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-141">The **VM images (classic)** group is listed under **Compute** when you view **More services**.</span></span>

7. <span data-ttu-id="4bc43-142">Nella barra dei comandi fare clic su **Capture**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-142">On the command bar, click **Capture**.</span></span>

   ![Acquisire la macchina virtuale](./media/capture-image/CaptureVM.png)

   <span data-ttu-id="4bc43-144">Viene visualizzata la finestra di dialogo **Capture the Virtual Machine** .</span><span class="sxs-lookup"><span data-stu-id="4bc43-144">The **Capture the Virtual Machine** dialog box appears.</span></span>

8. <span data-ttu-id="4bc43-145">In **Nome immagine** digitare un nome per la nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="4bc43-145">In **Image name**, type a name for the new image.</span></span> <span data-ttu-id="4bc43-146">In **Etichetta immagine** digitare un'etichetta per la nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="4bc43-146">In **Image label**, type a label for the new image.</span></span>

9. <span data-ttu-id="4bc43-147">Fare clic su **I've run Sysprep on the virtual machine** (Sysprep è stato eseguito sulla macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="4bc43-147">Click **I've run Sysprep on the virtual machine**.</span></span> <span data-ttu-id="4bc43-148">Questa casella di controllo si riferisce alle azioni con Sysprep nei passaggi 3-5.</span><span class="sxs-lookup"><span data-stu-id="4bc43-148">This checkbox refers to the actions with Sysprep in steps 3-5.</span></span> <span data-ttu-id="4bc43-149">Prima di aggiungere un'immagine di Windows Server al set di immagini personalizzate, è _necessario_ eseguire Sysprep per generalizzare un'immagine.</span><span class="sxs-lookup"><span data-stu-id="4bc43-149">An image _must_ be generalized by running Sysprep before you add a Windows Server image to your set of custom images.</span></span>

10. <span data-ttu-id="4bc43-150">Una volta completata l'acquisizione, la nuova immagine viene resa disponibile nel **Marketplace**, in **Calcolo**, nel contenitore **Immagini VM (classico)**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-150">Once the capture completes, the new image becomes available in the **Marketplace**, in the **Compute**, **VM images (classic)** container.</span></span>

    ![Acquisizione dell'immagine eseguita correttamente](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a><span data-ttu-id="4bc43-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bc43-152">Next steps</span></span>
<span data-ttu-id="4bc43-153">L'immagine è pronta per essere utilizzata per creare macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4bc43-153">The image is ready to be used to create virtual machines.</span></span> <span data-ttu-id="4bc43-154">A tale scopo, si creerà una macchina virtuale selezionando la voce di menu **Altri servizi** nella parte inferiore del menu dei servizi, quindi **Immagini VM (classico)** nel gruppo **Calcolo**.</span><span class="sxs-lookup"><span data-stu-id="4bc43-154">To do this, you'll create a virtual machine by selecting the **More services** menu item at the bottom of the services menu, then **VM images (classic)** in the **Compute** group.</span></span> <span data-ttu-id="4bc43-155">Per istruzioni, vedere [Creare una macchina virtuale da un'immagine](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="4bc43-155">For instructions, see [Create a virtual machine from an image](createportal.md).</span></span>

[How to sign in to a virtual machine running Windows Server]:connect-logon.md
[How to Use Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[The virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of the virtual machine]: ./media/capture-image/CaptureVM.png
[Enter the image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use the captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
