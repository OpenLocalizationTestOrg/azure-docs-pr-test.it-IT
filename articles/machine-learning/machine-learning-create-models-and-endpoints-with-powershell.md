---
title: "aaaCreate più modelli da un esperimento | Documenti Microsoft"
description: "Utilizzare PowerShell toocreate più modelli di Machine Learning e gli endpoint di servizio con hello web stesso algoritmo, ma i set di dati di training diversi."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Creare più modelli di Machine Learning ed endpoint di servizio Web da un esperimento usando PowerShell
Di seguito è un problema comune di apprendimento macchina: si desidera toocreate molti modelli contenenti hello stesso flusso di lavoro di training e utilizzare hello stesso algoritmo, ma dispone di set di dati di training diversi come input. In questo articolo illustra come toodo questo su larga scala in Azure Machine Learning Studio usando un esperimento di singolo.

Si supponga, ad esempio, di essere proprietari di un franchising globale di noleggio di biciclette. Si desidera toobuild una richiesta di noleggio di regressione modello toopredict hello in base ai dati cronologici. Posizioni di noleggio 1.000 sono mondo hello e aver raccolto un set di dati per ogni percorso che include funzionalità importanti, ad esempio data, ora, meteo e il traffico che sono specifici tooeach percorso.

Impossibile eseguire il training del modello una volta con una versione unita di tutti i set di hello in tutte le posizioni. Ma poiché ognuno dei percorsi di un ambiente univoco, un approccio migliore potrebbe essere tootrain il modello di regressione separatamente utilizzando hello set di dati per ogni posizione. In questo modo, ogni modello con training può richiedere in dimensioni di archivio diversi account hello, volume, geography, popolamento, ambiente, finestra bike orientato al traffico *e così via*.

Che può essere l'approccio migliore hello, ma non si vuole toocreate 1.000 esperimenti di training in Azure Machine Learning con ciascuno dei quali rappresenta un percorso univoco. Oltre a essere un'attività piuttosto complessa, è inoltre sembra molto inefficiente poiché ogni esperimento avrebbe tutti hello stessi componenti ad eccezione di hello training set.

Fortunatamente, è possibile effettuare questa operazione utilizzando hello [ripetizione di training API di Azure Machine Learning](machine-learning-retrain-models-programmatically.md) e automazione di attività hello con [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).

