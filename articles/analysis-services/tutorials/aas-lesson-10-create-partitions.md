---
title: 'Esercitazione su Azure Analysis Services - Lezione 10: Creare partizioni | Microsoft Docs'
description: Descrive come creare partizioni nel progetto per l'esercitazione su Azure Analysis Services.
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
ms.openlocfilehash: df74d9cbdcf4916c24955e491767589e72389155
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-10-create-partitions"></a><span data-ttu-id="42178-103">Lezione 10: Creare partizioni</span><span class="sxs-lookup"><span data-stu-id="42178-103">Lesson 10: Create partitions</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="42178-104">In questa lezione verranno create partizioni per dividere la tabella FactInternetSales in parti logiche più piccole che possono essere elaborate (aggiornate) indipendentemente da altre partizioni.</span><span class="sxs-lookup"><span data-stu-id="42178-104">In this lesson, you create partitions to divide the FactInternetSales table into smaller logical parts that can be processed (refreshed) independent of other partitions.</span></span> <span data-ttu-id="42178-105">Per impostazione predefinita, ogni tabella inclusa nel modello ha una sola partizione, che include tutte le colonne e le righe della tabella.</span><span class="sxs-lookup"><span data-stu-id="42178-105">By default, every table you include in your model has one partition, which includes all the table’s columns and rows.</span></span> <span data-ttu-id="42178-106">Per la tabella FactInternetSales i dati verranno suddivisi in base all'anno, ovvero una partizione per ognuno dei cinque anni della tabella.</span><span class="sxs-lookup"><span data-stu-id="42178-106">For the FactInternetSales table, we want to divide the data by year; one partition for each of the table’s five years.</span></span> <span data-ttu-id="42178-107">Ogni partizione può quindi essere elaborata in modo indipendente.</span><span class="sxs-lookup"><span data-stu-id="42178-107">Each partition can then be processed independently.</span></span> <span data-ttu-id="42178-108">Per altre informazioni, vedere [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular) (Partizioni).</span><span class="sxs-lookup"><span data-stu-id="42178-108">To learn more, see [Partitions](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular).</span></span> 
  
<span data-ttu-id="42178-109">Tempo previsto per il completamento della lezione: **15 minuti**</span><span class="sxs-lookup"><span data-stu-id="42178-109">Estimated time to complete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="42178-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="42178-110">Prerequisites</span></span>  
<span data-ttu-id="42178-111">Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato.</span><span class="sxs-lookup"><span data-stu-id="42178-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="42178-112">Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 9: Creare gerarchie](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="42178-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 9: Create Hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>  
  
## <a name="create-partitions"></a><span data-ttu-id="42178-113">Creare partizioni</span><span class="sxs-lookup"><span data-stu-id="42178-113">Create partitions</span></span>  
  
#### <a name="to-create-partitions-in-the-factinternetsales-table"></a><span data-ttu-id="42178-114">Per creare partizioni nella tabella FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42178-114">To create partitions in the FactInternetSales table</span></span>  
  
1.  <span data-ttu-id="42178-115">In Esplora modelli tabulari espandere **Tabelle** e quindi fare clic con il pulsante destro del mouse su **FactInternetSales** > **Partizioni**.</span><span class="sxs-lookup"><span data-stu-id="42178-115">In Tabular Model Explorer, expand **Tables**, and then right-click **FactInternetSales** > **Partitions**.</span></span>  
  
2.  <span data-ttu-id="42178-116">In Gestione partizioni fare clic su **Copia** e quindi modificare il nome in **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="42178-116">In Partition Manager, click **Copy**, and then change the name to **FactInternetSales2010**.</span></span>
  
    <span data-ttu-id="42178-117">Dato che si vuole che la partizione includa solo le righe all'interno di un determinato periodo, ovvero l'anno 2010, è necessario modificare l'espressione di query.</span><span class="sxs-lookup"><span data-stu-id="42178-117">Because you want the partition to include only those rows within a certain period, for the year 2010, you must modify the query expression.</span></span>
  
4.  <span data-ttu-id="42178-118">Fare clic su **Progetta** per aprire l'Editor di query e quindi fare clic sulla query **FactInternetSales2010**.</span><span class="sxs-lookup"><span data-stu-id="42178-118">Click **Design** to open Query Editor, and then click the **FactInternetSales2010** query.</span></span>

