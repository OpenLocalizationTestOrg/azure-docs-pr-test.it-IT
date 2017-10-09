---
title: aaaSample dati nelle tabelle di Azure HDInsight Hive | Documenti Microsoft
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
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a><span data-ttu-id="9b2d1-103">Dati di esempio nelle tabelle Hive di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b2d1-103">Sample data in Azure HDInsight Hive tables</span></span>
<span data-ttu-id="9b2d1-104">In questo articolo vengono descritte come toodown-esempio dati archiviati nelle tabelle di Azure HDInsight Hive usano query Hive.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-104">In this article, we describe how toodown-sample data stored in Azure HDInsight Hive tables using Hive queries.</span></span> <span data-ttu-id="9b2d1-105">Vengono trattati i tre metodi di campionamento utilizzati più frequentemente:</span><span class="sxs-lookup"><span data-stu-id="9b2d1-105">We cover three popularly used sampling methods:</span></span>

* <span data-ttu-id="9b2d1-106">Campionamento casuale uniforme</span><span class="sxs-lookup"><span data-stu-id="9b2d1-106">Uniform random sampling</span></span>
* <span data-ttu-id="9b2d1-107">Campionamento casuale per gruppi</span><span class="sxs-lookup"><span data-stu-id="9b2d1-107">Random sampling by groups</span></span>
* <span data-ttu-id="9b2d1-108">Campionamento stratificato</span><span class="sxs-lookup"><span data-stu-id="9b2d1-108">Stratified sampling</span></span>

<span data-ttu-id="9b2d1-109">esempio Hello **menu** collegamenti tootopics che descrivono come toosample dati da diversi ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span>

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="9b2d1-110">**Perché campionare i dati?**</span><span class="sxs-lookup"><span data-stu-id="9b2d1-110">**Why sample your data?**</span></span>
<span data-ttu-id="9b2d1-111">Se si prevede di tooanalyze set di dati hello è grande, è in genere un tooreduce di dati di buona toodown esempio hello è tooa più piccolo ma rappresentativo e gestibile dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="9b2d1-112">Questa operazione facilita la comprensione e l'esplorazione dei dati, nonché la progettazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="9b2d1-113">Il relativo ruolo nel processo di analisi scientifica dei dati di Team hello è tooenable rapida la creazione di prototipi di funzioni di elaborazione dei dati hello e modelli di machine learning.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-113">Its role in hello Team Data Science Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="9b2d1-114">Questa attività di campionamento è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="9b2d1-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="how-toosubmit-hive-queries"></a><span data-ttu-id="9b2d1-115">La modalità query Hive toosubmit</span><span class="sxs-lookup"><span data-stu-id="9b2d1-115">How toosubmit Hive queries</span></span>
<span data-ttu-id="9b2d1-116">È possibile inviare query hive dalla console di riga di comando Hadoop hello nel nodo head di hello del cluster Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-116">Hive queries can be submitted from hello Hadoop Command Line console on hello head node of hello Hadoop cluster.</span></span> <span data-ttu-id="9b2d1-117">toodo questa operazione, accedere al nodo head di hello del cluster Hadoop hello, aprire console della riga di comando Hadoop hello e inviare query Hive hello da qui.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-117">toodo this, log into hello head node of hello Hadoop cluster, open hello Hadoop Command Line console, and submit hello Hive queries from there.</span></span> <span data-ttu-id="9b2d1-118">Per istruzioni sull'invio di query Hive nella console della riga di comando Hadoop hello, vedere [come tooSubmit query Hive](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="9b2d1-118">For instructions on submitting Hive queries in hello Hadoop Command Line console, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="9b2d1-119"><a name="uniform"></a> Campionamento casuale uniforme</span><span class="sxs-lookup"><span data-stu-id="9b2d1-119"><a name="uniform"></a> Uniform random sampling</span></span>
<span data-ttu-id="9b2d1-120">Campionamento casuale Uniform significa che ogni riga nel set di dati hello stessa probabilità di in fase di campionamento.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-120">Uniform random sampling means that each row in hello data set has an equal chance of being sampled.</span></span> <span data-ttu-id="9b2d1-121">Questo può essere implementata tramite l'aggiunta di un set di dati campo aggiuntivo toohello rand () in query "select" interna hello e hello query "select" esterna tale condizione su quel campo casuale.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-121">This can be implemented by adding an extra field rand() toohello data set in hello inner "select" query, and in hello outer "select" query that condition on that random field.</span></span>

