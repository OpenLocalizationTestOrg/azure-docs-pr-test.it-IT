---
title: Annullare ed eliminare un processo di Importazione/Esportazione di Azure | Documentazione Microsoft
description: Informazioni su come annullare ed eliminare i processi per il servizio Importazione/Esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="7ba8c-103">Annullamento ed eliminazione dei processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="7ba8c-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="7ba8c-104">È possibile richiedere che un processo venga annullato prima che entri nello stato `Packaging` chiamando l'operazione [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) e impostando l'elemento `CancelRequested` su `true`.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-104">You can request that a job be cancelled before it is in the `Packaging` state by calling the [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting the `CancelRequested` element to `true`.</span></span> <span data-ttu-id="7ba8c-105">Il processo verrà annullato nel modo più efficiente possibile.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-105">The job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="7ba8c-106">Se nelle unità è in corso il trasferimento dei dati, dati possono continuare a essere trasferiti anche dopo che è stato richiesto l'annullamento.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-106">If drives are in the process of transferring data, data may continue to be transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="7ba8c-107">Un processo annullato passa nello stato `Completed` e vi rimane per 90 giorni, dopo i quali verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-107">A cancelled job will move to the `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="7ba8c-108">Per eliminare un processo, chiamare l'operazione [Elimina processo](/rest/api/storageimportexport/jobs#Jobs_Delete) prima che questo venga inviato (*ad esempio*, mentre il processo si trova nello stato `Creating`).</span><span class="sxs-lookup"><span data-stu-id="7ba8c-108">To delete a job, call the [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before the job has shipped (*i.e.*, while the job is in the `Creating` state).</span></span> <span data-ttu-id="7ba8c-109">È possibile eliminare un processo anche quando è nello stato `Completed`.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-109">You can also delete a job when it is in the `Completed` state.</span></span> <span data-ttu-id="7ba8c-110">Dopo che un processo è stato eliminato, il relativo stato e le relative informazioni non saranno più accessibili tramite l'API REST o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7ba8c-110">After a job has been deleted, its information and status are no longer accessible via the REST API or the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba8c-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7ba8c-111">Next steps</span></span>

* [<span data-ttu-id="7ba8c-112">Uso dell'API REST del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="7ba8c-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
