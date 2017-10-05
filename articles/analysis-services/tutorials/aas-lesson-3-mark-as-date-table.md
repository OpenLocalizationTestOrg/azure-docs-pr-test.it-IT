---
title: 'Esercitazione su Azure Analysis Services - Lezione 3: Contrassegnare come tabella data | Microsoft Docs'
description: Descrive come contrassegnare una tabella data nel progetto per l'esercitazione su Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: c62f2726fef5219155a08b70c61162c914600d1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-3-mark-as-date-table"></a><span data-ttu-id="b5735-103">Lezione 3: Contrassegnare come tabella data</span><span class="sxs-lookup"><span data-stu-id="b5735-103">Lesson 3: Mark as Date Table</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b5735-104">Nella lezione 2: Ottenere i dati è stata importata una tabella delle dimensioni denominata DimDate.</span><span class="sxs-lookup"><span data-stu-id="b5735-104">In Lesson 2: Get data, you imported a dimension table named DimDate.</span></span> <span data-ttu-id="b5735-105">Anche se nel modello questa tabella è denominata DimDate, è anche nota come *tabella data*, perché contiene dati di data e ora.</span><span class="sxs-lookup"><span data-stu-id="b5735-105">While in your model this table is named DimDate, it can also be known as a *Date table*, in that it contains date and time data.</span></span>  
  
<span data-ttu-id="b5735-106">Quando si usano funzioni di Business Intelligence per le gerarchie temporali DAX, è necessario specificare alcune proprietà, tra cui una *tabella data* e una *colonna data* che funge da identificatore univoco nella tabella.</span><span class="sxs-lookup"><span data-stu-id="b5735-106">Whenever you use DAX time-intelligence functions, like when you create measures later, you must specify properties which include a *Date table* and a unique identifier *Date column* in that table.</span></span>
  
<span data-ttu-id="b5735-107">In questa lezione la tabella DimDate verrà contrassegnata come *tabella data* e la colonna Date (nella tabella Date) come *colonna data* (identificatore univoco).</span><span class="sxs-lookup"><span data-stu-id="b5735-107">In this lesson, you mark the DimDate table as the *Date table* and the Date column (in the Date table) as the *Date column* (unique identifier).</span></span>  

<span data-ttu-id="b5735-108">Prima di contrassegnare la tabella data e la colonna data, è il momento di eseguire alcuni piccoli aggiustamenti per rendere il modello più facile da comprendere.</span><span class="sxs-lookup"><span data-stu-id="b5735-108">Before you mark the date table and date column, it's a good time to do a little housekeeping to make your model easier to understand.</span></span> <span data-ttu-id="b5735-109">Nella tabella DimDate è presente un colonna denominata **FullDateAlternateKey**,</span><span class="sxs-lookup"><span data-stu-id="b5735-109">Notice in the DimDate table a column named **FullDateAlternateKey**.</span></span> <span data-ttu-id="b5735-110">che contiene una riga per ogni giorno di ogni anno di calendario incluso nella tabella.</span><span class="sxs-lookup"><span data-stu-id="b5735-110">This column contains one row for every day in each calendar year included in the table.</span></span> <span data-ttu-id="b5735-111">Questa colonna viene usata molto spesso nelle formule per le misure e nei report,</span><span class="sxs-lookup"><span data-stu-id="b5735-111">You use this column a lot in measure formulas and in reports.</span></span> <span data-ttu-id="b5735-112">ma FullDateAlternateKey non è in realtà un buon identificatore per questa colonna.</span><span class="sxs-lookup"><span data-stu-id="b5735-112">But, FullDateAlternateKey isn't really a good identifier for this column.</span></span> <span data-ttu-id="b5735-113">La colonna viene rinominata **Date** per facilitarne l'identificazione e l'uso nelle formule.</span><span class="sxs-lookup"><span data-stu-id="b5735-113">You rename it to **Date**, making it easier to identify and include in formulas.</span></span> <span data-ttu-id="b5735-114">Quando possibile, è consigliabile rinominare gli oggetti, come le tabelle e le colonne, in modo che siano più facilmente identificabili in SSDT e in applicazioni client per la creazione di report, come Power BI ed Excel.</span><span class="sxs-lookup"><span data-stu-id="b5735-114">Whenever possible, it's a good idea to rename objects like tables and columns to make them easier to identify in SSDT and client reporting applications like Power BI and Excel.</span></span> 
  
