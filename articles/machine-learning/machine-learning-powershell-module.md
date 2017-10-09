---
title: modulo aaaPowerShell per Machine Learning | Documenti Microsoft
description: "Hello modulo di PowerShell per Azure Machine Learning è disponibile in modalità di anteprima pubblica. Utilizzare PowerShell toocreate e gestire le aree di lavoro, esperimenti, servizi web e altro ancora."
keywords: esperimento,regressione lineare,algoritmi di machine learning,esercitazione su machine learning,tecniche di modellazione predittiva,esperimento di analisi scientifica dei dati
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: a9001cc2-3aa0-47e1-b175-1f76408ba1d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: garye;haining
ms.openlocfilehash: 59362027356b86bf286b7c07380db677ae1d71c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-module-for-microsoft-azure-machine-learning"></a>Modulo PowerShell per Microsoft Azure Machine Learning
modulo di PowerShell Hello per Azure Machine Learning è uno strumento potente che consente di aree di lavoro toomanage toouse Windows PowerShell, esperimenti, set di dati, servizi web classica e altro ancora.

È possibile visualizzare la documentazione di hello e scaricare il modulo di hello, insieme al codice sorgente completo hello, al [https://aka.ms/amlps](https://aka.ms/amlps). 

> [!NOTE]
> modulo PowerShell di Azure Machine Learning Hello è attualmente in modalità di anteprima. modulo Hello continuerà toobe migliorata ed espanse durante questo periodo di anteprima. È consigliabile monitorare hello [Intelligence Cortana e Blog di Machine Learning](https://blogs.technet.microsoft.com/machinelearning/) per notizie e informazioni.

## <a name="what-is-hello-machine-learning-powershell-module"></a>Che cos'è il modulo di Machine Learning PowerShell hello?
modulo di Machine Learning PowerShell Hello è una. Modulo DLL basata su rete che consente di toofully gestire aree di lavoro di Azure Machine Learning, esperimenti, set di dati, servizi web classica ed endpoint del servizio web classica di Windows PowerShell. 

Insieme a modulo hello, è possibile scaricare il codice sorgente completo hello che include un nettamente separate [livello API c#](https://github.com/hning86/azuremlps/blob/master/code/AzureMLSDK.cs). È possibile fare riferimento a questa DLL dal proprio progetto .NET e gestire Azure Machine Learning tramite il codice .NET. Inoltre, hello DLL dipende da API REST sottostanti che è possibile utilizzare direttamente dal client preferito.

## <a name="what-can-i-do-with-hello-powershell-module"></a>Che cosa può fare con il modulo PowerShell di hello?
Ecco alcune delle attività hello che è possibile eseguire con questo modulo di PowerShell. Estrarre hello [completo documentazione](https://aka.ms/amlps) per queste e molte altre funzioni.

* Effettuare il provisioning di una nuova area di lavoro usando un certificato di gestione ([New-AmlWorkspace](https://github.com/hning86/azuremlps#new-amlworkspace))
* Esportare e importare un file JSON che rappresenta un grafico di un esperimento ([Export-AmlExperimentGraph](https://github.com/hning86/azuremlps#export-amlexperimentgraph) e [Import-AmlExperimentGraph](https://github.com/hning86/azuremlps#import-amlexperimentgraph))
* Eseguire un esperimento ([Start-AmlExperiment](https://github.com/hning86/azuremlps#start-amlexperiment))
* Creare un servizio Web al di fuori di un esperimento predittivo ([New-AmlWebService](https://github.com/hning86/azuremlps#new-amlwebservice))
* Creare un endpoint in un servizio Web pubblicato ([Add-AmlWebServiceEndpoint](https://github.com/hning86/azuremlps#add-amlwebserviceendpoint))
* Richiamare un endpoint di servizio Web RRS e/o BES ([Invoke-AmlWebServiceRRSEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) e [Invoke-AmlWebServicBESEndpoint](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint))

Di seguito è riportato un esempio di PowerShell toorun un esperimento esistente utilizzando:

        #Find hello first Experiment named “xyz”
        $exp = (Get-AmlExperiment | where Description -eq ‘xyz’)[0]
        #Run hello Experiment
        Start-AmlExperiment -ExperimentId $exp.ExperimentId 

Per un caso d'uso più dettagliate, vedere l'articolo sull'utilizzo di hello PowerShell modulo tooautomate un'attività in genere richieste: [creare molti modelli di Machine Learning e web gli endpoint del servizio da un esperimento con PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).

## <a name="how-do-i-get-started"></a>Come iniziare?
tooget avviato con PowerShell di Machine Learning, scaricare hello [pacchetto versione](https://github.com/hning86/azuremlps/releases) da GitHub e seguire hello [istruzioni per l'installazione](https://github.com/hning86/azuremlps/blob/master/README.md). istruzioni di Hello spiegano come toounblock hello scaricato/decompressi nella DLL e quindi importarlo in ambiente di PowerShell. La maggior parte dei cmdlet è necessario fornire l'ID area di lavoro hello, token di autorizzazione hello dell'area di lavoro e hello regione di Azure che hello dell'area di lavoro hello è in. valori Hello più semplici modo tooprovide hello viene eseguita tramite un file config. JSON predefinito. istruzioni di Hello illustrano inoltre come tooconfigure questo file. 

E, se si desidera, è possibile clonare albero git hello, modificare codice hello e compilare localmente tramite Visual Studio.

## <a name="next-steps"></a>Passaggi successivi
È possibile trovare la documentazione completa di hello per il modulo PowerShell di hello in [https://aka.ms/amlps](https://aka.ms/amlps). 

Per un esempio esteso di modalità toouse hello modulo in uno scenario reale, estrazione hello approfondita utilizzare case, [creare molti modelli di Machine Learning e web gli endpoint del servizio da un esperimento con PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md).
