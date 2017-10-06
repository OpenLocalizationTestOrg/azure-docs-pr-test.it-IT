---
title: aaaGet avviato con query tra database (partizionamento verticale) | Documenti Microsoft
description: la query di database elastico toouse con partizionato verticalmente i database
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Introduzione alle query tra database (partizionamento verticale) (anteprima)
Query di database elastico (anteprima) per il Database SQL di Azure consente query T-SQL toorun che si estendono su più database utilizzando un singolo punto di connessione. Questo argomento si applica troppo[partizionato verticalmente database](sql-database-elastic-query-vertical-partitioning.md).  

Al termine, sarà possibile: informazioni su come tooconfigure e utilizzare un Database SQL di Azure di tooperform query suddivisi in più database correlati. 

Per ulteriori informazioni sulla funzionalità di query di database elastico hello, vedere [panoramica delle query di Database di SQL Azure database elastico](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Prerequisiti

L'utente deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE. Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello. Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.

## <a name="create-hello-sample-databases"></a>Creare i database di esempio di hello
toostart con, è necessario toocreate due database, **clienti** e **ordini**, in hello uguali o diversi server logici.   

Eseguire hello seguendo le query hello **ordini** hello toocreate database **OrderInformation** tabella e l'input di dati di esempio hello. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

A questo punto, eseguire query su hello riportata di seguito **clienti** hello toocreate database **CustomerInformation** tabella e l'input di dati di esempio hello. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Creare oggetti di database
### <a name="database-scoped-master-key-and-credentials"></a>Chiave master e credenziali con ambito database
1. Apri SQL Server Management Studio e SQL Server Data Tools in Visual Studio
2. La connessione a database Orders toohello ed eseguire hello comandi T-SQL seguente:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Hello "nomeutente" e "password" deve essere hello username e password utilizzati toologin nel database di clienti hello.
    L'autenticazione tramite Azure Active Directory con query elastiche non è attualmente supportata.

### <a name="external-data-sources"></a>DROP EXTERNAL DATA SOURCE
toocreate un'origine dati esterna, eseguire comando seguente nel database Orders hello hello: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Tabelle esterne
Creare una tabella esterna nel database Orders hello, che corrisponde a definizione hello della tabella CustomerInformation hello:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Eseguire una query di esempio elastica database T-SQL
Dopo aver definito l'origine dati esterna e le tabelle esterne, è ora possibile usare tooquery T-SQL le tabelle esterne. Eseguire la query sul database Orders hello: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Costi
Attualmente, funzionalità di query di database elastico hello è incluso nel costo hello del Database SQL di Azure.  

Per informazioni sui prezzi, vedere [Database SQL - Prezzi](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Passaggi successivi

* Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).
* Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)
* Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).
* Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)
* Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.