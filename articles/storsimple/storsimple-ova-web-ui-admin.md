---
title: web Array virtuale aaaStorSimple amministrazione dell'interfaccia utente | Documenti Microsoft
description: "Viene descritto come l'attività di amministrazione di base del dispositivo di tooperform tramite l'interfaccia utente web Array virtuale StorSimple di hello."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="4e031-103">Utilizzare hello dell'interfaccia utente Web tooadminister l'Array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="4e031-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![flusso del processo di installazione](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="4e031-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4e031-105">Overview</span></span>
<span data-ttu-id="4e031-106">esercitazioni di Hello in questo articolo si applicano versione di disponibilità generale (GA) di toohello Microsoft Azure StorSimple Virtual Array (noto anche come hello StorSimple nel dispositivo virtuale locale) in esecuzione marzo 2016.</span><span class="sxs-lookup"><span data-stu-id="4e031-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="4e031-107">Questo articolo descrive alcuni dei flussi di lavoro complessi hello e attività di gestione che possono essere eseguite su hello Array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4e031-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="4e031-108">È possibile gestire hello StorSimple Array virtuale utilizzando l'interfaccia utente (tooas cui hello interfaccia utente del portale) del servizio StorSimple Manager hello e interfaccia utente web locale per il dispositivo hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="4e031-109">Questo articolo è incentrato sulle attività hello che è possibile eseguire tramite interfaccia utente web hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="4e031-110">In questo articolo include hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="4e031-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="4e031-111">Ottenere la chiave di crittografia di hello servizio dati</span><span class="sxs-lookup"><span data-stu-id="4e031-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="4e031-112">Risolvere i problemi relativi agli errori di installazione dell'interfaccia utente Web</span><span class="sxs-lookup"><span data-stu-id="4e031-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="4e031-113">Generare un pacchetto di log</span><span class="sxs-lookup"><span data-stu-id="4e031-113">Generate a log package</span></span>
* <span data-ttu-id="4e031-114">Arrestare o riavviare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="4e031-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="4e031-115">Ottenere la chiave di crittografia di hello servizio dati</span><span class="sxs-lookup"><span data-stu-id="4e031-115">Get hello service data encryption key</span></span>
<span data-ttu-id="4e031-116">Una chiave DEK del servizio viene generata quando si registra il primo dispositivo con hello servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="4e031-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="4e031-117">Questa chiave è quindi necessario con hello servizio registrazione tooregister chiave ulteriori dispositivi con hello servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="4e031-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="4e031-118">Se è stato smarrito la chiave DEK del servizio e tooretrieve necessario, eseguire l'esempio hello passaggi hello interfaccia web locale del dispositivo hello registrato con il servizio.</span><span class="sxs-lookup"><span data-stu-id="4e031-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="4e031-119">chiave di crittografia tooget hello servizio dati</span><span class="sxs-lookup"><span data-stu-id="4e031-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="4e031-120">Connettere l'interfaccia utente web locale toohello.</span><span class="sxs-lookup"><span data-stu-id="4e031-120">Connect toohello local web UI.</span></span> <span data-ttu-id="4e031-121">Andare troppo**configurazione** > **le impostazioni del Cloud**.</span><span class="sxs-lookup"><span data-stu-id="4e031-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="4e031-122">Nella parte inferiore di hello della pagina hello, fare clic su **chiave DEK del servizio Get**.</span><span class="sxs-lookup"><span data-stu-id="4e031-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="4e031-123">Viene visualizzata una chiave.</span><span class="sxs-lookup"><span data-stu-id="4e031-123">A key will appear.</span></span> <span data-ttu-id="4e031-124">Copiare e salvare questa chiave.</span><span class="sxs-lookup"><span data-stu-id="4e031-124">Copy and save this key.</span></span>
   
    ![ottenere la chiave DEK del servizio 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="4e031-126">Risolvere i problemi relativi agli errori di installazione dell'interfaccia utente Web</span><span class="sxs-lookup"><span data-stu-id="4e031-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="4e031-127">In alcuni casi quando si configura il dispositivo di hello tramite web locale hello dell'interfaccia utente, verifichino errori.</span><span class="sxs-lookup"><span data-stu-id="4e031-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="4e031-128">toodiagnose e risolvere questi errori, è possibile eseguire il test di diagnostica hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="4e031-129">test diagnostici hello toorun</span><span class="sxs-lookup"><span data-stu-id="4e031-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="4e031-130">In hello interfaccia utente web locale, andare troppo**Troubleshooting** > **test diagnostici**.</span><span class="sxs-lookup"><span data-stu-id="4e031-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![eseguire diagnostica 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="4e031-132">Nella parte inferiore di hello della pagina hello, fare clic su **eseguire i test diagnostici**.</span><span class="sxs-lookup"><span data-stu-id="4e031-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="4e031-133">Verrà avviata test toodiagnose qualsiasi possibili problemi di rete, dispositivi, proxy web, ora o le impostazioni del cloud.</span><span class="sxs-lookup"><span data-stu-id="4e031-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="4e031-134">Si riceverà una notifica che il dispositivo hello è in esecuzione di test.</span><span class="sxs-lookup"><span data-stu-id="4e031-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="4e031-135">Dopo aver completato il test di hello, hello risultati verranno visualizzati.</span><span class="sxs-lookup"><span data-stu-id="4e031-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="4e031-136">Hello seguente esempio vengono illustrati hello risultati test di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="4e031-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="4e031-137">Si noti che le impostazioni di proxy web hello non sono state configurate su questo dispositivo, e di conseguenza, i test di proxy web hello non è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="4e031-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="4e031-138">Tutti gli altri test per le impostazioni di rete, server DNS, di hello e le impostazioni dell'ora hanno avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="4e031-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![eseguire diagnostica 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="4e031-140">Generare un pacchetto di log</span><span class="sxs-lookup"><span data-stu-id="4e031-140">Generate a log package</span></span>
<span data-ttu-id="4e031-141">Un pacchetto di log è costituito da tutti i log rilevanti hello che consentono di supporto alla risoluzione dei problemi qualsiasi dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e031-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="4e031-142">In questa versione, è possibile generare un pacchetto di log tramite l'interfaccia utente web locale hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="4e031-143">pacchetto di log hello toogenerate</span><span class="sxs-lookup"><span data-stu-id="4e031-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="4e031-144">In hello interfaccia utente web locale, andare troppo**Troubleshooting** > **i registri di sistema**.</span><span class="sxs-lookup"><span data-stu-id="4e031-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![generare pacchetto di log 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="4e031-146">Nella parte inferiore di hello della pagina hello, fare clic su **creare il pacchetto di log**.</span><span class="sxs-lookup"><span data-stu-id="4e031-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="4e031-147">Verrà creato un pacchetto di hello i registri di sistema.</span><span class="sxs-lookup"><span data-stu-id="4e031-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="4e031-148">L'operazione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="4e031-148">This will take a couple of minutes.</span></span>
   
    ![generare pacchetto di log 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="4e031-150">Dopo che viene creato correttamente i pacchetti hello e hello pagina verrà aggiornata ora hello tooindicate e data di creazione pacchetto hello si riceverà la notifica.</span><span class="sxs-lookup"><span data-stu-id="4e031-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![generare pacchetto di log 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="4e031-152">Fare clic su **Scarica pacchetto di log**.</span><span class="sxs-lookup"><span data-stu-id="4e031-152">Click **Download log package**.</span></span> <span data-ttu-id="4e031-153">Un pacchetto compresso viene scaricato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="4e031-153">A zipped package will be downloaded on your system.</span></span>
   
    ![generare pacchetto di log 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="4e031-155">È possibile decomprimere il pacchetto di log scaricati hello e visualizzare i file di registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="4e031-156">Arrestare e riavviare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="4e031-156">Shut down and restart your device</span></span>
<span data-ttu-id="4e031-157">È possibile arrestare o riavviare il dispositivo virtuale utilizzando l'interfaccia utente web locale hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="4e031-158">È consigliabile che prima di riavviare, richiedere hello volumi o condivisioni a offline nell'host di hello e quindi hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4e031-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="4e031-159">Questa operazione consente di eliminare qualsiasi  rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="4e031-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="4e031-160">tooshut verso il basso il dispositivo virtuale</span><span class="sxs-lookup"><span data-stu-id="4e031-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="4e031-161">In hello interfaccia utente web locale, andare troppo**manutenzione** > **impostazioni di risparmio energia**.</span><span class="sxs-lookup"><span data-stu-id="4e031-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="4e031-162">Nella parte inferiore di hello della pagina hello, fare clic su **arresto**.</span><span class="sxs-lookup"><span data-stu-id="4e031-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![arresto del dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="4e031-164">Verrà visualizzato un avviso che informa che un arresto del dispositivo hello interromperà tutti i/o in corso, risultante in un tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="4e031-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="4e031-165">Fare clic sull'icona di controllo hello</span><span class="sxs-lookup"><span data-stu-id="4e031-165">Click hello check icon</span></span> ![icona del segno di spunta](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="4e031-167">.</span><span class="sxs-lookup"><span data-stu-id="4e031-167">.</span></span>
   
    ![avviso di arresto del dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="4e031-169">Si riceverà una notifica che è stata avviata la chiusura hello.</span><span class="sxs-lookup"><span data-stu-id="4e031-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![arresto del dispositivo avviato](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="4e031-171">dispositivo Hello verrà arrestato.</span><span class="sxs-lookup"><span data-stu-id="4e031-171">hello device will now shut down.</span></span> <span data-ttu-id="4e031-172">Se si desidera toostart il dispositivo, è necessario toodo che tramite hello Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="4e031-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="4e031-173">toorestart del dispositivo virtuale</span><span class="sxs-lookup"><span data-stu-id="4e031-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="4e031-174">In hello interfaccia utente web locale, andare troppo**manutenzione** > **impostazioni di risparmio energia**.</span><span class="sxs-lookup"><span data-stu-id="4e031-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="4e031-175">Nella parte inferiore di hello della pagina hello, fare clic su **riavviare**.</span><span class="sxs-lookup"><span data-stu-id="4e031-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![riavvio del dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="4e031-177">Verrà visualizzato un avviso che informa che il dispositivo hello riavviare interromperà qualsiasi IOs in corso, risultante in un tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="4e031-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="4e031-178">Fare clic sull'icona di controllo hello</span><span class="sxs-lookup"><span data-stu-id="4e031-178">Click hello check icon</span></span> ![icona del segno di spunta](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="4e031-180">.</span><span class="sxs-lookup"><span data-stu-id="4e031-180">.</span></span>
   
    ![avviso di riavvio](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="4e031-182">Si riceverà una notifica che il riavvio hello è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="4e031-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![riavvio iniziato](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="4e031-184">Durante il riavvio di hello è in corso, si perderà hello connessione toohello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4e031-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="4e031-185">È possibile monitorare il riavvio di hello aggiornando periodicamente hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="4e031-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="4e031-186">In alternativa, è possibile monitorare lo stato di riavvio del dispositivo hello tramite hello Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="4e031-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e031-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4e031-187">Next steps</span></span>
<span data-ttu-id="4e031-188">Informazioni su come troppo[utilizzare hello toomanage servizio StorSimple Manager dispositivo](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="4e031-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

