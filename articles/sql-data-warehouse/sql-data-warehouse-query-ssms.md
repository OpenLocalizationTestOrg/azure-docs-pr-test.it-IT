---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Documenti Microsoft
description: Utilizzare SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>Connettersi tooSQL Data Warehouse con SQL Server Management Studio (SSMS)
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilizzare SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse. 

## <a name="prerequisites"></a>Prerequisiti
toouse questa esercitazione, è necessario:

* Un'istanza di SQL Data Warehouse esistente. toocreate uno, vedere [creare un Data Warehouse SQL][Create a SQL Data Warehouse].
* SQL Server Management Studio (SSMS) installato. [Installare SSMS][Install SSMS] gratuitamente se non è già stato installato.
* Hello completo nome SQL server. toofind questa operazione, vedere [connessione Data Warehouse tooSQL][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Connettersi tooyour SQL Data Warehouse
1. Aprire SQL Server Management Studio.
2. Aprire Esplora oggetti. toodo, selezionare **File** > **Connetti Esplora oggetti**.
   
    ![Esplora oggetti di SQL Server][1]
3. Compilare i campi di hello nella finestra di tooServer hello Connect.
   
    ![Connettersi tooServer][2]
   
   * **Nome server**. Immettere hello **nome server** identificati in precedenza.
   * **Autenticazione**. Selezionare **Autenticazione di SQL Server** o **Autenticazione integrata di Active Directory**.
   * **Nome utente** e **Password**. Se è stata selezionata l'autenticazione di SQL Server, immettere il nome utente e la password.
   * Fare clic su **Connetti**.
4. tooexplore, espandere il server SQL Azure. È possibile visualizzare i database di hello associati hello server. Espandere AdventureWorksDW toosee hello tabelle nel database di esempio.
   
    ![Esplorare AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a>2. Eseguire una query di esempio
Ora che una connessione è stata stabilita tooyour database, è possibile scrivere una query.

1. Fare clic con il pulsante destro del mouse sul database in Esplora oggetti di SQL Server.
2. Scegliere **Nuova query**. Verrà visualizzata una nuova finestra di query.
   
    ![Nuova query][4]
3. Copiare la query TSQL nella finestra query hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Eseguire query hello. toodo, fare clic su `Execute` o utilizzare hello seguente collegamento: `F5`.
   
    ![Esegui query][5]
5. Esaminare i risultati di query hello. In questo esempio, nella tabella FactInternetSales hello è 60398 righe.
   
    ![Risultati query][6]

## <a name="next-steps"></a>Passaggi successivi
Ora che è possibile connettersi ed eseguire query, provare [visualizzazione dei dati di hello con Power BI][visualizing hello data with PowerBI].

tooconfigure l'ambiente per l'autenticazione di Azure Active Directory, vedere [autenticare tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
