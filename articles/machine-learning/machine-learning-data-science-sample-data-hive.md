---
title: Dati di esempio nelle tabelle Hive di Azure HDInsight | Microsoft Docs
description: Esecuzione del sotto-campionamento dei dati nelle tabelle Hive (Hadoop) di Azure HDInsight
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: d46297dfaf85976114fbf610803e5f1a997041e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="21782-103">Dati di esempio nelle tabelle Hive di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="21782-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="21782-104">In questo articolo, viene descritto come eseguire il downsampling dei dati archiviati nelle tabelle Hive di Azure HDInsight usando le query Hive.</span><span class="sxs-lookup"><span data-stu-id="21782-104">In this article, we describe how to down-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="21782-105">Vengono trattati i tre metodi di campionamento utilizzati più frequentemente:</span><span class="sxs-lookup"><span data-stu-id="21782-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="21782-106">Campionamento casuale uniforme</span><span class="sxs-lookup"><span data-stu-id="21782-106">Uniform random sampling</span></span>
* <span data-ttu-id="21782-107">Campionamento casuale per gruppi</span><span class="sxs-lookup"><span data-stu-id="21782-107">Random sampling by groups</span></span>
* <span data-ttu-id="21782-108">Campionamento stratificato</span><span class="sxs-lookup"><span data-stu-id="21782-108">Stratified sampling</span></span>

<span data-ttu-id="21782-109">Il **menu** seguente contiene collegamenti ad argomenti che descrivono come campionare dati di vari ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="21782-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="21782-110">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="21782-110">**Why sample your data?**</span></span>
<span data-ttu-id="21782-111">Se il set di dati da analizzare è grande, è in genere opportuno sottocampionare i dati per ridurlo e ottenere dimensioni inferiori più facilmente gestibili ma comunque rappresentative.</span><span class="sxs-lookup"><span data-stu-id="21782-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="21782-112">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="21782-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="21782-113">Il suo ruolo nel Processo di analisi scientifica dei dati per i team consiste nell'abilitare la creazione relativa a prototipi di funzioni di elaborazione dei dati e di modelli di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="21782-113">Its role in the Team Data Science Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="21782-114">Questo campionamento è un passaggio del [Processo di analisi scientifica dei dati per i team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="21782-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-to-submit-hive-queries"></a><span data-ttu-id="21782-115">Come inviare query Hive</span><span class="sxs-lookup"><span data-stu-id="21782-115">How to submit Hive queries</span></span>
<span data-ttu-id="21782-116">Le query Hive possono essere inviate dalla console della riga di comando di Hadoop nel nodo head del cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="21782-116">Hive queries can be submitted from the Hadoop Command Line console on the head node of the Hadoop cluster.</span></span> <span data-ttu-id="21782-117">Per effettuare questa operazione, accedere al nodo head del cluster Hadoop, aprire la console della riga di comando e inviare le query Hive da tale posizione.</span><span class="sxs-lookup"><span data-stu-id="21782-117">To do this, log into the head node of the Hadoop cluster, open the Hadoop Command Line console, and submit the Hive queries from there.</span></span> <span data-ttu-id="21782-118">Per istruzioni su come inviare le query Hive nella console della riga di comando di Hadoop, vedere [Come inviare le query Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="21782-118">For instructions on submitting Hive queries in the Hadoop Command Line console, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="21782-119"><a name="uniform"></a> Campionamento casuale uniforme</span><span class="sxs-lookup"><span data-stu-id="21782-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="21782-120">Nel campionamento casuale uniforme tutte le righe del set di dati hanno la stessa possibilità di essere sottoposte a campionamento.</span><span class="sxs-lookup"><span data-stu-id="21782-120">Uniform random sampling means that each row in the data set has an equal chance of being sampled.</span></span> <span data-ttu-id="21782-121">Tale metodo può essere implementato aggiungendo un ulteriore campo casuale () al set di dati relativo alla query "select" interna e a quella "select" esterna che condizionano il campo casuale.</span><span class="sxs-lookup"><span data-stu-id="21782-121">This can be implemented by adding an extra field rand() to the data set in the inner "select" query, and in the outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="21782-122">Di seguito è fornito un esempio di query:</span><span class="sxs-lookup"><span data-stu-id="21782-122">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

<span data-ttu-id="21782-123">In questo caso, `<sample rate, 0-1>` indica la proporzione di record che gli utenti desiderano campionare.</span><span class="sxs-lookup"><span data-stu-id="21782-123">Here, `<sample rate, 0-1>` specifies the proportion of records that the users want to sample.</span></span>

## <span data-ttu-id="21782-124"><a name="group"></a> Campionamento casuale per gruppi</span><span class="sxs-lookup"><span data-stu-id="21782-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="21782-125">Quando si esegue il campionamento dei dati di categoria, è possibile scegliere di includere o di escludere tutte le istanze di un determinato valore di una variabile di categoria.</span><span class="sxs-lookup"><span data-stu-id="21782-125">When sampling categorical data, you may want to either include or exclude all of the instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="21782-126">Questo è il significato di "campionamento per gruppi".</span><span class="sxs-lookup"><span data-stu-id="21782-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="21782-127">Ad esempio, se si dispone di variabile di categoria "State" con valori quali NY, MA, CA, NJ, PA e così via, è possibile che l'utente desideri che i record dello stesso stato siano sempre visualizzati insieme, che siano campionati o meno.</span><span class="sxs-lookup"><span data-stu-id="21782-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of the same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="21782-128">Di seguito è presentata una query di esempio che consente di eseguire il campionamento per gruppi:</span><span class="sxs-lookup"><span data-stu-id="21782-128">Here is an example query that samples by group:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <span data-ttu-id="21782-129"><a name="stratified"></a> Campionamento stratificato</span><span class="sxs-lookup"><span data-stu-id="21782-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="21782-130">Il campionamento casuale è stratificato rispetto a una variabile di categoria, nel caso in cui i campioni ottenuti presentino, per quella categoria, valori di proporzione equivalente a quelli del popolamento padre dal quale sono stati ottenuti i campioni.</span><span class="sxs-lookup"><span data-stu-id="21782-130">Random sampling is stratified with respect to a categorical variable when the samples obtained have values of that categorical that are in the same ratio as in the parent population from which the samples were obtained.</span></span> <span data-ttu-id="21782-131">Usando lo stesso esempio precedente, si supponga che i dati dispongano di un popolamento secondario in base allo stato. Ad esempio, NJ dispone di 100 osservazioni, NY dispone di 60 osservazioni e WA di 300 osservazioni.</span><span class="sxs-lookup"><span data-stu-id="21782-131">Using the same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="21782-132">Se si specifica che la proporzione del campionamento stratificato sia pari a 0,5, il campione ottenuto deve disporre all'incirca di 50, 30 e 150 osservazioni per NJ, NY e WA</span><span class="sxs-lookup"><span data-stu-id="21782-132">If you specify the rate of stratified sampling to be 0.5, then the sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="21782-133">Di seguito è fornito un esempio di query:</span><span class="sxs-lookup"><span data-stu-id="21782-133">Here is an example query:</span></span>

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


<span data-ttu-id="21782-134">Per informazioni su metodi di campionamento più avanzati disponibili in Hive, vedere [Campionamento di LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="21782-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