<span data-ttu-id="b5735-115">Tempo previsto per il completamento della lezione: **tre minuti**</span><span class="sxs-lookup"><span data-stu-id="b5735-115">Estimated time to complete this lesson: **Three minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b5735-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b5735-116">Prerequisites</span></span>  
<span data-ttu-id="b5735-117">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="b5735-117">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b5735-118">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 2: Ottenere i dati](../tutorials/aas-lesson-2-get-data.md).</span><span class="sxs-lookup"><span data-stu-id="b5735-118">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 2: Get data](../tutorials/aas-lesson-2-get-data.md).</span></span> 

### <a name="to-rename-the-fulldatealternatekey-column"></a><span data-ttu-id="b5735-119">Per rinominare la colonna FullDateAlternateKey</span><span class="sxs-lookup"><span data-stu-id="b5735-119">To rename the FullDateAlternateKey column</span></span>

1.  <span data-ttu-id="b5735-120">Nella finestra di progettazione dei modelli fare clic sula tabella **DimDate**.</span><span class="sxs-lookup"><span data-stu-id="b5735-120">In the model designer, click the **DimDate** table.</span></span>

2.  <span data-ttu-id="b5735-121">Fare doppio clic sull'intestazione della colonna **FullDateAlternateKey** e quindi rinominarla **Date**.</span><span class="sxs-lookup"><span data-stu-id="b5735-121">Double-click the header for the **FullDateAlternateKey** column, and then rename it to **Date**.</span></span>

  
### <a name="to-set-mark-as-date-table"></a><span data-ttu-id="b5735-122">Per impostare Contrassegna come tabella data</span><span class="sxs-lookup"><span data-stu-id="b5735-122">To set Mark as Date Table</span></span>  
  
1.  <span data-ttu-id="b5735-123">Selezionare la colonna **Date** e quindi nella finestra **Proprietà**, in **Tipo di dati**, assicurarsi che sia selezionato il tipo **Data**.</span><span class="sxs-lookup"><span data-stu-id="b5735-123">Select the **Date** column, and then in the **Properties** window, under **Data Type**, make sure  **Date** is selected.</span></span>  
  
2.  <span data-ttu-id="b5735-124">Fare clic sul menu **Tabella**, quindi su **Data** e infine su **Contrassegna come tabella data**.</span><span class="sxs-lookup"><span data-stu-id="b5735-124">Click the **Table** menu, then click **Date**, and then click **Mark as Date Table**.</span></span>  
  
3.  <span data-ttu-id="b5735-125">Nella finestra di dialogo **Contrassegna come tabella data** selezionare la colonna **Date** come identificatore univoco nella casella di riepilogo **Data**.</span><span class="sxs-lookup"><span data-stu-id="b5735-125">In the **Mark as Date Table** dialog box, in the **Date** listbox, select the **Date** column as the unique identifier.</span></span> <span data-ttu-id="b5735-126">In genere, è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b5735-126">It's usually selected by default.</span></span> <span data-ttu-id="b5735-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5735-127">Click **OK**.</span></span> 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a><span data-ttu-id="b5735-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b5735-129">What's next?</span></span>
<span data-ttu-id="b5735-130">[Lezione 4: Creare relazioni](../tutorials/aas-lesson-4-create-relationships.md).</span><span class="sxs-lookup"><span data-stu-id="b5735-130">[Lesson 4: Create relationships](../tutorials/aas-lesson-4-create-relationships.md).</span></span>
  
