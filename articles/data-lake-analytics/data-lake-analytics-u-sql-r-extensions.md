---
title: Estendere gli script U-SQL con R in Azure Data Lake Analytics | Microsoft Docs
description: Informazioni su come eseguire il codice R negli script U-SQL
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="d4052-103">Esercitazione: Introduzione all'estensione di U-SQL con R</span><span class="sxs-lookup"><span data-stu-id="d4052-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="d4052-104">L'esempio seguente illustra i passaggi di base per la distribuzione del codice R:</span><span class="sxs-lookup"><span data-stu-id="d4052-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="d4052-105">Usare l'istruzione `REFERENCE ASSEMBLY` per abilitare le estensioni R per lo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4052-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="d4052-106">Usare l'operazione ` REDUCE` per partizionare i dati di input in una chiave.</span><span class="sxs-lookup"><span data-stu-id="d4052-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="d4052-107">Le estensioni R per U-SQL includono un riduttore predefinito (`Extension.R.Reducer`) che esegue il codice R in ogni vertice assegnato al riduttore.</span><span class="sxs-lookup"><span data-stu-id="d4052-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="d4052-108">Utilizzo dei frame di dati denominati dedicati chiamati rispettivamente `inputFromUSQL` e `outputToUSQL ` per passare dati tra U-SQL e R. I nomi di input e di output dell'identificatore DataFrame sono fissi (vale a dire, gli utenti non possono modificare i nomi predefiniti di input e di output degli identificatori DataFrame).</span><span class="sxs-lookup"><span data-stu-id="d4052-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="d4052-109">Incorporare il codice R nello script U-SQL</span><span class="sxs-lookup"><span data-stu-id="d4052-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="d4052-110">È possibile incorporare il codice R nello script U-SQL usando il parametro del comando di `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="d4052-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="d4052-111">Ad esempio, è possibile dichiarare lo script R come una variabile di stringa e passarlo come parametro al Reducer.</span><span class="sxs-lookup"><span data-stu-id="d4052-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="d4052-112">Mantenere il codice R in un file separato e farvi riferimento nello script U-SQL</span><span class="sxs-lookup"><span data-stu-id="d4052-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="d4052-113">L'esempio seguente illustra un uso più complesso.</span><span class="sxs-lookup"><span data-stu-id="d4052-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="d4052-114">In questo caso, il codice R è distribuito come una RISORSA che rappresenta lo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4052-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="d4052-115">Salvare il codice R come file separato.</span><span class="sxs-lookup"><span data-stu-id="d4052-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="d4052-116">Usare uno script U-SQL per distribuire lo script R con l'istruzione DEPLOY RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="d4052-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="d4052-117">Come R si integra con U-SQL</span><span class="sxs-lookup"><span data-stu-id="d4052-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="d4052-118">Tipi di dati</span><span class="sxs-lookup"><span data-stu-id="d4052-118">Datatypes</span></span>
* <span data-ttu-id="d4052-119">Le colonne di tipo stringa e numeriche di U-SQL vengono convertite così come sono tra DataFrame R e U-SQL [tipi supportati: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="d4052-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="d4052-120">Il datatype `Factor` non è supportato in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4052-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="d4052-121">`byte[]` deve essere serializzato come `string` con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="d4052-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="d4052-122">Le stringhe U-SQL possono essere convertite in fattori nel codice R, una volta che U SQL crea il frame di dati R di input o impostando il parametro riduttore `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="d4052-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="d4052-123">Schemi</span><span class="sxs-lookup"><span data-stu-id="d4052-123">Schemas</span></span>
* <span data-ttu-id="d4052-124">I set di dati di U-SQL non possono avere nomi di colonna duplicati.</span><span class="sxs-lookup"><span data-stu-id="d4052-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="d4052-125">I nomi di colonna dei set di dati di U-SQL devono essere stringhe.</span><span class="sxs-lookup"><span data-stu-id="d4052-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="d4052-126">I nomi di colonna devono essere identici in U-SQL e negli script R.</span><span class="sxs-lookup"><span data-stu-id="d4052-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="d4052-127">Le colonne di sola lettura non possono fare parte del frame di dati di output.</span><span class="sxs-lookup"><span data-stu-id="d4052-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="d4052-128">Poiché le colonne di sola lettura vengono inserite automaticamente nella tabella U-SQL se fanno parte dello schema di output degli oggetti UDO.</span><span class="sxs-lookup"><span data-stu-id="d4052-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="d4052-129">Limitazioni funzionali</span><span class="sxs-lookup"><span data-stu-id="d4052-129">Functional limitations</span></span>
* <span data-ttu-id="d4052-130">Non è possibile creare due volte un'istanza del motore R nello stesso processo.</span><span class="sxs-lookup"><span data-stu-id="d4052-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="d4052-131">Attualmente, U-SQL non supporta UDO Combiner per la stima mediante modelli partizionati generati usando UDO Reducer.</span><span class="sxs-lookup"><span data-stu-id="d4052-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="d4052-132">Gli utenti possono dichiarare i modelli partizionati come risorsa e usarli negli script R. Vedere il codice di esempio `ExtR_PredictUsingLMRawStringReducer.usql`.</span><span class="sxs-lookup"><span data-stu-id="d4052-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="d4052-133">Versioni R</span><span class="sxs-lookup"><span data-stu-id="d4052-133">R Versions</span></span>
<span data-ttu-id="d4052-134">È supportato solo R 3.2.2.</span><span class="sxs-lookup"><span data-stu-id="d4052-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="d4052-135">Moduli R standard</span><span class="sxs-lookup"><span data-stu-id="d4052-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="d4052-136">Limitazioni delle dimensioni di input e output</span><span class="sxs-lookup"><span data-stu-id="d4052-136">Input and Output size limitations</span></span>
<span data-ttu-id="d4052-137">A ogni vertice è assegnata una quantità di memoria limitata,</span><span class="sxs-lookup"><span data-stu-id="d4052-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="d4052-138">Poiché devono esistere frame di dati di input e di output in memoria nel codice R, le dimensioni totali per l'input e per l'output non possono superare i 500 MB.</span><span class="sxs-lookup"><span data-stu-id="d4052-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="d4052-139">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="d4052-139">Sample Code</span></span>
<span data-ttu-id="d4052-140">Altri esempi di codice sono disponibili nell'account Data Lake Store dopo aver installato le estensioni Advanced Analytics U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4052-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="d4052-141">Il percorso per il codice di esempio aggiuntivo è: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="d4052-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="d4052-142">Distribuzione dei moduli personalizzati R con U-SQL</span><span class="sxs-lookup"><span data-stu-id="d4052-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="d4052-143">Innanzitutto, creare un modulo personalizzato R fare lo zip e quindi caricare il file del modulo personalizzato R compresso in un archivio ADL.</span><span class="sxs-lookup"><span data-stu-id="d4052-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="d4052-144">Nell'esempio, si caricherà magittr_1.5.zip nella radice dell'account predefinito ADLS dell'account ADLA che si sta usando.</span><span class="sxs-lookup"><span data-stu-id="d4052-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="d4052-145">Dopo aver caricato il modulo nell'archivio ADL, dichiararlo come quando si usa DEPLOY RESOURCE per renderlo disponibile nello script U-SQL script e chiamare il metodo `install.packages` per installarlo.</span><span class="sxs-lookup"><span data-stu-id="d4052-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="d4052-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4052-146">Next Steps</span></span>
* [<span data-ttu-id="d4052-147">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d4052-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="d4052-148">Sviluppare script U-SQL mediante Strumenti di Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4052-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="d4052-149">Uso delle funzioni finestra di U-SQL per i processi di Analisi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="d4052-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
