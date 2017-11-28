---
title: record di controllo di accesso aaaManage in StorSimple | Documenti Microsoft
description: Viene descritto come il controllo di accesso toouse registra toodetermine (ACR) quali host possono connettersi tooa volume nel dispositivo StorSimple hello.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="2680b-103">Utilizzare i record di controllo accesso toomanage servizio StorSimple Manager hello</span><span class="sxs-lookup"><span data-stu-id="2680b-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="2680b-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2680b-104">Overview</span></span>
<span data-ttu-id="2680b-105">Record di controllo di accesso (ACR) consentono di toospecify quali host possono connettersi tooa volume nel dispositivo StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="2680b-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="2680b-106">ACR impostati volume specifico tooa e contenere hello iSCSI nomi completi (nomi iqn) degli host hello.</span><span class="sxs-lookup"><span data-stu-id="2680b-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="2680b-107">Quando un host tenta tooconnect tooa volume, il dispositivo hello controlla hello che ACR associata a tale volume nome IQN hello e, se viene trovata una corrispondenza, hello connessione.</span><span class="sxs-lookup"><span data-stu-id="2680b-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="2680b-108">sezione in hello dei record di controllo di accesso Hello **configura** pagina siano presenti tutti i record di controllo di accesso hello hello nomi iqn degli host hello corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2680b-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="2680b-109">In questa esercitazione illustra hello attività comuni correlate ai record di seguito:</span><span class="sxs-lookup"><span data-stu-id="2680b-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="2680b-110">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-110">Add an access control record</span></span> 
* <span data-ttu-id="2680b-111">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-111">Edit an access control record</span></span> 
* <span data-ttu-id="2680b-112">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="2680b-113">Quando si assegna un volume tooa ACR, prestare attenzione che hello volume non è accedano contemporaneamente da più di un host non in cluster perché si potrebbe danneggiare il volume di hello.</span><span class="sxs-lookup"><span data-stu-id="2680b-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="2680b-114">Quando si elimina un record da un volume, assicurarsi che tale host corrispondente hello non accedono al volume hello perché hello eliminazione potrebbe comportare un'interruzione di lettura / scrittura.</span><span class="sxs-lookup"><span data-stu-id="2680b-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="2680b-115">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-115">Add an access control record</span></span>
<span data-ttu-id="2680b-116">Utilizzare un servizio StorSimple Manager hello **configura** pagina ACR tooadd.</span><span class="sxs-lookup"><span data-stu-id="2680b-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="2680b-117">In genere, un record di controllo di accesso verrà associato a un volume.</span><span class="sxs-lookup"><span data-stu-id="2680b-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="2680b-118">Eseguire hello seguendo i passaggi tooadd un record.</span><span class="sxs-lookup"><span data-stu-id="2680b-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="2680b-119">tooadd un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-119">tooadd an access control record</span></span>
1. <span data-ttu-id="2680b-120">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="2680b-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="2680b-121">In hello tabulare visualizzata in **record di controllo di accesso**, fornire un **nome** del record.</span><span class="sxs-lookup"><span data-stu-id="2680b-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="2680b-122">Specificare il nome IQN hello dell'host di Windows in **nome iniziatore iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="2680b-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="2680b-123">hello tooget hello IQN dell'host, Windows Server seguenti:</span><span class="sxs-lookup"><span data-stu-id="2680b-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="2680b-124">Avviare l'iniziatore iSCSI Microsoft di hello nell'host di Windows.</span><span class="sxs-lookup"><span data-stu-id="2680b-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="2680b-125">In hello **iniziatore iSCSI-proprietà** finestra hello **configurazione** , selezionare e copiare la stringa hello hello **nome iniziatore** campo.</span><span class="sxs-lookup"><span data-stu-id="2680b-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="2680b-126">Incollare la stringa hello **nome iniziatore iSCSI** campo nella tabella ACR hello hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="2680b-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="2680b-127">Fare clic su **salvare** hello toosave nuovi record.</span><span class="sxs-lookup"><span data-stu-id="2680b-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="2680b-128">Hello tabulare elenco verrà aggiornato tooreflect di essere aggiunta.</span><span class="sxs-lookup"><span data-stu-id="2680b-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="2680b-129">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-129">Edit an access control record</span></span>
<span data-ttu-id="2680b-130">Utilizzare hello **configura** pagina hello ACR Azure tooedit portale classico.</span><span class="sxs-lookup"><span data-stu-id="2680b-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="2680b-131">È possibile modificare solo i record di controllo di acceso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="2680b-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="2680b-132">tooedit che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.</span><span class="sxs-lookup"><span data-stu-id="2680b-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="2680b-133">Eseguire hello seguendo i passaggi tooedit un record.</span><span class="sxs-lookup"><span data-stu-id="2680b-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="2680b-134">tooedit un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-134">tooedit an access control record</span></span>
1. <span data-ttu-id="2680b-135">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="2680b-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="2680b-136">Nell'elenco tabulare di hello dei record di controllo di accesso di hello, passare il mouse sul record che si desidera toomodify hello.</span><span class="sxs-lookup"><span data-stu-id="2680b-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="2680b-137">Specificare un nuovo nome e/o il nome IQN hello ACR.</span><span class="sxs-lookup"><span data-stu-id="2680b-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="2680b-138">Fare clic su **salvare** toosave hello modificato ACR.</span><span class="sxs-lookup"><span data-stu-id="2680b-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="2680b-139">Hello tabulare elenco verrà aggiornato tooreflect di essere questa modifica.</span><span class="sxs-lookup"><span data-stu-id="2680b-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="2680b-140">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-140">Delete an access control record</span></span>
<span data-ttu-id="2680b-141">Utilizzare hello **configura** pagina hello ACR Azure toodelete portale classico.</span><span class="sxs-lookup"><span data-stu-id="2680b-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="2680b-142">È possibile eliminare solo i record di controllo di acceso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="2680b-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="2680b-143">toodelete che un record associato a un volume che è attualmente in uso, è necessario innanzitutto portare hello volume offline.</span><span class="sxs-lookup"><span data-stu-id="2680b-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="2680b-144">Eseguire hello seguendo i passaggi toodelete un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="2680b-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="2680b-145">toodelete un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="2680b-145">toodelete an access control record</span></span>
1. <span data-ttu-id="2680b-146">Nella pagina di destinazione del servizio hello, selezionare il servizio, fare doppio clic sul nome del servizio hello e quindi fare clic su hello **configura** scheda.</span><span class="sxs-lookup"><span data-stu-id="2680b-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="2680b-147">Nell'elenco tabulare di hello dei record di controllo di accesso hello (ACR), passare il mouse sul record che si desidera toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="2680b-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="2680b-148">Un'icona di eliminazione (**x**) verrà visualizzato nella colonna destra estrema hello per hello record selezionato.</span><span class="sxs-lookup"><span data-stu-id="2680b-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="2680b-149">Fare clic su hello **x** hello toodelete icona record.</span><span class="sxs-lookup"><span data-stu-id="2680b-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="2680b-150">Quando viene richiesta la conferma, fare clic su **Sì** toocontinue con l'eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="2680b-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="2680b-151">Elenco tabulare Hello sarà aggiornata tooreflect hello eliminazione.</span><span class="sxs-lookup"><span data-stu-id="2680b-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2680b-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2680b-152">Next steps</span></span>
* <span data-ttu-id="2680b-153">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="2680b-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="2680b-154">Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2680b-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

