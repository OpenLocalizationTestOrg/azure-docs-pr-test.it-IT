---
title: aaaMove tooand di dati dall'archiviazione Blob di Azure | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d6681e30-ab45-45ea-a9fb-ac8acefe544d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;sachouks
ms.openlocfilehash: e12b8c157955195e826f8b108075afaf25ca7bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage"></a><span data-ttu-id="86048-103">Spostare dati tooand dall'archiviazione Blob di Azure</span><span class="sxs-lookup"><span data-stu-id="86048-103">Move data tooand from Azure Blob Storage</span></span>
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

<span data-ttu-id="86048-104">Quale sia il metodo adatto dipenderà dallo scenario.</span><span class="sxs-lookup"><span data-stu-id="86048-104">Which method is best for you depends on your scenario.</span></span> <span data-ttu-id="86048-105">Hello [scenari per analitica avanzate in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) articolo consente di determinare le risorse di hello necessarie per un'ampia gamma di flussi di lavoro di analisi scientifica dei dati utilizzati in hello avanzate processo analitica.</span><span class="sxs-lookup"><span data-stu-id="86048-105">hello [Scenarios for advanced analytics in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) article helps you determine hello resources you need for a variety of data science workflows used in hello advanced analytics process.</span></span>

> [!NOTE]
> <span data-ttu-id="86048-106">Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="86048-106">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

<span data-ttu-id="86048-107">In alternativa, è possibile utilizzare [Data factory di Azure](https://azure.microsoft.com/services/data-factory/) per:</span><span class="sxs-lookup"><span data-stu-id="86048-107">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to:</span></span> 

* <span data-ttu-id="86048-108">creare e pianificare una pipeline che scarica i dati dall'archiviazione BLOB di Azure;</span><span class="sxs-lookup"><span data-stu-id="86048-108">create and schedule a pipeline that downloads data from Azure blob storage,</span></span> 
* <span data-ttu-id="86048-109">passarlo tooa pubblicati servizio web Azure Machine Learning,</span><span class="sxs-lookup"><span data-stu-id="86048-109">pass it tooa published Azure Machine Learning web service,</span></span> 
* <span data-ttu-id="86048-110">ricevere i risultati di hello analitica predittiva, e</span><span class="sxs-lookup"><span data-stu-id="86048-110">receive hello predictive analytics results, and</span></span> 
* <span data-ttu-id="86048-111">caricare toostorage risultati hello.</span><span class="sxs-lookup"><span data-stu-id="86048-111">upload hello results toostorage.</span></span> 

<span data-ttu-id="86048-112">Per altre informazioni, vedere [Creare pipeline predittive tramite Data factory di Azure e Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="86048-112">For more information, see [Create predictive pipelines using Azure Data Factory and Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86048-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="86048-113">Prerequisites</span></span>
<span data-ttu-id="86048-114">Questo documento si presuppone la presenza di una sottoscrizione di Azure, un account di archiviazione e chiave di archiviazione per l'account corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="86048-114">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="86048-115">Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="86048-115">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="86048-116">tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86048-116">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="86048-117">Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="86048-117">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

