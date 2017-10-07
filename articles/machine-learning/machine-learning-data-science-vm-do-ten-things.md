---
title: aaaTen operazioni da eseguire nella macchina virtuale di analisi scientifica dei dati di hello | Documenti Microsoft
description: "Eseguire varie attività di modellazione ed esplorazione dei dati in analisi scientifica dei dati hello macchina virtuale."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Dieci operazioni che è possibile eseguire su analisi scientifica dei dati hello macchina virtuale
Hello Microsoft Data Science macchina virtuale (DSVM) è un ambiente di sviluppo dell'analisi scientifica dei dati potente che consente di tooperform varie attività di esplorazione e modellazione dei dati. Hello ambiente viene fornito già compilato e in dotazione con i dati più diffusi diversi strumenti analitica che consentono di tooget facile iniziare rapidamente con l'analisi per On-Premise, Cloud o ibrida distribuzioni. Hello DSVM collabora a stretto contatto con molti servizi di Azure ed è in grado di tooread ed elaborare dati che sono già archiviati in Azure, Azure SQL Data Warehouse, Azure Data Lake, archiviazione di Azure o nel database di Azure Cosmos. Può anche sfruttare altri strumenti di analisi come Azure Machine Learning e Azure Data Factory.

In questo articolo viene illustrato come toouse il tooperform DSVM analisi scientifica dei dati di varie attività e interagire con altri servizi di Azure. Ecco alcune delle operazioni di hello che è possibile eseguire sul hello DSVM:

1. Esplorare i dati e lo sviluppo di modelli in locale hello DSVM utilizzando Microsoft R Server, Python
2. Usare un tooexperiment notebook Jupyter con i dati in un browser utilizzando una versione di pronto dell'organizzazione di R progettato per la scalabilità e prestazioni di Python 2, 3 Python, Microsoft R
3. Rendere operativi i modelli compilati usando R e Python in Azure Machine Learning in modo che le applicazioni client possano accedere ai modelli con una semplice interfaccia di servizi Web
4. Amministrare le risorse di Azure usando il portale di Azure o PowerShell
5. Estendere lo spazio di archiviazione e condividere codice o set di dati su larga scala con l'intero team creando un archivio file di Azure come unità installabile in DSVM
6. Condividere codice con il team tramite GitHub e accedere repository utilizzando hello pre-installate client Git - Git Bash, GUI Git.
7. Accedere a diversi servizi dati e analisi di Azure, ad esempio Archiviazione BLOB di Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse e database
8. Creare report e dashboard tramite Power BI Desktop pre-installato hello DSVM hello e distribuirle nel cloud hello
9. Applicare la scalabilità dinamicamente il toomeet DSVM che richiesto dal progetto
10. Installare strumenti aggiuntivi nella macchina virtuale   

