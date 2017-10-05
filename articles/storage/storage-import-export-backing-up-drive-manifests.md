---
title: "Backup dei manifesti delle unità di Importazione/Esportazione | Documentazione Microsoft"
description: "Informazioni su come impostare il backup automatico dei manifesti delle unità per il servizio Importazione/Esportazione di Microsoft Azure."
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
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="a400c-103">Backup dei manifesti delle unità per i processi di Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a400c-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="a400c-104">È possibile eseguire il backup automatico dei manifesti delle unità in BLOB impostando la proprietà `BackupDriveManifest` su `true` nelle operazioni dell'API REST [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="a400c-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="a400c-105">Per impostazione predefinita non viene eseguito il backup dei manifesti delle unità.</span><span class="sxs-lookup"><span data-stu-id="a400c-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="a400c-106">I relativi backup vengono archiviati come BLOB in blocchi in un contenitore nell'account di archiviazione associato al processo.</span><span class="sxs-lookup"><span data-stu-id="a400c-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="a400c-107">Per impostazione predefinita, il nome del contenitore è `waimportexport`, ma è possibile specificare un nome diverso nella proprietà `DiagnosticsPath` quando si chiamano le operazioni `Put Job` o `Update Job Properties`.</span><span class="sxs-lookup"><span data-stu-id="a400c-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="a400c-108">Il BLOB dei manifesti di backup vengono denominati con il seguente formato: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a400c-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="a400c-109">È possibile recuperare l'URI dei manifesti delle unità di backup per un processo chiamando l'operazione [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="a400c-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="a400c-110">L'URI del BLOB viene restituito nella proprietà `ManifestUri` per ciascuna unità.</span><span class="sxs-lookup"><span data-stu-id="a400c-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a400c-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a400c-111">Next steps</span></span>

* [<span data-ttu-id="a400c-112">Uso dell'API REST del servizio Importazione/Esportazione</span><span class="sxs-lookup"><span data-stu-id="a400c-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
