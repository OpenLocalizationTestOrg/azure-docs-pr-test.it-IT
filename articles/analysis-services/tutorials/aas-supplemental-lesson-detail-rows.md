---
title: 'Lezione supplementare dell''esercitazione su Azure Analysis Services: righe di dettaglio | Microsoft Docs'
description: Descrive come creare un'espressione di righe di dettaglio nell'esercitazione su Azure Analysis Services.
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
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: fde5cd9a9efc3a13e731a91962ced5c086a72355
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="f1757-103">Lezione supplementare: Righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="f1757-103">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f1757-104">In questa lezione supplementare si userà l'Editor DAX per definire un'espressione di righe di dettaglio personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f1757-104">In this supplemental lesson, you use the DAX Editor to define a custom Detail Rows Expression.</span></span> <span data-ttu-id="f1757-105">Un'espressione di righe di dettaglio è una proprietà su una misura, che offre agli utenti finali ulteriori informazioni sui risultati aggregati di una misura.</span><span class="sxs-lookup"><span data-stu-id="f1757-105">A Detail Rows Expression is a property on a measure, providing end-users more information about the aggregated results of a measure.</span></span> 
  
<span data-ttu-id="f1757-106">Tempo previsto per il completamento della lezione: **10 minuti**</span><span class="sxs-lookup"><span data-stu-id="f1757-106">Estimated time to complete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f1757-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f1757-107">Prerequisites</span></span>  
<span data-ttu-id="f1757-108">L'argomento di questa lezione supplementare fa parte di un'esercitazione sulla creazione di modelli tabulari.</span><span class="sxs-lookup"><span data-stu-id="f1757-108">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="f1757-109">Prima di eseguire le attività di questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti o avere a disposizione un progetto completo del modello di esempio Adventure Works Internet Sales.</span><span class="sxs-lookup"><span data-stu-id="f1757-109">Before performing the tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-to-solve"></a><span data-ttu-id="f1757-110">Qual è l'esigenza?</span><span class="sxs-lookup"><span data-stu-id="f1757-110">What do we need to solve?</span></span>
<span data-ttu-id="f1757-111">Prima di aggiungere un'espressione di righe di dettaglio, verrà esaminata in dettaglio la misura InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="f1757-111">Let's look at the details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="f1757-112">In SSDT fare clic sul menu **Modello** > **Analizza in Excel** per aprire Excel e creare una tabella pivot vuota.</span><span class="sxs-lookup"><span data-stu-id="f1757-112">In SSDT, click the **Model** menu > **Analyze in Excel** to open Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="f1757-113">In **Campi tabella pivot** aggiungere la misura **InternetTotalSales** dalla tabella FactInternetSales in **Valori**, **CalendarYear** dalla tabella DimDate in **Colonne** e **EnglishCountryRegionName** in **Righe**.</span><span class="sxs-lookup"><span data-stu-id="f1757-113">In **PivotTable Fields**, add the **InternetTotalSales** measure from the FactInternetSales table to **Values**, **CalendarYear** from the DimDate table to **Columns**, and **EnglishCountryRegionName** to **Rows**.</span></span> <span data-ttu-id="f1757-114">La tabella pivot offre ora i risultati aggregati dalla misura InternetTotalSales per area e anno.</span><span class="sxs-lookup"><span data-stu-id="f1757-114">Our PivotTable now gives us aggregated results from the InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="f1757-116">Nella tabella pivot fare doppio clic su un valore aggregato per un anno e un nome di area.</span><span class="sxs-lookup"><span data-stu-id="f1757-116">In the PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="f1757-117">In questo esempio sono stati selezionati l'Australia e l'anno 2014.</span><span class="sxs-lookup"><span data-stu-id="f1757-117">Here we double-clicked the value for Australia and the year 2014.</span></span> <span data-ttu-id="f1757-118">Viene aperto un nuovo foglio contenente alcuni dati, ma non molto utili.</span><span class="sxs-lookup"><span data-stu-id="f1757-118">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="f1757-120">In questo caso, sarebbe invece utile una tabella contenente colonne e righe dei dati che contribuiscono al risultato aggregato della misura InternetTotalSales.</span><span class="sxs-lookup"><span data-stu-id="f1757-120">What we would like to see here is a table containing columns and rows of data that contribute to the aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="f1757-121">A tale scopo, è possibile aggiungere un'espressione di righe di dettaglio come proprietà della misura.</span><span class="sxs-lookup"><span data-stu-id="f1757-121">To do that, we can add a Detail Rows Expression as a property of the measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="f1757-122">Aggiungere un'espressione di righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="f1757-122">Add a Detail Rows Expression</span></span>

#### <a name="to-create-a-detail-rows-expression"></a><span data-ttu-id="f1757-123">Per creare un'espressione di righe di dettaglio</span><span class="sxs-lookup"><span data-stu-id="f1757-123">To create a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="f1757-124">In SSDT, nella griglia delle misure della tabella FactInternetSales, fare clic sulla misura **InternetTotalSales**.</span><span class="sxs-lookup"><span data-stu-id="f1757-124">In SSDT, in the FactInternetSales table's measure grid, click the **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="f1757-125">In **Proprietà** > **Espressione righe di dettaglio** fare clic sul pulsante con i tre puntini per aprire l'Editor DAX.</span><span class="sxs-lookup"><span data-stu-id="f1757-125">In **Properties** > **Detail Rows Expression**, click the editor button to open the DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="f1757-127">Nell'Editor DAX immettere l'espressione seguente:</span><span class="sxs-lookup"><span data-stu-id="f1757-127">In DAX Editor, enter the following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="f1757-128">Questa espressione specifica che i nomi, le colonne e i risultati delle misure dalla tabella FactInternetSales e dalle tabelle correlate vengono restituiti quando un utente fa doppio clic su un risultato aggregato in una tabella pivot o un report.</span><span class="sxs-lookup"><span data-stu-id="f1757-128">This expression specifies names, columns, and measure results from the FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="f1757-129">Tornare a Excel ed eliminare il foglio creato nel passaggio 3, quindi fare doppio clic su un valore aggregato.</span><span class="sxs-lookup"><span data-stu-id="f1757-129">Back in Excel, delete the sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="f1757-130">Questa volta, dopo aver definito una proprietà di espressione di righe di dettaglio per la misura, viene aperto un nuovo foglio contenente dati molto più utili.</span><span class="sxs-lookup"><span data-stu-id="f1757-130">This time, with a Detail Rows Expression property defined for the measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="f1757-132">Ridistribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="f1757-132">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="f1757-133">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="f1757-133">See Also</span></span>  
<span data-ttu-id="f1757-134">[SELECTCOLUMNS Function (DAX) (Funzione DAX SELECTCOLUMNS)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="f1757-134">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="f1757-135">Lezione supplementare: Sicurezza dinamica</span><span class="sxs-lookup"><span data-stu-id="f1757-135">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="f1757-136">Lezione supplementare: Gerarchie incomplete</span><span class="sxs-lookup"><span data-stu-id="f1757-136">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
