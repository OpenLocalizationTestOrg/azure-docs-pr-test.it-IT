---
title: Installare l'aggiornamento 0.6 nell'array virtuale StorSimple | Microsoft Docs
description: Descrive come usare l'interfaccia utente Web dell'array virtuale StorSimple per applicare aggiornamenti tramite il portale di Azure e gli hotfix
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 111976cd684561f5bc63b92f09a20470fe3036d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a><span data-ttu-id="37776-103">Installare l'aggiornamento 0.6 nell'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="37776-103">Install Update 0.6 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="37776-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="37776-104">Overview</span></span>

<span data-ttu-id="37776-105">Questo articolo descrive i passaggi necessari per installare l'aggiornamento 0.6 nell'array virtuale StorSimple tramite l'interfaccia utente Web locale e il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37776-105">This article describes the steps required to install Update 0.6 on your StorSimple Virtual Array via the local web UI and via the Azure portal.</span></span> <span data-ttu-id="37776-106">È necessario applicare aggiornamenti software o aggiornamenti rapidi per mantenere l'array virtuale StorSimple sempre aggiornato.</span><span class="sxs-lookup"><span data-stu-id="37776-106">You apply the software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="37776-107">Prima di applicare un aggiornamento, si consiglia di portare offline i volumi o le condivisioni, prima nell'host e poi nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37776-107">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="37776-108">Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="37776-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="37776-109">Quando i volumi o le condivisioni sono offline, è consigliabile eseguire anche un backup manuale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37776-109">After the volumes or shares are offline, you should also take a manual backup of the device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="37776-110">L'aggiornamento 0.6 corrisponde alla versione del software **10.0.10293.0** nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37776-110">Update 0.6 corresponds to **10.0.10293.0** software version on your device.</span></span> <span data-ttu-id="37776-111">Per informazioni sulle novità in questo aggiornamento, vedere le [note sulla versione per l'aggiornamento 0.6](storsimple-virtual-array-update-06-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="37776-111">For information on what is new in this update, go to [Release notes for Update 0.6](storsimple-virtual-array-update-06-release-notes.md).</span></span>
>
> - <span data-ttu-id="37776-112">Se si esegue l'aggiornamento 0.2 o versione successiva, è consigliabile installare gli aggiornamenti tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37776-112">If you are running Update 0.2 or later, we recommend that you install the updates via the Azure portal.</span></span> <span data-ttu-id="37776-113">Se si esegue l'aggiornamento 0.1 o una versione del software disponibile a livello generale, è necessario usare il metodo hotfix tramite l'interfaccia utente Web locale per installare l'aggiornamento 0.6.</span><span class="sxs-lookup"><span data-stu-id="37776-113">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install Update 0.6.</span></span>
>
> - <span data-ttu-id="37776-114">Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37776-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="37776-115">Dato che l'array virtuale StorSimple è un dispositivo a nodo singolo, gli eventuali I/O in corso vengono interrotti e il dispositivo registra un periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="37776-115">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="37776-116">Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="37776-116">Use the Azure portal</span></span>

<span data-ttu-id="37776-117">Se si esegue l'aggiornamento 0.2 o versione successiva, è consigliabile installare gli aggiornamenti tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37776-117">If running Update 0.2 and later, we recommend that you install updates through the Azure portal.</span></span> <span data-ttu-id="37776-118">La procedura del portale richiede all'utente di analizzare, scaricare e installare gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="37776-118">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="37776-119">Questa procedura di aggiornamento richiede circa 7 minuti per il completamento.</span><span class="sxs-lookup"><span data-stu-id="37776-119">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="37776-120">Seguire questa procedura per installare l'aggiornamento o l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="37776-120">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="37776-121">Al termine dell'installazione, passare al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="37776-121">After the installation is complete, go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="37776-122">Selezionare **Dispositivi** e quindi selezionare e fare clic sul dispositivo appena aggiornato.</span><span class="sxs-lookup"><span data-stu-id="37776-122">Select **Devices** and then select and click the device you just updated.</span></span> <span data-ttu-id="37776-123">Passare a **Impostazioni > Gestisci > Device Updates** (Aggiornamenti dispositivi).</span><span class="sxs-lookup"><span data-stu-id="37776-123">Go to **Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="37776-124">La versione del software visualizzata dovrebbe essere **10.0.10293.0**.</span><span class="sxs-lookup"><span data-stu-id="37776-124">The displayed software version should be **10.0.10293.0**.</span></span>

