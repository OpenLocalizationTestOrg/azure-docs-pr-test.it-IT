---
title: aaaOverview dell'analisi scientifica dei dati utilizzando Spark in HDInsight di Azure | Documenti Microsoft
description: "Hello Spark MLlib toolkit offre funzionalità toohello distribuita HDInsight ambiente di modellazione apprendimento considerevole."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Panoramica dell'analisi scientifica dei dati con Spark in Azure HDInsight
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

In questo gruppo di argomenti viene illustrato come attività di toouse HDInsight Spark toocomplete comuni analisi scientifica dei dati, ad esempio l'inserimento di dati, progettazione di funzionalità, modellazione e valutazione del modello. dati Hello utilizzati sono un esempio di hello 2013 NYC taxi di andata e ritorno e tariffa set di dati. i modelli di Hello compilati includono la regressione logistica e lineare, foreste casuali e sfumati alberi con Boosting. Hello argomenti anche mostrano come toostore questi modelli in Azure blob storage (WASB) e in che modo tooscore e valutare le prestazioni predittiva. Argomenti più avanzati illustrano le modalità di training dei modelli con la convalida incrociata e lo sweep di iperparametri. Questo argomento introduttivo fa anche riferimento argomenti hello che descrivono come tooset backup hello cluster Spark necessari passaggi di hello toocomplete nelle procedure dettagliate di hello fornite. 

## <a name="spark-and-mllib"></a>Spark e MLlib
[Spark](http://spark.apache.org/) è un framework di elaborazione parallela open source che supporta in memoria prestazioni di elaborazione tooboost hello delle applicazioni analitiche big data. motore di elaborazione Spark Hello viene compilato per la velocità, semplicità di utilizzo e analitica sofisticate. La funzionalità di calcolo distribuito in memoria di Spark è molto adatto per algoritmi di hello iterativo usato nei calcoli di machine learning e graph. [MLlib](http://spark.apache.org/mllib/) è libreria di apprendimento di Spark scalabile di macchine che mette a disposizione hello algoritmico modellazione ambiente distribuito toothis di funzionalità. 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure ospitata offerta di Spark open source. Include inoltre il supporto per **Jupyter PySpark notebook** in cluster Spark hello che è possibile eseguire query interattive di Spark SQL per la trasformazione, filtro e visualizzazione dei dati archiviati nel BLOB di Azure (WASB). PySpark è hello API Python per Spark. frammenti di codice Hello che forniscono soluzioni hello e visualizzare i dati di hello tracciati rilevanti toovisualize hello qui eseguiti in server Jupyter notebook installato nel cluster Spark hello. passaggi di modellazione Hello in questi argomenti contengono codice che illustra come tootrain, valutare, salvare e utilizzare ogni tipo di modello. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Configurazione: cluster Spark e notebook di Jupyter
La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6. Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0. Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono. Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark. Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito. Per praticità, di seguito sono collegamenti hello toohello Jupyter notebook per Spark 1.6 (toobe eseguito nel kernel pySpark hello di hello server Jupyter Notebook) e Spark 2.0 (toobe eseguito nel kernel pySpark3 hello di hello server Jupyter Notebook):

### <a name="spark-16-notebooks"></a>Notebook Spark 1.6
Questi blocchi appunti sono toobe eseguito nel kernel pySpark hello del server Jupyter notebook.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi con diversi algoritmi.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): include gli argomenti nel notebook numero 1 e modella lo sviluppo usando l'ottimizzazione degli iperparametri e la convalida incrociata.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): mostra come toooperationalize un modello salvato usando Python in HDInsight cluster.

### <a name="spark-20-notebooks"></a>Notebook Spark 2.0
Questi blocchi appunti sono toobe eseguito nel kernel pySpark3 hello del server Jupyter notebook.