> [!NOTE]
> Spese aggiuntive si applicano per molti servizi hello dati aggiuntivi analitica e archiviazione elencate in questo articolo. Consultare toohello [dei prezzi di Azure](https://azure.microsoft.com/pricing/) pagina per informazioni dettagliate.
> 
> 

**Prerequisiti**

* È necessaria una sottoscrizione di Azure. È possibile iscriversi per una versione di valutazione gratuita di Azure [qui](https://azure.microsoft.com/free/).
* Istruzioni per il provisioning di una macchina virtuale di analisi scientifica dei dati nel portale di Azure hello [la creazione di una macchina virtuale](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Esplorare dati e sviluppare modelli usando Microsoft R Server o Python
È possibile utilizzare linguaggi come R e Python toodo analitica i dati direttamente nel hello DSVM.

Per R, è possibile utilizzare un ambiente di sviluppo integrato denominato "Revolution R Enterprise 8.0" sono disponibili nel menu start hello o desktop hello. Librerie aggiuntive sopra hello Apri origine/CRAN-R tooenable scalabile analitica e hello possibilità tooanalyze dati più grande delle dimensioni di memoria hello consentita in questo modo parallelo analisi blocchi forniti da Microsoft. È anche possibile installare l'IDE R di desiderato, ad esempio [RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Per Python, è possibile utilizzare un IDE come Visual Studio Community Edition che ha hello strumenti Python per l'estensione di Visual Studio (PTVS) pre-installato. Per impostazione predefinita, in PTVS è configurato solo Python 2.7 di base, senza librerie di analisi come SciKit o Pandas. In ordine tooenable Anaconda Python 2.7 e 3.5, è necessario seguente hello toodo:

* Creare ambienti personalizzati per ogni versione passando troppo**strumenti** -> **Python Tools** -> **ambienti Python** e quindi fare clic su " **+ Personalizzato**"in Visual Studio 2015 Community Edition hello
* Immettere una descrizione e impostare l'ambiente di hello percorsi prefisso come *c:\anaconda* per Anaconda Python 2.7 o *c:\anaconda\envs\py35* per Anaconda Python 3.5
* Fare clic su **rilevamento automatico** e quindi **applica** ambiente hello toosave.

Di seguito è riportato il programma di installazione di hello ambiente personalizzato simile in Visual Studio.

![Configurazione di PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Vedere hello [documentazione PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) per altre informazioni su come toocreate ambienti Python.

Ora è l'impostazione toocreate un nuovo progetto di Python. Passare troppo**File** -> **New** -> **progetto** -> **Python** e selezionare il tipo di hello di Applicazione Python che si sta compilando. È possibile impostare l'ambiente Python hello hello corrente progetto toohello versione desiderata (Anaconda 2.7 o 3.5): pulsante destro del mouse hello **ambiente Python**selezionare **gli ambienti Python Aggiungi/Rimuovi**, e quindi seleziona hello desiderato tooassociate ambiente progetto hello. È possibile trovare ulteriori informazioni sull'utilizzo di PTVS prodotto hello [documentazione](https://github.com/Microsoft/PTVS/wiki) pagina.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. Usando i dati di un modello e un server Jupyter Notebook tooexplore con Python o R
Hello Server Jupyter Notebook è un ambiente potente che fornisce basate su browser "IDE" per la modellazione e l'esplorazione dei dati. È possibile utilizzare Python 2, 3 Python o R (Open Source e Microsoft R Server hello) in un server Jupyter Notebook.

hello toolaunch server Jupyter Notebook fare clic sull'icona del menu start hello / icona sul desktop denominato **server Jupyter Notebook**. In hello DSVM è inoltre possibile esplorare troppo "https://localhost:9999 /" tooaccess hello Jupiter Notebook. Se viene richiesto di immettere una password, usare le istruzioni fornite in hello ***come una password complessa nel server notebook jupyter hello toocreate*** sezione di hello [hello provisioning macchina virtuale di Microsoft Data Science](machine-learning-data-science-provision-vm.md)toocreate argomento un server Jupyter notebook hello tooaccess di una password complessa. 

Dopo aver aperto notebook hello, dovrebbe essere una directory che contiene alcuni blocchi appunti di esempio che sono sotto forma di pacchetto in hello DSVM. A questo punto è possibile:

* Fare clic sul codice hello toosee di hello notebook.
* Eseguire ogni cella premendo **MAIUSC+INVIO**.
* eseguire l'intero blocco hello facendo clic su **cella** -> **eseguire**
* creare un nuovo blocco appunti facendo clic sul hello icona Jupyter (angolo superiore sinistro) e quindi fare clic su **New** pulsante hello destro, quindi scegliere il linguaggio di notebook hello (noto anche come kernel).   

> [!NOTE]
> Attualmente è supportato Python 2.7, Python 3.5 e R. kernel hello R supporta la programmazione in R Open source nonché a enterprise hello scalabile Microsoft R Server.   
> 
> 

Una volta nel blocco note hello è possibile esplorare i dati, compilare il modello di hello, hello modello con le librerie di test.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Compilare modelli usando R o Python e renderli operativi con Azure Machine Learning
Dopo aver compilato e convalidato il passaggio successivo hello di modello è in genere toodeploy in produzione. In questo modo, il client stime modello hello tooinvoke di applicazioni in un tempo reale o in base a una modalità batch. Azure Machine Learning fornisce un meccanismo toooperationalize un modello compilato in R o Python.

Quando si rende operativo il modello in Azure Machine Learning, viene esposto un servizio web che consente ai client le chiamate REST toomake che passano nei parametri di input e di ricezione stime dal modello hello come output.   

> [!NOTE]
> Se non è ancora iscritti per Azure Machine Learning, è possibile ottenere un'area di lavoro gratuita o un'area di lavoro standard visitando hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page e facendo clic su "Introduzione".   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Compilare e rendere operativi i modelli Python
Di seguito è riportato un frammento di codice sviluppato in un server Jupyter Notebook di Python che consente di creare un modello semplice utilizzando hello informazioni SciKit libreria.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

metodo Hello utilizzato toodeploy il tooAzure modelli python Machine Learning esegue il wrapping hello stima del modello di hello in una funzione e decora con gli attributi forniti dalla libreria python di Azure Machine Learning pre-installata hello che identificano il computer di Azure ID area di lavoro di apprendimento e la chiave API hello di input e restituire i parametri.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Un client possa ora effettuare chiamate toohello web service. Sono disponibili wrapper praticità per costruire le richieste API REST di hello. Di seguito è un servizio web di hello tooconsume di codice di esempio.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> libreria di Azure Machine Learning Hello è supportata solo su Python 2.7 attualmente.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Compilare e rendere operativi i modelli R
È possibile distribuire i modelli di R compilati nel hello macchina virtuale di analisi scientifica dei dati o in un' posizione in Azure Machine Learning in modo simile toohow che completamento per Python. Sua hello passaggi:

* creare un tooprovide file Settings l'ID area di lavoro e l'autenticazione del token come illustrato nel seguente esempio di codice hello.
* scrivere un wrapper per il modello di hello predict-funzione.
* chiamare ```publishWebService``` in Azure Machine Learning libreria toopass wrapper funzione hello hello.  

Di seguito è hello procedure e frammenti di codice che possono essere utilizzato tooset up, compilare, pubblicare e utilizzare un modello come un servizio web in Azure Machine Learning.

#### <a name="setup"></a>Configurazione
1. Installare il pacchetto di Machine Learning R hello digitando ```install.packages("AzureML")``` Revolution R Enterprise 8.0 IDE o l'IDE di R.
2. Scaricare RTools da [qui](https://cran.r-project.org/bin/windows/Rtools/). È necessario hello zip utilità percorso hello (e denominato zip.exe) toooperationalize il pacchetto R in Machine Learning.
3. Creare un file Settings in una directory denominata ```.azureml``` nella directory principale e immettere i parametri di hello dall'area di lavoro di Azure Machine Learning:

Struttura del file settings.json:

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Compilare un modello in R e pubblicarlo in Azure Machine Learning
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Utilizzare il modello di hello distribuito in Azure Machine Learning
modello di hello tooconsume da un'applicazione client, utilizziamo hello Azure Machine Learning libreria toolook backup hello servizio web pubblicato per nome utilizzando hello `services` endpoint hello toodetermine chiamata dell'API. È sufficiente chiamare hello `consume` funzione e passare hello toobe di frame di dati previsto.
Hello seguente di codice è il modello di hello tooconsume utilizzati pubblicato come servizio web di Azure Machine Learning.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Sono disponibili ulteriori informazioni sulla libreria di Azure Machine Learning R hello [qui](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Amministrare le risorse di Azure usando il portale di Azure o PowerShell
Hello DSVM consente non solo toobuild soluzione analitica localmente sul hello macchina virtuale, ma consente anche tooaccess servizi nel cloud di Microsoft Azure. Azure offre diversi servizi di calcolo, archiviazione e analisi dei dati e altri servizi amministrabili e accessibili da DSVM.

tooadminister le risorse di sottoscrizione e nel cloud Azure è possibile utilizzare il browser e il punto toothe [portale di Azure](https://portal.azure.com). Sottoscrizione di Azure e alle risorse tramite uno script, è possibile utilizzare anche tooadminister Azure Powershell.
È possibile eseguire Azure Powershell da un collegamento sul desktop hello o da hello menu intitolato "Microsoft Azure Powershell" di avvio. Per altre informazioni su come amministrare le risorse e la sottoscrizione di Azure con gli script di Windows PowerShell, vedere la [documentazione di Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) .

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Estendere lo spazio di archiviazione con un file system condiviso
Gli esperti di dati possono condividere i set di dati di grandi dimensioni, codice o altre risorse all'interno del team di hello. Hello DSVM stesso è di circa 70GB di spazio disponibile. tooextend lo spazio di archiviazione, è possibile utilizzare hello servizio File di Azure e montarlo in hello DSVM o accedervi tramite un'API REST.   

> [!NOTE]
> lo spazio massimo di Hello della condivisione File servizio hello è 5TB e il limite di dimensioni di singoli file è di 1TB.   
> 
> 

È possibile usare Azure Powershell toocreate una condivisione di File di servizio. Di seguito è toorun script hello in Azure PowerShell toocreate una condivisione di File di Azure del servizio.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


A questo punto, dopo avere creato una condivisione file di Azure, è possibile installarla in una macchina virtuale in Azure. È consigliabile che hello VM è nella stessa data center di Azure come latenza tooavoid account di archiviazione hello e dati gli addebiti di trasferimento. Di seguito sono unità di hello comandi toomount hello in hello DSVM che è possibile eseguire in Azure Powershell.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


È ora possibile accedere questa unità come si farebbe per qualsiasi unità normale su hello VM.

## <a name="6-share-code-with-your-team-using-github"></a>6. Condividere il codice con il team usando GitHub
GitHub è un repository di codice in cui è possibile trovare una notevole quantità di codice di esempio e origini per diversi strumenti con varie tecnologie condivise da una community di sviluppatori hello. Git viene utilizzato come hello versioni tootrack e l'archivio della tecnologia dei file di codice hello. GitHub è inoltre una piattaforma in cui è possibile creare la propria toostore repository codice condiviso e la documentazione, il team implementa il controllo delle versioni e controllo che dispongono dell'accesso tooview e fornire codice. Visitare hello [pagine della Guida di GitHub](https://help.github.com/) per ulteriori informazioni sull'uso di Git. È possibile utilizzare GitHub come uno dei hello modi toocollaborate con il team, usare il codice sviluppato dalla community di hello e collaborazione della community toohello indietro di codice.

Hello DSVM include già caricato con gli strumenti client sia come ben GUI tooaccess repository GitHub della riga di comando. Hello strumento da riga di comando toowork con Git e GitHub viene chiamato Git Bash. Visual Studio installata sul hello DSVM dispone di estensioni di Git hello. È possibile trovare le icone di avvio per questi strumenti nel menu start hello e sul desktop hello.

codice toodownload da un repository GitHub utilizzare hello ```git clone``` comando. Ad esempio repository di toodownload analisi scientifica dei dati pubblicati da Microsoft nella directory corrente hello è possibile eseguire hello comando seguente, una volta nel ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

In Visual Studio, è possibile effettuare hello stessa operazione di clonazione. Hello cattura di schermata seguente mostra come tooaccess Git e GitHub degli strumenti in Visual Studio.

![Git in Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

È possibile trovare ulteriori informazioni sull'uso di Git toowork con il repository GitHub da diverse risorse disponibili in github.com. Hello [foglio informativo](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) è un utile riferimento.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Accedere a diversi servizi dati e analisi di Azure
### <a name="azure-blob"></a>BLOB Azure
BLOB di Azure è una risorsa di archiviazione cloud conveniente e affidabile per piccole e grandi quantità di dati. Esaminiamo come è possibile spostare tooAzure dati Blob e accedere ai dati archiviati in un Blob di Azure.

**Prerequisito**

* **Creare l'account di archiviazione BLOB di Azure nel [portale di Azure](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Verificare che hello pre-installato da riga di comando strumento AzCopy si trova in corrispondenza ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. È possibile aggiungere hello directory contenitore hello azcopy.exe tooyour ambiente tooavoid variabile digitando hello comando completo percorso quando si esegue questo strumento. Per ulteriori informazioni sullo strumento AzCopy, vedere troppo[documentazione AzCopy](../storage/common/storage-use-azcopy.md)
* Avviare lo strumento di hello Azure Storage Explorer. È possibile scaricarlo da [Esplora archivi di Microsoft Azure](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Spostare i dati da una macchina virtuale tooAzure Blob: AzCopy**

toomove dati tra i file locali e l'archiviazione blob, è possibile usare AzCopy nella riga di comando o PowerShell:

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Sostituire **C:\myfolder** toohello percorso in cui è archiviato il file, **mystorageaccount** nome account di archiviazione blob di tooyour, **mycontainer** il nome del contenitore toohello **chiave account di archiviazione** chiave di accesso di archiviazione blob tooyour. È possibile trovare le credenziali dell'account di archiviazione nel [portale di Azure](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

Eseguire il comando AzCopy in PowerShell o al prompt dei comandi. Ecco un esempio di utilizzo del comando AzCopy:

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Dopo aver eseguito la tooan toocopy di AzCopy comando è visualizzato il file del blob di Azure viene visualizzato in Esplora archivi Azure a breve.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Spostare i dati da una macchina virtuale tooAzure Blob: Azure Storage Explorer**

È inoltre possibile caricare i dati da file locale hello nella macchina virtuale tramite Esplora archivi Azure:

* contenitore di tooa dati tooupload, hello contenitore e fare clic su di destinazione selezionare hello **caricare** pulsante.![ Carica in Esplora archivi](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Fare clic su hello **...**  toohello diritto di hello **file** , selezionare uno o più tooupload file dal file system di hello e fare clic su **caricare** toobegin caricamento file hello.![ Caricare file tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Leggere i dati dal BLOB di Azure: modulo Reader di Machine Learning**

In Azure Machine Learning Studio è possibile utilizzare un **modulo Importa dati** dati tooread il blob.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Leggere i dati dal BLOB di Azure: ODBC Python**

È possibile utilizzare **BlobService** dati tooread libreria direttamente dal blob in un programma server Jupyter Notebook o Python.

Prima di tutto importare i pacchetti necessari:

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

Quindi collegare le credenziali dell'account BLOB di Azure e leggere i dati dal BLOB:

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

sono possibile leggerlo dati Hello come frame di dati:

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
Un Archivio Azure Data Lake è un repository con iperscalabilità per i carichi di lavoro di analisi dei Big Data compatibile con Hadoop Distributed File System (HDFS). Funziona con l'ecosistema di Hadoop hello sia hello Azure Data Lake Analitica. Ecco come è possibile spostare i dati in archivio Azure Data Lake hello ed eseguire analitica usando Azure Data Lake Analitica.

**Prerequisito**

* Creare Azure Data Lake Analytics nel [portale di Azure](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Hello **Azure Data Lake Tools** in **Visual Studio** trovare questo [collegamento](https://www.microsoft.com/download/details.aspx?id=49504) è già installato in Visual Studio Community Edition che si trova su una macchina virtuale hello hello. Dopo aver avviato Visual Studio e registrazione nella sottoscrizione di Azure, si dovrebbe essere l'account di Azure dati Analitica e l'archiviazione nel riquadro sinistro di hello di Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Spostare i dati da una macchina virtuale tooData Lake: esplorazione di Azure Data Lake**

È possibile utilizzare **Azure Data Lake Explorer** dati tooupload da file locali di hello nell'archiviazione Lake tooData macchina virtuale.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

È anche possibile compilare un tooproductionize pipeline di dati del tooor lo spostamento dei dati da Azure Data Lake tramite hello [Azure dati Factory(ADF)](https://azure.microsoft.com/services/data-factory/). Vedere toothis [articolo](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide è tra i dati di hello passaggi toobuild hello pipeline.

**Leggere i dati da Azure Blob tooData Lake: U-SQL**

Se i dati si trovano nell'archivio BLOB di Azure, è possibile leggerli direttamente dal BLOB di archiviazione di Azure nella query U-SQL. Prima di composizione di query U-SQL, assicurarsi che l'account di archiviazione blob è tooyour collegato Azure Data Lake. Andare troppo**portale di Azure**, trovare il dashboard di Azure Data Lake Analitica, fare clic su **Aggiungi origine dati**, selezionare il tipo di archiviazione troppo**di archiviazione di Azure** e plug-in di archiviazione di Azure Nome dell'account e la chiave. Si è tooreference in grado di dati di hello archiviati nell'account di archiviazione hello.

![Immettere l'account di archiviazione e la chiave](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

In Visual Studio, è possibile leggere i dati dall'archiviazione blob, eseguire alcune manipolazione dei dati, progettazione di funzionalità e output hello risultante data tooeither Azure Data Lake o archiviazione Blob di Azure. Quando si fa riferimento a dati hello nell'archiviazione blob, utilizzare **wasb: / /**; quando si fa riferimento a dati hello in Azure Data Lake, utilizzare **swbhdfs: / /**

![Frame di dati](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

È possibile utilizzare hello seguente query U-SQL in Visual Studio:

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



Dopo che la query è inviata toohello server, viene visualizzato un diagramma che illustra lo stato di hello del processo.

![Diagramma dello stato del processo](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Effettuare una query dei dati in Data Lake: U-SQL**

Set di dati hello vengono acquisiti in Azure Data Lake, è possibile utilizzare [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery ed esplorare i dati di hello. Linguaggio U-SQL è simile tooT-SQL, ma combina alcune funzionalità di c# in modo che gli utenti possono scrivere moduli personalizzati e funzioni definite dall'utente e così via. È possibile utilizzare script hello nel passaggio precedente hello.

Dopo aver inviato tooserver, tripdata_summary query hello. CSV sono reperibili poco **Azure Data Lake Explorer**, è possibile visualizzare l'anteprima dati hello dal file hello pulsante destro del mouse.

![File in Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

informazioni sui file di hello toosee:

![Riepilogo del file](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Cluster Hadoop di HDInsight
Azure HDInsight è un servizio gestito di Apache Hadoop, Spark, HBase e Storm nel cloud hello. È possibile utilizzare facilmente con i cluster HDInsight di Azure dalla macchina virtuale di analisi scientifica dei dati hello.

**Prerequisito**

* Creare l'account di archiviazione BLOB di Azure nel [portale di Azure](https://portal.azure.com). Questo account di archiviazione è dati toostore utilizzato per i cluster HDInsight.

![Creare un account di archiviazione BLOB di Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Personalizzare i cluster Hadoop di Azure HDInsight nel [portale di Azure](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * È necessario collegare l'account di archiviazione hello creato con il cluster HDInsight quando viene creato. Questo account di archiviazione viene utilizzato per accedere ai dati che possono essere elaborati all'interno di cluster hello.

![Collegamento toostorage account creato con il cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* È necessario abilitare **accesso remoto** toohello nodo head del cluster di hello dopo averlo creato. Memorizza le credenziali di accesso remoto hello è possibile specificare (diverse da quelle specificate per il cluster hello al momento della relativa creazione): non è presente la procedura successiva hello.

![Abilitare l'accesso remoto](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Creare un'area di lavoro di Azure Machine Learning. Gli esperimenti di Machine Learning vengono archiviati in questa area di lavoro di Machine Learning. Selezionare opzioni di hello evidenziato nel portale, come illustrato nella seguente schermata hello:

![Creare un'area di lavoro di Machine Learning di Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Quindi immettere i parametri di hello per l'area di lavoro

![Immettere i parametri dell'area di lavoro di Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Caricare i dati con IPython Notebook. È innanzitutto necessario importare pacchetti richiesti, inserire le credenziali, creare un database nell'account di archiviazione, quindi caricare cluster tooHDI di dati.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* In alternativa, è possibile seguire questo [procedura dettagliata](machine-learning-data-science-process-hive-walkthrough.md) tooupload cluster tooHDI di NYC Taxi dati. I passaggi più importanti includono:
  
  * AzCopy: download compresso CSV dalla cartella locale di blob pubblici tooyour
  * AzCopy: caricare decompresso CSV dal cluster tooHDI cartella locale
  * Accedere al nodo head di hello del cluster Hadoop e la preparazione per l'analisi esplorativa dei dati

Dopo aver caricato tooHDI cluster dati hello, è possibile controllare i dati in Azure Storage Explorer. Nel cluster HDI è stato creato un database nyctaxidb.

**Esplorazione dei dati: query Hive in Python**

Poiché i dati di hello sono in cluster Hadoop, è possibile utilizzare hello pyodbc pacchetto tooconnect tooHadoop cluster e database di query utilizzando Progettazione di funzionalità e l'esplorazione toodo Hive. È possibile visualizzare le tabelle esistenti di hello che è creati nel passaggio dei prerequisiti di hello.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Visualizzare tabelle esistenti](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Esaminiamo il numero di hello di record in ogni mese e hello le frequenze di inclinato o non presente nella tabella di andata e ritorno hello:

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Tracciato del numero di record in ogni mese](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Tracciato della frequenze delle mance](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

È possibile anche calcolare distanza hello tra il percorso di prelievo e dropoff e confrontare quindi toohello attivarsi distanza.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Tabella di punti di partenza e punti di arrivo](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Tracciato di distanza tootrip prelievo/dropoff distanza](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

Verrà ora preparato un set di dati sottocampionati (1%) per la modellazione. È possibile usare questi dati nel modulo Reader di Machine Learning.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

Dopo un periodo di tempo, è possibile visualizzare dati hello sono stati caricati nel cluster Hadoop:

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Tabella di dati](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Leggere i dati da HDI con il modulo Reader di Machine Learning**

È inoltre possibile utilizzare hello **lettore** modulo di Machine Learning Studio tooaccess hello database in un cluster Hadoop. Collegare le credenziali di hello dei cluster HDI e Account di archiviazione Azure tooenable compilazione sta eseguendo un'operazione di machine learning i modelli di utilizzo di database in cluster HDI.

![Proprietà del modulo Reader](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Hello set di dati con punteggio possono quindi essere visualizzati:

![Visualizzare il set di dati con i punteggi](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL Data Warehouse e database
Azure SQL Data Warehouse è un data warehouse elastico distribuito come servizio con l'esperienza di classe enterprise di SQL Server.

È possibile eseguire il provisioning di Azure SQL Data Warehouse seguendo le istruzioni di hello fornite in questo [articolo](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Una volta che viene effettuato il provisioning di Azure SQL Data Warehouse, è possibile utilizzare questo [procedura dettagliata](machine-learning-data-science-process-sqldw-walkthrough.md) di caricamento dei dati toodo, esplorazione e modellazione utilizzando i dati all'interno di hello SQL Data Warehouse.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
DB Cosmos Azure è un database NoSQL nel cloud hello. Consente si toowork con i documenti come JSON e consente toostore ed eseguire query sui documenti hello.

È necessario hello toodo seguenti per ogni ora passaggi tooaccess Azure Cosmos DB dagli hello DSVM.

1. Installare l'SDK DocumentDB Python eseguendo ```pip install pydocumentdb``` al prompt dei comandi
2. Creare l'account e il database Azure Cosmos DB nel [portale di Azure](https://portal.azure.com)
3. Scaricare "Strumento di migrazione DB Cosmos di Azure" da [qui](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) ed estrarre tooa directory scelta
4. Importare i dati JSON (dati volcano) archiviati in un [blob pubblici](https://cahandson.blob.core.windows.net/samples/volcano.json) in DB Cosmos con seguente comando parametri toohello strumento di migrazione (dtui.exe dalla directory hello in cui è installato lo strumento di migrazione DB Cosmos hello). Immettere percorso di origine e destinazione hello con i seguenti parametri:
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

Quando si importano dati hello, è possibile passare tooJupyter e blocco note aprire hello intitolata *DocumentDBSample* che contiene python codice tooaccess DocumentDB ed eseguire alcune query di base. Maggiori informazioni su DB Cosmos visitando servizio hello [pagina della documentazione](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Creare report e dashboard tramite Power BI Desktop hello
Segnalare il problema, visualizzare i file JSON Volcano hello che è stato illustrato nell'esempio sopra riportato DB Cosmos in Power BI toogain visual approfondite dati hello hello. I passaggi dettagliati sono disponibili in hello [articolo Power BI](../cosmos-db/powerbi-visualize.md). Ecco i passaggi di alto livello hello:

1. Aprire Power BI Desktop ed eseguire "Recupera dati". Specificare l'URL come hello: https://cahandson.blob.core.windows.net/samples/volcano.json
2. Dovrebbe essere importato come un elenco di record di hello JSON
3. Convertire tabella tooa di hello elenco in modo che Power BI può lavorare con hello stesso
4. Espandere le colonne di hello facendo clic su hello espandono l'icona (Buongiorno uno con l'icona di "freccia sinistra e una freccia a destra" hello in hello destra della colonna hello)
5. La posizione è un campo "Record". Espandere i record di hello e selezionare solo le coordinate di hello. La coordinata è una colonna elenco.
6. Aggiungere una nuova colonna tooconvert hello elenco coordinate colonna in una colonna di LatLong separata da virgole concatenazione elementi hello due nel campo elenco coordinate hello utilizzando la formula hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Convertire infine hello ```Elevation``` tooDecimal di colonna e seleziona hello **Chiudi** e **applica**.

Anziché passaggi precedenti, è possibile incollare hello seguente di codice che consente di generare script hello passaggi utilizzati in hello Editor avanzato in Power BI che consente le trasformazioni dei dati hello toowrite in un linguaggio di query.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Dati hello è ora disponibile nel modello di dati di Power BI. Power BI Desktop deve avere ora un aspetto simile al seguente:

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

È possibile avviare la creazione di report e visualizzazioni con modello di dati hello. È possibile seguire i passaggi di hello in questo [articolo Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild un report. risultato finale Hello è un report simile al seguente hello.

![Visualizzazione report di Power BI Desktop - Connettore Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Applicare la scalabilità dinamicamente il toomeet DSVM che richiesto dal progetto
È possibile scalarle toomeet DSVM hello che richiesto dal progetto. Se non è necessario toouse hello VM sera hello o nei fine settimana, è possibile semplicemente arrestare hello VM da hello [portale di Azure](https://portal.azure.com).

> [!NOTE]
> Essere addebitati anche se si utilizza solo pulsante di arresto del sistema operativo hello in hello macchina virtuale.  
> 
> 

Se è necessario toohandle analisi su larga scala e necessario aumentare la capacità della CPU, memoria o disco sono disponibili diverse dimensioni delle macchine Virtuali in termini di core CPU, memoria e tipi di disco (incluse le unità SSD) che soddisfano le esigenze bilancio e il calcolo. Hello elenco completo delle macchine virtuali con il piano tariffario calcolo oraria è disponibile in hello [prezzi delle macchine virtuali di Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) pagina.

Analogamente, se si riduce la necessità di capacità di elaborazione di macchina virtuale (ad esempio: è stato spostato tooa un carico di lavoro principali Hadoop o in un cluster Spark), è possibile scalare verso il basso cluster hello da hello [portale di Azure](https://portal.azure.com) e in uscita toohello impostazioni della macchina virtuale istanza. Ecco uno screenshot.

![Impostazioni dell'istanza della VM](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Installare strumenti aggiuntivi nella macchina virtuale
È stato incluso nel pacchetto di diversi strumenti che si ritiene che sono in grado di tooaddress numerose esigenze di analitica dei dati comuni hello e che deve risparmiare tempo evitando con tooinstall e configurare gli ambienti uno alla volta e risparmiare denaro pagando solo per le risorse utilizzare.

È possibile usare altri dati di Azure e servizi analitica profilato in questo articolo di tooenhance ambiente analitica. È possibile che in alcuni casi siano necessari strumenti aggiuntivi, inclusi alcuni strumenti proprietari di terze parti. Disporre dell'accesso amministrativo completo in hello macchina virtuale tooinstall nuovi strumenti che necessari. È anche possibile installare pacchetti aggiuntivi in Python e in R non preinstallati. Per Python è possibile usare ```conda``` o ```pip```. R è possibile utilizzare hello ```install.packages()``` in hello R console oppure utilizzare hello IDE e scegliere "**pacchetti** -> **pacchetti di installazione...** ".

## <a name="summary"></a>Riepilogo
Questi sono solo alcune delle operazioni di hello che è possibile eseguire nella macchina virtuale di Microsoft Data Science hello. Sono disponibili molte altre operazioni che è possibile eseguire toomake è un ambiente analitica effettivo.

