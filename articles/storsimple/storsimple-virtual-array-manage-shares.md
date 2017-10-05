---
title: Gestire le condivisioni sull'array virtuale StorSimple | Documentazione Microsoft
description: Descrive Gestione dispositivi StorSimple e illustra come usare questo servizio per gestire le condivisioni sull'array virtuale StorSimple.
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
ms.openlocfilehash: e5c62689de36baa175001f5f4f70d87568876ef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-shares-on-the-storsimple-virtual-array"></a><span data-ttu-id="e50f9-103">Usare il servizio Gestione dispositivi StorSimple per visualizzare le condivisioni sull'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="e50f9-103">Use the StorSimple Device Manager service to manage shares on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="e50f9-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e50f9-104">Overview</span></span>

<span data-ttu-id="e50f9-105">Questa esercitazione illustra come usare il servizio Gestione dispositivi StorSimple per creare e gestire le condivisioni sull'array virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="e50f9-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="e50f9-106">Il servizio Gestione dispositivi StorSimple è un'estensione del portale di Azure che consente di gestire la soluzione StorSimple da un'unica interfaccia Web.</span><span class="sxs-lookup"><span data-stu-id="e50f9-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="e50f9-107">Oltre alla gestione di condivisioni e volumi, è possibile usare il servizio Gestione dispositivi StorSimple per visualizzare e gestire dispositivi, visualizzare avvisi, gestire criteri di backup e il catalogo di backup.</span><span class="sxs-lookup"><span data-stu-id="e50f9-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, manage backup policies, and manage the backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="e50f9-108">Tipi di condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-108">Share Types</span></span>

