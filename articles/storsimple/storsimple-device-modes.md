---
title: "Cambiare la modalità del dispositivo StorSimple | Microsoft Docs"
description: "Vengono descritte le modalità del dispositivo StorSimple e viene illustrato come utilizzare Windows PowerShell per StorSimple per modificare la modalità del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: e9d7d277-8a2f-45eb-9fef-355486e14cbc
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2016
ms.author: alkohli
ms.openlocfilehash: 33c65bf2eecff3914f3227c76f7d638a4507e1f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-device-mode-on-your-storsimple-device"></a><span data-ttu-id="5477c-103">Cambiare le modalità del dispositivo sul dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="5477c-103">Change the device mode on your StorSimple device</span></span>
<span data-ttu-id="5477c-104">In questo articolo viene fornita una breve descrizione delle varie modalità in cui può operare il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5477c-104">This article provides a brief description of the various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="5477c-105">Il dispositivo StorSimple può funzionare in tre modalità: normale, manutenzione e ripristino.</span><span class="sxs-lookup"><span data-stu-id="5477c-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span> 

<span data-ttu-id="5477c-106">Una volta letto l'articolo, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="5477c-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="5477c-107">Quali sono le modalità del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="5477c-107">What the StorSimple device modes are</span></span>
* <span data-ttu-id="5477c-108">Come determinare la modalità corrente del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="5477c-108">How to figure out which mode the StorSimple device is in</span></span>
* <span data-ttu-id="5477c-109">Come cambiare la modalità da normale a manutenzione e *viceversa*</span><span class="sxs-lookup"><span data-stu-id="5477c-109">How to change from normal to maintenance mode and *vice versa*</span></span>

<span data-ttu-id="5477c-110">Le attività di gestione precedenti possono essere eseguite solo tramite l'interfaccia di Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5477c-110">The above management tasks can only be performed via the Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="5477c-111">Informazioni sulle modalità del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="5477c-111">About StorSimple device modes</span></span>
<span data-ttu-id="5477c-112">Il dispositivo StorSimple può funzionare in modalità normale, manutenzione o ripristino.</span><span class="sxs-lookup"><span data-stu-id="5477c-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="5477c-113">Ognuna di queste modalità viene brevemente descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="5477c-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="5477c-114">Modalità normale</span><span class="sxs-lookup"><span data-stu-id="5477c-114">Normal mode</span></span>
<span data-ttu-id="5477c-115">Si tratta della modalità operativa normale di un dispositivo StorSimple completamente configurato.</span><span class="sxs-lookup"><span data-stu-id="5477c-115">This is defined as the normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="5477c-116">Per impostazione predefinita, il dispositivo deve essere in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="5477c-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="5477c-117">Modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="5477c-117">Maintenance mode</span></span>
<span data-ttu-id="5477c-118">Talvolta potrebbe essere necessario avere il dispositivo StorSimple in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5477c-118">Sometimes the StorSimple device may need to be placed into maintenance mode.</span></span> <span data-ttu-id="5477c-119">Questa modalità consente di eseguire la manutenzione del dispositivo e installare gli aggiornamenti improvvisi, ad esempio quelli relativi al firmware del disco.</span><span class="sxs-lookup"><span data-stu-id="5477c-119">This mode allows you to perform maintenance on the device and install disruptive updates, such as those related to disk firmware.</span></span>

