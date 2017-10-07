---
title: condivide Array virtuale StorSimple aaaManage | Documenti Microsoft
description: Gestione di dispositivi StorSimple hello descrive e illustra come toouse, condivisioni toomanage l'Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="809da-103">Utilizzare condivisioni toomanage del servizio gestione di dispositivi StorSimple hello in hello Array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="809da-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="809da-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="809da-104">Overview</span></span>

<span data-ttu-id="809da-105">In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire condivisioni nell'Array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="809da-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="809da-106">servizio di gestione di dispositivi StorSimple Hello è un'estensione in hello portale di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="809da-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="809da-107">In aggiunta toomanaging condivisioni e volumi, è possibile utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire i dispositivi, visualizzare gli avvisi, gestire criteri di backup e gestire catalogo di backup hello.</span><span class="sxs-lookup"><span data-stu-id="809da-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="809da-108">Tipi di condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-108">Share Types</span></span>

<span data-ttu-id="809da-109">Le condivisioni StorSimple possono essere:</span><span class="sxs-lookup"><span data-stu-id="809da-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="809da-110">**Aggiunto in locale**: dati in tali condivisioni rimane nella matrice hello in qualsiasi momento e non lo spill toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="809da-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="809da-111">**A più livelli**: toohello cloud possono lo spill dei dati in tali condivisioni.</span><span class="sxs-lookup"><span data-stu-id="809da-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="809da-112">Quando si crea una condivisione a livelli, viene eseguito il provisioning di circa il 10% di spazio hello a livello locale hello e 90% dello spazio di hello è disponibile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="809da-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="809da-113">Ad esempio, se è stato eseguito il provisioning di una condivisione di 1 TB, 100 GB si troverà nello spazio locale hello e 900 GB verrebbe utilizzato nel cloud hello hello quando i livelli dati.</span><span class="sxs-lookup"><span data-stu-id="809da-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="809da-114">A sua volta, ciò implica che se si esaurisce tutto lo spazio locale hello sul dispositivo hello, è Impossibile eseguire il provisioning una condivisione a livelli (poiché hello 10% è necessario in hello locale livello non sarà disponibile).</span><span class="sxs-lookup"><span data-stu-id="809da-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="809da-115">Capacità con provisioning</span><span class="sxs-lookup"><span data-stu-id="809da-115">Provisioned capacity</span></span>

<span data-ttu-id="809da-116">Fare riferimento toohello per la capacità massima di provisioning per ogni tipo di condivisione nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="809da-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="809da-117">**Identificatore limite**</span><span class="sxs-lookup"><span data-stu-id="809da-117">**Limit identifier**</span></span> | <span data-ttu-id="809da-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="809da-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="809da-119">Dimensione minima di una condivisione a livelli</span><span class="sxs-lookup"><span data-stu-id="809da-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="809da-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="809da-120">500 GB</span></span> |
| <span data-ttu-id="809da-121">Dimensione massima di una condivisione a livelli</span><span class="sxs-lookup"><span data-stu-id="809da-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="809da-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="809da-122">20 TB</span></span> |
| <span data-ttu-id="809da-123">Dimensione minima di una condivisione aggiunta in locale</span><span class="sxs-lookup"><span data-stu-id="809da-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="809da-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="809da-124">50 GB</span></span> |
| <span data-ttu-id="809da-125">Dimensione massima di una condivisione aggiunta in locale</span><span class="sxs-lookup"><span data-stu-id="809da-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="809da-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="809da-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="809da-127">Pannello condivisioni Hello</span><span class="sxs-lookup"><span data-stu-id="809da-127">hello Shares blade</span></span>

