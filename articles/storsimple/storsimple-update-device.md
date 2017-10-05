---
title: Aggiornare il dispositivo StorSimple | Documentazione Microsoft
description: "Viene illustrato come utilizzare la funzionalità di aggiornamento StorSimple per installare gli aggiornamenti rapidi in modalità normale e manutenzione."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="87779-103">Aggiornare il dispositivo StorSimple 8000 serie</span><span class="sxs-lookup"><span data-stu-id="87779-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="87779-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="87779-104">Overview</span></span>
<span data-ttu-id="87779-105">La funzionalità di aggiornamento StorSimple consentono di tenere aggiornato il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87779-105">The StorSimple updates features allow you to easily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="87779-106">A seconda del tipo di aggiornamento, è possibile applicare gli aggiornamenti al dispositivo tramite il portale di Azure classico o tramite l'interfaccia Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87779-106">Depending on the update type, you can apply updates to the device via the Azure classic portal or via the Windows PowerShell interface.</span></span> <span data-ttu-id="87779-107">In questa esercitazione vengono descritti i tipi di aggiornamento e come installarli.</span><span class="sxs-lookup"><span data-stu-id="87779-107">This tutorial describes the update types and how to install each of them.</span></span>

<span data-ttu-id="87779-108">È possibile applicare due tipi di aggiornamenti del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="87779-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="87779-109">Aggiornamenti regolari (o in modalità normale)</span><span class="sxs-lookup"><span data-stu-id="87779-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="87779-110">Aggiornamenti in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="87779-110">Maintenance mode updates</span></span>

<span data-ttu-id="87779-111">È possibile installare aggiornamenti regolari tramite il portale di Azure classico o Windows PowerShell; tuttavia, è necessario utilizzare Windows PowerShell per installare gli aggiornamenti in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="87779-111">You can install regular updates via the Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell to install Maintenance mode updates.</span></span> 

