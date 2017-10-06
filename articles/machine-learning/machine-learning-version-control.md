---
title: in Azure Machine Learning aaaALM | Documenti Microsoft
description: Applicare le procedure consigliate per la gestione del ciclo di vita dell'applicazione in Azure Machine Learning Studio
keywords: ALM, AML, Azure ML, Gestione del ciclo di vita dell'applicazione, Controllo delle versioni
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Gestione del ciclo di vita dell'applicazione in Azure Machine Learning Studio
Azure Machine Learning Studio è uno strumento per lo sviluppo di esperimenti di machine learning che sono operativi nella piattaforma di cloud di Azure hello. È ad esempio hello IDE di Visual Studio e il servizio cloud scalabili unite in un'unica piattaforma. È possibile incorporare procedure standard di Application Lifecycle Management (ALM), dal controllo delle versioni delle varie risorse tooautomated esecuzione e la distribuzione, in Azure Machine Learning Studio. In questo articolo vengono descritte alcune delle opzioni di hello e approcci.

## <a name="versioning-experiment"></a>Controllo della versione degli esperimenti
Esistono due metodi consigliati tooversion gli esperimenti. È possibile basarsi sulla cronologia di esecuzione predefinita, o esportare esperimento hello in formato JavaScript Object Notation (JSON) e gestirlo esternamente. Ecco vantaggi e svantaggi di ogni approccio.

### <a name="experiment-snapshots-using-run-history"></a>Snapshot dell'esperimento tramite la cronologia di esecuzione
Nel modello di esecuzione hello di hello learning di Azure Machine Learning Studio esperimento, ogni volta che si fa clic su hello **eseguire** pulsante nell'editor di sperimentazione hello, uno snapshot non modificabile di sperimentazione hello viene inviato toohello pianificatore di processi. È possibile visualizzare l'elenco di snapshot, fare clic su hello **eseguire cronologia** pulsante sulla barra dei comandi di hello in vista dell'editor hello esperimento.

![Pulsante Cronologia di esecuzione](media/machine-learning-version-control/runhistory.png)

È possibile quindi snapshot hello aperto in modalità bloccato facendo clic sul nome hello dell'esperimento hello all'esperimento di hello hello ora è stato inviato toorun e hello dello snapshot. Si noti che solo hello primo elemento nell'elenco di hello, che rappresenta l'esperimento corrente hello, è in uno stato modificabile. Si osservi anche che ogni snapshot può presentare diversi stati, tra cui Completato (esecuzione parziale), Non riuscito, Non riuscito (esecuzione parziale) o Bozza.

![Elenco Cronologia di esecuzione](media/machine-learning-version-control/runhistorylist.png)

Dopo che è aperto, è possibile salvare hello snapshot esperimento come un esperimento di nuovo e quindi modificarlo. Se lo snapshot esperimento contiene risorse, ad esempio un modello con training, trasformazione o set di dati che dispongano di versioni aggiornate, snapshot hello mantenere versione originale di hello riferimenti toohello hello dello snapshot. Se si salva hello bloccato snapshot come un esperimento di nuovo, Azure Machine Learning Studio rileva l'esistenza di hello di una versione più recente di queste risorse e aggiorna automaticamente nell'esperimento nuovo hello.

Se si elimina l'esperimento hello, vengono eliminati tutti gli snapshot di tale esperimento.

