---
title: hello aaaProvision macchina virtuale di analisi scientifica dei dati di Linux | Documenti Microsoft
description: Configurare e creare una macchina di virtuale analisi scientifica dei dati di Linux in Azure toodo analitica e machine learning.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3bab0ab9-3ea5-41a6-a62a-8c44fdbae43b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 81dfa90f6cd4b4f33535a20fb97442bf9152d829
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-linux-data-science-virtual-machine"></a>Eseguire il provisioning di hello macchina virtuale di analisi scientifica dei dati di Linux
Hello macchina virtuale di analisi scientifica dei dati di Linux è una CentOS basato su macchina virtuale di Azure che include una raccolta di strumenti di pre-installati. Questi strumenti vengono comunemente usati per eseguire l'analisi dei dati e il Machine Learning. i componenti software chiave Hello inclusi sono:

* Sistema operativo: distribuzione di Linux CentOS.
* Microsoft R Server Developer Edition
* Distribuzione di Anaconda Python, versioni 2.7 e 3.5, incluse le più comuni librerie di analisi dei dati
* JuliaPro: un'accurata distribuzione di linguaggio Julia con librerie scientifiche e dati di analitica diffuse
* Istanza Spark univoca e un solo nodo Hadoop (HDFS, Yarn)
* JupyterHub: un server notebook Jupyter multiutente che supporta kernel R, Python, PySpark e Julia
* Azure Storage Explorer
* Interfaccia della riga di comando di Azure per la gestione delle risorse di Azure
* Database PostgresSQL
* Strumenti di Machine Learning
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK): toolkit di software di formazione avanzato sviluppato da Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): sistema di apprendimento automatico rapido che supporta tecniche come hash, allreduce, reduction, learning2search, nonché apprendimento online, attivo e interattivo.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): strumento che consente un'implementazione dell'albero con boosting rapida e accurata.
  * [Rattle](http://rattle.togaware.com/) (strumento di analisi R tooLearn hello facilmente): uno strumento che consente l'introduzione analitica dei dati e machine learning in R semplice, con l'esplorazione dei dati basata su interfaccia utente grafica e di modellazione con generazione automatica di codice R.
* Azure SDK in Java, Python, Node.js, Ruby, PHP
* Librerie in R e Python da usare in Azure Machine Learning e altri servizi di Azure
* Editor e strumenti di sviluppo (RStudio, PyCharm, IntelliJ, Emacs, gedit, VI)


L'esecuzione dell'analisi scientifica dei dati comporta l'iterazione di una sequenza di attività quali:

1. Ricerca, caricamento e pre-elaborazione dei dati
2. Compilazione e test di modelli
3. Distribuzione di modelli di hello per l'utilizzo in applicazioni intelligenti

Gli esperti di dati utilizzano vari strumenti toocomplete queste attività. Può essere molto tempo toofind versioni appropriate di hello del software hello e toodownload, quindi compilare e installare le versioni.

Macchina virtuale di analisi scientifica dei dati di Linux Hello facilita questo carico significativo. Utilizzarlo toojump avvio progetto analitica. Consente di toowork attività in varie lingue, tra cui R, Python, SQL, Java e C++. Eclipse fornisce un toodevelop IDE e testare il codice che è facile toouse. Hello incluso in hello VM di Azure SDK consente toobuild le applicazioni usando vari servizi in Linux per hello Microsoft cloud platform. Inoltre, si dispongono di accesso tooother lingue come Ruby, Perl, PHP e node.js anche pre-installate.

Per questa immagine di VM per l'analisi scientifica dei dati non sono previsti costi per il software. Si paga solo hello tariffe che vengono valutate in base alle dimensioni di hello di macchina virtuale hello è effettuare il provisioning con immagine di macchina virtuale hello sull'utilizzo di hardware di Azure. Ulteriori dettagli su hello calcolano le commissioni possono trovarsi in hello [pagina elenco VM hello Azure Marketplace ](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm/).

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Altre versioni di hello macchina virtuale di analisi scientifica dei dati
Un [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md) immagine è disponibile, con molti hello stesso strumenti come hello immagine CentOS più Framework di formazione. È disponibile anche un'immagine [Windows](machine-learning-data-science-provision-vm.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di creare una macchina di virtuale analisi scientifica dei dati di Linux, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**: tooobtain uno, vedere [versione di valutazione gratuita di Azure ottenere](https://azure.microsoft.com/free/).
* **Un account di archiviazione di Azure**: toocreate uno, vedere [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). In alternativa, è possibile creare account di archiviazione hello come parte del processo di hello di creazione di hello macchina virtuale, se non si desidera toouse un account esistente.

## <a name="create-your-linux-data-science-virtual-machine"></a>Creare la macchina virtuale Linux per l'analisi scientifica dei dati
Di seguito è hello passaggi toocreate un'istanza di macchina virtuale di analisi scientifica dei dati di Linux hello:

1. Passare a macchina virtuale toohello elenco su hello [portale di Azure](https://portal.azure.com/#create/microsoft-ads.linux-data-science-vmlinuxdsvm).
2. Fare clic su **crea** (nella parte inferiore di hello) toobring guidata hello.![ configurare-data-scienza-vm](./media/machine-learning-data-science-linux-dsvm-intro/configure-linux-data-science-virtual-machine.png)
3. Hello le sezioni seguenti consentono di input hello per ognuno di hello passaggi nella procedura guidata hello (enumerata in hello destra della figura precedente hello) hello toocreate macchina virtuale di analisi scientifica dei dati di Microsoft. Di seguito sono hello input Necessito tooconfigure ciascuna di queste operazioni:
   
   a. **Nozioni di base**:
   
   * **Name**: nome del server di analisi scientifica dei dati che si sta creando.
   * **Nome utente**: primo ID di accesso dell'account.
   * **Password**: la prima password dell'account. È possibile usare una chiave pubblica SSH invece di una password.
   * **Sottoscrizione**: se si dispone di più di una sottoscrizione, selezionare hello uno in cui hello il computer è toobe creato e fatturato. È necessario disporre di privilegi di creazione delle risorse per questa sottoscrizione.
   * **Gruppo di risorse**: è possibile creare un nuovo gruppo di risorse o usarne uno esistente.
   * **Percorso**: hello selezionare data center situato più appropriato. In genere è centro dati hello che include la maggior parte dei dati oppure è più vicino tooyour di posizione fisica per l'accesso di rete più veloce.
   
   b. **Dimensione**:
   
   * Selezionare uno dei tipi di server hello che soddisfa i requisiti funzionali e vincoli di costo. Selezionare **Visualizza tutto** toosee altre opzioni di dimensioni delle macchine Virtuali.
   
   c. **Impostazioni**:
   
   * **Tipo di disco**: se si preferisce un'unità a stato solido, scegliere **Premium**. In caso contrario, scegliere **Standard**.
   * **Account di archiviazione**: È possibile creare un nuovo account di archiviazione di Azure nella sottoscrizione o utilizzarne uno esistente in hello stessa ubicazione in cui è stato scelto in hello **nozioni di base** passaggio della procedura guidata hello.
   * **Altri parametri**: nella maggior parte dei casi, è sufficiente utilizzare i valori predefiniti di hello. valori non predefiniti tooconsider, passare il mouse su un collegamento informativo hello per consentono in campi specifici di hello.
   
   d. **Riepilogo**:
   
   * Verificare che tutte le informazioni immesse siano corrette.
   
   e. **Acquisto**:
   
   * toostart hello provisioning, fare clic su **acquistare**. Termini toohello di transazione hello viene fornito un collegamento. Hello macchina virtuale non dispone di costi aggiuntivi oltre calcolo hello per le dimensioni del server hello scelto nel hello **dimensioni** passaggio.

provisioning di Hello dovrebbe richiedere circa 10-20 minuti. stato di Hello di provisioning hello viene visualizzato nel portale di Azure hello.

## <a name="how-tooaccess-hello-linux-data-science-virtual-machine"></a>Come tooaccess hello macchina virtuale di analisi scientifica dei dati di Linux
Dopo aver hello che viene creata la VM, è possibile firmare tooit utilizzando SSH. Utilizzare le credenziali dell'account hello creati in hello **nozioni di base** sezione del passaggio 3 per l'interfaccia di shell testo hello. In Windows è possibile scaricare uno strumento client SSH come [Putty](http://www.putty.org). Se si preferisce un desktop con interfaccia grafico (sistema Windows X), è possibile utilizzare in Putty di inoltro X11 o installare il client X2Go hello.

> [!NOTE]
> client Hello X2Go eseguita in modo significativo migliore nel test di inoltro X11. È consigliabile utilizzare client X2Go hello per un'interfaccia grafica desktop.
> 
> 

## <a name="installing-and-configuring-x2go-client"></a>Installazione e configurazione del client X2Go
è già effettuato il provisioning di Hello VM Linux con X2Go server e le connessioni client tooaccept pronto. tooconnect toohello desktop grafica VM Linux, hello seguente nel client:

1. Scaricare e installare il client hello X2Go per la piattaforma del client da [X2Go](http://wiki.x2go.org/doku.php/doc:installation:x2goclient).    
2. Eseguire il client hello X2Go e selezionare **nuova sessione**. Viene visualizzata una finestra di configurazione con più schede. Immettere i seguenti parametri di configurazione hello:
   * **Scheda Session**(Sessione):
     * **Host**: nome host hello o l'indirizzo IP della VM Linux analisi scientifica dei dati.
     * **Account di accesso**: nome utente indicato sul hello VM Linux.
     * **Porta SSH**: lasciarlo 22, valore predefinito di hello.
     * **Tipo di sessione**: tooXFCE valore hello di modifica. Hello VM Linux supporta attualmente solo desktop XFCE.
   * **Scheda supporto**: È possibile disattivare il supporto di audio e stampa se non è necessario toouse client li.
   * **Cartelle condivise**: se si desidera directory dal computer client montato su hello VM Linux, aggiungere le cartelle del computer client hello che si desidera tooshare con hello VM in questa scheda.

Dopo l'accesso toohello VM utilizzando client SSH hello o desktop con interfaccia grafica di XFCE tramite client X2Go hello, si è pronti toostart hello strumenti vengono installati e configurati in hello VM. Nella XFCE, è possibile visualizzare i collegamenti di applicazioni del menu e icone del desktop per molti degli strumenti hello.

## <a name="tools-installed-on-hello-linux-data-science-virtual-machine"></a>Strumenti installati nella macchina virtuale di analisi scientifica dei dati di Linux hello
### <a name="microsoft-r-server"></a>Microsoft R Server
R è uno dei linguaggi più diffusi di hello per analisi dei dati e machine learning. Se si desidera toouse R per l'analitica, hello VM è Microsoft R Server (Signora) con hello Microsoft R Open (MRO) e libreria del Kernel matematico (MKL). Hello MKL Ottimizza operazioni matematiche comuni negli algoritmi analitici. Una delle librerie R hello pubblicate in CRAN può essere installata in hello MRO MRO è compatibile con CRAN R al 100%. MRS garantisce scalabilità e messa in funzione dei modelli R nei servizi Web. È possibile modificare i programmi di R in uno degli editor predefiniti hello, ad esempio RStudio, vi, Emacs o gedit. Se si utilizza l'editor Emacs hello, si noti che il pacchetto Emacs hello ESS (Emacs pronuncia statistiche), che semplifica l'utilizzo dei file di R nell'editor di Emacs hello pre-installato.

console toolaunch R, sufficiente digitare **R** nella shell di hello. Consente di procedere ambiente interattivo tooan. toodevelop del programma di R, in genere, utilizzare un editor come Emacs o vi o gedit e quindi eseguire uno script di hello in R. Con RStudio, è necessario un grafico completo toodevelop ambiente IDE con il programma di R.

È inoltre disponibile uno script R per tooinstall hello [pacchetti R 20 Top](http://www.kdnuggets.com/2015/06/top-20-r-packages.html) se si desidera. Questo script può essere eseguito una volta nell'interfaccia interattiva hello R, che può essere inserita (come indicato) digitando **R** nella shell di hello.  

### <a name="python"></a>Python
Per lo sviluppo tramite Python, è installata la distribuzione Anaconda Python 2.7 e 3.5. Questo tipo di distribuzione contiene hello Python con circa 300 di hello più diffusi matematiche, ingegneria e analitica pacchetti di dati di base. È possibile utilizzare l'editor di testo hello predefiniti. Si può anche usare Spyder, un IDE Python incluso nelle distribuzioni di Anaconda Python. Spyder richiede un desktop con interfaccia grafica o X11 Forwarding. Nel desktop grafica hello viene fornito un tooSpyder di scelta rapida.

Poiché si dispone di Python 2.7 e 3.5, è necessario toospecifically Attiva versione di Python hello desiderato (conda environment) da toowork su in hello sessione corrente. il processo di attivazione Hello imposta versione desiderata toohello variabile PATH di hello di Python.

tooactivate hello Python 2.7 conda ambiente eseguire hello dalla shell hello:

    source /anaconda/bin/activate root

Python 2.7 viene installato in */anaconda/bin*.

tooactivate hello Python 3.5 conda ambiente eseguire hello dalla shell hello:

    source /anaconda/bin/activate py35


Python 3.5 viene installato in */anaconda/envs/py35/bin*.

tooinvoke una sessione interattiva di Python, è sufficiente digitare **python** nella shell di hello. Se si trovano su un'interfaccia grafica o utilizzare X11 inoltro set di backup, è possibile digitare **pycharm** toolaunch hello PyCharm dell'IDE Python.

tooinstall librerie aggiuntive di Python, è necessario toorun ```conda``` o ````pip```` comando in sudo e fornire il percorso completo di gestione di pacchetti Python hello (conda o pip) tooinstall toohello Python ambiente corretto. ad esempio:

    sudo /anaconda/bin/pip install <package> #for Python 2.7 environment
    sudo /anaconda/envs/py35/bin/pip install <package> # for Python 3.5 environment


### <a name="jupyter-notebook"></a>Notebook di Jupyter
Hello distribuzione Anaconda include anche un server Jupyter notebook, un codice tooshare ambiente e l'analisi. notebook Jupyter Hello è accessibile tramite JupyterHub. Per eseguire l'accesso, usare il nome utente e la password locali di Linux.

Server notebook jupyter Hello preconfigurata con Python 2, 3 Python e kernel R. È disponibile un'icona desktop denominata "Server Jupyter Notebook" toolaunch hello browser tooaccess hello notebook server. Se si utilizza hello VM tramite SSH o X2Go client, è inoltre possibile visitare [https://localhost:8000 /](https://localhost:8000/) tooaccess hello server Jupyter notebook.

> [!NOTE]
> Se vengono visualizzati avvisi relativi al certificato, scegliere di continuare.
> 
> 

Server notebook jupyter hello è possibile accedere da qualsiasi host. digitando semplicemente *https://\<nome DNS o indirizzo IP della VM\>:8000/*

> [!NOTE]
> Porta 8000 viene aperta nel firewall hello per impostazione predefinita quando viene eseguito il provisioning hello VM.
> 
> 

È stato incluso nel pacchetto di esempi di blocchi appunti - Python in uno e uno in R. È possibile visualizzare esempi di hello collegamento toohello nella home page di hello notebook dopo l'autenticazione toohello server Jupyter notebook utilizzando il nome utente di Linux locale e la password. È possibile creare un nuovo blocco appunti selezionando **New**e quindi hello lingua appropriata kernel. Se non viene visualizzato hello **New** fare clic su hello **Jupyter** icona hello toogo sinistra superiore toohello home page di server notebook hello.

### <a name="apache-spark-standalone"></a>Apache Spark autonomo 
Un'istanza autonoma di Apache Spark è preinstallata in hello toohelp Linux DSVM sviluppare applicazioni Spark localmente prima prima di test e la distribuzione in cluster di grandi dimensioni. È possibile eseguire i programmi PySpark attraverso il kernel di Jupyter hello. Quando si apre Jupyter e fare clic sul pulsante "Nuovo" hello, verrà visualizzato un elenco di kernel disponibile. "Spark – Python" Hello è kernel PySpark hello che consente di compilare applicazioni usando il linguaggio Python di Spark. È inoltre possibile utilizzare un come PyCharm o Spyder toobuild nascita dell'IDE Python programma. Poiché si tratta di un'istanza autonoma, stack Spark hello viene eseguito all'interno di hello chiamata programma client. Questo rende più veloce e più facilmente problemi tootroubleshoot confrontata toodeveloping in un cluster Spark. 

Nel server Jupyter che è possibile trovare nella directory "SparkML" hello nella home directory di hello del server Jupyter ($HOME/notebook/SparkML/pySpark) è disponibile un notebook PySpark di esempio. 

Se si programma in R per Spark, è possibile usare Microsoft R Server, SparkR o sparklyr. 

Prima di eseguire nel contesto di Spark in Microsoft R Server, è necessario toodo un una volta il programma di installazione passaggio tooenable un singolo nodo Hadoop HDFS locale e un'istanza di Yarn. Per impostazione predefinita, i servizi Hadoop sono installati ma disabilitati su hello DSVM. In ordine tooenable, è necessario hello toorun seguenti comandi come hello radice prima volta:

    echo -e 'y\n' | ssh-keygen -t rsa -P '' -f ~hadoop/.ssh/id_rsa
    cat ~hadoop/.ssh/id_rsa.pub >> ~hadoop/.ssh/authorized_keys
    chmod 0600 ~hadoop/.ssh/authorized_keys
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa
    chown hadoop:hadoop ~hadoop/.ssh/id_rsa.pub
    chown hadoop:hadoop ~hadoop/.ssh/authorized_keys
    systemctl start hadoop-namenode hadoop-datanode hadoop-yarn

È possibile arrestare hello Hadoop relativi servizi quando non sono necessari eseguendo ````systemctl stop hadoop-namenode hadoop-datanode hadoop-yarn```` un esempio che illustri come Signora toodevelop e test nel contesto di Spark remoto (che è l'istanza di Spark autonoma hello in hello DSVM) viene fornito e disponibile in hello `/dsvm/samples/MRS` directory. 

### <a name="ides-and-editors"></a>IDE ed editor
È possibile scegliere tra diversi editor di codice. Ciò include VI/VIM, Emacs, gEdit, PyCharm, RStudio, Eclipse e IntelliJ. gEdit, Eclipse, IntelliJ, RStudio e PyCharm sono editor grafici e necessario toobe li ha firmati in toouse desktop grafica tooa. Questi editor dispongono di applicazione e desktop dal menu di scelta rapida toolaunch li.

**VIM** e **Emacs** sono editor basati su testo. Emacs, è stato installato un pacchetto di componente aggiuntivo denominato Emacs pronuncia statistiche (SSE) che consente più facilmente all'interno dell'editor Emacs hello working with R. Altre informazioni sono disponibili nella pagina relativa a [ESS](http://ess.r-project.org/).

**Eclipse** è un IDE open source estendibile che supporta più linguaggi. edizione gli sviluppatori Java di Hello è istanza hello installata su hello macchina virtuale. Sono disponibili i plug-in per i diversi linguaggi più diffusi che possono essere ambiente hello tooextend installato. È anche disponibile un plug-in installato in Eclipse, **Toolkit di Azure per Eclipse**. Consente di toocreate, sviluppare, testare e distribuire applicazioni Azure mediante l'ambiente di sviluppo Eclipse hello che supporta i linguaggi come Java. È inoltre disponibile un **Azure SDK per Java** che consente l'accesso toodifferent servizi di Azure da un ambiente Java. Altre informazioni su Azure Toolkit for Eclipse sono disponibili nella pagina [Azure Toolkit for Eclipse](../azure-toolkit-for-eclipse.md).

**Acrilica** viene installato tramite il pacchetto texlive hello insieme a un componente aggiuntivo Emacs [auctex](https://www.gnu.org/software/auctex/manual/auctex/auctex.html) pacchetto, che semplifica la creazione di documenti acrilica interno Emacs.  

### <a name="databases"></a>Database
#### <a name="postgres"></a>Postgres
database di origine aprire Hello **Postgres** è disponibile in hello macchina virtuale, con servizi hello in esecuzione e initdb già completata. È comunque necessario agli utenti e i database toocreate. Per ulteriori informazioni, vedere hello [Postgres documentazione](https://www.postgresql.org/docs/).  

#### <a name="graphical-sql-client"></a>Client SQL grafico
**Esce SQL**, un client SQL con interfaccia grafico, è stato fornito tooconnect toodifferent database (ad esempio Microsoft SQL Server, Postgres e MySQL) e query SQL toorun. Puoi eseguire da una sessione di desktop con interfaccia grafica (tramite client X2Go hello, ad esempio). tooinvoke esce SQL, è possibile avviarla dall'icona hello sul desktop hello o eseguire hello comando seguente nella shell di hello.

    /usr/local/squirrel-sql-3.7/squirrel-sql.sh

Prima di utilizzare innanzitutto hello, configurare i driver e gli alias di database. driver JDBC Hello si trovano in:

*/usr/share/Java/jdbcdrivers*

Per altre informazioni, vedere [SQL SQuirrel](http://squirrel-sql.sourceforge.net/index.php?page=screenshots).

#### <a name="command-line-tools-for-accessing-microsoft-sql-server"></a>Strumenti da riga di comando per l'accesso a Microsoft SQL Server
pacchetto di driver Hello ODBC per SQL Server è disponibili due strumenti da riga di comando:

**bcp**: hello bcp utilità copia bulk dei dati tra un'istanza di Microsoft SQL Server e un file di dati in un formato specificato dall'utente. utilità bcp Hello può essere utilizzato tooimport un numero elevato di nuove righe nelle tabelle di SQL Server o tooexport dati dalle tabelle in file di dati. tooimport dati in una tabella, è necessario utilizzare un file di formato creato per la tabella o conoscere la struttura della tabella di hello e i tipi di dati validi per le colonne hello hello.

Per altre informazioni, vedere [Connessione a bcp](https://msdn.microsoft.com/library/hh568446.aspx).

**SQLCMD**: È possibile immettere istruzioni Transact-SQL con l'utilità sqlcmd hello, nonché le procedure di sistema e i file del prompt dei comandi hello script. Questa utilità utilizza batch tooexecute Transact-SQL ODBC.

Per altre informazioni, vedere [Connessione con sqlcmd](https://msdn.microsoft.com/library/hh568447.aspx).

> [!NOTE]
> Esistono alcune differenze in questa utilità tra le piattaforme Linux e Windows. Vedere la documentazione di hello per informazioni dettagliate.
> 
> 

#### <a name="database-access-libraries"></a>Librerie di accesso al database
Sono disponibili librerie disponibili nei database tooaccess R e Python.

* In R, hello **RODBC** pacchetto o **dplyr** pacchetto consente tooquery o eseguire istruzioni SQL nel server di database hello.
* Nella finestra Python, hello **pyodbc** libreria fornisce l'accesso al database con ODBC come hello livello sottostante.  

tooaccess **Postgres**:

* Da r: Utilizzare hello un pacchetto di **RPostgreSQL**.
* Da Python: Hello utilizzare **psycopg2** libreria.

### <a name="azure-tools"></a>Strumenti di Azure
Hello seguendo gli strumenti di Azure viene installato in hello VM:

* **Interfaccia della riga di comando di Azure**: hello CLI di Azure consente toocreate e gestire le risorse di Azure tramite i comandi della shell. tooinvoke hello gli strumenti di Azure, è sufficiente digitare **Guida azure**. Per ulteriori informazioni, vedere hello [pagina della documentazione di Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* **Microsoft Azure Storage Explorer**: Microsoft Azure Storage Explorer è uno strumento grafico che viene utilizzato toobrowse tramite oggetti hello archiviati nell'account di archiviazione di Azure e tooand tooupload e download di dati BLOB di Azure. È possibile accedere a Esplora archivi dall'icona di collegamento sul desktop hello. Questo strumento può essere richiamato da un prompt della shell digitando **StorageExplorer**. Accesso eseguito da un client X2Go toobe necessarie o dispone di set di backup di inoltro X11.
* **Librerie di Azure**: hello seguito vengono illustrate alcune librerie di hello pre-installate.
  
  * **Python**: hello correlate ad Azure librerie in Python installati sono **azure**, **Azure ml**, **pydocumentdb**, e **pyodbc** . Con i primi tre librerie hello, è possibile accedere a servizi di archiviazione di Azure, Azure Machine Learning e Azure Cosmos DB (un database NoSQL in Azure). libreria quarto Hello, pyodbc (insieme hello driver Microsoft ODBC per SQL Server), consente accesso tooSQL Server, Database SQL di Azure e Azure SQL Data Warehouse da Python usando un'interfaccia ODBC. Immettere **elenco pip** toosee tutti hello elencati librerie. Essere toorun che questo comando in entrambi hello Python 2.7 e 3.5 ambienti.
  * **R**: hello Azure relative librerie in R installati sono **Azure ml** e **RODBC**.
  * **Java**: hello elenco delle librerie di Java di Azure è disponibile nella directory hello **/dsvm/sdk/AzureSDKJava** su hello macchina virtuale. librerie chiave Hello sono Azure archiviazione e la gestione API, Azure Cosmos DB e JDBC driver per SQL Server.  

È possibile accedere hello [portale di Azure](https://portal.azure.com) dal browser Firefox pre-installate hello. Nel portale di Azure hello, è possibile creare, gestire e monitorare le risorse di Azure.

### <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning è un servizio cloud completamente gestito che consente di toobuild, distribuire e condividere soluzioni analitica predittiva. Si possono creare esperimenti e modelli da Azure Machine Learning Studio, Essere accessibile da un browser web nella macchina virtuale di analisi scientifica dei dati hello visitando [Microsoft Azure Machine Learning](https://studio.azureml.net).

Dopo l'accesso tooAzure Machine Learning Studio, è necessario accedere tooan sperimentazione area di disegno in cui è possibile compilare un flusso logico per hello algoritmi di machine learning. Ha accesso tooa server Jupyter notebook ospitato in Azure Machine Learning e funziona perfettamente con esperimenti hello in Machine Learning Studio. Rendere operativo hello modelli di machine learning generati eseguendo il wrapping in un'interfaccia del servizio web. In questo modo i client scritti in eventuali stime tooinvoke language da hello modelli di machine learning. Per ulteriori informazioni, vedere hello [documentazione di Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

È possibile compilare anche i modelli R o Python su hello macchina virtuale e quindi distribuirla nell'ambiente di produzione in Azure Machine Learning. È stato installato librerie in R (**Azure ml**) e Python (**Azure ml**) tooenable questa funzionalità.

Per informazioni su come modelli di toodeploy in R e Python in Azure Machine Learning, vedere [dieci operazioni da eseguire su hello analisi scientifica dei dati macchina virtuale](machine-learning-data-science-vm-do-ten-things.md) (in particolare, hello sezione "compilazione di modelli utilizzando R o Python e rendere operative le loro con Azure Machine Learning").

> [!NOTE]
> Queste istruzioni sono state scritte per la versione di Windows hello di hello VM di analisi scientifica dei dati. Ma informazioni hello purché esista nella distribuzione di modelli tooAzure Machine Learning sono applicabile toohello VM Linux.
> 
> 

### <a name="machine-learning-tools"></a>Strumenti di Machine Learning
Hello VM viene fornito con alcuni di algoritmi che sono stati precompilati e pre-installati in locale e gli strumenti di apprendimento automatico. incluse le seguenti:

* **CNTK** (Computational Network Toolkit di Microsoft Research): toolkit di apprendimento avanzato.
* **Vowpal Wabbit**: algoritmo di apprendimento rapido online.
* **xgboost**: strumento che fornisce algoritmi di albero con boosting ottimizzati.
* **Python**: Anaconda Python integra algoritmi Machine Learning con librerie come Scikit-learn. È possibile installare altre librerie mediante hello `pip install` comando.
* **R**: una libreria completa delle funzioni di machine learning è disponibile per R. Alcune delle librerie di hello pre-installati sono lm, glm, randomForest, rpart. Altre librerie possono essere installate eseguendo:
  
        install.packages(<lib name>)

Ecco alcune informazioni aggiuntive sul hello innanzitutto tre strumenti di apprendimento di computer nell'elenco di hello.

#### <a name="cntk"></a>CNTK
È un toolkit open source di apprendimento avanzato È uno strumento da riga di comando (cntk) ed è già in hello percorso.

toorun un esempio di base, eseguire hello comandi nella shell di hello seguenti:

    cd /home/[USERNAME]/notebooks/CNTK/HelloWorld-LogisticRegression
    cntk configFile=lr_bs.cntk makeMode=false command=Train

Per ulteriori informazioni, vedere la sezione CNTK di hello [GitHub](https://github.com/Microsoft/CNTK), hello e [CNTK wiki](https://github.com/Microsoft/CNTK/wiki).

#### <a name="vowpal-wabbit"></a>Vowpal Wabbit
Vowpal Wabbit è un sistema di apprendimento automatico che usa tecniche come hash, allreduce, reduction, learning2search, nonché apprendimento online, attivo e interattivo.

strumento di hello toorun su un esempio molto semplice, hello seguenti:

    cp -r /dsvm/tools/VowpalWabbit/demo vwdemo
    cd vwdemo
    vw house_dataset

Nella directory sono presenti altre demo più approfondite. Per ulteriori informazioni sulle unità VW, vedere [in questa sezione di GitHub](https://github.com/JohnLangford/vowpal_wabbit), hello e [wiki di Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit/wiki).

#### <a name="xgboost"></a>XGBoost
Si tratta di una libreria progettata e ottimizzata per gli algoritmi di albero con boosting. obiettivo di Hello di questa libreria è limiti di calcolo toopush hello di estremi toohello macchine necessari tooprovide boosting dell'albero su larga scala che sia scalabile, portabile e accurate.

Viene fornita sia come riga di comando che come libreria R.

toouse questa libreria in R, è possibile avviare una sessione interattiva di R (digitando semplicemente **R** nella shell di hello) e il caricamento della libreria di hello.

Ecco un semplice esempio eseguibile al prompt di R:

    library(xgboost)

    data(agaricus.train, package='xgboost')
    data(agaricus.test, package='xgboost')
    train <- agaricus.train
    test <- agaricus.test
    bst <- xgboost(data = train$data, label = train$label, max.depth = 2,
                    eta = 1, nthread = 2, nround = 2, objective = "binary:logistic")
    pred <- predict(bst, test$data)

riga di comando xgboost hello toorun, ecco hello comandi tooexecute nella shell di hello:

    cp -r /dsvm/tools/xgboost/demo/binary_classification/ xgboostdemo
    cd xgboostdemo
    xgboost mushroom.conf


Un file. Model viene scritto toohello directory specificata. Altre informazioni su questa demo sono disponibili [su GitHub](https://github.com/dmlc/xgboost/tree/master/demo/binary_classification).

Per ulteriori informazioni su xgboost, vedere hello [pagina della documentazione xgboost](https://xgboost.readthedocs.org/en/latest/)e il relativo [repository GitHub](https://github.com/dmlc/xgboost).

#### <a name="rattle"></a>Rattle
Rattle (hello **R** **A**nalytical **T**Tool esegue **T**o **L**guadagnare **E** asily) utilizza modellazione e l'esplorazione dei dati basata su interfaccia utente grafica. Presenta statistiche e visual riepiloghi dei dati, trasformazioni che possono essere modellate immediatamente, compila supervisionati e non supervisionati modelli dai dati hello presenta hello prestazioni dei modelli graficamente e set di dati nuovi di punteggi. Genera inoltre il codice R, la replica di operazioni di hello in hello dell'interfaccia utente che possono essere eseguite direttamente nello R o utilizzate come punto di partenza per un'ulteriore analisi.

toorun sonagli, è necessario toobe in una grafica desktop sessione di accesso. Nella finestra terminal hello, digitare ```R``` ambiente hello R tooenter. Al prompt dei comandi hello R, immettere hello seguenti comandi:

    library(rattle)
    rattle()

Si apre un'interfaccia grafica con un set di schede. Di seguito sono hello passaggi toouse sonagli necessario un set di dati meteo di esempio e compilare un modello di avvio rapido. Alcuni dei passaggi di hello riportati di seguito, si installa tooautomatically richiesta e caricare alcuni pacchetti R richiesti che sono già disponibili nel sistema hello.

> [!NOTE]
> Se non si dispone di pacchetto di accesso tooinstall hello nella directory di sistema hello (impostazione predefinita hello), venga visualizzato un prompt dei comandi in R console finestra tooinstall pacchetti tooyour libreria personali. Se vengono visualizzate queste richieste, rispondere *y* (Sì).
> 
> 

1. Fare clic su **Execute**.
2. Una finestra di dialogo viene visualizzata, in cui viene richiesto se si desidera toouse hello esempio set di dati meteo. Fare clic su **Sì** esempio hello tooload.
3. Fare clic su hello **modello** scheda.
4. Fare clic su **Execute** toobuild un albero delle decisioni.
5. Fare clic su **disegnare** albero delle decisioni di hello toodisplay.
6. Fare clic su hello **foresta** pulsante di opzione e fare clic su **Execute** toobuild una foresta casuale.
7. Fare clic su hello **Evaluate** scheda.
8. Fare clic su hello **rischio** pulsante di opzione e fare clic su **Execute** toodisplay due rischio (cumulativo) prestazioni tracciati.
9. Fare clic su hello **Log** hello tooshow scheda generare il codice R per hello operazioni precedenti.
   (A causa di tooa bug nella versione corrente di hello di sonagli, è necessario tooinsert un  *#*  carattere davanti *esportare questo file di registro...*  nel testo hello del log hello.)
10. Fare clic su hello **esportare** file script di pulsante toosave hello R denominato *weather_script. R* toohello home directory.

È possibile uscire sonagli e R. È possibile modificare lo script R hello generato o utilizzarlo come toorun, in qualsiasi momento toorepeat tutto ciò che è stata eseguita all'interno di hello Rattle dell'interfaccia utente. In particolare per utenti meno esperti in R, questo è un modo semplice tooquickly eseguire analisi e machine learning in un'interfaccia grafica semplice, durante la generazione automatica di codice in R toomodify e/o informazioni.

## <a name="next-steps"></a>Passaggi successivi
Ecco come è possibile continuare l'apprendimento e l'esplorazione:

* Hello [analisi scientifica dei dati nella macchina virtuale di analisi scientifica dei dati di Linux hello](machine-learning-data-science-linux-dsvm-walkthrough.md) procedura dettagliata viene illustrato come tooperform attività più comuni analisi scientifica dei dati con hello VM di analisi scientifica dei dati di Linux provisioning qui. 
* Esplorare hello vari strumenti di analisi scientifica dei dati su hello analisi scientifica dei dati VM provando ad strumenti hello descritti in questo articolo. È anche possibile eseguire *dsvm-più-info* su shell hello hello di macchina virtuale per un'introduzione e i puntatori toomore le informazioni di base sugli strumenti hello installato hello VM.  
* Informazioni su come soluzioni di analisi end-to-end toobuild sistematicamente utilizzando hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).
* Visitare hello [Cortana Analitica raccolta](http://gallery.cortanaanalytics.com) per analitica di machine learning e i dati di esempio che hello utilizzare Cortana Analitica Suite.

