---
title: Installare aggiornamenti su un array virtuale Microsoft Azure StorSimple | Documentazione Microsoft
description: Viene illustrato come usare l'interfaccia utente Web dell'array virtuale StorSimple per applicare aggiornamenti tramite il portale e gli hotfix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c2d081604c0ca01f47c3ff2aab7477859d280963
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="a8bce-103">Installare aggiornamenti nell'array virtuale StorSimple - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a8bce-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="a8bce-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a8bce-104">Overview</span></span>

<span data-ttu-id="a8bce-105">Questo articolo descrive i passaggi necessari per installare aggiornamenti sull'array virtuale StorSimple mediante l'interfaccia utente Web locale e il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8bce-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="a8bce-106">È necessario applicare aggiornamenti software o hotfix per mantenere StorSimple Virtual Array sempre aggiornato.</span><span class="sxs-lookup"><span data-stu-id="a8bce-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="a8bce-107">Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8bce-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="a8bce-108">Dato che l'array virtuale StorSimple è un dispositivo a nodo singolo, gli eventuali I/O in corso vengono interrotti e il dispositivo registra un periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="a8bce-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="a8bce-109">Prima di applicare un aggiornamento, si consiglia di portare offline i volumi o le condivisioni, prima nell'host e poi nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8bce-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="a8bce-110">Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="a8bce-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8bce-111">Se si esegue l'aggiornamento 0.1 o una versione del software GA, è necessario usare il metodo hotfix tramite l'interfaccia utente Web locale per installare l'aggiornamento 0.3.</span><span class="sxs-lookup"><span data-stu-id="a8bce-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="a8bce-112">Se si esegue l'aggiornamento 0.2, si consiglia di installare gli aggiornamenti tramite il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="a8bce-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="a8bce-113">Usare l'interfaccia utente Web locale</span><span class="sxs-lookup"><span data-stu-id="a8bce-113">Use the local web UI</span></span>

<span data-ttu-id="a8bce-114">Quando si usa l'interfaccia utente Web locale, è necessario eseguire due passaggi:</span><span class="sxs-lookup"><span data-stu-id="a8bce-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="a8bce-115">Scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="a8bce-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="a8bce-116">Installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="a8bce-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="a8bce-117">Scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="a8bce-117">Download the update or the hotfix</span></span>

<span data-ttu-id="a8bce-118">Eseguire i passaggi seguenti per scaricare l'aggiornamento del software da Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="a8bce-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="a8bce-119">Per scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="a8bce-119">To download the update or the hotfix</span></span>

1. <span data-ttu-id="a8bce-120">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a8bce-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="a8bce-121">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="a8bce-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="a8bce-122">Nella casella di ricerca di Microsoft Update Catalog, immettere il numero dell'hotfix da scaricare riportato nella Knowledge Base (KB).</span><span class="sxs-lookup"><span data-stu-id="a8bce-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="a8bce-123">Digitare **3182061** per l'aggiornamento 0.3, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="a8bce-124">Viene visualizzato l'elenco degli hotfix, tra cui l' **aggiornamento 0.3 per l'array virtuale StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="a8bce-126">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-126">Click **Add**.</span></span> <span data-ttu-id="a8bce-127">L'aggiornamento viene aggiunto al carrello.</span><span class="sxs-lookup"><span data-stu-id="a8bce-127">The update is added to the basket.</span></span>

5. <span data-ttu-id="a8bce-128">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="a8bce-129">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-129">Click **Download**.</span></span> <span data-ttu-id="a8bce-130">Specificare o **selezionare** il percorso locale in cui salvare i file scaricati.</span><span class="sxs-lookup"><span data-stu-id="a8bce-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="a8bce-131">Gli aggiornamenti vengono scaricati nel percorso specificato e inseriti in una sottocartella con lo stesso nome dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a8bce-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="a8bce-132">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8bce-132">The folder can also be copied to a network share that is reachable from the device.</span></span>

7. <span data-ttu-id="a8bce-133">Aprire la cartella copiata e si dovrebbe vedere un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="a8bce-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="a8bce-134">Si usa questo file per installare l'hotfix o aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="a8bce-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="a8bce-135">Installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="a8bce-135">Install the update or the hotfix</span></span>

