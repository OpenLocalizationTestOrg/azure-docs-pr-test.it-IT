---
title: Procedure dettagliate di data science per SQL Server con R, Python e T-SQL | Microsoft Docs
description: Esempi che illustrano l'uso di R, Python e T-SQL in SQL Server per eseguire analisi predittive.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 333fd4ee6dcdcbfd347d6b5e8cb900474f6ec8cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="sql-server-data-science-walkthroughs-using-r-python-and-t-sql"></a><span data-ttu-id="4913d-103">Procedure dettagliate di data science per SQL Server con R, Python e T-SQL</span><span class="sxs-lookup"><span data-stu-id="4913d-103">SQL Server data science walkthroughs using R, Python and T-SQL</span></span>

<span data-ttu-id="4913d-104">Queste procedure dettagliate usano SQL Server, SQL Server R Services e SQL Server Python Services per eseguire analisi predittive.</span><span class="sxs-lookup"><span data-stu-id="4913d-104">These walkthroughs use SQL Server, SQL Server R Services, and SQL Server Python Services to do predictive analytics.</span></span> <span data-ttu-id="4913d-105">Il codice R e Python è distribuito in stored procedure.</span><span class="sxs-lookup"><span data-stu-id="4913d-105">R and Python code is deployed in stored procedures.</span></span> <span data-ttu-id="4913d-106">Seguono i passaggi descritti nel processo di data science per i team.</span><span class="sxs-lookup"><span data-stu-id="4913d-106">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="4913d-107">Per una panoramica del processo di data science per i team, vedere [Processo di data science](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4913d-107">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> 

<span data-ttu-id="4913d-108">Le procedure dettagliate di data science aggiuntive che eseguono il processo di data science per i team sono raggruppate in base alla **piattaforma** che usano:</span><span class="sxs-lookup"><span data-stu-id="4913d-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-python-and-sql-queries-with-sql-server"></a><span data-ttu-id="4913d-109">Stimare le mance dei taxi usando Python e query SQL con SQL Server</span><span class="sxs-lookup"><span data-stu-id="4913d-109">Predict taxi tips using Python and SQL queries with SQL Server</span></span> 

<span data-ttu-id="4913d-110">La procedura dettagliata relativa all'[uso di SQL Server](machine-learning-data-science-process-sql-walkthrough.md) illustra come compilare e distribuire modelli di classificazione e regressione di Machine Learning usando SQL Server per un set di dati disponibile pubblicamente relativo a corse e tariffe dei taxi nella città di New York.</span><span class="sxs-lookup"><span data-stu-id="4913d-110">The [Use SQL Server](machine-learning-data-science-process-sql-walkthrough.md) walkthrough shows how you build and deploy machine learning classification and regression models using SQL Server and a publicly available NYC taxi trip and fare dataset.</span></span>


## <a name="predict-taxi-tips-using-microsoft-r-with-sql-server"></a><span data-ttu-id="4913d-111">Stimare le mance dei taxi usando Microsoft R con SQL Server</span><span class="sxs-lookup"><span data-stu-id="4913d-111">Predict taxi tips using Microsoft R with SQL Server</span></span> 

<span data-ttu-id="4913d-112">La procedura dettagliata relativa all'[uso di servizi R per SQL Server](https://msdn.microsoft.com/library/mt612857.aspx) offre ai data scientist una combinazione di codice R, dati SQL Server e funzioni SQL personalizzate per compilare e distribuire un modello R in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4913d-112">The [Use SQL Server R Services](https://msdn.microsoft.com/library/mt612857.aspx) walkthrough provides data scientists with a combination of R code, SQL Server data, and custom SQL functions to build and deploy an R model to SQL Server.</span></span> <span data-ttu-id="4913d-113">La procedura dettagliata è progettata per illustrare R Services agli sviluppatori R (nel database).</span><span class="sxs-lookup"><span data-stu-id="4913d-113">The walkthrough is designed to introduce R developers to R Services (In-Database).</span></span>


## <a name="predict-taxi-tips-using-r-from-t-sql-or-stored-procedures-with-sql-server"></a><span data-ttu-id="4913d-114">Stimare le mance dei taxi usando R da T-SQL o stored procedure con SQL Server</span><span class="sxs-lookup"><span data-stu-id="4913d-114">Predict taxi tips using R from T-SQL or stored procedures with SQL Server</span></span>

<span data-ttu-id="4913d-115">La procedura dettagliata relativa a [R e SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) offre ai programmatori SQL indicazioni per la compilazione di una soluzione di analisi avanzata con Transact-SQL usando i servizi R per SQL Server per rendere operativa una soluzione R.</span><span class="sxs-lookup"><span data-stu-id="4913d-115">The [Data science walkthrough for R and SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/walkthrough-data-science-end-to-end-walkthrough) provides SQL programmers with experience building an advanced analytics solution with Transact-SQL using SQL Server R Services to operationalize an R solution.</span></span> 


## <a name="predict-taxi-tips-using-python-in-sql-server-stored-procedures"></a><span data-ttu-id="4913d-116">Stimare le mance dei taxi usando Python in stored procedure SQL Server</span><span class="sxs-lookup"><span data-stu-id="4913d-116">Predict taxi tips using Python in SQL Server stored procedures</span></span>

<span data-ttu-id="4913d-117">La procedura dettagliata relativa all'[uso di T-SQL con i servizi Python per SQL Server](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) offre ai programmatori SQL indicazioni per la compilazione di una soluzione di apprendimento automatico in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4913d-117">The [Use T-SQL with SQL Server Python Services](https://docs.microsoft.com/en-us/sql/advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers) walkthrough provides SQL programmers with experience building a machine learning solution in SQL Server.</span></span> <span data-ttu-id="4913d-118">Illustra come incorporare Python in un'applicazione aggiungendo il codice Python alle stored procedure.</span><span class="sxs-lookup"><span data-stu-id="4913d-118">It demonstrates how to incorporate Python into an application by adding Python code to stored procedures.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4913d-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4913d-119">Next steps</span></span>

<span data-ttu-id="4913d-120">Per una descrizione dei componenti principali che costituiscono il processo di data science per i team, vedere [Panoramica del processo di data science per i team](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4913d-120">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="4913d-121">Per una descrizione del ciclo di vita del processo di data science per i team che è possibile usare per definire la struttura dei progetti di data science, vedere [Ciclo di vita del processo di data science per i team](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="4913d-121">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="4913d-122">Il ciclo di vita descrive tutti i passaggi generalmente seguiti dai progetti in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4913d-122">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 