---
title: un servizio web Azure Machine Learning nuovo con PowerShell aaaRetrain | Documenti Microsoft
description: Informazioni su come tooprogrammatically ripetere il training di un modello e l'aggiornamento hello toouse hello appena sottoposto a training modello di servizio web in Azure Machine Learning tramite i cmdlet di PowerShell di gestione di Machine Learning hello.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Ripetere il training di un servizio web basato su nuovo gestore di risorse utilizzando i cmdlet di PowerShell di gestione di Machine Learning hello
Quando si ripetere il training di un nuovo servizio web, si aggiorna hello predittiva definizione tooreference hello nuovo sottoposto a training modello di servizio web.  

## <a name="prerequisites"></a>Prerequisiti
È necessario impostare un esperimento di training e un esperimento predittivo come illustrato in [Ripetere il training dei modelli di Machine Learning in modo programmatico](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> sperimentazione predittiva Hello deve essere distribuito come una gestione risorse di Azure (nuovo) basato su servizio web machine learning. un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Per altre informazioni sulla distribuzione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Questo processo richiede che sia stato installato hello cmdlet di Azure Machine Learning. Per installare i cmdlet di Machine Learning hello di informazioni, vedere hello [i cmdlet di Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) riferimento su MSDN.

Hello copiato dalla ripetizione di training output hello le seguenti informazioni:

* BaseLocation
* RelativeLocation

Hello i passaggi sono:

1. Accedi tooyour account di gestione risorse di Azure.
2. Ottenere una definizione del servizio web hello
3. Esportazione hello definizione del servizio Web nel formato JSON
4. Aggiornare i blob di ilearner toohello riferimento hello in hello JSON.
5. Importare hello JSON in una definizione del servizio Web
6. Aggiornare il servizio web hello con nuova definizione del servizio Web

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Accedi tooyour account di gestione risorse di Azure
È necessario innanzitutto accedere nell'account di Azure dall'ambiente di PowerShell hello utilizzando hello tooyour [Aggiungi AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.

## <a name="get-hello-web-service-definition"></a>Ottenere hello definizione del servizio Web
Quindi, ottenere hello servizio Web dal chiamante hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Hello definizione del servizio Web è una rappresentazione interna del modello con training di hello del servizio web hello e non è direttamente modificabile. Assicurarsi che si desidera recuperare hello definizione del servizio Web per l'esperimento predittiva e non l'esperimento di training.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello Nome gruppo di risorse di un servizio web esistente, eseguire il cmdlet Get-AzureRmMlWebService hello senza servizi parametri toodisplay hello web nella sottoscrizione. Servizio web hello di individuare e quindi esaminare il relativo ID di servizio web. nome di Hello hello del gruppo di risorse è elemento quarto hello ID hello, subito dopo hello *resourceGroups* elemento. Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

In alternativa, toodetermine hello Nome gruppo di risorse di un servizio web esistente, i log nel portale di servizi Web di Microsoft Azure Machine Learning toohello. Selezionare servizio web hello. nome del gruppo di risorse Hello è hello quinto elemento hello URL del servizio web hello, subito dopo hello *resourceGroups* elemento. Nell'esempio seguente di hello, nome del gruppo di risorse hello è MachineLearning-predefinito-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Esportazione hello definizione del servizio Web nel formato JSON
toomodify hello definizione toohello training del modello toouse hello appena modello con training, è innanzitutto necessario utilizzare hello [esportazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport cmdlet è tooa file di formato JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Aggiornare i blob di ilearner toohello riferimento hello in hello JSON.
Attività hello, individuare hello [modello con training], aggiornamento hello *uri* valore hello *locationInfo* nodo con l'URI del blob ilearner hello hello. Hello URI viene generato dalla combinazione hello *BaseLocation* hello e *RelativeLocation* dall'output di hello di chiamata i BES hello. Aggiorna hello percorso tooreference hello nuovo modello con training.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition"></a>Importare hello JSON in una definizione del servizio Web
È necessario utilizzare hello [importazione AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modificati file JSON in una definizione del servizio Web che è possibile utilizzare tooupdate hello definizione del servizio Web.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Aggiornare il servizio web hello con nuova definizione del servizio Web
Utilizzare infine [aggiornamento AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello definizione del servizio Web.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Riepilogo
Utilizzando i cmdlet di gestione di PowerShell di Machine Learning hello, è possibile aggiornare il modello con training di hello di un servizio Web predittivo l'abilitazione di scenari, ad esempio:

* Ripetizione periodica del training del modello con nuovi dati.
* Distribuzione di un modello di toocustomers con obiettivo hello di informarli del training modello di hello usando i propri dati.

