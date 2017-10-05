---
title: Esplorare i dati nelle tabelle Hive con query Hive | Documentazione Microsoft
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
ms.openlocfilehash: 67a33a9abc3d3dcdd2fc7205e11feff97e3582a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a><span data-ttu-id="c2b72-103">Esplorare i dati nelle tabelle Hive con  query Hive.</span><span class="sxs-lookup"><span data-stu-id="c2b72-103">Explore data in Hive tables with Hive queries</span></span>
<span data-ttu-id="c2b72-104">Questo documento fornisce alcuni script Hive di esempio che sono utilizzati per esplorare i dati nelle tabelle Hive in un cluster HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c2b72-104">This document provides sample Hive scripts that are used to explore data in Hive tables in an HDInsight Hadoop cluster.</span></span>

<span data-ttu-id="c2b72-105">Il **menu** seguente collega ad argomenti che descrivono come usare gli strumenti per esplorare i dati da vari ambienti di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c2b72-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="c2b72-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c2b72-106">Prerequisites</span></span>
<span data-ttu-id="c2b72-107">Questo articolo presuppone che l'utente abbia:</span><span class="sxs-lookup"><span data-stu-id="c2b72-107">This article assumes that you have:</span></span>

* <span data-ttu-id="c2b72-108">Creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c2b72-108">Created an Azure storage account.</span></span> <span data-ttu-id="c2b72-109">Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c2b72-109">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="c2b72-110">Eseguito il provisioning di un cluster Hadoop personalizzato con il servizio HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2b72-110">Provisioned a customized Hadoop cluster with the HDInsight service.</span></span> <span data-ttu-id="c2b72-111">Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c2b72-111">If you need instructions, see [Customize Azure HDInsight Hadoop Clusters for Advanced Analytics](machine-learning-data-science-customize-hadoop-cluster.md).</span></span>
* <span data-ttu-id="c2b72-112">Caricato i dati nelle tabelle Hive dei cluster Hadoop di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2b72-112">The data has been uploaded to Hive tables in Azure HDInsight Hadoop clusters.</span></span> <span data-ttu-id="c2b72-113">Se questa operazione non è stata eseguita, seguire le istruzioni in [Creazione e caricamento di dati nelle tabelle Hive](machine-learning-data-science-move-hive-tables.md) per caricare prima di tutto i dati nelle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="c2b72-113">If it has not, follow the instructions in [Create and load data to Hive tables](machine-learning-data-science-move-hive-tables.md) to upload data to Hive tables first.</span></span>
* <span data-ttu-id="c2b72-114">Abilitato l'accesso remoto al cluster.</span><span class="sxs-lookup"><span data-stu-id="c2b72-114">Enabled remote access to the cluster.</span></span> <span data-ttu-id="c2b72-115">Per istruzioni, vedere [Accesso al nodo head del cluster Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="c2b72-115">If you need instructions, see [Access the Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>
* <span data-ttu-id="c2b72-116">Per istruzioni su come inviare query Hive, vedere [Come inviare query Hive](machine-learning-data-science-move-hive-tables.md#submit)</span><span class="sxs-lookup"><span data-stu-id="c2b72-116">If you need instructions on how to submit Hive queries, see [How to Submit Hive Queries](machine-learning-data-science-move-hive-tables.md#submit)</span></span>

## <a name="example-hive-query-scripts-for-data-exploration"></a><span data-ttu-id="c2b72-117">Script delle query Hive di esempio per l'esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="c2b72-117">Example Hive query scripts for data exploration</span></span>
1. <span data-ttu-id="c2b72-118">Visualizzare il numero di osservazioni per partizione `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span><span class="sxs-lookup"><span data-stu-id="c2b72-118">Get the count of observations per partition  `SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`</span></span>
2. <span data-ttu-id="c2b72-119">Visualizzare il numero di osservazioni per giorno `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span><span class="sxs-lookup"><span data-stu-id="c2b72-119">Get the count of observations per day  `SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`</span></span>
3. <span data-ttu-id="c2b72-120">Visualizzare i livelli in una colonna di categoria </span><span class="sxs-lookup"><span data-stu-id="c2b72-120">Get the levels in a categorical column</span></span>  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. <span data-ttu-id="c2b72-121">Visualizzare il numero di livelli in una combinazione di due colonne di categoria `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span><span class="sxs-lookup"><span data-stu-id="c2b72-121">Get the number of levels in combination of two categorical columns  `SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`</span></span>
5. <span data-ttu-id="c2b72-122">Visualizzare la distribuzione per colonne numeriche </span><span class="sxs-lookup"><span data-stu-id="c2b72-122">Get the distribution for numerical columns</span></span>  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. <span data-ttu-id="c2b72-123">Estrarre i record dall'unione di due tabelle</span><span class="sxs-lookup"><span data-stu-id="c2b72-123">Extract records from joining two tables</span></span>
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a><span data-ttu-id="c2b72-124">Script delle query aggiuntive per gli scenari relativi ai dati delle corse dei taxi</span><span class="sxs-lookup"><span data-stu-id="c2b72-124">Additional query scripts for taxi trip data scenarios</span></span>
<span data-ttu-id="c2b72-125">Nell'[archivio GitHub](http://chriswhong.com/open-data/foil_nyc_taxi/) sono disponibili anche alcuni esempi di query specifiche per gli scenari relativi ai [dati dei tragitti dei taxi di NYC](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span><span class="sxs-lookup"><span data-stu-id="c2b72-125">Examples of queries that are specific to [NYC Taxi Trip Data](http://chriswhong.com/open-data/foil_nyc_taxi/) scenarios are also provided in [GitHub repository](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts).</span></span> <span data-ttu-id="c2b72-126">Tali query dispongono già di un determinato schema dei dati e possono essere inviate e usate immediatamente.</span><span class="sxs-lookup"><span data-stu-id="c2b72-126">These queries already have data schema specified and are ready to be submitted to run.</span></span>

