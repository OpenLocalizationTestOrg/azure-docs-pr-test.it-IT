---
title: dati aaaImport in Machine Learning Studio | Documenti Microsoft
description: Come tooimport i dati in Azure Machine Learning Studio di varie origini dati. Informazioni sui tipi di dati e i formati di dati supportati.
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
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a><span data-ttu-id="bc3b0-105">Importare dati di training in Azure Machine Learning Studio da varie origini dati</span><span class="sxs-lookup"><span data-stu-id="bc3b0-105">Import your training data into Azure Machine Learning Studio from various data sources</span></span>
<span data-ttu-id="bc3b0-106">toouse i propri dati in Machine Learning Studio toodevelop e train una soluzione analitica predittiva, è possibile:</span><span class="sxs-lookup"><span data-stu-id="bc3b0-106">toouse your own data in Machine Learning Studio toodevelop and train a predictive analytics solution, you can:</span></span> 

* <span data-ttu-id="bc3b0-107">caricare i dati da un **file locale** avanti rispetto ora da toocreate il disco rigido di un modulo di set di dati nell'area di lavoro</span><span class="sxs-lookup"><span data-stu-id="bc3b0-107">upload data from a **local file** ahead of time from your hard drive toocreate a dataset module in your workspace</span></span>
* <span data-ttu-id="bc3b0-108">accedere ai dati da uno dei diversi **le origini dati online** durante l'esecuzione dell'esperimento usando hello [l'importazione dei dati] [ import-data] modulo</span><span class="sxs-lookup"><span data-stu-id="bc3b0-108">access data from one of several **online data sources** while your experiment is running using hello [Import Data][import-data] module</span></span> 
* <span data-ttu-id="bc3b0-109">Usare i dati da un altro **esperimento** di Azure Machine Learning salvato come un set di dati.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-109">use data from another Azure Machine learning **experiment** saved as a dataset</span></span>
* <span data-ttu-id="bc3b0-110">Usare i dati da un **database di SQL Server** locale</span><span class="sxs-lookup"><span data-stu-id="bc3b0-110">use data from an on-premises **SQL Server database**</span></span>

<span data-ttu-id="bc3b0-111">Ognuna di queste opzioni è descritta in uno degli argomenti hello menu hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-111">Each of these options is described in one of hello topics on hello menu below.</span></span> <span data-ttu-id="bc3b0-112">Questi argomenti illustrano come tooimport dati da queste varie origini toouse in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-112">These topics show you how tooimport data from these various data sources toouse in Machine Learning Studio.</span></span> 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> <span data-ttu-id="bc3b0-113">In Machine Learning Studio sono disponibili numerosi set di dati di esempio che è possibile usare per questo scopo.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-113">There are a number of sample datasets available in Machine Learning Studio that you can use for training data.</span></span> <span data-ttu-id="bc3b0-114">Per informazioni, vedere [utilizzare set di dati di esempio hello in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span><span class="sxs-lookup"><span data-stu-id="bc3b0-114">For information on these, see [Use hello sample datasets in Azure Machine Learning Studio](machine-learning-use-sample-datasets.md)).</span></span>
> 
> 

<span data-ttu-id="bc3b0-115">In questo argomento introduttivo, inoltre, viene descritto l'utilizzo in Machine Learning Studio tooget dati pronti per e descrive quali i formati di dati e tipi di dati sono supportati.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-115">This introductory topic also discusses how tooget data ready for use in Machine Learning Studio and describes which data formats and data types are supported.</span></span> 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a><span data-ttu-id="bc3b0-116">Preparare i dati da usare in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="bc3b0-116">Get data ready for use in Azure Machine Learning Studio</span></span>
<span data-ttu-id="bc3b0-117">Machine Learning Studio è progettato toowork con i dati tabulari o rettangolari, ad esempio i dati di testo delimitato o strutturato i dati da un database, anche se in alcuni casi potrebbero essere utilizzati dati non rettangolari.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-117">Machine Learning Studio is designed toowork with rectangular or tabular data, such as text data that's delimited or structured data from a database, though in some circumstances non-rectangular data may be used.</span></span>

<span data-ttu-id="bc3b0-118">È consigliabile che i dati siano relativamente puliti.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-118">It's best if your data is relatively clean.</span></span> <span data-ttu-id="bc3b0-119">Tootake cure problemi, ad esempio stringhe non racchiusi tra virgolette, è necessario prima di caricare dati hello nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-119">That is, you'll want tootake care of issues such as unquoted strings before you upload hello data into your experiment.</span></span>

<span data-ttu-id="bc3b0-120">In Machine Learning Studio sono tuttavia disponibili moduli che consentono di eseguire alcune modifiche dei dati all'interno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-120">However, there are modules available in Machine Learning Studio that enable some manipulation of data within your experiment.</span></span> <span data-ttu-id="bc3b0-121">A seconda di algoritmi di machine learning hello userai, potrebbe essere necessario come toodecide gestire problemi strutturali di dati, ad esempio i valori mancanti e i dati di tipo sparse e sono disponibili i moduli che possono risultare utili che.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-121">Depending on hello machine learning algorithms you'll be using, you may need toodecide how you'll handle data structural issues such as missing values and sparse data, and there are modules that can help with that.</span></span> <span data-ttu-id="bc3b0-122">Cerca in hello **Data Transformation** sezione della tavolozza modulo hello per i moduli che queste funzioni.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-122">Look in hello **Data Transformation** section of hello module palette for modules that perform these functions.</span></span>

<span data-ttu-id="bc3b0-123">In qualsiasi momento nell'esperimento, è possibile visualizzare o scaricare dati hello sono prodotto da un modulo, fare clic sulla porta di output di hello.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-123">At any point in your experiment you can view or download hello data that's produced by a module by clicking hello output port.</span></span> <span data-ttu-id="bc3b0-124">In base al modulo hello, opzioni di download diversi potrebbero essere disponibili, o è in grado di toovisualize hello dati all'interno del browser in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-124">Depending on hello module, there may be different download options available, or you may be able toovisualize hello data within your web browser in Machine Learning Studio.</span></span>

## <a name="data-formats-and-data-types-supported"></a><span data-ttu-id="bc3b0-125">Tipi di dati e formati di dati supportati</span><span class="sxs-lookup"><span data-stu-id="bc3b0-125">Data formats and data types supported</span></span>
<span data-ttu-id="bc3b0-126">È possibile importare un numero di tipi di dati nell'esperimento, a seconda di quale meccanismo è utilizzare dati tooimport e dove provengono da:</span><span class="sxs-lookup"><span data-stu-id="bc3b0-126">You can import a number of data types into your experiment, depending on what mechanism you use tooimport data and where it's coming from:</span></span>

* <span data-ttu-id="bc3b0-127">Testo normale (con estensione txt)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-127">Plain text (.txt)</span></span>
* <span data-ttu-id="bc3b0-128">Valori delimitati da virgole (CSV) con un'intestazione (con estensione csv) o senza intestazione (con estensione nh.csv)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-128">Comma-separated values (CSV) with a header (.csv) or without (.nh.csv)</span></span>
* <span data-ttu-id="bc3b0-129">Valori separati da tabulazioni (TSV) con un'intestazione (con estensione tsv) o senza intestazione (con estensione nh.tsv)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-129">Tab-separated values (TSV) with a header (.tsv) or without (.nh.tsv)</span></span>
* <span data-ttu-id="bc3b0-130">File di Excel</span><span class="sxs-lookup"><span data-stu-id="bc3b0-130">Excel file</span></span>
* <span data-ttu-id="bc3b0-131">Tabella di Azure</span><span class="sxs-lookup"><span data-stu-id="bc3b0-131">Azure table</span></span>
* <span data-ttu-id="bc3b0-132">Tabella Hive</span><span class="sxs-lookup"><span data-stu-id="bc3b0-132">Hive table</span></span>
* <span data-ttu-id="bc3b0-133">Tabella di database SQL</span><span class="sxs-lookup"><span data-stu-id="bc3b0-133">SQL database table</span></span>
* <span data-ttu-id="bc3b0-134">Valori OData</span><span class="sxs-lookup"><span data-stu-id="bc3b0-134">OData values</span></span>
* <span data-ttu-id="bc3b0-135">Dati SVMLight (.svmlight) (vedere hello [SVMLight definizione](http://svmlight.joachims.org/) informazioni di formato)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-135">SVMLight data (.svmlight) (see hello [SVMLight definition](http://svmlight.joachims.org/) for format information)</span></span>
* <span data-ttu-id="bc3b0-136">Dati di relazione File formato ARFF () (.arff) dell'attributo (vedere hello [definizione ARFF](http://weka.wikispaces.com/ARFF) informazioni di formato)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-136">Attribute Relation File Format (ARFF) data (.arff) (see hello [ARFF definition](http://weka.wikispaces.com/ARFF) for format information)</span></span>
* <span data-ttu-id="bc3b0-137">File ZIP (con estensione zip)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-137">Zip file (.zip)</span></span>
* <span data-ttu-id="bc3b0-138">File dell’oggetto o dell'area di lavoro R (con estensione RData)</span><span class="sxs-lookup"><span data-stu-id="bc3b0-138">R object or workspace file (.RData)</span></span>

<span data-ttu-id="bc3b0-139">Se si importano dati in un formato quale ARFF che include i metadati, Machine Learning Studio Usa questa voce di metadati toodefine hello e tipo di dati di ogni colonna.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-139">If you import data in a format such as ARFF that includes metadata, Machine Learning Studio uses this metadata toodefine hello heading and data type of each column.</span></span>

<span data-ttu-id="bc3b0-140">Se si importano dati, ad esempio il formato TSV o CSV che non include i metadati, Machine Learning Studio deduce il tipo di dati hello per ogni colonna tramite il campionamento dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-140">If you import data such as TSV or CSV format that doesn't include this metadata, Machine Learning Studio infers hello data type for each column by sampling hello data.</span></span> <span data-ttu-id="bc3b0-141">Se i dati di hello non dispone anche di intestazioni di colonna, Machine Learning Studio fornisce i nomi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-141">If hello data also doesn't have column headings, Machine Learning Studio provides default names.</span></span>

<span data-ttu-id="bc3b0-142">È possibile in modo esplicito specificare o modificare tipi di dati e le intestazioni di hello per le colonne utilizzando hello [Modifica metadati][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="bc3b0-142">You can explicitly specify or change hello headings and data types for columns using hello [Edit Metadata][edit-metadata].</span></span>

<span data-ttu-id="bc3b0-143">esempio Hello **tipi di dati** sono riconosciuti da Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="bc3b0-143">hello following **data types** are recognized by Machine Learning Studio:</span></span>

* <span data-ttu-id="bc3b0-144">String</span><span class="sxs-lookup"><span data-stu-id="bc3b0-144">String</span></span>
* <span data-ttu-id="bc3b0-145">Integer</span><span class="sxs-lookup"><span data-stu-id="bc3b0-145">Integer</span></span>
* <span data-ttu-id="bc3b0-146">Double</span><span class="sxs-lookup"><span data-stu-id="bc3b0-146">Double</span></span>
* <span data-ttu-id="bc3b0-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="bc3b0-147">Boolean</span></span>
* <span data-ttu-id="bc3b0-148">DateTime</span><span class="sxs-lookup"><span data-stu-id="bc3b0-148">DateTime</span></span>
* <span data-ttu-id="bc3b0-149">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="bc3b0-149">TimeSpan</span></span>

<span data-ttu-id="bc3b0-150">Machine Learning Studio Usa un tipo di dati interno denominato ***tabella dati*** toopass dati tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-150">Machine Learning Studio uses an internal data type called ***Data Table*** toopass data between modules.</span></span> <span data-ttu-id="bc3b0-151">È possibile convertire in modo esplicito i dati in formato tabella di dati utilizzando hello [convertire tooDataset] [ convert-to-dataset] modulo.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-151">You can explicitly convert your data into Data Table format using hello [Convert tooDataset][convert-to-dataset] module.</span></span>

<span data-ttu-id="bc3b0-152">Tutti i moduli che accetta i formati diversi da tabella dati convertirà automaticamente hello dati tooData tabella prima di passarlo toohello successivo modulo.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-152">Any module that accepts formats other than Data Table will convert hello data tooData Table silently before passing it toohello next module.</span></span>

<span data-ttu-id="bc3b0-153">Se necessario, è possibile convertire il formato Tabella dati in CSV, TSV, ARFF o SVMLight usando altri moduli di conversione.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-153">If necessary, you can convert Data Table format back into CSV, TSV, ARFF, or SVMLight format using other conversion modules.</span></span>
<span data-ttu-id="bc3b0-154">Cerca in hello **Data Format Conversions** sezione della tavolozza modulo hello per i moduli che queste funzioni.</span><span class="sxs-lookup"><span data-stu-id="bc3b0-154">Look in hello **Data Format Conversions** section of hello module palette for modules that perform these functions.</span></span>

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
