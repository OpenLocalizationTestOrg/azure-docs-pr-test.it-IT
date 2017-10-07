---
title: Azure Machine Learning con SQL Data Warehouse aaaUse | Documenti Microsoft
description: Suggerimenti per l'uso di Azure Machine Learning con Azure SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="e297f-103">Usare Azure Machine Learning con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e297f-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="e297f-104">Azure Machine Learning è un servizio completamente gestito analitica predittiva, che è possibile utilizzare modelli predittivi toocreate basati sui dati in SQL Data Warehouse e quindi pubblicare come servizi web pronto all'uso.</span><span class="sxs-lookup"><span data-stu-id="e297f-104">Azure Machine Learning is a fully managed predictive analytics service that you can use toocreate predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="e297f-105">È possibile apprendere nozioni di base di hello di analitica predittiva e machine learning leggendo [tooMachine introduzione di apprendimento in Azure][Introduction tooMachine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="e297f-105">You can learn hello basics of predictive analytics and machine learning by reading [Introduction tooMachine Learning on Azure][Introduction tooMachine Learning on Azure].</span></span>  <span data-ttu-id="e297f-106">Sarà possibile apprendere come toocreate, eseguire il training, assegnare un punteggio e testare un modello di machine learning usando hello [crea esperimento esercitazione][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="e297f-106">You can then learn how toocreate, train, score and test a machine learning model using hello [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="e297f-107">In questo articolo si apprenderà come hello toodo seguenti utilizzando hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="e297f-107">In this article, you will learn how toodo hello following using hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="e297f-108">Dati letti da toocreate il database, eseguire il training e un modello predittivo di punteggio</span><span class="sxs-lookup"><span data-stu-id="e297f-108">Read data from your database toocreate, train and score a predictive model</span></span>
* <span data-ttu-id="e297f-109">Scrittura dati tooyour database</span><span class="sxs-lookup"><span data-stu-id="e297f-109">Write data tooyour database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="e297f-110">Leggere dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e297f-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="e297f-111">Si verranno leggere dati dalla tabella Product nel database AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-111">We will read data from Product table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="e297f-112">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e297f-112">Step 1</span></span>
<span data-ttu-id="e297f-113">Avviare un esperimento di nuovo facendo clic su + Nuovo nella parte inferiore di hello di hello finestra Machine Learning Studio, selezionare ESPERIMENTO, quindi provare vuoto.</span><span class="sxs-lookup"><span data-stu-id="e297f-113">Start a new experiment by clicking +NEW at hello bottom of hello Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="e297f-114">Predefinito selezionare hello sperimentare nome nella parte superiore di hello dell'area di disegno hello e rinominarlo toosomething significativo, ad esempio, stima di prezzo di biciclette.</span><span class="sxs-lookup"><span data-stu-id="e297f-114">Select hello default experiment name at hello top of hello canvas and rename it toosomething meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="e297f-115">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e297f-115">Step 2</span></span>
<span data-ttu-id="e297f-116">Cerca modulo del lettore hello nella tavolozza hello dei set di dati e i moduli in a sinistra dell'area di disegno esperimento hello hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-116">Look for hello Reader module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="e297f-117">Trascinare l'area di disegno hello modulo toohello esperimento.</span><span class="sxs-lookup"><span data-stu-id="e297f-117">Drag hello module toohello experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="e297f-118">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e297f-118">Step 3</span></span>
<span data-ttu-id="e297f-119">Selezionare modulo del lettore hello e compilare riquadro Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-119">Select hello Reader module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="e297f-120">Selezionare i Database SQL di Azure come hello origine dati.</span><span class="sxs-lookup"><span data-stu-id="e297f-120">Select Azure SQL Database as hello Data Source.</span></span>
2. <span data-ttu-id="e297f-121">Nome del server di database: nome del server di tipo hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-121">Database server name: Type hello server name.</span></span> <span data-ttu-id="e297f-122">È possibile utilizzare hello [portale di Azure] [ Azure portal] toofind questo.</span><span class="sxs-lookup"><span data-stu-id="e297f-122">You can use hello [Azure portal][Azure portal] toofind this.</span></span>

![][server_name]

1. <span data-ttu-id="e297f-123">Nome del database: nome hello del tipo di un database nel server di hello è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="e297f-123">Database name: Type hello name of a database on hello server you just specified.</span></span>
2. <span data-ttu-id="e297f-124">Nome dell'account utente server: digitare il nome utente hello di un account che disponga delle autorizzazioni di accesso per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-124">Server user account name:  Type hello user name of an account that has access permissions for hello database.</span></span>
3. <span data-ttu-id="e297f-125">Password dell'account utente server: fornire password hello per hello l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="e297f-125">Server user account password: Provide hello password for hello specified user account.</span></span>
4. <span data-ttu-id="e297f-126">Accettare qualsiasi certificato server: usare questa opzione (meno sicura) se si desidera tooskip revisione certificato del sito hello prima di leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="e297f-126">Accept any server certificate: Use this option (less secure) if you want tooskip reviewing hello site certificate before you read your data.</span></span>
5. <span data-ttu-id="e297f-127">Query di database: immettere un'istruzione SQL che descrive i dati di hello da tooread.</span><span class="sxs-lookup"><span data-stu-id="e297f-127">Database query: Enter a SQL statement that describes hello data you want tooread.</span></span> <span data-ttu-id="e297f-128">In questo caso, si verranno leggere dati dalla tabella di prodotto usando hello seguente query.</span><span class="sxs-lookup"><span data-stu-id="e297f-128">In this case, we will read data from Product table using hello following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="e297f-129">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="e297f-129">Step 4</span></span>
1. <span data-ttu-id="e297f-130">Eseguire l'esperimento di hello facendo clic su Esegui in area di disegno di hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="e297f-130">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="e297f-131">Al termine dell'esperimento hello, il modulo del lettore hello avrà tooindicate un segno di spunta verde che è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="e297f-131">When hello experiment finishes, hello Reader module will have a green check mark tooindicate that it has completed successfully.</span></span> <span data-ttu-id="e297f-132">Si noti inoltre hello completato allo stato in esecuzione nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-132">Notice also hello Finished running status in hello upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="e297f-133">toosee hello dati importati, fare clic sulla porta di output di hello nella parte inferiore di hello del set di dati automobili hello e selezionare Visualizza.</span><span class="sxs-lookup"><span data-stu-id="e297f-133">toosee hello imported data, click hello output port at hello bottom of hello automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="e297f-134">Creare, eseguire il training e assegnare un punteggio a un modello</span><span class="sxs-lookup"><span data-stu-id="e297f-134">Create, train and score a model</span></span>
<span data-ttu-id="e297f-135">A questo punto è possibile utilizzare questo set di dati per:</span><span class="sxs-lookup"><span data-stu-id="e297f-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="e297f-136">Creare un modello: elaborare i dati e definire le funzionalità</span><span class="sxs-lookup"><span data-stu-id="e297f-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="e297f-137">Modello di training hello: scegliere e applica un algoritmo di apprendimento</span><span class="sxs-lookup"><span data-stu-id="e297f-137">Train hello model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="e297f-138">Punteggio e test hello modello: stimare di nuovo prezzo di biciclette</span><span class="sxs-lookup"><span data-stu-id="e297f-138">Score and test hello model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="e297f-139">informazioni su come toocreate, eseguire il training, assegnare un punteggio e testare un machine learning hello utilizzare modello toolearn [crea esperimento esercitazione][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="e297f-139">toolearn more about how toocreate, train, score and test a machine learning model use hello [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-tooazure-sql-data-warehouse"></a><span data-ttu-id="e297f-140">Scrivere dati tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e297f-140">Write data tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="e297f-141">Tabella tooProductPriceForecast set di risultati hello verrà scritto nel database AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-141">We will write hello result set tooProductPriceForecast table in hello AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="e297f-142">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="e297f-142">Step 1</span></span>
<span data-ttu-id="e297f-143">Cerca modulo Writer hello nella tavolozza hello dei set di dati e i moduli in a sinistra dell'area di disegno esperimento hello hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-143">Look for hello Writer module in hello palette of datasets and modules on hello left of hello experiment canvas.</span></span> <span data-ttu-id="e297f-144">Trascinare l'area di disegno hello modulo toohello esperimento.</span><span class="sxs-lookup"><span data-stu-id="e297f-144">Drag hello module toohello experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="e297f-145">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="e297f-145">Step 2</span></span>
<span data-ttu-id="e297f-146">Selezionare il modulo di scrittura hello e compilare riquadro Proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-146">Select hello Writer module and fill out hello properties pane.</span></span>

1. <span data-ttu-id="e297f-147">Selezionare il Database di SQL Azure come destinazione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-147">Select Azure SQL Database as hello Data Destination.</span></span>
2. <span data-ttu-id="e297f-148">Nome del server di database: nome del server di tipo hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-148">Database server name: Type hello server name.</span></span> <span data-ttu-id="e297f-149">È possibile utilizzare hello [portale di Azure] [ Azure portal] toofind questo.</span><span class="sxs-lookup"><span data-stu-id="e297f-149">You can use hello [Azure portal][Azure portal] toofind this.</span></span>
3. <span data-ttu-id="e297f-150">Nome del database: nome hello del tipo di un database nel server di hello è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="e297f-150">Database name: Type hello name of a database on hello server you just specified.</span></span>
4. <span data-ttu-id="e297f-151">Nome dell'account utente server: digitare il nome utente hello di un account che disponga di autorizzazioni di scrittura per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-151">Server user account name:  Type hello user name of an account that has write permissions for hello database.</span></span>
5. <span data-ttu-id="e297f-152">Password dell'account utente server: fornire password hello per hello l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="e297f-152">Server user account password: Provide hello password for hello specified user account.</span></span>
6. <span data-ttu-id="e297f-153">Accettare qualsiasi certificato del server (non protetto): selezionare questa opzione se non si desidera certificato hello tooview.</span><span class="sxs-lookup"><span data-stu-id="e297f-153">Accept any server certificate (insecure): Select this option if you don’t want tooview hello certificate.</span></span>
7. <span data-ttu-id="e297f-154">Elenco delimitato da virgole di colonne toobe salvato: fornire un elenco di colonne di set di dati o un risultato hello che si desidera toooutput.</span><span class="sxs-lookup"><span data-stu-id="e297f-154">Comma-separated list of columns toobe saved: Provide a list of hello dataset or result columns that you want toooutput.</span></span>
8. <span data-ttu-id="e297f-155">Nome della tabella dati: specificare il nome di hello della tabella di dati hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-155">Data table name: Specify hello name of hello data table.</span></span>
9. <span data-ttu-id="e297f-156">Elenco delimitato da virgole delle colonne di datatable: specificare toouse i nomi di colonna hello hello nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="e297f-156">Comma-separated list of datatable columns:  Specify hello column names toouse in hello new table.</span></span> <span data-ttu-id="e297f-157">Hello i nomi di colonna possono essere diversi da hello quelli hello DataSet di origine, ma è necessario elencare hello stesso numero di colonne qui definite per la tabella di output di hello.</span><span class="sxs-lookup"><span data-stu-id="e297f-157">hello column names can be different from hello ones in hello source dataset, but you must list hello same number of columns here that you define for hello output table.</span></span>
10. <span data-ttu-id="e297f-158">Numero di righe scritte per ogni operazione di SQL Azure: È possibile configurare hello numero di righe che vengono scritti i database SQL tooa in un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="e297f-158">Number of rows written per SQL Azure operation: You can configure hello number of rows that are written tooa SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="e297f-159">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="e297f-159">Step 3</span></span>
1. <span data-ttu-id="e297f-160">Eseguire l'esperimento di hello facendo clic su Esegui in area di disegno di hello esperimento.</span><span class="sxs-lookup"><span data-stu-id="e297f-160">Run hello experiment by clicking Run under hello experiment canvas.</span></span>
2. <span data-ttu-id="e297f-161">Al termine dell'esperimento hello, tutti i moduli avrà tooindicate un segno di spunta verde che è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="e297f-161">When hello experiment finishes, all modules will have a green check mark tooindicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e297f-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e297f-162">Next steps</span></span>
<span data-ttu-id="e297f-163">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e297f-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
