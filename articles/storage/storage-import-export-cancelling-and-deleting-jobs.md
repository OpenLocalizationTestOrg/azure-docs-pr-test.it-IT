---
title: aaaCancel ed eliminare un processo di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come toocancel ed eliminare i processi per hello servizio importazione/esportazione di Microsoft Azure.
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
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="8721f-103">Annullamento ed eliminazione dei processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8721f-103">Canceling and deleting Azure Import/Export jobs</span></span>

<span data-ttu-id="8721f-104">È possibile richiedere che un processo annullato prima che sia in hello `Packaging` stato dal chiamante hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione e impostazione hello `CancelRequested` elemento troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="8721f-104">You can request that a job be cancelled before it is in hello `Packaging` state by calling hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and setting hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="8721f-105">il processo di Hello verrà annullato con cadenza principio del best effort.</span><span class="sxs-lookup"><span data-stu-id="8721f-105">hello job will be cancelled on a best-effort basis.</span></span> <span data-ttu-id="8721f-106">Se le unità sono nel processo di hello di trasferimento dei dati, dati possono continuare toobe trasferiti anche dopo che è stato richiesto l'annullamento.</span><span class="sxs-lookup"><span data-stu-id="8721f-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="8721f-107">Un processo annullato passerà toohello `Completed` stato e verrà conservato per 90 giorni, a quel punto verrà eliminato.</span><span class="sxs-lookup"><span data-stu-id="8721f-107">A cancelled job will move toohello `Completed` state and be kept for 90 days, at which point it will be deleted.</span></span>

 <span data-ttu-id="8721f-108">toodelete un processo, chiamata hello [Elimina processo](/rest/api/storageimportexport/jobs#Jobs_Delete) operazione prima di hello processo venga spedito (*ad esempio*, durante il processo di hello hello `Creating` stato).</span><span class="sxs-lookup"><span data-stu-id="8721f-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (*i.e.*, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="8721f-109">È anche possibile eliminare un processo in questo caso hello `Completed` stato.</span><span class="sxs-lookup"><span data-stu-id="8721f-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="8721f-110">Dopo aver eliminato un processo, lo stato e le relative informazioni non saranno più accessibili tramite l'API REST hello o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8721f-110">After a job has been deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8721f-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8721f-111">Next steps</span></span>

* [<span data-ttu-id="8721f-112">Tramite l'API REST del servizio importazione/esportazione hello</span><span class="sxs-lookup"><span data-stu-id="8721f-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
