---
title: 'Passaggio 1: Creare un''area di lavoro di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 1 di hello sviluppare una procedura dettagliata soluzione predittiva: informazioni su come tooset una nuova area di lavoro di Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a>Passaggio 1 della procedura dettagliata: Creare un'area di lavoro di Machine Learning
Questo è hello primo passaggio della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md).

1. **Creare un'area di lavoro di Machine Learning**
2. [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)
3. [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eseguire il training e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Distribuzione di servizio Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accedere al servizio Web hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

toouse Machine Learning Studio, è necessario toohave un'area di lavoro di Microsoft Azure Machine Learning. L'area di lavoro contiene strumenti hello necessari toocreate, gestire e pubblicare esperimenti.  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

messaggio per l'amministratore per la sottoscrizione di Azure deve dell'area di lavoro di toocreate hello e quindi aggiunto come proprietario o collaboratore. Per informazioni, vedere [Creare un'area di lavoro di Azure Machine Learning](machine-learning-create-workspace.md).

Dopo aver creato l'area di lavoro, aprire Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net/Home)). Se si dispone di più di un'area di lavoro, è possibile selezionare l'area di lavoro hello hello sulla barra degli strumenti hello alto a destra della finestra hello.

![Selezionare l'area di lavoro in Studio][2]

> [!TIP]
> Se sono state apportate un proprietario dell'area di lavoro hello, è possibile condividere gli esperimenti di hello si sta lavorando per invitare altri utenti toohello dell'area di lavoro. È possibile farlo in Machine Learning Studio su hello **impostazioni** pagina. Per ogni utente è sufficiente hello account di Microsoft o aziendale.
> 
> In hello **impostazioni** pagina, fare clic su **utenti**, quindi fare clic su **INVITARE utenti più** nella parte inferiore di hello della finestra hello.
> 
> 

- - -
**Passaggio successivo: [Caricare i dati esistenti](machine-learning-walkthrough-2-upload-data.md)**

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
