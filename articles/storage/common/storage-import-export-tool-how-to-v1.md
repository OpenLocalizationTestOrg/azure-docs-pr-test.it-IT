---
title: Uso dello strumento Importazione/Esportazione di Azure - versione 1 | Documentazione Microsoft
description: Informazioni su come usare lo strumento Importazione/Esportazione per preparare i dischi rigidi per un processo di importazione o per ripristinare un processo di importazione o esportazione.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 4ce2273cc0dcc456c2edc8c5dd2fc22496f20380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool-classic-deployment-model"></a><span data-ttu-id="a455c-103">Utilizzo dello strumento di importazione/esportazione di Azure (modello di distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="a455c-103">Using the Azure Import/Export Tool (classic deployment model)</span></span>

<span data-ttu-id="a455c-104">Lo strumento Importazione/Esportazione di Azure (WAImportExport.exe) consente di creare e gestire i processi per il servizio Importazione/Esportazione di Azure e trasferire così grandi quantità di dati da e verso l'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a455c-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="a455c-105">Questa documentazione fa riferimento al modello di distribuzione classica dello strumento di importazione/esportazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a455c-105">This documentation is for the classic deployment model of the Azure Import/Export Tool.</span></span> <span data-ttu-id="a455c-106">Per informazioni sull'utilizzo della versione più recente dello strumento, vedere [Uso dello strumento di importazione/esportazione di Azure](../storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a455c-106">For information about using the most recent version of the tool, see [Using the Azure Import/Export Tool](../storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="a455c-107">Gli articoli seguenti mostrano come:</span><span class="sxs-lookup"><span data-stu-id="a455c-107">The following articles show you how to:</span></span>

- <span data-ttu-id="a455c-108">Installare e configurare lo strumento di importazione/esportazione.</span><span class="sxs-lookup"><span data-stu-id="a455c-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="a455c-109">Preparare i dischi rigidi per un processo di importazione di dati dalle unità dell'utente all'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="a455c-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="a455c-110">Esaminare lo stato di un processo con i file di log di copia.</span><span class="sxs-lookup"><span data-stu-id="a455c-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="a455c-111">Ripristinare un processo di importazione.</span><span class="sxs-lookup"><span data-stu-id="a455c-111">Repair an import job.</span></span> 
- <span data-ttu-id="a455c-112">Ripristinare un processo di esportazione.</span><span class="sxs-lookup"><span data-stu-id="a455c-112">Repair an export job.</span></span> 
- <span data-ttu-id="a455c-113">Risolvere i problemi relativi allo strumento di importazione/esportazione di Azure, in caso di problemi durante il processo.</span><span class="sxs-lookup"><span data-stu-id="a455c-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a455c-114">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a455c-114">Next steps</span></span>

* <span data-ttu-id="a455c-115">[Setting up the WAImportExport tool](../storage-import-export-tool-how-to.md) (Configurazione dello strumento WAImportExport)</span><span class="sxs-lookup"><span data-stu-id="a455c-115">[Setting up the WAImportExport tool](../storage-import-export-tool-how-to.md)</span></span>