---
title: Elencare tutti i processi di Importazione/Esportazione di Azure | Documentazione Microsoft
description: Informazioni su come elencare tutti i processi del servizio Importazione/Esportazione di Azure in una sottoscrizione.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="0afde-103">Enumerazione dei processi nel servizio Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0afde-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="0afde-104">Per enumerare tutti i processi in una sottoscrizione, chiamare l'operazione [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List).</span><span class="sxs-lookup"><span data-stu-id="0afde-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="0afde-105">`List Jobs` restituisce un elenco dei processi nonché gli attributi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0afde-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="0afde-106">Tipo di processo (importazione o esportazione)</span><span class="sxs-lookup"><span data-stu-id="0afde-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="0afde-107">Stato corrente del processo</span><span class="sxs-lookup"><span data-stu-id="0afde-107">The current job state</span></span>

-   <span data-ttu-id="0afde-108">Account di archiviazione associato al processo</span><span class="sxs-lookup"><span data-stu-id="0afde-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="0afde-109">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0afde-109">Next steps</span></span>

* [<span data-ttu-id="0afde-110">Uso dell'API REST del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="0afde-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
