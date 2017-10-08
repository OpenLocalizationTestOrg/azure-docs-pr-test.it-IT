---
title: "Verificare l'unità d: di una macchina virtuale un disco dati hello | Documenti Microsoft"
description: "Descrive la modalità di lettere di unità toochange per una macchina virtuale Windows in modo che è possibile utilizzare l'unità d: hello come un'unità dati."
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
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a><span data-ttu-id="ace75-103">Utilizzare l'unità d: hello come un'unità di dati in una macchina virtuale Windows</span><span class="sxs-lookup"><span data-stu-id="ace75-103">Use hello D: drive as a data drive on a Windows VM</span></span>
<span data-ttu-id="ace75-104">Se l'applicazione deve hello toouse dati toostore di unità D, seguire questi toouse istruzioni una lettera di unità diversa per il disco temporaneo hello.</span><span class="sxs-lookup"><span data-stu-id="ace75-104">If your application needs toouse hello D drive toostore data, follow these instructions toouse a different drive letter for hello temporary disk.</span></span> <span data-ttu-id="ace75-105">Non utilizzare mai hello disco temporaneo toostore che i dati necessari tookeep.</span><span class="sxs-lookup"><span data-stu-id="ace75-105">Never use hello temporary disk toostore data that you need tookeep.</span></span>

<span data-ttu-id="ace75-106">Se si ridimensiona o **arresto (deallocazione)** una macchina virtuale, si può attivare la selezione di hello macchina virtuale tooa nuovo hypervisor.</span><span class="sxs-lookup"><span data-stu-id="ace75-106">If you resize or **Stop (Deallocate)** a virtual machine, this may trigger placement of hello virtual machine tooa new hypervisor.</span></span> <span data-ttu-id="ace75-107">Tale posizionamento può attivare un evento di manutenzione pianificato o non pianificato.</span><span class="sxs-lookup"><span data-stu-id="ace75-107">A planned or unplanned maintenance event may also trigger this placement.</span></span> <span data-ttu-id="ace75-108">In questo scenario, il disco temporaneo hello sarà toohello riassegnati prima lettera di unità disponibili.</span><span class="sxs-lookup"><span data-stu-id="ace75-108">In this scenario, hello temporary disk will be reassigned toohello first available drive letter.</span></span> <span data-ttu-id="ace75-109">Se si dispone di un'applicazione che richiede l'unità d: hello in particolare, è necessario toofollow questi passaggi tootemporarily spostamento hello pagefile.sys, collegare un nuovo disco dati e assegnargli hello lettera D e spostamento hello pagefile.sys unità temporanea toohello di eseguire il backup.</span><span class="sxs-lookup"><span data-stu-id="ace75-109">If you have an application that specifically requires hello D: drive, you need toofollow these steps tootemporarily move hello pagefile.sys, attach a new data disk and assign it hello letter D and then move hello pagefile.sys back toohello temporary drive.</span></span> <span data-ttu-id="ace75-110">Una volta completato, Azure non porterà hello d: se hello VM si sposta tooa diversi hypervisor.</span><span class="sxs-lookup"><span data-stu-id="ace75-110">Once complete, Azure will not take back hello D: if hello VM moves tooa different hypervisor.</span></span>

<span data-ttu-id="ace75-111">Per ulteriori informazioni sull'utilizzo disco temporaneo hello in Azure, vedere [informazioni sulle unità temporanea hello in macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="ace75-111">For more information about how Azure uses hello temporary disk, see [Understanding hello temporary drive on Microsoft Azure Virtual Machines](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)</span></span>

