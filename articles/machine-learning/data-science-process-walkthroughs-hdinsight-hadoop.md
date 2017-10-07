---
title: procedure dettagliate dell'analisi scientifica dei dati Hadoop aaaHDInsight con Hive in Azure | Documenti Microsoft
description: Esempi di hello processo di analisi scientifica dei dati di Team che indicano l'utilizzo hello di Hive in Azure HDInsight Hadoop toodo predittiva analitica.
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
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="b24dd-103">Procedure dettagliate di data science per HDInsight Hadoop con Hive in Azure</span><span class="sxs-lookup"><span data-stu-id="b24dd-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="b24dd-104">Queste procedure dettagliate utilizzano Hive con un analitica predittiva di cluster toodo HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b24dd-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="b24dd-105">Le funzioni seguono hello procedure hello processo di analisi scientifica dei dati del Team.</span><span class="sxs-lookup"><span data-stu-id="b24dd-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="b24dd-106">Per una panoramica del processo di analisi scientifica dei dati di Team hello, vedere [il processo di analisi scientifica dei dati](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b24dd-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="b24dd-107">Per un'introduzione tooAzure HDInsight, vedere [tooAzure introduzione HDInsight, hello Hadoop allo stack di tecnologie e i cluster Hadoop](../hdinsight/hdinsight-hadoop-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b24dd-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="b24dd-108">Procedure dettagliate di analisi scientifica dei dati aggiuntivi che eseguono hello processo di analisi scientifica dei dati di Team vengono raggruppate in hello **piattaforma** che utilizzano:</span><span class="sxs-lookup"><span data-stu-id="b24dd-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="b24dd-109">Stimare le mance dei taxi usando Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="b24dd-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="b24dd-110">Hello [cluster utilizzare HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) procedura dettagliata Usa i dati di New York taxi toopredict:</span><span class="sxs-lookup"><span data-stu-id="b24dd-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="b24dd-111">Se viene lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="b24dd-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="b24dd-112">distribuzione di Hello degli importi di suggerimento</span><span class="sxs-lookup"><span data-stu-id="b24dd-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="b24dd-113">scenario di Hello viene implementato utilizzando Hive con un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b24dd-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="b24dd-114">Viene descritta la modalità toostore, esplorare e tecnico dati da un disponibile pubblicamente trip taxi NYC caratteristiche e presentare set di dati.</span><span class="sxs-lookup"><span data-stu-id="b24dd-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="b24dd-115">Inoltre, utilizzare toobuild Azure Machine Learning e distribuire modelli hello.</span><span class="sxs-lookup"><span data-stu-id="b24dd-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="b24dd-116">Stimare i clic sugli annunci usando Hive con HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="b24dd-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="b24dd-117">Hello [cluster HDInsight Hadoop Azure di utilizzare un set di dati di 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md) procedura dettagliata viene utilizzato un documento disponibile pubblicamente [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) fare clic su set di dati toopredict se un suggerimento di pagamento e hello intervallo di quantità prevista.</span><span class="sxs-lookup"><span data-stu-id="b24dd-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="b24dd-118">scenario di Hello viene implementato utilizzando Hive con un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, esplorare, funzionalità tecnico e verso il basso di dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="b24dd-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="b24dd-119">Usa toobuild Azure Machine Learning, eseguire il training e assegnare un punteggio stimare se un utente fa clic su un annuncio di un modello di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="b24dd-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="b24dd-120">procedura dettagliata Hello conclude che mostra come toopublish uno di questi modelli come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="b24dd-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b24dd-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b24dd-121">Next steps</span></span>

<span data-ttu-id="b24dd-122">Per una descrizione dei componenti principali di hello che costituiscono hello processo di analisi scientifica dei dati di Team, vedere [Cenni preliminari sul processo di analisi scientifica dei dati di Team](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b24dd-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="b24dd-123">Per una descrizione del ciclo di vita di processo di analisi scientifica dei dati di Team hello che è possibile utilizzare toostructure i progetti di analisi scientifica dei dati, vedere [ciclo di vita del processo di analisi scientifica dei dati di Team](data-science-process-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="b24dd-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="b24dd-124">ciclo di vita Hello descrive i passaggi di hello, dall'inizio toofinish, i progetti seguenti in genere quando vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="b24dd-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

