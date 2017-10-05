---
title: Informazioni di riferimento rapido sui comandi per i processi di importazione dello strumento Importazione/Esportazione di Azure | Documentazione Microsoft
description: Guida di riferimento per i comandi dello strumento Importazione/Esportazione di Azure usati di frequente per i processi di importazione.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: d51ae35ead0e7d8289de663e5b7b48d28271e810
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="793b5-103">Informazioni di riferimento rapido sui comandi di uso frequente per i processi di importazione</span><span class="sxs-lookup"><span data-stu-id="793b5-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="793b5-104">Questo articolo contiene informazioni di riferimento rapido su alcuni comandi di uso frequente.</span><span class="sxs-lookup"><span data-stu-id="793b5-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="793b5-105">Per informazioni dettagliate sull'uso, vedere [Preparazione dei dischi rigidi per un processo di importazione](../storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="793b5-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="793b5-106">Prima sessione</span><span class="sxs-lookup"><span data-stu-id="793b5-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="793b5-107">Seconda sessione</span><span class="sxs-lookup"><span data-stu-id="793b5-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="793b5-108">Interrompere l'ultima sessione</span><span class="sxs-lookup"><span data-stu-id="793b5-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="793b5-109">Riprendere l'ultima sessione interrotta</span><span class="sxs-lookup"><span data-stu-id="793b5-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-to-latest-session"></a><span data-ttu-id="793b5-110">Aggiungere unità all'ultima sessione</span><span class="sxs-lookup"><span data-stu-id="793b5-110">Add drives to latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="793b5-111">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="793b5-111">Next steps</span></span>

* <span data-ttu-id="793b5-112">[Sample workflow to prepare hard drives for an import job](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) (Flusso di lavoro campione per preparare i dischi rigidi per un processo di importazione)</span><span class="sxs-lookup"><span data-stu-id="793b5-112">[Sample workflow to prepare hard drives for an import job](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)</span></span>
