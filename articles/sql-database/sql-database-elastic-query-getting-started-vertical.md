---
title: Introduzione alle query tra database (partizionamento verticale) | Documentazione Microsoft
description: Informazioni sull'uso della query del database elastico con database con partizionamento verticale.
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
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="67b9d-103">Introduzione alle query tra database (partizionamento verticale) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="67b9d-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="67b9d-104">La query del database elastico (anteprima) per il database SQL di Azure consente di eseguire query T-SQL che si estendono a più database usando un unico punto di connessione.</span><span class="sxs-lookup"><span data-stu-id="67b9d-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="67b9d-105">Questo argomento si applica ai [database con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="67b9d-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="67b9d-106">Al termine, si apprenderà come configurare e usare un database SQL di Azure per eseguire query che coinvolgono più database correlati.</span><span class="sxs-lookup"><span data-stu-id="67b9d-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="67b9d-107">Per altre informazioni sulla funzionalità di query del database elastico, vedere [Panoramica delle query su database elastico del database SQL di Azure](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67b9d-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="67b9d-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67b9d-108">Prerequisites</span></span>

<span data-ttu-id="67b9d-109">L'utente deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="67b9d-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="67b9d-110">Questa autorizzazione è inclusa nell'autorizzazione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="67b9d-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="67b9d-111">Per il riferimento all'origine dati sottostante sono necessarie autorizzazioni ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="67b9d-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="67b9d-112">Creare i database di esempio</span><span class="sxs-lookup"><span data-stu-id="67b9d-112">Create the sample databases</span></span>
<span data-ttu-id="67b9d-113">Per iniziare, è necessario creare due database, **Customers** e **Orders**, in server logici uguali o diversi.</span><span class="sxs-lookup"><span data-stu-id="67b9d-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="67b9d-114">Eseguire le query seguenti sul database **Orders** per creare la tabella **OrderInformation** e inserire i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="67b9d-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="67b9d-115">Eseguire quindi la query seguente sul database **Customers** per creare la tabella **CustomerInformation** e inserire i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="67b9d-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="67b9d-116">Creare oggetti di database</span><span class="sxs-lookup"><span data-stu-id="67b9d-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="67b9d-117">Chiave master e credenziali con ambito database</span><span class="sxs-lookup"><span data-stu-id="67b9d-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="67b9d-118">Apri SQL Server Management Studio e SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="67b9d-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="67b9d-119">Connettersi al database Orders ed eseguire i comandi T-SQL seguenti:</span><span class="sxs-lookup"><span data-stu-id="67b9d-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="67b9d-120">Il nome utente e la password devono corrispondere al nome utente e alla password usati per l'accesso al database Customers.</span><span class="sxs-lookup"><span data-stu-id="67b9d-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="67b9d-121">L'autenticazione tramite Azure Active Directory con query elastiche non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="67b9d-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="67b9d-122">DROP EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="67b9d-122">External data sources</span></span>
<span data-ttu-id="67b9d-123">Per creare un'origine dati esterna, eseguire il comando seguente sul database Orders:</span><span class="sxs-lookup"><span data-stu-id="67b9d-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="67b9d-124">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="67b9d-124">External tables</span></span>
<span data-ttu-id="67b9d-125">Creare una tabella esterna nel database Orders che corrisponda alla definizione della tabella CustomerInformation:</span><span class="sxs-lookup"><span data-stu-id="67b9d-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="67b9d-126">Eseguire una query di esempio elastica database T-SQL</span><span class="sxs-lookup"><span data-stu-id="67b9d-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="67b9d-127">Dopo aver definito l'origine dati esterna e le tabelle esterne, è possibile usare T-SQL per eseguire query nelle tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="67b9d-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="67b9d-128">Eseguire questa query nel database Orders:</span><span class="sxs-lookup"><span data-stu-id="67b9d-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="67b9d-129">Costi</span><span class="sxs-lookup"><span data-stu-id="67b9d-129">Cost</span></span>
<span data-ttu-id="67b9d-130">Attualmente, la funzionalità di query del database elastico è compresa nel costo del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="67b9d-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="67b9d-131">Per informazioni sui prezzi, vedere [Database SQL - Prezzi](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="67b9d-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="67b9d-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67b9d-132">Next steps</span></span>

* <span data-ttu-id="67b9d-133">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67b9d-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="67b9d-134">Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="67b9d-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="67b9d-135">Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="67b9d-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="67b9d-136">Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="67b9d-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="67b9d-137">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="67b9d-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>