---
title: Aggiornamento 0,5 in StorSimple Virtual Array aaaInstall | Documenti Microsoft
description: Viene descritto come toouse hello Array virtuale StorSimple web aggiornamenti dell'interfaccia utente tooapply utilizzando hello Azure portale e l'aggiornamento rapido (metodo)
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
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="50c8c-103">Installare l'aggiornamento 0.5 nell'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="50c8c-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="50c8c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="50c8c-104">Overview</span></span>

<span data-ttu-id="50c8c-105">Questo articolo descrive hello passaggi necessari tooinstall aggiornamento 0,5 nell'Array virtuale StorSimple tramite l'interfaccia utente web locale hello e tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50c8c-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="50c8c-106">È necessario tooapply software aggiornamenti o hotfix tookeep l'Array virtuale StorSimple aggiornato.</span><span class="sxs-lookup"><span data-stu-id="50c8c-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="50c8c-107">Prima di applicare un aggiornamento, è consigliabile eseguire volumi hello o condivisioni offline in hello innanzitutto l'host e quindi hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50c8c-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="50c8c-108">Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="50c8c-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="50c8c-109">Dopo aver hello volumi o condivisioni sono offline, è inoltre necessario eseguire il manuale di un backup del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="50c8c-110">Aggiornamento 0,5 corrisponde troppo**10.0.10290.0** versione del software nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50c8c-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="50c8c-111">Per informazioni sulle novità in questo aggiornamento, visitare troppo[note sulla versione di aggiornamento 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="50c8c-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="50c8c-112">Se si esegue l'aggiornamento 0,2 o versioni successive, è consigliabile installare aggiornamenti hello tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50c8c-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="50c8c-113">Se si esegue l'aggiornamento 0,1 o versioni del software GA, è necessario utilizzare il metodo di aggiornamento rapido hello tramite tooinstall di interfaccia utente web locale hello aggiornamento 0,5.</span><span class="sxs-lookup"><span data-stu-id="50c8c-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="50c8c-114">Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50c8c-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="50c8c-115">Dato che hello Array virtuale StorSimple è un dispositivo singolo nodo, viene interrotta qualsiasi i/o in corso e il dispositivo si verifica nel tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="50c8c-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="50c8c-116">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="50c8c-116">Use hello Azure portal</span></span>

<span data-ttu-id="50c8c-117">Se l'esecuzione di Update 0,2 e versioni successive, è consigliabile installare gli aggiornamenti tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50c8c-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="50c8c-118">procedure portale Hello richiede hello utente tooscan, scaricare e installare gli aggiornamenti di hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="50c8c-119">Questa procedura accetta toocomplete circa 7 minuti.</span><span class="sxs-lookup"><span data-stu-id="50c8c-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="50c8c-120">Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.</span><span class="sxs-lookup"><span data-stu-id="50c8c-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="50c8c-121">Dopo aver hello installazione è completata, passare tooyour servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="50c8c-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="50c8c-122">Selezionare **dispositivi** selezionare e fare clic su dispositivo hello hai appena aggiornato.</span><span class="sxs-lookup"><span data-stu-id="50c8c-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="50c8c-123">Andare troppo**Impostazioni > Gestisci > gli aggiornamenti del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="50c8c-124">la versione software Hello visualizzato deve essere **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="50c8c-125">Utilizzare l'interfaccia utente web locale hello</span><span class="sxs-lookup"><span data-stu-id="50c8c-125">Use hello local web UI</span></span>

<span data-ttu-id="50c8c-126">Quando si utilizza l'interfaccia utente web locale hello, sono disponibili due passaggi:</span><span class="sxs-lookup"><span data-stu-id="50c8c-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="50c8c-127">Scaricare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="50c8c-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="50c8c-128">Installare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="50c8c-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="50c8c-129">Scaricare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="50c8c-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="50c8c-130">Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="50c8c-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="50c8c-131">hotfix di aggiornamento o hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="50c8c-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="50c8c-132">Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="50c8c-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="50c8c-133">Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="50c8c-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="50c8c-134">Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload.</span><span class="sxs-lookup"><span data-stu-id="50c8c-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="50c8c-135">Immettere **4021576** per l'aggiornamento 0.5 e quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="50c8c-136">Hello hotfix elenco viene visualizzato, ad esempio, **StorSimple Virtual Array aggiornamento 0,5**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="50c8c-138">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-138">Click **Download**.</span></span> 

