---
title: dati aaaSample in Azure contenitori, SQL Server, blob e tabelle Hive | Documenti Microsoft
description: "Modalità di archiviazione in vari enviromnents Azure tooexplore dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="861bc-103"><a name="heading"></a>Campionare i dati in contenitori BLOB di Azure, SQL Server e nelle tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="861bc-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="861bc-104">Questo documento collega tootopics che illustra come toosample i dati archiviati in uno dei tre percorsi diversi di Azure:</span><span class="sxs-lookup"><span data-stu-id="861bc-104">This document links tootopics that covers how toosample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="861bc-105">**I dati del contenitore BLOB di Azure** vengono campionati scaricandoli a livello di programmazione ed eseguendo il successivo campionamento usando un codice Python di esempio.</span><span class="sxs-lookup"><span data-stu-id="861bc-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="861bc-106">**Dati di SQL Server** campionato utilizzando il linguaggio di programmazione Python hello e SQL.</span><span class="sxs-lookup"><span data-stu-id="861bc-106">**SQL Server data** is sampled using both SQL and hello Python Programming Language.</span></span> 
* <span data-ttu-id="861bc-107">**Dati della tabella hive** vengono campionati utilizzando le query Hive.</span><span class="sxs-lookup"><span data-stu-id="861bc-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="861bc-108">esempio Hello **menu** collegamenti toohello argomenti che descrivono come dati toosample da ognuno di questi ambienti di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="861bc-108">hello following **menu** links toohello topics that describe how toosample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="861bc-109">Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="861bc-109">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="861bc-110">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="861bc-110">**Why sample data?**</span></span>

<span data-ttu-id="861bc-111">Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni.</span><span class="sxs-lookup"><span data-stu-id="861bc-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="861bc-112">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="861bc-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="861bc-113">Il relativo ruolo nel processo di Cortana Analitica hello è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.</span><span class="sxs-lookup"><span data-stu-id="861bc-113">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

