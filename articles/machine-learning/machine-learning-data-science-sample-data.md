---
title: Campionare i dati in contenitori BLOB di Azure, SQL Server e nelle tabelle Hive | Documentazione Microsoft
description: Come esplorare i dati archiviati in vari ambienti di Azure.
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
ms.openlocfilehash: 0683be564a88ef54882e8d882d196851ecac243d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="297f0-103"><a name="heading"></a>Campionare i dati in contenitori BLOB di Azure, SQL Server e nelle tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="297f0-103"><a name="heading"></a>Sample data in Azure blob containers, SQL Server, and Hive tables</span></span>
<span data-ttu-id="297f0-104">Questo documento include collegamenti ad argomenti che trattano come campionare i dati archiviati in uno fra tre diversi percorsi di Azure:</span><span class="sxs-lookup"><span data-stu-id="297f0-104">This document links to topics that covers how to sample data that is stored in one of three different Azure locations:</span></span>

* <span data-ttu-id="297f0-105">**I dati del contenitore BLOB di Azure** vengono campionati scaricandoli a livello di programmazione ed eseguendo il successivo campionamento usando un codice Python di esempio.</span><span class="sxs-lookup"><span data-stu-id="297f0-105">**Azure blob container data** is sampled by downloading it programmatically and then sampling it with sample Python code.</span></span>
* <span data-ttu-id="297f0-106">**Dati di SQL Server** vengono campionati utilizzando sia il linguaggio di programmazione Python che SQL.</span><span class="sxs-lookup"><span data-stu-id="297f0-106">**SQL Server data** is sampled using both SQL and the Python Programming Language.</span></span> 
* <span data-ttu-id="297f0-107">**Dati della tabella hive** vengono campionati utilizzando le query Hive.</span><span class="sxs-lookup"><span data-stu-id="297f0-107">**Hive table data** is sampled using Hive queries.</span></span>

<span data-ttu-id="297f0-108">Il **menu** seguente contiene collegamenti ad argomenti che descrivono come campionare i dati da ognuno di questi ambienti di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="297f0-108">The following **menu** links to the topics that describe how to sample data from each of these Azure storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="297f0-109">Questo campionamento è un passaggio del [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="297f0-109">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="297f0-110">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="297f0-110">**Why sample data?**</span></span>

<span data-ttu-id="297f0-111">Se il set di dati da analizzare è grande, è in genere opportuno sottocampionare i dati per ridurlo e ottenere dimensioni inferiori più facilmente gestibili ma comunque rappresentative.</span><span class="sxs-lookup"><span data-stu-id="297f0-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="297f0-112">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="297f0-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="297f0-113">Il suo ruolo nel Cortana Analytics Process consiste nell'abilitare la creazione relativa a prototipi di funzioni di elaborazione dei dati e di modelli per l'apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="297f0-113">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

