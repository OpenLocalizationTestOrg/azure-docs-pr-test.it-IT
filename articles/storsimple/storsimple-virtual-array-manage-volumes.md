---
title: Gestire i volumi sull'array virtuale StorSimple | Documentazione Microsoft
description: Descrive Gestione dispositivi StorSimple e illustra come usare questo servizio per gestire i volumi sull'array virtuale StorSimple.
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
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="56866-103">Usare il servizio Gestione dispositivi StorSimple per visualizzare i volumi sull'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="56866-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="56866-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="56866-104">Overview</span></span>

<span data-ttu-id="56866-105">Questa esercitazione illustra come usare il servizio Gestione dispositivi StorSimple per creare e gestire i volumi nell'array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="56866-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="56866-106">Il servizio Gestione dispositivi StorSimple è un'estensione del portale di Azure che consente di gestire la soluzione StorSimple da un'unica interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="56866-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="56866-107">Oltre alla gestione di condivisioni e volumi, è possibile usare il servizio Gestione dispositivi StorSimple per visualizzare e gestire dispositivi, visualizzare avvisi, visualizzare e gestire criteri di backup e il catalogo di backup.</span><span class="sxs-lookup"><span data-stu-id="56866-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="56866-108">Tipi di volume</span><span class="sxs-lookup"><span data-stu-id="56866-108">Volume Types</span></span>

<span data-ttu-id="56866-109">I volumi di StorSimple possono essere:</span><span class="sxs-lookup"><span data-stu-id="56866-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="56866-110">**Aggiunto in locale**: i dati in questi volumi rimangono sempre nell'array e non vengono distribuiti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="56866-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="56866-111">**A livelli**: i dati in questi volumi possono essere distribuiti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="56866-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="56866-112">Quando si crea un volume a livelli, viene eseguito il provisioning di circa il 10% dello spazio a livello locale e del 90% dello spazio nel cloud.</span><span class="sxs-lookup"><span data-stu-id="56866-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="56866-113">Ad esempio, se si esegue il provisioning di un volume da 1 TB, 100 GB si trovano nello spazio locale e 900 GB vengono usati nel cloud quando i dati sono disposti a livelli.</span><span class="sxs-lookup"><span data-stu-id="56866-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="56866-114">Questo implica che, se si esaurisce tutto lo spazio locale nel dispositivo, non è possibile eseguire il provisioning di una volume a livelli (perché il 10% necessario a livello locale non è disponibile).</span><span class="sxs-lookup"><span data-stu-id="56866-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="56866-115">Capacità con provisioning</span><span class="sxs-lookup"><span data-stu-id="56866-115">Provisioned capacity</span></span>
<span data-ttu-id="56866-116">Fare riferimento alla tabella seguente per conoscere la capacità massima di cui viene eseguito il provisioning per ogni tipo di volume.</span><span class="sxs-lookup"><span data-stu-id="56866-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="56866-117">**Identificatore limite**</span><span class="sxs-lookup"><span data-stu-id="56866-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="56866-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="56866-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="56866-119">Dimensione minima di un volume a livelli</span><span class="sxs-lookup"><span data-stu-id="56866-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="56866-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="56866-120">500 GB</span></span>        |
| <span data-ttu-id="56866-121">Dimensione massima di un volume a livelli</span><span class="sxs-lookup"><span data-stu-id="56866-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="56866-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="56866-122">5 TB</span></span>          |
| <span data-ttu-id="56866-123">Dimensione minima di un volume aggiunto in locale</span><span class="sxs-lookup"><span data-stu-id="56866-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="56866-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="56866-124">50 GB</span></span>         |
| <span data-ttu-id="56866-125">Dimensione massima di un volume aggiunto in locale</span><span class="sxs-lookup"><span data-stu-id="56866-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="56866-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="56866-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="56866-127">Il pannello Volumi</span><span class="sxs-lookup"><span data-stu-id="56866-127">The Volumes blade</span></span>
<span data-ttu-id="56866-128">Il menu **Volumi** nel pannello di riepilogo servizio StorSimple visualizza l'elenco di volumi di archiviazione su un determinato array StorSimple e ne consente la gestione.</span><span class="sxs-lookup"><span data-stu-id="56866-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Pannello Volumi](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="56866-130">Un volume è costituito da una serie di attributi:</span><span class="sxs-lookup"><span data-stu-id="56866-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="56866-131">**Nome volume** : un nome descrittivo che deve essere univoco e consente di identificare il volume.</span><span class="sxs-lookup"><span data-stu-id="56866-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="56866-132">**Stato** : online oppure offline.</span><span class="sxs-lookup"><span data-stu-id="56866-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="56866-133">Se un volume è offline, non è visibile agli iniziatori (server) che possono accedervi per usarlo.</span><span class="sxs-lookup"><span data-stu-id="56866-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="56866-134">**Tipo**: indica se il volume è **A livelli** (impostazione predefinita) o **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="56866-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="56866-135">**Capacità**: specifica la quantità di dati usati rispetto alle quantità totale di dati che possono essere archiviati dall'iniziatore (server).</span><span class="sxs-lookup"><span data-stu-id="56866-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="56866-136">**Backup**: nel caso dell'array virtuale StorSimple, tutti i volumi vengono abilitati automaticamente per il backup.</span><span class="sxs-lookup"><span data-stu-id="56866-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="56866-137">**Host connessi**: specifica gli iniziatori (server) a cui è consentito l'accesso a questo volume.</span><span class="sxs-lookup"><span data-stu-id="56866-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Dettagli sui volumi](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="56866-139">Usare le istruzioni di questa esercitazione per eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="56866-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="56866-140">Aggiungere un volume</span><span class="sxs-lookup"><span data-stu-id="56866-140">Add a volume</span></span>
* <span data-ttu-id="56866-141">Modificare un volume</span><span class="sxs-lookup"><span data-stu-id="56866-141">Modify a volume</span></span>
* <span data-ttu-id="56866-142">Portare un volume offline</span><span class="sxs-lookup"><span data-stu-id="56866-142">Take a volume offline</span></span>
* <span data-ttu-id="56866-143">Eliminare un volume</span><span class="sxs-lookup"><span data-stu-id="56866-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="56866-144">Aggiungere un volume</span><span class="sxs-lookup"><span data-stu-id="56866-144">Add a volume</span></span>

