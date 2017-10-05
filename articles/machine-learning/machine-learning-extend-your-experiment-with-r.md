---
title: Estendere l'esperimento con R | Microsoft Docs
description: "Come estendere le funzionalità di Azure Machine Learning Studio tramite il linguaggio R usando il modulo Execute R Script."
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
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="1017b-103">Estendere l'esperimento con R</span><span class="sxs-lookup"><span data-stu-id="1017b-103">Extend your experiment with R</span></span>
<span data-ttu-id="1017b-104">È possibile estendere le funzionalità di Azure Machine Learning Studio tramite il linguaggio R usando il modulo [Execute R Script][execute-r-script].</span><span class="sxs-lookup"><span data-stu-id="1017b-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="1017b-105">Questo modulo accetta più set di dati di input e produce un singolo set di dati come output.</span><span class="sxs-lookup"><span data-stu-id="1017b-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="1017b-106">È possibile digitare uno script R nel parametro **R Script** del modulo [Execute R Script][execute-r-script] (Esegui script R).</span><span class="sxs-lookup"><span data-stu-id="1017b-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="1017b-107">Per accedere a ogni porta di input del modulo, usare codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="1017b-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="1017b-108">Elenco di tutti i pacchetti installati attualmente</span><span class="sxs-lookup"><span data-stu-id="1017b-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="1017b-109">L'elenco dei pacchetti installati può cambiare.</span><span class="sxs-lookup"><span data-stu-id="1017b-109">The list of installed packages can change.</span></span> <span data-ttu-id="1017b-110">Un elenco dei pacchetti attualmente installati è disponibile in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx) (Pacchetti R supportati da Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="1017b-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="1017b-111">Per ottenere l'elenco completo e aggiornato dei pacchetti installati, immettere il codice seguente nel modulo [Execute R Script][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="1017b-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="1017b-112">In questo modo l'elenco dei pacchetti viene inviato alla porta di output del modulo [Execute R Script][execute-r-script] (Esegui script R).</span><span class="sxs-lookup"><span data-stu-id="1017b-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="1017b-113">Per visualizzare l'elenco di pacchetti, connettere un modulo di conversione, ad esempio [Convert to CSV][convert-to-csv] (Converti in CSV) all'output di sinistra del modulo [Execute R Script][execute-r-script] (Esegui script R), eseguire l'esperimento, quindi fare clic sull'output del modulo di conversione e selezionare **Download**.</span><span class="sxs-lookup"><span data-stu-id="1017b-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

![Scaricare l'output del modulo "Convert to CSV" (Converti in CSV)](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="1017b-115">Importazione di pacchetti</span><span class="sxs-lookup"><span data-stu-id="1017b-115">Importing packages</span></span>
<span data-ttu-id="1017b-116">Per importare i pacchetti non ancora installati, è possibile usare i comandi seguenti nel modulo [Execute R Script][execute-r-script]:</span><span class="sxs-lookup"><span data-stu-id="1017b-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="1017b-117">Il file `my_favorite_package.zip` contiene il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1017b-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