5.  <span data-ttu-id="42178-119">Nell'anteprima fare clic sulla freccia in giù nell'intestazione di colonna **OrderDate** e quindi fare clic su **Filtri per data/ora** > **Tra**.</span><span class="sxs-lookup"><span data-stu-id="42178-119">In preview, click the down arrow in the **OrderDate** column heading, and then click **Date/Time Filters** > **Between**.</span></span>

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  <span data-ttu-id="42178-121">Nella finestra di dialogo Filtra righe in **Mostra righe in cui: OrderDate**, lasciare **è dopo o uguale a** e quindi immettere **1/1/2010** nel campo della data.</span><span class="sxs-lookup"><span data-stu-id="42178-121">In the Filter Rows dialog box, in **Show rows where: OrderDate**, leave **is after or equal to**, and then in the date field, enter **1/1/2010**.</span></span> <span data-ttu-id="42178-122">Lasciare selezionato l'operatore **And**, selezionare **è prima di**, immettere **1/1/2011** nel campo della data e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="42178-122">Leave the **And** operator selected, then select **is before**, then in the date field, enter **1/1/2011**, and then click **OK**.</span></span>

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    <span data-ttu-id="42178-124">Si noti che nell'Editor di query, in Passaggi applicati, è visualizzato un altro passaggio denominato Filtrate righe.</span><span class="sxs-lookup"><span data-stu-id="42178-124">Notice in Query Editor, in APPLIED STEPS, you see another step named Filtered Rows.</span></span> <span data-ttu-id="42178-125">Questo è il filtro applicato per selezionare solo le date degli ordini dal 2010.</span><span class="sxs-lookup"><span data-stu-id="42178-125">This filter is to select only order dates from 2010.</span></span>

8.  <span data-ttu-id="42178-126">Fare clic su **Importa**.</span><span class="sxs-lookup"><span data-stu-id="42178-126">Click **Import**.</span></span>

    <span data-ttu-id="42178-127">In Gestione partizioni si noti che l'espressione di query include ora una clausola Filtrate righe aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="42178-127">In Partition Manager, notice the query expression now has an additional Filtered Rows clause.</span></span>

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    <span data-ttu-id="42178-129">Questa istruzione specifica che la partizione deve includere solo i dati nelle righe in cui OrderDate rientra nell'anno di calendario 2010 come specificato nella clausola Filtrate righe.</span><span class="sxs-lookup"><span data-stu-id="42178-129">This statement specifies this partition should include only the data in those rows where the OrderDate is in the 2010 calendar year as specified in the filtered rows clause.</span></span>  
  
  
#### <a name="to-create-a-partition-for-the-2011-year"></a><span data-ttu-id="42178-130">Per creare una partizione per l'anno 2011</span><span class="sxs-lookup"><span data-stu-id="42178-130">To create a partition for the 2011 year</span></span>  
  
1.  <span data-ttu-id="42178-131">Nell'elenco delle partizioni fare clic sulla partizione **FactInternetSales2010** creata e quindi fare clic su **Copia**.</span><span class="sxs-lookup"><span data-stu-id="42178-131">In the partitions list, click the **FactInternetSales2010** partition you created, and then click **Copy**.</span></span>  <span data-ttu-id="42178-132">Modificare il nome della partizione in **FactInternetSales2011**.</span><span class="sxs-lookup"><span data-stu-id="42178-132">Change the partition name to **FactInternetSales2011**.</span></span> 

    <span data-ttu-id="42178-133">Non è necessario usare l'Editor di query per creare una nuova clausola Righe filtrate.</span><span class="sxs-lookup"><span data-stu-id="42178-133">You do not need to use Query Editor to create a new filtered rows clause.</span></span> <span data-ttu-id="42178-134">Dato che è stata creata una copia della query per il 2010, è sufficiente apportare una piccola modifica nella query per il 2011.</span><span class="sxs-lookup"><span data-stu-id="42178-134">Because you created a copy of the query for 2010, all you need to do is make a slight change in the query for 2011.</span></span>
  
2.  <span data-ttu-id="42178-135">Per fare in modo che questa partizione includa solo le righe per l'anno 2011, in **Espressione query** sostituire gli anni nella clausola Filtrate righe rispettivamente con **2011** e **2012**, come di seguito:</span><span class="sxs-lookup"><span data-stu-id="42178-135">In **Query Expression**, in-order for this partition to include only those rows for the 2011 year, replace the years in the Filtered Rows clause with **2011** and **2012**, respectively, like:</span></span>  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="to-create-partitions-for-2012-2013-and-2014"></a><span data-ttu-id="42178-136">Per creare partizioni per gli anni 2012, 2013 e 2014</span><span class="sxs-lookup"><span data-stu-id="42178-136">To create partitions for 2012, 2013, and 2014.</span></span>  
  
- <span data-ttu-id="42178-137">Seguire i passaggi precedenti e creare partizioni per gli anni 2012, 2013 e 2014, modificando gli anni nella clausola Filtrate righe in modo da includere solo le righe per ognuno di questi anni.</span><span class="sxs-lookup"><span data-stu-id="42178-137">Follow the previous steps, creating partitions for 2012, 2013, and 2014, changing the years in the Filtered Rows clause to include only rows for that year.</span></span> 
  

