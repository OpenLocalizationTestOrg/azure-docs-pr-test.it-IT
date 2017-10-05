---
title: "Usare l'unità D come unità dati in una macchina virtuale Windows | Microsoft Docs"
description: "Descrive come modificare le lettere di unità per una VM Windows, in modo da poter usare l'unità D: come unità dati."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 7667175c01be2421bfc3badd83b1d8aaeb29bfde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="9c1e8-103">Usare l'unità D come unità dati in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="9c1e8-103">Use the D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="9c1e8-104">Se l'applicazione deve usare l'unità D per archiviare i dati, seguire le istruzioni seguenti per usare una lettera di unità diversa per il disco temporaneo.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-104">If your application needs to use the D drive to store data, follow these instructions to use a different drive letter for the temporary disk.</span></span> <span data-ttu-id="9c1e8-105">Non utilizzare mai il disco temporaneo per archiviare i dati da conservare.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-105">Never use the temporary disk to store data that you need to keep.</span></span>

<span data-ttu-id="9c1e8-106">Se si ridimensiona o si **Arresta (dealloca)** una macchina virtuale, potrebbe essere attivato il posizionamento della macchina virtuale su un nuovo hypervisor.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of the virtual machine to a new hypervisor.</span></span> <span data-ttu-id="9c1e8-107">Tale posizionamento può attivare un evento di manutenzione pianificato o non pianificato.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="9c1e8-108">In questo scenario il disco temporaneo sarà riassegnato alla prima lettera di unità disponibile.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-108">In this scenario, the temporary disk will be reassigned to the first available drive letter.</span></span> <span data-ttu-id="9c1e8-109">Se si dispone di un'applicazione che richiede specificamente l'unità D:, è necessario seguire questi passaggi per spostare temporaneamente pagefile.sys, collegare un nuovo disco dati e assegnargli la lettera D, quindi spostare di nuovo pagefile.sys nell’unità temporanea.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-109">If you have an application that specifically requires the D: drive, you need to follow these steps to temporarily move the pagefile.sys, attach a new data disk and assign it the letter D and then move the pagefile.sys back to the temporary drive.</span></span> <span data-ttu-id="9c1e8-110">Al termine, Azure non riprenderà D: se la VM viene spostata in un hypervisor diverso.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-110">Once complete, Azure will not take back the D: if the VM moves to a different hypervisor.</span></span>

