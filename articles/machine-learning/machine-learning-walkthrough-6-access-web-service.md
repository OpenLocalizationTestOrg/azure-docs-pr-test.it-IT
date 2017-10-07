---
title: 'Passaggio 6: Accesso del servizio Web di Machine Learning hello | Documenti Microsoft'
description: 'Passaggio 6 di hello sviluppare una procedura dettagliata soluzione predittiva: accedere a un servizio Web di Azure Machine Learning attivo.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Procedura dettagliata passaggio 6: Accedere al servizio web Azure Machine Learning hello

Hello ultimo passaggio della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)
3. [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eseguire il training e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Distribuzione di servizio Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. **Accedere al servizio Web hello**

- - -
Nel passaggio precedente di hello in questa procedura dettagliata sono stati distribuiti un servizio web che utilizza il nostro modello di stima rischio di credito. Ora gli utenti sono in grado di toosend dati tooit e ricevano i risultati. 

Hello servizio Web è un servizio web di Azure che può ricevere e restituire dati tramite le API REST in uno dei due modi:  

* **Richiesta/risposta** : utente hello invia uno o più righe di carta di credito dati toohello del servizio tramite un protocollo HTTP e hello servizio risponde con uno o più set di risultati.
* **Esecuzione batch** : utente hello archivia uno o più righe di dati di carta di credito in un Azure blob e quindi invia hello blob percorso toohello servizio. Archivia i risultati in un altro blob hello e restituisce l'URL del contenitore di hello hello di punteggi servizio Hello che tutti hello righe di dati nel blob di input.  

Hello tooaccess modo rapido e semplice consiste nell'utilizzare un servizio web classica hello [Azure ML richiesta-risposta del servizio Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) o [modello di App di Azure ML Batch esecuzione del servizio Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

I modelli di app Web consentono di compilare un'app Web personalizzata che riconosce i dati di input del servizio Web e i dati da restituire. È sufficiente toodo forniscono dati e servizio web di accesso tooyour e modello hello hello rest.

Per ulteriori informazioni sull'utilizzo di modelli di hello web app, vedere [utilizzo di un servizio Web di Azure Machine Learning con un modello di app web](machine-learning-consume-web-service-with-web-app-template.md).

È inoltre possibile sviluppare un servizio web di applicazione personalizzata tooaccess hello utilizzando il codice di avvio disponibile per l'utente in R, c# e linguaggi di programmazione Python.

È possibile trovare informazioni dettagliate in [come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).

