---
title: Gestire la potenza di calcolo in Azure SQL Data Warehouse (Portale di Azure) | Microsoft Docs
description: "Attività del portale di Azure per la gestione della potenza di calcolo. Ridimensionare le risorse di calcolo cambiando il numero di DWU. In alternativa, sospendere e riprendere le risorse di calcolo per ridurre i costi."
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
ms.openlocfilehash: 63888d5dd103b585cf18e4787d3e779810163e3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="cce7e-105">Gestire la potenza di calcolo in Azure SQL Data Warehouse (portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="cce7e-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cce7e-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cce7e-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="cce7e-107">Portale</span><span class="sxs-lookup"><span data-stu-id="cce7e-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="cce7e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cce7e-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="cce7e-109">REST</span><span class="sxs-lookup"><span data-stu-id="cce7e-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="cce7e-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="cce7e-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="cce7e-111">Ridimensionare la potenza di calcolo</span><span class="sxs-lookup"><span data-stu-id="cce7e-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="cce7e-112">Per modificare le risorse di calcolo:</span><span class="sxs-lookup"><span data-stu-id="cce7e-112">To change compute resources:</span></span>

1. <span data-ttu-id="cce7e-113">Aprire il [portale di Azure][Azure portal] e quindi il database e fare clic su **Ridimensiona**.</span><span class="sxs-lookup"><span data-stu-id="cce7e-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Fare clici su Ridimensiona][1]
2. <span data-ttu-id="cce7e-115">Nel pannello Scala, spostare il dispositivo di scorrimento a sinistra o a destra per modificare l'impostazione delle DWU.</span><span class="sxs-lookup"><span data-stu-id="cce7e-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Spostare il dispositivo di scorrimento][2]
3. <span data-ttu-id="cce7e-117">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="cce7e-117">Click **Save**.</span></span> <span data-ttu-id="cce7e-118">Viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="cce7e-118">A confirmation message appears.</span></span> <span data-ttu-id="cce7e-119">Fare clic su **Sì** per confermare o su **No** per annullare.</span><span class="sxs-lookup"><span data-stu-id="cce7e-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Fare clic su Salva.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="cce7e-121">Sospendere il calcolo</span><span class="sxs-lookup"><span data-stu-id="cce7e-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="cce7e-122">Per sospende un database:</span><span class="sxs-lookup"><span data-stu-id="cce7e-122">To pause a database:</span></span>

1. <span data-ttu-id="cce7e-123">Aprire il [portale di Azure][Azure portal] e quindi il database.</span><span class="sxs-lookup"><span data-stu-id="cce7e-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="cce7e-124">Osservare che lo stato è **Online**.</span><span class="sxs-lookup"><span data-stu-id="cce7e-124">Notice that the Status is **Online**.</span></span>

    ![Stato online][6]
2. <span data-ttu-id="cce7e-126">Per sospendere il calcolo e le risorse di memoria, fare clic su **Sospendi**. Viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="cce7e-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="cce7e-127">Fare clic su **Sì** per confermare o su **No** per annullare.</span><span class="sxs-lookup"><span data-stu-id="cce7e-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Conferma sospensione][7]
3. <span data-ttu-id="cce7e-129">Durante l'avvio di SQL Data Warehouse lo stato del database è **Sospensione in corso**.</span><span class="sxs-lookup"><span data-stu-id="cce7e-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="cce7e-130">Quando lo stato diventa **Sospeso**, l'operazione di sospensione è completa e le DWU non vengono più addebitate.</span><span class="sxs-lookup"><span data-stu-id="cce7e-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Stato di sospensione][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="cce7e-132">Riavviare le risorse di calcolo</span><span class="sxs-lookup"><span data-stu-id="cce7e-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="cce7e-133">Per riattivare un database:</span><span class="sxs-lookup"><span data-stu-id="cce7e-133">To resume a database:</span></span>

1. <span data-ttu-id="cce7e-134">Aprire il [portale di Azure][Azure portal] e quindi il database.</span><span class="sxs-lookup"><span data-stu-id="cce7e-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="cce7e-135">Osservare che lo stato è **Sospeso**.</span><span class="sxs-lookup"><span data-stu-id="cce7e-135">Notice that the Status is **Paused**.</span></span>

    ![Database in pausa][4]
2. <span data-ttu-id="cce7e-137">Per riattivare il database fare clic su **Avvia**. Viene visualizzato un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="cce7e-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="cce7e-138">Fare clic su **Sì** per confermare o su **No** per annullare.</span><span class="sxs-lookup"><span data-stu-id="cce7e-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Conferma riattivazione][5]
3. <span data-ttu-id="cce7e-140">Durante l'avvio di SQL Data Warehouse lo stato del database è "Sospensione in corso".</span><span class="sxs-lookup"><span data-stu-id="cce7e-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="cce7e-141">Quando lo stato diventa **Online**il database è pronto.</span><span class="sxs-lookup"><span data-stu-id="cce7e-141">When the status is **online**, the database is ready.</span></span>

    ![Stato online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="cce7e-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cce7e-143">Next steps</span></span>
<span data-ttu-id="cce7e-144">Per altre informazioni, vedere la [panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="cce7e-144">For more information, see [Management overview][Management overview].</span></span>

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
