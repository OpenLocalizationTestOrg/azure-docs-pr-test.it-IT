---
title: aaaCreate un SQL Data Warehouse con TSQL | Documenti Microsoft
description: Informazioni su come toocreate un esempio di SQL Azure Data Warehouse con TSQL
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Creare un database di SQL Data Warehouse usando Transact-SQL (TSQL)
> [!div class="op_single_selector"]
> * [portale di Azure](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Questo articolo illustra come toocreate un SQL Data Warehouse utilizzando T-SQL.

## <a name="prerequisites"></a>Prerequisiti
tooget avviato, è necessario:

* **Account Azure**: visitare [versione di valutazione gratuita di Azure] [ Azure Free Trial] o [crediti Azure MSDN] [ MSDN Azure Credits] toocreate un account.
* **Server SQL Azure**: vedere [creare un server logico di Database SQL di Azure con il portale di Azure hello] [creare un server logico di Database SQL di Azure con il portale di Azure hello] o [creare un server logico di Database SQL di Azure con PowerShell] [creare SQL Azure Server logico di database con PowerShell] per ulteriori dettagli.
* **Gruppo di risorse**: utilizzare hello stessa risorsa gruppo di server SQL Azure o vedere [come un gruppo di risorse toocreate][how toocreate a resource group].
* **Ambiente tooexecute T-SQL**: È possibile utilizzare [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], o [SQLServerManagementStudio] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> La creazione di un'istanza di SQL Data Warehouse può dare luogo a un nuovo servizio fatturabile.  Per altre informazioni dettagliate sui prezzi, vedere [Prezzi di SQL Data Warehouse][SQL Data Warehouse pricing].
>
>

## <a name="create-a-database-with-visual-studio"></a>Creare un database con Visual Studio
Nel caso di nuova tooVisual Studio, vedere l'articolo hello [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, aprire Esplora oggetti di SQL Server in Visual Studio e connettersi toohello server che ospiterà il database di SQL Data Warehouse.  Una volta connessi, è possibile creare un Data Warehouse SQL tramite l'esecuzione comando SQL contro hello seguente hello **master** database.  Questo comando crea il database di hello MySqlDwDb con un obiettivo di servizio di DW400 e consentire hello toogrow tooa dimensioni massime del database di 10 TB.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Creare un database con sqlcmd
In alternativa, è possibile eseguire hello stesso comando con sqlcmd eseguendo hello seguente a un prompt dei comandi.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

Hello regole di confronto predefinite quando non viene specificato è COLLATE SQL_Latin1_General_CP1_CI_AS.  Hello `MAXSIZE` deve essere compreso tra 250 GB e TB 240.  Hello `SERVICE_OBJECTIVE` deve essere compreso tra DW100 e DW2000 [DWU][DWU].  Per un elenco di tutti i valori validi, vedere la documentazione MSDN hello per [CREATE DATABASE][CREATE DATABASE].  Hello MAXSIZE sia possono SERVICE_OBJECTIVE essere modificati con un [ALTER DATABASE] [ ALTER DATABASE] comando T-SQL.  regole di confronto di Hello di un database non possono essere modificate dopo la creazione.   Attenzione deve essere utilizzato quando la modifica hello SERVICE_OBJECTIVE come la modifica DWU comporta il riavvio dei servizi, che annulla tutte le query in fase di trasferimento.  La modifica di MAXSIZE non riavvia i servizi, perché si tratta di una semplice operazione sui metadati.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver completato il provisioning è possibile il Data Warehouse di SQL [caricare dati di esempio] [ load sample data] o estrarlo come troppo[sviluppare][develop], [caricare][load], o [migrare][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
