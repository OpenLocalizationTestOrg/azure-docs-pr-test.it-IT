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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="3672c-103">Introduzione alle query tra database (partizionamento verticale) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="3672c-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="3672c-104">Query di database elastico (anteprima) per il Database SQL di Azure consente query T-SQL toorun che si estendono su più database utilizzando un singolo punto di connessione.</span><span class="sxs-lookup"><span data-stu-id="3672c-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="3672c-105">Questo argomento si applica troppo[partizionato verticalmente database](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="3672c-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="3672c-106">Al termine, sarà possibile: informazioni su come tooconfigure e utilizzare un Database SQL di Azure di tooperform query suddivisi in più database correlati.</span><span class="sxs-lookup"><span data-stu-id="3672c-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="3672c-107">Per ulteriori informazioni sulla funzionalità di query di database elastico hello, vedere [panoramica delle query di Database di SQL Azure database elastico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3672c-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3672c-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3672c-108">Prerequisites</span></span>

<span data-ttu-id="3672c-109">L'utente deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="3672c-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="3672c-110">Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="3672c-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="3672c-111">Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="3672c-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="3672c-112">Creare i database di esempio di hello</span><span class="sxs-lookup"><span data-stu-id="3672c-112">Create hello sample databases</span></span>
<span data-ttu-id="3672c-113">toostart con, è necessario toocreate due database, **clienti** e **ordini**, in hello uguali o diversi server logici.</span><span class="sxs-lookup"><span data-stu-id="3672c-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="3672c-114">Eseguire hello seguendo le query hello **ordini** hello toocreate database **OrderInformation** tabella e l'input di dati di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="3672c-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="3672c-115">A questo punto, eseguire query su hello riportata di seguito **clienti** hello toocreate database **CustomerInformation** tabella e l'input di dati di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="3672c-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="3672c-116">Creare oggetti di database</span><span class="sxs-lookup"><span data-stu-id="3672c-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="3672c-117">Chiave master e credenziali con ambito database</span><span class="sxs-lookup"><span data-stu-id="3672c-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="3672c-118">Apri SQL Server Management Studio e SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3672c-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="3672c-119">La connessione a database Orders toohello ed eseguire hello comandi T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="3672c-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="3672c-120">Hello "nomeutente" e "password" deve essere hello username e password utilizzati toologin nel database di clienti hello.</span><span class="sxs-lookup"><span data-stu-id="3672c-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="3672c-121">L'autenticazione tramite Azure Active Directory con query elastiche non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="3672c-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="3672c-122">DROP EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="3672c-122">External data sources</span></span>
<span data-ttu-id="3672c-123">toocreate un'origine dati esterna, eseguire comando seguente nel database Orders hello hello:</span><span class="sxs-lookup"><span data-stu-id="3672c-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="3672c-124">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="3672c-124">External tables</span></span>
<span data-ttu-id="3672c-125">Creare una tabella esterna nel database Orders hello, che corrisponde a definizione hello della tabella CustomerInformation hello:</span><span class="sxs-lookup"><span data-stu-id="3672c-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="3672c-126">Eseguire una query di esempio elastica database T-SQL</span><span class="sxs-lookup"><span data-stu-id="3672c-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="3672c-127">Dopo aver definito l'origine dati esterna e le tabelle esterne, è ora possibile usare tooquery T-SQL le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="3672c-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="3672c-128">Eseguire la query sul database Orders hello:</span><span class="sxs-lookup"><span data-stu-id="3672c-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="3672c-129">Costi</span><span class="sxs-lookup"><span data-stu-id="3672c-129">Cost</span></span>
<span data-ttu-id="3672c-130">Attualmente, funzionalità di query di database elastico hello è incluso nel costo hello del Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="3672c-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="3672c-131">Per informazioni sui prezzi, vedere [Database SQL - Prezzi](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="3672c-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3672c-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3672c-132">Next steps</span></span>

* <span data-ttu-id="3672c-133">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3672c-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="3672c-134">Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="3672c-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="3672c-135">Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3672c-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="3672c-136">Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="3672c-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="3672c-137">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="3672c-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>