---
title: aaaA soluzione predittiva per il rischio di credito con Machine Learning | Documenti Microsoft
description: Una procedura dettagliata che illustra come una soluzione analitica predittiva, per la carta di credito toocreate valutazione dei rischi in Azure Machine Learning Studio.
keywords: rischio di credito, soluzione di analisi predittiva, valutazione del rischio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Procedura dettagliata: Sviluppare una soluzione di analisi predittiva per la valutazione del rischio di credito in Azure Machine Learning

In questa procedura dettagliata, abbiamo esaminato un estesa processo hello di sviluppo di una soluzione analitica predittiva in Machine Learning Studio. È un semplice modello di Machine Learning Studio di sviluppare e quindi distribuirla come servizio web di Azure Machine Learning in modello hello possibile effettuare stime utilizzando nuovi dati. 

In questa procedura dettagliata si presuppone che Machine Learning Studio sia già stato usato almeno una volta e che alcuni concetti di Machine Learning siano noti, ma non si dà per scontato che l'utente sia un esperto.

Se non si è mai utilizzato **Azure Machine Learning Studio** prima, potrebbe essere necessario toostart esercitazione hello, [crea l'analisi scientifica dei dati prima di provare in Azure Machine Learning Studio](machine-learning-create-experiment.md). Tale esercitazione illustra Machine Learning Studio hello per la prima volta. Viene nozioni fondamentali di hello dei moduli come toodrag e rilascio nell'esperimento, collegarli, eseguire l'esperimento hello e visualizzare i risultati di hello. Un altro strumento che può risultare utile per iniziare è un diagramma che offra una panoramica delle funzionalità di hello di Machine Learning Studio. È possibile scaricarlo e stamparlo da qui: [Diagramma della panoramica delle funzionalità di Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
 
Se si è nuovo campo toohello di machine learning in generale, è una serie di video che potrebbe essere utile tooyou. Viene chiamato [analisi scientifica dei dati per i principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) ed è possibile concedere una formazione toomachine introduzione grande usando vocaboli e concetti.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>problema di Hello

Si supponga che è necessario toopredict il rischio di credito dei singoli in base alle informazioni di hello fornita in un'applicazione di carta di credito.  

La valutazione del rischio di credito è un problema complesso, ma è possibile semplificarla per questa procedura dettagliata. Verrà usata come esempio di come è possibile creare una soluzione di analisi predittiva con Microsoft Azure Machine Learning Studio. toodo, vengono utilizzati da Azure Machine Learning Studio e un servizio web Machine Learning.  

## <a name="hello-solution"></a>soluzione Hello

In questa procedura dettagliata, si inizia con dati sul rischio di credito disponibili pubblicamente, quindi si sviluppa e si crea un modello predittivo in base a tali dati. Quindi è distribuire il modello di hello come servizio web in modo che può essere utilizzato da altri utenti per valutare il rischio di credito.

toocreate questa soluzione di valutazione dei rischi di carta di credito, eseguire la procedura seguente è:  

1. [Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)
3. [Creare un esperimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eseguire il training e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Distribuzione di servizio web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Servizio web di accesso hello](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> È possibile trovare una copia di lavoro dell'esperimento hello che si sviluppa in questa procedura dettagliata in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Andare troppo**[procedura dettagliata: stima di rischio di credito](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  e fare clic su **Open in Studio** toodownload una copia dell'esperimento hello nell'area di lavoro di Machine Learning Studio.
> 
> Questa procedura dettagliata è basata su una versione semplificata dell'esperimento di esempio hello [Binary Classification: stima di rischio di credito](http://go.microsoft.com/fwlink/?LinkID=525270), disponibile anche in hello [raccolta](http://gallery.cortanaintelligence.com/).
