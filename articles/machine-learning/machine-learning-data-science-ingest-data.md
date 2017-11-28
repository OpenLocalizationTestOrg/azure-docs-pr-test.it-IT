---
title: dati aaaLoad in ambienti di archiviazione di Azure per analitica | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="cd3e5-103">Caricare i dati in ambienti di archiviazione per l'analisi</span><span class="sxs-lookup"><span data-stu-id="cd3e5-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="cd3e5-104">Processo di analisi scientifica dei dati di Team Hello richiede che dati caricamento o caricati in un'ampia gamma di archiviazione diversi ambienti toobe elaborato o analizzare in modo più appropriato hello in ogni fase del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="cd3e5-104">hello Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments toobe processed or analyzed in hello most appropriate way in each stage of hello process.</span></span> <span data-ttu-id="cd3e5-105">Le destinazioni dei dati più comunemente usate per l'elaborazione includono l'archiviazione BLOB di Azure, i database di SQL Azure, SQL Server nella macchina virtuale di Azure, HDInsight (Hadoop) e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cd3e5-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="cd3e5-106">Questo **menu** collegamenti tootopics che descrivono come dati tooingest in questi ambienti in cui i dati hello sono archiviati ed elaborati come destinazione.</span><span class="sxs-lookup"><span data-stu-id="cd3e5-106">This **menu** links tootopics that describe how tooingest data into these target environments where hello data is stored and processed.</span></span>

<span data-ttu-id="cd3e5-107">Le esigenze aziendali e tecnici, nonché percorso iniziale hello, formattazione e determina la dimensione dei dati agli ambienti di destinazione hello in quale hello toobe caricamento tooachieve hello obiettivi dell'analisi, è necessario dati.</span><span class="sxs-lookup"><span data-stu-id="cd3e5-107">Technical and business needs, as well as hello initial location, format and size of your data will determine hello target environments into which hello data needs toobe ingested tooachieve hello goals of your analysis.</span></span> <span data-ttu-id="cd3e5-108">Non è raro che un toobe di dati toorequire scenario spostata tra diversi ambienti tooachieve hello svariati tooconstruct necessarie attività un modello predittivo.</span><span class="sxs-lookup"><span data-stu-id="cd3e5-108">It is not uncommon for a scenario toorequire data toobe moved between several environments tooachieve hello variety of tasks required tooconstruct a predictive model.</span></span> <span data-ttu-id="cd3e5-109">Questa sequenza di attività può includere, ad esempio, l'esplorazione dei dati, la pre-elaborazione, la pulizia, il sottocampionamento e il training del modello.</span><span class="sxs-lookup"><span data-stu-id="cd3e5-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

