---
title: aaaCreate SQL Data Warehouse mediante PowerShell | Documenti Microsoft
description: Creare un'istanza di SQL Data Warehouse con PowerShell
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>Creare SQL Data Warehouse con PowerShell
> [!div class="op_single_selector"]
> * [portale di Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Questo articolo illustra come toocreate un SQL Data Warehouse tramite PowerShell.

## <a name="prerequisites"></a>Prerequisiti
tooget avviato, è necessario:

* **Account Azure**: visitare [versione di valutazione gratuita di Azure] [ Azure Free Trial] o [crediti Azure MSDN] [ MSDN Azure Credits] toocreate un account.
* **Server SQL Azure**: vedere [creare un database SQL di Azure nel portale di Azure hello] [ Create an Azure SQL database in hello Azure Portal] o [creare un database SQL di Azure con PowerShell] [ Create an Azure SQL database with PowerShell] per altri dettagli.
* **Gruppo di risorse**: utilizzare hello stessa risorsa gruppo di server SQL Azure o vedere [come un gruppo di risorse toocreate](../azure-resource-manager/resource-group-portal.md).
* **PowerShell versione 1.0.3 o successiva**: è possibile verificare la versione in uso eseguendo **Get-Module -ListAvailable -Name Azure**.  è possibile installare la versione più recente di Hello da [installazione guidata piattaforma Web di Microsoft][Microsoft Web Platform Installer].  Per ulteriori informazioni su come installare la versione più recente di hello, vedere [come tooinstall e configurare Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.  Per altre informazioni dettagliate sui prezzi, vedere [Prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>Creare un SQL Data Warehouse
1. Aprire Windows PowerShell.
2. Eseguire questo tooAzure toologin cmdlet Gestione risorse.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Selezionare la sottoscrizione di hello da toouse per la sessione corrente.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Creare il database. In questo esempio viene creato un database denominato "mynewsqldw", con l'obiettivo livello di servizio "DW400", toohello server denominato "sqldwserver1", nel gruppo di risorse di hello denominato "mywesteuroperesgp1".

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

I parametri obbligatori sono:

* **RequestedServiceObjectiveName**: quantità di hello di [DWU] [ DWU] richiesta.  I valori supportati sono: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 e DW6000.
* **DatabaseName**: nome hello di hello SQL Data Warehouse che si sta creando.
* **ServerName**: nome hello del server di hello che si sta utilizzando per la creazione (deve essere V12).
* **ResourceGroupName**: il gruppo di risorse in uso.  toofind gruppi di risorse disponibili nella sottoscrizione utilizzano Get-AzureResource.
* **Edizione**: deve essere "Data warehouse" toocreate un SQL Data Warehouse.

I parametri facoltativi sono:

* **CollationName**: hello regole di confronto predefinite se non specificato è SQL_Latin1_General_CP1_CI_AS.  Non è possibile modificare le regole di confronto in un database.
* **MaxSizeBytes**: dimensioni massime di hello predefinito di un database sono di 10 GB.

Per ulteriori dettagli sulle opzioni di parametro hello, vedere [New AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] e [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Passaggi successivi
Dopo che il Data Warehouse SQL ha completato il provisioning è opportuno tootry [durante il caricamento di dati di esempio] [ loading sample data] o estrarlo come troppo[sviluppare] [ develop] , [caricare][load], o [migrare][migrate].

Se si è interessati in altre informazioni su come toomanage SQL Data Warehouse a livello di codice, vedere l'articolo su come toouse [i cmdlet di PowerShell e API REST][PowerShell cmdlets and REST APIs].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
