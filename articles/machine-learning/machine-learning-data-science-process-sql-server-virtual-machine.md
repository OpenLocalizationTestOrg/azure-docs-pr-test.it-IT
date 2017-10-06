---
title: aaaExplore dati in una macchina virtuale di SQL Server in Azure | Documenti Microsoft
description: "Esplorare dati e generare funzionalità in una macchina virtuale di SQL Server in Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Elaborazione dei dati della macchina virtuale di SQL Server in Azure
Questo documento descrive come tooexplore dati e generare le funzionalità per i dati archiviati in una macchina virtuale di SQL Server in Azure. Questa operazione può essere eseguita gestendo i dati tramite SQL o utilizzando un linguaggio di programmazione come Python.

> [!NOTE]
> le istruzioni SQL Hello in questo documento si presuppongono che i dati siano in SQL Server. In caso contrario, fare riferimento toohello cloud data science processo mappa toolearn come toomove il tooSQL dati Server.
> 
> 

## <a name="SQL"></a>Utilizzo di SQL
Viene descritto hello seguenti attività wrangling di dati in questa sezione tramite SQL:

1. [Esplorazione dei dati](#sql-dataexploration)
2. [Creazione di funzionalità](#sql-featuregen)

### <a name="sql-dataexploration"></a>Esplorazione dei dati
Ecco alcuni script SQL di esempio che possono essere utilizzati tooexplore archivi di dati in SQL Server.

> [!NOTE]
> Per un esempio pratico, è possibile utilizzare hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) e fare riferimento toohello IPNB intitolato [dati NYC wrangling utilizzando SQL Server e IPython Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) per una procedura dettagliata end-to-end.
> 
> 

1. Ottenere il conteggio di hello di osservazioni al giorno
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Ottenere livelli hello in una colonna categorica
   
    `select  distinct <column_name> from <databasename>`
3. Ottenere il numero di hello dei livelli nella combinazione di due colonne categoriche 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Ottenere la distribuzione hello per le colonne numeriche
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Creazione di funzionalità
In questa sezione viene descritto come creare funzionalità tramite SQL:  

1. [Creazione di funzionalità basate sul conteggio](#sql-countfeature)
2. [Creazione di contenitori per la creazione di funzionalità](#sql-binningfeature)
3. [Implementazione della funzionalità hello da una singola colonna](#sql-featurerollout)

> [!NOTE]
> Dopo avere generato le funzionalità aggiuntive, è possibile aggiungerli come tabella di colonne toohello esistente o creare una nuova tabella con le funzionalità aggiuntive di hello e la chiave primaria, che può essere unita con la tabella originale hello. 
> 
> 

### <a name="sql-countfeature"></a>Creazione di funzionalità basate sul conteggio
Hello seguenti esempi illustrano due modi per generare le funzionalità di conteggio. primo metodo Hello utilizza somma condizionale e secondo Usa metodo di hello hello clausola 'where'. Questi possono quindi essere aggiunti con hello originale (tramite le colonne chiave primaria) toohave conteggio caratteristiche della tabella insieme ai dati originali hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Creazione di contenitori per la creazione di funzionalità
Hello esempio seguente viene illustrato come toogenerate suddiviso funzionalità tramite la creazione di contenitori (tramite cinque bin) una colonna numerica che può essere utilizzata come una funzionalità alternativa:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Implementazione della funzionalità hello da una singola colonna
In questa sezione viene illustrato come tooroll out una singola colonna in una tabella toogenerate ulteriori funzionalità. esempio Hello si presuppone che esista una colonna di longitudine o latitudine nella tabella hello da cui si sta tentando di toogenerate funzionalità.

Ecco una breve panoramica sui dati di posizione di latitudine e longitudine (lecito da stackoverflow [come toomeasure hello accuratezza di latitudine e longitudine?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Ciò è utile toounderstand prima di campo, località featurizing hello:

* sign Hello indica se è in corso Nord o sud, est o occidentale mondo hello.
* Una cifra nell'ordine delle centinaia diversa da zero indica che si sta usando la longitudine invece della latitudine.
* cifra Hello decine offre una posizione tooabout chilometri 1.000. Inoltre, fornisce informazioni utili sul continente o sull'oceano in cui si trova l'utente.
* singola unità Hello (un grado decimale) offre una posizione in alto too111 chilometri (60 miglia, circa miglia 69). Inoltre, indica in quale stato o regione si trova l'utente.
* Hello prima cifra decimale vale la pena di km too11.1: è possibile distinguere posizione hello di una città di grandi dimensioni di una città di grandi dimensioni adiacente.
* Hello seconda posizione decimale vale la pena di km too1.1: è possibile separare una località da hello successivamente.
* terzo decimale Hello vale la pena di m: too110 in grado di identificare un campo agricoltura di grandi dimensioni o istituzionale campus.
* quarto decimale Hello vale la pena di m: too11 in grado di identificare le superfici. È confrontabile toohello accuratezza tipico di un'unità GPS non corrette con nessuna interferenza.
* cifra decimale quinto Hello vale la pena di m: too1.1 alberi che distinguono tra loro. Livello di toothis accuratezza con unità GPS esterna può essere ottenuto solo con la correzione differenziale.
* cifra decimale sesto Hello vale la pena di m: too0.11 che è possibile utilizzarlo per layout di strutture in dettaglio, per la progettazione di scenari, compilazione strade. È più che sufficiente per rilevare i movimenti dei ghiacciai e dei fiumi. È possibile ottenere questa accuratezza eseguendo misurazioni accurate con il GPS, quale quello corretto in modo differenziale.

le informazioni sul percorso Hello può essere trasformato come indicato di seguito, separare i area, percorso e città. Si noti che è anche possibile chiamare il punto finale di REST, ad esempio disponibile all'API di Bing Maps [individuare il percorso dal punto](https://msdn.microsoft.com/library/ff701710.aspx) informazioni sulla regione/zona di tooget hello.

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

Queste funzionalità in base alla posizione possono essere ulteriormente le funzionalità aggiuntive conteggio toogenerate usato come descritto in precedenza. 

> [!TIP]
> A livello di codice, è possibile inserire i record di hello mediante il linguaggio scelto. Potrebbe essere necessario dati hello tooinsert l'efficienza di blocchi tooimprove scrittura (per un esempio di come toodo questo uso pyodbc, vedere [tooaccess di esempio HelloWorld A SQL Server con python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). In alternativa è tooinsert dati nel database di hello utilizzando hello [utilità BCP](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Connessione tooAzure Machine Learning
funzionalità Hello appena generato può aggiunto come colonna tooan tabella esistente o archiviati in una nuova tabella e unito in join alla tabella originale di hello per machine learning. Funzionalità possono essere generate o accedere se è già stato creato, utilizzando hello [l'importazione dei dati] [ import-data] modulo in Azure Machine Learning, come illustrato di seguito:

![lettori azureml][1] 

## <a name="python"></a>Utilizzo di un linguaggio di programmazione quale Python
Utilizzando i dati di tooexplore Python e generare funzionalità quando hello dati sono disponibile in SQL Server è dati tooprocessing simili in blob di Azure usando Python, come documentato [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md). dati Hello deve toobe caricati dal database hello in un frame di dati pandas e quindi possono essere elaborati ulteriormente. Abbiamo documento processo hello di connessione database toohello e il caricamento dei dati hello in frame di dati hello in questa sezione.

Hello seguente formato di stringa di connessione può essere utilizzato tooconnect tooa database di SQL Server da Python mediante pyodbc (sostituire servername, dbname, username e password con i valori specifici):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Hello [libreria Pandas](http://pandas.pydata.org/) in Python fornisce un ampio set di strutture di dati e gli strumenti di analisi di dati per la manipolazione dei dati per la programmazione Python. codice Hello seguente legge hello restituiti da un database di SQL Server in un frame di dati Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

È ora possibile lavorare con i frame di dati Pandas hello come illustrato nell'articolo hello [dati Blob di Azure processo nell'ambiente di analisi scientifica dei dati](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Analisi scientifica dei dati di Azure nell'esempio di azione
Per un esempio di questa procedura dettagliata end-to-end di hello processo di analisi scientifica dei dati di Azure usando un set di dati pubblici, vedere [processo di analisi scientifica dei dati di Azure nell'azione](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

