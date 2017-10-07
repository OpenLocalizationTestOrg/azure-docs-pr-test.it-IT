---
title: aaaUpdate dispositivo StorSimple | Documenti Microsoft
description: "Viene illustrato come toouse hello StorSimple Aggiorna funzionalità tooinstall regolari e gli aggiornamenti in modalità manutenzione e aggiornamenti rapidi."
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
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a><span data-ttu-id="0b35e-103">Aggiornare il dispositivo StorSimple 8000 serie</span><span class="sxs-lookup"><span data-stu-id="0b35e-103">Update your StorSimple 8000 Series device</span></span>
## <a name="overview"></a><span data-ttu-id="0b35e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0b35e-104">Overview</span></span>
<span data-ttu-id="0b35e-105">Hello StorSimple aggiornamenti consentono tooeasily mantenere aggiornato il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b35e-105">hello StorSimple updates features allow you tooeasily keep your StorSimple device up-to-date.</span></span> <span data-ttu-id="0b35e-106">In base al tipo di aggiornamento hello, è possibile applicare il dispositivo toohello aggiornamenti hello portale di Azure classico o mediante l'interfaccia di Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-106">Depending on hello update type, you can apply updates toohello device via hello Azure classic portal or via hello Windows PowerShell interface.</span></span> <span data-ttu-id="0b35e-107">Questa esercitazione vengono descritti i tipi di aggiornamento hello e come tooinstall di essi.</span><span class="sxs-lookup"><span data-stu-id="0b35e-107">This tutorial describes hello update types and how tooinstall each of them.</span></span>

<span data-ttu-id="0b35e-108">È possibile applicare due tipi di aggiornamenti del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="0b35e-108">You can apply two types of device updates:</span></span> 

* <span data-ttu-id="0b35e-109">Aggiornamenti regolari (o in modalità normale)</span><span class="sxs-lookup"><span data-stu-id="0b35e-109">Regular (or Normal mode) updates</span></span>
* <span data-ttu-id="0b35e-110">Aggiornamenti in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="0b35e-110">Maintenance mode updates</span></span>

<span data-ttu-id="0b35e-111">È possibile installare gli aggiornamenti periodici tramite Windows PowerShell o di hello portale di Azure classico Tuttavia, è necessario utilizzare Windows PowerShell tooinstall aggiornamenti in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="0b35e-111">You can install regular updates via hello Azure classic portal or Windows PowerShell; however, you must use Windows PowerShell tooinstall Maintenance mode updates.</span></span> 

<span data-ttu-id="0b35e-112">Di seguito viene separatamente descritto ogni tipo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="0b35e-112">Each update type is described separately, below.</span></span>

### <a name="regular-updates"></a><span data-ttu-id="0b35e-113">Aggiornamenti regolari</span><span class="sxs-lookup"><span data-stu-id="0b35e-113">Regular updates</span></span>
<span data-ttu-id="0b35e-114">Gli aggiornamenti regolari sono aggiornamenti non comportano interruzioni del servizio che possono essere installati quando il dispositivo di hello è in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="0b35e-114">Regular updates are non-disruptive updates that can be installed when hello device is in Normal mode.</span></span> <span data-ttu-id="0b35e-115">Questi aggiornamenti vengono applicati tramite controller del dispositivo tooeach sito Web Microsoft Update hello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-115">These updates are applied through hello Microsoft Update website tooeach device controller.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0b35e-116">Un failover del controller possono verificarsi durante il processo di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-116">A controller failover may occur during hello update process.</span></span> <span data-ttu-id="0b35e-117">Tuttavia, questa operazione non modificherà la disponibilità o l'operatività del sistema.</span><span class="sxs-lookup"><span data-stu-id="0b35e-117">However, this will not affect system availability or operation.</span></span>
> 
> 