<span data-ttu-id="e50f9-109">Le condivisioni StorSimple possono essere:</span><span class="sxs-lookup"><span data-stu-id="e50f9-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="e50f9-110">**Aggiunto in locale**: i dati in queste condivisioni rimangono sempre nell'array e non vengono distribuiti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e50f9-110">**Locally pinned**: Data in these shares stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="e50f9-111">**A livelli**: i dati in queste condivisioni possono essere distribuiti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e50f9-111">**Tiered**: Data in these shares can spill to the cloud.</span></span> <span data-ttu-id="e50f9-112">Quando si crea una condivisione a livelli, viene eseguito il provisioning di circa il 10% dello spazio a livello locale e del 90% dello spazio nel cloud.</span><span class="sxs-lookup"><span data-stu-id="e50f9-112">When you create a tiered share, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="e50f9-113">Ad esempio, se si esegue il provisioning di una condivisione da 1 TB, 100 GB si trovano nello spazio locale e 900 GB vengono usati nel cloud quando i dati sono disposti a livelli.</span><span class="sxs-lookup"><span data-stu-id="e50f9-113">For example, if you provisioned a 1 TB share, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="e50f9-114">Questo implica che, se si esaurisce tutto lo spazio locale nel dispositivo, non è possibile eseguire il provisioning di una condivisione a livelli perché il 10% necessario a livello locale non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="e50f9-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered share (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="e50f9-115">Capacità con provisioning</span><span class="sxs-lookup"><span data-stu-id="e50f9-115">Provisioned capacity</span></span>

<span data-ttu-id="e50f9-116">Fare riferimento alla tabella seguente per conoscere la capacità massima di cui viene eseguito il provisioning per ogni tipo di condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-116">Refer to the following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="e50f9-117">**Identificatore limite**</span><span class="sxs-lookup"><span data-stu-id="e50f9-117">**Limit identifier**</span></span> | <span data-ttu-id="e50f9-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="e50f9-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="e50f9-119">Dimensione minima di una condivisione a livelli</span><span class="sxs-lookup"><span data-stu-id="e50f9-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="e50f9-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="e50f9-120">500 GB</span></span> |
| <span data-ttu-id="e50f9-121">Dimensione massima di una condivisione a livelli</span><span class="sxs-lookup"><span data-stu-id="e50f9-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="e50f9-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="e50f9-122">20 TB</span></span> |
| <span data-ttu-id="e50f9-123">Dimensione minima di una condivisione aggiunta in locale</span><span class="sxs-lookup"><span data-stu-id="e50f9-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="e50f9-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="e50f9-124">50 GB</span></span> |
| <span data-ttu-id="e50f9-125">Dimensione massima di una condivisione aggiunta in locale</span><span class="sxs-lookup"><span data-stu-id="e50f9-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="e50f9-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="e50f9-126">2 TB</span></span> |

## <a name="the-shares-blade"></a><span data-ttu-id="e50f9-127">Il pannello Condivisioni</span><span class="sxs-lookup"><span data-stu-id="e50f9-127">The Shares blade</span></span>

<span data-ttu-id="e50f9-128">Il menu **Condivisioni** nel pannello di riepilogo servizio StorSimple visualizza l'elenco di condivisioni di archiviazione su un determinato array StorSimple e ne consente la gestione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-128">The **Shares** menu on your StorSimple service summary blade displays the list of storage shares on a given StorSimple array and allows you to manage them.</span></span>

![Pannello Condivisioni](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="e50f9-130">Una condivisione è costituita da una serie di attributi:</span><span class="sxs-lookup"><span data-stu-id="e50f9-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="e50f9-131">**Nome condivisione**: un nome descrittivo che deve essere univoco e identifica la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-131">**Share Name** – A descriptive name that must be unique and helps identify the share.</span></span>
* <span data-ttu-id="e50f9-132">**Stato** : online oppure offline.</span><span class="sxs-lookup"><span data-stu-id="e50f9-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="e50f9-133">Se una condivisione è offline, gli utenti della condivisione non saranno in grado di accedervi.</span><span class="sxs-lookup"><span data-stu-id="e50f9-133">If a share is offline, users of the share will not be able to access it.</span></span>
* <span data-ttu-id="e50f9-134">**Tipo**: indica se la condivisione è **A livelli** (impostazione predefinita) o **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-134">**Type** – Indicates whether the share is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="e50f9-135">**Capacità**: specifica la quantità di dati usati rispetto alle quantità totale di dati che possono essere archiviati nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored on the share.</span></span>
* <span data-ttu-id="e50f9-136">**Descrizione**: impostazione facoltativa che consente di descrivere la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-136">**Description** – An optional setting that helps describe the share.</span></span>
* <span data-ttu-id="e50f9-137">**Autorizzazioni**: autorizzazioni NTFS per la condivisione che possono essere gestite tramite Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="e50f9-137">**Permissions** - The NTFS permissions to the share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="e50f9-138">**Backup**: nel caso dell'array virtuale StorSimple, tutte le condivisioni vengono abilitate automaticamente per il backup.</span><span class="sxs-lookup"><span data-stu-id="e50f9-138">**Backup** – In case of the StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Dettagli sulle condivisioni](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="e50f9-140">Usare le istruzioni di questa esercitazione per eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="e50f9-140">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="e50f9-141">Aggiungere una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-141">Add a share</span></span>
* <span data-ttu-id="e50f9-142">Modificare una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-142">Modify a share</span></span>
* <span data-ttu-id="e50f9-143">Portare offline una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-143">Take a share offline</span></span>
* <span data-ttu-id="e50f9-144">Eliminare una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="e50f9-145">Aggiungere una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-145">Add a share</span></span>

1. <span data-ttu-id="e50f9-146">Nel pannello di riepilogo servizio StorSimple fare clic su **+ Aggiungi condivisione** dalla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="e50f9-146">From the StorSimple service summary blade, click **+ Add share** from the command bar.</span></span> <span data-ttu-id="e50f9-147">Verrà visualizzato il pannello **Aggiungi condivisione**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-147">This opens up the **Add share** blade.</span></span>

    ![Aggiungere la condivisione](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="e50f9-149">Nel pannello **Aggiungi condivisione** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="e50f9-149">In the **Add share** blade, do the following:</span></span>
   
    1. <span data-ttu-id="e50f9-150">Nel campo **Nome della condivisione** immettere un nome univoco per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-150">In the **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="e50f9-151">Il nome deve essere una stringa contenente da 3 a 127 caratteri.</span><span class="sxs-lookup"><span data-stu-id="e50f9-151">The name must be a string that contains 3 to 127 characters.</span></span>

    2. <span data-ttu-id="e50f9-152">Una **Descrizione** facoltativa per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-152">An optional **Description** for the share.</span></span> <span data-ttu-id="e50f9-153">La descrizione consente di identificare i proprietari della condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-153">The description will help identify the share owners.</span></span>

    3. <span data-ttu-id="e50f9-154">Nell'elenco a discesa **Tipo** specificare se creare una condivisione **A livelli** o **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-154">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="e50f9-155">Per carichi di lavoro che richiedono garanzie locali, latenze basse e prestazioni di livello superiore, selezionare la condivisione **Aggiunto in locale**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="e50f9-156">Per tutti gli altri dati, selezionare una condivisone **A livelli** .</span><span class="sxs-lookup"><span data-stu-id="e50f9-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="e50f9-157">Nel campo **Capacità** specificare le dimensioni della condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-157">In the **Capacity** field, specify the size of the share.</span></span> <span data-ttu-id="e50f9-158">Una condivisione a livelli deve essere compresa tra 500 GB e 20 TB e una condivisione aggiunta in locale deve essere compresa tra 50 GB e 2 TB.</span><span class="sxs-lookup"><span data-stu-id="e50f9-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="e50f9-159">Nel campo **Set default full permissions to** (Imposta le autorizzazioni complete predefinite su) assegnare le autorizzazioni all'utente o al gruppo che avrà accesso a questa condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-159">In the **Set default full permissions to** field, assign the permissions to the user, or the group that is accessing this share.</span></span> <span data-ttu-id="e50f9-160">Specificare il nome dell'utente o del gruppo di utenti nel formato _john@contoso.com_.</span><span class="sxs-lookup"><span data-stu-id="e50f9-160">Specify the name of the user or the user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="e50f9-161">Si consiglia di usare un gruppo di utenti (anziché un singolo utente) per consentire ai privilegi amministratore di accedere a queste condivisioni.</span><span class="sxs-lookup"><span data-stu-id="e50f9-161">We recommend that you use a user group (instead of a single user) to allow admin privileges to access these shares.</span></span> <span data-ttu-id="e50f9-162">Dopo aver assegnato le autorizzazioni in questa fase, è possibile modificarle con Esplora file.</span><span class="sxs-lookup"><span data-stu-id="e50f9-162">After you have assigned the permissions here, you can then use File Explorer to modify these permissions.</span></span>
3. <span data-ttu-id="e50f9-163">Al termine della configurazione della condivisione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="e50f9-164">Verrà creata una condivisione con le impostazioni specificate e verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="e50f9-164">A share will be created with the specified settings and you will see a notification.</span></span> <span data-ttu-id="e50f9-165">Per impostazione predefinita, il backup verrà abilitato per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-165">By default, backup will be enabled for the share.</span></span>
4. <span data-ttu-id="e50f9-166">Per verificare che la condivisione sia stata creata, passare al pannello **Condivisioni**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-166">To confirm that the share was successfully created, go to the **Shares** blade.</span></span> <span data-ttu-id="e50f9-167">La condivisione viene visualizzata nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="e50f9-167">You should see the share listed.</span></span>
   
    ![Creazione della condivisione completata](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="e50f9-169">Modificare una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-169">Modify a share</span></span>

<span data-ttu-id="e50f9-170">Modificare una condivisione quando è necessario modificarne la descrizione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-170">Modify a share when you need to change the description of the share.</span></span> <span data-ttu-id="e50f9-171">Dopo la creazione della condivisione, non è possibile modificare nessuna altra proprietà della condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-171">No other share properties can be modified once the share is created.</span></span>

#### <a name="to-modify-a-share"></a><span data-ttu-id="e50f9-172">Per modificare una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-172">To modify a share</span></span>

1. <span data-ttu-id="e50f9-173">Nell'impostazione **Condivisioni** del pannello di riepilogo servizio StorSimple selezionare l'array virtuale in cui risiede la condivisione da modificare.</span><span class="sxs-lookup"><span data-stu-id="e50f9-173">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to modify resides.</span></span>
2. <span data-ttu-id="e50f9-174">**Selezionare** la condivisione per visualizzare e modificare la descrizione corrente.</span><span class="sxs-lookup"><span data-stu-id="e50f9-174">**Select** the share to view the current description and modify it.</span></span>
3. <span data-ttu-id="e50f9-175">Salvare le modifiche facendo clic sulla barra di comando **Salva**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-175">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="e50f9-176">Verranno applicate le impostazioni specificate e verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="e50f9-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="e50f9-177">Modificare la condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="e50f9-178">Portare offline una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-178">Take a share offline</span></span>

<span data-ttu-id="e50f9-179">Potrebbe essere necessario portare una condivisione offline per modificarla o eliminarla.</span><span class="sxs-lookup"><span data-stu-id="e50f9-179">You may need to take a share offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="e50f9-180">Quando una condivisione è offline, non è disponibile per l'accesso in lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="e50f9-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="e50f9-181">È necessario portare offline la condivisione sull'host e sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e50f9-181">You will need to take the share offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-share-offline"></a><span data-ttu-id="e50f9-182">Per portare offline una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-182">To take a share offline</span></span>

1. <span data-ttu-id="e50f9-183">Assicurarsi che la condivisione in questione non sia in uso prima di portarla offline.</span><span class="sxs-lookup"><span data-stu-id="e50f9-183">Make sure that the share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="e50f9-184">Portare offline la condivisione dell'array attenendosi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e50f9-184">Take the share on the array offline by performing the following steps:</span></span>
   
    1. <span data-ttu-id="e50f9-185">Nell'impostazione **Condivisioni** del pannello di riepilogo servizio StorSimple selezionare l'array virtuale in cui risiede la condivisione da portare offline.</span><span class="sxs-lookup"><span data-stu-id="e50f9-185">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish you to take offline resides.</span></span>

    2. <span data-ttu-id="e50f9-186">**Selezionare** la condivisione e fare clic su **...** (in alternativa fare clic con il pulsante destro del mouse su questa riga) e selezionare **Porta offline** nel menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="e50f9-186">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Condivisione offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="e50f9-188">Esaminare le informazioni nel pannello **Porta offline** e confermare l'accettazione dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-188">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="e50f9-189">Fare clic su **Porta offline** per portare offilne la condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-189">Click **Take offline** to take the share offline.</span></span> <span data-ttu-id="e50f9-190">Verrà visualizzata una notifica dell'operazione in corso.</span><span class="sxs-lookup"><span data-stu-id="e50f9-190">You will see a notification of the operation in progress.</span></span>

    4. <span data-ttu-id="e50f9-191">Per verificare che la condivisione sia stata portata offline, passare al pannello **Condivisioni**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-191">To confirm that the share was successfully taken offline, go to the **Shares** blade.</span></span> <span data-ttu-id="e50f9-192">Lo stato della condivisione dovrebbe essere offline.</span><span class="sxs-lookup"><span data-stu-id="e50f9-192">You should see the status of the share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="e50f9-193">Eliminare una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e50f9-194">È possibile eliminare una condivisione solo se è offline.</span><span class="sxs-lookup"><span data-stu-id="e50f9-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="e50f9-195">Completare la procedura seguente per eliminare una condivisione.</span><span class="sxs-lookup"><span data-stu-id="e50f9-195">Complete the following steps to delete a share.</span></span>

#### <a name="to-delete-a-share"></a><span data-ttu-id="e50f9-196">Per eliminare una condivisione</span><span class="sxs-lookup"><span data-stu-id="e50f9-196">To delete a share</span></span>

1. <span data-ttu-id="e50f9-197">Nell'impostazione **Condivisioni** del pannello di riepilogo servizio StorSimple selezionare l'array virtuale in cui risiede la condivisione da eliminare.</span><span class="sxs-lookup"><span data-stu-id="e50f9-197">From the **Shares** setting on the StorSimple service summary blade, select the virtual array on which the share you wish to delete resides.</span></span>
2. <span data-ttu-id="e50f9-198">**Selezionare** la condivisione e fare clic su **...** (in alternativa fare clic con il pulsante destro del mouse su questa riga) e selezionare **Elimina** nel menu di scelta rapida.</span><span class="sxs-lookup"><span data-stu-id="e50f9-198">**Select** the share and Click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Eliminare la condivisione](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="e50f9-200">Verificare lo stato della condivisione che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="e50f9-200">Check the status of the share you want to delete.</span></span> <span data-ttu-id="e50f9-201">Se la condivisione da eliminare non è offline, portarla prima offline.</span><span class="sxs-lookup"><span data-stu-id="e50f9-201">If the share you want to delete is not offline, take it offline first.</span></span> <span data-ttu-id="e50f9-202">Seguire la procedura illustrata in [Portare offline una condivisione](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="e50f9-202">Follow the steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="e50f9-203">Alla richiesta di conferma nel pannello **Elimina** accettare la conferma e fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="e50f9-203">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="e50f9-204">Verrà eliminata la condivisione; il pannello **Condivisioni** mostra l'elenco aggiornato delle condivisioni all'interno dell'array virtuale.</span><span class="sxs-lookup"><span data-stu-id="e50f9-204">The share will now be deleted and the **Shares** blade shows the updated list of shares within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e50f9-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e50f9-205">Next steps</span></span>
<span data-ttu-id="e50f9-206">Informazioni su come [clonare una condivisione StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="e50f9-206">Learn how to [clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

