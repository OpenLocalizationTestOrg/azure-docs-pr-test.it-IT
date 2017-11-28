---
title: record di controllo di accesso aaaManage in StorSimple | Documenti Microsoft
description: Viene descritto come il controllo di accesso toouse registra toodetermine (ACR) quali host possono connettersi tooa volume nel dispositivo StorSimple hello.
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
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="26315-103">Utilizzare i record di controllo accesso toomanage servizio StorSimple Manager hello</span><span class="sxs-lookup"><span data-stu-id="26315-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="26315-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="26315-104">Overview</span></span>
<span data-ttu-id="26315-105">Record di controllo di accesso (ACR) consentono di toospecify quali host possono connettersi tooa volume nel dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="26315-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="26315-106">ACR impostati volume specifico tooa e contenere hello iSCSI nomi completi (nomi iqn) degli host hello.</span><span class="sxs-lookup"><span data-stu-id="26315-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="26315-107">Quando un host tenta tooconnect tooa volume, il dispositivo hello controlla hello che ACR associata a tale volume nome IQN hello e, se viene trovata una corrispondenza, hello connessione.</span><span class="sxs-lookup"><span data-stu-id="26315-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="26315-108">record di controllo di accesso in hello Hello **configurazione** sezione del Pannello di servizio gestione di dispositivi StorSimple visualizzare tutti i record di controllo di accesso hello con hello nomi iqn degli host hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="26315-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="26315-109">In questa esercitazione illustra hello attività comuni correlate ai record di seguito:</span><span class="sxs-lookup"><span data-stu-id="26315-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="26315-110">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-110">Add an access control record</span></span>
* <span data-ttu-id="26315-111">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-111">Edit an access control record</span></span>
* <span data-ttu-id="26315-112">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="26315-113">Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="26315-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="26315-114">Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.</span><span class="sxs-lookup"><span data-stu-id="26315-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="26315-115">Ottenere hello IQN</span><span class="sxs-lookup"><span data-stu-id="26315-115">Get hello IQN</span></span>

<span data-ttu-id="26315-116">Eseguire hello seguendo i passaggi tooget hello nome qualificato iSCSI di un host Windows che esegue Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="26315-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="26315-117">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-117">Add an access control record</span></span>
<span data-ttu-id="26315-118">Utilizzare hello **configurazione** sezione nel servizio pannello tooadd ACR di hello dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="26315-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="26315-119">In genere, un record di controllo di accesso verrà associato a un volume.</span><span class="sxs-lookup"><span data-stu-id="26315-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="26315-120">Eseguire hello seguendo i passaggi tooadd un record.</span><span class="sxs-lookup"><span data-stu-id="26315-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="26315-121">un record tooadd</span><span class="sxs-lookup"><span data-stu-id="26315-121">tooadd an ACR</span></span>

1. <span data-ttu-id="26315-122">Il servizio di gestione di dispositivi StorSimple tooyour go, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="26315-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="26315-123">In hello **record di controllo di accesso** pannello, fare clic su **+ Aggiungi ACR**.</span><span class="sxs-lookup"><span data-stu-id="26315-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="26315-125">In hello **aggiungere ACR** pannello hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="26315-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="26315-126">Fornire un nome per il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="26315-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="26315-127">Specificare il nome IQN hello dell'host Windows Server in **nome iniziatore (IQN) iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="26315-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="26315-128">Fare clic su **Aggiungi** toocreate hello ACR.</span><span class="sxs-lookup"><span data-stu-id="26315-128">Click **Add** toocreate hello ACR.</span></span>

        ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="26315-130">Hello appena aggiunti che record verrà visualizzato nell'elenco in formato tabulare hello ACR.</span><span class="sxs-lookup"><span data-stu-id="26315-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Clic su Aggiungi record di controllo di accesso](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="26315-132">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-132">Edit an access control record</span></span>
<span data-ttu-id="26315-133">Utilizzare hello **configurazione** sezione nel servizio pannello tooedit ACR di hello dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="26315-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="26315-134">È consigliabile modificare solo i record di controllo di accesso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="26315-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="26315-135">tooedit che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.</span><span class="sxs-lookup"><span data-stu-id="26315-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="26315-136">Eseguire hello seguendo i passaggi tooedit un record.</span><span class="sxs-lookup"><span data-stu-id="26315-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="26315-137">tooedit un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="26315-138">Il servizio di gestione di dispositivi StorSimple tooyour go, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="26315-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="26315-140">Nell'elenco tabulare di hello dei record di controllo di accesso di hello, fare clic e selezionare i record che si desidera toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="26315-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="26315-142">In hello **record di controllo di accesso di modifica** pannello, fornire un diverso host tooanother IQN corrispondente.</span><span class="sxs-lookup"><span data-stu-id="26315-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="26315-144">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="26315-144">Click **Save**.</span></span> <span data-ttu-id="26315-145">Alla richiesta di conferma fare clic su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="26315-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Modificare i record di controllo di accesso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="26315-147">Ricevono una notifica quando viene aggiornata hello ACR.</span><span class="sxs-lookup"><span data-stu-id="26315-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="26315-148">Elenco tabulare Hello aggiorna anche modifica hello tooreflect.</span><span class="sxs-lookup"><span data-stu-id="26315-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="26315-149">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-149">Delete an access control record</span></span>
<span data-ttu-id="26315-150">Utilizzare hello **configurazione** sezione nel servizio pannello toodelete ACR di hello dispositivo StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="26315-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="26315-151">È possibile eliminare solo i record di controllo di acceso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="26315-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="26315-152">toodelete che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.</span><span class="sxs-lookup"><span data-stu-id="26315-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="26315-153">Eseguire hello seguendo i passaggi toodelete un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="26315-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="26315-154">toodelete un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="26315-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="26315-155">Il servizio di gestione di dispositivi StorSimple tooyour go, fare doppio clic sul servizio hello nome e quindi all'interno di hello **configurazione** fare clic su **record di controllo di accesso**.</span><span class="sxs-lookup"><span data-stu-id="26315-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="26315-157">Nell'elenco tabulare di hello dei record di controllo di accesso di hello, fare clic e selezionare i record che si desidera toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="26315-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="26315-159">Menu di scelta rapida tooinvoke hello e scegliere **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="26315-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="26315-161">Quando viene richiesta la conferma, esaminare le informazioni di hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="26315-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="26315-163">Ricevono una notifica al termine dell'eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="26315-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="26315-164">Elenco tabulare Hello è l'eliminazione di hello tooreflect aggiornato.</span><span class="sxs-lookup"><span data-stu-id="26315-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Passare tooaccess record di controllo](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="26315-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="26315-166">Next steps</span></span>
* <span data-ttu-id="26315-167">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="26315-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="26315-168">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="26315-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