5. <span data-ttu-id="50c8c-139">Due toodownload di file, verrà visualizzato un *msu* e *CAB* file.</span><span class="sxs-lookup"><span data-stu-id="50c8c-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="50c8c-140">Scaricare ciascun tali tooa cartella dei file.</span><span class="sxs-lookup"><span data-stu-id="50c8c-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="50c8c-141">cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="50c8c-142">Aprire la cartella hello in cui si trovano i file hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="50c8c-143">![File di pacchetto hello](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="50c8c-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="50c8c-144">Verranno visualizzati:</span><span class="sxs-lookup"><span data-stu-id="50c8c-144">You see:</span></span>
    -  <span data-ttu-id="50c8c-145">Un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="50c8c-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="50c8c-146">Questo file è un software di dispositivo hello tooupdate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="50c8c-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="50c8c-147">Un file di pacchetto dell'agente di monitoraggio Geneva `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="50c8c-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="50c8c-148">Questo file è utilizzato tooupdate hello monitoraggio e diagnostica (MDS) agente del servizio.</span><span class="sxs-lookup"><span data-stu-id="50c8c-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="50c8c-149">Fare doppio clic sul file cab hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-149">Double-click hello cab file.</span></span> <span data-ttu-id="50c8c-150">Verrà visualizzato un file con estensione msi.</span><span class="sxs-lookup"><span data-stu-id="50c8c-150">A .msi is displayed.</span></span> <span data-ttu-id="50c8c-151">File hello selezionare pulsante destro del mouse, quindi **estrarre** file hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="50c8c-152">Si utilizzerà hello _con estensione msi_ agente hello tooupdate.</span><span class="sxs-lookup"><span data-stu-id="50c8c-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Estrarre il file di aggiornamento dell'agente del servizio di monitoraggio e diagnostica (MDS)](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="50c8c-154">Installare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="50c8c-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="50c8c-155">Installazione di un hotfix o aggiornamento precedente toohello, assicurarsi che si dispone di hello aggiornamento o hotfix hello scaricato localmente nell'host o accessibile tramite una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="50c8c-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="50c8c-156">Utilizzare questo metodo tooinstall Aggiorna su un dispositivo che esegue GA o aggiornare le versioni di software 0,1.</span><span class="sxs-lookup"><span data-stu-id="50c8c-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="50c8c-157">Questa procedura richiede minore toocomplete 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="50c8c-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="50c8c-158">Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.</span><span class="sxs-lookup"><span data-stu-id="50c8c-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="50c8c-159">hotfix di aggiornamento o hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="50c8c-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="50c8c-160">In hello interfaccia utente web locale, andare troppo**manutenzione** > **aggiornamento Software**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="50c8c-162">In **percorso del file di aggiornamento**, immettere il nome di file hello per l'aggiornamento di hello o hello hotfix.</span><span class="sxs-lookup"><span data-stu-id="50c8c-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="50c8c-163">È inoltre possibile esplorare i file di installazione di un hotfix o aggiornamento toohello se inserito in una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="50c8c-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="50c8c-164">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-164">Click **Apply**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="50c8c-166">Verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="50c8c-166">A warning is displayed.</span></span> <span data-ttu-id="50c8c-167">Dato questo è un dispositivo singolo nodo, dopo che viene applicato l'aggiornamento di hello, hello dispositivo si riavvia e vi sia tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="50c8c-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="50c8c-168">Fare clic sull'icona di controllo di hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-168">Click hello check icon.</span></span>
   
   ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="50c8c-170">avvio dell'aggiornamento Hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-170">hello update starts.</span></span> <span data-ttu-id="50c8c-171">Dopo aver completato l'aggiornamento dispositivo hello, viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="50c8c-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="50c8c-172">Hello dell'interfaccia utente locale non è accessibile in tale intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="50c8c-172">hello local UI is not accessible in this duration.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="50c8c-174">Dopo aver completato il riavvio di hello, che viene visualizzata toohello **Accedi** pagina.</span><span class="sxs-lookup"><span data-stu-id="50c8c-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="50c8c-175">tooverify dispone di aggiornamento software per dispositivi hello nel web locale hello dell'interfaccia utente, andare troppo**manutenzione** > **aggiornamento Software**.</span><span class="sxs-lookup"><span data-stu-id="50c8c-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="50c8c-176">la versione software Hello visualizzato deve essere **10.0.0.0.0.10290.0** per l'aggiornamento di 0,5.</span><span class="sxs-lookup"><span data-stu-id="50c8c-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="50c8c-177">I report versioni del software hello in modo leggermente diverso nell'interfaccia utente web locale hello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="50c8c-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="50c8c-178">Ad esempio, hello report dell'interfaccia utente web locale **10.0.0.0.0.10290** e i report del portale Azure hello **10.0.10290.0** per hello stessa versione.</span><span class="sxs-lookup"><span data-stu-id="50c8c-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="50c8c-180">passaggio successivo Hello è l'agente tooupdate hello MDS.</span><span class="sxs-lookup"><span data-stu-id="50c8c-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="50c8c-181">In hello **aggiornamento Software** pagina, visitare toohello **percorso del file di aggiornamento** ed esplorare toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span><span class="sxs-lookup"><span data-stu-id="50c8c-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="50c8c-182">Ripetere i passaggi da 2 a 4.</span><span class="sxs-lookup"><span data-stu-id="50c8c-182">Repeat steps 2-4.</span></span> <span data-ttu-id="50c8c-183">Dopo il riavvio di array virtuale hello, effettuano l'interfaccia utente web locale hello.</span><span class="sxs-lookup"><span data-stu-id="50c8c-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="50c8c-184">aggiornamento di Hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="50c8c-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50c8c-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50c8c-185">Next steps</span></span>

<span data-ttu-id="50c8c-186">Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="50c8c-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