<span data-ttu-id="9c1e8-111">Per ulteriori informazioni sull'utilizzo del disco temporaneo in Azure, vedere [Informazioni sull'unità temporanea in Macchine virtuali di Microsoft Azure.](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="9c1e8-111">For more information about how Azure uses the temporary disk, see [Understanding the temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-the-data-disk"></a><span data-ttu-id="9c1e8-112">Collegare il disco dati</span><span class="sxs-lookup"><span data-stu-id="9c1e8-112">Attach the data disk</span></span>
<span data-ttu-id="9c1e8-113">Per prima cosa è necessario collegare il disco dati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-113">First, you'll need to attach the data disk to the virtual machine.</span></span> <span data-ttu-id="9c1e8-114">Per eseguire questa operazione tramite il portale, vedere [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md) (Come collegare un disco dati gestito nel Portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="9c1e8-114">To do this using the portal, see [How to attach a managed data disk in the Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-to-c-drive"></a><span data-ttu-id="9c1e8-115">Spostare temporaneamente pagefile.sys nell'unità C</span><span class="sxs-lookup"><span data-stu-id="9c1e8-115">Temporarily move pagefile.sys to C drive</span></span>
1. <span data-ttu-id="9c1e8-116">Connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-116">Connect to the virtual machine.</span></span> 
2. <span data-ttu-id="9c1e8-117">Fare clic con il pulsante destro del mouse sul menu **Start** e selezionare **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-117">Right-click the **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="9c1e8-118">Nel menu a sinistra selezionare **Impostazioni di sistema avanzate**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-118">In the left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="9c1e8-119">Nella sezione **Prestazioni** selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-119">In the **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="9c1e8-120">Selezionare la scheda **Avanzate** .</span><span class="sxs-lookup"><span data-stu-id="9c1e8-120">Select the **Advanced** tab.</span></span>
6. <span data-ttu-id="9c1e8-121">Nella sezione **Memoria virtuale** selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-121">In the **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="9c1e8-122">Selezionare l'unità **C** e quindi fare clic su **Dimensioni gestite dal sistema** e su **Imposta**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-122">Select the **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="9c1e8-123">Selezionare l'unità **D** e quindi fare clic su **Nessun file di paging** e su **Imposta**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-123">Select the **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="9c1e8-124">Fare clic su Applica.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-124">Click Apply.</span></span> <span data-ttu-id="9c1e8-125">Verrà visualizzato un avviso che informa che è necessario riavviare il computer per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-125">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
10. <span data-ttu-id="9c1e8-126">Riavviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-126">Restart the virtual machine.</span></span>

## <a name="change-the-drive-letters"></a><span data-ttu-id="9c1e8-127">Modificare le lettere di unità</span><span class="sxs-lookup"><span data-stu-id="9c1e8-127">Change the drive letters</span></span>
1. <span data-ttu-id="9c1e8-128">Dopo il riavvio della macchina virtuale, accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-128">Once the VM restarts, log back on to the VM.</span></span>
2. <span data-ttu-id="9c1e8-129">Fare clic sul menu **Start**, digitare **diskmgmt.msc** e premere Invio.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-129">Click the **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="9c1e8-130">Verrà avviato Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-130">Disk Management will start.</span></span>
3. <span data-ttu-id="9c1e8-131">Fare clic con il pulsante destro del mouse su **D**, l'unità di archiviazione temporanea, e quindi selezionare **Cambia lettera e percorso di unità**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-131">Right-click on **D**, the Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="9c1e8-132">In Lettera unità selezionare una nuova unità, ad esempio **T**, e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="9c1e8-133">Fare clic con il pulsante destro del mouse sul disco dati e selezionare **Cambia lettera e percorso di unità**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-133">Right-click on the data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="9c1e8-134">In Lettera unità selezionare l'unità **D** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-to-the-temporary-storage-drive"></a><span data-ttu-id="9c1e8-135">Spostare nuovamente pagefile.sys nell'unità di archiviazione temporanea</span><span class="sxs-lookup"><span data-stu-id="9c1e8-135">Move pagefile.sys back to the temporary storage drive</span></span>
1. <span data-ttu-id="9c1e8-136">Fare clic con il pulsante destro del mouse sul menu **Start** e selezionare **Sistema**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-136">Right-click the **Start** menu and select **System**</span></span>
2. <span data-ttu-id="9c1e8-137">Nel menu a sinistra selezionare **Impostazioni di sistema avanzate**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-137">In the left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="9c1e8-138">Nella sezione **Prestazioni** selezionare **Impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-138">In the **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="9c1e8-139">Selezionare la scheda **Avanzate** .</span><span class="sxs-lookup"><span data-stu-id="9c1e8-139">Select the **Advanced** tab.</span></span>
5. <span data-ttu-id="9c1e8-140">Nella sezione **Memoria virtuale** selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-140">In the **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="9c1e8-141">Selezionare l'unità del sistema operativo **C** e quindi fare clic su **Nessun file di paging** e su **Imposta**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-141">Select the OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="9c1e8-142">Selezionare l'unità di archiviazione temporanea **T** e quindi fare clic su **Dimensioni gestite dal sistema** e su **Imposta**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-142">Select the temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="9c1e8-143">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-143">Click **Apply**.</span></span> <span data-ttu-id="9c1e8-144">Verrà visualizzato un avviso che informa che è necessario riavviare il computer per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-144">You will get a warning that the computer needs to be restarted for the changes to take affect.</span></span>
9. <span data-ttu-id="9c1e8-145">Riavviare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9c1e8-145">Restart the virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c1e8-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c1e8-146">Next steps</span></span>
* <span data-ttu-id="9c1e8-147">È possibile aumentare la memoria disponibile per la macchina virtuale [collegando un disco dati aggiuntivo](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9c1e8-147">You can increase the storage available to your virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

