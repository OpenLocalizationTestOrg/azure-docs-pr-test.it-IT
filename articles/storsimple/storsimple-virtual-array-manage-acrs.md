---
title: record di controllo di accesso aaaManage per Array virtuale StorSimple | Documenti Microsoft
description: Viene descritto come il controllo di accesso toomanage registra toodetermine (ACR) quali host possono connettersi volume tooa hello Array virtuale StorSimple.
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
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="e90fe-103">Utilizzare Gestione periferiche di StorSimple toomanage record di controllo di accesso per Array virtuale StorSimple</span><span class="sxs-lookup"><span data-stu-id="e90fe-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="e90fe-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e90fe-104">Overview</span></span>

<span data-ttu-id="e90fe-105">Record di controllo di accesso (ACR) consentono di toospecify quali host possono connettersi volume tooa hello Array virtuale StorSimple (noto anche come hello StorSimple nel dispositivo virtuale locale).</span><span class="sxs-lookup"><span data-stu-id="e90fe-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="e90fe-106">ACR impostati volume specifico tooa e contenere hello iSCSI nomi completi (nomi iqn) degli host hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="e90fe-107">Quando un host tenta tooconnect tooa volume, il dispositivo hello controlla hello ACR associata a tale volume per il nome IQN hello e se viene trovata una corrispondenza, viene stabilita la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="e90fe-108">Hello **record di controllo di accesso** pannello all'interno di hello **configurazione** sezione del servizio di gestione dispositivi consente di visualizzare tutti i record di controllo di accesso hello con hello nomi iqn degli host hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e90fe-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Gestire record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="e90fe-110">In questa esercitazione illustra hello attività comuni correlate ai record di seguito:</span><span class="sxs-lookup"><span data-stu-id="e90fe-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="e90fe-111">Ottenere hello IQN</span><span class="sxs-lookup"><span data-stu-id="e90fe-111">Get hello IQN</span></span>
* <span data-ttu-id="e90fe-112">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-112">Add an access control record</span></span>
* <span data-ttu-id="e90fe-113">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-113">Edit an access control record</span></span>
* <span data-ttu-id="e90fe-114">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="e90fe-115">Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="e90fe-116">Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.</span><span class="sxs-lookup"><span data-stu-id="e90fe-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="e90fe-117">Ottenere hello IQN</span><span class="sxs-lookup"><span data-stu-id="e90fe-117">Get hello IQN</span></span>

<span data-ttu-id="e90fe-118">Eseguire hello seguendo i passaggi tooget hello nome qualificato iSCSI di un host Windows che esegue Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="e90fe-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="e90fe-119">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-119">Add an ACR</span></span>