> [!NOTE]
> toomake eseguito più velocemente di questo esempio, si sarà ridurre il numero di hello di percorsi da 1.000 too10. Ma hello gli stessi principi e procedure too1, posizioni 000. Hello unica differenza è che se si desidera tootrain da 1.000 set di dati si vorrà toothink dell'esecuzione di hello seguente script di PowerShell in parallelo. Come toodo che esula hello in questo articolo, ma è possibile trovare esempi di PowerShell multithreading in hello Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Impostare l'esperimento di training hello
Verrà riportato un esempio di toouse [esperimento di training](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) che abbiamo creato in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Aprire l'esperimento nell'area di lavoro di [Azure Machine Learning Studio](https://studio.azureml.net) .

> [!NOTE]
> In ordine toofollow con questo esempio, è opportuno toouse un'area di lavoro standard, anziché un'area di lavoro disponibile. Si verrà creato un endpoint per ogni cliente - per un totale di 10 endpoint - e che richiedono un'area di lavoro standard, poiché un'area di lavoro disponibile è limitata too3 endpoint. Se si dispone solo di un'area di lavoro disponibile, è sufficiente modificare script hello sotto tooallow per solo 3 posizioni.
> 
> 

sperimentazione Hello utilizza un **l'importazione dei dati** modulo tooimport hello training set *customer001.csv* da un account di archiviazione di Azure. Si supponga che abbiamo raccolti i set di dati di training da tutti i percorsi di noleggio di biciclette e salvate in hello stesso percorso di archiviazione del blob con nomi di file compreso tra *rentalloc001.csv* troppo*rentalloc10.csv* .

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Si noti che un **Output del servizio Web** modulo è stato aggiunto toohello **Train Model** modulo.
Quando questo esperimento viene distribuito come servizio web, in formato hello di un file .ilearner endpoint hello associata a tale output restituirà modello con training hello.

Si noti inoltre che è necessario impostare un parametro del servizio web per URL hello che hello **l'importazione dei dati** modulo Usa. In questo modo toouse hello parametro toospecify singoli set di dati tootrain hello modello di training per ogni posizione.
Esistono altri modi in cui è stato possibile eseguita questa operazione, ad esempio mediante una query SQL con un dati tooget parametro del servizio web da un database di SQL Azure o semplicemente un **Input del servizio Web** toopass modulo in un set di dati di toohello servizio web.

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

A questo punto, eseguire questo esperimento di training, specificando il valore predefinito di hello *rental001.csv* come hello set di dati di training. Se si visualizza l'output di hello di hello **Evaluate** modulo (output di hello scegliere **Visualizza**), è possibile vedere si ottiene un ragionevole delle prestazioni di *AUC* = 0.91. A questo punto, si è pronti toodeploy un servizio web da questo esperimento di training.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Distribuire training hello e assegnazione dei punteggi di servizi web
hello toodeploy training servizio web, fare clic su hello **di servizio Web** sotto l'area di disegno esperimento hello e selezionare **distribuzione servizio Web**. Denominare il servizio Web "Bike Rental Training".

A questo punto è necessario il servizio web assegnazione dei punteggi di toodeploy hello.
toodo, è possibile fare clic su **di servizio Web** seguito hello area di disegno e selezionare **servizio Web predittivo**. Verrà creato un esperimento di assegnazione dei punteggi.
È necessario toomake alcune piccole modifiche toomake, che funziona come un servizio web, ad esempio dati di input di rimuovere la colonna di etichetta hello "cnt" dalla hello e limitando l'id dell'istanza hello tooonly output hello e hello corrispondente valore stimato.

toosave manualmente che funzionano, è possibile aprire semplicemente hello [esperimento predittiva](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello raccolta che è già stata preparata.

servizio web di toodeploy hello, eseguire l'esperimento predittiva hello, quindi fare clic su hello **distribuzione servizio Web** pulsante sotto l'area di disegno hello. Hello Nome servizio web "Punteggio noleggio Bike" di punteggio ".

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Creare 10 endpoint di servizio Web identici con PowerShell
Questo servizio Web include un endpoint predefinito, Ma non siamo interessati come endpoint predefinito hello poiché non può essere aggiornata. È necessario toodo è toocreate 10 altri endpoint, uno per ogni posizione. A tale scopo, usare PowerShell.

Configurare l'ambiente PowerShell:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Eseguire quindi hello comando PowerShell seguente:

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Ora abbiamo creato 10 endpoint e contengono hello stesso modello con training sottoposto a training sui *customer001.csv*. È possibile visualizzarli in hello portale di gestione di Azure.

![immagine](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Aggiornare hello endpoint toouse separato training set di dati tramite PowerShell
passaggio successivo Hello è endpoint hello tooupdate con i modelli in modo univoco sottoposto a training sui singoli dati di ogni cliente. Ma è prima necessario tooproduce questi modelli da hello **Bike noleggio Training** servizio web. Necessario tornare indietro toohello **Bike noleggio Training** servizio web. È necessario toocall endpoint BES 10 volte con 10 set di dati di training diversi in modelli diversi di ordine tooproduce 10. Si userà hello **InovkeAmlWebServiceBESEndpoint** toodo cmdlet PowerShell questo.

È necessario anche tooprovide credenziali per l'account di archiviazione blob in `$configContent`, vale a dire, campi hello `AccountName`, `AccountKey` e `RelativeLocation`. Hello `AccountName` può essere uno dei nomi di account, come illustrato nel hello **portale di gestione di Azure classico** (*archiviazione* scheda). Quando si fa clic su un account di archiviazione, il relativo `AccountKey` sono reperibili effettuando premendo hello **Gestisci chiavi di accesso** pulsante nella parte inferiore di hello e copia hello *chiave di accesso primaria*. Hello `RelativeLocation` è archiviazione tooyour relativo percorso di hello in cui verrà archiviato un nuovo modello. Ad esempio, percorso di hello `hai/retrain/bike_rental/` nello script hello sotto punti tooa contenitore denominato `hai`, e `/retrain/bike_rental/` sono le sottocartelle. Attualmente, non è possibile creare sottocartelle tramite l'interfaccia utente del portale hello, ma esistono [Esplora archivi di Azure diversi](../storage/common/storage-explorers.md) che consentono di toodo così. Si consiglia di creare un nuovo contenitore nel hello toostore archiviazione nuovi modelli con training (file .ilearner) come segue: dalla pagina di archiviazione, fare clic su hello **Aggiungi** pulsante nella parte inferiore di hello e denominarlo `retrain`. In sintesi, script toohello le modifiche necessarie hello riportato di seguito riguardano troppo`AccountName`, `AccountKey` e `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> endpoint BES Hello è hello è supportato solo in modalità per questa operazione. Non è possibile usare la modalità RRS per la creazione di modelli di training.
> 
> 

Come si può notare, anziché costruire 10 diversi BES processo json i file di configurazione in modo dinamico invece di creare la stringa di configurazione hello i feed di toohello *jobConfigString* parametro di hello  **InvokeAmlWebServceBESEndpoint** cmdlet, perché non è realmente non tookeep necessità per una copia su disco.

Se tutto va bene, dopo un periodo di tempo dovrebbe 10 file .ilearner, da *model001.ilearner* troppo*model010.ilearner*, nell'account di archiviazione di Azure. Ora siamo tooupdate pronto i 10 punteggio web gli endpoint del servizio con questi modelli utilizzando hello **Patch AmlWebServiceEndpoint** cmdlet di PowerShell. Ricorda nuovamente è solo possibile applicare una patch endpoint non predefinito hello a livello di codice creato in precedenza.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

L'esecuzione dovrebbe essere abbastanza rapida. Al termine dell'esecuzione di hello, si sarà stato creato endpoint servizio web predittivo 10, ognuna delle quali contiene un modello con training, in modo univoco sottoposto a training sui hello set di dati specifico tooa località noleggio, da un esperimento di training singolo. tooverify, è possibile provare a chiamare questi endpoint utilizzando hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, fornire con hello stessi dati di input e, è necessario prevedere che i risultati di stima diverse toosee poiché sono modelli hello eseguito il training con set di training diversi.

## <a name="full-powershell-script"></a>Script di PowerShell completo
Ecco l'elenco hello del codice sorgente completo hello:

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
