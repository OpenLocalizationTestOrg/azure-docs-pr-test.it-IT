---
title: Usare Azure Machine Learning con SQL Data Warehouse | Documentazione Microsoft
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
ms.openlocfilehash: c19860c6b5b1c15d1e29ddc67f9cf9ad4618725b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a><span data-ttu-id="457b1-103">Usare Azure Machine Learning con SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="457b1-103">Use Azure Machine Learning with SQL Data Warehouse</span></span>
<span data-ttu-id="457b1-104">Azure Machine Learning è un servizio di analisi predittive completamente gestito, che può essere usato per creare modelli predittivi dei dati in SQL Data Warehouse e pubblicarli come servizi pronti all'uso.</span><span class="sxs-lookup"><span data-stu-id="457b1-104">Azure Machine Learning is a fully managed predictive analytics service that you can use to create predictive models against your data in SQL Data Warehouse, and then publish as ready-to-consume web services.</span></span> <span data-ttu-id="457b1-105">Per le nozioni di base sull'analisi predittiva e su Machine Learning, vedere [Introduzione a Machine Learning in Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="457b1-105">You can learn the basics of predictive analytics and machine learning by reading [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>  <span data-ttu-id="457b1-106">Sarà quindi possibile imparare a creare, eseguire il training, assegnare punteggi e testare un modello di Machine Learning usando l'[esercitazione per la creazione di esperimenti][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="457b1-106">You can then learn how to create, train, score and test a machine learning model using the [Create experiment tutorial][Create experiment tutorial].</span></span>

<span data-ttu-id="457b1-107">Questo articolo illustra come effettuare le operazioni seguenti usando [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span><span class="sxs-lookup"><span data-stu-id="457b1-107">In this article, you will learn how to do the following using the [Azure Machine Learning Studio][Azure Machine Learning Studio]:</span></span>

* <span data-ttu-id="457b1-108">Leggere i dati dal database da creare, eseguire il training e il punteggio di un modello di stima</span><span class="sxs-lookup"><span data-stu-id="457b1-108">Read data from your database to create, train and score a predictive model</span></span>
* <span data-ttu-id="457b1-109">Scrivere dati nel database</span><span class="sxs-lookup"><span data-stu-id="457b1-109">Write data to your database</span></span>

## <a name="read-data-from-sql-data-warehouse"></a><span data-ttu-id="457b1-110">Leggere dati da SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="457b1-110">Read data from SQL Data Warehouse</span></span>
<span data-ttu-id="457b1-111">Si leggeranno i dati dalla tabella Product nel database AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="457b1-111">We will read data from Product table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="457b1-112">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="457b1-112">Step 1</span></span>
<span data-ttu-id="457b1-113">Avviare un nuovo esperimento facendo clic su +NEW nella parte inferiore della finestra di Machine Learning Studio, selezionare EXPERIMENT, quindi Blank Experiment.</span><span class="sxs-lookup"><span data-stu-id="457b1-113">Start a new experiment by clicking +NEW at the bottom of the Machine Learning Studio window, select EXPERIMENT, and then select Blank Experiment.</span></span> <span data-ttu-id="457b1-114">Selezionare il nome dell'esperimento predefinito nella parte superiore dell'area di disegno e denominarlo in modo significativo, ad esempio Bicycle price prediction.</span><span class="sxs-lookup"><span data-stu-id="457b1-114">Select the default experiment name at the top of the canvas and rename it to something meaningful, for example, Bicycle price prediction.</span></span>

### <a name="step-2"></a><span data-ttu-id="457b1-115">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="457b1-115">Step 2</span></span>
<span data-ttu-id="457b1-116">Cercare il modulo Reader nella tavolozza dei set di dati e moduli a sinistra dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="457b1-116">Look for the Reader module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="457b1-117">Trascinare il set di dati nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="457b1-117">Drag the module to the experiment canvas.</span></span>
![][drag_reader]

### <a name="step-3"></a><span data-ttu-id="457b1-118">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="457b1-118">Step 3</span></span>
<span data-ttu-id="457b1-119">Selezionare il modulo Reader e compilare il riquadro delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="457b1-119">Select the Reader module and fill out the properties pane.</span></span>

1. <span data-ttu-id="457b1-120">Selezionare il database SQL di Azure in Data Source.</span><span class="sxs-lookup"><span data-stu-id="457b1-120">Select Azure SQL Database as the Data Source.</span></span>
2. <span data-ttu-id="457b1-121">Database server name: digitare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="457b1-121">Database server name: Type the server name.</span></span> <span data-ttu-id="457b1-122">Per trovarlo, è possibile usare il [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="457b1-122">You can use the [Azure portal][Azure portal] to find this.</span></span>

![][server_name]

1. <span data-ttu-id="457b1-123">Database name: digitare il nome del database nel server specificato.</span><span class="sxs-lookup"><span data-stu-id="457b1-123">Database name: Type the name of a database on the server you just specified.</span></span>
2. <span data-ttu-id="457b1-124">Server user account name: digitare il nome utente di un account con autorizzazioni di accesso al database.</span><span class="sxs-lookup"><span data-stu-id="457b1-124">Server user account name:  Type the user name of an account that has access permissions for the database.</span></span>
3. <span data-ttu-id="457b1-125">Server user account password: fornire la password per l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="457b1-125">Server user account password: Provide the password for the specified user account.</span></span>
4. <span data-ttu-id="457b1-126">Accept any server certificate: usare questa opzione (meno sicura) se si vuole evitare di rivedere il certificato del sito prima di leggere i dati.</span><span class="sxs-lookup"><span data-stu-id="457b1-126">Accept any server certificate: Use this option (less secure) if you want to skip reviewing the site certificate before you read your data.</span></span>
5. <span data-ttu-id="457b1-127">Database query: immettere un'istruzione SQL che descriva i dati da leggere.</span><span class="sxs-lookup"><span data-stu-id="457b1-127">Database query: Enter a SQL statement that describes the data you want to read.</span></span> <span data-ttu-id="457b1-128">In questo caso si leggeranno i dati dalla tabella Product usando la query seguente.</span><span class="sxs-lookup"><span data-stu-id="457b1-128">In this case, we will read data from Product table using the following query.</span></span>

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a><span data-ttu-id="457b1-129">Passaggio 4</span><span class="sxs-lookup"><span data-stu-id="457b1-129">Step 4</span></span>
1. <span data-ttu-id="457b1-130">Eseguire l'esperimento facendo clic su Run sotto l'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="457b1-130">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="457b1-131">Al termine dell'esperimento, il modulo Reader sarà contraddistinto da un segno di spunta verde per indicarne il corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="457b1-131">When the experiment finishes, the Reader module will have a green check mark to indicate that it has completed successfully.</span></span> <span data-ttu-id="457b1-132">Si noti anche lo stato Esecuzione terminata nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="457b1-132">Notice also the Finished running status in the upper-right corner.</span></span>

![][run]

1. <span data-ttu-id="457b1-133">Per visualizzare tutti i dati importati, fare clic sulla porta di output nella parte inferiore del set di dati relativo alle automobili e selezionare Visualize.</span><span class="sxs-lookup"><span data-stu-id="457b1-133">To see the imported data, click the output port at the bottom of the automobile dataset and select Visualize.</span></span>

## <a name="create-train-and-score-a-model"></a><span data-ttu-id="457b1-134">Creare, eseguire il training e assegnare un punteggio a un modello</span><span class="sxs-lookup"><span data-stu-id="457b1-134">Create, train and score a model</span></span>
<span data-ttu-id="457b1-135">A questo punto è possibile utilizzare questo set di dati per:</span><span class="sxs-lookup"><span data-stu-id="457b1-135">Now you can use this dataset to:</span></span>

* <span data-ttu-id="457b1-136">Creare un modello: elaborare i dati e definire le funzionalità</span><span class="sxs-lookup"><span data-stu-id="457b1-136">Create a Model: Process data and define features</span></span>
* <span data-ttu-id="457b1-137">Il training del modello: selezionare e applicare un algoritmo di apprendimento</span><span class="sxs-lookup"><span data-stu-id="457b1-137">Train the model: Choose and apply a learning algorithm</span></span>
* <span data-ttu-id="457b1-138">Assegnare un punteggio e testare il modello: stima di un nuovo prezzo di biciclette</span><span class="sxs-lookup"><span data-stu-id="457b1-138">Score and test the model: Predict new bicycle price</span></span>

![][model]

<span data-ttu-id="457b1-139">Per altre informazioni su come creare, eseguire il training, assegnare punteggi e testare un modello di Machine Learning, usare l'[esercitazione per la creazione di esperimenti][Create experiment tutorial].</span><span class="sxs-lookup"><span data-stu-id="457b1-139">To learn more about how to create, train, score and test a machine learning model use the [Create experiment tutorial][Create experiment tutorial].</span></span>

## <a name="write-data-to-azure-sql-data-warehouse"></a><span data-ttu-id="457b1-140">Scrivere dati in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="457b1-140">Write data to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="457b1-141">Si scriverà il set di risultati nella tabella ProductPriceForecast del database AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="457b1-141">We will write the result set to ProductPriceForecast table in the AdventureWorksDW database.</span></span>

### <a name="step-1"></a><span data-ttu-id="457b1-142">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="457b1-142">Step 1</span></span>
<span data-ttu-id="457b1-143">Cercare il modulo Writer nella tavolozza dei set di dati e moduli a sinistra dell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="457b1-143">Look for the Writer module in the palette of datasets and modules on the left of the experiment canvas.</span></span> <span data-ttu-id="457b1-144">Trascinare il set di dati nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="457b1-144">Drag the module to the experiment canvas.</span></span>

![][drag_writer]

### <a name="step-2"></a><span data-ttu-id="457b1-145">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="457b1-145">Step 2</span></span>
<span data-ttu-id="457b1-146">Selezionare il modulo Writer e compilare il riquadro delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="457b1-146">Select the Writer module and fill out the properties pane.</span></span>

1. <span data-ttu-id="457b1-147">Selezionare il database SQL di Azure in Data Destination.</span><span class="sxs-lookup"><span data-stu-id="457b1-147">Select Azure SQL Database as the Data Destination.</span></span>
2. <span data-ttu-id="457b1-148">Database server name: digitare il nome del server.</span><span class="sxs-lookup"><span data-stu-id="457b1-148">Database server name: Type the server name.</span></span> <span data-ttu-id="457b1-149">Per trovarlo, è possibile usare il [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="457b1-149">You can use the [Azure portal][Azure portal] to find this.</span></span>
3. <span data-ttu-id="457b1-150">Database name: digitare il nome del database nel server specificato.</span><span class="sxs-lookup"><span data-stu-id="457b1-150">Database name: Type the name of a database on the server you just specified.</span></span>
4. <span data-ttu-id="457b1-151">Server user account name: digitare il nome utente di un account con autorizzazioni di scrittura nel database.</span><span class="sxs-lookup"><span data-stu-id="457b1-151">Server user account name:  Type the user name of an account that has write permissions for the database.</span></span>
5. <span data-ttu-id="457b1-152">Server user account password: fornire la password per l'account utente specificato.</span><span class="sxs-lookup"><span data-stu-id="457b1-152">Server user account password: Provide the password for the specified user account.</span></span>
6. <span data-ttu-id="457b1-153">Accept any server certificate (insecure): selezionare questa opzione se non si vuole visualizzare il certificato.</span><span class="sxs-lookup"><span data-stu-id="457b1-153">Accept any server certificate (insecure): Select this option if you don’t want to view the certificate.</span></span>
7. <span data-ttu-id="457b1-154">Comma-separated list of columns to be saved: fornire un elenco del set di dati o delle colonne dei risultati da generare.</span><span class="sxs-lookup"><span data-stu-id="457b1-154">Comma-separated list of columns to be saved: Provide a list of the dataset or result columns that you want to output.</span></span>
8. <span data-ttu-id="457b1-155">Data table name: specificare il nome della tabella dati.</span><span class="sxs-lookup"><span data-stu-id="457b1-155">Data table name: Specify the name of the data table.</span></span>
9. <span data-ttu-id="457b1-156">Comma-separated list of datatable columns: specificare i nomi delle colonne da usare nella nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="457b1-156">Comma-separated list of datatable columns:  Specify the column names to use in the new table.</span></span> <span data-ttu-id="457b1-157">I nomi di colonna possono essere diversi da quelli del set di dati di origine, ma è necessario elencare lo stesso numero di colonne definite per la tabella di output.</span><span class="sxs-lookup"><span data-stu-id="457b1-157">The column names can be different from the ones in the source dataset, but you must list the same number of columns here that you define for the output table.</span></span>
10. <span data-ttu-id="457b1-158">Number of rows written per SQL Azure operation: è possibile configurare il numero di righe scritte in un database SQL in un'unica operazione.</span><span class="sxs-lookup"><span data-stu-id="457b1-158">Number of rows written per SQL Azure operation: You can configure the number of rows that are written to a SQL database in one operation.</span></span>

![][writer_properties]

### <a name="step-3"></a><span data-ttu-id="457b1-159">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="457b1-159">Step 3</span></span>
1. <span data-ttu-id="457b1-160">Eseguire l'esperimento facendo clic su Run sotto l'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="457b1-160">Run the experiment by clicking Run under the experiment canvas.</span></span>
2. <span data-ttu-id="457b1-161">Al termine dell'esperimento, tutti i moduli saranno contraddistinti da un segno di spunta verde per indicarne il corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="457b1-161">When the experiment finishes, all modules will have a green check mark to indicate that they completed successfully.</span></span>

## <a name="next-steps"></a><span data-ttu-id="457b1-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="457b1-162">Next steps</span></span>
<span data-ttu-id="457b1-163">Per altri suggerimenti sullo sviluppo, vedere [Panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="457b1-163">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Introduction to machine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