## <a name="delete-the-factinternetsales-partition"></a><span data-ttu-id="42178-138">Eliminare la partizione FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42178-138">Delete the FactInternetSales partition</span></span>
<span data-ttu-id="42178-139">Ora che sono disponibili partizioni per ogni anno, è possibile eliminare la partizione FactInternetSales, in modo da evitare sovrapposizioni quando si sceglie Elabora tutto per l'elaborazione delle partizioni.</span><span class="sxs-lookup"><span data-stu-id="42178-139">Now that you have partitions for each year, you can delete the FactInternetSales partition; preventing overlap when choosing Process all when processing partitions.</span></span>

#### <a name="to-delete-the-factinternetsales-partition"></a><span data-ttu-id="42178-140">Per eliminare la partizione FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42178-140">To delete the FactInternetSales partition</span></span>
-  <span data-ttu-id="42178-141">Fare clic sulla partizione FactInternetSales e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="42178-141">Click the FactInternetSales partition, and then click **Delete**.</span></span>



## <a name="process-partitions"></a><span data-ttu-id="42178-142">Elaborare le partizioni</span><span class="sxs-lookup"><span data-stu-id="42178-142">Process partitions</span></span>  
<span data-ttu-id="42178-143">In Gestione partizioni, si noti che la colonna **Ultima elaborazione** per ogni nuova partizione creata indica che queste partizioni non sono mai state elaborate.</span><span class="sxs-lookup"><span data-stu-id="42178-143">In Partition Manager, notice the **Last Processed** column for each of the new partitions you created shows these partitions have never been processed.</span></span> <span data-ttu-id="42178-144">Quando si creano partizioni, è necessario eseguire un'operazione Elabora partizioni o Elabora tabella per aggiornare i dati in tali partizioni.</span><span class="sxs-lookup"><span data-stu-id="42178-144">When you create partitions, you should run a Process Partitions or Process Table operation to refresh the data in those partitions.</span></span>  
  
#### <a name="to-process-the-factinternetsales-partitions"></a><span data-ttu-id="42178-145">Per elaborare le partizioni FactInternetSales</span><span class="sxs-lookup"><span data-stu-id="42178-145">To process the FactInternetSales partitions</span></span>  
  
1.  <span data-ttu-id="42178-146">Fare clic su **OK** per chiudere Gestione partizioni.</span><span class="sxs-lookup"><span data-stu-id="42178-146">Click **OK** to close Partition Manager.</span></span>  
  
2.  <span data-ttu-id="42178-147">Fare clic sulla tabella **FactInternetSales** e quindi fare clic sul menu **Modello** > **Elabora** > **Elabora partizioni**.</span><span class="sxs-lookup"><span data-stu-id="42178-147">Click the **FactInternetSales** table, then click the **Model** menu > **Process** > **Process Partitions**.</span></span>  
  
3.  <span data-ttu-id="42178-148">Nella finestra di dialogo Elabora partizioni verificare che **Modalità** sia impostata su **Elaborazione predefinita**.</span><span class="sxs-lookup"><span data-stu-id="42178-148">In the Process Partitions dialog box, verify **Mode** is set to **Process Default**.</span></span>  
  
4.  <span data-ttu-id="42178-149">Selezionare la casella di controllo **Elaborazione** per ognuna delle cinque partizioni create e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="42178-149">Select the checkbox in the **Process** column for each of the five partitions you created, and then click **OK**.</span></span>  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    <span data-ttu-id="42178-151">Se vengono richieste le credenziali di rappresentazione, immettere il nome utente e la password di Windows specificati nella lezione 2.</span><span class="sxs-lookup"><span data-stu-id="42178-151">If you're prompted for Impersonation credentials, enter the Windows user name and password you specified in Lesson 2.</span></span>  
  
    <span data-ttu-id="42178-152">Verrà aperta la finestra di dialogo **Elaborazione dati** in cui vengono visualizzati i dettagli dell'elaborazione per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="42178-152">The **Data Processing** dialog box appears and displays process details for each partition.</span></span> <span data-ttu-id="42178-153">Si noti che viene trasferito un numero diverso di righe per ogni partizione,</span><span class="sxs-lookup"><span data-stu-id="42178-153">Notice that a different number of rows for each partition are transferred.</span></span> <span data-ttu-id="42178-154">perché ogni partizione include solo le righe per l'anno specificato nella clausola WHERE nell'istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="42178-154">Each partition includes only those rows for the year specified in the WHERE clause in the SQL Statement.</span></span> <span data-ttu-id="42178-155">Al termine dell'elaborazione, proseguire e chiudere la finestra di dialogo Elaborazione dati.</span><span class="sxs-lookup"><span data-stu-id="42178-155">When processing is finished, go ahead and close the Data Processing dialog box.</span></span>  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a><span data-ttu-id="42178-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="42178-157">What's next?</span></span>
<span data-ttu-id="42178-158">Passare alla lezione successiva: [Lezione 11: Creare ruoli](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="42178-158">Go to the next lesson: [Lesson 11: Create Roles](../tutorials/aas-lesson-11-create-roles.md).</span></span> 
