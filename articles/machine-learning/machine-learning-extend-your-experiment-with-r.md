---
title: aaaExtend l'esperimento con R | Documenti Microsoft
description: "Tooextend hello come funzionalità di Azure Machine Learning Studio mediante il linguaggio R hello tramite modulo Execute R Script hello."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a>Estendere l'esperimento con R
È possibile estendere le funzionalità di hello di Azure Machine Learning Studio attraverso il linguaggio R hello utilizzando hello [Execute R Script] [ execute-r-script] modulo.

Questo modulo accetta più set di dati di input e produce un singolo set di dati come output. È possibile digitare uno script R in hello **Script R** parametro di hello [Execute R Script] [ execute-r-script] modulo.

Ogni porta di input del modulo hello è accedere usando codice simile toohello seguenti:

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a>Elenco di tutti i pacchetti installati attualmente
può modificare l'elenco di Hello dei pacchetti installati. Un elenco dei pacchetti attualmente installati è disponibile in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Pacchetti R supportati da Azure Machine Learning).

È anche possibile ottenere hello completo, corrente elenco dei pacchetti installati tramite l'immissione di hello seguente di codice in hello [Execute R Script] [ execute-r-script] modulo:

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

Consente di inviare l'elenco di hello pacchetti toohello porta di output di hello [Execute R Script] [ execute-r-script] modulo.
pacchetto di hello tooview elenco, collegare un modulo di conversione, ad esempio [convertire tooCSV] [ convert-to-csv] toohello a sinistra di output di hello [Execute R Script] [ execute-r-script]modulo, eseguire l'esperimento hello, quindi fare clic su output di hello del modulo di conversione hello e selezionare **scaricare**. 

![Scaricare l'output del modulo di "Convertire tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a>Importazione di pacchetti
È possibile importare pacchetti che non sono già installati utilizzando i seguenti comandi di hello hello [Execute R Script] [ execute-r-script] modulo:

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

in cui hello `my_favorite_package.zip` file contiene il pacchetto.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