1. <span data-ttu-id="56866-145">Nel pannello di riepilogo servizio StorSimple fare clic su **+ Aggiungi volume** dalla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="56866-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="56866-146">Verrà visualizzato il pannello **Aggiungi volume**.</span><span class="sxs-lookup"><span data-stu-id="56866-146">This opens up the **Add volume** blade.</span></span>
   
    ![Aggiungi volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="56866-148">Nel pannello **Aggiungi volume** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="56866-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="56866-149">Nel campo **Nome del volume** immettere un nome univoco per il volume.</span><span class="sxs-lookup"><span data-stu-id="56866-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="56866-150">Il nome deve essere una stringa contenente da 3 a 127 caratteri.</span><span class="sxs-lookup"><span data-stu-id="56866-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="56866-151">Nell'elenco a discesa **Tipo** specificare se creare un volume **A livelli** o **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="56866-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="56866-152">Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare il volume **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="56866-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="56866-153">Per tutti gli altri dati, selezionare volume **A livelli**.</span><span class="sxs-lookup"><span data-stu-id="56866-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="56866-154">Nel campo **Capacità** specificare le dimensioni del volume.</span><span class="sxs-lookup"><span data-stu-id="56866-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="56866-155">Un volume a livelli deve essere compreso tra 500 GB e 5 TB e un volume aggiunto in locale deve essere compreso tra 50 e 500 GB.</span><span class="sxs-lookup"><span data-stu-id="56866-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="56866-156">Fare clic su **Host connessi**, selezionare un record di controllo di accesso (ACR) corrispondente all'iniziatore iSCSI a cui si desidera connettere questo volume, quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="56866-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="56866-157">Per aggiungere un nuovo host connesso, fare clic su **Aggiungi nuovo**, immettere un nome per l'host e il relativo nome qualificato iSCSI (IQN) e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="56866-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Aggiungi volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="56866-159">Al termine della configurazione del volume, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="56866-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="56866-160">Verrà creato un volume con le impostazioni specificate e verrà visualizzata una notifica sulla creazione.</span><span class="sxs-lookup"><span data-stu-id="56866-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="56866-161">Per impostazione predefinita, il backup verrà abilitato per il volume.</span><span class="sxs-lookup"><span data-stu-id="56866-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="56866-162">Per verificare che il volume sia stato creato, passare al pannello **Volumi**.</span><span class="sxs-lookup"><span data-stu-id="56866-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="56866-163">Il volume deve essere visualizzato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="56866-163">You should see the volume listed.</span></span>
   
    ![Creazione del volume completata](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="56866-165">Modificare un volume</span><span class="sxs-lookup"><span data-stu-id="56866-165">Modify a volume</span></span>

<span data-ttu-id="56866-166">Modificare un volume quando occorre modificare gli host che vi accedono.</span><span class="sxs-lookup"><span data-stu-id="56866-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="56866-167">Gli altri attributi di un volume non possono essere modificati dopo aver creato il volume.</span><span class="sxs-lookup"><span data-stu-id="56866-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="56866-168">Per modificare un volume</span><span class="sxs-lookup"><span data-stu-id="56866-168">To modify a volume</span></span>

1. <span data-ttu-id="56866-169">Nell'impostazione **Volumi** del pannello di riepilogo servizio StorSimple selezionare l'array virtuale in cui risiede il volume da modificare.</span><span class="sxs-lookup"><span data-stu-id="56866-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="56866-170">**Selezionare** il volume e fare clic su **Host connessi** per visualizzare l'host attualmente connesso e modificarlo in un altro server.</span><span class="sxs-lookup"><span data-stu-id="56866-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Modificare il volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="56866-172">Salvare le modifiche facendo clic sulla barra di comando **Salva**.</span><span class="sxs-lookup"><span data-stu-id="56866-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="56866-173">Verranno applicate le impostazioni specificate e verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="56866-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="56866-174">Portare un volume offline</span><span class="sxs-lookup"><span data-stu-id="56866-174">Take a volume offline</span></span>

<span data-ttu-id="56866-175">Potrebbe essere necessario portare un volume offline per modificarlo o eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="56866-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="56866-176">Quando un volume è offline, non è disponibile per l'accesso in lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="56866-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="56866-177">È necessario portare offline il volume nell'host e sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="56866-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="56866-178">Per portare un volume offline</span><span class="sxs-lookup"><span data-stu-id="56866-178">To take a volume offline</span></span>

1. <span data-ttu-id="56866-179">Assicurarsi che il volume in questione non sia in uso prima di portarlo offline.</span><span class="sxs-lookup"><span data-stu-id="56866-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="56866-180">Portare offline il volume prima nell'host.</span><span class="sxs-lookup"><span data-stu-id="56866-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="56866-181">Ciò consente di eliminare qualsiasi potenziale rischio di danneggiamento dei dati nel volume.</span><span class="sxs-lookup"><span data-stu-id="56866-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="56866-182">Per i passaggi specifici, vedere le istruzioni per il sistema operativo dell’host.</span><span class="sxs-lookup"><span data-stu-id="56866-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="56866-183">Quando il volume sull'host è offline, portare il volume sull'array offline eseguendo i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="56866-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="56866-184">Nell'impostazione **Volumi** del pannello di riepilogo servizio StorSimple selezionare l'array virtuale in cui risiede il volume da portare offline.</span><span class="sxs-lookup"><span data-stu-id="56866-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="56866-185">**Selezionare** il volume e fare clic su **...** (in alternativa fare clic con il pulsante destro del mouse su questa riga) e selezionare **Porta offline** nel menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="56866-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="56866-187">Esaminare le informazioni nel pannello **Porta offline** e confermare l'accettazione dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="56866-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="56866-188">Fare clic su **Porta offline** per portare offilne il volume.</span><span class="sxs-lookup"><span data-stu-id="56866-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="56866-189">Verrà visualizzata una notifica dell'operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="56866-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="56866-190">Per verificare se il volume è stato portato offline, passare al pannello **Volumi**.</span><span class="sxs-lookup"><span data-stu-id="56866-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="56866-191">Lo stato del volume dovrebbe apparire come offline.</span><span class="sxs-lookup"><span data-stu-id="56866-191">You should see the status of the volume as offline.</span></span>
     
       ![Conferma volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="56866-193">Eliminare un volume</span><span class="sxs-lookup"><span data-stu-id="56866-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56866-194">È possibile eliminare un volume solo se è offline.</span><span class="sxs-lookup"><span data-stu-id="56866-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="56866-195">Completare la procedura seguente per eliminare un volume.</span><span class="sxs-lookup"><span data-stu-id="56866-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="56866-196">Per eliminare un volume</span><span class="sxs-lookup"><span data-stu-id="56866-196">To delete a volume</span></span>

1. <span data-ttu-id="56866-197">Nell'impostazione **Volumi** del pannello di riepilogo servizio StorSimple selezionare l'array virtuale in cui risiede il volume da eliminare.</span><span class="sxs-lookup"><span data-stu-id="56866-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="56866-198">**Selezionare** il volume e fare clic su **...** (in alternativa fare clic con il pulsante destro del mouse su questa riga) e selezionare **Elimina** nel menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="56866-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Eliminare il volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="56866-200">Verificare lo stato del volume che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="56866-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="56866-201">Se il volume che si desidera eliminare non è offline, portarlo innanzitutto offline seguendo i passaggi indicati in [Portare un volume offline](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="56866-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="56866-202">Alla richiesta di conferma nel pannello **Elimina** accettare la conferma e fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="56866-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="56866-203">Il volume verrà eliminato e nella pagina **Volumi** sarà visualizzato l'elenco aggiornato di volumi presenti nell'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="56866-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56866-204">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="56866-204">Next steps</span></span>

<span data-ttu-id="56866-205">Informazioni su come [clonare un volume StorSimple](storsimple-virtual-array-clone.md)</span><span class="sxs-lookup"><span data-stu-id="56866-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

