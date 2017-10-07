---
title: set di dati aaaAccess alla libreria client Python di Machine Learning | Documenti Microsoft
description: Installare e utilizzare hello tooaccess libreria client di Python e gestire i dati di Azure Machine Learning in modo sicuro da un ambiente locale in Python.
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Set di dati di accesso con Python mediante una libreria client di Azure Machine Learning Python hello
Anteprima Hello della libreria client Python di Microsoft Azure Machine Learning consente l'accesso sicuro tooyour Azure Machine Learning i set di dati da un ambiente di Python locale e consente la creazione di hello e gestione di set di dati in un'area di lavoro.

Questo argomento fornisce istruzioni su come:

* installare una libreria client di Machine Learning Python hello 
* accedere e caricare i set di dati, incluse le istruzioni su come tooget autorizzazione tooaccess set di dati di Azure Machine Learning dall'ambiente locale di Python
* Accedere ai set di dati intermedi di un esperimento
* Utilizzare i set di dati di hello Python client libreria tooenumerate, accedere ai metadati, leggere il contenuto di hello di un set di dati, creare nuovi set di dati e aggiornare i set di dati esistente

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Prerequisiti
libreria client Python di Hello è stata testata in hello seguenti ambienti:

* Windows, Mac e Linux
* Python 2.7, 3.3 e 3.4

E presenta una dipendenza su hello pacchetti seguenti:

* requests
* python-dateutil
* pandas

