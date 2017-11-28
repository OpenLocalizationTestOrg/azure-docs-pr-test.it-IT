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
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="077d5-103">Estendere l'esperimento con R</span><span class="sxs-lookup"><span data-stu-id="077d5-103">Extend your experiment with R</span></span>
<span data-ttu-id="077d5-104">È possibile estendere le funzionalità di hello di Azure Machine Learning Studio attraverso il linguaggio R hello utilizzando hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="077d5-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="077d5-105">Questo modulo accetta più set di dati di input e produce un singolo set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="077d5-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="077d5-106">È possibile digitare uno script R in hello **Script R** parametro di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="077d5-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="077d5-107">Ogni porta di input del modulo hello è accedere usando codice simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="077d5-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="077d5-108">Elenco di tutti i pacchetti installati attualmente</span><span class="sxs-lookup"><span data-stu-id="077d5-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="077d5-109">può modificare l'elenco di Hello dei pacchetti installati.</span><span class="sxs-lookup"><span data-stu-id="077d5-109">hello list of installed packages can change.</span></span> <span data-ttu-id="077d5-110">Un elenco dei pacchetti attualmente installati è disponibile in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Pacchetti R supportati da Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="077d5-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="077d5-111">È anche possibile ottenere hello completo, corrente elenco dei pacchetti installati tramite l'immissione di hello seguente di codice in hello [Execute R Script] [ execute-r-script] modulo:</span><span class="sxs-lookup"><span data-stu-id="077d5-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="077d5-112">Consente di inviare l'elenco di hello pacchetti toohello porta di output di hello [Execute R Script] [ execute-r-script] modulo.</span><span class="sxs-lookup"><span data-stu-id="077d5-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="077d5-113">pacchetto di hello tooview elenco, collegare un modulo di conversione, ad esempio [convertire tooCSV] [ convert-to-csv] toohello a sinistra di output di hello [Execute R Script] [ execute-r-script]modulo, eseguire l'esperimento hello, quindi fare clic su output di hello del modulo di conversione hello e selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="077d5-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![Scaricare l'output del modulo di "Convertire tooCSV"](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="077d5-115">Importazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="077d5-115">Importing packages</span></span>
<span data-ttu-id="077d5-116">È possibile importare pacchetti che non sono già installati utilizzando i seguenti comandi di hello hello [Execute R Script] [ execute-r-script] modulo:</span><span class="sxs-lookup"><span data-stu-id="077d5-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="077d5-117">in cui hello `my_favorite_package.zip` file contiene il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="077d5-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