<span data-ttu-id="5477c-120">È possibile porre il sistema in modalità di manutenzione solo tramite Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5477c-120">You can put the system into maintenance mode only via the Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="5477c-121">In questa modalità, tutte le richieste I/O sono sospese.</span><span class="sxs-lookup"><span data-stu-id="5477c-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="5477c-122">Inoltre vengono arrestati servizi come la memoria ad accesso casuale non volatile (NVRAM) o il servizio cluster.</span><span class="sxs-lookup"><span data-stu-id="5477c-122">Services such as non-volatile random access memory (NVRAM) or the clustering service are also stopped.</span></span> <span data-ttu-id="5477c-123">Entrambi i controller vengono riavviati quando si entra o si esce dalla modalità.</span><span class="sxs-lookup"><span data-stu-id="5477c-123">Both the controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="5477c-124">Quando si esce dalla modalità di manutenzione, tutti i servizi vengono ripresi e devono essere integri.</span><span class="sxs-lookup"><span data-stu-id="5477c-124">When you exit the maintenance mode, all the services will resume and should be healthy.</span></span> <span data-ttu-id="5477c-125">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5477c-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="5477c-126">**La modalità di manutenzione è supportata solo in un dispositivo che funziona correttamente. Non è supportata in un dispositivo in cui uno o entrambi i controller non funzionano.**
> </span><span class="sxs-lookup"><span data-stu-id="5477c-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of the controllers are not functioning.**
</span></span></br>
> 
> 

### <a name="recovery-mode"></a><span data-ttu-id="5477c-127">Modalità di ripristino</span><span class="sxs-lookup"><span data-stu-id="5477c-127">Recovery mode</span></span>
<span data-ttu-id="5477c-128">La modalità di ripristino può essere descritta come la "modalità provvisoria di Windows con supporto di rete".</span><span class="sxs-lookup"><span data-stu-id="5477c-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="5477c-129">La modalità di ripristino interessa il team del supporto tecnico Microsoft e consente di eseguire la diagnostica del sistema.</span><span class="sxs-lookup"><span data-stu-id="5477c-129">Recovery mode engages the Microsoft Support team and allows them to perform diagnostics on the system.</span></span> <span data-ttu-id="5477c-130">L'obiettivo principale della modalità di ripristino consiste nel recuperare i registri di sistema.</span><span class="sxs-lookup"><span data-stu-id="5477c-130">The primary goal of recovery mode is to retrieve the system logs.</span></span>