<span data-ttu-id="87779-112">Di seguito viene separatamente descritto ogni tipo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="87779-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="87779-113">Aggiornamenti regolari</span><span class="sxs-lookup"><span data-stu-id="87779-113">Regular updates</span></span>
<span data-ttu-id="87779-114">Gli aggiornamenti regolari sono aggiornamenti senza interruzioni che possono essere installati quando il dispositivo è in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="87779-114">Regular updates are non-disruptive updates that can be installed when the device is in Normal mode.</span></span> <span data-ttu-id="87779-115">Questi aggiornamenti vengono applicati tramite il sito Web Microsoft Update per ogni controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87779-115">These updates are applied through the Microsoft Update website to each device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="87779-116">Durante il processo di aggiornamento può verificarsi un failover del controller.</span><span class="sxs-lookup"><span data-stu-id="87779-116">A controller failover may occur during the update process.</span></span> <span data-ttu-id="87779-117">Tuttavia, questa operazione non modificherà la disponibilità o l'operatività del sistema.</span><span class="sxs-lookup"><span data-stu-id="87779-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="87779-118">Per informazioni dettagliate su come installare aggiornamenti regolari con il portale di Azure classico, vedere [Installare gli aggiornamenti regolari tramite il portale di Azure classico](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="87779-118">For details on how to install regular updates via the Azure classic portal, see [Install regular updates via the Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="87779-119">È anche possibile installare aggiornamenti regolari tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87779-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="87779-120">Per dettagli, vedere [Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple)</span><span class="sxs-lookup"><span data-stu-id="87779-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="87779-121">Aggiornamenti in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="87779-121">Maintenance mode updates</span></span>
<span data-ttu-id="87779-122">Gli aggiornamenti in modalità manutenzione sono aggiornamenti problematici, come gli aggiornamenti del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="87779-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="87779-123">Questi aggiornamenti richiedono che il dispositivo sia in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="87779-123">These updates require the device to be put into Maintenance mode.</span></span> <span data-ttu-id="87779-124">Per altri dettagli, vedere [Passaggio 2: Attivare la modalità di manutenzione](#step2).</span><span class="sxs-lookup"><span data-stu-id="87779-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="87779-125">Per installare gli aggiornamenti in modalità manutenzione, non è possibile usare il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="87779-125">You cannot use the Azure classic portal to install Maintenance mode updates.</span></span> <span data-ttu-id="87779-126">Pertanto è necessario utilizzare Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87779-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="87779-127">Per informazioni dettagliate su come installare gli aggiornamenti in modalità manutenzione, vedere [Installare gli aggiornamenti in modalità manutenzione tramite Windows PowerShell per StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="87779-127">For details on how to install Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87779-128">Gli aggiornamenti in modalità manutenzione devono essere applicati separatamente a ogni controller.</span><span class="sxs-lookup"><span data-stu-id="87779-128">Maintenance mode updates must be applied separately to each controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a><span data-ttu-id="87779-129">Installare gli aggiornamenti regolari tramite il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="87779-129">Install regular updates via the Azure classic portal</span></span>
<span data-ttu-id="87779-130">È possibile usare il portale di Azure classico per applicare gli aggiornamenti al dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87779-130">You can use the Azure classic portal to apply updates to your StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="87779-131">Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="87779-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="87779-132">In alternativa, è possibile utilizzare Windows PowerShell per StorSimple per applicare gli aggiornamenti regolari (modalità normale).</span><span class="sxs-lookup"><span data-stu-id="87779-132">Alternatively, you can use Windows PowerShell for StorSimple to apply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87779-133">Sebbene sia possibile installare aggiornamenti regolari tramite Windows PowerShell per StorSimple, è consigliabile installare gli aggiornamenti periodici tramite il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="87779-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through the Azure classic portal.</span></span> <span data-ttu-id="87779-134">A partire dall’aggiornamento 1, verranno eseguiti controlli preliminari prima di installare gli aggiornamenti dal portale.</span><span class="sxs-lookup"><span data-stu-id="87779-134">Beginning with Update 1, pre-checks will be performed prior to installing updates from the portal.</span></span> <span data-ttu-id="87779-135">Questi controlli preliminari preverranno errori e garantiranno un'esperienza più uniforme.</span><span class="sxs-lookup"><span data-stu-id="87779-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="87779-136">Installare gli aggiornamenti in modalità manutenzione tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="87779-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="87779-137">Utilizzare Windows PowerShell per StorSimple per applicare gli aggiornamenti in modalità manutenzione al dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87779-137">You use Windows PowerShell for StorSimple to apply Maintenance mode updates to your StorSimple device.</span></span> <span data-ttu-id="87779-138">In questa modalità, tutte le richieste I/O sono sospese.</span><span class="sxs-lookup"><span data-stu-id="87779-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="87779-139">Inoltre vengono arrestati servizi come la memoria ad accesso casuale non volatile (NVRAM) o il servizio cluster.</span><span class="sxs-lookup"><span data-stu-id="87779-139">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="87779-140">Entrambi i controller vengono riavviati quando si entra o esce dalla modalità.</span><span class="sxs-lookup"><span data-stu-id="87779-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="87779-141">Quando si esce da questa modalità, tutti i servizi vengono ripresi e devono essere integri.</span><span class="sxs-lookup"><span data-stu-id="87779-141">When you exit this mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="87779-142">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="87779-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="87779-143">Se è necessario applicare gli aggiornamenti in modalità manutenzione, si riceverà un avviso tramite il portale di Azure classico riguardo gli aggiornamenti che devono essere installati.</span><span class="sxs-lookup"><span data-stu-id="87779-143">If you need to apply Maintenance mode updates, you will receive an alert through the Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="87779-144">Questo avviso include le istruzioni sull'utilizzo di Windows PowerShell per StorSimple per installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="87779-144">This alert will include instructions for using Windows PowerShell for StorSimple to install the updates.</span></span> <span data-ttu-id="87779-145">Dopo aver aggiornato il dispositivo, utilizzare la stessa procedura per modificare il dispositivo alla modalità normale.</span><span class="sxs-lookup"><span data-stu-id="87779-145">After you update your device, use the same procedure to change the device to Regular mode.</span></span> <span data-ttu-id="87779-146">Per istruzioni dettagliate, vedere [Passaggio 4: Uscire dalla modalità di manutenzione](#step4).</span><span class="sxs-lookup"><span data-stu-id="87779-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="87779-147">Prima di entrare in modalità manutenzione, verificare che entrambi i controller di dispositivi siano integri controllando lo **Stato Hardware** sulla pagina **Manutenzione** nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="87779-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="87779-148">Se il controller non è integro, contattare il supporto tecnico Microsoft per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="87779-148">If the controller is not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="87779-149">Per altre informazioni, contattare il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87779-149">For more information, go to Contact Microsoft Support.</span></span> 
> * <span data-ttu-id="87779-150">In modalità manutenzione, è necessario applicare l’aggiornamento rapido prima in un controller e poi nell’altro.</span><span class="sxs-lookup"><span data-stu-id="87779-150">When you are in Maintenance mode, you need to apply the update first on one controller and then on the other controller.</span></span>
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a><span data-ttu-id="87779-151">Passaggio 1: Connettersi alla console seriale <a name="step1"></span><span class="sxs-lookup"><span data-stu-id="87779-151">Step 1: Connect to the serial console <a name="step1"></span></span>
<span data-ttu-id="87779-152">In primo luogo, utilizzare un'applicazione come PuTTY per accedere alla console seriale.</span><span class="sxs-lookup"><span data-stu-id="87779-152">First, use an application such as PuTTY to access the serial console.</span></span> <span data-ttu-id="87779-153">La procedura seguente illustra come utilizzare PuTTY per connettersi alla console seriale.</span><span class="sxs-lookup"><span data-stu-id="87779-153">The following procedure explains how to use PuTTY to connect to the serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="87779-154">Passaggio 2: Attivare la modalità di manutenzione <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="87779-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="87779-155">Dopo la connessione alla console, determinare se sono presenti aggiornamenti da installare e attivare la modalità manutenzione per installarli.</span><span class="sxs-lookup"><span data-stu-id="87779-155">After you connect to the console, determine whether there are updates to install, and enter Maintenance mode to install them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="87779-156">Passaggio 3: Installare gli aggiornamenti <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="87779-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="87779-157">Successivamente, installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="87779-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="87779-158">Passaggio 4: Uscire dalla modalità di manutenzione <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="87779-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="87779-159">Per terminare, uscire dalla modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="87779-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="87779-160">Installare gli aggiornamenti rapidi tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="87779-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="87779-161">A differenza degli aggiornamenti per Microsoft Azure StorSimple, gli aggiornamenti rapidi vengono installati da una cartella condivisa.</span><span class="sxs-lookup"><span data-stu-id="87779-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="87779-162">Come con gli aggiornamenti, sono disponibili due tipi di aggiornamenti rapidi:</span><span class="sxs-lookup"><span data-stu-id="87779-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="87779-163">Aggiornamenti rapidi regolari</span><span class="sxs-lookup"><span data-stu-id="87779-163">Regular hotfixes</span></span> 
* <span data-ttu-id="87779-164">Aggiornamenti rapidi in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="87779-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="87779-165">Nelle procedure seguenti viene illustrato come utilizzare Windows PowerShell per StorSimple per installare aggiornamenti rapidi regolari e di modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="87779-165">The following procedures explain how to use Windows PowerShell for StorSimple to install regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a><span data-ttu-id="87779-166">Cosa accade agli aggiornamenti se si esegue un ripristino delle impostazioni predefinite?</span><span class="sxs-lookup"><span data-stu-id="87779-166">What happens to updates if you perform a factory reset of the device?</span></span>
<span data-ttu-id="87779-167">Se il dispositivo viene ripristinato alle impostazioni predefinite, tutti gli aggiornamenti vengono persi.</span><span class="sxs-lookup"><span data-stu-id="87779-167">If a device is reset to factory settings, then all the updates are lost.</span></span> <span data-ttu-id="87779-168">Dopo aver registrato e configurato il dispositivo ripristinato alle impostazioni predefinite, sarà necessario installare manualmente gli aggiornamenti tramite il portale di Azure classico e/o Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87779-168">After the factory-reset device is registered and configured, you will need to manually install updates through the Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="87779-169">Per altre informazioni sul ripristino delle impostazioni predefinite, vedere [Ripristinare le impostazioni di fabbrica del dispositivo](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="87779-169">For more information about factory reset, see [Reset the device to factory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87779-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87779-170">Next steps</span></span>
* <span data-ttu-id="87779-171">Altre informazioni sull' [utilizzo di Windows PowerShell per StorSimple per amministrare il dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="87779-171">Learn more about [using Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="87779-172">Altre informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="87779-172">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

