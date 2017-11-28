---
title: aaaDesign il database SQL di Azure prima - c# | Documenti Microsoft
description: Informazioni su toodesign di un database SQL di Azure e connettersi tooit con un programma c# tramite ADO.NET.
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="32e3b-103">Progettare un database SQL di Azure e connettersi con C&#x23; e ADO.NET</span><span class="sxs-lookup"><span data-stu-id="32e3b-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="32e3b-104">Database SQL di Azure è un relazionale database-come a un servizio (DBaaS) in hello Cloud Microsoft ("Azure").</span><span class="sxs-lookup"><span data-stu-id="32e3b-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="32e3b-105">In questa esercitazione, è illustrato come toouse hello portale di Azure e ADO.NET con Visual Studio per:</span><span class="sxs-lookup"><span data-stu-id="32e3b-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="32e3b-106">Creare un database in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="32e3b-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="32e3b-107">Impostare una regola firewall di livello server nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="32e3b-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="32e3b-108">La connessione a database toohello con ADO.NET e Visual Studio</span><span class="sxs-lookup"><span data-stu-id="32e3b-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="32e3b-109">Creare tabelle con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="32e3b-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="32e3b-110">Inserire, aggiornare ed eliminare dati con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="32e3b-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="32e3b-111">Eseguire query sui dati con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="32e3b-111">Query data ADO.NET</span></span>

<span data-ttu-id="32e3b-112">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="32e3b-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32e3b-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="32e3b-113">Prerequisites</span></span>

<span data-ttu-id="32e3b-114">Un'installazione di [Visual Studio Community 2017, Visual Studio Professional 2017 o Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="32e3b-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="32e3b-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32e3b-115">Next steps</span></span>

<span data-ttu-id="32e3b-116">In questa esercitazione è stato attività di base del database, ad esempio creare un database e tabelle, caricare e query sui dati e hello database tooa precedente punto di ripristino temporizzato.</span><span class="sxs-lookup"><span data-stu-id="32e3b-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="32e3b-117">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="32e3b-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="32e3b-118">Creare un database</span><span class="sxs-lookup"><span data-stu-id="32e3b-118">Create a database</span></span>
> * <span data-ttu-id="32e3b-119">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="32e3b-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="32e3b-120">La connessione a database toohello con [c# e Visual Studio](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="32e3b-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="32e3b-121">Creare tabelle</span><span class="sxs-lookup"><span data-stu-id="32e3b-121">Create tables</span></span>
> * <span data-ttu-id="32e3b-122">Inserire, aggiornare ed eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="32e3b-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="32e3b-123">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="32e3b-123">Query data</span></span>

<span data-ttu-id="32e3b-124">Spostare toohello toolearn esercitazione successiva sulla migrazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="32e3b-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="32e3b-125">Eseguire la migrazione del tooAzure di database di SQL Server Database SQL</span><span class="sxs-lookup"><span data-stu-id="32e3b-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

