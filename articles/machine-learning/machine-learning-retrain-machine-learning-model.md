---
title: un modello di Machine Learning aaaRetrain | Documenti Microsoft
description: Informazioni su come tooretrain un modello e aggiornamento hello toouse hello appena sottoposto a training modello di servizio Web in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Ripetere il training di un modello di Machine Learning
Come parte del processo di hello di rendere operativo il computer di modelli di apprendimento in Azure Machine Learning, il modello è stato sottoposto a training e salvato. È quindi utilizzarlo toocreate predicative servizio Web. Hello servizio Web può quindi essere utilizzato in siti web, dashboard e App per dispositivi mobili. 

I modelli creati con Machine Learning in genere non sono statici. Man mano che diventano disponibili nuovi dati o quando il consumer hello di hello API ha i propri modelli di dati hello devono toobe ripetere il training. 

La ripetizione del training può avvenire di frequente. Grazie a funzionalità di API di ripetizione di training a livello di codice hello, è possibile a livello di programmazione ripetere il training modello di hello utilizzo hello servizio Web hello API ripetizione di training e di aggiornamento con modello sottoposto a training appena hello. 

Questo documento descrive hello processo di ripetizione di training e Mostra come toouse hello API ripetizione di training.

## <a name="why-retrain-defining-hello-problem"></a>Motivo per cui ripetere il training: definizione hello problema
Come parte di hello machine learning processo di training, un modello viene eseguito il training usando un set di dati. I modelli creati con Machine Learning in genere non sono statici. Man mano che diventano disponibili nuovi dati o quando il consumer hello di hello API ha i propri modelli di dati hello devono toobe ripetere il training.

In questi scenari, un'API a livello di codice fornisce un modo pratico di tooallow si o hello consumer del toocreate API, un client che è possibile, in modo occasionale o regolare, ripetere il training hello modello utilizzando i propri dati. Possono quindi valutare i risultati di hello di ripetizione di training e aggiornare hello API toouse hello appena sottoposto a training modello di servizio Web.

> [!NOTE]
> Se si dispone di un esperimento di Training esistenti e il servizio Web di nuovo, è consigliabile toocheck fuori servizio un Web predittivo esistente anziché hello nella procedura dettagliata seguente indicata nella seguente sezione hello ripeterne il training.
> 
> 

## <a name="end-to-end-workflow"></a>Flusso di lavoro end-to-end
processo Hello implica hello seguenti componenti: un esperimento di Training e un esperimento predittiva pubblicata come servizio Web. tooenable ripetizione di training di un modello con training, hello esperimento di Training deve essere pubblicata come servizio Web con l'output di hello di un modello con training. In questo modo modello toohello di accesso dell'API per la ripetizione di training. 

Hello alla procedura seguente si applica tooboth nuovo e classico servizi Web:

Creazione del servizio Web predittivo iniziale hello:

* Creare un esperimento di training
* Creare un esperimento Web predittivo
* Distribuire un servizio Web predittivo

Ripetere il training del servizio Web hello:

* Aggiornare tooallow esperimento di training per la ripetizione di training
* Distribuire hello ripetizione di training servizio web
* Utilizzare il modello hello tooretrain di hello servizio esecuzione Batch codice

Per una procedura dettagliata di hello passaggi precedenti, vedere [Machine Learning ripetere il training dei modelli a livello di codice](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> un nuovo servizio web deve disporre di autorizzazioni sufficienti in hello toowhich di sottoscrizione per la distribuzione del servizio web hello toodeploy. Per ulteriori informazioni, vedere [gestire un servizio Web tramite il portale di servizi Web di Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Se è stato distribuito un servizio Web classico:

* Creare un nuovo Endpoint nel servizio Web predittivo hello
* Ottenere l'URL di PATCH hello e codice
* Utilizzare prova URL PATCH toopoint prova nuovo Endpoint di hello ripetere il training del modello 

Per una procedura dettagliata di hello passaggi precedenti, vedere [ripetere il training di un servizio Web classico](machine-learning-retrain-a-classic-web-service.md).

Se si verificano problemi di un servizio Web classico di ripetizione di training, vedere [risoluzione dei problemi hello ripetizione di training di un servizio Web di Azure Machine Learning classico](machine-learning-troubleshooting-retraining-models.md).

Se è stato distribuito un nuovo servizio Web:

* Accedi tooyour account di gestione risorse di Azure
* Ottenere una definizione del servizio Web hello
* Esportazione hello definizione del servizio Web nel formato JSON
* Aggiornare hello riferimento toohello `ilearner` blob in hello JSON
* Importare hello JSON in una definizione del servizio Web
* Aggiornare il servizio Web hello con nuova definizione del servizio Web

Per una procedura dettagliata di hello passaggi precedenti, vedere [ripetere il training di un servizio Web di nuovo utilizzando i cmdlet di PowerShell di gestione di Machine Learning hello](machine-learning-retrain-new-web-service-using-powershell.md).

il processo di Hello per la configurazione di ripetizione di training per un servizio Web classico include hello alla procedura seguente:

![Panoramica del processo di ripetizione del training][1]

il processo di Hello per la configurazione di ripetizione di training per un servizio Web nuovo include hello alla procedura seguente:

![Panoramica del processo di ripetizione del training][7]

## <a name="other-resources"></a>Altre risorse
* [Retraining and Updating Azure Machine Learning models with Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/) (Ripetere il training e aggiornare modelli di Azure Machine Learning con Azure Data Factory)
* [Creare più modelli di Machine Learning ed endpoint di servizio Web da un esperimento usando PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)
* Hello [AML ripetizione di training modelli utilizzando le API](https://www.youtube.com/watch?v=wwjglA8xllg) video illustra la modalità di creazione di modelli di Machine Learning tooretrain in Azure Machine Learning usando hello API ripetizione di training e PowerShell.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

