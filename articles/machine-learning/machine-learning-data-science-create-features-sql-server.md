---
title: "funzionalità aaaCreate per i dati in SQL Server utilizzando SQL e Python | Documenti Microsoft"
description: Elaborazione dei dati di SQL Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>Creare funzionalità per i dati in SQL Server tramite SQL e Python
Questo documento illustra come toogenerate funzionalità per i dati archiviati in una macchina virtuale di SQL Server in Azure che consentono di algoritmi ottengono le informazioni in modo più efficiente da dati hello. Questa operazione può essere eseguita tramite SQL o usando un linguaggio di programmazione come Python. Questo esempio include una dimostrazione di entrambi.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Questo **menu** collegamenti tootopics che descrivono come toocreate funzionalità per i dati in vari ambienti. Questa attività è un passaggio di hello [Team Data Science processo (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Per un esempio pratico, è possibile consultare hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) e fare riferimento toohello IPNB intitolato [dati NYC wrangling utilizzando SQL Server e IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) per una procedura dettagliata end-to-end.
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente abbia:

* Creato un account di archiviazione di Azure. Per istruzioni, vedere [Creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* I dati vengono archiviati in SQL Server. In caso contrario, vedere [spostare dati tooan Database SQL di Azure per Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) per istruzioni su come toomove hello dati non esiste.

## <a name="sql-featuregen"></a>Creazione di funzionalità con SQL
In questa sezione viene descritto come creare funzionalità tramite SQL:  

1. [Creazione di funzionalità basate sul conteggio](#sql-countfeature)
2. [Creazione di contenitori per la creazione di funzionalità](#sql-binningfeature)
3. [Implementazione della funzionalità hello da una singola colonna](#sql-featurerollout)

> [!NOTE]
> Dopo avere generato le funzionalità aggiuntive, è possibile aggiungerli come tabella di colonne toohello esistente o creare una nuova tabella con le funzionalità aggiuntive di hello e la chiave primaria, che può essere unita con la tabella originale hello.
> 
> 

### <a name="sql-countfeature"></a>Creazione di funzionalità basate sul conteggio
In questo documento vengono descritte due modalità per creare funzionalità di conteggio. primo metodo Hello utilizza somma condizionale e secondo Usa metodo di hello hello clausola 'where'. Questi possono quindi essere aggiunti con hello originale (tramite le colonne chiave primaria) toohave conteggio caratteristiche della tabella insieme ai dati originali hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità
Hello esempio seguente viene illustrato come toogenerate suddiviso funzionalità tramite la creazione di contenitori (tramite 5 bin) una colonna numerica che può essere utilizzata come una funzionalità alternativa:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Implementazione della funzionalità hello da una singola colonna
In questa sezione viene illustrato come tooroll-out una singola colonna in una tabella toogenerate ulteriori funzionalità. esempio Hello si presuppone che esista una colonna di longitudine o latitudine nella tabella hello da cui si sta tentando di toogenerate funzionalità.

Di seguito, viene riportata una breve introduzione sui dati di posizione relativi a latitudine e longitudine (risorse assegnate da stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Ciò è utile toounderstand prima di campo, località featurizing hello:

* sign Hello indica se è in corso Nord o sud, est o occidentale mondo hello.
* Una cifra nell'ordine delle centinaia, diversa da zero, indica che si sta utilizzando la longitudine invece della latitudine.
* cifra Hello decine offre una posizione tooabout chilometri 1.000. Inoltre, fornisce informazioni utili sul continente o sull'oceano in cui si trova l'utente.
* singola unità Hello (un grado decimale) offre una posizione in alto too111 chilometri (60 miglia, circa miglia 69). Inoltre, indica in quale stato o regione si trova l'utente.
* Hello prima cifra decimale vale la pena di km too11.1: è possibile distinguere posizione hello di una città di grandi dimensioni di una città di grandi dimensioni adiacente.
* Hello seconda posizione decimale vale la pena di km too1.1: è possibile separare una località da hello successivamente.
* terzo decimale Hello vale la pena di m: too110 in grado di identificare un campo agricoltura di grandi dimensioni o istituzionale campus.
* quarto decimale Hello vale la pena di m: too11 in grado di identificare le superfici. È confrontabile toohello accuratezza tipico di un'unità GPS non corrette con nessuna interferenza.
* Hello quinta cifra decimale vale la pena di m: too1.1, alberi di distinguere tra loro. Livello di toothis accuratezza con unità GPS esterna può essere ottenuto solo con la correzione differenziale.
* cifra decimale sesto Hello vale la pena di m: too0.11 che è possibile utilizzarlo per layout di strutture in dettaglio, per la progettazione di scenari, compilazione strade. È più che sufficiente per rilevare i movimenti dei ghiacciai e dei fiumi. È possibile ottenere questa accuratezza eseguendo misurazioni accurate con il GPS, quale quello corretto in modo differenziale.

le informazioni sul percorso Hello possibile può essere trasformato come indicato di seguito, separare i area, percorso e informazioni di città. Si noti che una volta è inoltre possono chiamare il punto finale di REST, ad esempio disponibile all'API di Bing Maps `https://msdn.microsoft.com/library/ff701710.aspx` informazioni sulla regione/zona di tooget hello.

    select
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Hello sopra posizione le funzionalità di base possono essere ulteriormente utilizzati funzionalità aggiuntive di conteggio toogenerate come descritto in precedenza.

> [!TIP]
> A livello di codice, è possibile inserire i record di hello mediante il linguaggio scelto. Potrebbe essere necessario dati hello tooinsert l'efficienza di scrittura di blocchi tooimprove [estrarre l'esempio hello toodo questo usando pyodbc qui](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> In alternativa è tooinsert dati hello database mediante [utilità BCP](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Connessione tooAzure Machine Learning
funzionalità Hello appena generato può aggiunto come colonna tooan tabella esistente o archiviati in una nuova tabella e unito in join alla tabella originale di hello per machine learning. Funzionalità possono essere generate o accedere se è già stato creato, utilizzando hello [l'importazione dei dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) modulo in Machine Learning di Azure come illustrato di seguito:

![lettori azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Utilizzo di un linguaggio di programmazione quale Python
Utilizzo delle funzionalità di toogenerate Python quando hello dati in SQL Server è dati tooprocessing simili in blob di Azure usando Python, come documentato [dati Blob di Azure processo si dati scienza ambiente](machine-learning-data-science-process-data-blob.md). dati Hello deve toobe caricati dal database hello in un frame di dati pandas e quindi possono essere elaborati ulteriormente. Abbiamo documento processo hello di connessione database toohello e il caricamento dei dati hello in frame di dati hello in questa sezione.

Hello seguente formato di stringa di connessione può essere utilizzato tooconnect tooa database di SQL Server da Python mediante pyodbc (sostituire servername, dbname, nome utente e password con i valori specifici):

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [libreria Pandas](http://pandas.pydata.org/) in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python. codice Hello seguente legge hello restituiti da un database di SQL Server in un frame di dati Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

È ora possibile lavorare con i frame di dati Pandas hello come descritte negli argomenti [creano funzionalità per i dati di archiviazione blob di Azure mediante Panda](machine-learning-data-science-create-features-blob.md).

