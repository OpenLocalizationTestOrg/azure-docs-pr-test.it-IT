---
title: dati aaaExplore nella macchina virtuale SQL Server in Azure | Documenti Microsoft
description: Come tooexplore i dati archiviati in una macchina virtuale di SQL Server in Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Esplorazione dei dati nella macchina virtuale di SQL Server in Azure
Questo documento descrive come tooexplore i dati archiviati in una macchina virtuale di SQL Server in Azure. Questa operazione può essere eseguita gestendo i dati tramite SQL o utilizzando un linguaggio di programmazione come Python.

esempio Hello **menu** collegamenti tootopics che descrivono come toouse strumenti tooexplore dati da diversi ambienti di archiviazione. Questa attività è un passaggio di hello Cortana Analitica processo (CAP).

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> le istruzioni SQL Hello in questo documento si presuppongono che i dati siano in SQL Server. In caso contrario, fare riferimento toohello cloud data science processo mappa toolearn come toomove il tooSQL dati Server.
> 
> 

## <a name="sql-dataexploration"></a>Esplorare i dati SQL mediante gli script SQL
Ecco alcuni script SQL di esempio che possono essere utilizzati tooexplore archivi di dati in SQL Server.

1. Ottenere il conteggio di hello di osservazioni al giorno
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Ottenere livelli hello in una colonna categorica
   
    `select  distinct <column_name> from <databasename>`
3. Ottenere il numero di hello dei livelli nella combinazione di due colonne categoriche 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Ottenere la distribuzione hello per le colonne numeriche
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Per un esempio pratico, è possibile utilizzare hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) e fare riferimento toohello IPNB intitolato [dati NYC wrangling utilizzando SQL Server e IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) per una procedura dettagliata end-to-end.
> 
> 

## <a name="python"></a>Esplorare i dati SQL mediante Python
Utilizzando i dati di tooexplore Python e generare funzionalità quando hello dati sono disponibile in SQL Server simile tooprocessing dati in blob di Azure usando Python, come documentato [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md). dati Hello deve toobe caricati dal database hello un pandas frame di dati e quindi possono essere elaborati ulteriormente. Abbiamo documento processo hello di connessione database toohello e caricarvi i dati di hello hello frame di dati in questa sezione.

Hello seguente formato di stringa di connessione può essere utilizzato tooconnect tooa database di SQL Server da Python mediante pyodbc (sostituire servername, dbname, username e password con i valori specifici):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [libreria Pandas](http://pandas.pydata.org/) in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python. Hello codice seguente vengono letti hello restituiti da un database di SQL Server in un frame di dati Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

È ora possibile lavorare con hello Pandas frame di dati come illustrato nell'argomento hello [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Il Cortana Analytics Process nell’esempio di azione
Per un esempio di questa procedura dettagliata end-to-end di hello Cortana Analitica processo usando un set di dati pubblici, vedere [hello Team processo di analisi scientifica dei dati in azione: utilizzo di SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

