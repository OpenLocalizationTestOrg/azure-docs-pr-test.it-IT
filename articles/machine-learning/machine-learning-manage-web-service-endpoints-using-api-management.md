---
title: aaaLearn come toomanage Azure ml web services tramite Gestione API | Documenti Microsoft
description: Una Guida che illustra come toomanage Azure ml web services tramite Gestione API.
keywords: apprendimento automatico, gestione api
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Informazioni su come toomanage Azure ml web services tramite Gestione API
## <a name="overview"></a>Panoramica
Questa guida illustra come tooquickly informazioni introduttive sull'utilizzo di servizi web di Azure ml toomanage gestione API.

## <a name="what-is-azure-api-management"></a>Cos'è Gestione API di Azure?
Gestione API di Azure è un servizio di Azure che consente di gestire gli endpoint dell'API REST definendo l'accesso utente, la limitazione all'utilizzo e il monitoraggio del dashboard. Per informazioni dettagliate su Gestione API di Azure, fare clic [qui](https://azure.microsoft.com/services/api-management/) . Fare clic su [qui](../api-management/api-management-get-started.md) per una Guida per la modalità di avvio tooget con gestione API di Azure. L'altra guida, su cui è basata questa, tratta più argomenti, tra cui le configurazioni delle notifiche, il livello di prezzo, la gestione delle risposte, l'autenticazione utente, la creazione di prodotti, le sottoscrizioni per sviluppatori e il dashboarding dell'uso.

## <a name="what-is-azureml"></a>Informazioni su AzureML
Azure ml è un servizio di Azure per l'apprendimento automatico che consente la compilazione tooeasily, distribuire e condividere soluzioni analitica avanzate. Per informazioni dettagliate su AzureML, fare clic [qui](https://azure.microsoft.com/services/machine-learning/) .

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa Guida, è necessario:

