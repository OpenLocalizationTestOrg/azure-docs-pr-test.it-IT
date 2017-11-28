---
title: aaaInstall aggiornamenti in un Array virtuale StorSimple | Documenti Microsoft
description: Viene descritto come toouse hello Array virtuale StorSimple web UI tooapply Aggiorna metodo hello portale e l'aggiornamento rapido
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
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="8cf38-103">Installare aggiornamenti nell'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="8cf38-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="8cf38-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="8cf38-104">Overview</span></span>
<span data-ttu-id="8cf38-105">Questo articolo descrive hello passaggi tooinstall necessari aggiornamenti sull'Array virtuale StorSimple tramite l'interfaccia utente web locale hello e tramite hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="8cf38-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure classic portal.</span></span> <span data-ttu-id="8cf38-106">È necessario tooapply software aggiornamenti o hotfix tookeep l'Array virtuale StorSimple aggiornato.</span><span class="sxs-lookup"><span data-stu-id="8cf38-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="8cf38-107">Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8cf38-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="8cf38-108">Dato che hello Array virtuale StorSimple è un dispositivo singolo nodo, viene interrotta qualsiasi i/o in corso e il dispositivo si verifica nel tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="8cf38-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="8cf38-109">Prima di applicare un aggiornamento, è consigliabile eseguire volumi hello o condivisioni offline in hello innanzitutto l'host e quindi hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8cf38-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="8cf38-110">Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="8cf38-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cf38-111">Se si esegue l'aggiornamento 0,1 o versioni del software GA, è necessario utilizzare il metodo di aggiornamento rapido hello tramite l'aggiornamento di tooinstall dell'interfaccia utente web locale hello 0,3.</span><span class="sxs-lookup"><span data-stu-id="8cf38-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="8cf38-112">Se si esegue l'aggiornamento 0,2, è consigliabile installare gli aggiornamenti di hello tramite hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="8cf38-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
> 
> 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="8cf38-113">Utilizzare l'interfaccia utente web locale hello</span><span class="sxs-lookup"><span data-stu-id="8cf38-113">Use hello local web UI</span></span>
<span data-ttu-id="8cf38-114">Quando si utilizza l'interfaccia utente web locale hello, sono disponibili due passaggi:</span><span class="sxs-lookup"><span data-stu-id="8cf38-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="8cf38-115">Scaricare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="8cf38-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="8cf38-116">Installare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="8cf38-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cf38-117">Scaricare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="8cf38-117">Download hello update or hello hotfix</span></span>
<span data-ttu-id="8cf38-118">Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="8cf38-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cf38-119">hotfix di aggiornamento o hello hello toodownload</span><span class="sxs-lookup"><span data-stu-id="8cf38-119">toodownload hello update or hello hotfix</span></span>
1. <span data-ttu-id="8cf38-120">Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8cf38-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="8cf38-121">Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="8cf38-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="8cf38-122">Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload.</span><span class="sxs-lookup"><span data-stu-id="8cf38-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="8cf38-123">Digitare **3182061** per l'aggiornamento 0.3, quindi fare clic su **Cerca**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="8cf38-124">Hello hotfix elenco viene visualizzato, ad esempio, **StorSimple Virtual Array aggiornamento 0.3**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Cercare nel catalogo](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="8cf38-126">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-126">Click **Add**.</span></span> <span data-ttu-id="8cf38-127">aggiornamento di Hello viene aggiunto toohello carrello.</span><span class="sxs-lookup"><span data-stu-id="8cf38-127">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="8cf38-128">Fare clic su **Visualizza carrello**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="8cf38-129">Fare clic su **Download**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-129">Click **Download**.</span></span> <span data-ttu-id="8cf38-130">Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear.</span><span class="sxs-lookup"><span data-stu-id="8cf38-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="8cf38-131">Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserito in una sottocartella con stesso nome come aggiornamento hello hello.</span><span class="sxs-lookup"><span data-stu-id="8cf38-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="8cf38-132">cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8cf38-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
7. <span data-ttu-id="8cf38-133">Aprire hello copiati cartella, dovrebbe essere un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="8cf38-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="8cf38-134">Questo file è un hotfix o aggiornamento hello tooinstall utilizzato.</span><span class="sxs-lookup"><span data-stu-id="8cf38-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cf38-135">Installare l'aggiornamento di hello o un hotfix di hello</span><span class="sxs-lookup"><span data-stu-id="8cf38-135">Install hello update or hello hotfix</span></span>
<span data-ttu-id="8cf38-136">Installazione di un hotfix o aggiornamento precedente toohello, assicurarsi che si dispone di hello aggiornamento o hotfix hello scaricato localmente nell'host o accessibile tramite una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="8cf38-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="8cf38-137">Utilizzare questo metodo tooinstall Aggiorna su un dispositivo che esegue GA o aggiornare le versioni di software 0,1.</span><span class="sxs-lookup"><span data-stu-id="8cf38-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="8cf38-138">Questa procedura richiede minore toocomplete 2 minuti.</span><span class="sxs-lookup"><span data-stu-id="8cf38-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="8cf38-139">Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.</span><span class="sxs-lookup"><span data-stu-id="8cf38-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cf38-140">hotfix di aggiornamento o hello hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="8cf38-140">tooinstall hello update or hello hotfix</span></span>
1. <span data-ttu-id="8cf38-141">In hello interfaccia utente web locale, andare troppo**manutenzione** > **aggiornamento Software**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="8cf38-143">In **percorso del file di aggiornamento**, immettere il nome di file hello per l'aggiornamento di hello o hello hotfix.</span><span class="sxs-lookup"><span data-stu-id="8cf38-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="8cf38-144">È inoltre possibile esplorare i file di installazione di un hotfix o aggiornamento toohello se inserito in una condivisione di rete.</span><span class="sxs-lookup"><span data-stu-id="8cf38-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="8cf38-145">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-145">Click **Apply**.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="8cf38-147">Verrà visualizzato un avviso.</span><span class="sxs-lookup"><span data-stu-id="8cf38-147">A warning is displayed.</span></span> <span data-ttu-id="8cf38-148">Dato questo è un dispositivo singolo nodo, dopo che viene applicato l'aggiornamento di hello, hello dispositivo si riavvia e vi sia tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="8cf38-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="8cf38-149">Fare clic sull'icona di controllo di hello.</span><span class="sxs-lookup"><span data-stu-id="8cf38-149">Click hello check icon.</span></span>
   
   ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="8cf38-151">avvio dell'aggiornamento Hello.</span><span class="sxs-lookup"><span data-stu-id="8cf38-151">hello update starts.</span></span> <span data-ttu-id="8cf38-152">Dopo aver completato l'aggiornamento dispositivo hello, viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="8cf38-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="8cf38-153">Hello dell'interfaccia utente locale non è accessibile in tale intervallo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8cf38-153">hello local UI is not accessible in this duration.</span></span>
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="8cf38-155">Dopo aver completato il riavvio di hello, che viene visualizzata toohello **Accedi** pagina.</span><span class="sxs-lookup"><span data-stu-id="8cf38-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="8cf38-156">tooverify dispone di aggiornamento software per dispositivi hello nel web locale hello dell'interfaccia utente, andare troppo**manutenzione** > **aggiornamento Software**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="8cf38-157">la versione software Hello visualizzato deve essere **10.0.0.0.0.10288.0** per l'aggiornamento 0.3.</span><span class="sxs-lookup"><span data-stu-id="8cf38-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8cf38-158">I report versioni del software hello in modo leggermente diverso nell'interfaccia utente web locale hello hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="8cf38-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure classic portal.</span></span> <span data-ttu-id="8cf38-159">Ad esempio, hello report dell'interfaccia utente web locale **10.0.0.0.0.10288** e i report del portale di Azure classici hello **10.0.10288.0** per hello stessa versione.</span><span class="sxs-lookup"><span data-stu-id="8cf38-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure classic portal reports **10.0.10288.0** for hello same version.</span></span> 
   > 
   > 
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="8cf38-161">Utilizzare hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="8cf38-161">Use hello Azure classic portal</span></span>
<span data-ttu-id="8cf38-162">Se l'esecuzione di Update 0,2, è consigliabile installare gli aggiornamenti tramite hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="8cf38-162">If running Update 0.2, we recommend that you install updates through hello Azure classic portal.</span></span> <span data-ttu-id="8cf38-163">procedure portale Hello richiede hello utente tooscan, scaricare e installare gli aggiornamenti di hello.</span><span class="sxs-lookup"><span data-stu-id="8cf38-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="8cf38-164">Questa procedura accetta toocomplete circa 7 minuti.</span><span class="sxs-lookup"><span data-stu-id="8cf38-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="8cf38-165">Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.</span><span class="sxs-lookup"><span data-stu-id="8cf38-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="8cf38-166">Hello dopo l'installazione è stata completata (come indicato in base allo stato di processo al 100%), andare troppo**dispositivi > manutenzione > gli aggiornamenti Software**.</span><span class="sxs-lookup"><span data-stu-id="8cf38-166">After hello installation is complete (as indicated by job status at 100 %), go too**Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="8cf38-167">versione del software Hello visualizzato deve essere 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="8cf38-167">hello displayed software version should be 10.0.10288.0.</span></span>

![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="8cf38-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8cf38-169">Next steps</span></span>
<span data-ttu-id="8cf38-170">Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="8cf38-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

