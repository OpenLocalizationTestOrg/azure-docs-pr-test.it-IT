---
title: aaaExplore dati nelle tabelle Hive con query Hive | Documenti Microsoft
description: Esplorare i dati nelle tabelle Hive mediante le query Hive.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="2ca86-103">Esplorare i dati nelle tabelle Hive con  query Hive.</span><span class="sxs-lookup"><span data-stu-id="2ca86-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="2ca86-104">Questo documento fornisce esempi di script Hive che vengono utilizzati tooexplore dati nelle tabelle Hive in un cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2ca86-104">This document provides sample Hive scripts that are used tooexplore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="2ca86-105">esempio Hello **menu** collegamenti tootopics che descrivono come toouse strumenti tooexplore dati da diversi ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2ca86-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="2ca86-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ca86-106">Prerequisites</span></span>
<span data-ttu-id="2ca86-107">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="2ca86-107">This article assumes that you have:</span></span>

* <span data-ttu-id="2ca86-108">Creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2ca86-108">Created an Azure storage account.</span></span> <span data-ttu-id="2ca86-109">Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="2ca86-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="2ca86-110">Il provisioning di un cluster Hadoop personalizzato con hello servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2ca86-110">Provisioned a customized Hadoop cluster with hello HDInsight service.</span></span> <span data-ttu-id="2ca86-111">Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="2ca86-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="2ca86-112">dati Hello sono stato caricato tooHive tabelle cluster Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2ca86-112">hello data has been uploaded tooHive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="2ca86-113">In caso contrario, seguire le istruzioni hello [carico e creare tabelle di dati tooHive](machine-learning-data-science-move-hive-tables.md) tooupload dati tooHive tabelle prima.</span><span class="sxs-lookup"><span data-stu-id="2ca86-113">If it has not, follow hello instructions in [Create and load data tooHive tables](machine-learning-data-science-move-hive-tables.md) tooupload data tooHive tables first.</span></span>
* <span data-ttu-id="2ca86-114">Cluster toohello di accesso remoto abilitato.</span><span class="sxs-lookup"><span data-stu-id="2ca86-114">Enabled remote access toohello cluster.</span></span> <span data-ttu-id="2ca86-115">Se sono necessarie istruzioni, vedere [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="2ca86-115">If you need instructions, see [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="2ca86-116">Se sono necessarie istruzioni su come visualizzare le query Hive toosubmit, [come tooSubmit query Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="2ca86-116">If you need instructions on how toosubmit Hive queries, see [How tooSubmit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="2ca86-117">Script delle query Hive di esempio per l'esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="2ca86-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="2ca86-118">Ottenere il conteggio di hello di osservazioni per partizione`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="2ca86-118">Get hello count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="2ca86-119">Ottenere il conteggio di hello di osservazioni al giorno`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="2ca86-119">Get hello count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="2ca86-120">Ottenere livelli hello in una colonna categorica</span><span class="sxs-lookup"><span data-stu-id="2ca86-120">Get hello levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="2ca86-121">Ottenere il numero di hello dei livelli nella combinazione di due colonne categoriche`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="2ca86-121">Get hello number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="2ca86-122">Ottenere la distribuzione hello per le colonne numeriche</span><span class="sxs-lookup"><span data-stu-id="2ca86-122">Get hello distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="2ca86-123">Estrarre i record dall'unione di due tabelle</span><span class="sxs-lookup"><span data-stu-id="2ca86-123">Extract records from joining two tables</span></span>
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="2ca86-124">Script delle query aggiuntive per gli scenari relativi ai dati delle corse dei taxi</span><span class="sxs-lookup"><span data-stu-id="2ca86-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="2ca86-125">Esempi di query specifiche troppo[NYC Taxi viaggi dati](http://chriswhong.com/open-data/foil_nyc_taxi/) scenari vengono inoltre forniti [repository GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="2ca86-125">Examples of queries that are specific too[NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="2ca86-126">Queste query già uno schema di dati specificato e sono pronti toobe inviato toorun.</span><span class="sxs-lookup"><span data-stu-id="2ca86-126">These queries already have data schema specified and are ready toobe submitted toorun.</span></span>

