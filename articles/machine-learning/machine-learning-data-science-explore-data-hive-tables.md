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
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Esplorare i dati nelle tabelle Hive con  query Hive.
Questo documento fornisce esempi di script Hive che vengono utilizzati tooexplore dati nelle tabelle Hive in un cluster HDInsight Hadoop.

esempio Hello **menu** collegamenti tootopics che descrivono come toouse strumenti tooexplore dati da diversi ambienti di archiviazione.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente abbia:

* Creato un account di archiviazione di Azure. Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Il provisioning di un cluster Hadoop personalizzato con hello servizio HDInsight. Per istruzioni, vedere [Personalizzazione di cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md).
* dati Hello sono stato caricato tooHive tabelle cluster Azure HDInsight Hadoop. In caso contrario, seguire le istruzioni hello [carico e creare tabelle di dati tooHive](machine-learning-data-science-move-hive-tables.md) tooupload dati tooHive tabelle prima.
* Cluster toohello di accesso remoto abilitato. Se sono necessarie istruzioni, vedere [hello accesso nodo Head del Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Se sono necessarie istruzioni su come visualizzare le query Hive toosubmit, [come tooSubmit query Hive](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Script delle query Hive di esempio per l'esplorazione dei dati
1. Ottenere il conteggio di hello di osservazioni per partizione`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Ottenere il conteggio di hello di osservazioni al giorno`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Ottenere livelli hello in una colonna categorica  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. Ottenere il numero di hello dei livelli nella combinazione di due colonne categoriche`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Ottenere la distribuzione hello per le colonne numeriche  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. Estrarre i record dall'unione di due tabelle
   
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

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Script delle query aggiuntive per gli scenari relativi ai dati delle corse dei taxi
Esempi di query specifiche troppo[NYC Taxi viaggi dati](http://chriswhong.com/open-data/foil_nyc_taxi/) scenari vengono inoltre forniti [repository GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Queste query già uno schema di dati specificato e sono pronti toobe inviato toorun.