<span data-ttu-id="5477c-131">Se il sistema passa in modalità di ripristino, è necessario contattare il supporto tecnico Microsoft per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="5477c-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="5477c-132">Per ulteriori informazioni, andare a [Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="5477c-132">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5477c-133">**Non è possibile porre il dispositivo in modalità di ripristino. Se il dispositivo è in uno stato non valido, la modalità di ripristino tenta di impostare il dispositivo su uno stato che permetta al personale di supporto Microsoft di esaminarlo.**</span><span class="sxs-lookup"><span data-stu-id="5477c-133">**You cannot place the device in recovery mode. If the device is in a bad state, recovery mode tries to get the device into a state in which Microsoft Support personnel can examine it.**</span></span>
> 
> 

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="5477c-134">Determinare la modalità del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="5477c-134">Determine StorSimple device mode</span></span>
#### <a name="to-determine-the-current-device-mode"></a><span data-ttu-id="5477c-135">Per determinare la modalità corrente del dispositivo</span><span class="sxs-lookup"><span data-stu-id="5477c-135">To determine the current device mode</span></span>
1. <span data-ttu-id="5477c-136">Accedere alla console seriale del dispositivo seguendo i passaggi riportati in [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="5477c-136">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="5477c-137">Esaminare il messaggio dell'intestazione nel menu della console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5477c-137">Look at the banner message in the serial console menu of the device.</span></span> <span data-ttu-id="5477c-138">Questo messaggio indica in modo esplicito se il dispositivo è in modalità di manutenzione o di ripristino.</span><span class="sxs-lookup"><span data-stu-id="5477c-138">This message explicitly indicates whether the device is in maintenance or recovery mode.</span></span> <span data-ttu-id="5477c-139">Se il messaggio non contiene informazioni specifiche relative alla modalità di sistema, il dispositivo è in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="5477c-139">If the message does not contain any specific information pertaining to the system mode, the device is in normal mode.</span></span>

## <a name="change-the-storsimple-device-mode"></a><span data-ttu-id="5477c-140">Cambiare la modalità del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="5477c-140">Change the StorSimple device mode</span></span>
<span data-ttu-id="5477c-141">Per eseguire la manutenzione o installare gli aggiornamenti in modalità manutenzione, è possibile porre il dispositivo StorSimple in modalità di manutenzione (dalla modalità normale).</span><span class="sxs-lookup"><span data-stu-id="5477c-141">You can place the StorSimple device into maintenance mode (from normal mode) to perform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="5477c-142">Eseguire le procedure seguenti per attivare o disattivare la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5477c-142">Perform the following procedures to enter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5477c-143">Prima di entrare in modalità manutenzione, verificare che entrambi i controller di dispositivi siano integri effettuando l'accesso a **Stato Hardware** nella pagina **Manutenzione** nel Portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="5477c-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing the **Hardware Status** on the **Maintenance** page in the Azure classic portal.</span></span> <span data-ttu-id="5477c-144">Se uno o entrambi i controller non sono integri, contattare il supporto tecnico Microsoft per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="5477c-144">If one or both the controllers are not healthy, contact Microsoft Support for the next steps.</span></span> <span data-ttu-id="5477c-145">Per ulteriori informazioni, andare a [Contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="5477c-145">For more information, go to [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
> 
> 

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="5477c-146">Per attivare la modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="5477c-146">To enter maintenance mode</span></span>
1. <span data-ttu-id="5477c-147">Accedere alla console seriale del dispositivo seguendo i passaggi riportati in [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="5477c-147">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="5477c-148">Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="5477c-148">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="5477c-149">Quando richiesto, fornire la **password di amministratore del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="5477c-149">When prompted, provide the **device administrator password**.</span></span> <span data-ttu-id="5477c-150">La password predefinita è: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="5477c-150">The default password is: `Password1`.</span></span>
3. <span data-ttu-id="5477c-151">Al prompt dei comandi digitare</span><span class="sxs-lookup"><span data-stu-id="5477c-151">At the command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="5477c-152">Verrà visualizzato un messaggio di avviso indicante che la modalità di manutenzione interromperà tutte le richieste I/O e la connessione al portale di Azure classico e verrà richiesto di confermare che si desidera procedere.</span><span class="sxs-lookup"><span data-stu-id="5477c-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="5477c-153">Digitare **Y** per attivare la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5477c-153">Type **Y** to enter maintenance mode.</span></span>
5. <span data-ttu-id="5477c-154">Entrambi i controller verranno riavviati.</span><span class="sxs-lookup"><span data-stu-id="5477c-154">Both controllers will restart.</span></span> <span data-ttu-id="5477c-155">Una volta completato il riavvio, verrà visualizzato un altro messaggio che indica che il dispositivo è in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5477c-155">When the restart is complete, another message will appear indicating that the device is in maintenance mode.</span></span>

#### <a name="to-exit-maintenance-mode"></a><span data-ttu-id="5477c-156">Per uscire dalla modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="5477c-156">To exit maintenance mode</span></span>
1. <span data-ttu-id="5477c-157">Connettersi alla console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5477c-157">Log on to the device serial console.</span></span> <span data-ttu-id="5477c-158">Verificare nel messaggio dell'intestazione che il dispositivo è in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5477c-158">Verify from the banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="5477c-159">Al prompt dei comandi digitare:</span><span class="sxs-lookup"><span data-stu-id="5477c-159">At the command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="5477c-160">Verranno visualizzati un messaggio di avviso e un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="5477c-160">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="5477c-161">Digitare **Y** per uscire dalla modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="5477c-161">Type **Y** to exit maintenance mode.</span></span>
4. <span data-ttu-id="5477c-162">Entrambi i controller verranno riavviati.</span><span class="sxs-lookup"><span data-stu-id="5477c-162">Both controllers will restart.</span></span> <span data-ttu-id="5477c-163">Una volta completato il riavvio, verrà visualizzato un altro messaggio che indica che il dispositivo è in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="5477c-163">When the restart is complete, another message will appear indicating that the device is in normal mode.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5477c-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5477c-164">Next steps</span></span>
<span data-ttu-id="5477c-165">Informazioni su come [applicare gli aggiornamenti in modalità normale e manutenzione](storsimple-update-device.md) al dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5477c-165">Learn how to [apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

