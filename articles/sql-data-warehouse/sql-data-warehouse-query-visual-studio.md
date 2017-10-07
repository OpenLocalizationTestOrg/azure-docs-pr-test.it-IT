---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Documenti Microsoft
description: Eseguire query in SQL Data Warehouse con Visual Studio.
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Connettersi tooSQL Data Warehouse con Visual Studio e SSDT
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Utilizzare Visual Studio tooquery Azure SQL Data Warehouse in pochi minuti. Questo metodo Usa l'estensione di SQL Server Data Tools (SSDT) hello in Visual Studio. 

## <a name="prerequisites"></a>Prerequisiti
toouse questa esercitazione, è necessario:

* Un'istanza di SQL Data Warehouse esistente. toocreate uno, vedere [creare un Data Warehouse SQL][Create a SQL Data Warehouse].
* SSDT per Visual Studio. Se Visual Studio è già installato, probabilmente SSDT è già disponibile. Per istruzioni sull'installazione e sulle opzioni, vedere [Installazione di Visual Studio e SSDT][Installing Visual Studio and SSDT].
* Hello completo nome SQL server. toofind questa operazione, vedere [connessione Data Warehouse tooSQL][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. Connettersi tooyour SQL Data Warehouse
1. Aprire Visual Studio 2013 o 2015.
2. Aprire Esplora oggetti di SQL Server. toodo, selezionare **vista** > **Esplora oggetti di SQL Server**.
   
    ![Esplora oggetti di SQL Server][1]
3. Fare clic su hello **aggiungere SQL Server** icona.
   
    ![Aggiungi SQL Server][2]
4. Compilare i campi di hello nella finestra di tooServer hello Connect.
   
    ![Connettersi tooServer][3]
   
   * **Nome server**. Immettere hello **nome server** identificati in precedenza.
   * **Autenticazione**. Selezionare **Autenticazione di SQL Server** o **Autenticazione integrata di Active Directory**.
   * **Nome utente** e **Password**. Se è stata selezionata l'autenticazione di SQL Server, immettere il nome utente e la password.
   * Fare clic su **Connetti**.
5. tooexplore, espandere il server SQL Azure. È possibile visualizzare i database di hello associati hello server. Espandere AdventureWorksDW toosee hello tabelle nel database di esempio.
   
    ![Esplorare AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a>2. Eseguire una query di esempio
Ora che una connessione è stata stabilita tooyour database, è possibile scrivere una query.

1. Fare clic con il pulsante destro del mouse sul database in Esplora oggetti di SQL Server.
2. Scegliere **Nuova query**. Verrà visualizzata una nuova finestra di query.
   
    ![Nuova query][5]
3. Copiare la query TSQL nella finestra query hello:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Eseguire query hello. toodo, fare clic sulla freccia verde hello o utilizzare hello seguente collegamento: `CTRL` + `SHIFT` + `E`.
   
    ![Esegui query][6]
5. Esaminare i risultati di query hello. In questo esempio, nella tabella FactInternetSales hello è 60398 righe.
   
    ![Risultati query][7]

## <a name="next-steps"></a>Passaggi successivi
Ora che è possibile connettersi ed eseguire query, provare [visualizzazione dei dati di hello con Power BI][visualizing hello data with PowerBI].

tooconfigure l'ambiente per l'autenticazione di Azure Active Directory, vedere [autenticare tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
