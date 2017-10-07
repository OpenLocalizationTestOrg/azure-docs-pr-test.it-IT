---
title: cluster aaaKernels per server Jupyter notebook in Spark in HDInsight di Azure | Documenti Microsoft
description: Informazioni su hello PySpark PySpark3 e Spark. x Server Jupyter notebook disponibili con i cluster Spark in HDInsight di Azure.
keywords: notebook jupyter in spark, spark jupyter
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Kernel per il notebook di Jupyter nei cluster Spark in Azure HDInsight 

I cluster di HDInsight Spark includono kernel che è possibile utilizzare con i notebook Jupyter hello in Spark per il testing delle applicazioni. Un kernel è un programma che esegue e interpreta il codice. tre kernel Hello sono:

- **PySpark** per le applicazioni scritte in Python2
- **PySpark3** per le applicazioni scritte in Python3
- **Spark** per le applicazioni scritte in Scala

In questo articolo viene illustrato come toouse questi kernel e i vantaggi di hello del loro uso.

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Creare un notebook di Jupyter in HDInsight Spark

1. Da hello [portale di Azure](https://portal.azure.com/), aprire il cluster.  Vedere [elenco e visualizzare i cluster](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) per le istruzioni di hello. cluster Hello viene aperto in un nuovo pannello portale.

2. Da hello **collegamenti rapidi** fare clic su **Cluster dashboard** tooopen hello **Cluster dashboard** blade.  Se non viene visualizzato **collegamenti rapidi**, fare clic su **Panoramica** dal menu a sinistra nel pannello hello hello.

    ![Notebook di Jupyter in Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Notebook di Jupyter in Spark") 

3. Fare clic su **Notebook di Jupyter**. Se richiesto, immettere le credenziali di amministratore hello cluster hello.
   
   > [!NOTE]
   > È anche possibile raggiungere notebook Jupyter hello in cluster Spark dall'apertura hello seguente URL nel browser. Sostituire **CLUSTERNAME** con nome hello del cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Fare clic su **New**, quindi fare clic su **Pyspark**, **PySpark3**, o **Spark** toocreate un notebook. Utilizzare kernel Spark hello per le applicazioni di Scala e kernel PySpark Applications Python2 kernel PySpark3 Python3 Applications.
   
    ![Kernel per il notebook di Jupyter in Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Kernel per il notebook di Jupyter in Spark") 

4. Verrà visualizzata la finestra di un blocco per Appunti con kernel hello che è stata selezionata.

## <a name="benefits-of-using-hello-kernels"></a>Vantaggi dell'utilizzo di kernel hello

Ecco alcuni vantaggi dell'utilizzo kernel nuovo hello con server Jupyter notebook nei cluster HDInsight Spark.

- **Contesti predefiniti**. Con **PySpark**, **PySpark3**, o hello **Spark** kernel, non è necessario contesti di Spark o Hive hello tooset in modo esplicito prima di iniziare con le applicazioni. I contesti sono disponibili per impostazione predefinita. Questi contesti sono:
   
   * **sc** : per il contesto Spark
   * **sqlContext** : per il contesto Hive

    In tal caso, non è istruzioni toorun come hello seguenti contesti hello tooset:

        sc = SparkContext('yarn-client')    sqlContext = HiveContext(sc)

    In alternativa, è possibile utilizzare direttamente hello preimpostato contesti nell'applicazione.

- **Celle magic**. Hello kernel PySpark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con `%%` (ad esempio, `%%MAGIC` <args>). comando magic Hello deve essere hello prima parola di una cella di codice e consentono a più righe di contenuto. parola chiave Hello deve essere prima parola di hello nella cella hello. Aggiunta di qualsiasi altro magic hello, anche i commenti, causa un errore.     Per altre informazioni sui magic, vedere [questa pagina](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Hello nella tabella seguente sono elencati magics diversi hello disponibili attraverso il kernel hello.

   | Magic | Esempio | Descrizione |
   | --- | --- | --- |
   | help |`%%help` |Genera una tabella di tutti i magics disponibili hello con l'esempio e la descrizione |
   | info |`%%info` |Informazioni sulla sessione di output per l'endpoint di inserire il corrente hello |
   | CONFIGURA |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Configura parametri hello per la creazione di una sessione. Hello flag di forzatura (-f) è obbligatorio se una sessione è già stata creata, che garantisce la sessione di hello viene eliminato e ricreato. Visitare la pagina relativa al [corpo della richiesta POST/sessions di Livy](https://github.com/cloudera/livy#request-body) per un elenco dei parametri validi. Parametri devono essere passati come una stringa JSON e devono essere nella riga successiva hello dopo magic hello, come illustrato nell'esempio la colonna hello. |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |Esegue una query Hive sqlContext hello. Se hello `-o` parametro viene passato, il risultato di hello di hello query è persistente nel hello % % contesto Python locale come una [Pandas](http://pandas.pydata.org/) frame di dati. |
   | local |`%%local`<br>`a=1` |Tutto il codice hello nelle righe successive viene eseguito localmente. Codice deve essere valido codice Python2 anche indipendentemente dal kernel hello in uso. In questo caso, anche se si seleziona **PySpark3** o **Spark** kernel durante la creazione di notebook hello, se si utilizza hello `%%local` magic in una cella, quella cella deve avere solo codice Python2 valido... |
   | logs |`%%logs` |Output di hello log per la sessione corrente di inserire il hello. |
   | delete |`%%delete -f -s <session number>` |Elimina una sessione specifica dell'endpoint di inserire il corrente hello. Si noti che non è possibile eliminare sessione hello viene avviata per kernel hello stesso. |
   | cleanup |`%%cleanup -f` |Elimina tutte le sessioni di hello per endpoint inserire il corrente hello, tra cui la sessione del blocco appunti. Hello force flag -f è obbligatorio. |

   > [!NOTE]
   > Inoltre toohello magics aggiunte dal kernel PySpark hello, è inoltre possibile utilizzare hello [incorporato IPython magics](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), tra cui `%%sh`. È possibile utilizzare hello `%%sh` particolare toorun script e blocco di codice nel nodo head del cluster di hello.
   >
   >
2. **Visualizzazione automatica**. Hello **Pyspark** kernel Visualizza automaticamente l'output di hello di Hive e query SQL. È possibile scegliere tra diversi tipi di visualizzazione, inclusi Table, Pie, Line, Area e Bar.

## <a name="parameters-supported-with-hello-sql-magic"></a>Parametri supportati con hello % % magic sql
Hello `%%sql` magic supporta diversi parametri che è possibile utilizzare il tipo hello toocontrol dell'output visualizzato quando si eseguono query. Hello nella tabella seguente elenca l'output di hello.

| . | Esempio | Descrizione |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Utilizzare questo parametro toopersist hello di risultati di query hello, hello % % contesto Python locale, come un [Pandas](http://pandas.pydata.org/) frame di dati. nome Hello della variabile di frame di dati di hello è hello di nome di variabile specificato. |
| -q |`-q` |Utilizzare questo tooturn off visualizzazioni per la cella hello. Se non si desidera tooauto-visualizzare il contenuto di hello di una cella e si desidera toocapture come un frame di dati, quindi utilizzare `-q -o <VARIABLE>`. Se si desidera tooturn off visualizzazioni senza acquisire i risultati di hello (ad esempio, per l'esecuzione di una query SQL, ad esempio un `CREATE TABLE` istruzione), utilizzare `-q` senza specificare un `-o` argomento. |
| -m |`-m <METHOD>` |Dove **METHOD** è **take** o **sample**. L'impostazione predefinita è **take**. Se il metodo hello **richiedere**, kernel hello seleziona gli elementi dall'inizio di hello del set di dati di risultati hello specificato da MAXROWS (descritta più avanti in questa tabella). Se il metodo hello **esempio**, kernel hello un campionamento casuale gli elementi del set di dati hello in base troppo`-r` parametro, descritto di seguito in questa tabella. |
| -r |`-r <FRACTION>` |Qui **FRACTION** è un numero a virgola mobile compreso tra 0,0 e 1,0. Se il metodo di esempio hello per query SQL hello `sample`, quindi kernel hello frazione specificata di hello elementi hello di hello set di risultati per è un campionamento casuale. Ad esempio, se si esegue una query SQL con argomenti hello `-m sample -r 0.01`, % 1 hello di righe di risultati vengono campionati in modo casuale. |
| -n |`-n <MAXROWS>` |**MAXROWS** è un valore intero. kernel Hello limita il numero di hello di righe di output troppo**MAXROWS**. Se **MAXROWS** è un numero negativo, ad esempio **-1**, quindi hello numero di righe nel set di risultati hello non è limitato. |

**Esempio:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

istruzione Hello hello seguenti:

* Seleziona tutti i record da **hivesampletable**.
* Dal momento che viene usato -q, disattiva la visualizzazione automatica.
* Poiché si utilizzano `-m sample -r 0.1 -n 500` eseguito un campionamento casuale 10% delle righe hello hivesampletable hello e limiti hello dimensioni hello set too500 di righe di risultati.
* Infine, poiché è utilizzato `-o query2` salva anche una serie di output di hello in un frame di dati denominato **nella query 2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Considerazioni durante l'utilizzo di hello nuovo kernel

A seconda del valore kernel si utilizza, lasciando notebook hello in esecuzione utilizza le risorse cluster hello.  Con questi kernel, perché sono stati definiti i contesti di hello, semplicemente uscire notebook hello non terminare il contesto di hello e pertanto le risorse cluster hello continuano toobe in uso. Una procedura consigliata è hello toouse **chiudere e interrompere** opzione notebook hello **File** menu quando si ha terminato di utilizzare Blocco note hello, che termina il contesto di hello e quindi viene chiusa hello notebook.     

## <a name="show-me-some-examples"></a>Di seguito sono riportati alcuni esempi

Quando si apre un server Jupyter notebook, vengono visualizzati due cartelle a livello di radice hello.

* Hello **PySpark** cartella contiene esempi di blocchi appunti hello che usa new **Python** kernel.
* Hello **Scala** cartella contiene esempi di blocchi appunti hello che usa new **Spark** kernel.

È possibile aprire hello **00 - [leggere per primo] Spark Magic Kernel funzionalità** notebook da hello **PySpark** o **Spark** cartella toolearn su magics diversi hello disponibili. È inoltre possibile utilizzare hello come altri blocchi appunti di esempio disponibile in hello due cartelle toolearn tooachieve diversi scenari di utilizzo di server Jupyter notebook con i cluster HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>In cui sono archiviati i notebook hello?

Server Jupyter notebook vengono salvati toohello account di archiviazione associato al cluster di hello hello **/HdiNotebooks** cartella.  Cartelle create all'interno di Jupyter notebook e i file di testo sono accessibili dall'account di archiviazione hello.  Ad esempio, se si utilizza Jupyter toocreate una cartella **cartella** e un blocco per Appunti **myfolder/mynotebook.ipynb**, è possibile accedere a tale notebook `/HdiNotebooks/myfolder/mynotebook.ipynb` nell'account di archiviazione hello.  Hello inversa è anche true, vale a dire, se si carica un blocco per Appunti direttamente l'account di archiviazione tooyour in `/HdiNotebooks/mynotebook1.ipynb`, notebook hello è visibile dal server Jupyter anche.  Notebook rimangono nell'account di archiviazione hello anche dopo l'eliminazione di cluster hello.

modalità di Hello notebook salvataggio toohello account di archiviazione è compatibile con HDFS. Pertanto, se si SSH in cluster hello che è possibile utilizzare i comandi di gestione di file come illustrato nel seguente frammento di codice hello:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


Nel caso in cui sono presenti problemi di accesso di account di archiviazione hello per cluster hello, notebook hello vengono salvate anche nel nodo head hello `/var/lib/jupyter`.

## <a name="supported-browser"></a>Browser supportati

I notebook di Jupyter nei cluster HDInsight Spark sono supportati solo su Google Chrome.

## <a name="feedback"></a>Commenti e suggerimenti
kernel nuovo Hello sono in continua evoluzione fase e verrà maturo nel tempo. Questo potrebbe comportare un cambiamento delle API con l'evoluzione dei kernel. Sono graditi commenti e suggerimenti in merito all'uso di questi nuovi kernel. Ciò è utile nella determinazione versione finale di hello di questi kernel. È possibile lasciare commenti/commenti e suggerimenti in hello **commenti** hello ultima sezione di questo articolo.

## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight](hdinsight-apache-spark-use-bi-tools.md)
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale](hdinsight-apache-spark-eventhub-streaming.md)
* [Analisi dei log del sito Web mediante Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Creare ed eseguire applicazioni
* [Creare un'applicazione autonoma con Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Eseguire processi in modalità remota in un cluster Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Strumenti ed estensioni
* [Utilizzare i plug-in strumenti di HDInsight per toocreate IntelliJ IDEA e inviare applicazioni Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Utilizzare i plug-in strumenti di HDInsight per le applicazioni di Spark toodebug IntelliJ IDEA in modalità remota](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usare i notebook di Zeppelin con un cluster Spark in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Usare pacchetti esterni con i notebook Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Installare Jupyter nel computer e connettere il cluster HDInsight Spark tooan](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)