<span data-ttu-id="9b2d1-122">Di seguito è fornito un esempio di query:</span><span class="sxs-lookup"><span data-stu-id="9b2d1-122">Here is an example query:</span></span>

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

<span data-ttu-id="9b2d1-123">In questo caso, `<sample rate, 0-1>` specifica la proporzione di hello di record che gli utenti di hello desiderano toosample.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-123">Here, `<sample rate, 0-1>` specifies hello proportion of records that hello users want toosample.</span></span>

## <span data-ttu-id="9b2d1-124"><a name="group"></a> Campionamento casuale per gruppi</span><span class="sxs-lookup"><span data-stu-id="9b2d1-124"><a name="group"></a> Random sampling by groups</span></span>
<span data-ttu-id="9b2d1-125">Quando i dati di campionamento per categoria, è opportuno tooeither includere o escludere tutte le istanze di hello di un valore specifico di una variabile per categoria.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-125">When sampling categorical data, you may want tooeither include or exclude all of hello instances of some particular value of a categorical variable.</span></span> <span data-ttu-id="9b2d1-126">Questo è il significato di "campionamento per gruppi".</span><span class="sxs-lookup"><span data-stu-id="9b2d1-126">This is what is meant by "sampling by group".</span></span>
<span data-ttu-id="9b2d1-127">Ad esempio, se si dispone di una variabile categorica, "Stato", che ha valori NY AG, Canada, NJ, PA, e così via, che si desidera record di hello stesso stato sempre essere insieme, se vengono campionate o non.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-127">For example, if you have a categorical variable "State", which has values NY, MA, CA, NJ, PA, etc, you want records of hello same state be always together, whether they are sampled or not.</span></span>

<span data-ttu-id="9b2d1-128">Di seguito è presentata una query di esempio che consente di eseguire il campionamento per gruppi:</span><span class="sxs-lookup"><span data-stu-id="9b2d1-128">Here is an example query that samples by group:</span></span>

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

## <span data-ttu-id="9b2d1-129"><a name="stratified"></a> Campionamento stratificato</span><span class="sxs-lookup"><span data-stu-id="9b2d1-129"><a name="stratified"></a>Stratified sampling</span></span>
<span data-ttu-id="9b2d1-130">Campionamento casuale è stratificato con riguardo tooa categorico variabile quando i valori di categoria che devono di esempi di hello ottenuti in hello stesso rapporto come popolamento padre hello ottenuti dal quale hello esempi.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-130">Random sampling is stratified with respect tooa categorical variable when hello samples obtained have values of that categorical that are in hello same ratio as in hello parent population from which hello samples were obtained.</span></span> <span data-ttu-id="9b2d1-131">Utilizzando hello stesso esempio precedente, si supponga che i dati con popolazioni secondario gli stati, ad esempio NJ ha 100 osservazioni, NY è 60 osservazioni, e WA con 300 osservazioni.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-131">Using hello same example as above, suppose your data has sub-populations by states, say NJ has 100 observations, NY has 60 observations, and WA has 300 observations.</span></span> <span data-ttu-id="9b2d1-132">Se la frequenza di hello di campionamento toobe 0,5 stratificata, quindi hello ottenuto deve essere circa 50, 30 e 150 osservazioni di NJ NY e WA rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="9b2d1-132">If you specify hello rate of stratified sampling toobe 0.5, then hello sample obtained should have approximately 50, 30, and 150 observations of NJ, NY, and WA respectively.</span></span>

<span data-ttu-id="9b2d1-133">Di seguito è fornito un esempio di query:</span><span class="sxs-lookup"><span data-stu-id="9b2d1-133">Here is an example query:</span></span>

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


<span data-ttu-id="9b2d1-134">Per informazioni su metodi di campionamento più avanzati disponibili in Hive, vedere [Campionamento di LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span><span class="sxs-lookup"><span data-stu-id="9b2d1-134">For information on more advanced sampling methods that are available in Hive, see [LanguageManual Sampling](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).</span></span>

