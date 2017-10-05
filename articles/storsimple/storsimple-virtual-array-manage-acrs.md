---
title: Gestire i record di controllo di accesso per l'array virtuale StorSimple | Documentazione Microsoft
description: In questo articolo viene descritto come gestire i record di controllo di accesso (ACR) che consentono di specificare quali host possono connettersi a un volume nell'array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2ce65aa4efba735305208f7a6d761bc2814d1b8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-to-manage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="82255-103">Usare Gestione dispositivi StorSimple per gestire i record di controllo di accesso per l'array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="82255-103">Use StorSimple Device Manager to manage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="82255-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="82255-104">Overview</span></span>

<span data-ttu-id="82255-105">I record di controllo di accesso (ACR) consentono di specificare quali host possono connettersi a un volume nell'array virtuale StorSimple (noto anche come dispositivo virtuale locale StorSimple).</span><span class="sxs-lookup"><span data-stu-id="82255-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple Virtual Array (also known as the StorSimple on-premises virtual device).</span></span> <span data-ttu-id="82255-106">I record di controllo di accesso vengono impostati su un volume specifico e contengono i nomi completi iSCSI (IQN) degli host.</span><span class="sxs-lookup"><span data-stu-id="82255-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="82255-107">Quando un host prova a connettersi a un volume, il dispositivo verifica il record di controllo di accesso associato a tale volume per il nome qualificato iSCSI e, se esiste una corrispondenza, viene stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="82255-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name, and if there is a match, then the connection is established.</span></span> <span data-ttu-id="82255-108">Nel pannello **Record di controllo di accesso** nella sezione **Configura** del servizio Gestione dispositivi vengono visualizzati tutti i record di controllo di accesso insieme agli IQN degli host.</span><span class="sxs-lookup"><span data-stu-id="82255-108">The **Access control records** blade within the **Configuration** section of your Device Manager service displays all the access control records with the corresponding IQNs of the hosts.</span></span>

