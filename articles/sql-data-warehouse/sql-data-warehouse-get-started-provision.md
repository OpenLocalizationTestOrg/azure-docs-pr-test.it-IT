---
title: un Data Warehouse di SQL nel portale di Azure hello aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un Azure SQL Data Warehouse in hello portale di Azure
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a>Creare un Azure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [portale di Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Questa esercitazione Usa hello toocreate portale Azure un SQL Data Warehouse che contiene un database di esempio AdventureWorksDW.

## <a name="prerequisites"></a>Prerequisiti
tooget avviato, è necessario:

* **Account Azure**: visitare [versione di valutazione gratuita di Azure] [ Azure Free Trial] o [crediti Azure MSDN] [ MSDN Azure Credits] toocreate un account.
* **Server SQL Azure**: vedere [creare un database SQL di Azure con il portale di Azure hello] [ Create an Azure SQL database in hello Azure portal] per altri dettagli.

> [!NOTE]
> La creazione di un'istanza di SQL Data Warehouse può avere come risultato un nuovo servizio fatturabile.  Per altri dettagli, vedere la pagina relativa ai [prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Creare un SQL Data Warehouse
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **+ Nuovo** > **Database** > **SQL Data Warehouse**.

    ![Create](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. In hello **SQL Data Warehouse** pannello, compilare informazioni hello necessarie, quindi premere toocreate 'Crea'.

    ![Creazione del database](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Server**: è consigliabile selezionare prima di tutto il server.  
   * **Nome del database**: nome hello hello tooreference utilizzato SQL Data Warehouse.  Deve essere univoco toohello server.
   * **Prestazioni**: è consigliabile iniziare con 400 [DWU][DWU]. È possibile spostare hello toohello di dispositivo di scorrimento sinistro o destro del mouse sulle prestazioni di hello tooadjust del data warehouse o scala verso l'alto o verso il basso dopo la creazione.  toolearn ulteriori informazioni su Dwu, vedere la documentazione su [scalabilità](sql-data-warehouse-manage-compute-overview.md) o la [pagina dei prezzi][SQL Data Warehouse pricing].
   * **Sottoscrizione**: hello seleziona [sottoscrizione] che questo Data Warehouse SQL verranno fatturate per.
   * **Gruppo di risorse**: [gruppi di risorse] [ Resource group] sono toohelp contenitori progettati gestire una raccolta di risorse di Azure. Altre informazioni sui [gruppi di risorse](../azure-resource-manager/resource-group-overview.md).
   * **Selezionare l'origine**: fare clic su **Selezionare l'origine** > **Esempio**. Azure popola automaticamente hello **esempio seleziona** opzione con AdventureWorksDW.

   > [!NOTE]
   > regole di confronto predefinite Hello per un SQL Data Warehouse è SQL_Latin1_General_CP1_CI_AS. Se sono necessarie regole di confronto diverse, [T-SQL] [ T-SQL] può essere utilizzato toocreate hello database con regole di confronto diverse.
   >
   >

1. Fare clic su **crea** toocreate il SQL del Data Warehouse.
2. Attendere alcuni minuti. Quando il data warehouse è pronto, devono essere restituiti toohello [portale di Azure](https://portal.azure.com). È possibile trovare il Data Warehouse di SQL nel dashboard, elencati in database SQL o nella risorsa hello gruppo è stato utilizzato toocreate è.

    ![Visualizzazione del portale](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Passaggi successivi
Ora che è stato creato un SQL Data Warehouse, si è pronti troppo[Connetti](sql-data-warehouse-connect-overview.md) e iniziare l'esecuzione di query.

dati di tooload in SQL Data Warehouse, vedere hello [durante il caricamento di panoramica](sql-data-warehouse-overview-load.md).

Se si sta tentando di toomigrate un tooSQL di database del Data Warehouse esistente, vedere hello [Cenni preliminari sulla migrazione](sql-data-warehouse-overview-migrate.md) o utilizzare [utilità di migrazione](sql-data-warehouse-migrate-migration-utility.md).

Le regole firewall possono anche essere configurate con Transact-SQL. Per altre informazioni, vedere [sp_set_firewall_rule][sp_set_firewall_rule] e [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

È anche una buona idea toolook in hello [consigliate][Best practices].

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[sottoscrizione]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
