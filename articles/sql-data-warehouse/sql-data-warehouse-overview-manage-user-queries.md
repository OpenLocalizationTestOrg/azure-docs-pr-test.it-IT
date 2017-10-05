---
title: Monitorare le query utente in Azure SQL Data Warehouse | Documentazione Microsoft
description: "Panoramica delle considerazioni, delle procedure consigliate e delle attività per il monitoraggio delle query utente in Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 65509a65c2b34553822cc02d7a7fa5a614adc57f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="c0c99-103">Monitorare le query utente in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c0c99-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="c0c99-104">Panoramica delle considerazioni, delle procedure consigliate e delle attività per il monitoraggio delle query utente in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c0c99-104">Overview of the considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="c0c99-105">Categoria</span><span class="sxs-lookup"><span data-stu-id="c0c99-105">Category</span></span> | <span data-ttu-id="c0c99-106">Attività o considerazione</span><span class="sxs-lookup"><span data-stu-id="c0c99-106">Task or consideration</span></span> | <span data-ttu-id="c0c99-107">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c0c99-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c0c99-108">Rallentamento delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="c0c99-108">Slow performance</span></span> |<span data-ttu-id="c0c99-109">Trovare una query utente con esecuzione prolungata</span><span class="sxs-lookup"><span data-stu-id="c0c99-109">Find a long-running user query</span></span> |<span data-ttu-id="c0c99-110">[Trovare query con esecuzione prolungata][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="c0c99-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="c0c99-111">Concorrenza</span><span class="sxs-lookup"><span data-stu-id="c0c99-111">Concurrency</span></span> |<span data-ttu-id="c0c99-112">Assegnare risorse simultanee a query utente</span><span class="sxs-lookup"><span data-stu-id="c0c99-112">Assign concurrent resources to user queries</span></span> |<span data-ttu-id="c0c99-113">[Gestione della concorrenza e del carico di lavoro][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="c0c99-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c0c99-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0c99-114">Next steps</span></span>
<span data-ttu-id="c0c99-115">Per altri suggerimenti relativi alla gestione, andare alla [Panoramica della gestione][Management overview].</span><span class="sxs-lookup"><span data-stu-id="c0c99-115">For more management tips, head over to the [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
