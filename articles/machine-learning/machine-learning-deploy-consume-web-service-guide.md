---
title: 'Servizi Web di Azure Machine Learning: distribuzione e utilizzo | Documentazione Microsoft'
description: Risorse per la distribuzione e l'uso dei servizi Web.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Servizi Web di Azure Machine Learning: distribuzione e uso
È possibile utilizzare Azure Machine Learning toodeploy machine learning flussi di lavoro e i modelli come servizi web. Questi servizi web possono quindi essere modelli di machine learning hello toocall utilizzati dalle applicazioni tramite le stime toodo Internet hello in tempo reale o in modalità batch. Poiché i servizi web hello RESTful, è possibile chiamarli da diversi linguaggi di programmazione e piattaforme, ad esempio .NET e Java e da applicazioni, ad esempio Excel.

Nelle sezioni successive di Hello forniscono collegamenti toowalkthroughs, codice e documentazione toohelp iniziare.

## <a name="deploy-a-web-service"></a>Distribuire un servizio Web
### <a name="with-azure-machine-learning-studio"></a>Con Azure Machine Learning Studio
Machine Learning Studio e il portale di servizi Web di Microsoft Azure Machine Learning hello consentono di distribuire e gestire un servizio web senza scrivere codice.

i collegamenti seguenti Hello forniscono informazioni generali su come toodeploy un nuovo servizio web:

* Per una panoramica sul funzionamento toodeploy un nuovo servizio web che si basa su Gestione risorse di Azure, vedere [distribuire un nuovo servizio web](machine-learning-webservice-deploy-a-web-service.md).
* Per una procedura dettagliata su come toodeploy un servizio web, vedere [distribuire un servizio web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Per una procedura dettagliata completa sul toocreate e distribuire un servizio web, vedere [procedura dettagliata passaggio 1: creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).
* Per esempi specifici di distribuzione di un servizio Web, vedere:

  * [Procedura dettagliata passaggio 5: Distribuzione di servizio web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md)
  * [Come toodeploy web service toomultiple aree](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Con le API del provider di risorse di servizi Web (API di Azure Resource Manager)
provider di risorse di Azure Machine Learning Hello per servizi web consente la distribuzione e gestione dei servizi web tramite chiamate all'API REST. Per altre informazioni, vedere i riferimenti al [servizio Web di Machine Learning (REST)](/rest/api/machinelearning/index).

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Con i cmdlet di PowerShell
Il provider di risorse di Azure Machine Learning per i servizi Web consente di distribuire e gestire i servizi Web tramite cmdlet di PowerShell.

toouse hello cmdlet, è necessario innanzitutto accedere tooyour account di Azure dall'ambiente di PowerShell hello utilizzando hello [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Se non si ha familiarità con modalità toocall PowerShell comandi che si basano su Gestione risorse, vedere [tramite Azure PowerShell con Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport sperimentare la stima, utilizzare [questo codice di esempio](https://github.com/ritwik20/AzureML-WebServices). Dopo aver creato il file di .exe hello dal codice hello, è possibile digitare:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Esecuzione di un'applicazione hello crea un modello di JSON del servizio web. modello hello toouse toodeploy un servizio web, è necessario aggiungere hello le seguenti informazioni:

* Nome e chiave dell'account di archiviazione

    È possibile ottenere nome account di archiviazione hello e la chiave da entrambi hello [portale di Azure](https://portal.azure.com/) o hello [portale di Azure classico](http://manage.windowsazure.com/).
* ID del piano di impegno

    È possibile ottenere l'ID del piano hello da hello [servizi Web di Azure Machine Learning](https://services.azureml.net) portale Accedi e facendo clic sul nome di un piano.

Aggiungerli modello JSON toohello come elementi figlio di hello *proprietà* nodo hello stesso livello come hello *MachineLearningWorkspace* nodo.

Ad esempio:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Vedere i seguenti articoli hello e codice per altri dettagli di esempio:

* [cmdlet di Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) in MSDN
* [Procedura dettagliata](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) di esempio su GitHub

## <a name="consume-hello-web-services"></a>Utilizzare i servizi web hello
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>Da hello Azure Machine Learning servizi dell'interfaccia utente Web (test)
È possibile testare il servizio web dal portale di servizi Web di Azure Machine Learning hello. Ciò include la verifica del servizio di richiesta-risposta hello (RR) e delle interfacce del servizio esecuzione Batch (BES).

* [Distribuire un nuovo servizio Web](machine-learning-webservice-deploy-a-web-service.md)
* [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* [Procedura dettagliata passaggio 5: Distribuzione di servizio web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Da Excel
È possibile scaricare un modello di Excel che utilizza servizio web hello:

* [Utilizzo di un servizio Web di Azure Machine Learning da Excel](machine-learning-consuming-from-excel.md)
* [Componente aggiuntivo Excel per i servizi Web di Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>Da un client basato su REST
I servizi Web di Azure Machine Learning sono API RESTful. È possibile utilizzare queste API da diverse piattaforme, ad esempio .NET, Python, R, Java, hello e così via **consumare** pagina per il servizio web in hello [portale di servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net) dispone di esempio codice che consentono di iniziare. Per ulteriori informazioni, vedere [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).
