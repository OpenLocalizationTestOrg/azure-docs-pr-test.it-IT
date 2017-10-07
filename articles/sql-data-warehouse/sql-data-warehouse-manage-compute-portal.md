---
title: aaaManage calcolo power in Azure SQL Data Warehouse (portale di Azure) | Documenti Microsoft
description: "Attività del portale Azure toomanage potenza di calcolo. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, è possibile sospendere e riprendere toosave costi delle risorse di calcolo."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="3cf26-105">Gestire la potenza di calcolo in Azure SQL Data Warehouse (portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="3cf26-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3cf26-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3cf26-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="3cf26-107">Portale</span><span class="sxs-lookup"><span data-stu-id="3cf26-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="3cf26-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3cf26-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="3cf26-109">REST</span><span class="sxs-lookup"><span data-stu-id="3cf26-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="3cf26-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="3cf26-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="3cf26-111">Ridimensionare la potenza di calcolo</span><span class="sxs-lookup"><span data-stu-id="3cf26-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="3cf26-112">risorse di calcolo toochange:</span><span class="sxs-lookup"><span data-stu-id="3cf26-112">toochange compute resources:</span></span>

1. <span data-ttu-id="3cf26-113">Aprire hello [portale di Azure][Azure portal], aprire il database e fare clic su **scala**.</span><span class="sxs-lookup"><span data-stu-id="3cf26-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Fare clici su Ridimensiona][1]
2. <span data-ttu-id="3cf26-115">Nel Pannello di scala hello, hello scorrimento sinistro o destro del mouse all'impostazione DWU toochange hello.</span><span class="sxs-lookup"><span data-stu-id="3cf26-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Spostare il dispositivo di scorrimento][2]
3. <span data-ttu-id="3cf26-117">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="3cf26-117">Click **Save**.</span></span> <span data-ttu-id="3cf26-118">Viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="3cf26-118">A confirmation message appears.</span></span> <span data-ttu-id="3cf26-119">Fare clic su **Sì** tooconfirm o **non** toocancel.</span><span class="sxs-lookup"><span data-stu-id="3cf26-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Fare clic su Salva.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="3cf26-121">Sospendere le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="3cf26-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="3cf26-122">toopause un database:</span><span class="sxs-lookup"><span data-stu-id="3cf26-122">toopause a database:</span></span>

1. <span data-ttu-id="3cf26-123">Aprire hello [portale di Azure] [ Azure portal] e aprire il database.</span><span class="sxs-lookup"><span data-stu-id="3cf26-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="3cf26-124">Si noti che lo stato è di hello **Online**.</span><span class="sxs-lookup"><span data-stu-id="3cf26-124">Notice that hello Status is **Online**.</span></span>

    ![Stato online][6]
2. <span data-ttu-id="3cf26-126">Fare clic su risorse di calcolo e memoria toosuspend, **pausa**, e quindi viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="3cf26-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="3cf26-127">Fare clic su **Sì** tooconfirm o **non** toocancel.</span><span class="sxs-lookup"><span data-stu-id="3cf26-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Conferma sospensione][7]
3. <span data-ttu-id="3cf26-129">Durante l'avvio di SQL Data Warehouse database hello, lo stato di hello è **sospensione**.</span><span class="sxs-lookup"><span data-stu-id="3cf26-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="3cf26-130">Quando lo stato di hello è **pausa**, viene eseguita l'operazione di sospensione hello e non siano state addebitate per Dwu.</span><span class="sxs-lookup"><span data-stu-id="3cf26-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Stato di sospensione][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="3cf26-132">Riavviare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="3cf26-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="3cf26-133">tooresume un database:</span><span class="sxs-lookup"><span data-stu-id="3cf26-133">tooresume a database:</span></span>

1. <span data-ttu-id="3cf26-134">Aprire hello [portale di Azure] [ Azure portal] e aprire il database.</span><span class="sxs-lookup"><span data-stu-id="3cf26-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="3cf26-135">Si noti che lo stato è di hello **pausa**.</span><span class="sxs-lookup"><span data-stu-id="3cf26-135">Notice that hello Status is **Paused**.</span></span>

    ![Database in pausa][4]
2. <span data-ttu-id="3cf26-137">Fare clic su database di hello tooresume **avviare**, e quindi viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="3cf26-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="3cf26-138">Fare clic su **Sì** tooconfirm o **non** toocancel.</span><span class="sxs-lookup"><span data-stu-id="3cf26-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Conferma riattivazione][5]
3. <span data-ttu-id="3cf26-140">Durante l'avvio di SQL Data Warehouse database hello, lo stato di hello è "Fase di ripresa".</span><span class="sxs-lookup"><span data-stu-id="3cf26-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="3cf26-141">Quando lo stato di hello è **online**, hello database è pronto.</span><span class="sxs-lookup"><span data-stu-id="3cf26-141">When hello status is **online**, hello database is ready.</span></span>

    ![Stato online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="3cf26-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3cf26-143">Next steps</span></span>
<span data-ttu-id="3cf26-144">Per altre informazioni, vedere la [panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="3cf26-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