<span data-ttu-id="a8bce-136">Prima dell'installazione di un aggiornamento o un hotfix, assicurarsi di avere scaricato l'aggiornamento o l'hotfix in locale o sull'host, altrimenti che siano accessibili tramite una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="a8bce-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="a8bce-137">Usare questo metodo per installare gli aggiornamenti in un dispositivo che esegue GA o versioni del software con l'aggiornamento 0.1.</span><span class="sxs-lookup"><span data-stu-id="a8bce-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="a8bce-138">Questa procedura di aggiornamento richiede un massimo di 2 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="a8bce-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="a8bce-139">Seguire questa procedura per installare l'aggiornamento o l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="a8bce-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="a8bce-140">Per installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="a8bce-140">To install the update or the hotfix</span></span>

1. <span data-ttu-id="a8bce-141">Nell'interfaccia utente Web locale, accedere a **Manutenzione** > **Aggiornamento software**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="a8bce-143">In **Percorso del file di aggiornamento**, immettere il nome del file dell'aggiornamento o dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="a8bce-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="a8bce-144">È possibile anche cercare il file di installazione dell'aggiornamento o dell'hotfix, se posizionato in una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="a8bce-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="a8bce-145">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-145">Click **Apply**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="a8bce-147">Verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="a8bce-147">A warning is displayed.</span></span> <span data-ttu-id="a8bce-148">Dato che si tratta di un dispositivo a nodo singolo, dopo l'applicazione dell'aggiornamento il dispositivo si riavvia con un conseguente periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="a8bce-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="a8bce-149">Fare clic sull'icona del segno di spunta</span><span class="sxs-lookup"><span data-stu-id="a8bce-149">Click the check icon.</span></span>
   
   ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="a8bce-151">L'aggiornamento si avvia.</span><span class="sxs-lookup"><span data-stu-id="a8bce-151">The update starts.</span></span> <span data-ttu-id="a8bce-152">Dopo l'aggiornamento il dispositivo si riavvia in automatico.</span><span class="sxs-lookup"><span data-stu-id="a8bce-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="a8bce-153">In questo periodo di tempo l'interfaccia utente locale non è accessibile.</span><span class="sxs-lookup"><span data-stu-id="a8bce-153">The local UI is not accessible in this duration.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="a8bce-155">Al termine del riavvio si viene indirizzati alla pagina **di accesso** .</span><span class="sxs-lookup"><span data-stu-id="a8bce-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="a8bce-156">Per verificare se il software del dispositivo è stato aggiornato, nell'interfaccia utente Web locale passare a **Manutenzione** > **Aggiornamento software**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="a8bce-157">Dovrebbe essere visualizzata la versione del software **10.0.0.0.0.10288.0** per l'aggiornamento 0.3.</span><span class="sxs-lookup"><span data-stu-id="a8bce-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a8bce-158">Le versioni del software vengono riportate in modo leggermente diverso nell'interfaccia utente Web locale e nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8bce-158">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="a8bce-159">Ad esempio, l'interfaccia utente Web locale riporta **10.0.0.0.0.10288**, mentre il portale di Azure riporta **10.0.10288.0** per la stessa versione.</span><span class="sxs-lookup"><span data-stu-id="a8bce-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure portal reports **10.0.10288.0** for the same version.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a><span data-ttu-id="a8bce-161">Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a8bce-161">Use the Azure portal</span></span>

<span data-ttu-id="a8bce-162">Se si esegue l'aggiornamento 0.2, si consiglia di installare gli aggiornamenti tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a8bce-162">If running Update 0.2, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="a8bce-163">La procedura del portale richiede all'utente di analizzare, scaricare e installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="a8bce-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="a8bce-164">Questa procedura di aggiornamento richiede circa 7 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="a8bce-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="a8bce-165">Seguire questa procedura per installare l'aggiornamento o l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="a8bce-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="a8bce-166">Al termine dell'installazione, quando lo stato del processo è 100%, passare al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a8bce-166">After the installation is complete (as indicated by job status at 100 %), go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="a8bce-167">Selezionare **Dispositivi** e quindi selezionare e fare clic sul dispositivo che si vuole aggiornare nell'elenco di dispositivi connessi al servizio.</span><span class="sxs-lookup"><span data-stu-id="a8bce-167">Select **Devices** and then select and click the device you want to update from the list of devices connected to this service.</span></span> <span data-ttu-id="a8bce-168">Nel pannello **Impostazioni** andare alla sezione **Gestisci** e selezionare **Aggiornamenti del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-168">In the **Settings** blade, go to **Manage** section and select **Device updates**.</span></span> <span data-ttu-id="a8bce-169">La versione del software visualizzata dovrebbe essere **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="a8bce-169">The displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a8bce-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8bce-170">Next steps</span></span>

<span data-ttu-id="a8bce-171">Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="a8bce-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

