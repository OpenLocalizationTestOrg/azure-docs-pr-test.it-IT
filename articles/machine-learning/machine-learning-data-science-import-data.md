---
title: dati aaaImport in Machine Learning Studio | Documenti Microsoft
description: Come tooimport i dati in Azure Machine Learning Studio di varie origini dati. Informazioni sui tipi di dati e i formati di dati supportati.
keywords: dati di importazione,formato dati,tipi di dati,origini dati,dati di training
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importare dati di training in Azure Machine Learning Studio da varie origini dati
toouse i propri dati in Machine Learning Studio toodevelop e train una soluzione analitica predittiva, è possibile: 

* caricare i dati da un **file locale** avanti rispetto ora da toocreate il disco rigido di un modulo di set di dati nell'area di lavoro
* accedere ai dati da uno dei diversi **le origini dati online** durante l'esecuzione dell'esperimento usando hello [l'importazione dei dati] [ import-data] modulo 
* Usare i dati da un altro **esperimento** di Azure Machine Learning salvato come un set di dati.
* Usare i dati da un **database di SQL Server** locale

Ognuna di queste opzioni è descritta in uno degli argomenti hello menu hello riportato di seguito. Questi argomenti illustrano come tooimport dati da queste varie origini toouse in Machine Learning Studio. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> In Machine Learning Studio sono disponibili numerosi set di dati di esempio che è possibile usare per questo scopo. Per informazioni, vedere [utilizzare set di dati di esempio hello in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).
> 
> 

In questo argomento introduttivo, inoltre, viene descritto l'utilizzo in Machine Learning Studio tooget dati pronti per e descrive quali i formati di dati e tipi di dati sono supportati. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Preparare i dati da usare in Azure Machine Learning Studio
Machine Learning Studio è progettato toowork con i dati tabulari o rettangolari, ad esempio i dati di testo delimitato o strutturato i dati da un database, anche se in alcuni casi potrebbero essere utilizzati dati non rettangolari.

È consigliabile che i dati siano relativamente puliti. Tootake cure problemi, ad esempio stringhe non racchiusi tra virgolette, è necessario prima di caricare dati hello nell'esperimento.

In Machine Learning Studio sono tuttavia disponibili moduli che consentono di eseguire alcune modifiche dei dati all'interno dell'esperimento. A seconda di algoritmi di machine learning hello userai, potrebbe essere necessario come toodecide gestire problemi strutturali di dati, ad esempio i valori mancanti e i dati di tipo sparse e sono disponibili i moduli che possono risultare utili che. Cerca in hello **Data Transformation** sezione della tavolozza modulo hello per i moduli che queste funzioni.

In qualsiasi momento nell'esperimento, è possibile visualizzare o scaricare dati hello sono prodotto da un modulo, fare clic sulla porta di output di hello. In base al modulo hello, opzioni di download diversi potrebbero essere disponibili, o è in grado di toovisualize hello dati all'interno del browser in Machine Learning Studio.

## <a name="data-formats-and-data-types-supported"></a>Tipi di dati e formati di dati supportati
È possibile importare un numero di tipi di dati nell'esperimento, a seconda di quale meccanismo è utilizzare dati tooimport e dove provengono da:

* Testo normale (con estensione txt)
* Valori delimitati da virgole (CSV) con un'intestazione (con estensione csv) o senza intestazione (con estensione nh.csv)
* Valori separati da tabulazioni (TSV) con un'intestazione (con estensione tsv) o senza intestazione (con estensione nh.tsv)
* File di Excel
* Tabella di Azure
* Tabella Hive
* Tabella di database SQL
* Valori OData
* Dati SVMLight (.svmlight) (vedere hello [SVMLight definizione](http://svmlight.joachims.org/) informazioni di formato)
* Dati di relazione File formato ARFF () (.arff) dell'attributo (vedere hello [definizione ARFF](http://weka.wikispaces.com/ARFF) informazioni di formato)
* File ZIP (con estensione zip)
* File dell’oggetto o dell'area di lavoro R (con estensione RData)

Se si importano dati in un formato quale ARFF che include i metadati, Machine Learning Studio Usa questa voce di metadati toodefine hello e tipo di dati di ogni colonna.

Se si importano dati, ad esempio il formato TSV o CSV che non include i metadati, Machine Learning Studio deduce il tipo di dati hello per ogni colonna tramite il campionamento dei dati di hello. Se i dati di hello non dispone anche di intestazioni di colonna, Machine Learning Studio fornisce i nomi predefiniti.

È possibile in modo esplicito specificare o modificare tipi di dati e le intestazioni di hello per le colonne utilizzando hello [Modifica metadati][edit-metadata].

esempio Hello **tipi di dati** sono riconosciuti da Machine Learning Studio:

* String
* Integer
* Double
* Boolean
* DateTime
* TimeSpan

Machine Learning Studio Usa un tipo di dati interno denominato ***tabella dati*** toopass dati tra i moduli. È possibile convertire in modo esplicito i dati in formato tabella di dati utilizzando hello [convertire tooDataset] [ convert-to-dataset] modulo.

Tutti i moduli che accetta i formati diversi da tabella dati convertirà automaticamente hello dati tooData tabella prima di passarlo toohello successivo modulo.

Se necessario, è possibile convertire il formato Tabella dati in CSV, TSV, ARFF o SVMLight usando altri moduli di conversione.
Cerca in hello **Data Format Conversions** sezione della tavolozza modulo hello per i moduli che queste funzioni.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
