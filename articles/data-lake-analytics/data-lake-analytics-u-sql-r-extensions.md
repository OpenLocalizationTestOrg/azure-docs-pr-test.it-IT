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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Esercitazione: Introduzione all'estensione di U-SQL con R

Hello di esempio seguente illustra i passaggi di base per la distribuzione di codice R hello:
* Hello utilizzare `REFERENCE ASSEMBLY` estensioni tooenable R istruzione per hello Script U-SQL.
* Utilizzare il` REDUCE` hello toopartition operazione dati su una chiave di input.
* le estensioni di Hello R U-SQL includono un riduttore incorporato (`Extension.R.Reducer`) che esegue codice R in ogni riduttore toohello vertice assegnato. 
* Utilizzo di dedicato denominato frame di dati denominati `inputFromUSQL` e `outputToUSQL `rispettivamente toopass dati tra U-SQL e R. Input e output vengono corretti i nomi degli identificatori di frame di dati (vale a dire gli utenti non è possibile modificare questi nomi predefiniti dell'input e frame di dati di output identificatori).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>Incorporare codice R in hello script U-SQL

È possibile codice hello R inline script U-SQL utilizzando il parametro di comando hello di hello `Extension.R.Reducer`. Ad esempio, è possibile dichiarare hello script R come una variabile di stringa e passarlo come toohello un parametro del Reducer.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Conservare il codice hello R in un file separato e farvi riferimento script hello U-SQL

Hello di esempio seguente viene illustrato un utilizzo più complesso. In questo caso, il codice R hello viene distribuito come una risorsa che è hello script U-SQL.

Salvare il codice R come file separato.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Utilizzare un toodeploy script U-SQL script R con hello istruzione distribuire risorse.

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

## <a name="how-r-integrates-with-u-sql"></a>Come R si integra con U-SQL

### <a name="datatypes"></a>Tipi di dati
* Le colonne di tipo stringa e numeriche di U-SQL vengono convertite così come sono tra DataFrame R e U-SQL [tipi supportati: `double`, `string`, `bool`, `integer`, `byte`].
* Hello `Factor` tipo di dati non è supportato in U-SQL.
* `byte[]` deve essere serializzato come `string` con codifica Base 64.
* U-SQL le stringhe possono essere convertiti toofactors nel codice R, una volta U-SQL create input frame di dati R dall'impostazione parametro riduttore hello `stringsAsFactors: true`.

### <a name="schemas"></a>Schemi
* I set di dati di U-SQL non possono avere nomi di colonna duplicati.
* I nomi di colonna dei set di dati di U-SQL devono essere stringhe.
* I nomi di colonna deve essere hello stesso negli script U-SQL e R.
* Colonna di sola lettura non può far parte di hello dataframe di output. Poiché le colonne di sola lettura vengono inserite automaticamente nella tabella di hello U-SQL se fa parte dello schema di output dell'operatore definito dall'utente.

### <a name="functional-limitations"></a>Limitazioni funzionali
* Hello motore R non è possibile creare due volte in hello stesso processo. 
* Attualmente, U-SQL non supporta UDO Combiner per la stima mediante modelli partizionati generati usando UDO Reducer. Gli utenti possono dichiarare i modelli di hello partizionata come risorse e utilizzarle nei loro Script di R (vedere il codice di esempio `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>Versioni R
È supportato solo R 3.2.2.

### <a name="standard-r-modules"></a>Moduli R standard

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

### <a name="input-and-output-size-limitations"></a>Limitazioni delle dimensioni di input e output
Ogni vertice ha una quantità limitata di memoria assegnata tooit. Poiché hello frame di dati di input e output devono essere presenti in memoria nel codice hello R, dimensione totale di hello per hello input e output non può superare i 500 MB.

### <a name="sample-code"></a>Codice di esempio
Dopo aver installato le estensioni di hello Analitica avanzate U-SQL, è disponibile nell'account archivio Data Lake ulteriori esempi di codice. percorso di Hello per ulteriori esempi di codice è: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Distribuzione dei moduli personalizzati R con U-SQL

Innanzitutto, creare un modulo personalizzato R e zip e quindi caricare hello compresso archivio ADL tooyour file modulo personalizzato di R. Nell'esempio hello, si caricheranno magittr_1.5.zip toohello principale dell'account ADLS hello predefinito per l'account ADLA usiamo hello. Dopo aver caricato l'archivio di tooADL modulo hello, dichiararla come distribuire risorse toomake disponibile nel script U-SQL e chiamare `install.packages` tooinstall è.

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

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica di Analisi Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Sviluppare script U-SQL mediante Strumenti di Data Lake per Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Uso delle funzioni finestra di U-SQL per i processi di Analisi Azure Data Lake](data-lake-analytics-use-window-functions.md)
