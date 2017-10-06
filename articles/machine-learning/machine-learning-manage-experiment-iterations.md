---
title: aaaManage sperimentare le iterazioni in Machine Learning Studio | Documenti Microsoft
description: Come toomanage sperimentare le iterazioni in Azure Machine Learning Studio
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>Gestire iterazioni dell'esperimento in Azure Machine Learning Studio
Sviluppo di un modello di analisi predittiva è un processo iterativo - durante la modifica di hello diverse funzioni e parametri dell'esperimento, eseguire la convergenza i risultati fino a quando non si è soddisfatti di disporre di un modello con training ed efficace. Chiave toothis processo è hello di rilevamento diverse iterazioni ai parametri di sperimentazione e alle configurazioni.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

È possibile esaminare le esecuzioni precedenti degli esperimenti in qualsiasi momento nell'ordine toochallenge, rivedere e infine confermare o ridefinire i presupposti precedenti. Quando si esegue un esperimento, Machine Learning Studio mantiene una cronologia di hello eseguire, tra cui set di dati, modulo e le connessioni di porta e i parametri. Questa cronologia acquisisce anche i risultati, le informazioni di runtime come l'ora di inizio e di fine, i messaggi di log e lo stato dell'esecuzione. È possibile esaminare nuovamente uno di questi viene eseguito in qualsiasi ordine cronologico hello tooreview di fase di sperimentazione e i risultati intermedi. È anche possibile utilizzare un'esecuzione precedente del toolaunch esperimento in una nuova fase della richiesta e l'individuazione sul percorso toocreating semplice, complessi o anche insieme soluzioni di modellazione.

> [!NOTE]
> Quando si visualizza un'esecuzione precedente di un esperimento, la versione di prova hello è bloccata e non può essere modificata. È possibile, tuttavia, salvare una copia facendo **SAVE AS** e fornendo un nuovo nome per la copia di hello. Machine Learning Studio apre hello nuova copia, è quindi possibile modificare ed eseguire. Questa copia dell'esperimento è disponibile in hello **ESPERIMENTI** elenco insieme a tutti gli altri esperimenti.
> 
> 

## <a name="viewing-hello-prior-run"></a>Visualizzazione hello eseguire precedente
Dopo aver aperto esperimento che è stata eseguita almeno una volta, è possibile visualizzare hello precedente esecuzione dell'esperimento hello facendo **eseguire precedente** nel riquadro Proprietà hello.

Si supponga ad esempio di creare un esperimento e di eseguirne tre versioni, alle 11:23, alle 11:42 e alle 11:55. Se si apre ultima esecuzione di hello dell'esperimento hello (11:55) e fare clic su **eseguire precedente**, apertura di una versione di hello è stato eseguito a 11:42.

## <a name="viewing-hello-run-history"></a>Hello di visualizzazione della cronologia di esecuzione
È possibile visualizzare tutte le esecuzioni precedenti hello dell'esperimento facendo **Visualizza cronologia di esecuzione** in un esperimento aperto.

Ad esempio, si supponga di crea un esperimento con hello [Linear Regression] [ linear-regression] modulo e si desidera l'effetto di hello tooobserve di modifica del valore hello **velocità di apprendimento** in i risultati dell'esperimento. Eseguire esperimento hello più volte con valori diversi per questo parametro, come indicato di seguito:

| Valore di Learning rate | Ora di inizio dell'esecuzione |
| --- | --- |
| 0,1 |11/9/2014 16:18:58 |
| 0,2 |11/9/2014 16:24:33 |
| 0,4 |11/9/2014 16:28:36 |
| 0,5 |11/9/2014 16:33:31 |

Se si fa clic su **VIEW RUN HISTORY**, verrà visualizzato un elenco di tutte le esecuzioni:

![Esempio di cronologia delle esecuzioni][runhistory]

Fare clic su uno di questi tooview viene eseguito uno snapshot di hello sperimentare in fase di hello è stato eseguito. Hello configurazione, i valori dei parametri, i commenti e i risultati vengono mantenuti tutti toogive è un record completo di tale esecuzione dell'esperimento.

> [!TIP]
> toodocument le iterazioni dell'esperimento hello, è possibile modificare il titolo di hello ogni esecuzione, è possibile aggiornare hello **riepilogo** di hello sperimentare nel riquadro Proprietà hello ed è possibile aggiungere o aggiornare i commenti su singoli moduli toorecord le modifiche. commenti di titolo e riepilogo modulo Hello vengono salvati con ogni esecuzione dell'esperimento hello.
> 
> 

elenco di Hello degli esperimenti in hello **ESPERIMENTI** scheda in Machine Learning Studio visualizza sempre hello l'ultima versione di un esperimento. Se si apre un'esecuzione precedente di sperimentazione hello (utilizzando **eseguire precedente** o **Visualizza cronologia di esecuzione**), è possibile restituire una versione bozza toohello facendo **Visualizza cronologia di esecuzione** e selezionando Hello iterazione con un **stato** di **Editable**.

## <a name="iterating-on-a-previous-run"></a>Iterazione dell'esecuzione precedente 
Se si fa clic su **Prior Run** (Esecuzione precedente) o **VIEW RUN HISTORY** (VISUALIZZA CRONOLOGIA DI ESECUZIONE) e si apre un'esecuzione precedente, è possibile visualizzare un esperimento completato in modalità di sola lettura.

Se si desidera toobegin un'iterazione dell'esperimento a partire da modo hello è configurato per un'esecuzione precedente, è possibile farlo hello aprendo Esegui e facendo clic su **SAVE AS**. Verrà creato un esperimento di nuovo con un nuovo titolo, una cronologia di esecuzione vuota e tutti i componenti di hello e i valori dei parametri di hello precedente esecuzione. Questo nuovo esperimento è elencato nella hello **ESPERIMENTI** scheda home page di Machine Learning Studio hello ed è possibile modificare ed eseguirlo, avviare un nuovo eseguire cronologia per l'iterazione dell'esperimento. 

Ad esempio, si supponga esperimento hello illustrata nella sezione precedente hello cronologia di esecuzione. Si desidera tooobserve cosa accade quando si imposta hello **velocità di apprendimento** parametro too0.4 e provare diversi valori per hello **numero di periodi di formazione** parametro.

1. Fare clic su **Visualizza cronologia di esecuzione** e aprire iterazione hello dell'esperimento hello che è stato eseguito alle 4:28:36 pm (in cui vengono impostati too0.4 valore di parametro hello).
2. Fare clic su **SAVE AS**.
3. Immettere il nuovo titolo e fare clic su hello **OK** segno di spunta. Viene creata una nuova copia dell'esperimento hello.
4. Modificare hello **numero di periodi di formazione** parametro.
5. Fare clic su **RUN**.

È ora possibile continuare toomodify ed eseguire questa versione di esperimento, la creazione di un nuovo toorecord cronologia di esecuzione del lavoro.

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