* Un account Azure. Se non si dispone di un account Azure, fare clic su [qui](https://azure.microsoft.com/pricing/free-trial/) per informazioni dettagliate su come toocreate un account di prova.
* Un account AzureML. Se non si dispone di un account di Azure ml, fare clic su [qui](https://studio.azureml.net/) per informazioni dettagliate su come toocreate un account di prova.
* area di lavoro Hello e del servizio api_key per un esperimento di Azure ml distribuito come servizio web. Fare clic su [qui](machine-learning-create-experiment.md) per informazioni dettagliate sulla modalità di sperimentare toocreate un Azure ml. Fare clic su [qui](machine-learning-publish-a-machine-learning-web-service.md) per informazioni dettagliate su come toodeploy un Azure ml esperimento come servizio web. In alternativa, nell'appendice contiene istruzioni di toocreate test un Azure ml semplice esperimento ed e distribuirla come servizio web.

## <a name="create-an-api-management-instance"></a>Creare un'istanza di Gestione API
Di seguito sono passaggi hello per l'utilizzo di gestione API toomanage il servizio web di Azure ml. Creare innanzitutto un'istanza del servizio. Accedi toohello [portale classico](https://manage.windowsazure.com/) e fare clic su **New** > **servizi App** > **gestione API**  >  **Creare**.

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Specificare un **URL**univoco. Questa Guida usa **demoazureml** – toochoose sarà necessario un valore diverso. Scegliere hello desiderato **sottoscrizione** e **area** per l'istanza del servizio. Dopo aver effettuato le selezioni, fare clic sul pulsante Avanti hello.

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Specificare un valore per hello **nome organizzazione**. Questa Guida usa **demoazureml** – toochoose sarà necessario un valore diverso. Immettere l'indirizzo di posta elettronica in hello **posta elettronica amministratore** campo. Questo indirizzo di posta elettronica viene utilizzato per notifiche da hello sistema gestione API.

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Fare clic su hello casella di controllo toocreate all'istanza del servizio. *Occupi toothirty minuti per un nuovo toobe servizio creato*.

## <a name="create-hello-api"></a>Creare API hello
Una volta creata l'istanza del servizio hello, hello sarà toocreate hello API. Un'API rappresenta un set di operazioni che possono essere richiamate da un'applicazione client. Le operazioni dell'API sono servizi web tooexisting elaborate. Questa Guida consente di creare le API che toohello proxy AzureML RRS e BES servizi web esistenti.

API create e configurate dal portale di pubblicazione di hello API, è possibile accedervi tramite hello portale classico di Azure. tooreach hello selezionare portale, server di pubblicazione all'istanza del servizio.

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Fare clic su **Gestisci** in hello portale classico di Azure per il servizio Gestione API.

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **aggiungere API**.

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Tipo **API di Azure ml Demo** come hello **nome API Web**. Tipo **https://ussouthcentral.services.azureml.net** come hello **URL servizio Web**. Tipo **demo di Azure ml** come hello **suffisso URL dell'API Web**. Controllare **HTTPS** come hello **l'URL dell'API Web** schema. Selezionare **Starter** (Avviatore) in **Prodotti**. Al termine, fare clic su **salvare** toocreate hello API.

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Aggiungere le operazioni di hello
Fare clic su **l'operazione di aggiunta** tooadd operazioni toothis API.

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Hello **nuova operazione** finestra verranno visualizzate e hello **firma** scheda verrà selezionata per impostazione predefinita.

## <a name="add-rrs-operation"></a>Aggiungere un'operazione RRS
Creare innanzitutto un'operazione per il servizio AzureML RRS hello. Selezionare **POST** come hello **verbo HTTP**. Tipo **/workspaces/ {area di lavoro} / Services / {servizio} / execute? api-version = {apiversion} & dettagli = {dettagli}** come hello **modello di URL**. Tipo **RR eseguire** come hello **nome visualizzato**.

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**. Fare clic su **salvare** toosave questa operazione.

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Aggiungere operazioni BES
Schermate non sono incluse per hello operazioni BES come se fossero toothose molto simili per l'aggiunta di operazione RR hello.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Inviare (ma non avviare) un processo di esecuzione in batch
Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API. Selezionare **POST** per hello **verbo HTTP**. Tipo **/workspaces/ {area di lavoro} / Services / {servizio} / processi? api-version = {apiversion}** per hello **modello di URL**. Tipo **inviare BES** per hello **nome visualizzato**. Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**. Fare clic su **salvare** toosave questa operazione.

### <a name="start-a-batch-execution-job"></a>Avviare un processo di esecuzione in batch
Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API. Selezionare **POST** per hello **verbo HTTP**. Tipo **/workspaces/ {area di lavoro} / Services / {servizio} /jobs/ {jobid} / avvia? api-version = {apiversion}** per hello **modello di URL**. Tipo **avviare BES** per hello **nome visualizzato**. Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**. Fare clic su **salvare** toosave questa operazione.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Ottenere lo stato di hello o il risultato di un processo di esecuzione Batch
Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API. Selezionare **ottenere** per hello **verbo HTTP**. Tipo **/workspaces/ {area di lavoro} / Services / {servizio} /jobs/ {jobid}? api-version = {apiversion}** per hello **modello di URL**. Tipo **stato BES** per hello **nome visualizzato**. Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**. Fare clic su **salvare** toosave questa operazione.

### <a name="delete-a-batch-execution-job"></a>Eliminare un processo di esecuzione in batch
Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API. Selezionare **eliminare** per hello **verbo HTTP**. Tipo **/workspaces/ {area di lavoro} / Services / {servizio} /jobs/ {jobid}? api-version = {apiversion}** per hello **modello di URL**. Tipo **eliminare BES** per hello **nome visualizzato**. Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**. Fare clic su **salvare** toosave questa operazione.

## <a name="call-an-operation-from-hello-developer-portal"></a>Chiamare un'operazione dal portale per sviluppatori hello
Operazioni possono essere chiamate direttamente dal portale per sviluppatori di hello, che fornisce un modo pratico di tooview e testare il funzionamento di hello di un'API. In questo passaggio Guida si chiamerà hello **RR eseguire** metodo che è stato aggiunto toohello **API di Azure ml Demo**. Fare clic su **portale per sviluppatori** dal menu hello hello in alto a destra di hello portale classico.

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Fare clic su **API** dal menu superiore hello e quindi fare clic su **API di Azure ml Demo** operazioni hello toosee disponibili.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Selezionare **RR eseguire** per l'operazione di hello. Fare clic su **Prova**.

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Per i parametri di richiesta, digitare il **dell'area di lavoro**, **servizio**, **2.0** per hello **apiversion**, e **true**per hello **dettagli**. È possibile trovare il **dell'area di lavoro** e **servizio** nel dashboard del servizio web di Azure ml hello (vedere **Test servizio web hello** nell'appendice).

Per le intestazioni della richiesta, fare clic su **Aggiungi intestazione**, digitare **Content-Type** e **application/json**, quindi fare clic su **Aggiungi intestazione** e digitare **Authorization** e **Bearer <YOUR AZUREML SERVICE API-KEY>**. È possibile trovare il **chiave api** nel dashboard del servizio web di Azure ml hello (vedere **Test servizio web hello** nell'appendice).

Tipo **{"Input": {"input1": {"ColumnNames": "Valori" ["Col2"]: [["questo è un buon giorno"]]}}, "Globalparameters della": {}}** per il corpo della richiesta hello.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Fare clic su **Send**.

![Send](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Dopo un'operazione viene richiamata, il portale per sviluppatori di hello Visualizza hello **URL richiesto** dal servizio back-end hello, hello **stato della risposta**, hello **le intestazioni di risposta**, e qualsiasi **contenuto della risposta**.

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Appendice A - Creazione e test di un semplice servizio Web di AzureML
### <a name="creating-hello-experiment"></a>Creazione di sperimentazione hello
Di seguito sono passaggi hello per la creazione di un semplice esperimento di Azure ml e distribuirla come servizio web. Hello web servizio accetta come input una colonna di testo arbitrario e restituisce un set di funzionalità rappresentati come numeri interi. ad esempio:

| Text | Testo con hash |
| --- | --- |
| This is a good day |1 1 2 2 0 2 0 1 |

In primo luogo, usando un browser di propria scelta, passare a: [https://studio.azureml.net/](https://studio.azureml.net/) e immettere le credenziali toolog in. Quindi creare un nuovo esperimento vuoto.

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Rinominarlo troppo**SimpleFeatureHashingExperiment**. Espandere **Saved Datasets** (Set di dati salvati) e trascinare **Book Reviews from Amazon** (Recensioni di libri da Amazon) sull'esperimento.

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Espandere **Data Transformation** (Trasformazioni di dati) e **Manipulation** (Manipolazione), quindi trascinare **Select Columns in Dataset** (Seleziona colonne in set di dati) sull'esperimento. Connettersi **recensioni da Amazon** troppo**selezionare le colonne nel set di dati**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Fare clic su **Select Columns in Dataset** (Seleziona colonne in set di dati), quindi fare clic su **Launch column selector** (Avvia selettore di colonna) e selezionare **Col2**. Fare clic su hello segno di spunta tooapply queste modifiche.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Espandere **testo Analitica** e trascinare **Feature Hashing** nella sperimentazione hello. Connettersi **selezionare le colonne nel set di dati** troppo**Feature Hashing**.

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Tipo **3** per hello **Hashing bitsize**. Verranno create 8 (23) colonne.

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

A questo punto, è opportuno tooclick **eseguire** esperimento hello tootest.

![Run](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Creare un servizio Web
Ora creare un servizio Web. Espandere **Servizio Web** e trascinare **Input** sull'esperimento. Connettersi **Input** troppo**Feature Hashing**. Trascinare anche **output** sull'esperimento. Connettersi **Output** troppo**Feature Hashing**.

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Fare cli su **Publish web service**.

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Fare clic su **Sì** esperimento hello toopublish.

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Servizio web hello di test
Un servizio Web di AzureML è costituito dagli endpoint RSS (servizio di richiesta/risposta) e BES (servizio di esecuzione batch). RSS è per l'esecuzione sincrona. BES è per l'esecuzione di processi asincrona. tootest del servizio web con origine Python hello esempio riportato di seguito, potrebbe essere necessario toodownload e hello installare Azure SDK per Python (vedere: [come tooinstall Python](../python-how-to-install.md)).

È inoltre necessario hello **dell'area di lavoro**, **servizio**, e **api_key** dell'esperimento per l'origine di esempio hello riportato di seguito. È possibile trovare l'area di lavoro hello e il servizio facendo clic su **richiesta/risposta** o **esecuzione Batch** per l'esperimento nel dashboard del servizio web hello.

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

È possibile trovare hello **api_key** facendo esperimento nel dashboard del servizio web hello.

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Testare l'endpoint RRS
##### <a name="test-button"></a>Pulsante Test
Un endpoint di record di risorse facilmente tootest hello è tooclick **Test** nel dashboard del servizio web hello.

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Digitare **This is a good day** in **col2**. Fare clic su hello segno di spunta.

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Verrà visualizzato qualcosa di simile a quanto segue

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Codice di esempio
Un altro modo tootest i record di risorse è dal codice client. Se si fa clic **richiesta/risposta** hello dashboard e scorrere toohello lato inferiore, verrà visualizzato il codice di esempio per c#, Python e R. Si verifica anche la sintassi di hello di richieste di record di risorse hello, inclusi hello richiesta URI, intestazioni e corpo.

Questa guida mostra un esempio di Python funzionante. Sarà necessario toomodify con hello **dell'area di lavoro**, **servizio**, e **api_key** dell'esperimento.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Testare l'endpoint BES
Fare clic su **esecuzione Batch** nella parte inferiore di toohello dashboard e scorrere hello. Verrà visualizzato il codice di esempio per c#, Python e R. Si verifica anche la sintassi di hello di hello BES richieste toosubmit un processo, avviare un processo, ottenere lo stato di hello o risultati di un processo ed eliminare un processo.

Questa guida mostra un esempio di Python funzionante. È necessario toomodify con hello **dell'area di lavoro**, **servizio**, e **api_key** dell'esperimento. Inoltre, è necessario hello toomodify **nome account di archiviazione**, **chiave account di archiviazione**, e **nome del contenitore di archiviazione**. Infine, sarà necessario percorso hello toomodify di hello **file di input** e il percorso di hello di hello **file di output**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