Si consiglia di utilizzare, ad esempio una distribuzione di Python [Anaconda](http://continuum.io/downloads#all) o [Canopy](https://store.enthought.com/downloads/), che vengono forniti con Python, IPython e installare i pacchetti hello tre elencati in precedenza. Sebbene IPython non sia obbligatorio, costituisce un ambiente ottimale per la manipolazione e la visualizzazione dei dati in modo interattivo.

### <a name="installation"></a>Come tooinstall hello libreria client Python di Azure Machine Learning
libreria client di Azure Machine Learning Python Hello debba essere installati toocomplete hello attività descritte in questo argomento. È disponibile da hello [indice del pacchetto Python](https://pypi.python.org/pypi/azureml). tooinstall Python nell'ambiente in uso, eseguirlo hello il seguente comando da ambiente locale Python:

    pip install azureml

In alternativa, è possibile scaricare e installare da origini hello in [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Se si dispone di git installati nel computer, è possibile utilizzare tooinstall pip direttamente dal repository git hello:

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Utilizzano i DataSet tooaccess frammenti di codice Studio
libreria client Python di Hello permette l'accesso programmatico tooyour set di dati esistenti da esperimenti che sono stati eseguiti.

Dall'interfaccia web di hello Studio, è possibile generare frammenti di codice che includono tutti i toodownload le informazioni necessarie hello e deserializzare i set di dati come oggetti Pandas frame di dati nel computer di percorso.

### <a name="security"></a>Sicurezza per l'accesso ai dati
frammenti di codice forniti da Studio per utilizzare alla libreria client Python di hello include l'id area di lavoro e l'autorizzazione di Hello token. Questi forniscono l'area di lavoro tooyour accesso completo e deve essere protetto, ad esempio una password.

Per motivi di sicurezza, la funzionalità dei frammenti di codice hello è solo toousers disponibile con il proprio ruolo impostato come **proprietario** per area di lavoro hello. Il ruolo verrà visualizzato in Azure Machine Learning Studio hello **utenti** pagina **impostazioni**.

![Sicurezza][security]

Se il ruolo non è impostato come **proprietario**, è possibile richiedere toobe invito come proprietario, o richiedere al proprietario di hello dell'area di lavoro tooprovide hello è con il frammento di codice hello.

token di autorizzazione hello tooobtain, è possibile eseguire una delle seguenti hello:

* Chiedere un token a un proprietario. I proprietari possono accedere i token di autorizzazione dalla pagina di impostazioni di hello della propria area di lavoro di Studio. Selezionare **impostazioni** dal riquadro e fare clic a sinistra hello **token di autorizzazione** toosee hello token primario e secondario.  Sebbene hello primario o i token di autorizzazione secondario hello possono essere utilizzati nel frammento di codice hello, è consigliabile che i proprietari condividano solo i token di autorizzazione secondario hello.

![Token di autorizzazione](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Chiedere toorole toobe alzate di livello del proprietario.  toodo questa operazione, un proprietario corrente di hello dell'area di lavoro esigenze toofirst è rimuovere dall'area di lavoro hello quindi nuovamente invito tooit come proprietario.

Dopo aver ottenuto gli sviluppatori id area di lavoro hello e l'autorizzazione token, sono in grado di tooaccess area di lavoro hello tramite il frammento di codice hello indipendentemente dal loro ruolo.

Token di autorizzazione vengono gestiti nel hello **token di autorizzazione** pagina **impostazioni**. Può essere rigenerato, ma questa procedura revoca token di accesso toohello precedente.

### <a name="accessingDatasets"></a>Accedere a set di dati da un'applicazione Python locale
1. In Machine Learning Studio, fare clic su **set di dati** hello sinistra sulla barra di navigazione hello.
2. Selezionare hello set di dati tooaccess. È possibile selezionare uno dei set di dati hello hello **set di dati personali** elenco o da hello **esempi** elenco.
3. Dalla barra degli strumenti nella parte inferiore di hello, fare clic su **genera codice di accesso ai dati**. Se i dati di hello in un formato incompatibile con una libreria client Python di hello, questo pulsante è disabilitato.
   
    ![DATASETS][datasets]
4. Selezionare il frammento di codice hello dalla finestra hello che viene visualizzata e copiarlo negli Appunti tooyour.
   
    ![Codice di accesso][dataset-access-code]
5. Incollare il codice hello notebook hello di applicazione Python locale.
   
    ![Blocco appunti][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Accedere a set di dati intermedi da esperimenti di Machine Learning
Dopo l'esecuzione di un esperimento in hello Machine Learning Studio, è possibile tooaccess hello intermedia set di dati di nodi di output di hello dei moduli. I set di dati intermedi sono costituiti da dati creati e usati per i passaggi intermedi quando è in esecuzione uno strumento di modello.

Set di dati intermedi sono accessibili, purché il formato di dati hello è compatibile con libreria client Python di hello.

Hello sono supportati i seguenti formati (costanti per questi sono hello `azureml.DataTypeIds` classe):

* PlainText
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

È possibile determinare formato hello al passaggio del mouse su un nodo di output del modulo. Viene visualizzato insieme al nome nodo hello, in una descrizione comando.

Alcuni dei moduli di hello, ad esempio hello [Split] [ split] modulo, denominato formato di output tooa `Dataset`, che non è supportato dalla libreria client Python di hello.

![Formato del set di dati][dataset-format]

È necessario toouse un modulo di conversione, ad esempio [convertire tooCSV][convert-to-csv], tooget un output in un formato supportato.

![Formato GenericCSV][csv-format]

Hello passaggi seguenti viene illustrato un esempio che crea un esperimento, eseguirlo e accede a set di dati intermedi hello.

1. Creare un nuovo esperimento.
2. Inserire un modulo **Adult Census Income Binary Classification dataset** .
3. Inserire un [Split] [ split] modulo e connettere l'output di modulo di input toohello set di dati.
4. Inserire un [convertire tooCSV] [ convert-to-csv] modulo e il relativo input tooone di hello connettersi [Split] [ split] modulo restituisce.
5. Salvare l'esperimento hello, eseguirlo e attendere che toofinish in esecuzione.
6. Fare clic sul nodo di output di hello in hello [convertire tooCSV] [ convert-to-csv] modulo.
7. Quando viene visualizzato il menu di scelta rapida hello, selezionare **genera codice di accesso ai dati**.
   
    ![Menu di scelta rapida][experiment]
8. Selezionare il frammento di codice hello e copiarlo negli Appunti tooyour dalla finestra hello che viene visualizzata.
   
    ![Codice di accesso][intermediate-dataset-access-code]
9. Incollare il codice hello nel blocco note.
   
    ![Blocco appunti][ipython-intermediate-dataset]
10. È possibile visualizzare i dati di hello usando matplotlib. Verrà visualizzata in un istogramma per la colonna age hello:
    
    ![Istogramma][ipython-histogram]

## <a name="clientApis"></a>Utilizzare tooaccess libreria client Python di Machine Learning di hello, leggere, creare e gestire set di dati
### <a name="workspace"></a>Area di lavoro
area di lavoro di Hello è il punto di ingresso hello per la libreria client Python di hello. Fornire hello `Workspace` classe con l'area di lavoro id e l'autorizzazione toocreate di token a un'istanza:

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Enumerare set di dati
tooenumerate tutti i set di dati di una determinata area di lavoro:

    for ds in ws.datasets:
        print(ds.name)

tooenumerate hello appena creati dall'utente i set di dati:

    for ds in ws.user_datasets:
        print(ds.name)

tooenumerate set di dati per l'esempio hello solo:

    for ds in ws.example_datasets:
        print(ds.name)

È possibile accedere a un set di dati per nome (si applica la distinzione maiuscole/minuscole):

    ds = ws.datasets['my dataset name']

In alternativa, è possibile accedere tramite indice:

    ds = ws.datasets[0]


### <a name="metadata"></a>Metadata
Set di dati dispongono di metadati, in aggiunta toocontent. (Set di dati intermedi sono una regola di eccezione toothis e non dispone di tutti i metadati).

Alcuni valori dei metadati vengono assegnati dall'utente hello in fase di creazione:

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

Altri valori vengono assegnati da Azure Machine Learning:

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Vedere hello `SourceDataset` classe per altre su hello disponibili i metadati.

### <a name="read-contents"></a>Leggere il contenuto
frammenti di codice Hello forniti automaticamente da Machine Learning Studio scaricano e deserializzare l'oggetto di hello dataset tooa Pandas frame di dati. Questa operazione viene eseguita con hello `to_dataframe` metodo:

    frame = ds.to_dataframe()

Se si preferiscono dati non elaborati di toodownload hello ed esegue manualmente la deserializzazione di hello, che è un'opzione. In un momento hello, questa è hello unica opzione per i formati, ad esempio 'ARFF', non è possibile deserializzare la libreria client Python di hello.

contenuto di hello tooread come testo:

    text_data = ds.read_as_text()

contenuto di hello tooread in formato binario:

    binary_data = ds.read_as_binary()

È possibile anche aprire un contenuto di flusso toohello:

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Creare un nuovo set di dati
libreria client Python di Hello consente tooupload i set di dati dal programma Python. per poterli usare nell'area di lavoro.

Se i dati si trovano in un frame di dati Pandas, utilizzare hello seguente codice:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Se invece i dati sono già serializzati, è possibile usare:

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

libreria client Python Hello è in grado di tooserialize Pandas DataFrame toohello seguito formati (costanti per questi sono hello `azureml.DataTypeIds` classe):

* PlainText
* GenericCSV
* GenericTSV
* GenericCSVNoHeader
* GenericTSVNoHeader

### <a name="update-an-existing-dataset"></a>Aggiornare un set di dati esistente
Se si tenta di tooupload un nuovo set di dati con un nome che corrisponde a un set di dati esistente, è necessario ottenere un errore di conflitto.

tooupdate un set di dati esistente, è innanzitutto necessario tooget un dataset esistente toohello di riferimento:

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Utilizzare quindi `update_from_dataframe` tooserialize e sostituire contenuto hello del set di dati di hello in Azure:

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Se si desidera tooserialize hello dati tooa altro formato, specificare un valore per hello facoltativo `data_type_id` parametro.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Facoltativamente, è possibile impostare una nuova descrizione specificando un valore per hello `description` parametro.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

Facoltativamente, è possibile impostare un nuovo nome, specificando un valore per hello `name` parametro. In futuro, si recupererà hello dataset utilizzando hello solo nuovo nome. Hello seguente codice Aggiorna dati hello, descrizione e nome.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Hello `data_type_id`, `name` e `description` i parametri sono facoltativi e il valore precedente tootheir predefinito. Hello `dataframe` parametro è sempre obbligatorio.

Se i dati sono già serializzati, usare `update_from_raw_data` anziché `update_from_dataframe`. Il funzionamento è analogo: è sufficiente passare `raw_data` invece di `dataframe`.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

