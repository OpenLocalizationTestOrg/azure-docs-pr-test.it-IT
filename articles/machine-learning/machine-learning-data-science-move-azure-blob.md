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
# <a name="move-data-tooand-from-azure-blob-storage"></a>Spostare dati tooand dall'archiviazione Blob di Azure
[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<!-- just in case, adding this tooseparate these two include references -->

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

Quale sia il metodo adatto dipenderà dallo scenario. Hello [scenari per analitica avanzate in Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md) articolo consente di determinare le risorse di hello necessarie per un'ampia gamma di flussi di lavoro di analisi scientifica dei dati utilizzati in hello avanzate processo analitica.

> [!NOTE]
> Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

In alternativa, è possibile utilizzare [Data factory di Azure](https://azure.microsoft.com/services/data-factory/) per: 

* creare e pianificare una pipeline che scarica i dati dall'archiviazione BLOB di Azure; 
* passarlo tooa pubblicati servizio web Azure Machine Learning, 
* ricevere i risultati di hello analitica predittiva, e 
* caricare toostorage risultati hello. 

Per altre informazioni, vedere [Creare pipeline predittive tramite Data factory di Azure e Azure Machine Learning](../data-factory/data-factory-azure-ml-batch-execution-activity.md).

## <a name="prerequisites"></a>Prerequisiti
Questo documento si presuppone la presenza di una sottoscrizione di Azure, un account di archiviazione e chiave di archiviazione per l'account corrispondente hello. Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.

* tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).

