---
title: Caricare i dati in ambienti di archiviazione di Azure per l'analisi | Documentazione Microsoft
description: Spostamento dei dati da e verso l'archiviazione BLOB di Azure
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
ms.openlocfilehash: 7fbf3bfedca8fa57a5e9428c9399558992b4acbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a><span data-ttu-id="47c75-103">Caricare i dati in ambienti di archiviazione per l'analisi</span><span class="sxs-lookup"><span data-stu-id="47c75-103">Load data into storage environments for analytics</span></span>
<span data-ttu-id="47c75-104">Il Processo di analisi scientifica dei dati per i team richiede l'inserimento o il caricamento di dati in una vasta gamma di ambienti di archiviazione diversi per l'elaborazione e l'analisi nei modi più appropriati in ogni fase del processo.</span><span class="sxs-lookup"><span data-stu-id="47c75-104">The Team Data Science Process requires that data be ingested or loaded into a variety of different storage environments to be processed or analyzed in the most appropriate way in each stage of the process.</span></span> <span data-ttu-id="47c75-105">Le destinazioni dei dati più comunemente usate per l'elaborazione includono l'archiviazione BLOB di Azure, i database di SQL Azure, SQL Server nella macchina virtuale di Azure, HDInsight (Hadoop) e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="47c75-105">Data destinations commonly used for processing include Azure Blob Storage, SQL Azure databases, SQL Server on Azure VM, HDInsight (Hadoop), and Azure Machine Learning.</span></span> 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="47c75-106">Questo **menu** si collega ad argomenti che descrivono come inserire dati in questi ambienti di destinazione dove i dati vengono archiviati ed elaborati.</span><span class="sxs-lookup"><span data-stu-id="47c75-106">This **menu** links to topics that describe how to ingest data into these target environments where the data is stored and processed.</span></span>

<span data-ttu-id="47c75-107">Le esigenze aziendali e tecniche specifiche, nonché la posizione iniziale, il formato e le dimensioni dei dati determinano gli ambienti di destinazione in cui i dati devono essere inseriti per raggiungere gli obiettivi dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="47c75-107">Technical and business needs, as well as the initial location, format and size of your data will determine the target environments into which the data needs to be ingested to achieve the goals of your analysis.</span></span> <span data-ttu-id="47c75-108">Non è insolito per uno scenario richiedere lo spostamento dei dati tra ambienti diversi per disporre di tutte le attività necessarie per creare un modello predittivo.</span><span class="sxs-lookup"><span data-stu-id="47c75-108">It is not uncommon for a scenario to require data to be moved between several environments to achieve the variety of tasks required to construct a predictive model.</span></span> <span data-ttu-id="47c75-109">Questa sequenza di attività può includere, ad esempio, l'esplorazione dei dati, la pre-elaborazione, la pulizia, il sottocampionamento e il training del modello.</span><span class="sxs-lookup"><span data-stu-id="47c75-109">This sequence of tasks can include, for example, data exploration, pre-processing, cleaning, down-sampling, and model training.</span></span>