- [Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi in Spark 2.0 cluster tramite hello viaggi NYC Taxi e set di dati tariffa descritto [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Questo blocco può essere un buon punto di partenza per esplorare rapidamente codice hello che è stato fornito per Spark 2.0. Per un blocco per Appunti più dettagliata analizza hello dati NYC Taxi, vedere notebook avanti di hello in questo elenco. Vedere le note di hello seguendo questo elenco di confrontare questi notebook. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): questo file viene illustrato come tooperform dati wrangling (operazioni Spark SQL e frame di dati), l'esplorazione, modellazione e assegnazione dei punteggi usando hello viaggi NYC Taxi e tariffa set di dati descritto [ qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): questo file viene illustrato come tooperform dati wrangling (operazioni Spark SQL e frame di dati), l'esplorazione, modellazione e assegnazione dei punteggi usando hello partenza in fase di Airline noto set di dati da 2011 e 2012. È integrato hello airline dataset con hello aeroporto weather dati (ad esempio, velocità del vento, temperatura, altitudine e così via) precedenti toomodeling, in modo queste funzionalità weather possono essere incluso nel modello di hello.

<!-- -->

> [!NOTE]
> set di dati airline Hello è stato aggiunto notebook toohello Spark 2.0 toobetter illustrano l'utilizzo di hello di algoritmi di classificazione. Vedere i seguenti collegamenti per informazioni sui set di dati in fase di partenza airline e set di dati meteo hello:

>- Dati sulle partenze puntuali dei voli della compagnia aerea: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Dati sulle condizioni atmosferiche dell'aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Appunti di Spark 2.0 Hello in hello taxi NYC e airline flight delay-set di dati può richiedere 10 minuti o più toorun (a seconda delle dimensioni di hello del cluster HDI). primo notebook in hello sopra elenco Hello Mostra molti aspetti di esplorazione dei dati di hello, training in un blocco per Appunti che accetta toorun meno tempo con ridotti NYC set di dati, in cui hello sono stati già aggiunti a un file taxi e fare del modello di visualizzazione e ML: [ Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) il blocco accetta un molto più breve tempo toofinish (2-3 minuti) e può essere un buon punto di partenza per esplorare rapidamente codice hello abbiamo fornito per Spark 2.0. 

<!-- -->

Per indicazioni su come rendere operativo hello un modello Spark 2.0 e l'utilizzo di modello per il punteggio, vedere hello [Spark 1.6 documento sul consumo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) per un esempio di struttura passaggi hello necessari. toouse questo su Spark 2.0, sostituire i file di codice Python hello con [questo file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Prerequisiti
Hello, seguire le procedure seguenti è correlati tooSpark 1.6. Per la versione di hello Spark 2.0, usare hello notebook descritto e collegati toopreviously. 

1. È necessario avere una sottoscrizione di Azure. Se non è già disponibile, vedere l'articolo che illustra [come ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2. è necessario un toocomplete cluster Spark 1.6 questa procedura dettagliata. toocreate uno, vedere le istruzioni di hello fornite [Introduzione: creare Apache Spark in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). viene specificato il tipo di cluster Hello e la versione da hello **Seleziona tipo di Cluster** menu. 

![Configurare il cluster](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Per un argomento che illustra come toouse Scala anziché Python toocomplete attività per un processo di analisi scientifica dei dati end-to-end, vedere hello [analisi scientifica dei dati con Scala Spark in Azure](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Hello dati NYC 2013 Taxi
dati di andata e ritorno Taxi NYC Hello è di circa 20 GB di file compressi valori delimitati da virgole (CSV) (~ 48 GB non compressi), che comprendono 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario. Ogni record di andata e ritorno include hello preleva deposito e ora, hack anonimi (driver) il numero di licenza e numero medallion (id univoco del taxi). dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:

1. file CSV di Hello 'trip_data' contengono i dettagli di andata e ritorno, ad esempio il numero di persone, sollevare e dropoff punta, attivarsi durata e la lunghezza di andata e ritorno. Di seguito vengono forniti alcuni record di esempio:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. file CSV di Hello 'trip_fare' contengono i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato. Di seguito vengono forniti alcuni record di esempio:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

È stato reindirizzato a un campione di 0,1% di questi file e di andata e ritorno hello unita in join\_dati e andata e ritorno\_presentare file CVS in toouse un singolo set di dati come set di dati input hello per questa procedura dettagliata. viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da campi hello: medallion, le maggiori\_titolo e prelievo\_datetime. Ogni record del set di dati hello contiene hello gli attributi che rappresentano un trip NYC Taxi seguenti:

| Campo | Breve descrizione |
| --- | --- |
| medallion |Numero di licenza anonimo (ID univoco del taxi). |
| hack_license |Numero di licenza anonimo di vetture a noleggio |
| vendor_id |ID del fornitore del taxi |
| rate_code |Tariffe dei taxi di NYC |
| store_and_fwd_flag |Contrassegno di registrazione e inoltro |
| pickup_datetime |Data e ora di partenza |
| dropoff_datetime |Data e ora di arrivo |
| pickup_hour |Ora di partenza |
| pickup_week |Prelevare settimana dell'anno hello |
| weekday |Giorno della settimana (intervallo 1-7) |
| passenger_count |Numero di passeggeri in una corsa del taxi |
| trip_time_in_secs |Tempo delle corse in secondi |
| trip_distance |Distanza delle corse percorsa in miglia |
| pickup_longitude |Longitudine di partenza |
| pickup_latitude |Latitudine di partenza |
| dropoff_longitude |Longitudine di arrivo |
| dropoff_latitude |Latitudine di arrivo |
| direct_distance |Distanza diretta tra le località di partenza e di arrivo |
| payment_type |Tipo di pagamento (contanti, carta di credito e così via). |
| fare_amount |Imposto della tariffa in |
| surcharge |Sovrapprezzo |
| mta_tax |Tassa MTA |
| tip_amount |Importo delle mance |
| tolls_amount |Importo dei pedaggi |
| total_amount |Importo totale |
| tipped |Mancia lasciata (0/1 per no o sì) |
| tip_class |Categoria mance (0: $ 0, 1: $ 0-5, 2: $ 6-10, 3: $ 11-20, 4: > $ 20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Eseguire il codice da un server Jupyter notebook nel cluster Spark hello
È possibile avviare hello server Jupyter Notebook da hello portale di Azure. Trovare il cluster Spark nel dashboard e farvi clic sopra tooenter pagina di gestione per il cluster. Fare clic su Blocco note hello tooopen associato al cluster Spark hello, **dashboard del Cluster** -> **server Jupyter Notebook** .

![Dashboard del cluster](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

È inoltre possibile esplorare troppo***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess hello Jupyter notebook. Sostituisce parte CLUSTERNAME hello di questo URL con nome hello di un cluster personale. È necessario password hello per notebook amministratore account tooaccess hello.

![Sfogliare i notebook di Jupyter](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Selezionare PySpark toosee una directory che contiene alcuni esempi di Appunti sotto forma di pacchetto che utilizzano hello notebook PySpark API.hello che contengono gli esempi di codice hello per il gruppo di argomento Spark sono disponibili in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

È possibile caricare notebook hello direttamente da [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) toohello server notebook jupyter il cluster Spark. Scegliere hello hello home page del server Jupyter **caricare** pulsante nella parte destra della schermata di hello hello. Verrà visualizzata una finestra di esplorazione file, Qui è possibile incollare l'URL di GitHub (contenuto non elaborato) hello di hello Notebook e fare clic su **aprire**. 

Vedrai il nome di file hello dell'elenco di file server Jupyter con un **caricare** nuovamente clic sul pulsante. Fare clic sul pulsante **Upload** (Carica). A questo punto sono stati importati notebook hello. Ripetere questi hello tooupload passaggi altri blocchi appunti di questa procedura dettagliata.

> [!TIP]
> È possibile fare doppio clic su collegamenti hello del browser e selezionare **Copia collegamento** tooget hello URL contenuto non elaborato a github. È possibile incollare l'URL in hello Jupyter caricare file Esplora la finestra di dialogo.
> 
> 

A questo punto è possibile:

* Visualizzare codice hello facendo notebook hello.
* Eseguire ogni cella premendo **MAIUSC+INVIO**.
* Eseguire l'intero blocco hello facendo clic su **cella** -> **eseguire**.
* Utilizzare hello visualizzazione automatica delle query.

> [!TIP]
> kernel PySpark Hello Visualizza automaticamente l'output di hello delle query SQL (HiveQL). Hello opzione tooselect tra diversi tipi di visualizzazioni (tabella, a torta, linea, Area o barra) viene fornita tramite hello **tipo** pulsanti di menu in blocco per Appunti hello:
> 
> 

![Curva ROC di regressione logistica per approccio generico](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>Passaggi successivi
Ora che si sono configurati con un cluster HDInsight Spark e caricate notebook Jupyter hello, si è pronti toowork tramite argomenti hello corrispondenti toohello tre PySpark notebook. Vengono visualizzate come tooexplore i dati e come quindi toocreate e utilizzare i modelli. Hello avanzate di esplorazione dei dati e modellazione notebook Mostra come tooinclude convalida incrociata, hyper-parameter sweep e valutazione del modello. 

**Esplorazione dei dati e modellazione con Spark:** esplorare hello set di dati e creare, assegnare un punteggio e valutare i modelli di machine learning hello affrontando hello [creare modelli di classificazione e regressione binari per i dati con hello Spark Toolkit MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) argomento.

**Utilizzo del modello:** toolearn come modelli di classificazione e regressione hello tooscore creato in questo argomento, vedere [punteggio e valutare i modelli di apprendimento macchina compilato Spark](machine-learning-data-science-spark-model-consumption.md).

**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri

