---
title: hello aaaProvision macchina virtuale di Microsoft Data Science | Documenti Microsoft
description: Configurare e creare una macchina virtuale di Data Science in Azure per l'analisi dei dati e l'apprendimento automatico.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e1467c0f-497b-48f7-96a0-7f806a7bec0b
ms.service: machine-learning
ms.workload: data-services
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 907a3bdc7e480d05e8e245f5e50d632900fcf471
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-hello-microsoft-data-science-virtual-machine"></a>Eseguire il provisioning di hello macchina virtuale di analisi scientifica dei dati di Microsoft
Hello macchina virtuale di Microsoft Data Science è un'immagine di macchina virtuale (VM) di Windows Azure pre-installato e configurato con diversi strumenti comuni che vengono generalmente utilizzati per analitica dei dati e machine learning. sono inclusi gli strumenti di Hello:

* Microsoft R Server Developer Edition
* Distribuzione Anaconda Python
* Notebook Jupyter (con kernel R o Python)
* Visual Studio Community Edition
* Power BI Desktop
* SQL Server 2016 Developer Edition
* Strumenti di apprendimento automatico e analisi dei dati
  * [Computational Network Toolkit (CNTK)](https://github.com/Microsoft/CNTK): toolkit di software di formazione avanzato sviluppato da Microsoft Research.
  * [Vowpal Wabbit](https://github.com/JohnLangford/vowpal_wabbit): sistema di apprendimento automatico rapido che supporta tecniche come hash, allreduce, reduction, learning2search, nonché apprendimento online, attivo e interattivo.
  * [XGBoost](https://xgboost.readthedocs.org/en/latest/): strumento che consente un'implementazione dell'albero con boosting rapida e accurata.
  * [Rattle](http://rattle.togaware.com/) (strumento di analisi R tooLearn hello facilmente): uno strumento che consente l'introduzione analitica dei dati e machine learning in R semplice, con l'esplorazione dei dati basata su interfaccia utente grafica e di modellazione con generazione automatica di codice R.
  * [mxnet](https://github.com/dmlc/mxnet): un framework di apprendimento avanzato progettato per l'efficienza e la flessibilità
  * [Weka](http://www.cs.waikato.ac.nz/ml/weka/): software di apprendimento automatico e data mining visivo in Java.
  * [Apache Drill](https://drill.apache.org/): motore di query SQL senza schema per Hadoop, NoSQL e Cloud Storage.  Supporta ODBC e JDBC tooenable interfacce NoSQL e i file di strumenti di Business Intelligence standard, come Power BI, Excel, Tableau l'esecuzione di query.
* Librerie in R e Python da usare in Azure Machine Learning e altri servizi di Azure
* GIT inclusi Git Bash toowork repository di codice sorgente incluso GitHub, Visual Studio Team Services
* Porte Windows di diverse comuni utilità della riga di comando di Linux (tra cui awk, sed, perl, grep, find, wget, curl e così via) accessibili dal prompt dei comandi. 

L'esecuzione dell'analisi scientifica dei dati comporta l'iterazione di una sequenza di attività quali:

1. Ricerca, caricamento e pre-elaborazione dei dati
2. Compilazione e test di modelli
3. Distribuzione di modelli di hello per l'utilizzo in applicazioni intelligenti

Gli esperti di dati utilizzano un'ampia gamma di strumenti toocomplete queste attività. Può essere molto tempo toofind versioni appropriate di hello del software di hello e quindi scaricare e installarli. Hello macchina virtuale di Microsoft Data Science facilita queste problematiche offrendo un'immagine di pronto all'uso che è possibile effettuare il provisioning in Azure con tutti i più comuni strumenti di pre-installato e configurato. 

Macchina virtuale di Microsoft Data Science Hello jump-starts progetto analitica. Consente di toowork attività in varie lingue, tra cui R, Python, SQL e c#. Visual Studio fornisce un toodevelop IDE e testare il codice che è facile toouse. Hello incluso in hello VM di Azure SDK consente toobuild applicazioni utilizzando i vari servizi nella piattaforma cloud di Microsoft. 

Per questa immagine di VM per l'analisi scientifica dei dati non sono previsti costi per il software. Si paga solo per gli addebiti di utilizzo di Azure hello dipendenti dai quali dimensioni hello della macchina virtuale hello che viene effettuato il provisioning. Ulteriori dettagli su hello calcolano le commissioni sono reperibile nella sezione dettagli prezzi hello hello [macchina virtuale di analisi scientifica dei dati](https://azure.microsoft.com/marketplace/partners/microsoft-ads/standard-data-science-vm/) pagina. 

## <a name="other-versions-of-hello-data-science-virtual-machine"></a>Altre versioni di hello macchina virtuale di analisi scientifica dei dati
Oggetto [CentOS](machine-learning-data-science-linux-dsvm-intro.md) immagine è disponibile, con molti hello stesso strumenti come immagine di Windows hello. È disponibile anche un'immagine [Ubuntu](machine-learning-data-science-dsvm-ubuntu-intro.md), con molti strumenti simili, oltre a framework di apprendimento avanzato.

## <a name="prerequisites"></a>Prerequisiti
Prima di creare una macchina virtuale di Microsoft Data Science, è necessario disporre delle seguenti hello:

* **Una sottoscrizione di Azure**: tooobtain uno, vedere [versione di valutazione gratuita di Azure ottenere](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Un account di archiviazione di Azure**: toocreate uno, vedere [creare un account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account). In alternativa, è possibile creare account di archiviazione di hello come parte del processo di hello di creazione di hello macchina virtuale se non si desidera toouse un account esistente.

## <a name="create-your-microsoft-data-science-virtual-machine"></a>Creare la macchina virtuale per l'analisi scientifica dei dati di Microsoft
Di seguito è hello passaggi toocreate un'istanza di macchina virtuale di Microsoft Data Science hello:

1. Passare una macchina virtuale toohello elenco su [portale di Azure](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).
2. Seleziona hello **crea** pulsante toobe inferiore hello tiene una procedura guidata.![ configurare-data-scienza-vm](./media/machine-learning-data-science-provision-vm/configure-data-science-virtual-machine.png)
3. Hello guidata utilizzata toocreate hello macchina virtuale di Microsoft Data Science richiede **input** per ognuna delle hello **cinque passaggi** enumerata in hello destra della figura. Di seguito sono hello input Necessito tooconfigure ciascuna di queste operazioni:
   
   1. **Nozioni di base**
      
      1. **Name**: nome del server di analisi scientifica dei dati che si sta creando.
      2. **Nome utente**: ID di accesso dell'account amministratore.
      3. **Password**: password dell'account amministratore.
      4. **Sottoscrizione**: se si dispone di più di una sottoscrizione, selezionare hello uno in cui hello il computer è toobe creato e fatturato.
      5. **Gruppo di risorse**: è possibile creare un nuovo gruppo di risorse o usarne uno esistente.
      6. **Percorso**: hello selezionare data center situato più appropriato. In genere è centro dati hello che include la maggior parte dei dati o è più vicino tooyour di posizione fisica per l'accesso di rete più veloce.
   2. **Dimensioni**: selezionare uno dei tipi di server hello che soddisfa i requisiti funzionali e vincoli di costo. Per accedere ad altre opzioni di dimensioni delle VM, selezionare "Visualizza tutto".
   3. **Impostazioni**:
      
      1. **Tipo di disco**: scegliere Premium se si preferisce un'unità SSD, in caso contrario scegliere "Standard".
      2. **Account di archiviazione**: È possibile creare un nuovo account di archiviazione di Azure nella sottoscrizione o utilizzarne uno esistente in hello stesso *percorso* che è stato scelto in hello **nozioni di base** passaggio della procedura guidata hello.
      3. **Altri parametri**: in genere è sufficiente utilizzare i valori predefiniti di hello. È possibile passare il mouse su un collegamento informativo hello per informazioni su campi specifici di hello nel caso in cui si desidera utilizzare hello tooconsider di valori non predefiniti.
   4. **Riepilogo**: verificare che tutte le informazioni immesse siano corrette.
   5. **Acquistare**: fare clic su **acquistare** toostart hello provisioning. Termini toohello di transazione hello viene fornito un collegamento. Hello macchina virtuale non dispone di costi aggiuntivi oltre calcolo hello per le dimensioni del server hello scelto nel hello **dimensioni** passaggio. 

> [!NOTE]
> provisioning di Hello dovrebbe richiedere circa 10-20 minuti. stato di Hello di provisioning hello viene visualizzato nel portale di Azure hello.
> 
> 

## <a name="how-tooaccess-hello-microsoft-data-science-virtual-machine"></a>Come tooaccess hello macchina virtuale di analisi scientifica dei dati di Microsoft
Una volta hello viene creata la VM, è possibile desktop remoto usando le credenziali dell'account amministratore hello configurata in precedenza hello **nozioni di base** sezione. 

Dopo aver creata la macchina virtuale e il provisioning, si è pronti toostart hello strumenti vengono installati e configurati su di esso. Sono presenti riquadri del menu start e icone del desktop per la maggior parte degli strumenti hello. 

## <a name="how-toocreate-a-strong-password-for-jupyter-and-start-hello-notebook-server"></a>Come una password complessa per l'avvio e Jupyter toocreate hello server notebook
Per impostazione predefinita, server notebook jupyter hello è preconfigurato ma disabilitata nella macchina virtuale hello finché non viene impostata una password Jupyter. chiamato hello esecuzione comando da un prompt dei comandi nel hello Data Science macchina virtuale o fare doppio clic sul collegamento sul desktop hello nostre seguente toocreate una password complessa per hello server notebook jupyter installato nel computer di hello,  **Imposta Password Jupyter & inizio** da un account di amministratore locale di macchina virtuale.

    C:\dsvm\tools\setup\JupyterSetPasswordAndStart.cmd

Seguire i messaggi hello e scegliere una password complessa quando richiesto.

Hello script precedente crea un hash della password e le archivia nel file di configurazione Jupyter hello che si trovano in: **C:\ProgramData\jupyter\jupyter_notebook_config.py** sotto il nome di parametro hello ***c. NotebookApp.password***.

script Hello attiva e l'esecuzione anche server Jupyter hello in background hello. Server Jupyter viene creata un'attività di windows in utilità di pianificazione di WIndows hello chiamato **Start_IPython_Notebook**.  È possibile toowait per pochi secondi dopo l'impostazione di password hello prima di aprire Blocco note hello del browser. Vedere hello sezione seguente **server Jupyter Notebook** in modo tooaccess hello server Jupyter notebook. 


## <a name="tools-installed-on-hello-microsoft-data-science-virtual-machine"></a>Strumenti installati nella macchina virtuale di Microsoft Data Science hello

### <a name="microsoft-r-server-developer-edition"></a>Microsoft R Server Developer Edition
Se si desidera l'analitica toouse R, hello VM è Microsoft R Server Developer edition installata. Microsoft R Server è una piattaforma di analisi di livello aziendale su vasta scala basata su R supportata, scalabile e sicura. Supporta un'ampia gamma di statistiche di dati di grandi dimensioni, la modellazione predittiva e funzionalità di apprendimento automatico, R Server supporta una gamma completa di hello di analitica: esplorazione, analisi, visualizzazione e modellazione. Per utilizzo ed estensione R open source, Microsoft R Server è completamente compatibile con gli script R, funzioni e i pacchetti CRAN, tooanalyze dati su scala enterprise. Inoltre, gli indirizzi limitazioni di hello in memoria di R di origine aprire aggiungendo parallele e blocchi l'elaborazione dei dati. In questo modo è analitica toorun sui dati di dimensioni molto maggiori rispetto a ciò che rientra nella memoria principale.  Visual Studio Community Edition incluso nel hello che VM contiene strumenti R hello per le estensioni di Visual Studio che fornisce un IDE completo per l'uso di R. È anche possibile scaricare e usare altri IDE, nonché come [RStudio](http://www.rstudio.com). 

### <a name="python"></a>Python
Per lo sviluppo tramite Python, è installata la distribuzione Anaconda Python 2.7 e 3.5. Questo tipo di distribuzione contiene hello Python con circa 300 di hello più diffusi matematiche, ingegneria e analitica pacchetti di dati di base. È possibile utilizzare gli strumenti Python per Visual Studio (PTVS) che viene installato all'interno di edizione di Visual Studio 2015 Community hello o un IDE in bundle con Anaconda come inattivo o Spyder hello. È possibile avviare uno di questi eseguendo una ricerca nella barra di ricerca hello (**Win** + **S** chiave).

> [!NOTE]
> hello toopoint Python Tools per Visual Studio in Anaconda Python 2.7 e 3.5, è necessario toocreate personalizzato ambienti per ogni versione. passare a troppo tooset di questi percorsi di ambiente in Visual Studio 2015 Community Edition, hello**strumenti** -> **Python Tools** -> **gliambientiPython** e quindi fare clic su **+ personalizzato**. 
> 
> 

Anaconda Python 2.7 viene installato in C:\Anaconda e Anaconda Python 3.5 viene installato in C:\Anaconda\envs\py35. Per la procedura dettagliata, vedere la [documentazione di PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) . 

### <a name="jupyter-notebook"></a>Notebook Jupyter
Distribuzione anaconda include anche un server Jupyter notebook, un codice tooshare ambiente e l'analisi. Un server Jupyter Notebook è stato preconfigurato con Python 2.7, Python 3.4, Python 3.5 e i kernel R. È disponibile un'icona desktop denominata "server Jupyter Notebook toolaunch hello browser tooaccess hello server Notebook. Se si utilizza hello macchina virtuale tramite desktop remoto, è inoltre possibile visitare [https://localhost:9999 /](https://localhost:9999/) tooaccess hello server Jupyter notebook quando toohello macchina virtuale è connesso.

> [!NOTE]
> Se vengono visualizzati avvisi relativi al certificato, scegliere di continuare. 
> 
> 

Ci sono incluse diverse notebook esempio Python e in R. hello Mostra notebook Jupyter come toowork con Microsoft R Server, SQL Server 2016 R Services (analitica nel database), Python, Microsoft cognitivi ToolKit (CNTK) per l'apprendimento completa e altri Azure tecnologie di una volta che si accede tooJupyter. È possibile visualizzare esempi di hello collegamento toohello nella home page di hello notebook dopo l'autenticazione tramite password hello creata in un passaggio precedente toohello server Jupyter notebook. 

### <a name="visual-studio-2015-community-edition"></a>Visual Studio 2015 Community Edition
Visual Studio Community edition installato nella macchina virtuale hello. È una versione gratuita di hello IDE più diffusi da Microsoft che è possibile utilizzare per scopi di valutazione e per piccoli team. È possibile estrarre hello alle condizioni di licenza [qui](https://www.visualstudio.com/support/legal/mt171547).  Aprire Visual Studio facendo doppio clic sull'icona sul desktop hello o hello **avviare** menu. È anche possibile cercare i programmi usando la combinazione di tasti **Win** + **S** e immettendo "Visual Studio". È quindi possibile creare progetti in linguaggi come C#, Python, R e node.js. I plug-in vengono installati anche che la rendono utile toowork con servizi di Azure quali Azure Data Catalog, Azure HDInsight (Hadoop, Spark) e Azure Data Lake. 

> [!NOTE]
> Potrebbe essere visualizzato un messaggio indicante che il periodo di valutazione è scaduto. Immettere le credenziali dell'account Microsoft o creare un nuovo toohello di accesso di account gratuito tooget Visual Studio Community Edition. 
> 
> 

### <a name="sql-server-2016-developer-edition"></a>SQL Server 2016 Developer Edition
Nel hello macchina virtuale è disponibile una versione per gli sviluppatori di SQL Server 2016 con analitica di R Services toorun nel database. I servizi R offrono una piattaforma per lo sviluppo e la distribuzione di applicazioni intelligenti. È possibile usare linguaggio R, potente e ricco di hello e hello molti pacchetti dai modelli di toocreate community hello e generare stime per i dati di SQL Server. È possibile mantenere i dati toohello Chiudi analitica perché R Services (In-database) integrazione linguaggio hello R con SQL Server. In questo modo si evita hello costi e i rischi di sicurezza associati allo spostamento dei dati.

> [!NOTE]
> Hello SQL Server 2016 developer edition può essere utilizzato solo per lo sviluppo e a scopo di test. È necessario un toorun di licenza in produzione. 
> 
> 

È possibile accedere a server SQL hello avviando **SQL Server Management Studio**. Il nome della macchina virtuale viene popolato con hello nome del Server. Utilizzare l'autenticazione di Windows durante l'accesso come amministratore in Windows hello. Una volta eseguito l'accesso a SQL Server Management Studio è possibile creare altri utenti, creare database, importare i dati ed eseguire query SQL. 

analitica tooenable nel database utilizzando Microsoft R, eseguire hello dopo un comando ora azione SQL Server management Studio dopo l'accesso come amministratore del server hello. 

        CREATE LOGIN [%COMPUTERNAME%\SQLRUserGroup] FROM WINDOWS 

        (Please replace hello %COMPUTERNAME% with your VM name)


### <a name="azure"></a>Azure
Nel hello VM vengono installati diversi strumenti di Azure:

* È un collegamento sul desktop di tooaccess documentazione di Azure SDK hello. 
* **AzCopy**: utilizzato toomove dati da e verso l'Account di archiviazione di Microsoft Azure. utilizzo di toosee, tipo **Azcopy** un utilizzo di hello toosee prompt dei comandi. 
* **Microsoft Azure Storage Explorer**: utilizzato toobrowse tramite oggetti hello archiviati all'interno del tooand dati Account di archiviazione di Azure e il trasferimento dall'archiviazione di Azure. È possibile digitare **Esplora archivi** in Cerca o trova sul hello tooaccess di menu Start di Windows questo strumento. 
* **Adlcopy**: utilizzato toomove dati tooAzure Data Lake. utilizzo di toosee, tipo **adlcopy** un prompt dei comandi. 
* **dtui**: utilizzato toomove tooand di dati da un database NoSQL nel cloud hello Azure Cosmos DB. Digitare **dtui** al prompt dei comandi. 
* **Gateway di gestione dati di Microsoft**: consente lo spostamento di dati tra origini dati locali e il cloud. Viene usato all'interno di strumenti come Data Factory di Azure. 
* **Microsoft Azure Powershell**: uno strumento utilizzato tooadminister le risorse di Azure in hello Powershell linguaggio di scripting viene installato anche nella macchina virtuale. 

### <a name="power-bi"></a>Power BI
toohelp compili dashboard e visualizzazioni grande, hello **Power BI Desktop** è stato installato. Utilizzare questi dati toopull strumento provenienti da origini diverse, tooauthor dashboard e report e toopublish li toohello cloud. Per informazioni, vedere hello [Power BI](http://powerbi.microsoft.com) sito. Power BI desktop sono disponibili nel menu di avvio hello. 

> [!NOTE]
> È necessario un tooaccess account Office 365 Power BI. 
> 
> 

## <a name="additional-microsoft-development-tools"></a>Altri strumenti di sviluppo Microsoft
Hello [ **installazione guidata piattaforma Web di Microsoft** ](https://www.microsoft.com/web/downloads/platform.aspx) possibile toodiscover utilizzato e scaricare altri strumenti di sviluppo Microsoft. È inoltre disponibile uno strumento di toohello collegamento fornito nel desktop di macchina virtuale di Microsoft Data Science hello.  

## <a name="important-directories-on-hello-vm"></a>Directory importante hello VM
| Elemento | Directory |
| --- | --- |
| Configurazioni del server Jupyter Notebook |C:\ProgramData\jupyter |
| Home directory degli esempi di Jupyter Notebook |c:\dsvm\notebooks |
| Altri esempi |c:\dsvm\samples |
| Anaconda (impostazione predefinita: Python 2.7) |c:\Anaconda |
| Ambiente Anaconda Python 3.5 |c:\Anaconda\envs\py35 |
| Directory dell'istanza autonoma di R Server (istanza predefinita di R basata su R3.2.2) |C:\Programmi\Microsoft SQL Server\130\R_SERVER |
| Directory dell'istanza nel database di R Server (R3.2.2) |C:\Programmi\Microsoft SQL Server\MSSQL13. MSSQLSERVER\R_SERVICES |
| Directory dell'istanza di Microsoft R Open (R3.3.1) |C:\Programmi\Microsoft\MRO-3.3.1 |
| Strumenti vari |c:\dsvm\tools |

> [!NOTE]
> Le istanze di macchina virtuale di Microsoft Data Science creato prima 1.5.0 (prima 3 settembre 2016) hello utilizzate una struttura di directory leggermente diverso rispetto a quanto specificato nella tabella precedente hello. 
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Ecco alcuni toocontinue passaggi successivi, l'apprendimento e l'esplorazione. 

* Esplorare i diversi strumenti di analisi scientifica dei dati su poiché analisi scientifica dei dati hello VM facendo hello menu di avvio e l'estrazione di strumenti hello elencati nel menu hello hello.
* Passare troppo**C:\Program Files\Microsoft SQL Server\130\R_SERVER\library\RevoScaleR\demoScripts** per esempi di libreria RevoScaleR hello in R che supporta analitica dei dati su scala enterprise.  
* Leggere l'articolo hello: [10 operazioni da eseguire su hello analisi scientifica dei dati macchina virtuale](http://aka.ms/dsvmtenthings)
* Informazioni su come toobuild tooend analitici soluzioni end sistematicamente utilizzando hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/data-science-process/).
* Visitare hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com) per analitica di machine learning e i dati di esempio che hello utilizzare Cortana Intelligence Suite. Microsoft fornisce anche un'icona su hello **avviare** menu e sul desktop di hello della raccolta di toothis hello macchina virtuale.