<span data-ttu-id="e90fe-120">Utilizzare **record di controllo di accesso** pannello all'interno di hello **configurazione** sezione tooadd di servizio ACR il dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="e90fe-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="e90fe-121">In genere, a un volume viene associato un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="e90fe-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="e90fe-122">Per informazioni sull'associazione di un record con un volume, andare troppo[aggiungere un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="e90fe-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e90fe-123">Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="e90fe-124">Eseguire hello seguendo i passaggi tooadd un record.</span><span class="sxs-lookup"><span data-stu-id="e90fe-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="e90fe-125">un record tooadd</span><span class="sxs-lookup"><span data-stu-id="e90fe-125">tooadd an ACR</span></span>

1. <span data-ttu-id="e90fe-126">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="e90fe-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="e90fe-127">In hello **record di controllo di accesso** pannello, fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="e90fe-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="e90fe-128">In hello **aggiungere ACR** pannello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e90fe-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="e90fe-129">Fornire un **Nome** per l'ACR.</span><span class="sxs-lookup"><span data-stu-id="e90fe-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="e90fe-130">In **nome iniziatore iSCSI**, fornire il nome IQN hello dell'host Windows.</span><span class="sxs-lookup"><span data-stu-id="e90fe-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="e90fe-131">hello tooget hello IQN dell'host, Windows Server seguenti:</span><span class="sxs-lookup"><span data-stu-id="e90fe-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="e90fe-132">Avviare l'iniziatore iSCSI Microsoft di hello nell'host di Windows.</span><span class="sxs-lookup"><span data-stu-id="e90fe-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="e90fe-133">Nella finestra Proprietà iniziatore iSCSI di hello, su hello **configurazione** , selezionare e copiare la stringa hello hello **nome iniziatore** campo.</span><span class="sxs-lookup"><span data-stu-id="e90fe-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="e90fe-134">Incollare la stringa hello **IQN** campo hello **aggiungere ACR** blade.</span><span class="sxs-lookup"><span data-stu-id="e90fe-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="e90fe-135">Fare clic su **Aggiungi** tooadd hello ACR.</span><span class="sxs-lookup"><span data-stu-id="e90fe-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Aggiungere record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="e90fe-137">Elenco tabulare Hello viene aggiornato tooreflect questa aggiunta.</span><span class="sxs-lookup"><span data-stu-id="e90fe-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="e90fe-138">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-138">Edit an ACR</span></span>

<span data-ttu-id="e90fe-139">Utilizzare hello **record di controllo di accesso** pannello all'interno di hello **configurazione** sezione del servizio di Gestione periferiche in hello ACR tooedit portale Azure.</span><span class="sxs-lookup"><span data-stu-id="e90fe-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="e90fe-140">Non è opportuno modificare un record di controllo di accesso attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="e90fe-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="e90fe-141">tooedit che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.</span><span class="sxs-lookup"><span data-stu-id="e90fe-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="e90fe-142">Eseguire hello seguendo i passaggi tooedit un record.</span><span class="sxs-lookup"><span data-stu-id="e90fe-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="e90fe-143">un record tooedit</span><span class="sxs-lookup"><span data-stu-id="e90fe-143">tooedit an ACR</span></span>

1. <span data-ttu-id="e90fe-144">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** sezione **record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="e90fe-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="e90fe-145">In hello **record di controllo di accesso** pannello, dall'elenco in formato tabulare hello dei record di controllo di accesso hello, fare doppio clic sul record che si desidera toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="e90fe-146">In hello **record di controllo di accesso di modifica** pannello hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="e90fe-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="e90fe-147">Alimentatore hello IQN per hello ACR.</span><span class="sxs-lookup"><span data-stu-id="e90fe-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="e90fe-148">Fare clic su **salvare** nella parte superiore di hello di hello pannello toosave hello modificato ACR.</span><span class="sxs-lookup"><span data-stu-id="e90fe-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="e90fe-149">Vedrai hello messaggio di conferma seguente:</span><span class="sxs-lookup"><span data-stu-id="e90fe-149">You see hello following confirmation message:</span></span>
   
        ![Modificare i record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="e90fe-151">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-151">Delete an access control record</span></span>

<span data-ttu-id="e90fe-152">Utilizzare hello **configurazione** pagina hello ACR toodelete portale Azure.</span><span class="sxs-lookup"><span data-stu-id="e90fe-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="e90fe-153">Non è opportuno eliminare un record di controllo di accesso attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="e90fe-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="e90fe-154">toodelete che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.</span><span class="sxs-lookup"><span data-stu-id="e90fe-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="e90fe-155">Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.</span><span class="sxs-lookup"><span data-stu-id="e90fe-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="e90fe-156">Eseguire hello seguendo i passaggi toodelete un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="e90fe-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="e90fe-157">toodelete un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="e90fe-157">toodelete an access control record</span></span>

1. <span data-ttu-id="e90fe-158">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** sezione **record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="e90fe-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="e90fe-159">In hello **record di controllo di accesso** pannello, dall'elenco in formato tabulare hello dei record di controllo di accesso hello, fare doppio clic sul record che si desidera toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="e90fe-160">Nel Pannello di hello Modifica accesso controllo record, fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="e90fe-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![Eliminare record di controllo di accesso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="e90fe-162">Quando viene richiesta la conferma, fare clic su **eliminare** toocontinue con l'eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="e90fe-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="e90fe-163">Elenco tabulare Hello è l'eliminazione di hello tooreflect aggiornato.</span><span class="sxs-lookup"><span data-stu-id="e90fe-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Messaggio di avviso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="e90fe-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e90fe-165">Next steps</span></span>

* <span data-ttu-id="e90fe-166">Altre informazioni sull' [aggiunta di volumi e la configurazione di record di controllo di accesso](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="e90fe-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