## <a name="use-the-local-web-ui"></a><span data-ttu-id="37776-125">Usare l'interfaccia utente Web locale</span><span class="sxs-lookup"><span data-stu-id="37776-125">Use the local web UI</span></span>

<span data-ttu-id="37776-126">Quando si usa l'interfaccia utente Web locale, è necessario eseguire due passaggi:</span><span class="sxs-lookup"><span data-stu-id="37776-126">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="37776-127">Scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="37776-127">Download the update or the hotfix</span></span>
* <span data-ttu-id="37776-128">Installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="37776-128">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="37776-129">Scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="37776-129">Download the update or the hotfix</span></span>

<span data-ttu-id="37776-130">Eseguire i passaggi seguenti per scaricare l'aggiornamento del software da Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="37776-130">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="37776-131">Per scaricare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="37776-131">To download the update or the hotfix</span></span>

1. <span data-ttu-id="37776-132">Avviare Internet Explorer e accedere al sito [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="37776-132">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="37776-133">Se si usa Microsoft Update Catalog nel computer per la prima volta, fare clic su **Installa** quando viene richiesto di installare il componente aggiuntivo Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="37776-133">If you are using the Microsoft Update Catalog for the first time on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="37776-134">Nella casella di ricerca di Microsoft Update Catalog, immettere il numero dell'hotfix da scaricare riportato nella Knowledge Base (KB).</span><span class="sxs-lookup"><span data-stu-id="37776-134">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="37776-135">Immettere **4023268** per l'aggiornamento 0.6 e quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="37776-135">Enter **4023268** for Update 0.6, and then click **Search**.</span></span>
   
    <span data-ttu-id="37776-136">Verrà visualizzato l'elenco degli aggiornamenti rapidi, tra cui l'**aggiornamento 0.6 per l'array virtuale StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="37776-136">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.6**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-virtual-array-install-update-06/download1.png)

4. <span data-ttu-id="37776-138">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="37776-138">Click **Download**.</span></span>

5. <span data-ttu-id="37776-139">Vengono visualizzati cinque file da scaricare.</span><span class="sxs-lookup"><span data-stu-id="37776-139">You should see five files to download.</span></span> <span data-ttu-id="37776-140">Scaricare ognuno dei file in una cartella.</span><span class="sxs-lookup"><span data-stu-id="37776-140">Download each of those files to a folder.</span></span> <span data-ttu-id="37776-141">Inoltre, la cartella può essere copiata in una condivisione di rete raggiungibile dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37776-141">The folder can also be copied to a network share that is reachable from the device.</span></span>

6. <span data-ttu-id="37776-142">Aprire la cartella in cui si trovano i file.</span><span class="sxs-lookup"><span data-stu-id="37776-142">Open the folder where the files are located.</span></span>
    <span data-ttu-id="37776-143">![File nel pacchetto](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span><span class="sxs-lookup"><span data-stu-id="37776-143">![Files in the package](./media/storsimple-virtual-array-install-update-06/update06folder.png)</span></span>

    <span data-ttu-id="37776-144">Verranno visualizzati:</span><span class="sxs-lookup"><span data-stu-id="37776-144">You see:</span></span>
    -  <span data-ttu-id="37776-145">Un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="37776-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="37776-146">Questo file viene usato per aggiornare il software del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37776-146">This file is used to update the device software.</span></span>
    - <span data-ttu-id="37776-147">Un file di pacchetto dell'agente di monitoraggio Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="37776-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="37776-148">Questo file viene usato per aggiornare l'agente del servizio di monitoraggio e diagnostica (MDS).</span><span class="sxs-lookup"><span data-stu-id="37776-148">This file is used to update the Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="37776-149">Fare doppio clic sul file con estensione cab.</span><span class="sxs-lookup"><span data-stu-id="37776-149">Double-click the cab file.</span></span> <span data-ttu-id="37776-150">Viene visualizzato un file con estensione _MSI_.</span><span class="sxs-lookup"><span data-stu-id="37776-150">A _.msi_ is displayed.</span></span> <span data-ttu-id="37776-151">Selezionare il file, fare clic con il pulsante destro del mouse e quindi scegliere **Estrai**.</span><span class="sxs-lookup"><span data-stu-id="37776-151">Select the file, right-click, and then **Extract** the file.</span></span> <span data-ttu-id="37776-152">Usare il file con estensione _MSI_ per aggiornare l'agente.</span><span class="sxs-lookup"><span data-stu-id="37776-152">You use the _.msi_ file to update the agent.</span></span>

        ![Estrarre il file di aggiornamento dell'agente del servizio di monitoraggio e diagnostica (MDS)](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > <span data-ttu-id="37776-154">Non è necessario aggiornare l'agente MDS, se si esegue l'aggiornamento 0.5 di StorSimple Update (0.0.10293.0).</span><span class="sxs-lookup"><span data-stu-id="37776-154">You do not need to update the MDS agent if you are running StorSimple Update 0.5 (0.0.10293.0).</span></span>

    - <span data-ttu-id="37776-155">Tre file che contengono gli aggiornamenti critici della sicurezza di Windows, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64` e `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="37776-155">Three files that contain critical Windows security updates, `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span>


### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="37776-156">Installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="37776-156">Install the update or the hotfix</span></span>

<span data-ttu-id="37776-157">Prima dell'installazione di un aggiornamento o un hotfix, assicurarsi di avere scaricato l'aggiornamento o l'hotfix in locale o sull'host, altrimenti che siano accessibili tramite una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="37776-157">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="37776-158">Usare questo metodo per installare gli aggiornamenti in un dispositivo che esegue GA o versioni del software con l'aggiornamento 0.1.</span><span class="sxs-lookup"><span data-stu-id="37776-158">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="37776-159">Il completamento di questa procedura richiede circa 12 minuti.</span><span class="sxs-lookup"><span data-stu-id="37776-159">This procedure takes approximately 12 minutes to complete.</span></span> <span data-ttu-id="37776-160">Seguire questa procedura per installare l'aggiornamento o l'hotfix.</span><span class="sxs-lookup"><span data-stu-id="37776-160">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="37776-161">Per installare l'aggiornamento o l'hotfix</span><span class="sxs-lookup"><span data-stu-id="37776-161">To install the update or the hotfix</span></span>

1. <span data-ttu-id="37776-162">Nell'interfaccia utente Web locale, accedere a **Manutenzione** > **Aggiornamento software**.</span><span class="sxs-lookup"><span data-stu-id="37776-162">In the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="37776-163">Prendere nota della versione del software in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="37776-163">Make a note of the software version that you are running.</span></span> <span data-ttu-id="37776-164">Se si esegue la versione **10.0.10290.0**, non è necessario aggiornare l'agente MDS nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="37776-164">If you are running **10.0.10290.0**, you do not need to update the MDS agent in step 6.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="37776-166">In **Percorso del file di aggiornamento**, immettere il nome del file dell'aggiornamento o dell'hotfix.</span><span class="sxs-lookup"><span data-stu-id="37776-166">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="37776-167">È possibile anche cercare il file di installazione dell'aggiornamento o dell'hotfix, se posizionato in una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="37776-167">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="37776-168">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="37776-168">Click **Apply**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="37776-170">Verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="37776-170">A warning is displayed.</span></span> <span data-ttu-id="37776-171">Visto che l'array virtuale è un dispositivo a nodo singolo, dopo l'applicazione dell'aggiornamento il dispositivo si riavvia con un conseguente periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="37776-171">Given the virtual array is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="37776-172">Fare clic sull'icona del segno di spunta</span><span class="sxs-lookup"><span data-stu-id="37776-172">Click the check icon.</span></span>
   
   ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="37776-174">L'aggiornamento si avvia.</span><span class="sxs-lookup"><span data-stu-id="37776-174">The update starts.</span></span> <span data-ttu-id="37776-175">Dopo l'aggiornamento il dispositivo si riavvia in automatico.</span><span class="sxs-lookup"><span data-stu-id="37776-175">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="37776-176">In questo periodo di tempo l'interfaccia utente locale non è accessibile.</span><span class="sxs-lookup"><span data-stu-id="37776-176">The local UI is not accessible in this duration.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="37776-178">Al termine del riavvio si viene indirizzati alla pagina **di accesso** .</span><span class="sxs-lookup"><span data-stu-id="37776-178">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="37776-179">Per verificare se il software del dispositivo è stato aggiornato, nell'interfaccia utente Web locale passare a **Manutenzione** > **Aggiornamento software**.</span><span class="sxs-lookup"><span data-stu-id="37776-179">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="37776-180">Dovrebbe essere visualizzata la versione del software **10.0.0.0.0.10293** per l'aggiornamento 0.6.</span><span class="sxs-lookup"><span data-stu-id="37776-180">The displayed software version should be **10.0.0.0.0.10293** for Update 0.6.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="37776-181">Le versioni del software vengono riportate in modo leggermente diverso nell'interfaccia utente Web locale e nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37776-181">We report the software versions in a slightly different way in the local web UI and the Azure portal.</span></span> <span data-ttu-id="37776-182">Ad esempio, l'interfaccia utente Web locale indica **10.0.0.0.0.10293**, mentre il portale di Azure indica **10.0.10293.0** per la stessa versione.</span><span class="sxs-lookup"><span data-stu-id="37776-182">For example, the local web UI reports **10.0.0.0.0.10293** and the Azure portal reports **10.0.10293.0** for the same version.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. <span data-ttu-id="37776-184">Ignorare questo passaggio se si eseguiva l'aggiornamento 0.5 dell'array virtuale StorSimple (**10.0.10290.0**) prima di applicare questo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="37776-184">Skip this step if you were running StorSimple Virtual Array Update 0.5 (**10.0.10290.0**) before you applied this update.</span></span> <span data-ttu-id="37776-185">L'utente ha preso nota della versione del software nel passaggio 1 prima di avviare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="37776-185">You made a note of the software version in step 1 before you began to update.</span></span> <span data-ttu-id="37776-186">Se veniva eseguito l'aggiornamento 0.5, l'agente MDS è già aggiornato.</span><span class="sxs-lookup"><span data-stu-id="37776-186">If you were running Update 0.5, your MDS agent is already up-to-date .</span></span>

    <span data-ttu-id="37776-187">Se si esegue una versione del software precedente all'aggiornamento 0.5, il passaggio successivo per l'utente consiste nell'aggiornare l'agente MDS.</span><span class="sxs-lookup"><span data-stu-id="37776-187">If you are running a software version prior to Update 0.5, the next step for you is to update the MDS agent.</span></span> <span data-ttu-id="37776-188">Nella pagina **Software Update** (Aggiornamento software), passare a **Update file path** (Aggiorna percorso file) e cercare il file `GenevaMonitoringAgentPackageInstaller.msi`.</span><span class="sxs-lookup"><span data-stu-id="37776-188">In the **Software Update** page, go to the **Update file path** and browse to the `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="37776-189">Ripetere i passaggi da 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="37776-189">Repeat steps 2-4.</span></span> <span data-ttu-id="37776-190">Dopo il riavvio dell'array virtuale, accedere all'interfaccia utente Web locale.</span><span class="sxs-lookup"><span data-stu-id="37776-190">After the virtual array restarts, sign into the local web UI.</span></span>

7. <span data-ttu-id="37776-191">Ripetere i passaggi da 2 a 4 per installare le correzioni della sicurezza di Windows usando i file `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64` e `windows8.1-kb4019213-x64`.</span><span class="sxs-lookup"><span data-stu-id="37776-191">Repeat step 2-4 to install the Windows security fixes using files `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, and `windows8.1-kb4019213-x64`.</span></span> <span data-ttu-id="37776-192">L'array virtuale viene riavviato dopo ogni installazione ed è necessario accedere all'interfaccia utente Web locale.</span><span class="sxs-lookup"><span data-stu-id="37776-192">The virtual array restarts after each install and you need to sign into the local web UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37776-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37776-193">Next steps</span></span>

<span data-ttu-id="37776-194">Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="37776-194">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