## <a name="attach-hello-data-disk"></a><span data-ttu-id="ace75-112">Collegare il disco dati hello</span><span class="sxs-lookup"><span data-stu-id="ace75-112">Attach hello data disk</span></span>
<span data-ttu-id="ace75-113">In primo luogo, è necessario tooattach hello macchina virtuale di dati su disco toohello.</span><span class="sxs-lookup"><span data-stu-id="ace75-113">First, you'll need tooattach hello data disk toohello virtual machine.</span></span> <span data-ttu-id="ace75-114">toodo questo tramite il portale di hello, vedere [come disco di tooattach dati gestiti nel portale di Azure hello](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ace75-114">toodo this using hello portal, see [How tooattach a managed data disk in hello Azure portal](attach-managed-disk-portal.md).</span></span>

## <a name="temporarily-move-pagefilesys-tooc-drive"></a><span data-ttu-id="ace75-115">Spostare pagefile.sys tooC unità</span><span class="sxs-lookup"><span data-stu-id="ace75-115">Temporarily move pagefile.sys tooC drive</span></span>
1. <span data-ttu-id="ace75-116">Connessione macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="ace75-116">Connect toohello virtual machine.</span></span> 
2. <span data-ttu-id="ace75-117">Pulsante destro del mouse hello **avviare** dal menu **sistema**.</span><span class="sxs-lookup"><span data-stu-id="ace75-117">Right-click hello **Start** menu and select **System**.</span></span>
3. <span data-ttu-id="ace75-118">Nel menu a sinistra di hello, selezionare **impostazioni di sistema avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ace75-118">In hello left-hand menu, select **Advanced system settings**.</span></span>
4. <span data-ttu-id="ace75-119">In hello **prestazioni** selezionare **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ace75-119">In hello **Performance** section, select **Settings**.</span></span>
5. <span data-ttu-id="ace75-120">Seleziona hello **avanzate** scheda.</span><span class="sxs-lookup"><span data-stu-id="ace75-120">Select hello **Advanced** tab.</span></span>
6. <span data-ttu-id="ace75-121">In hello **memoria virtuale** selezionare **modifica**.</span><span class="sxs-lookup"><span data-stu-id="ace75-121">In hello **Virtual memory** section, select **Change**.</span></span>
7. <span data-ttu-id="ace75-122">Seleziona hello **C** unità e quindi fare clic su **dimensioni gestite dal sistema** e quindi fare clic su **impostare**.</span><span class="sxs-lookup"><span data-stu-id="ace75-122">Select hello **C** drive and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="ace75-123">Seleziona hello **D** unità e quindi fare clic su **Nessun file di paging** e quindi fare clic su **impostare**.</span><span class="sxs-lookup"><span data-stu-id="ace75-123">Select hello **D** drive and then click **No paging file** and then click **Set**.</span></span>
9. <span data-ttu-id="ace75-124">Fare clic su Applica.</span><span class="sxs-lookup"><span data-stu-id="ace75-124">Click Apply.</span></span> <span data-ttu-id="ace75-125">Verrà visualizzato un avviso che computer hello deve toobe riavviare hello modifiche tootake effetto.</span><span class="sxs-lookup"><span data-stu-id="ace75-125">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
10. <span data-ttu-id="ace75-126">Riavviare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ace75-126">Restart hello virtual machine.</span></span>

