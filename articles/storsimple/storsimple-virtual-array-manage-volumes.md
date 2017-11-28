---
title: i volumi StorSimple Virtual Array aaaManage | Documenti Microsoft
description: Gestione di dispositivi StorSimple hello descrive e illustra come toouse volumi toomanage l'Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="3c70e-103">Utilizzare Gestione periferiche di StorSimple servizio toomanage volumi hello Array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="3c70e-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="3c70e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3c70e-104">Overview</span></span>

<span data-ttu-id="3c70e-105">In questa esercitazione viene illustrato come toouse hello toocreate servizio di gestione di dispositivi StorSimple e gestire volumi sull'Array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="3c70e-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="3c70e-106">servizio di gestione di dispositivi StorSimple Hello è un'estensione in hello portale di Azure che consente di gestire la soluzione StorSimple da una singola interfaccia web.</span><span class="sxs-lookup"><span data-stu-id="3c70e-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="3c70e-107">In aggiunta toomanaging condivisioni e volumi, è possibile utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire i dispositivi, visualizzare gli avvisi, visualizzare e gestire criteri di backup e di catalogo di backup hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="3c70e-108">Tipi di volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-108">Volume Types</span></span>

<span data-ttu-id="3c70e-109">I volumi di StorSimple possono essere:</span><span class="sxs-lookup"><span data-stu-id="3c70e-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="3c70e-110">**Aggiunto in locale**: dati in tali volumi rimane nella matrice hello in qualsiasi momento e non lo spill toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="3c70e-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="3c70e-111">**A più livelli**: toohello cloud possono lo spill dei dati in tali volumi.</span><span class="sxs-lookup"><span data-stu-id="3c70e-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="3c70e-112">Quando si crea un volume a livelli, viene eseguito il provisioning di circa il 10% di spazio hello a livello locale hello e 90% dello spazio di hello è disponibile nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="3c70e-113">Ad esempio, se è stato eseguito il provisioning di un volume di 1 TB, 100 GB si troverà nello spazio locale hello e 900 GB verrebbe utilizzato nel cloud hello hello quando i livelli dati.</span><span class="sxs-lookup"><span data-stu-id="3c70e-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="3c70e-114">A sua volta, ciò implica che se si esaurisce tutto lo spazio locale hello sul dispositivo hello, è Impossibile eseguire il provisioning un volume a livelli (poiché hello 10% è necessario in hello locale livello non sarà disponibile).</span><span class="sxs-lookup"><span data-stu-id="3c70e-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="3c70e-115">Capacità con provisioning</span><span class="sxs-lookup"><span data-stu-id="3c70e-115">Provisioned capacity</span></span>
<span data-ttu-id="3c70e-116">Fare riferimento toohello seguente tabella per la capacità massima di provisioning per ogni tipo di volume.</span><span class="sxs-lookup"><span data-stu-id="3c70e-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="3c70e-117">**Identificatore limite**</span><span class="sxs-lookup"><span data-stu-id="3c70e-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="3c70e-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="3c70e-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="3c70e-119">Dimensione minima di un volume a livelli</span><span class="sxs-lookup"><span data-stu-id="3c70e-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="3c70e-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="3c70e-120">500 GB</span></span>        |
| <span data-ttu-id="3c70e-121">Dimensione massima di un volume a livelli</span><span class="sxs-lookup"><span data-stu-id="3c70e-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="3c70e-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="3c70e-122">5 TB</span></span>          |
| <span data-ttu-id="3c70e-123">Dimensione minima di un volume aggiunto in locale</span><span class="sxs-lookup"><span data-stu-id="3c70e-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="3c70e-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="3c70e-124">50 GB</span></span>         |
| <span data-ttu-id="3c70e-125">Dimensione massima di un volume aggiunto in locale</span><span class="sxs-lookup"><span data-stu-id="3c70e-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="3c70e-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="3c70e-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="3c70e-127">Pannello volumi Hello</span><span class="sxs-lookup"><span data-stu-id="3c70e-127">hello Volumes blade</span></span>
<span data-ttu-id="3c70e-128">Hello **volumi** menu del Pannello di riepilogo del servizio StorSimple Visualizza elenco hello di volumi di archiviazione in una matrice specificata di StorSimple e consente toomanage li.</span><span class="sxs-lookup"><span data-stu-id="3c70e-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Pannello Volumi](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="3c70e-130">Un volume è costituito da una serie di attributi:</span><span class="sxs-lookup"><span data-stu-id="3c70e-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="3c70e-131">**Nome del volume** : un nome descrittivo che deve essere univoco e consente di identificare il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="3c70e-132">**Stato** : online oppure offline.</span><span class="sxs-lookup"><span data-stu-id="3c70e-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="3c70e-133">Se un volume è offline, non è visibile tooinitiators (server) che è consentito l'accesso toouse hello volume.</span><span class="sxs-lookup"><span data-stu-id="3c70e-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="3c70e-134">**Tipo** – indica se il volume di hello è **a livelli** (hello predefinito) o **aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="3c70e-135">**Capacità** – specifica hello quantità di dati utilizzati come toohello confrontata la quantità totale di dati che possono essere archiviati dall'iniziatore hello (server).</span><span class="sxs-lookup"><span data-stu-id="3c70e-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="3c70e-136">**Backup** : nel caso di hello Array virtuale StorSimple, tutti i volumi vengono abilitati automaticamente per il backup.</span><span class="sxs-lookup"><span data-stu-id="3c70e-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="3c70e-137">**Gli host connessi** – specifica iniziatori hello (server) che sono consentiti l'accesso toothis volume.</span><span class="sxs-lookup"><span data-stu-id="3c70e-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Dettagli sui volumi](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="3c70e-139">Hello seguire le istruzioni riportate in questa esercitazione tooperform di hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="3c70e-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="3c70e-140">Aggiungere un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-140">Add a volume</span></span>
* <span data-ttu-id="3c70e-141">Modificare un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-141">Modify a volume</span></span>
* <span data-ttu-id="3c70e-142">Portare un volume offline</span><span class="sxs-lookup"><span data-stu-id="3c70e-142">Take a volume offline</span></span>
* <span data-ttu-id="3c70e-143">Eliminare un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="3c70e-144">Aggiungere un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-144">Add a volume</span></span>

