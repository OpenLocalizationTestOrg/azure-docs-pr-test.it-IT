---
title: Procedure dettagliate di data science per HDInsight Hadoop con Hive in Azure | Microsoft Docs
description: Esempi del processo di data science per i team che descrive l'uso di Hive in Azure HDInsight Hadoop per eseguire analisi predittive.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="c8fdc-103">Procedure dettagliate di data science per HDInsight Hadoop con Hive in Azure</span><span class="sxs-lookup"><span data-stu-id="c8fdc-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="c8fdc-104">Queste procedure dettagliate usano Hive con un cluster HDInsight Hadoop per eseguire analisi predittive.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="c8fdc-105">Seguono i passaggi descritti nel processo di data science per i team.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="c8fdc-106">Per una panoramica del processo di data science per i team, vedere [Processo di data science](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8fdc-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="c8fdc-107">Per un'introduzione ad Azure HDInsight, vedere [Introduzione ad Azure HDInsight, allo stack di tecnologie Hadoop e ai cluster Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8fdc-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="c8fdc-108">Le procedure dettagliate di data science aggiuntive che eseguono il processo di data science per i team sono raggruppate in base alla **piattaforma** che usano:</span><span class="sxs-lookup"><span data-stu-id="c8fdc-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="c8fdc-109">Stimare le mance dei taxi usando Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8fdc-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="c8fdc-110">La procedura dettagliata [Usare cluster HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) utilizza i dati relativi ai taxi di New York per prevedere:</span><span class="sxs-lookup"><span data-stu-id="c8fdc-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="c8fdc-111">Se viene lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="c8fdc-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="c8fdc-112">La distribuzione degli importi delle mance</span><span class="sxs-lookup"><span data-stu-id="c8fdc-112">The distribution of tip amounts</span></span>

<span data-ttu-id="c8fdc-113">Lo scenario viene implementato usando Hive con un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c8fdc-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="c8fdc-114">Viene illustrato come archiviare ed esplorare i dati e progettarne le funzionalità da un set di dati relativo a corse e tariffe dei taxi di NYC disponibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="c8fdc-115">Si usa inoltre Azure Machine Learning per compilare e distribuire i modelli.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="c8fdc-116">Stimare i clic sugli annunci usando Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8fdc-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="c8fdc-117">La procedura dettagliata [Usare cluster Hadoop di Azure HDInsight in un set di dati da 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) usa un set di dati relativo ai clic su [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) disponibile pubblicamente per stimare se viene lasciata una mancia e l'intervallo di importi previsto.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="c8fdc-118">Lo scenario viene implementato usando Hive con un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) per archiviare ed esplorare i dati di esempio nonché progettarne le funzionalità e sottocampionarli.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="c8fdc-119">Usa Azure Machine Learning per compilare, eseguire il training e assegnare un punteggio a un modello di classificazione binario che prevede se un utente fa clic su un annuncio.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="c8fdc-120">La procedura dettagliata si conclude illustrando come pubblicare uno di questi modelli come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c8fdc-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8fdc-121">Next steps</span></span>

<span data-ttu-id="c8fdc-122">Per una descrizione dei componenti principali che costituiscono il processo di data science per i team, vedere [Panoramica del processo di data science per i team](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c8fdc-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="c8fdc-123">Per una descrizione del ciclo di vita del processo di data science per i team che è possibile usare per definire la struttura dei progetti di data science, vedere [Ciclo di vita del processo di data science per i team](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="c8fdc-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="c8fdc-124">Il ciclo di vita descrive tutti i passaggi generalmente seguiti dai progetti in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c8fdc-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

