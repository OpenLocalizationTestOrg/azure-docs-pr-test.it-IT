---
title: "aaaBacking dei manifesti dell'unità di importazione/esportazione di Azure | Documenti Microsoft"
description: "Informazioni su come toohave manifesti di unità per il servizio di importazione/esportazione di Microsoft Azure hello automaticamente il backup."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="22cdd-103">Backup dei manifesti delle unità per i processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="22cdd-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="22cdd-104">Manifesti dell'unità è possibile eseguire automaticamente backup tooblobs dall'impostazione hello `BackupDriveManifest` proprietà troppo`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazioni dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="22cdd-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="22cdd-105">Per impostazione predefinita, manifesti dell'unità di hello non sottoposti a backup.</span><span class="sxs-lookup"><span data-stu-id="22cdd-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="22cdd-106">Hello unità relativi backup vengono archiviati come BLOB in blocchi in un contenitore nell'account di archiviazione hello associata al processo hello.</span><span class="sxs-lookup"><span data-stu-id="22cdd-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="22cdd-107">Per impostazione predefinita, il nome di contenitore hello è `waimportexport`, ma è possibile specificare un nome diverso in hello `DiagnosticsPath` proprietà quando si chiama hello `Put Job` o `Update Job Properties` operazioni.</span><span class="sxs-lookup"><span data-stu-id="22cdd-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="22cdd-108">Hello blob del manifesto di backup sono denominati in hello seguente formato: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="22cdd-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="22cdd-109">È possibile recuperare l'URI dell'unità di backup hello manifesti per un processo dal chiamante hello hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione.</span><span class="sxs-lookup"><span data-stu-id="22cdd-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="22cdd-110">blob Hello viene restituito l'URI in hello `ManifestUri` proprietà per ogni unità.</span><span class="sxs-lookup"><span data-stu-id="22cdd-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22cdd-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22cdd-111">Next steps</span></span>

* [<span data-ttu-id="22cdd-112">Tramite l'API REST del servizio importazione/esportazione hello</span><span class="sxs-lookup"><span data-stu-id="22cdd-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
