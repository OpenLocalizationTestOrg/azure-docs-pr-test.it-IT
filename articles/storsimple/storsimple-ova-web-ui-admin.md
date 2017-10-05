---
title: Amministrazione dell'interfaccia utente Web dell'array virtuale StorSimple | Microsoft Docs
description: "Viene illustrato come eseguire attività di amministrazione di base del dispositivo tramite l'interfaccia utente Web dell'array virtuale StorSimple."
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
ms.openlocfilehash: 989e7b697f9b527df549fb32be18edd1d3c8d224
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-web-ui-to-administer-your-storsimple-virtual-array"></a><span data-ttu-id="397aa-103">Usare l'interfaccia utente Web per amministrare StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="397aa-103">Use the Web UI to administer your StorSimple Virtual Array</span></span>
![flusso del processo di installazione](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="397aa-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="397aa-105">Overview</span></span>
<span data-ttu-id="397aa-106">Le esercitazioni in questo articolo si applicano a Microsoft Azure StorSimple Virtual Array (noto anche come dispositivo virtuale locale StorSimple) che esegue la versione di disponibilità generale (GA) di marzo 2016.</span><span class="sxs-lookup"><span data-stu-id="397aa-106">The tutorials in this article apply to the Microsoft Azure StorSimple Virtual Array (also known as the StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="397aa-107">Questo articolo illustra una parte dei flussi di lavoro e delle attività di gestione complessi eseguibili sull'array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="397aa-107">This article describes some of the complex workflows and management tasks that can be performed on the StorSimple Virtual Array.</span></span> <span data-ttu-id="397aa-108">È possibile gestire StorSimple Virtual Array usando l'interfaccia utente del servizio StorSimple Manager (interfaccia utente del portale) e l'interfaccia utente Web locale per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="397aa-108">You can manage the StorSimple Virtual Array using the StorSimple Manager service UI (referred to as the portal UI) and the local web UI for the device.</span></span> <span data-ttu-id="397aa-109">Questo articolo è incentrato sulle attività che è possibile eseguire con l'interfaccia utente Web.</span><span class="sxs-lookup"><span data-stu-id="397aa-109">This article focuses on the tasks that you can perform using the web UI.</span></span>

<span data-ttu-id="397aa-110">L'articolo include le esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="397aa-110">This article includes the following tutorials:</span></span>

* <span data-ttu-id="397aa-111">Ottenere la chiave DEK del servizio</span><span class="sxs-lookup"><span data-stu-id="397aa-111">Get the service data encryption key</span></span>
* <span data-ttu-id="397aa-112">Risolvere i problemi relativi agli errori di installazione dell'interfaccia utente Web</span><span class="sxs-lookup"><span data-stu-id="397aa-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="397aa-113">Generare un pacchetto di log</span><span class="sxs-lookup"><span data-stu-id="397aa-113">Generate a log package</span></span>
* <span data-ttu-id="397aa-114">Arrestare o riavviare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="397aa-114">Shut down or restart your device</span></span>

## <a name="get-the-service-data-encryption-key"></a><span data-ttu-id="397aa-115">Ottenere la chiave DEK del servizio</span><span class="sxs-lookup"><span data-stu-id="397aa-115">Get the service data encryption key</span></span>
<span data-ttu-id="397aa-116">Una chiave DEK del servizio viene generata quando si registra il primo dispositivo con il servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="397aa-116">A service data encryption key is generated when you register your first device with the StorSimple Manager service.</span></span> <span data-ttu-id="397aa-117">Questa chiave viene richiesta con la chiave di registrazione del servizio per registrare altri dispositivi con il servizio StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="397aa-117">This key is then required with the service registration key to register additional devices with the StorSimple Manager service.</span></span>

<span data-ttu-id="397aa-118">Se la chiave DEK del servizio è stata smarrita ed è necessario recuperarla, eseguire i passaggi seguenti nell'interfaccia utente Web locale del dispositivo registrato con il servizio.</span><span class="sxs-lookup"><span data-stu-id="397aa-118">If you have misplaced your service data encryption key and need to retrieve it, perform the following steps in the local web UI of the device registered with your service.</span></span>

#### <a name="to-get-the-service-data-encryption-key"></a><span data-ttu-id="397aa-119">Per ottenere la chiave DEK del servizio</span><span class="sxs-lookup"><span data-stu-id="397aa-119">To get the service data encryption key</span></span>
1. <span data-ttu-id="397aa-120">Connettersi all'interfaccia utente Web locale.</span><span class="sxs-lookup"><span data-stu-id="397aa-120">Connect to the local web UI.</span></span> <span data-ttu-id="397aa-121">Passare a **Configurazione** > **Impostazioni cloud**.</span><span class="sxs-lookup"><span data-stu-id="397aa-121">Go to **Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="397aa-122">Nella parte inferiore della pagina fare clic su **Ottieni chiave DEK del servizio**.</span><span class="sxs-lookup"><span data-stu-id="397aa-122">At the bottom of the page, click **Get service data encryption key**.</span></span> <span data-ttu-id="397aa-123">Viene visualizzata una chiave.</span><span class="sxs-lookup"><span data-stu-id="397aa-123">A key will appear.</span></span> <span data-ttu-id="397aa-124">Copiare e salvare questa chiave.</span><span class="sxs-lookup"><span data-stu-id="397aa-124">Copy and save this key.</span></span>
   
    ![ottenere la chiave DEK del servizio 1](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="397aa-126">Risolvere i problemi relativi agli errori di installazione dell'interfaccia utente Web</span><span class="sxs-lookup"><span data-stu-id="397aa-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="397aa-127">In alcuni casi, quando si configura il dispositivo tramite l'interfaccia utente Web locale, è possibile riscontrare alcuni errori.</span><span class="sxs-lookup"><span data-stu-id="397aa-127">In some instances when you configure the device through the local web UI, you might run into errors.</span></span> <span data-ttu-id="397aa-128">Per diagnosticare e risolvere questi errori, è possibile eseguire i test di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="397aa-128">To diagnose and troubleshoot such errors, you can run the diagnostics tests.</span></span>

#### <a name="to-run-the-diagnostic-tests"></a><span data-ttu-id="397aa-129">Per eseguire i test di diagnostica</span><span class="sxs-lookup"><span data-stu-id="397aa-129">To run the diagnostic tests</span></span>
1. <span data-ttu-id="397aa-130">Nell'interfaccia utente Web locale passare a **Risoluzione dei problemi** > **Test diagnostici**.</span><span class="sxs-lookup"><span data-stu-id="397aa-130">In the local web UI, go to **Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![eseguire diagnostica 1](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="397aa-132">Nella parte inferiore della pagina fare clic su **Esegui test diagnostici**.</span><span class="sxs-lookup"><span data-stu-id="397aa-132">At the bottom of the page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="397aa-133">Si avviano così i test per diagnosticare eventuali problemi con la rete, il dispositivo, il proxy Web, l'ora o le impostazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="397aa-133">This will initiate tests to diagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="397aa-134">Si riceve una notifica in cui si comunica che il dispositivo sta eseguendo dei test.</span><span class="sxs-lookup"><span data-stu-id="397aa-134">You will be notified that the device is running tests.</span></span>
3. <span data-ttu-id="397aa-135">Al termine dei test, vengono visualizzati i risultati.</span><span class="sxs-lookup"><span data-stu-id="397aa-135">After the tests have completed, the results will be displayed.</span></span> <span data-ttu-id="397aa-136">L'esempio seguente mostra i risultati dei test di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="397aa-136">The following example shows the results of diagnostic tests.</span></span> <span data-ttu-id="397aa-137">Notare che le impostazioni del proxy Web non sono state configurate in questo dispositivo, quindi il test del proxy Web non è stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="397aa-137">Note that the web proxy settings were not configured on this device, and therefore, the web proxy test was not run.</span></span> <span data-ttu-id="397aa-138">Tutti gli altri test per le impostazioni di rete, il server DNS e le impostazioni ora sono stati completati correttamente.</span><span class="sxs-lookup"><span data-stu-id="397aa-138">All the other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![eseguire diagnostica 2](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="397aa-140">Generare un pacchetto di log</span><span class="sxs-lookup"><span data-stu-id="397aa-140">Generate a log package</span></span>
<span data-ttu-id="397aa-141">Un pacchetto di log è costituito da tutti i log rilevanti utili al supporto tecnico Microsoft nella risoluzione dei problemi del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="397aa-141">A log package is comprised of all the relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="397aa-142">In questa versione, un pacchetto di log può essere generato tramite l'interfaccia utente Web locale.</span><span class="sxs-lookup"><span data-stu-id="397aa-142">In this release, a log package can be generated via the local web UI.</span></span>

#### <a name="to-generate-the-log-package"></a><span data-ttu-id="397aa-143">Per generare il pacchetto di log</span><span class="sxs-lookup"><span data-stu-id="397aa-143">To generate the log package</span></span>
1. <span data-ttu-id="397aa-144">Nell'interfaccia utente Web locale passare a **Risoluzione dei problemi** > **Log di sistema**.</span><span class="sxs-lookup"><span data-stu-id="397aa-144">In the local web UI, go to **Troubleshooting** > **System logs**.</span></span>
   
    ![generare pacchetto di log 1](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="397aa-146">Nella parte inferiore della pagina fare clic su **Crea pacchetto di log**.</span><span class="sxs-lookup"><span data-stu-id="397aa-146">At the bottom of the page, click **Create log package**.</span></span> <span data-ttu-id="397aa-147">Viene creato un pacchetto di log del sistema.</span><span class="sxs-lookup"><span data-stu-id="397aa-147">A package of the system logs will be created.</span></span> <span data-ttu-id="397aa-148">L'operazione richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="397aa-148">This will take a couple of minutes.</span></span>
   
    ![generare pacchetto di log 2](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="397aa-150">Se il pacchetto è stato creato correttamente, si riceve una notifica e la pagina viene aggiornata per indicare l'ora e la data di creazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="397aa-150">You will be notified after the package is successfully created, and the page will be updated to indicate the time and date when the package was created.</span></span>
   
    ![generare pacchetto di log 3](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="397aa-152">Fare clic su **Scarica pacchetto di log**.</span><span class="sxs-lookup"><span data-stu-id="397aa-152">Click **Download log package**.</span></span> <span data-ttu-id="397aa-153">Un pacchetto compresso viene scaricato nel sistema.</span><span class="sxs-lookup"><span data-stu-id="397aa-153">A zipped package will be downloaded on your system.</span></span>
   
    ![generare pacchetto di log 4](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="397aa-155">È possibile decomprimere il pacchetto di log scaricato e visualizzare i file di log del sistema.</span><span class="sxs-lookup"><span data-stu-id="397aa-155">You can unzip the downloaded log package and view the system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="397aa-156">Arrestare e riavviare il dispositivo</span><span class="sxs-lookup"><span data-stu-id="397aa-156">Shut down and restart your device</span></span>
<span data-ttu-id="397aa-157">È possibile arrestare o riavviare il dispositivo virtuale tramite l'interfaccia utente Web locale.</span><span class="sxs-lookup"><span data-stu-id="397aa-157">You can shut down or restart your virtual device using the local web UI.</span></span> <span data-ttu-id="397aa-158">Prima di riavviare, si consiglia di portare offline i volumi o le condivisioni sull'host e quindi sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="397aa-158">We recommend that before you restart, take the volumes or shares offline on the host and then the device.</span></span> <span data-ttu-id="397aa-159">Questa operazione consente di eliminare qualsiasi  rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="397aa-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="to-shut-down-your-virtual-device"></a><span data-ttu-id="397aa-160">Per arrestare il dispositivo virtuale</span><span class="sxs-lookup"><span data-stu-id="397aa-160">To shut down your virtual device</span></span>
1. <span data-ttu-id="397aa-161">Nell'interfaccia utente Web locale passare a **Manutenzione** > **Impostazioni di risparmio energia**.</span><span class="sxs-lookup"><span data-stu-id="397aa-161">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="397aa-162">Nella parte inferiore della pagina fare clic su **Arresto**.</span><span class="sxs-lookup"><span data-stu-id="397aa-162">At the bottom of the page, click **Shutdown**.</span></span>
   
    ![arresto del dispositivo 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="397aa-164">Verrà visualizzato un avviso per segnalare che l'arresto del dispositivo interromperà ogni IO in corso, causando un periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="397aa-164">A warning will appear stating that a shutdown of the device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="397aa-165">Fare clic sull’icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="397aa-165">Click the check icon</span></span> ![icona del segno di spunta](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="397aa-167">.</span><span class="sxs-lookup"><span data-stu-id="397aa-167">.</span></span>
   
    ![avviso di arresto del dispositivo](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="397aa-169">Si riceve una notifica in cui si comunica che l'arresto è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="397aa-169">You will be notified that the shutdown has been initiated.</span></span>
   
    ![arresto del dispositivo avviato](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="397aa-171">Il dispositivo viene ora arrestato.</span><span class="sxs-lookup"><span data-stu-id="397aa-171">The device will now shut down.</span></span> <span data-ttu-id="397aa-172">Se si desidera avviare il dispositivo, è necessario farlo tramite la console di gestione Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="397aa-172">If you want to start your device, you will need to do that through the Hyper-V Manager.</span></span>

#### <a name="to-restart-your-virtual-device"></a><span data-ttu-id="397aa-173">Per riavviare il dispositivo virtuale</span><span class="sxs-lookup"><span data-stu-id="397aa-173">To restart your virtual device</span></span>
1. <span data-ttu-id="397aa-174">Nell'interfaccia utente Web locale passare a **Manutenzione** > **Impostazioni di risparmio energia**.</span><span class="sxs-lookup"><span data-stu-id="397aa-174">In the local web UI, go to **Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="397aa-175">Nella parte inferiore della pagina fare clic su **Riavvia**.</span><span class="sxs-lookup"><span data-stu-id="397aa-175">At the bottom of the page, click **Restart**.</span></span>
   
    ![riavvio del dispositivo](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="397aa-177">Viene visualizzato un avviso in cui si informa che il riavvio del dispositivo interromperà ogni IO in corso, causando un tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="397aa-177">A warning will appear stating that restarting the device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="397aa-178">Fare clic sull’icona del segno di spunta </span><span class="sxs-lookup"><span data-stu-id="397aa-178">Click the check icon</span></span> ![icona del segno di spunta](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="397aa-180">.</span><span class="sxs-lookup"><span data-stu-id="397aa-180">.</span></span>
   
    ![avviso di riavvio](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="397aa-182">Si riceve una notifica in cui si comunica che il riavvio è iniziato.</span><span class="sxs-lookup"><span data-stu-id="397aa-182">You will be notified that the restart has been initiated.</span></span>
   
    ![riavvio iniziato](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="397aa-184">Durante il riavvio, si perde la connessione all'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="397aa-184">While the restart is in progress, you will lose the connection to the UI.</span></span> <span data-ttu-id="397aa-185">È possibile monitorare il riavvio aggiornando periodicamente l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="397aa-185">You can monitor the restart by refreshing the UI periodically.</span></span> <span data-ttu-id="397aa-186">In alternativa, è possibile monitorare lo stato di riavvio del dispositivo tramite la console di gestione Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="397aa-186">Alternatively, you can monitor the device restart status through the Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="397aa-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="397aa-187">Next steps</span></span>
<span data-ttu-id="397aa-188">Informazioni su come [Utilizzare il servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="397aa-188">Learn how to [use the StorSimple Manager service to manage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