## <a name="change-hello-drive-letters"></a><span data-ttu-id="ace75-127">Le lettere di unità hello</span><span class="sxs-lookup"><span data-stu-id="ace75-127">Change hello drive letters</span></span>
1. <span data-ttu-id="ace75-128">Una volta hello riavvio della macchina virtuale, eseguire nuovamente l'accesso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="ace75-128">Once hello VM restarts, log back on toohello VM.</span></span>
2. <span data-ttu-id="ace75-129">Fare clic su hello **avviare** menu e il tipo **diskmgmt.msc** e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="ace75-129">Click hello **Start** menu and type **diskmgmt.msc** and hit Enter.</span></span> <span data-ttu-id="ace75-130">Verrà avviato Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="ace75-130">Disk Management will start.</span></span>
3. <span data-ttu-id="ace75-131">Fare clic su **D**, unità di archiviazione temporanea di hello e selezionare **Cambia lettera di unità e percorsi**.</span><span class="sxs-lookup"><span data-stu-id="ace75-131">Right-click on **D**, hello Temporary Storage drive, and select **Change Drive Letter and Paths**.</span></span>
4. <span data-ttu-id="ace75-132">In Lettera unità selezionare una nuova unità, ad esempio **T**, e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ace75-132">Under Drive letter, select a new drive such as **T** and then click **OK**.</span></span> 
5. <span data-ttu-id="ace75-133">Fare clic sul disco dati hello e selezionare **Cambia lettera di unità e percorsi**.</span><span class="sxs-lookup"><span data-stu-id="ace75-133">Right-click on hello data disk, and select **Change Drive Letter and Paths**.</span></span>
6. <span data-ttu-id="ace75-134">In Lettera unità selezionare l'unità **D** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ace75-134">Under Drive letter, select drive **D** and then click **OK**.</span></span> 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a><span data-ttu-id="ace75-135">Spostare pagefile.sys unità di archiviazione temporanea toohello indietro</span><span class="sxs-lookup"><span data-stu-id="ace75-135">Move pagefile.sys back toohello temporary storage drive</span></span>
1. <span data-ttu-id="ace75-136">Pulsante destro del mouse hello **avviare** dal menu **sistema**</span><span class="sxs-lookup"><span data-stu-id="ace75-136">Right-click hello **Start** menu and select **System**</span></span>
2. <span data-ttu-id="ace75-137">Nel menu a sinistra di hello, selezionare **impostazioni di sistema avanzate**.</span><span class="sxs-lookup"><span data-stu-id="ace75-137">In hello left-hand menu, select **Advanced system settings**.</span></span>
3. <span data-ttu-id="ace75-138">In hello **prestazioni** selezionare **impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="ace75-138">In hello **Performance** section, select **Settings**.</span></span>
4. <span data-ttu-id="ace75-139">Seleziona hello **avanzate** scheda.</span><span class="sxs-lookup"><span data-stu-id="ace75-139">Select hello **Advanced** tab.</span></span>
5. <span data-ttu-id="ace75-140">In hello **memoria virtuale** selezionare **modifica**.</span><span class="sxs-lookup"><span data-stu-id="ace75-140">In hello **Virtual memory** section, select **Change**.</span></span>
6. <span data-ttu-id="ace75-141">Selezionare l'unità del sistema operativo hello **C** e fare clic su **Nessun file di paging** e quindi fare clic su **impostare**.</span><span class="sxs-lookup"><span data-stu-id="ace75-141">Select hello OS drive **C** and click **No paging file** and then click **Set**.</span></span>
7. <span data-ttu-id="ace75-142">Selezionare l'unità di archiviazione temporanea hello **T** e quindi fare clic su **dimensioni gestite dal sistema** e quindi fare clic su **impostare**.</span><span class="sxs-lookup"><span data-stu-id="ace75-142">Select hello temporary storage drive **T** and then click **System managed size** and then click **Set**.</span></span>
8. <span data-ttu-id="ace75-143">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="ace75-143">Click **Apply**.</span></span> <span data-ttu-id="ace75-144">Verrà visualizzato un avviso che computer hello deve toobe riavviare hello modifiche tootake effetto.</span><span class="sxs-lookup"><span data-stu-id="ace75-144">You will get a warning that hello computer needs toobe restarted for hello changes tootake affect.</span></span>
9. <span data-ttu-id="ace75-145">Riavviare la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="ace75-145">Restart hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ace75-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ace75-146">Next steps</span></span>
* <span data-ttu-id="ace75-147">È possibile aumentare hello archiviazione tooyour disponibili per macchina virtuale [collegando un disco dati aggiuntivo](attach-managed-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ace75-147">You can increase hello storage available tooyour virtual machine by [attaching a additional data disk](attach-managed-disk-portal.md).</span></span>

