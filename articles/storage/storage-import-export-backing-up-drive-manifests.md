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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Backup dei manifesti delle unità per i processi di Importazione/Esportazione di Azure

Manifesti dell'unità è possibile eseguire automaticamente backup tooblobs dall'impostazione hello `BackupDriveManifest` proprietà troppo`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazioni dell'API REST. Per impostazione predefinita, manifesti dell'unità di hello non sottoposti a backup. Hello unità relativi backup vengono archiviati come BLOB in blocchi in un contenitore nell'account di archiviazione hello associata al processo hello. Per impostazione predefinita, il nome di contenitore hello è `waimportexport`, ma è possibile specificare un nome diverso in hello `DiagnosticsPath` proprietà quando si chiama hello `Put Job` o `Update Job Properties` operazioni. Hello blob del manifesto di backup sono denominati in hello seguente formato: `waies/jobname_driveid_timestamp_manifest.xml`.

 È possibile recuperare l'URI dell'unità di backup hello manifesti per un processo dal chiamante hello hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione. blob Hello viene restituito l'URI in hello `ManifestUri` proprietà per ogni unità.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
