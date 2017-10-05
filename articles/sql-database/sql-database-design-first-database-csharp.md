---
title: Progettare il primo database SQL di Azure - C# | Microsoft Docs
description: Informazioni su come progettare il primo database SQL di Azure e connettersi a esso con un programma C# tramite ADO.NET.
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
ms.openlocfilehash: d9731cf5399cce6f103129ccda521f2867bd8da6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="c6acb-103">Progettare un database SQL di Azure e connettersi con C&#x23; e ADO.NET</span><span class="sxs-lookup"><span data-stu-id="c6acb-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="c6acb-104">Il database SQL di Azure è un database relazionale come servizio (DBaaS, Database-As-A-Service) disponibile in Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="c6acb-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="c6acb-105">In questa esercitazione viene illustrato come usare il portale di Azure e ADO.NET con Visual Studio per eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="c6acb-105">In this tutorial, you learn how to use the Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c6acb-106">Creare un database nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6acb-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="c6acb-107">Impostare una regola del firewall a livello di server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c6acb-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="c6acb-108">Connettersi al database con ADO.NET e Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6acb-108">Connect to the database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="c6acb-109">Creare tabelle con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="c6acb-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="c6acb-110">Inserire, aggiornare ed eliminare dati con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="c6acb-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="c6acb-111">Eseguire query sui dati con ADO.NET</span><span class="sxs-lookup"><span data-stu-id="c6acb-111">Query data ADO.NET</span></span>

<span data-ttu-id="c6acb-112">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="c6acb-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6acb-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c6acb-113">Prerequisites</span></span>

<span data-ttu-id="c6acb-114">Un'installazione di [Visual Studio Community 2017, Visual Studio Professional 2017 o Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c6acb-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- The following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- The following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="c6acb-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6acb-115">Next steps</span></span>

<span data-ttu-id="c6acb-116">Questa esercitazione ha illustrato le attività di base che è possibile eseguire con i database, come creare database e tabelle, caricare dati, eseguire query sui dati e ripristinare un database a un momento precedente.</span><span class="sxs-lookup"><span data-stu-id="c6acb-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="c6acb-117">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="c6acb-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="c6acb-118">Creare un database</span><span class="sxs-lookup"><span data-stu-id="c6acb-118">Create a database</span></span>
> * <span data-ttu-id="c6acb-119">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="c6acb-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="c6acb-120">Connettersi al database con [Visual Studio e C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="c6acb-120">Connect to the database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="c6acb-121">Creare tabelle</span><span class="sxs-lookup"><span data-stu-id="c6acb-121">Create tables</span></span>
> * <span data-ttu-id="c6acb-122">Inserire, aggiornare ed eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="c6acb-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="c6acb-123">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="c6acb-123">Query data</span></span>

<span data-ttu-id="c6acb-124">Passare all'esercitazione successiva per ottenere informazioni sulla migrazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c6acb-124">Advance to the next tutorial to learn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="c6acb-125">Eseguire la migrazione di un database SQL Server a un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="c6acb-125">Migrate your SQL Server database to Azure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

