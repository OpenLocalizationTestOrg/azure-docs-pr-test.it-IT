---
title: Importare dati in Machine Learning Studio | Microsoft Docs
description: Come importare dati in Azure Machine Learning Studio da varie origini dati. Informazioni sui tipi di dati e i formati di dati supportati.
keywords: dati di importazione,formato dati,tipi di dati,origini dati,dati di training
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: b92b480e62f4ce4f4836dc5d0f6afbe80c6b664a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="c9b64-105">Importare dati di training in Azure Machine Learning Studio da varie origini dati</span><span class="sxs-lookup"><span data-stu-id="c9b64-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="c9b64-106">Per usare i propri dati in Machine Learning Studio per sviluppare ed eseguire il training di una soluzione di analisi predittiva, è possibile:</span><span class="sxs-lookup"><span data-stu-id="c9b64-106">To use your own data in Machine Learning Studio to develop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="c9b64-107">Caricare anticipatamente i dati da un **file locale** nel disco rigido per creare un modulo di set di dati nell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="c9b64-107">upload data from a **local file** ahead of time from your hard drive to create a dataset module in your workspace</span></span>
* <span data-ttu-id="c9b64-108">Accedere ai dati da una delle diverse **origini dati online** mentre l'esperimento viene eseguito tramite il modulo [Import Data][import-data]</span><span class="sxs-lookup"><span data-stu-id="c9b64-108">access data from one of several **online data sources** while your experiment is running using the [Import Data][import-data] module</span></span> 
* <span data-ttu-id="c9b64-109">Usare i dati da un altro **esperimento** di Azure Machine Learning salvato come un set di dati.</span><span class="sxs-lookup"><span data-stu-id="c9b64-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="c9b64-110">Usare i dati da un **database di SQL Server** locale</span><span class="sxs-lookup"><span data-stu-id="c9b64-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="c9b64-111">Ciascuna di queste opzioni viene descritta in uno degli argomenti del menu sottostante.</span><span class="sxs-lookup"><span data-stu-id="c9b64-111">Each of these options is described in one of the topics on the menu below.</span></span> <span data-ttu-id="c9b64-112">Questi argomenti illustrano come importare dati da diverse origini dati da utilizzare in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c9b64-112">These topics show you how to import data from these various data sources to use in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="c9b64-113">In Machine Learning Studio sono disponibili numerosi set di dati di esempio che è possibile usare per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="c9b64-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="c9b64-114">Per informazioni, vedere [Usare i set di dati di esempio in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="c9b64-114">For information on these, see [Use the sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="c9b64-115">Questo argomento introduttivo illustra anche come ottenere dati pronti per l'uso in Machine Learning Studio e descrive i tipi e i formati di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="c9b64-115">This introductory topic also discusses how to get data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="c9b64-116">Preparare i dati da usare in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="c9b64-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="c9b64-117">Machine Learning Studio è progettato per lavorare con dati tabulari o rettangolari, ad esempio dati di testo che rappresentano dati delimitati o strutturati di un database, anche se in alcuni casi potrebbero essere usati dati non rettangolari.</span><span class="sxs-lookup"><span data-stu-id="c9b64-117">Machine Learning Studio is designed to work with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="c9b64-118">È consigliabile che i dati siano relativamente puliti.</span><span class="sxs-lookup"><span data-stu-id="c9b64-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="c9b64-119">Ciò significa che, prima di caricare i dati nell’esperimento, è opportuno risolvere eventuali problemi, ad esempio stringhe non racchiuse tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="c9b64-119">That is, you'll want to take care of issues such as unquoted strings before you upload the data into your experiment.</span></span>

<span data-ttu-id="c9b64-120">In Machine Learning Studio sono tuttavia disponibili moduli che consentono di eseguire alcune modifiche dei dati all'interno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="c9b64-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="c9b64-121">A seconda degli algoritmi di Machine Learning usati, potrebbe essere necessario stabilire come gestire problemi strutturali di dati, ad esempio valori mancanti e dati di tipo sparse. A tale scopo, esistono moduli che possono rivelarsi utili.</span><span class="sxs-lookup"><span data-stu-id="c9b64-121">Depending on the machine learning algorithms you'll be using, you may need to decide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="c9b64-122">Vedere la sezione **Trasformazione dei dati** della tavolozza dei moduli per i moduli che eseguono queste funzioni.</span><span class="sxs-lookup"><span data-stu-id="c9b64-122">Look in the **Data Transformation** section of the module palette for modules that perform these functions.</span></span>

<span data-ttu-id="c9b64-123">In qualsiasi momento dell'esperimento, è possibile visualizzare o scaricare i dati prodotti da un modulo facendo clic sulla porta di output.</span><span class="sxs-lookup"><span data-stu-id="c9b64-123">At any point in your experiment you can view or download the data that's produced by a module by clicking the output port.</span></span> <span data-ttu-id="c9b64-124">A seconda del modulo, potrebbero essere disponibili opzioni di download diverse, oppure l'utente potrebbe essere in grado di visualizzare i dati dal browser Web in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c9b64-124">Depending on the module, there may be different download options available, or you may be able to visualize the data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="c9b64-125">Tipi di dati e formati di dati supportati</span><span class="sxs-lookup"><span data-stu-id="c9b64-125">Data formats and data types supported</span></span>
<span data-ttu-id="c9b64-126">È possibile importare diversi tipi di dati nell'esperimento, a seconda del meccanismo usato per importare dati e della relativa provenienza:</span><span class="sxs-lookup"><span data-stu-id="c9b64-126">You can import a number of data types into your experiment, depending on what mechanism you use to import data and where it's coming from:</span></span>

* <span data-ttu-id="c9b64-127">Testo normale (con estensione txt)</span><span class="sxs-lookup"><span data-stu-id="c9b64-127">Plain text (.txt)</span></span>
* <span data-ttu-id="c9b64-128">Valori delimitati da virgole (CSV) con un'intestazione (con estensione csv) o senza intestazione (con estensione nh.csv)</span><span class="sxs-lookup"><span data-stu-id="c9b64-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="c9b64-129">Valori separati da tabulazioni (TSV) con un'intestazione (con estensione tsv) o senza intestazione (con estensione nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="c9b64-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="c9b64-130">File di Excel</span><span class="sxs-lookup"><span data-stu-id="c9b64-130">Excel file</span></span>
* <span data-ttu-id="c9b64-131">Tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="c9b64-131">Azure table</span></span>
* <span data-ttu-id="c9b64-132">Tabella Hive</span><span class="sxs-lookup"><span data-stu-id="c9b64-132">Hive table</span></span>
* <span data-ttu-id="c9b64-133">Tabella di database SQL</span><span class="sxs-lookup"><span data-stu-id="c9b64-133">SQL database table</span></span>
* <span data-ttu-id="c9b64-134">Valori OData</span><span class="sxs-lookup"><span data-stu-id="c9b64-134">OData values</span></span>
* <span data-ttu-id="c9b64-135">Dati SVMLight (con estensione svmlight) (vedere la [definizione di SVMLight](http://svmlight.joachims.org/) per informazioni sul formato)</span><span class="sxs-lookup"><span data-stu-id="c9b64-135">SVMLight data (.svmlight) (see the [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="c9b64-136">Dati ARFF (Attribute Relation File Format) (con estensione arff) (vedere la [definizione di ARFF](http://weka.wikispaces.com/ARFF) per informazioni sul formato)</span><span class="sxs-lookup"><span data-stu-id="c9b64-136">Attribute Relation File Format (ARFF) data (.arff) (see the [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="c9b64-137">File ZIP (con estensione zip)</span><span class="sxs-lookup"><span data-stu-id="c9b64-137">Zip file (.zip)</span></span>
* <span data-ttu-id="c9b64-138">File dell’oggetto o dell'area di lavoro R (con estensione RData)</span><span class="sxs-lookup"><span data-stu-id="c9b64-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="c9b64-139">Se si importano dati in un formato quale ARFF che include metadati, Machine Learning Studio usa i metadati per definire l'intestazione e il tipo di dati di ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="c9b64-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata to define the heading and data type of each column.</span></span>

<span data-ttu-id="c9b64-140">Se si importano dati in un formato quale TSV o CSV che non include metadati, Machine Learning Studio deduce il tipo di dati per ogni colonna tramite il campionamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="c9b64-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers the data type for each column by sampling the data.</span></span> <span data-ttu-id="c9b64-141">Se nemmeno i dati presentano intestazioni di colonna, Machine Learning Studio fornisce nomi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="c9b64-141">If the data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="c9b64-142">È possibile specificare in modo esplicito o modificare le intestazioni e i tipi di dati delle colonne tramite l'[Editor metadati][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="c9b64-142">You can explicitly specify or change the headings and data types for columns using the [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="c9b64-143">I seguenti **tipi di dati** vengono riconosciuti da Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="c9b64-143">The following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="c9b64-144">String</span><span class="sxs-lookup"><span data-stu-id="c9b64-144">String</span></span>
* <span data-ttu-id="c9b64-145">Integer</span><span class="sxs-lookup"><span data-stu-id="c9b64-145">Integer</span></span>
* <span data-ttu-id="c9b64-146">Double</span><span class="sxs-lookup"><span data-stu-id="c9b64-146">Double</span></span>
* <span data-ttu-id="c9b64-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="c9b64-147">Boolean</span></span>
* <span data-ttu-id="c9b64-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="c9b64-148">DateTime</span></span>
* <span data-ttu-id="c9b64-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c9b64-149">TimeSpan</span></span>

<span data-ttu-id="c9b64-150">Machine Learning Studio usa un tipo di dati interno denominato ***Tabella dati*** per passare i dati tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="c9b64-150">Machine Learning Studio uses an internal data type called ***Data Table*** to pass data between modules.</span></span> <span data-ttu-id="c9b64-151">È possibile convertire in modo esplicito i dati in formato Tabella dati tramite il modulo [Convertire in set di dati][convert-to-dataset].</span><span class="sxs-lookup"><span data-stu-id="c9b64-151">You can explicitly convert your data into Data Table format using the [Convert to Dataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="c9b64-152">I moduli che accettano formati diversi da Tabella dati convertiranno i dati in Tabella dati in modo automatico, prima di passare al modulo successivo.</span><span class="sxs-lookup"><span data-stu-id="c9b64-152">Any module that accepts formats other than Data Table will convert the data to Data Table silently before passing it to the next module.</span></span>

<span data-ttu-id="c9b64-153">Se necessario, è possibile convertire il formato Tabella dati in CSV, TSV, ARFF o SVMLight usando altri moduli di conversione.</span><span class="sxs-lookup"><span data-stu-id="c9b64-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="c9b64-154">Esaminare la sezione **Conversioni di formati di dati** della tavolozza dei moduli per i moduli che eseguono queste funzioni.</span><span class="sxs-lookup"><span data-stu-id="c9b64-154">Look in the **Data Format Conversions** section of the module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