* <span data-ttu-id="0b35e-118">Per informazioni dettagliate su come tooinstall regular Aggiorna tramite hello portale di Azure classico, vedere [installare aggiornamenti periodici tramite hello portale di Azure classico](#install-regular-updates-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="0b35e-118">For details on how tooinstall regular updates via hello Azure classic portal, see [Install regular updates via hello Azure classic portal](#install-regular-updates-via-the-azure-classic-portal).</span></span>
* <span data-ttu-id="0b35e-119">È anche possibile installare aggiornamenti regolari tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b35e-119">You can also install regular updates via Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="0b35e-120">Per dettagli, vedere [Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple)</span><span class="sxs-lookup"><span data-stu-id="0b35e-120">For details, see [Install regular updates via Windows PowerShell for StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple).</span></span>

### <a name="maintenance-mode-updates"></a><span data-ttu-id="0b35e-121">Aggiornamenti in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="0b35e-121">Maintenance mode updates</span></span>
<span data-ttu-id="0b35e-122">Gli aggiornamenti in modalità manutenzione sono aggiornamenti problematici, come gli aggiornamenti del firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="0b35e-122">Maintenance Mode updates are disruptive updates such as disk firmware upgrades.</span></span> <span data-ttu-id="0b35e-123">Questi aggiornamenti richiedono hello dispositivo toobe modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="0b35e-123">These updates require hello device toobe put into Maintenance mode.</span></span> <span data-ttu-id="0b35e-124">Per altri dettagli, vedere [Passaggio 2: Attivare la modalità di manutenzione](#step2).</span><span class="sxs-lookup"><span data-stu-id="0b35e-124">For details, see [Step 2: Enter Maintenance mode](#step2).</span></span> <span data-ttu-id="0b35e-125">Non è possibile utilizzare gli aggiornamenti in modalità manutenzione hello Azure tooinstall portale classico.</span><span class="sxs-lookup"><span data-stu-id="0b35e-125">You cannot use hello Azure classic portal tooinstall Maintenance mode updates.</span></span> <span data-ttu-id="0b35e-126">Pertanto è necessario utilizzare Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b35e-126">Instead, you must use Windows PowerShell for StorSimple.</span></span> 

<span data-ttu-id="0b35e-127">Per informazioni dettagliate sulla modalità di aggiornamento tooinstall la modalità di manutenzione, vedere [aggiornamenti in modalità manutenzione installare tramite Windows PowerShell per StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="0b35e-127">For details on how tooinstall Maintenance mode updates, see [Install Maintenance mode updates via Windows PowerShell for StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b35e-128">Modalità manutenzione gli aggiornamenti devono essere applicate separatamente tooeach controller.</span><span class="sxs-lookup"><span data-stu-id="0b35e-128">Maintenance mode updates must be applied separately tooeach controller.</span></span> 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a><span data-ttu-id="0b35e-129">Installare gli aggiornamenti periodici tramite hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="0b35e-129">Install regular updates via hello Azure classic portal</span></span>
<span data-ttu-id="0b35e-130">È possibile utilizzare il dispositivo StorSimple tooyour di hello Azure tooapply portale classico gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="0b35e-130">You can use hello Azure classic portal tooapply updates tooyour StorSimple device.</span></span>

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="0b35e-131">Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="0b35e-131">Install regular updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="0b35e-132">In alternativa, è possibile utilizzare Windows PowerShell per gli aggiornamenti di StorSimple tooapply normale (modalità normale).</span><span class="sxs-lookup"><span data-stu-id="0b35e-132">Alternatively, you can use Windows PowerShell for StorSimple tooapply regular (Normal mode) updates.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b35e-133">Sebbene sia possibile installare gli aggiornamenti periodici tramite Windows PowerShell per StorSimple, è consigliabile installare gli aggiornamenti periodici tramite hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="0b35e-133">Although you can install regular updates using Windows PowerShell for StorSimple, we strongly recommend that you install regular updates through hello Azure classic portal.</span></span> <span data-ttu-id="0b35e-134">A partire da Update 1, controlli preliminari saranno disponibili aggiornamenti tooinstalling precedenti eseguite dal portale hello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-134">Beginning with Update 1, pre-checks will be performed prior tooinstalling updates from hello portal.</span></span> <span data-ttu-id="0b35e-135">Questi controlli preliminari preverranno errori e garantiranno un'esperienza più uniforme.</span><span class="sxs-lookup"><span data-stu-id="0b35e-135">These pre-checks will preempt failures and ensure a smoother experience.</span></span> 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="0b35e-136">Installare gli aggiornamenti in modalità manutenzione tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="0b35e-136">Install Maintenance mode updates via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="0b35e-137">Utilizzare Windows PowerShell per il dispositivo di StorSimple tooapply manutenzione modalità aggiornamenti tooyour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b35e-137">You use Windows PowerShell for StorSimple tooapply Maintenance mode updates tooyour StorSimple device.</span></span> <span data-ttu-id="0b35e-138">In questa modalità, tutte le richieste I/O sono sospese.</span><span class="sxs-lookup"><span data-stu-id="0b35e-138">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="0b35e-139">Inoltre vengono arrestati i servizi, ad esempio memoria ad accesso casuale non volatile (NVRAM) o hello servizio cluster.</span><span class="sxs-lookup"><span data-stu-id="0b35e-139">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="0b35e-140">Entrambi i controller vengono riavviati quando si entra o esce dalla modalità.</span><span class="sxs-lookup"><span data-stu-id="0b35e-140">Both controllers are rebooted when you enter or exit this mode.</span></span> <span data-ttu-id="0b35e-141">Quando si esce da questa modalità, tutti i servizi di hello riprenderanno e devono essere integri.</span><span class="sxs-lookup"><span data-stu-id="0b35e-141">When you exit this mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="0b35e-142">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="0b35e-142">(This may take a few minutes.)</span></span>

<span data-ttu-id="0b35e-143">Se è necessario tooapply aggiornamenti in modalità manutenzione, si riceverà un avviso in presenza di aggiornamenti che devono essere installati tramite hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="0b35e-143">If you need tooapply Maintenance mode updates, you will receive an alert through hello Azure classic portal that you have updates that must be installed.</span></span> <span data-ttu-id="0b35e-144">Questo avviso include istruzioni per l'utilizzo di Windows PowerShell per gli aggiornamenti di StorSimple tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-144">This alert will include instructions for using Windows PowerShell for StorSimple tooinstall hello updates.</span></span> <span data-ttu-id="0b35e-145">Dopo aver aggiornato il dispositivo, utilizzare hello stessa modalità di procedure toochange hello dispositivo tooRegular.</span><span class="sxs-lookup"><span data-stu-id="0b35e-145">After you update your device, use hello same procedure toochange hello device tooRegular mode.</span></span> <span data-ttu-id="0b35e-146">Per istruzioni dettagliate, vedere [Passaggio 4: Uscire dalla modalità di manutenzione](#step4).</span><span class="sxs-lookup"><span data-stu-id="0b35e-146">For step-by-step instructions, see [Step 4: Exit Maintenance mode](#step4).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="0b35e-147">Prima di passare alla modalità manutenzione, verificare che entrambi i controller di dispositivo sono integri controllando hello **stato Hardware** su hello **manutenzione** pagina hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="0b35e-147">Before entering Maintenance mode, verify that both device controllers are healthy by checking hello **Hardware Status** on hello **Maintenance** page in hello Azure classic portal.</span></span> <span data-ttu-id="0b35e-148">Se il controller di hello non è integro, contattare il supporto Microsoft per i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-148">If hello controller is not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="0b35e-149">Per ulteriori informazioni, visitare tooContact supporto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0b35e-149">For more information, go tooContact Microsoft Support.</span></span> 
> * <span data-ttu-id="0b35e-150">Quando si è in modalità manutenzione, è necessario tooapply hello prima di aggiornamento su un controller e quindi su hello altro controller.</span><span class="sxs-lookup"><span data-stu-id="0b35e-150">When you are in Maintenance mode, you need tooapply hello update first on one controller and then on hello other controller.</span></span>
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a><span data-ttu-id="0b35e-151">Passaggio 1: Connettere la console seriale toohello<a name="step1"></span><span class="sxs-lookup"><span data-stu-id="0b35e-151">Step 1: Connect toohello serial console <a name="step1"></span></span>
<span data-ttu-id="0b35e-152">Innanzitutto, utilizzare un'applicazione, ad esempio PuTTY tooaccess hello console seriale.</span><span class="sxs-lookup"><span data-stu-id="0b35e-152">First, use an application such as PuTTY tooaccess hello serial console.</span></span> <span data-ttu-id="0b35e-153">Hello procedura riportata di seguito viene illustrato come console seriale di toouse tooconnect PuTTY toohello.</span><span class="sxs-lookup"><span data-stu-id="0b35e-153">hello following procedure explains how toouse PuTTY tooconnect toohello serial console.</span></span>

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a><span data-ttu-id="0b35e-154">Passaggio 2: Attivare la modalità di manutenzione <a name="step2"></span><span class="sxs-lookup"><span data-stu-id="0b35e-154">Step 2: Enter Maintenance mode <a name="step2"></span></span>
<span data-ttu-id="0b35e-155">Dopo aver connesso toohello console, determinare se sono presenti aggiornamenti tooinstall e immettere tooinstall modalità manutenzione li.</span><span class="sxs-lookup"><span data-stu-id="0b35e-155">After you connect toohello console, determine whether there are updates tooinstall, and enter Maintenance mode tooinstall them.</span></span>

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a><span data-ttu-id="0b35e-156">Passaggio 3: Installare gli aggiornamenti <a name="step3"></span><span class="sxs-lookup"><span data-stu-id="0b35e-156">Step 3: Install your updates <a name="step3"></span></span>
<span data-ttu-id="0b35e-157">Successivamente, installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="0b35e-157">Next, install your updates.</span></span>

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a><span data-ttu-id="0b35e-158">Passaggio 4: Uscire dalla modalità di manutenzione <a name="step4"></span><span class="sxs-lookup"><span data-stu-id="0b35e-158">Step 4: Exit Maintenance mode <a name="step4"></span></span>
<span data-ttu-id="0b35e-159">Per terminare, uscire dalla modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="0b35e-159">Finally, exit Maintenance mode.</span></span>

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="0b35e-160">Installare gli aggiornamenti rapidi tramite Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="0b35e-160">Install hotfixes via Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="0b35e-161">A differenza degli aggiornamenti per Microsoft Azure StorSimple, gli aggiornamenti rapidi vengono installati da una cartella condivisa.</span><span class="sxs-lookup"><span data-stu-id="0b35e-161">Unlike updates for Microsoft Azure StorSimple, hotfixes are installed from a shared folder.</span></span> <span data-ttu-id="0b35e-162">Come con gli aggiornamenti, sono disponibili due tipi di aggiornamenti rapidi:</span><span class="sxs-lookup"><span data-stu-id="0b35e-162">As with updates, there are two types of hotfixes:</span></span> 

* <span data-ttu-id="0b35e-163">Aggiornamenti rapidi regolari</span><span class="sxs-lookup"><span data-stu-id="0b35e-163">Regular hotfixes</span></span> 
* <span data-ttu-id="0b35e-164">Aggiornamenti rapidi in modalità manutenzione</span><span class="sxs-lookup"><span data-stu-id="0b35e-164">Maintenance mode hotfixes</span></span>  

<span data-ttu-id="0b35e-165">Hello procedure seguenti illustrano come toouse Windows PowerShell per StorSimple tooinstall regolare e hotfix in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="0b35e-165">hello following procedures explain how toouse Windows PowerShell for StorSimple tooinstall regular and Maintenance mode hotfixes.</span></span>

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a><span data-ttu-id="0b35e-166">Cosa accade tooupdates se si esegue una factory di reimpostazione del dispositivo hello?</span><span class="sxs-lookup"><span data-stu-id="0b35e-166">What happens tooupdates if you perform a factory reset of hello device?</span></span>
<span data-ttu-id="0b35e-167">Se un dispositivo è toofactory di ripristino delle impostazioni, quindi tutti gli aggiornamenti di hello andranno persi.</span><span class="sxs-lookup"><span data-stu-id="0b35e-167">If a device is reset toofactory settings, then all hello updates are lost.</span></span> <span data-ttu-id="0b35e-168">Dopo che il dispositivo di ripristino delle impostazioni predefinite hello è registrato e configurato, sarà necessario toomanually installa gli aggiornamenti tramite hello portale di Azure classico e/o di Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b35e-168">After hello factory-reset device is registered and configured, you will need toomanually install updates through hello Azure classic portal and/or Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="0b35e-169">Per ulteriori informazioni sulle impostazioni di fabbrica, vedere [ripristinare le impostazioni predefinite di hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="0b35e-169">For more information about factory reset, see [Reset hello device toofactory default settings](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b35e-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b35e-170">Next steps</span></span>
* <span data-ttu-id="0b35e-171">Altre informazioni, vedere [tramite Windows PowerShell per StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0b35e-171">Learn more about [using Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="0b35e-172">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0b35e-172">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

