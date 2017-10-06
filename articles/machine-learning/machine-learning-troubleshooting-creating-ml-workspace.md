---
title: 'Risolvere i problemi: Creare e collegare l''area di lavoro Machine Learning tooa | Documenti Microsoft'
description: Soluzioni ai problemi comuni per la creazione e la connessione dell'area di lavoro di tooan Azure Machine Learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Guida alla risoluzione dei problemi: creare e collegare l'area di lavoro Machine Learning tooan
Questa guida offre soluzioni per alcuni problemi frequenti relativi alla configurazione di aree di lavoro di Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Proprietario dell'area di lavoro
tooopen un'area di lavoro in Machine Learning Studio, è necessario essere connessi toohello Account Microsoft è stato usato area hello toocreate oppure è necessario un invito dall'area di lavoro di hello proprietario toojoin hello tooreceive. Dal portale di Azure è possibile gestire hello hello area di lavoro che include l'accesso tooconfigure possibilità di hello.

Per altre informazioni sulla gestione di un'area di lavoro, vedere [Gestire un'area di lavoro di Azure Machine Learning].

[Gestire un'area di lavoro di Azure Machine Learning]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Aree geografiche disponibili
Machine Learning è attualmente disponibile in un numero limitato di aree. Se la sottoscrizione non include una di queste aree, verrà visualizzato il messaggio di errore hello, "Si sono presenti sottoscrizioni nelle consentiti aree hello."

toorequest da un'area aggiunto tooyour sottoscrizione, creare una nuova richiesta di supporto Microsoft dal portale di Azure hello scegliere **fatturazione** come tipo di problema hello e seguire hello richiede toosubmit la richiesta.

## <a name="storage-account"></a>Account di archiviazione
Hello servizio Machine Learning è necessario un toostore dati dell'account di archiviazione. È possibile utilizzare un account di archiviazione esistente o quando si crea l'area di lavoro Machine Learning nuovo hello (se si dispone di quota toocreate un nuovo account di archiviazione), è possibile creare un nuovo account di archiviazione.

Dopo aver creato l'area di lavoro Machine Learning nuovo hello, per accedere tooMachine Learning Studio usando account Microsoft hello che dell'area di lavoro di toocreate hello è stato utilizzato. Se viene visualizzato il messaggio di errore hello, "Area di lavoro non trovato" (toohello simile seguente schermata), utilizzare hello seguendo i passaggi toodelete i cookie del browser.

![Area di lavoro non trovata][screen3]

**cookie del browser toodelete**

1. Se si utilizza Internet Explorer, fare clic su hello **strumenti** nell'angolo superiore destro hello e selezionare **Opzioni Internet**.  

![Opzioni Internet][screen4]

2. In hello **generale** scheda, fare clic su **eliminare...**

![Generale][screen5]

3. In hello **Elimina cronologia esplorazioni** finestra di dialogo verificare **cookie e dati del sito Web** sia selezionata e fare clic su **eliminare**.

![Eliminare i cookie][screen6]

Dopo l'eliminazione dei cookie hello, riavviare il browser hello e quindi passare toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) pagina. Quando viene chiesto di immettere un nome utente e una password, hello stesso account Microsoft usato dell'area di lavoro di toocreate hello.

## <a name="comments"></a>Commenti

L'obiettivo è toomake hello esperienza di Machine Learning più semplice possibile. Inviare eventuali commenti e i problemi in hello [forum di Azure Machine Learning](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp a un servizio migliore.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
