---
title: Gestire i record di controllo di accesso in StorSimple | Microsoft Docs
description: In questo articolo vengono descritti i record di controllo di accesso (ACR) che consentono di specificare quali host possono connettersi a un volume nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="65653-103">Utilizzare il servizio StorSimple Manager per gestire li record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="65653-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="65653-104">Overview</span></span>
<span data-ttu-id="65653-105">I record di controllo di accesso (ACR) consentono di specificare quali host possono connettersi a un volume nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65653-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="65653-106">I record di controllo di accesso vengono impostati su un volume specifico e contengono i nomi completi iSCSI (IQN) degli host.</span><span class="sxs-lookup"><span data-stu-id="65653-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="65653-107">Quando un host prova a connettersi a un volume, il dispositivo controlla il record di controllo di accesso associato a tale volume per l'IQN e, se esiste una corrispondenza, viene stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="65653-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="65653-108">I record di controllo di accesso nella sezione **Configurazione** del pannello del servizio Gestione dispositivi StorSimple visualizzano tutti i record di controllo di accesso con gli IQN corrispondenti degli host.</span><span class="sxs-lookup"><span data-stu-id="65653-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="65653-109">In questa esercitazione vengono illustrate le seguenti attività comuni correlate ai record di controllo di accesso:</span><span class="sxs-lookup"><span data-stu-id="65653-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="65653-110">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-110">Add an access control record</span></span>
* <span data-ttu-id="65653-111">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-111">Edit an access control record</span></span>
* <span data-ttu-id="65653-112">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="65653-113">Quando si assegna un record di controllo di accesso a un volume, fare attenzione che nel volume non abbiano effettuato l'accesso più di un host non cluster perché ciò potrebbe danneggiare il volume.</span><span class="sxs-lookup"><span data-stu-id="65653-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="65653-114">Quando si elimina un record di controllo di accesso da un volume, assicurarsi che l'host corrispondente non acceda al volume perché l'eliminazione potrebbe comportare un'interruzione di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="65653-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="65653-115">Ottenere il nome qualificato iSCSI</span><span class="sxs-lookup"><span data-stu-id="65653-115">Get the IQN</span></span>

<span data-ttu-id="65653-116">Eseguire i passaggi seguenti per ottenere il nome qualificato iSCSI di un host di Windows che esegue Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="65653-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="65653-117">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-117">Add an access control record</span></span>
<span data-ttu-id="65653-118">Per aggiungere record di controllo di accesso, usare la sezione **Configurazione** del pannello del servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65653-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="65653-119">In genere, un record di controllo di accesso verrà associato a un volume.</span><span class="sxs-lookup"><span data-stu-id="65653-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="65653-120">Attenersi alla seguente procedura per aggiungere un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="65653-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="65653-121">Per aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-121">To add an ACR</span></span>

1. <span data-ttu-id="65653-122">Nel servizio, fare doppio clic sul nome del servizio e nella sezione **Configurazione** fare clic su **Record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="65653-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="65653-123">Nel pannello **Record di controllo di accesso** fare clic su **+ Aggiungi record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="65653-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="65653-125">Nel pannello **Aggiungi record di controllo di accesso** attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="65653-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="65653-126">Fornire un nome per il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="65653-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="65653-127">In **Nome iniziatore iSCSI**, fornire l'IQN dell'host di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="65653-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="65653-128">Fare clic su **Aggiungi** per creare il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="65653-128">Click **Add** to create the ACR.</span></span>

        ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="65653-130">Il record di controllo di accesso appena aggiunto verrà visualizzato nel relativo elenco tabulare.</span><span class="sxs-lookup"><span data-stu-id="65653-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="65653-132">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-132">Edit an access control record</span></span>
<span data-ttu-id="65653-133">Per modificare i record di controllo di accesso, usare la sezione **Configurazione** del pannello del servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65653-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="65653-134">È consigliabile modificare solo i record di controllo di accesso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="65653-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="65653-135">Per modificare un record di controllo di accesso associato a un volume attualmente in uso, è innanzitutto necessario rendere il volume offline.</span><span class="sxs-lookup"><span data-stu-id="65653-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="65653-136">Seguire questa procedura per modificare un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="65653-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="65653-137">Per modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-137">To edit an access control record</span></span>
1.  <span data-ttu-id="65653-138">Nel servizio, fare doppio clic sul nome del servizio e nella sezione **Configurazione** fare clic su **Record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="65653-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Passare ai record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="65653-140">Nell'elenco tabulare dei record di controllo di accesso, fare clic e selezionare il record di controllo di accesso da modificare.</span><span class="sxs-lookup"><span data-stu-id="65653-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="65653-142">Nel pannello **Modifica record di controllo di accesso**, fornire un nome IQN diverso, corrispondente a un altro host.</span><span class="sxs-lookup"><span data-stu-id="65653-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="65653-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="65653-144">Click **Save**.</span></span> <span data-ttu-id="65653-145">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="65653-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="65653-147">Quando un record di controllo di accesso viene aggiornato l'utente riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="65653-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="65653-148">Anche l'elenco tabulare viene aggiornato per riflettere le modifiche.</span><span class="sxs-lookup"><span data-stu-id="65653-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="65653-149">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-149">Delete an access control record</span></span>
<span data-ttu-id="65653-150">Per eliminare i record di controllo di accesso, usare la sezione **Configurazione** del pannello del servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="65653-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="65653-151">È possibile eliminare solo i record di controllo di acceso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="65653-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="65653-152">Per eliminare un record di controllo di accesso associato a un volume attualmente in uso, è innanzitutto necessario rendere il volume offline.</span><span class="sxs-lookup"><span data-stu-id="65653-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="65653-153">Attenersi alla procedura seguente per eliminare un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="65653-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="65653-154">Per eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="65653-154">To delete an access control record</span></span>
1.  <span data-ttu-id="65653-155">Nel servizio, fare doppio clic sul nome del servizio e nella sezione **Configurazione** fare clic su **Record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="65653-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Passare ai record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="65653-157">Nell'elenco tabulare dei record di controllo di accesso, fare clic e selezionare il record di controllo di accesso da eliminare.</span><span class="sxs-lookup"><span data-stu-id="65653-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Passare ai record di controllo di accesso](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="65653-159">Fare clic con il pulsante destro del mouse per richiamare il menu di scelta rapida e quindi selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="65653-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Passare ai record di controllo di accesso](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="65653-161">Quando viene richiesta la conferma, esaminare le informazioni e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="65653-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Passare ai record di controllo di accesso](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="65653-163">Quando un record di controllo di accesso viene eliminato l'utente riceve una notifica.</span><span class="sxs-lookup"><span data-stu-id="65653-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="65653-164">L'elenco tabulare viene aggiornato per riflettere l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="65653-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Passare ai record di controllo di accesso](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="65653-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65653-166">Next steps</span></span>
* <span data-ttu-id="65653-167">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="65653-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="65653-168">Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="65653-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