![Gestire record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="82255-110">In questa esercitazione vengono illustrate le seguenti attività comuni correlate ai record di controllo di accesso:</span><span class="sxs-lookup"><span data-stu-id="82255-110">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="82255-111">Ottenere il nome qualificato iSCSI</span><span class="sxs-lookup"><span data-stu-id="82255-111">Get the IQN</span></span>
* <span data-ttu-id="82255-112">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-112">Add an access control record</span></span>
* <span data-ttu-id="82255-113">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-113">Edit an access control record</span></span>
* <span data-ttu-id="82255-114">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="82255-115">Quando si assegna un record di controllo di accesso a un volume, fare attenzione che nel volume non abbiano effettuato l'accesso più di un host non cluster perché ciò potrebbe danneggiare il volume.</span><span class="sxs-lookup"><span data-stu-id="82255-115">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="82255-116">Quando si elimina un record di controllo di accesso da un volume, assicurarsi che l'host corrispondente non acceda al volume perché l'eliminazione potrebbe comportare un'interruzione di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="82255-116">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


## <a name="get-the-iqn"></a><span data-ttu-id="82255-117">Ottenere il nome qualificato iSCSI</span><span class="sxs-lookup"><span data-stu-id="82255-117">Get the IQN</span></span>

<span data-ttu-id="82255-118">Eseguire i passaggi seguenti per ottenere il nome qualificato iSCSI di un host di Windows che esegue Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="82255-118">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="82255-119">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-119">Add an ACR</span></span>

<span data-ttu-id="82255-120">Usare il pannello **Record di controllo di accesso** nella sezione **Configurazione** del servizio Gestione dispositivi StorSimple per aggiungere record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-120">You use **Access control records** blade within the **Configuration** section of your StorSimple Device Manager service to add ACRs.</span></span> <span data-ttu-id="82255-121">In genere, a un volume viene associato un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="82255-122">Per informazioni sull'associazione di un record di controllo di accesso con un volume, vedere [Aggiungere un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="82255-122">For information about associating an ACR with a volume, go to [add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82255-123">Quando si assegna un record di controllo di accesso a un volume, fare attenzione che nel volume non abbiano effettuato l'accesso più di un host non cluster perché ciò potrebbe danneggiare il volume.</span><span class="sxs-lookup"><span data-stu-id="82255-123">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>


<span data-ttu-id="82255-124">Attenersi alla seguente procedura per aggiungere un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-124">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="82255-125">Per aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-125">To add an ACR</span></span>

1. <span data-ttu-id="82255-126">Nella pagina di destinazione del servizio selezionare il servizio, fare doppio clic sul nome del servizio e nella sezione **Configurazione** fare clic su **Record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="82255-126">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="82255-127">Nel pannello **Record di controllo di accesso** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="82255-127">In the **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="82255-128">Nel pannello **Aggiungi record di controllo di accesso** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="82255-128">In the **Add ACR** blade, do the following:</span></span>
   
    1. <span data-ttu-id="82255-129">Fornire un **Nome** per l'ACR.</span><span class="sxs-lookup"><span data-stu-id="82255-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="82255-130">In **Nome iniziatore iSCSI**fornire il nome qualificato iSCSI dell'host di Windows.</span><span class="sxs-lookup"><span data-stu-id="82255-130">Under **iSCSI Initiator Name**, provide the IQN name of your Windows host.</span></span> <span data-ttu-id="82255-131">Per ottenere l'IQN dell'host di Windows Server, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="82255-131">To get the IQN of your Windows Server host, do the following:</span></span>
   
    3. <span data-ttu-id="82255-132">Avviare l'iniziatore iSCSI di Microsoft sull’host di Windows.</span><span class="sxs-lookup"><span data-stu-id="82255-132">Start the Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="82255-133">Nella scheda **Configurazione** della finestra delle proprietà dell'iniziatore iSCSI selezionare e copiare la stringa dal campo **Nome iniziatore**.</span><span class="sxs-lookup"><span data-stu-id="82255-133">In the iSCSI Initiator Properties window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
    <span data-ttu-id="82255-134">Incollare questa stringa nel campo **IQN** nel pannello **Aggiungi record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="82255-134">Paste this string in the **IQN** field in the **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="82255-135">Fare clic su **Aggiungi** per aggiungere il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-135">Click **Add** to add the ACR.</span></span>  
   
        ![Aggiungere record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="82255-137">L'elenco tabulare viene aggiornato per riflettere questa aggiunta.</span><span class="sxs-lookup"><span data-stu-id="82255-137">The tabular listing is updated to reflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="82255-138">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-138">Edit an ACR</span></span>

<span data-ttu-id="82255-139">Usare il pannello **Record di controllo di accesso** nella sezione **Configurazione** del servizio Gestione dispositivi nel portale di Azure per modificare i record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-139">You use the **Access control records** blade within the **Configuration** section of your Device Manager service in the Azure portal to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="82255-140">Non è opportuno modificare un record di controllo di accesso attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="82255-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="82255-141">Per modificare un record di controllo di accesso associato a un volume attualmente in uso, è innanzitutto necessario rendere il volume offline.</span><span class="sxs-lookup"><span data-stu-id="82255-141">To edit an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>


<span data-ttu-id="82255-142">Seguire questa procedura per modificare un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-142">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-acr"></a><span data-ttu-id="82255-143">Per modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-143">To edit an ACR</span></span>

1. <span data-ttu-id="82255-144">Nella pagina di destinazione del servizio selezionare il servizio, fare doppio clic sul nome del servizio e nella sezione **Configurazione** fare clic su **Record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="82255-144">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="82255-145">Nell'elenco tabulare dei record di controllo di accesso nel pannello **Record di controllo di accesso** fare doppio clic sul record di controllo di accesso che si vuole modificare.</span><span class="sxs-lookup"><span data-stu-id="82255-145">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="82255-146">Nel pannello **Modifica record di controllo di accesso** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="82255-146">In the **Edit access control records** blade, do the following:</span></span>
   
    1. <span data-ttu-id="82255-147">Fornire il nome qualificato ISCSI per il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-147">Supply the IQN for the ACR.</span></span>
   
    2. <span data-ttu-id="82255-148">Fare clic su **Salva** nella parte superiore del pannello per salvare il record di controllo di accesso modificato.</span><span class="sxs-lookup"><span data-stu-id="82255-148">Click **Save** at the top of the blade to save the modified ACR.</span></span> <span data-ttu-id="82255-149">Viene visualizzato il messaggio di conferma seguente:</span><span class="sxs-lookup"><span data-stu-id="82255-149">You see the following confirmation message:</span></span>
   
        ![Modificare i record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="82255-151">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-151">Delete an access control record</span></span>

<span data-ttu-id="82255-152">Per eliminare record di controllo di accesso, usare la pagina **Configurazione** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="82255-152">You use the **Configuration** page in the Azure portal to delete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="82255-153">Non è opportuno eliminare un record di controllo di accesso attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="82255-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="82255-154">Per eliminare un record di controllo di accesso associato a un volume attualmente in uso, è innanzitutto necessario rendere il volume offline.</span><span class="sxs-lookup"><span data-stu-id="82255-154">To delete an ACR associated with a volume that is currently in use, you should first take the volume offline.</span></span>
> * <span data-ttu-id="82255-155">Quando si elimina un record di controllo di accesso da un volume, assicurarsi che l'host corrispondente non acceda al volume perché l'eliminazione potrebbe comportare un'interruzione di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="82255-155">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="82255-156">Attenersi alla procedura seguente per eliminare un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="82255-156">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="82255-157">Per eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="82255-157">To delete an access control record</span></span>

1. <span data-ttu-id="82255-158">Nella pagina di destinazione del servizio selezionare il servizio, fare doppio clic sul nome del servizio e nella sezione **Configurazione** fare clic su **Record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="82255-158">On the service landing page, select your service, double-click the service name, and then within the **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="82255-159">Nell'elenco tabulare dei record di controllo di accesso nel pannello **Record di controllo di accesso** fare doppio clic sul record di controllo di accesso che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="82255-159">In the **Access control records** blade, from the tabular listing of the access control records, double-click the ACR that you wish to delete.</span></span>

3. <span data-ttu-id="82255-160">Nel pannello Modifica record di controllo di accesso fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="82255-160">In the Edit access control records blade, click **Delete**.</span></span>
   
    ![Eliminare record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="82255-162">Quando viene richiesta la conferma, fare clic su **Elimina** per continuare con l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="82255-162">When prompted for confirmation, click **Delete** to continue with the deletion.</span></span> <span data-ttu-id="82255-163">L'elenco tabulare viene aggiornato per riflettere l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="82255-163">The tabular listing is updated to reflect the deletion.</span></span>
   
   ![Messaggio di avviso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="82255-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="82255-165">Next steps</span></span>

* <span data-ttu-id="82255-166">Altre informazioni sull' [aggiunta di volumi e la configurazione di record di controllo di accesso](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="82255-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

