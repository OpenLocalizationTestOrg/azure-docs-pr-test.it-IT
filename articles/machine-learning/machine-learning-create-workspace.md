---
title: un'area di lavoro di Machine Learning aaaCreate | Documenti Microsoft
description: Come toocreate un'area di lavoro per Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Creare e condividere un'area di lavoro di Azure Machine Learning
Questo menu Collega tootopics che descrivono come tooset backup hello diversi ambienti di analisi scientifica dei dati utilizzata dal hello Cortana Analitica processo (CAP).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse Azure Machine Learning Studio, è necessario toohave un'area di lavoro di Machine Learning. L'area di lavoro contiene strumenti hello necessari toocreate, gestire e pubblicare esperimenti.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate un'area di lavoro
1. Accedi toohello [portale di Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign in e creare un'area di lavoro, è necessario toobe amministratore della sottoscrizione di Azure. 
    >
    > 

2. Fare clic su **+Nuovo**

3. Selezionare **Intelligence e analisi**, fare clic su **Area di lavoro di Machine Learning** e quindi su **Crea**

4. Immettere le informazioni sull'area di lavoro

    - Hello *nome area di lavoro* può essere up too260 caratteri, che non terminano in uno spazio. nome di Hello non può includere i seguenti caratteri:`< > * % & : \ ? + /`
    - Hello *il piano di servizio web* si sceglie (o creare), insieme a hello associata *tariffario* seleziona, verrà utilizzata se si distribuiscono servizi web dall'area di lavoro.

    ![Creazione di una nuova area di lavoro](media/machine-learning-create-workspace/create-new-workspace.png)

5. Fare clic su **Crea**

Dopo aver distribuito l'area di lavoro hello, è possibile aprirlo in Machine Learning Studio.

1. Sfoglia tooMachine Learning Studio a [https://studio.azureml.net/](https://studio.azureml.net/).

2. Selezionare l'area di lavoro nell'angolo superiore a destra di hello.

    ![Selezionare l'area di lavoro](media/machine-learning-create-workspace/open-workspace.png)

3. Fare clic su **esperimenti personali**.

    ![Aprire gli esperimenti](media/machine-learning-create-workspace/my-experiments.png)

Per informazioni sulla gestione dell'area di lavoro, vedere [Gestire un'area di lavoro di Azure Machine Learning](machine-learning-manage-workspace.md).
Se si verifica un problema durante la creazione dell'area di lavoro, vedere [Troubleshooting guide: creare e collegare l'area di lavoro Machine Learning tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Condivisione di un'area di lavoro di Azure Machine Learning
Dopo aver creato un'area di lavoro di Machine Learning, è possibile invitare utenti tooyour dell'area di lavoro tooshare accesso tooyour dell'area di lavoro e tutti i relativi esperimenti, set di dati, blocchi appunti e così via. È possibile aggiungere gli utenti in due ruoli:

* **Utente** -un utente dell'area di lavoro può creare, aprire, modificare ed eliminare gli esperimenti, set di dati, e così via. nell'area di lavoro hello.
* **Proprietario** : possibile invitare un proprietario e rimuovere gli utenti nell'area di lavoro hello in toowhat inoltre un utente possono eseguire.

> [!NOTE]
> account amministratore Hello Crea area di lavoro hello viene automaticamente aggiunto toohello dell'area di lavoro come proprietario dell'area di lavoro. Tuttavia, altri amministratori o utenti in sottoscrizione non sono automaticamente concesso l'accesso toohello dell'area di lavoro, è necessario tooinvite loro in modo esplicito.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare un'area di lavoro

1. Accedi tooMachine Learning Studio a [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. Nel riquadro sinistro di hello, fare clic su **impostazioni**

3. Fare clic su hello **utenti** scheda

4. Fare clic su **INVITARE utenti più** nella parte inferiore di hello della pagina hello

    ![Impostazioni di Studio](media/machine-learning-create-workspace/settings.png)

5. Immettere uno o più indirizzi di posta elettronica. gli utenti di Hello è necessario un account Microsoft valido o un account aziendale (da Azure Active Directory).

6. Selezionare se si desidera che gli utenti di hello tooadd come proprietario o l'utente.

7. Fare clic su hello **OK** segno di spunta.

Ogni utente che si aggiunge un messaggio e-mail con le istruzioni su come area di lavoro è condivisa in toohello toosign.

> [!NOTE]
> Per gli utenti toobe in grado di toodeploy o gestire servizi web nell'area di lavoro, devono essere Collaboratore o amministratore di hello sottoscrizione di Azure. 



