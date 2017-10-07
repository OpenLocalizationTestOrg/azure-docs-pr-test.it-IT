---
title: 'Passaggio 2: Caricare dati in un esperimento di Machine Learning | Documentazione Microsoft'
description: 'Passaggio 2 di hello sviluppare una procedura dettagliata soluzione predittiva: caricamento archiviati dati pubblici in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 0ea21dcca2d0934ed06508560cf85cf31b48ce6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a>Passaggio 2 della procedura dettagliata: Caricare dati esistenti in un esperimento di Azure Machine Learning
Questo è hello secondo passaggio della procedura dettagliata hello [sviluppare una soluzione analitica predittiva in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Creare un'area di lavoro di Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. **Caricare i dati esistenti**
3. [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Eseguire il training e valutare i modelli di hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Distribuzione di servizio Web hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Accedere al servizio Web hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
toodevelop un modello predittivo per rischio di credito, è necessario che i dati che è possibile utilizzare tootrain e quindi testare il modello di hello. Per questa procedura dettagliata, verrà utilizzata dal repository UC Irvine Machine Learning hello hello "Set di dati UCI Statlog (tedesco credito dati)". disponibile al seguente indirizzo:  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

Si userà il file hello denominato **german.data**. Scaricare questo file tooyour disco rigido locale.  

Hello **german.data** set di dati contiene righe di 20 variabili per 1000 ultimi candidati per la carta di credito. Queste 20 variabili rappresentano il set di hello del set di funzionalità (hello *vettore di funzione*), che fornisce le caratteristiche di identificazione per ciascun candidato di carta di credito. Una colonna aggiuntiva in ogni riga rappresenta il rischio di credito calcolata del candidato hello, con i 700 candidati identificati come un rischio di credito bassa e 300 come un rischio elevato.

sito UCI Hello fornisce una descrizione degli attributi di hello del vettore di funzione hello per questi dati. Questo include informazioni finanziarie, storico dei crediti, stato di occupazione e dati personali. Per ogni richiedente è stata assegnata una valutazione in formato binario per indicare se è a basso o ad alto rischio. 

Verrà utilizzata questa tootrain dati un modello predittivo analitica. Al termine, il modello deve essere in grado di tooaccept un vettore di funzione per un nuovo utente e stimare se è un rischio di credito low o high.  

Ma ecco un'interessante svolta. Hello descrizione del set di dati di hello in menziona sito UCI di hello comportano anche costi se si misclassify il rischio di credito di una persona.
Se il modello di hello viene stimato un rischio elevato per un utente che è effettivamente un rischio di credito bassa, il modello di hello ha una classificazione non corretta.
Ma classificazione non corretta inversa hello è cinque volte più costosa istituto toohello: se il modello di hello viene stimato un rischio di credito insufficiente per un utente che è effettivamente un rischio elevato.

In tal caso, è necessario tootrain il nostro modello in modo che il costo di hello di questo tipo di classificazione non corretta di quest'ultimo è cinque volte superiore interpretata hello altro modo.
Un modo semplice toodo questo modello hello nell'esperimento di training quando è duplicando (cinque volte) le voci che rappresentano un utente con un rischio elevato. Quindi, se il modello di hello interpreta come un rischio di credito insufficiente quando sono in realtà un rischio elevato, hello modello non tale classificazione non corretta stesso cinque volte, una volta per ogni elemento duplicato. Si aumenterà il costo di hello di questo errore nei risultati di training hello.


## <a name="convert-hello-dataset-format"></a>Convertire il formato di set di dati hello
set di dati originale Hello utilizza un formato delimitato da spazio vuoto. Machine Learning Studio funziona meglio con un valore delimitato da virgole (CSV), quindi verrà convertito hello dataset sostituendo gli spazi con virgole.  

Esistono molti modi tooconvert questi dati. Un modo consiste nell'utilizzare hello comando di Windows PowerShell seguente:   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

È inoltre possibile utilizzare hello Unix sed comando:  

    sed 's/ /,/g' german.data > german.csv  

In entrambi i casi, è stata creata una versione delimitato da virgole dei dati di hello in un file denominato **german.csv** che è possibile utilizzare nell'esperimento.

## <a name="upload-hello-dataset-toomachine-learning-studio"></a>Caricare set di dati di hello tooMachine Learning Studio
Dopo aver convertito tooCSV formato dati hello, dobbiamo tooupload in Machine Learning Studio. 

1. Home page di hello aprire Machine Learning Studio ([https://studio.azureml.net](https://studio.azureml.net)). 

2. Fare clic sul menu hello ![Menu][1] hello superiore sinistro della finestra hello, fare clic su **Azure Machine Learning**selezionare **Studio**ed eseguire l'accesso.

3. Fare clic su **+ nuovo** nella parte inferiore di hello della finestra hello.

4. Selezionare **DATASET**.

5. Selezionare **FROM LOCAL FILE**.

    ![Aggiungere un set di dati da un file locale][2]

6. In hello **caricare un nuovo set di dati** finestra di dialogo, fare clic su **Sfoglia** e trovare hello **german.csv** file creato.

7. Immettere un nome per set di dati hello. Per questa procedura, il nome sarà "UCI German Credit Card Data".

8. Come tipo di dati selezionare **Generic CSV File With no header (.nh.csv)**.

9. Aggiungere un'eventuale descrizione.

10. Fare clic su hello **OK** segno di spunta.  

    ![Caricare set di dati hello][3]

Consente di caricare dati hello in un modulo di set di dati che è possibile utilizzare in un esperimento.

È possibile gestire i set di dati che è stato caricato tooStudio facendo hello **set di dati** toohello scheda a sinistra della finestra Studio hello.

![Gestire i set di dati][4]

Per altre informazioni sull'importazione di altri tipi di dati in un esperimento, vedere [Importare dati di training in Azure Machine Learning Studio](machine-learning-data-science-import-data.md).

**Passaggi successivi: [Creare un nuovo esperimento](machine-learning-walkthrough-3-create-new-experiment.md)**

[1]: media/machine-learning-walkthrough-2-upload-data/menu.png
[2]: media/machine-learning-walkthrough-2-upload-data/add-dataset.png
[3]: media/machine-learning-walkthrough-2-upload-data/upload-dataset.png
[4]: media/machine-learning-walkthrough-2-upload-data/dataset-list.png