1. <span data-ttu-id="3c70e-145">Pannello riepilogo servizio StorSimple hello, fare clic su **+ Aggiungi volume** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="3c70e-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="3c70e-146">Verrà visualizzata hello **aggiungere volume** blade.</span><span class="sxs-lookup"><span data-stu-id="3c70e-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Aggiungi volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="3c70e-148">In hello **aggiungere volume** pannello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c70e-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="3c70e-149">In hello **nome Volume** immettere un nome univoco per il volume.</span><span class="sxs-lookup"><span data-stu-id="3c70e-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="3c70e-150">nome Hello deve essere una stringa che contiene 3 too127 caratteri.</span><span class="sxs-lookup"><span data-stu-id="3c70e-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="3c70e-151">In hello **tipo** elenco a discesa specificare se toocreate un **a livelli** o **aggiunto in locale** volume.</span><span class="sxs-lookup"><span data-stu-id="3c70e-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="3c70e-152">Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare il volume **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="3c70e-153">Per tutti gli altri dati, selezionare volume **A livelli**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="3c70e-154">In hello **capacità** specificare dimensioni di hello del volume hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="3c70e-155">Un volume a livelli deve essere compreso tra 500 GB e 5 TB e un volume aggiunto in locale deve essere compreso tra 50 e 500 GB.</span><span class="sxs-lookup"><span data-stu-id="3c70e-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="3c70e-156">Fare clic su **connesso host**, selezionare un accesso controllo record (ACR) corrispondente toohello iniziatore iSCSI che desidera tooconnect toothis volume e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="3c70e-157">tooadd un nuovo host connessi, fare clic su **Aggiungi nuovo**, immettere un nome per l'host di hello e relativo iSCSI nome qualificato e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Aggiungi volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="3c70e-159">Al termine della configurazione del volume, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="3c70e-160">Verrà creato un volume con hello specificato le impostazioni e verrà visualizzata una notifica al momento della creazione ha esito positivo di hello di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="3c70e-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="3c70e-161">Per impostazione predefinita, il backup verrà abilitato per il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="3c70e-162">tooconfirm che hello volume è stato creato correttamente, andare toohello **volumi** blade.</span><span class="sxs-lookup"><span data-stu-id="3c70e-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="3c70e-163">Verrà visualizzato il volume di hello elencato.</span><span class="sxs-lookup"><span data-stu-id="3c70e-163">You should see hello volume listed.</span></span>
   
    ![Creazione del volume completata](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="3c70e-165">Modificare un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-165">Modify a volume</span></span>

<span data-ttu-id="3c70e-166">Modificare un volume quando sono necessari toochange hello host che accedono a volume hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="3c70e-167">Hello altri attributi di un volume non possono essere modificati dopo aver creato il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="3c70e-168">toomodify un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-168">toomodify a volume</span></span>

1. <span data-ttu-id="3c70e-169">Da hello **volumi** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello volume desiderato toomodify risiede.</span><span class="sxs-lookup"><span data-stu-id="3c70e-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="3c70e-170">**Selezionare** hello volume e fare clic su **connesso host** tooview hello host attualmente connesso e modificarlo tooa diversi server.</span><span class="sxs-lookup"><span data-stu-id="3c70e-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Modificare il volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="3c70e-172">Salvare le modifiche, fare clic su hello **salvare** barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="3c70e-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="3c70e-173">Verranno applicate le impostazioni specificate e verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="3c70e-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="3c70e-174">Portare un volume offline</span><span class="sxs-lookup"><span data-stu-id="3c70e-174">Take a volume offline</span></span>

<span data-ttu-id="3c70e-175">Potrebbe essere necessario tootake un volume offline quando si pianifica toomodify o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="3c70e-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="3c70e-176">Quando un volume è offline, non è disponibile per l'accesso in lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="3c70e-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="3c70e-177">Sarà necessario tootake hello volume offline nell'host di hello e sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="3c70e-178">tootake un volume offline</span><span class="sxs-lookup"><span data-stu-id="3c70e-178">tootake a volume offline</span></span>

1. <span data-ttu-id="3c70e-179">Assicurarsi che il volume di hello in questione non è in uso prima di portarlo offline.</span><span class="sxs-lookup"><span data-stu-id="3c70e-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="3c70e-180">Portare hello volume offline nell'host di hello prima.</span><span class="sxs-lookup"><span data-stu-id="3c70e-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="3c70e-181">In questo modo si evita i potenziali rischi di danneggiamento dei dati nel volume hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="3c70e-182">Per passaggi specifici, vedere toohello istruzioni per il sistema operativo host.</span><span class="sxs-lookup"><span data-stu-id="3c70e-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="3c70e-183">Una volta volume hello host hello è offline, adottare volume hello nella matrice hello offline eseguendo hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3c70e-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="3c70e-184">Da hello **volumi** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello risiede volume desiderato tootake offline.</span><span class="sxs-lookup"><span data-stu-id="3c70e-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="3c70e-185">**Selezionare** hello volume e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **portare offline**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="3c70e-187">Esaminare le informazioni di hello in hello **portare offline** pannello e confermare l'operazione di accettazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="3c70e-188">Fare clic su **portare offline** tootake offline volume hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="3c70e-189">Si noterà una notifica dell'operazione di hello in corso.</span><span class="sxs-lookup"><span data-stu-id="3c70e-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="3c70e-190">tooconfirm volume hello correttamente è stato portato offline, visitare toohello **volumi** blade.</span><span class="sxs-lookup"><span data-stu-id="3c70e-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="3c70e-191">Si dovrebbe essere stato hello del volume di hello come offline.</span><span class="sxs-lookup"><span data-stu-id="3c70e-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Conferma volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="3c70e-193">Eliminare un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c70e-194">È possibile eliminare un volume solo se è offline.</span><span class="sxs-lookup"><span data-stu-id="3c70e-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="3c70e-195">Completare hello seguendo i passaggi toodelete un volume.</span><span class="sxs-lookup"><span data-stu-id="3c70e-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="3c70e-196">toodelete un volume</span><span class="sxs-lookup"><span data-stu-id="3c70e-196">toodelete a volume</span></span>

1. <span data-ttu-id="3c70e-197">Da hello **volumi** impostato nel Pannello di riepilogo di hello StorSimple servizio, selezionare hello array virtuale in cui hello volume desiderato toodelete risiede.</span><span class="sxs-lookup"><span data-stu-id="3c70e-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="3c70e-198">**Selezionare** hello volume e fare clic su **...**  (in alternativa fare doppio clic su questa riga) e selezionare il menu di scelta rapida hello **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Eliminare il volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="3c70e-200">Controllare lo stato di hello del volume hello desiderato toodelete.</span><span class="sxs-lookup"><span data-stu-id="3c70e-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="3c70e-201">Se volume hello da toodelete non è offline, le operazioni non in linea hello in primo luogo, seguenti [portare offline un volume](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="3c70e-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="3c70e-202">Alla richiesta di conferma in hello **eliminare** pannello accettare conferma hello e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="3c70e-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="3c70e-203">volume Hello verrà eliminata e hello **volumi** pannello verrà visualizzato l'elenco di hello aggiornato di volumi presenti array virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3c70e-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c70e-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c70e-204">Next steps</span></span>

<span data-ttu-id="3c70e-205">Informazioni su come troppo[clonare un volume StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="3c70e-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

