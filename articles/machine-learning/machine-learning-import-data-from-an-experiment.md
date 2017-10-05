---
title: Importare i dati in Azure Machine Learning Studio da un altro esperimento | Microsoft Docs
description: Come salvare i dati di training in Azure Machine Learning Studio e utilizzarli in un altro esperimento.
keywords: dati di importazione, dati,origini dati,dati di training
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 7da9dcec-5693-4bb6-8166-15904e7f75c3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: ecfa2110d0d51511ceb5bd07b730732ecfa2e9e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-data-into-azure-machine-learning-studio-from-another-experiment"></a><span data-ttu-id="11e1f-104">Importare i dati in Azure Machine Learning Studio da un altro esperimento</span><span class="sxs-lookup"><span data-stu-id="11e1f-104">Import your data into Azure Machine Learning Studio from another experiment</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="11e1f-105">Talvolta si vuole ottenere un risultato intermedio da un esperimento e usare tale risultato come parte di un altro esperimento.</span><span class="sxs-lookup"><span data-stu-id="11e1f-105">There will be times when you'll want to take an intermediate result from one experiment and use it as part of another experiment.</span></span> <span data-ttu-id="11e1f-106">A tale scopo, si salva il modulo come un set di dati:</span><span class="sxs-lookup"><span data-stu-id="11e1f-106">To do this, you save the module as a dataset:</span></span>

1. <span data-ttu-id="11e1f-107">Fare clic sull'output del modulo da salvare come set di dati.</span><span class="sxs-lookup"><span data-stu-id="11e1f-107">Click the output of the module that you want to save as a dataset.</span></span>
2. <span data-ttu-id="11e1f-108">Fare clic su **Salva come set di dati**.</span><span class="sxs-lookup"><span data-stu-id="11e1f-108">Click **Save as Dataset**.</span></span>
3. <span data-ttu-id="11e1f-109">Quando richiesto, immettere un nome e una descrizione che consentiranno di identificare facilmente il set di dati.</span><span class="sxs-lookup"><span data-stu-id="11e1f-109">When prompted, enter a name and a description that would allow you to identify the dataset easily.</span></span>
4. <span data-ttu-id="11e1f-110">Fare clic sul segno di spunta **OK** .</span><span class="sxs-lookup"><span data-stu-id="11e1f-110">Click the **OK** checkmark.</span></span>

<span data-ttu-id="11e1f-111">Al termine del salvataggio, il set di dati sarà disponibile per l'uso in qualsiasi esperimento dell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="11e1f-111">When the save finishes, the dataset will be available for use within any experiment in your workspace.</span></span> <span data-ttu-id="11e1f-112">È possibile individuarlo nell’elenco **Set di dati salvati** nella tavolozza dei moduli.</span><span class="sxs-lookup"><span data-stu-id="11e1f-112">You can find it in the **Saved Datasets** list in the module palette.</span></span>

