---
title: aaaExtend U-SQL consente di generare script di R in Azure Data Lake Analitica | Documenti Microsoft
description: Informazioni su come toorun R code negli script U-SQL
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
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="c90be-103">Esercitazione: Introduzione all'estensione di U-SQL con R</span><span class="sxs-lookup"><span data-stu-id="c90be-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="c90be-104">Hello di esempio seguente illustra i passaggi di base per la distribuzione di codice R hello:</span><span class="sxs-lookup"><span data-stu-id="c90be-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="c90be-105">Hello utilizzare `REFERENCE ASSEMBLY` estensioni tooenable R istruzione per hello Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c90be-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="c90be-106">Utilizzare il` REDUCE` hello toopartition operazione dati su una chiave di input.</span><span class="sxs-lookup"><span data-stu-id="c90be-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="c90be-107">le estensioni di Hello R U-SQL includono un riduttore incorporato (`Extension.R.Reducer`) che esegue codice R in ogni riduttore toohello vertice assegnato.</span><span class="sxs-lookup"><span data-stu-id="c90be-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="c90be-108">Utilizzo di dedicato denominato frame di dati denominati `inputFromUSQL` e `outputToUSQL `rispettivamente toopass dati tra U-SQL e R. Input e output vengono corretti i nomi degli identificatori di frame di dati (vale a dire gli utenti non è possibile modificare questi nomi predefiniti dell'input e frame di dati di output identificatori).</span><span class="sxs-lookup"><span data-stu-id="c90be-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="c90be-109">Incorporare codice R in hello script U-SQL</span><span class="sxs-lookup"><span data-stu-id="c90be-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="c90be-110">È possibile codice hello R inline script U-SQL utilizzando il parametro di comando hello di hello `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="c90be-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="c90be-111">Ad esempio, è possibile dichiarare hello script R come una variabile di stringa e passarlo come toohello un parametro del Reducer.</span><span class="sxs-lookup"><span data-stu-id="c90be-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="c90be-112">Conservare il codice hello R in un file separato e farvi riferimento script hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="c90be-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="c90be-113">Hello di esempio seguente viene illustrato un utilizzo più complesso.</span><span class="sxs-lookup"><span data-stu-id="c90be-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="c90be-114">In questo caso, il codice R hello viene distribuito come una risorsa che è hello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c90be-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="c90be-115">Salvare il codice R come file separato.</span><span class="sxs-lookup"><span data-stu-id="c90be-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="c90be-116">Utilizzare un toodeploy script U-SQL script R con hello istruzione distribuire risorse.</span><span class="sxs-lookup"><span data-stu-id="c90be-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="c90be-117">Come R si integra con U-SQL</span><span class="sxs-lookup"><span data-stu-id="c90be-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="c90be-118">Tipi di dati</span><span class="sxs-lookup"><span data-stu-id="c90be-118">Datatypes</span></span>
* <span data-ttu-id="c90be-119">Le colonne di tipo stringa e numeriche di U-SQL vengono convertite così come sono tra DataFrame R e U-SQL [tipi supportati: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="c90be-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="c90be-120">Hello `Factor` tipo di dati non è supportato in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="c90be-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="c90be-121">`byte[]` deve essere serializzato come `string` con codifica Base 64.</span><span class="sxs-lookup"><span data-stu-id="c90be-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="c90be-122">U-SQL le stringhe possono essere convertiti toofactors nel codice R, una volta U-SQL create input frame di dati R dall'impostazione parametro riduttore hello `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="c90be-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="c90be-123">Schemi</span><span class="sxs-lookup"><span data-stu-id="c90be-123">Schemas</span></span>
* <span data-ttu-id="c90be-124">I set di dati di U-SQL non possono avere nomi di colonna duplicati.</span><span class="sxs-lookup"><span data-stu-id="c90be-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="c90be-125">I nomi di colonna dei set di dati di U-SQL devono essere stringhe.</span><span class="sxs-lookup"><span data-stu-id="c90be-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="c90be-126">I nomi di colonna deve essere hello stesso negli script U-SQL e R.</span><span class="sxs-lookup"><span data-stu-id="c90be-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="c90be-127">Colonna di sola lettura non può far parte di hello dataframe di output.</span><span class="sxs-lookup"><span data-stu-id="c90be-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="c90be-128">Poiché le colonne di sola lettura vengono inserite automaticamente nella tabella di hello U-SQL se fa parte dello schema di output dell'operatore definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="c90be-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="c90be-129">Limitazioni funzionali</span><span class="sxs-lookup"><span data-stu-id="c90be-129">Functional limitations</span></span>
* <span data-ttu-id="c90be-130">Hello motore R non è possibile creare due volte in hello stesso processo.</span><span class="sxs-lookup"><span data-stu-id="c90be-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="c90be-131">Attualmente, U-SQL non supporta UDO Combiner per la stima mediante modelli partizionati generati usando UDO Reducer.</span><span class="sxs-lookup"><span data-stu-id="c90be-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="c90be-132">Gli utenti possono dichiarare i modelli di hello partizionata come risorse e utilizzarle nei loro Script di R (vedere il codice di esempio `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="c90be-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="c90be-133">Versioni R</span><span class="sxs-lookup"><span data-stu-id="c90be-133">R Versions</span></span>
<span data-ttu-id="c90be-134">È supportato solo R 3.2.2.</span><span class="sxs-lookup"><span data-stu-id="c90be-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="c90be-135">Moduli R standard</span><span class="sxs-lookup"><span data-stu-id="c90be-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="c90be-136">Limitazioni delle dimensioni di input e output</span><span class="sxs-lookup"><span data-stu-id="c90be-136">Input and Output size limitations</span></span>
<span data-ttu-id="c90be-137">Ogni vertice ha una quantità limitata di memoria assegnata tooit.</span><span class="sxs-lookup"><span data-stu-id="c90be-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="c90be-138">Poiché hello frame di dati di input e output devono essere presenti in memoria nel codice hello R, dimensione totale di hello per hello input e output non può superare i 500 MB.</span><span class="sxs-lookup"><span data-stu-id="c90be-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="c90be-139">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="c90be-139">Sample Code</span></span>
<span data-ttu-id="c90be-140">Dopo aver installato le estensioni di hello Analitica avanzate U-SQL, è disponibile nell'account archivio Data Lake ulteriori esempi di codice.</span><span class="sxs-lookup"><span data-stu-id="c90be-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="c90be-141">percorso di Hello per ulteriori esempi di codice è: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="c90be-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="c90be-142">Distribuzione dei moduli personalizzati R con U-SQL</span><span class="sxs-lookup"><span data-stu-id="c90be-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="c90be-143">Innanzitutto, creare un modulo personalizzato R e zip e quindi caricare hello compresso archivio ADL tooyour file modulo personalizzato di R.</span><span class="sxs-lookup"><span data-stu-id="c90be-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="c90be-144">Nell'esempio hello, si caricheranno magittr_1.5.zip toohello principale dell'account ADLS hello predefinito per l'account ADLA usiamo hello.</span><span class="sxs-lookup"><span data-stu-id="c90be-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="c90be-145">Dopo aver caricato l'archivio di tooADL modulo hello, dichiararla come distribuire risorse toomake disponibile nel script U-SQL e chiamare `install.packages` tooinstall è.</span><span class="sxs-lookup"><span data-stu-id="c90be-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
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

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="c90be-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c90be-146">Next Steps</span></span>
* [<span data-ttu-id="c90be-147">Panoramica di Analisi Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c90be-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="c90be-148">Sviluppare script U-SQL mediante Strumenti di Data Lake per Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c90be-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="c90be-149">Uso delle funzioni finestra di U-SQL per i processi di Analisi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c90be-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
