---
title: Gestire i record di controllo di accesso in StorSimple | Microsoft Docs
description: In questo articolo vengono descritti i record di controllo di accesso (ACR) che consentono di specificare quali host possono connettersi a un volume nel dispositivo StorSimple.
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
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="08df3-103">Utilizzare il servizio StorSimple Manager per gestire li record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="08df3-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="08df3-104">Overview</span></span>
<span data-ttu-id="08df3-105">I record di controllo di accesso (ACR) consentono di specificare quali host possono connettersi a un volume nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="08df3-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="08df3-106">I record di controllo di accesso vengono impostati su un volume specifico e contengono i nomi completi iSCSI (IQN) degli host.</span><span class="sxs-lookup"><span data-stu-id="08df3-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="08df3-107">Quando un host prova a connettersi a un volume, il dispositivo controlla il record di controllo di accesso associato a tale volume per l'IQN e, se esiste una corrispondenza, viene stabilita la connessione.</span><span class="sxs-lookup"><span data-stu-id="08df3-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="08df3-108">Nella sezione dei record di controllo di accesso nella pagina **Configura** vengono visualizzati tutti i record di controllo di accesso insieme agli IQN degli host.</span><span class="sxs-lookup"><span data-stu-id="08df3-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="08df3-109">In questa esercitazione vengono illustrate le seguenti attività comuni correlate ai record di controllo di accesso:</span><span class="sxs-lookup"><span data-stu-id="08df3-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="08df3-110">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-110">Add an access control record</span></span> 
* <span data-ttu-id="08df3-111">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-111">Edit an access control record</span></span> 
* <span data-ttu-id="08df3-112">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="08df3-113">Quando si assegna un record di controllo di accesso a un volume, fare attenzione che nel volume non abbiano effettuato l'accesso più di un host non cluster perché ciò potrebbe danneggiare il volume.</span><span class="sxs-lookup"><span data-stu-id="08df3-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="08df3-114">Quando si elimina un record di controllo di accesso da un volume, assicurarsi che l'host corrispondente non acceda al volume perché l'eliminazione potrebbe comportare un'interruzione di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="08df3-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="08df3-115">Aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-115">Add an access control record</span></span>
<span data-ttu-id="08df3-116">Si utilizza la pagina **Configura** del servizio StorSimple Manager per aggiungere record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="08df3-117">In genere, un record di controllo di accesso verrà associato a un volume.</span><span class="sxs-lookup"><span data-stu-id="08df3-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="08df3-118">Attenersi alla seguente procedura per aggiungere un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="08df3-119">Per aggiungere un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-119">To add an access control record</span></span>
1. <span data-ttu-id="08df3-120">Nella pagina di destinazione del servizio, selezionare il servizio, fare doppio clic sul nome del servizio, quindi fare clic sulla scheda **Configura** .</span><span class="sxs-lookup"><span data-stu-id="08df3-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="08df3-121">Nell'elenco tabulare in **Record di controllo di accesso** fornire un **nome** per il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="08df3-122">In **Nome iniziatore iSCSI**, fornire l'IQN dell'host di Windows.</span><span class="sxs-lookup"><span data-stu-id="08df3-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="08df3-123">Per ottenere l'IQN dell'host di Windows Server, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="08df3-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="08df3-124">Avviare l'iniziatore iSCSI di Microsoft sull’host di Windows.</span><span class="sxs-lookup"><span data-stu-id="08df3-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="08df3-125">Nella scheda **Configurazione** della finestra delle **proprietà dell'iniziatore iSCSI** selezionare e copiare la stringa dal campo **Nome iniziatore**.</span><span class="sxs-lookup"><span data-stu-id="08df3-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="08df3-126">Incollare la stringa nel campo **Nome iniziatore iSCSI** nella tabella dei record di controllo di accesso nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="08df3-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="08df3-127">Fare clic su **Salva** per salvare il record di controllo di accesso appena creato.</span><span class="sxs-lookup"><span data-stu-id="08df3-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="08df3-128">L'elenco tabulare verrà aggiornato per riflettere questa aggiunta.</span><span class="sxs-lookup"><span data-stu-id="08df3-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="08df3-129">Modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-129">Edit an access control record</span></span>
<span data-ttu-id="08df3-130">Per modificare record di controllo di accesso, utilizzare la pagina **Configura** nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="08df3-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="08df3-131">È possibile modificare solo i record di controllo di acceso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="08df3-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="08df3-132">Per modificare un record di controllo di accesso associato a un volume attualmente in uso, è innanzitutto necessario rendere il volume offline.</span><span class="sxs-lookup"><span data-stu-id="08df3-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="08df3-133">Seguire questa procedura per modificare un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="08df3-134">Per modificare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-134">To edit an access control record</span></span>
1. <span data-ttu-id="08df3-135">Nella pagina di destinazione del servizio, selezionare il servizio, fare doppio clic sul nome del servizio, quindi fare clic sulla scheda **Configura** .</span><span class="sxs-lookup"><span data-stu-id="08df3-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="08df3-136">Nell'elenco tabulare dei record di controllo di accesso, passare il mouse sul record di controllo di accesso che si desidera modificare.</span><span class="sxs-lookup"><span data-stu-id="08df3-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="08df3-137">Fornire un nuovo nome e/o l'IQN del record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="08df3-138">Fare clic su **Salva** per salvare il record di controllo di accesso modificato.</span><span class="sxs-lookup"><span data-stu-id="08df3-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="08df3-139">L'elenco tabulare verrà aggiornato per riflettere questa modifica.</span><span class="sxs-lookup"><span data-stu-id="08df3-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="08df3-140">Eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-140">Delete an access control record</span></span>
<span data-ttu-id="08df3-141">Per eliminare record di controllo di accesso, utilizzare la pagina **Configura** nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="08df3-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="08df3-142">È possibile eliminare solo i record di controllo di acceso che non sono attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="08df3-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="08df3-143">Per eliminare un record di controllo di accesso associato a un volume attualmente in uso, è innanzitutto necessario rendere il volume offline.</span><span class="sxs-lookup"><span data-stu-id="08df3-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="08df3-144">Attenersi alla procedura seguente per eliminare un record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="08df3-145">Per eliminare un record di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="08df3-145">To delete an access control record</span></span>
1. <span data-ttu-id="08df3-146">Nella pagina di destinazione del servizio, selezionare il servizio, fare doppio clic sul nome del servizio, quindi fare clic sulla scheda **Configura** .</span><span class="sxs-lookup"><span data-stu-id="08df3-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="08df3-147">Nell'elenco tabulare dei record di controllo di accesso, passare il mouse sul record di controllo di accesso che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="08df3-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="08df3-148">Nella colonna all'estrema destra del record di controllo di accesso selezionato, verrà visualizzata un'icona di eliminazione (**x**).</span><span class="sxs-lookup"><span data-stu-id="08df3-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="08df3-149">Fare clic sull'icona **x** per eliminare il record di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="08df3-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="08df3-150">Quando viene richiesta la conferma, fare clic su **SÌ** per continuare con l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="08df3-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="08df3-151">L'elenco tabulare verrà aggiornato per riflettere l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="08df3-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08df3-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08df3-152">Next steps</span></span>
* <span data-ttu-id="08df3-153">Ulteriori informazioni sulla [gestione di volumi StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="08df3-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="08df3-154">Ulteriori informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="08df3-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

