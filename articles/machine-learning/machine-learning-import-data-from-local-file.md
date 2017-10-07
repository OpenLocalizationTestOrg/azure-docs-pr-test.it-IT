---
title: aaaImport dati da un file in Azure Machine Learning Studio | Documenti Microsoft
description: Informazioni su come il tooAzure rigido Machine Learning Studio file tooupload dati di training. Consente di creare un modulo di set di dati nell'area di lavoro hello.
keywords: dati di importazione, formato dati, tipi di dati, origini dati, dati di training
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>Importare dati di training da un file sul disco rigido in Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

Informazioni su come tooupload un tipo di dati di file da toouse il disco rigido come dati di training in Azure Machine Learning Studio. Tramite l'importazione di file di dati hello, si dispone di un modulo di set di dati pronto per l'utilizzo nell'area di lavoro.

## <a name="steps-tooimport-data-from-a-local-file"></a>Dati tooimport i passaggi da un file locale
tooimport dati da un disco rigido locale, hello seguenti:

1. Fare clic su **+ nuovo** nella parte inferiore di hello della finestra di Machine Learning Studio hello.
2. Selezionare **DATASET** (SET DI DATI) e **FROM LOCAL FILE** (DA FILE LOCALE).
3. In hello **caricare un nuovo set di dati** finestra di dialogo Sfoglia toohello file da tooupload
4. Immettere un nome, identificare il tipo di dati hello e immettere facoltativamente una descrizione. È consigliabile una descrizione: consente toorecord qualsiasi caratteristica sui dati hello che si desidera tooremember quando si utilizzano dati hello in futuro hello.
5. casella di controllo di Hello **si tratta hello nuova versione di un set di dati esistente** consente tooupdate un set di dati esistente con nuovi dati. Fare clic su questa casella di controllo e quindi immettere il nome di hello di un set di dati esistente.

![Caricare un nuovo set di dati](media/machine-learning-import-data-from-local-file/upload-dataset.png)

Durante il caricamento, verrà visualizzato un messaggio che indica che il file è in fase di caricamento. Caricare tempo dipende dalle dimensioni hello la velocità di hello e dati del servizio toohello connessione. Se si conosce il file hello richiederà molto tempo, è possibile eseguire altre operazioni all'interno di Machine Learning Studio durante l'attesa. Tuttavia, chiudere il browser hello determina toofail di caricamento dati hello.

## <a name="dataset-module-is-ready-for-use"></a>Il modulo set di dati è pronto per l'utilizzo
Dopo aver caricati i dati, viene archiviato in un modulo di set di dati e viene esperimento tooany disponibile nell'area di lavoro.

Quando si modifica un esperimento, è possibile trovare hello set di dati sono stati creati in hello **set di dati personali** elenco hello **Saved Datasets** elenco tavolozza modulo hello. È possibile trascinare e rilasciare hello set di dati nell'area di disegno esperimento hello quando si desidera toouse hello set di dati per un'ulteriore analitica e machine learning.