<span data-ttu-id="809da-128">Hello **condivisioni** menu del Pannello di riepilogo del servizio StorSimple Visualizza elenco hello delle quote di archiviazione in una matrice specificata di StorSimple e consente toomanage li.</span><span class="sxs-lookup"><span data-stu-id="809da-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Pannello Condivisioni](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="809da-130">Una condivisione è costituita da una serie di attributi:</span><span class="sxs-lookup"><span data-stu-id="809da-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="809da-131">**Nome condivisione** : un nome descrittivo che deve essere univoco e consente di identificare condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="809da-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="809da-132">**Stato** : online oppure offline.</span><span class="sxs-lookup"><span data-stu-id="809da-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="809da-133">Se una condivisione è offline, gli utenti della condivisione di hello non saranno in grado di tooaccess è.</span><span class="sxs-lookup"><span data-stu-id="809da-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="809da-134">**Tipo** – indica se la condivisione hello è **a livelli** (hello predefinito) o **aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="809da-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="809da-135">**Capacità** – specifica hello quantità di dati utilizzati come toohello confrontata la quantità totale di dati che possono essere archiviati nella condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="809da-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="809da-136">**Descrizione** – un'impostazione facoltativa che consente di descrivere condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="809da-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="809da-137">**Autorizzazioni** -hello NTFS autorizzazioni toohello condivisione può essere gestite tramite Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="809da-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="809da-138">**Backup** : nel caso di hello Array virtuale StorSimple, tutte le condivisioni vengono abilitate automaticamente per il backup.</span><span class="sxs-lookup"><span data-stu-id="809da-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Dettagli sulle condivisioni](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="809da-140">Hello seguire le istruzioni riportate in questa esercitazione tooperform di hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="809da-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="809da-141">Aggiungere una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-141">Add a share</span></span>
* <span data-ttu-id="809da-142">Modificare una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-142">Modify a share</span></span>
* <span data-ttu-id="809da-143">Portare offline una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-143">Take a share offline</span></span>
* <span data-ttu-id="809da-144">Eliminare una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="809da-145">Aggiungere una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-145">Add a share</span></span>

1. <span data-ttu-id="809da-146">Pannello riepilogo servizio StorSimple hello, fare clic su **+ Aggiungi condivisione** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="809da-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="809da-147">Verrà visualizzata hello **Aggiungi condivisione** blade.</span><span class="sxs-lookup"><span data-stu-id="809da-147">This opens up hello **Add share** blade.</span></span>

    ![Aggiungere la condivisione](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="809da-149">In hello **Aggiungi condivisione** pannello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="809da-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="809da-150">In hello **nome condivisione** immettere un nome univoco per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="809da-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="809da-151">nome Hello deve essere una stringa che contiene 3 too127 caratteri.</span><span class="sxs-lookup"><span data-stu-id="809da-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="809da-152">Facoltativo **descrizione** per condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="809da-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="809da-153">Descrizione Hello consentirà di identificare i proprietari di condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="809da-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="809da-154">In hello **tipo** elenco a discesa specificare se toocreate un **a livelli** o **aggiunto in locale** condividere.</span><span class="sxs-lookup"><span data-stu-id="809da-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="809da-155">Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare la condivisione **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="809da-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="809da-156">Per tutti gli altri dati, selezionare una condivisone **A livelli** .</span><span class="sxs-lookup"><span data-stu-id="809da-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="809da-157">In hello **capacità** , specificare una dimensione di hello della condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="809da-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="809da-158">Una condivisione a livelli deve essere compresa tra 500 GB e 20 TB e una condivisione aggiunta in locale deve essere compresa tra 50 GB e 2 TB.</span><span class="sxs-lookup"><span data-stu-id="809da-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="809da-159">In hello **impostare come predefinita per le autorizzazioni complete** campo, assegnare hello autorizzazioni toohello utente o gruppo hello che accede a questa condivisione.</span><span class="sxs-lookup"><span data-stu-id="809da-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="809da-160">Specificare il nome di hello di hello utente o gruppo di utenti di hello in  _john@contoso.com_  formato.</span><span class="sxs-lookup"><span data-stu-id="809da-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="809da-161">È consigliabile utilizzare un tooaccess privilegi di amministratore di utente gruppo (anziché un singolo utente) tooallow tali condivisioni.</span><span class="sxs-lookup"><span data-stu-id="809da-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="809da-162">Dopo aver assegnato le autorizzazioni di hello qui, è possibile quindi utilizzare Esplora File toomodify queste autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="809da-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="809da-163">Al termine della configurazione della condivisione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="809da-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="809da-164">Verrà creata una condivisione con hello specificato le impostazioni e verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="809da-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="809da-165">Per impostazione predefinita, il backup verrà abilitato per la condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="809da-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="809da-166">tooconfirm che hello condivisione è stato creato correttamente, andare toohello **condivisioni** blade.</span><span class="sxs-lookup"><span data-stu-id="809da-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="809da-167">Dovrebbe essere hello condividere elencati.</span><span class="sxs-lookup"><span data-stu-id="809da-167">You should see hello share listed.</span></span>
   
    ![Creazione della condivisione completata](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="809da-169">Modificare una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-169">Modify a share</span></span>

<span data-ttu-id="809da-170">Modificare una condivisione quando è necessario descrizione hello toochange della condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="809da-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="809da-171">Una volta creata la condivisione di hello, è non possibile modificare nessuna altra proprietà di condivisione.</span><span class="sxs-lookup"><span data-stu-id="809da-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="809da-172">toomodify una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-172">toomodify a share</span></span>

1. <span data-ttu-id="809da-173">Da hello **condivisioni** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello condivisione desiderato toomodify risiede.</span><span class="sxs-lookup"><span data-stu-id="809da-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="809da-174">**Selezionare** hello condivisione tooview hello corrente descrizione e la modifica.</span><span class="sxs-lookup"><span data-stu-id="809da-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="809da-175">Salvare le modifiche, fare clic su hello **salvare** barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="809da-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="809da-176">Verranno applicate le impostazioni specificate e verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="809da-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="809da-177">Modificare la condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="809da-178">Portare offline una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-178">Take a share offline</span></span>

<span data-ttu-id="809da-179">Potrebbe essere necessario tootake una condivisione non in linea durante la pianificazione toomodify o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="809da-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="809da-180">Quando una condivisione è offline, non è disponibile per l'accesso in lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="809da-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="809da-181">Sarà necessario tootake hello condivisione offline nell'host di hello e sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="809da-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="809da-182">tootake una condivisione non in linea</span><span class="sxs-lookup"><span data-stu-id="809da-182">tootake a share offline</span></span>

1. <span data-ttu-id="809da-183">Assicurarsi che la condivisione hello in questione non è in uso prima di portarlo offline.</span><span class="sxs-lookup"><span data-stu-id="809da-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="809da-184">Assumere hello condivisione matrice hello offline eseguendo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="809da-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="809da-185">Da hello **condivisioni** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello risiede condivisione desiderato tootake offline.</span><span class="sxs-lookup"><span data-stu-id="809da-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="809da-186">**Selezionare** condivisione hello e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **portare offline**.</span><span class="sxs-lookup"><span data-stu-id="809da-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Condivisione offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="809da-188">Esaminare le informazioni di hello in hello **portare offline** pannello e confermare l'operazione di accettazione di hello.</span><span class="sxs-lookup"><span data-stu-id="809da-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="809da-189">Fare clic su **portare offline** tootake della condivisione hello offline.</span><span class="sxs-lookup"><span data-stu-id="809da-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="809da-190">Si noterà una notifica dell'operazione di hello in corso.</span><span class="sxs-lookup"><span data-stu-id="809da-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="809da-191">tooconfirm che hello condivisione è stato eseguito correttamente non in linea, andare toohello **condivisioni** blade.</span><span class="sxs-lookup"><span data-stu-id="809da-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="809da-192">Dovrebbe essere stato hello della condivisione hello come non in linea.</span><span class="sxs-lookup"><span data-stu-id="809da-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="809da-193">Eliminare una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="809da-194">È possibile eliminare una condivisione solo se è offline.</span><span class="sxs-lookup"><span data-stu-id="809da-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="809da-195">Completare hello seguendo i passaggi toodelete una condivisione.</span><span class="sxs-lookup"><span data-stu-id="809da-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="809da-196">toodelete una condivisione</span><span class="sxs-lookup"><span data-stu-id="809da-196">toodelete a share</span></span>

1. <span data-ttu-id="809da-197">Da hello **condivisioni** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui condivisione hello desiderato toodelete risiede.</span><span class="sxs-lookup"><span data-stu-id="809da-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="809da-198">**Selezionare** condivisione hello e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="809da-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Eliminare la condivisione](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="809da-200">Controllare lo stato di hello della condivisione hello desiderato toodelete.</span><span class="sxs-lookup"><span data-stu-id="809da-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="809da-201">Se si desidera toodelete condivisione di hello non è offline, portarlo prima offline.</span><span class="sxs-lookup"><span data-stu-id="809da-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="809da-202">Seguire i passaggi di hello in [portare offline una condivisione di](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="809da-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="809da-203">Alla richiesta di conferma in hello **eliminare** pannello accettare conferma hello e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="809da-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="809da-204">condivisione di Hello verrà eliminata e hello **condivisioni** pannello mostra l'elenco di hello aggiornato delle azioni all'interno della matrice virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="809da-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="809da-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="809da-205">Next steps</span></span>
<span data-ttu-id="809da-206">Informazioni su come troppo[clonare una condivisione di StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="809da-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

