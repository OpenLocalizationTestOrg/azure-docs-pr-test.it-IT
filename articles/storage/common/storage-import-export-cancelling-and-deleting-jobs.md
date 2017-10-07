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
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="33a56-103">Annullamento ed eliminazione dei processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="33a56-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="33a56-104">toorequest che un processo annullato prima che si trova in hello `Packaging` stato, chiamata hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione e set hello `CancelRequested` elemento troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="33a56-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="33a56-105">Hello processi vengono annullati su base principio del best effort.</span><span class="sxs-lookup"><span data-stu-id="33a56-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="33a56-106">Se le unità sono nel processo di hello di trasferimento dei dati, dati possono continuare toobe trasferiti anche dopo che è stato richiesto l'annullamento.</span><span class="sxs-lookup"><span data-stu-id="33a56-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="33a56-107">Un processo annullato viene spostata toohello `Completed` stato e vengono mantenuti per 90 giorni, a quel punto viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="33a56-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="33a56-108">toodelete un processo, chiamata hello [Elimina processo](/rest/api/storageimportexport/jobs#Jobs_Delete) operazione prima di hello processo venga spedito (vale a dire, durante il processo di hello hello `Creating` stato).</span><span class="sxs-lookup"><span data-stu-id="33a56-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="33a56-109">È anche possibile eliminare un processo in questo caso hello `Completed` stato.</span><span class="sxs-lookup"><span data-stu-id="33a56-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="33a56-110">Dopo l'eliminazione di un processo, lo stato e le relative informazioni non saranno più accessibili tramite l'API REST hello o hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="33a56-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33a56-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33a56-111">Next steps</span></span>

* [<span data-ttu-id="33a56-112">Tramite l'API REST del servizio importazione/esportazione hello</span><span class="sxs-lookup"><span data-stu-id="33a56-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
