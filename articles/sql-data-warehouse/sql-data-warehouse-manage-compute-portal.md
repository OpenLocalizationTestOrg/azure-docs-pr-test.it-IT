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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Gestire la potenza di calcolo in Azure SQL Data Warehouse (portale di Azure)
> [!div class="op_single_selector"]
> * [Panoramica](sql-data-warehouse-manage-compute-overview.md)
> * [Portale](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Ridimensionare la potenza di calcolo
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

risorse di calcolo toochange:

1. Aprire hello [portale di Azure][Azure portal], aprire il database e fare clic su **scala**.

    ![Fare clici su Ridimensiona][1]
2. Nel Pannello di scala hello, hello scorrimento sinistro o destro del mouse all'impostazione DWU toochange hello.

    ![Spostare il dispositivo di scorrimento][2]
3. Fare clic su **Save**. Viene visualizzato un messaggio di conferma. Fare clic su **Sì** tooconfirm o **non** toocancel.

    ![Fare clic su Salva.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Sospendere le risorse di calcolo
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause un database:

1. Aprire hello [portale di Azure] [ Azure portal] e aprire il database. Si noti che lo stato è di hello **Online**.

    ![Stato online][6]
2. Fare clic su risorse di calcolo e memoria toosuspend, **pausa**, e quindi viene visualizzato un messaggio di conferma. Fare clic su **Sì** tooconfirm o **non** toocancel.

    ![Conferma sospensione][7]
3. Durante l'avvio di SQL Data Warehouse database hello, lo stato di hello è **sospensione**.
4. Quando lo stato di hello è **pausa**, viene eseguita l'operazione di sospensione hello e non siano state addebitate per Dwu.

    ![Stato di sospensione][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Riavviare le risorse di calcolo
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume un database:

1. Aprire hello [portale di Azure] [ Azure portal] e aprire il database. Si noti che lo stato è di hello **pausa**.

    ![Database in pausa][4]
2. Fare clic su database di hello tooresume **avviare**, e quindi viene visualizzato un messaggio di conferma. Fare clic su **Sì** tooconfirm o **non** toocancel.

    ![Conferma riattivazione][5]
3. Durante l'avvio di SQL Data Warehouse database hello, lo stato di hello è "Fase di ripresa".
4. Quando lo stato di hello è **online**, hello database è pronto.

    ![Stato online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere la [panoramica della gestione][Management overview].

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