### <a name="exportimport-experiment-in-json-format"></a>Esportare/importare un esperimento in formato JSON
gli snapshot della cronologia di esecuzione Hello mantenere una versione non modificabile di hello esperimento in Azure Machine Learning Studio ogni volta che viene inviato toorun. È possibile inoltre salvare una copia locale di sperimentazione hello archiviarlo nel sistema di controllo origine preferito tooyour, ad esempio Team Foundation Server e ricreare un esperimento dai file locali in un secondo momento. È possibile utilizzare hello [Azure Machine Learning PowerShell](http://aka.ms/amlps) cmdlet [ *esportazione AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) e [  *Importazione AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish che.

file JSON Hello è una rappresentazione testuale di hello sperimentare grafico, che potrebbe includere un riferimento tooassets nell'area di lavoro di hello, ad esempio un set di dati o un modello con training. Non contiene una versione serializzata di asset hello. Se si tenta di documento JSON di hello tooimport indietro nell'area di lavoro di hello, asset hello a cui fa riferimento deve essere già esistente con hello stesso asset ID a cui fa riferimento nell'esperimento hello. In caso contrario non sarà in grado di tooaccess hello importato esperimento.

## <a name="versioning-trained-model"></a>Controllo della versione del modello sottoposto a training
Un modello con Training in Azure Machine Learning viene serializzato in un formato noto come un file .iLearner e viene archiviato nell'account di archiviazione Blob di Azure hello associati hello area di lavoro. Un modo tooget una copia del file .iLearner hello viene eseguita tramite hello ripetizione di training API. [In questo articolo](machine-learning-retrain-models-programmatically.md) illustra il funzionamento hello ripetizione di training API. passaggi di alto livello Hello:

1. Impostare l'esperimento di training.
2. Aggiungere un modulo Train Model toohello di web service output porta o un modulo hello che produce modello con training hello, ad esempio ottimizzare modello Hyperparameter o Create R Model.
3. Eseguire l'esperimento di training e quindi distribuirlo come servizio Web di training del modello.
4. Chiamare hello BES endpoint di hello training servizio web e specificare nome del file hello .iLearner desiderato e posizione dell'account di archiviazione Blob in cui verrà archiviata.
5. Al termine del raccolto hello prodotto .iLearner file dopo la chiamata hello BES.

File di un altro modo tooretrieve hello .iLearner è tramite il cmdlet di PowerShell hello [ *Download AmlExperimentNodeOutput*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Questo potrebbe essere più semplice se si desidera tooget una copia di hello .iLearner file senza modello hello tooretrain necessità di hello a livello di codice.

Dopo aver hello .iLearner contenente modello con training hello, è quindi possibile utilizzare la propria strategia di controllo delle versioni. strategia di Hello può essere semplice come l'applicazione di un precedente/suffisso come una convenzione di denominazione e lasciando solo il file .iLearner hello nell'archiviazione Blob o copia/importandoli nel sistema di controllo delle versioni.

file di .iLearner salvato Hello può quindi essere utilizzato per il punteggio tramite servizi web distribuiti.

## <a name="versioning-web-service"></a>Controllo della versione del servizio Web
È possibile distribuire due tipi di servizi Web da un esperimento di Azure Machine Learning. servizio web classico Hello è strettamente con esperimento hello come area di lavoro hello. nuovo servizio web di Hello utilizza il framework di gestione risorse di Azure hello e non è accoppiato con area di lavoro di hello o esperimento originale hello.

### <a name="classic-web-service"></a>Servizio Web classico
tooversion un servizio web classico, è possibile usufruire di costrutto di endpoint servizio web hello. Ecco un metodo tipico:

1. Dall'esperimento predittivo, distribuire un nuovo servizio Web classico che contiene un endpoint predefinito.
2. Si crea un nuovo endpoint denominato ep2, che espone versione corrente di hello di hello esperimento o training del modello.
3. È necessario tornare indietro e aggiornare l'esperimento predittivo e il modello sottoposto a training.
4. Si ridistribuisce l'esperimento predittiva hello, che verrà quindi aggiornare l'endpoint predefinito hello. Ciò non incide sull'ep2.
5. Si crea un endpoint aggiuntivo denominato ep3, che espone una nuova versione di hello dell'esperimento hello e il modello con training.
6. Tornare indietro toostep 3 se necessario.

Nel corso del tempo, potrebbe essere creati molti nel hello stesso al servizio web. Ogni endpoint rappresenta una copia in un momento di sperimentazione hello contenente hello temporizzati nella versione del modello con training hello. È quindi possibile utilizzare toodetermine logica esterna che toocall endpoint, che comporta la selezione di una versione di hello training del modello per l'esecuzione dell'assegnazione punteggio hello.

È possibile inoltre creare molti endpoint del servizio web identici e quindi applicare patch versioni diverse di hello .iLearner file toohello endpoint tooachieve paragonabile. [In questo articolo](machine-learning-create-models-and-endpoints-with-powershell.md) viene illustrato in dettaglio come tooaccomplish che.

### <a name="new-web-service"></a>Nuovo servizio Web
Se si crea un nuovo servizio web basato su Gestione risorse di Azure, hello endpoint costrutto non è più disponibile. In alternativa, è possibile generare file di definizione (WSD) del servizio web, in formato JSON, dall'esperimento usando hello predittiva [esportazione AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) cmdlet di PowerShell, oppure utilizzando hello [ *Esportazione AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet di PowerShell da un servizio web basato su Gestione risorse distribuite.

Dopo aver esportato hello controllare tale versione e il file WSD, è inoltre possibile distribuire hello WSD come un nuovo servizio web in un piano di servizio web diversi in un'area diversa di Azure. È sufficiente Assicurarsi che è specificare l'account di archiviazione appropriato hello configurazione nonché hello web nuovo ID del piano di servizio toopatch .iLearner diversi file, è possibile modificare il file WSD hello e riferimento al percorso di aggiornamento hello di hello eseguito il training del modello e distribuirlo come un nuovo servizio web.

## <a name="automate-experiment-execution-and-deployment"></a>Automatizzare la distribuzione e l'esecuzione dell'esperimento
Un aspetto importante di ALM è esecuzione hello tooautomate in grado di toobe e processo di distribuzione di un'applicazione hello. In Azure Machine Learning, è possibile effettuare questa operazione utilizzando hello [modulo PowerShell](http://aka.ms/amlps). Di seguito è riportato un esempio di passaggi end-to-end che risultano rilevanti tooa del processo di esecuzione/distribuzione standard ALM automatizzata con hello [modulo PowerShell di Azure Machine Learning Studio](http://aka.ms/amlps). Ogni passaggio è collegato tooone o più cmdlet PowerShell che è possibile utilizzare tooaccomplish passaggio.

1. [Caricare un set di dati](https://github.com/hning86/azuremlps#upload-amldataset).
2. Copiare un esperimento di training hello area di lavoro da un [dell'area di lavoro](https://github.com/hning86/azuremlps#copy-amlexperiment) o da [raccolta](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), o [importare](https://github.com/hning86/azuremlps#import-amlexperimentgraph) un [esportato](https://github.com/hning86/azuremlps#export-amlexperimentgraph) sperimentare da disco locale.
3. [Aggiornare i set di dati hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) nell'esperimento di training hello.
4. [Eseguire l'esperimento di training hello](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Alzare di livello del modello con training hello](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Copiare un esperimento predittivo](https://github.com/hning86/azuremlps#copy-amlexperiment) nell'area di lavoro hello.
7. [Training modello di aggiornamento hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) nell'esperimento predittiva hello.
8. [Eseguire l'esperimento predittiva hello](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Distribuire un servizio web](https://github.com/hning86/azuremlps#new-amlwebservice) da esperimento predittiva hello.
10. Test di servizio web hello [RR](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) o [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) endpoint.

## <a name="next-steps"></a>Passaggi successivi
* Scaricare hello [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps) tooautomate modulo e avviare le attività ALM.
* Informazioni su come troppo[creare e gestire un numero elevato di modelli di Machine Learning tramite un esperimento di singolo](machine-learning-create-models-and-endpoints-with-powershell.md) tramite PowerShell e API di ripetizione di training.
* Altre informazioni sulla [distribuzione di servizi Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
