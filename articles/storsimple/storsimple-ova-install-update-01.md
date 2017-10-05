---
title: Installare aggiornamenti in un array virtuale StorSimple | Microsoft Docs
description: Viene illustrato come usare l'interfaccia utente Web dell'array virtuale StorSimple per applicare aggiornamenti tramite il portale e gli hotfix.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="10d30-103">Installare aggiornamenti nell'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="10d30-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="10d30-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="10d30-104">Overview</span></span>
<span data-ttu-id="10d30-105">Questo articolo descrive i passaggi necessari per installare aggiornamenti nell'array virtuale StorSimple mediante l'interfaccia utente Web locale e il portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="10d30-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="10d30-106">È necessario applicare aggiornamenti software o hotfix per mantenere StorSimple Virtual Array sempre aggiornato.</span><span class="sxs-lookup"><span data-stu-id="10d30-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="10d30-107">Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10d30-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="10d30-108">Dato che l'array virtuale StorSimple è un dispositivo a nodo singolo, gli eventuali I/O in corso vengono interrotti e il dispositivo registra un periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="10d30-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="10d30-109">Prima di applicare un aggiornamento, si consiglia di portare offline i volumi o le condivisioni, prima nell'host e poi nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10d30-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="10d30-110">Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="10d30-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10d30-111">Se si esegue l'aggiornamento 0.1 o una versione del software GA, è necessario usare il metodo hotfix tramite l'interfaccia utente Web locale per installare l'aggiornamento 0.3.</span><span class="sxs-lookup"><span data-stu-id="10d30-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="10d30-112">Se si esegue l'aggiornamento 0.2, si consiglia di installare gli aggiornamenti tramite il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="10d30-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="10d30-113">Usare l'interfaccia utente Web locale</span><span class="sxs-lookup"><span data-stu-id="10d30-113">Use the local web UI</span></span>
<span data-ttu-id="10d30-114">Quando si usa l'interfaccia utente Web locale, è necessario eseguire due passaggi:</span><span class="sxs-lookup"><span data-stu-id="10d30-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="10d30-115">Scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="10d30-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="10d30-116">Installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="10d30-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="10d30-117">Scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="10d30-117">Download the update or the hotfix</span></span>
<span data-ttu-id="10d30-118">Eseguire i passaggi seguenti per scaricare l'aggiornamento del software da Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="10d30-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="10d30-119">Per scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="10d30-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="10d30-120">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="10d30-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="10d30-121">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="10d30-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="10d30-122">Nella casella di ricerca di Microsoft Update Catalog, immettere il numero dell'hotfix da scaricare riportato nella Knowledge Base (KB).</span><span class="sxs-lookup"><span data-stu-id="10d30-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="10d30-123">Digitare **3182061** per l'aggiornamento 0.3, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="10d30-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="10d30-124">Viene visualizzato l'elenco degli hotfix, tra cui l' **aggiornamento 0.3 per l'array virtuale StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="10d30-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="10d30-126">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="10d30-126">Click **Add**.</span></span> <span data-ttu-id="10d30-127">L'aggiornamento viene aggiunto al carrello.</span><span class="sxs-lookup"><span data-stu-id="10d30-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="10d30-128">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="10d30-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="10d30-129">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="10d30-129">Click **Download**.</span></span> <span data-ttu-id="10d30-130">Specificare o **selezionare** il percorso locale in cui salvare i file scaricati.</span><span class="sxs-lookup"><span data-stu-id="10d30-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="10d30-131">Gli aggiornamenti vengono scaricati nel percorso specificato e inseriti in una sottocartella con lo stesso nome dell'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="10d30-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="10d30-132">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="10d30-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="10d30-133">Aprire la cartella copiata e si dovrebbe vedere un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="10d30-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="10d30-134">Si usa questo file per installare l'hotfix o aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="10d30-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="10d30-135">Installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="10d30-135">Install the update or the hotfix</span></span>
<span data-ttu-id="10d30-136">Prima dell'installazione di un aggiornamento o un hotfix, assicurarsi di avere scaricato l'aggiornamento o l'hotfix in locale o sull'host, altrimenti che siano accessibili tramite una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="10d30-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="10d30-137">Usare questo metodo per installare gli aggiornamenti in un dispositivo che esegue GA o versioni del software con l'aggiornamento 0.1.</span><span class="sxs-lookup"><span data-stu-id="10d30-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="10d30-138">Questa procedura di aggiornamento richiede un massimo di 2 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="10d30-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="10d30-139">Seguire questa procedura per installare l'aggiornamento o l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="10d30-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="10d30-140">Per installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="10d30-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="10d30-141">Nell'interfaccia utente Web locale, accedere a **Manutenzione** > **Aggiornamento software**.</span><span class="sxs-lookup"><span data-stu-id="10d30-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="10d30-143">In **Percorso del file di aggiornamento**, immettere il nome del file dell'aggiornamento o dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="10d30-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="10d30-144">È possibile anche cercare il file di installazione dell'aggiornamento o dell'hotfix, se posizionato in una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="10d30-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="10d30-145">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="10d30-145">Click **Apply**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="10d30-147">Verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="10d30-147">A warning is displayed.</span></span> <span data-ttu-id="10d30-148">Dato che si tratta di un dispositivo a nodo singolo, dopo l'applicazione dell'aggiornamento il dispositivo si riavvia con un conseguente periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="10d30-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="10d30-149">Fare clic sull'icona del segno di spunta</span><span class="sxs-lookup"><span data-stu-id="10d30-149">Click the check icon.</span></span>
   
   ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="10d30-151">L'aggiornamento si avvia.</span><span class="sxs-lookup"><span data-stu-id="10d30-151">The update starts.</span></span> <span data-ttu-id="10d30-152">Dopo l'aggiornamento il dispositivo si riavvia in automatico.</span><span class="sxs-lookup"><span data-stu-id="10d30-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="10d30-153">In questo periodo di tempo l'interfaccia utente locale non è accessibile.</span><span class="sxs-lookup"><span data-stu-id="10d30-153">The local UI is not accessible in this duration.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="10d30-155">Al termine del riavvio si viene indirizzati alla pagina **di accesso** .</span><span class="sxs-lookup"><span data-stu-id="10d30-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="10d30-156">Per verificare se il software del dispositivo è stato aggiornato, nell'interfaccia utente Web locale passare a **Manutenzione** > **Aggiornamento software**.</span><span class="sxs-lookup"><span data-stu-id="10d30-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="10d30-157">Dovrebbe essere visualizzata la versione del software **10.0.0.0.0.10288.0** per l'aggiornamento 0.3.</span><span class="sxs-lookup"><span data-stu-id="10d30-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="10d30-158">Le versioni del software vengono riportate in modo leggermente diverso nell'interfaccia utente Web locale e nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="10d30-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="10d30-159">Ad esempio, l'interfaccia utente Web locale riporta **10.0.0.0.0.10288**, mentre il portale di Azure classico riporta **10.0.10288.0** per la stessa versione.</span><span class="sxs-lookup"><span data-stu-id="10d30-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="10d30-161">Usare il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="10d30-161">Use the Azure classic portal</span></span>
<span data-ttu-id="10d30-162">Se si esegue l'aggiornamento 0.2, si consiglia di installare gli aggiornamenti tramite il portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="10d30-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="10d30-163">La procedura del portale richiede all'utente di analizzare, scaricare e installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="10d30-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="10d30-164">Questa procedura di aggiornamento richiede circa 7 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="10d30-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="10d30-165">Seguire questa procedura per installare l'aggiornamento o l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="10d30-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="10d30-166">Quando l'installazione è completa (lo stato del processo è 100%), passare a **Dispositivi > Manutenzione > Aggiornamenti software**.</span><span class="sxs-lookup"><span data-stu-id="10d30-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="10d30-167">La versione del software visualizzata dovrebbe essere 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="10d30-167">The displayed software version should be 10.0.10288.0.</span></span>

![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="10d30-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10d30-169">Next steps</span></span>
<span data-ttu-id="10d30-170">Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="10d30-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

