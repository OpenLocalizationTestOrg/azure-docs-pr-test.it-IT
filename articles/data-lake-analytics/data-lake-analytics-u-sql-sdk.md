---
title: locale aaaScale U-SQL eseguire e testare con Azure Data Lake U-SQL SDK | Documenti Microsoft
description: Informazioni su come eseguire e i test con riga di comando e le interfacce di programmazione nella workstation locale toouse processi tooscale U-SQL di Azure Data Lake U-SQL SDK locali.
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="af7e7-103">Ridimensionare esecuzione e test locali di U-SQL con l'SDK U-SQL di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="af7e7-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="af7e7-104">Quando si sviluppano script U-SQL, è toorun comuni e script di test U-SQL localmente inviare prima toocloud.</span><span class="sxs-lookup"><span data-stu-id="af7e7-104">When developing U-SQL script, it is common toorun and test U-SQL script locally before submit it toocloud.</span></span> <span data-ttu-id="af7e7-105">Per questo scenario, Azure Data Lake offre un pacchetto NuGet, denominato SDK U-SQL di Azure Data Lake, tramite cui è possibile ridimensionare facilmente l'esecuzione e il test locali di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="af7e7-106">È inoltre possibile toointegrate questo U-SQL di test con l'elemento di configurazione (integrazione continua) sistema tooautomate hello compilazione e test.</span><span class="sxs-lookup"><span data-stu-id="af7e7-106">It is also possible toointegrate this U-SQL test with CI (Continuous Integration) system tooautomate hello compile and test.</span></span>

<span data-ttu-id="af7e7-107">Se si è interessati come toomanually locale esecuzione e il debug di script U-SQL con strumenti di grafica, è possibile utilizzare Azure Data Lake Tools per Visual Studio per tale.</span><span class="sxs-lookup"><span data-stu-id="af7e7-107">If you care about how toomanually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="af7e7-108">Altre informazioni sono disponibili [qui](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="af7e7-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="af7e7-109">Installare l'SDK U-SQL di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="af7e7-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="af7e7-110">È possibile ottenere hello Azure Data Lake U-SQL SDK [qui](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) in Nuget.org. E prima di utilizzarlo, è necessario toomake che si dispone di dipendenze, come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="af7e7-110">You can get hello Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org. And before using it, you need toomake sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="af7e7-111">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="af7e7-111">Dependencies</span></span>

<span data-ttu-id="af7e7-112">Hello SDK Data Lake U-SQL, è necessario hello seguenti dipendenze:</span><span class="sxs-lookup"><span data-stu-id="af7e7-112">hello Data Lake U-SQL SDK requires hello following dependencies:</span></span>

- <span data-ttu-id="af7e7-113">[Microsoft .NET Framework 4.6 o versione successiva](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="af7e7-113">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="af7e7-114">Microsoft Visual C++ 14 e Windows SDK 10.0.10240.0 o versione successiva (CppSDK in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="af7e7-114">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="af7e7-115">Esistono due modi tooget CppSDK:</span><span class="sxs-lookup"><span data-stu-id="af7e7-115">There are two ways tooget CppSDK:</span></span>

    - <span data-ttu-id="af7e7-116">Installare [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="af7e7-116">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="af7e7-117">È una cartella \Windows Kits\10 nella cartella programmi hello - ad esempio C:\Program Files (x86) \Windows Kits\10\.</span><span class="sxs-lookup"><span data-stu-id="af7e7-117">You'll have a \Windows Kits\10 folder under hello Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="af7e7-118">Versione di Windows 10 SDK hello in \Windows Kits\10\Lib sono anche disponibili.</span><span class="sxs-lookup"><span data-stu-id="af7e7-118">You'll also find hello Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="af7e7-119">Se non viene visualizzato, le cartelle, reinstallare Visual Studio e che tooselect hello Windows 10 SDK durante l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-119">If you don’t see these folders, reinstall Visual Studio and be sure tooselect hello Windows 10 SDK during hello installation.</span></span> <span data-ttu-id="af7e7-120">Se si dispone di questo installato con Visual Studio, del compilatore locale di hello U-SQL troverà automaticamente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-120">If you have this installed with Visual Studio, hello U-SQL local compiler will find it automatically.</span></span>

    ![Windows 10 SDK ad esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="af7e7-122">Installare [Strumenti Data Lake per Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="af7e7-122">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="af7e7-123">È possibile trovare hello commercializzato solo se preconfezionato C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK file Visual C++ e Windows SDK.</span><span class="sxs-lookup"><span data-stu-id="af7e7-123">You can find hello prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="af7e7-124">In questo caso, compilatore locale di hello U-SQL non è possibile trovare dipendenze hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-124">In this case, hello U-SQL local compiler cannot find hello dependencies automatically.</span></span> <span data-ttu-id="af7e7-125">Percorso di CppSDK toospecify hello è necessario per tale.</span><span class="sxs-lookup"><span data-stu-id="af7e7-125">You need toospecify hello CppSDK path for it.</span></span> <span data-ttu-id="af7e7-126">È possibile copiare tooanother percorso dei file di hello o utilizzarla lasciandola invariata.</span><span class="sxs-lookup"><span data-stu-id="af7e7-126">You can either copy hello files tooanother location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="af7e7-127">Comprendere i concetti di base</span><span class="sxs-lookup"><span data-stu-id="af7e7-127">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="af7e7-128">Radice dei dati</span><span class="sxs-lookup"><span data-stu-id="af7e7-128">Data root</span></span>

<span data-ttu-id="af7e7-129">cartella dati radice Hello è "archivio locale" per l'account di calcolo locale hello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-129">hello data-root folder is a "local store" for hello local compute account.</span></span> <span data-ttu-id="af7e7-130">Account archivio Azure Data Lake toohello equivalente di un account Data Lake Analitica è.</span><span class="sxs-lookup"><span data-stu-id="af7e7-130">It's equivalent toohello Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="af7e7-131">Cartella radice di dati diverso cambio tooa è analoga a commutazione tooa archivio diverso account.</span><span class="sxs-lookup"><span data-stu-id="af7e7-131">Switching tooa different data-root folder is just like switching tooa different store account.</span></span> <span data-ttu-id="af7e7-132">Se si desidera tooaccess comunemente condiviso dati con le cartelle radice di dati diverso, è necessario utilizzare i percorsi assoluti negli script.</span><span class="sxs-lookup"><span data-stu-id="af7e7-132">If you want tooaccess commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="af7e7-133">In alternativa, creare collegamenti simbolici di file system (ad esempio, **mklink** in NTFS) in hello dati radice cartella toopoint toohello di dati condivisi.</span><span class="sxs-lookup"><span data-stu-id="af7e7-133">Or, create file system symbolic links (for example, **mklink** on NTFS) under hello data-root folder toopoint toohello shared data.</span></span>

<span data-ttu-id="af7e7-134">cartella dati radice Hello viene utilizzato per:</span><span class="sxs-lookup"><span data-stu-id="af7e7-134">hello data-root folder is used to:</span></span>

- <span data-ttu-id="af7e7-135">Archiviare i metadati locali, inclusi database, tabelle, funzioni con valori di tabella e assembly.</span><span class="sxs-lookup"><span data-stu-id="af7e7-135">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="af7e7-136">Cercare hello di input e i percorsi di output che sono definiti come percorsi relativi nel U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-136">Look up hello input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="af7e7-137">Utilizzando i percorsi relativi rende più semplice toodeploy il tooAzure progetti U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-137">Using relative paths makes it easier toodeploy your U-SQL projects tooAzure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="af7e7-138">Percorso dei file in U-SQL</span><span class="sxs-lookup"><span data-stu-id="af7e7-138">File path in U-SQL</span></span>

<span data-ttu-id="af7e7-139">Negli script U-SQL è possibile usare sia un percorso relativo sia un percorso assoluto locale.</span><span class="sxs-lookup"><span data-stu-id="af7e7-139">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="af7e7-140">percorso relativo di Hello è toohello relativo percorso della cartella radice di dati specificato.</span><span class="sxs-lookup"><span data-stu-id="af7e7-140">hello relative path is relative toohello specified data-root folder path.</span></span> <span data-ttu-id="af7e7-141">È consigliabile che si utilizza "/" come script compatibili con lato server hello hello toomake separatore di percorso.</span><span class="sxs-lookup"><span data-stu-id="af7e7-141">We recommend that you use "/" as hello path separator toomake your scripts compatible with hello server side.</span></span> <span data-ttu-id="af7e7-142">Di seguito sono riportati alcuni esempi di percorsi relativi e dei loro percorsi assoluti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="af7e7-142">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="af7e7-143">In questi esempi, C:\LocalRunDataRoot è cartella dati radice hello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-143">In these examples, C:\LocalRunDataRoot is hello data-root folder.</span></span>

|<span data-ttu-id="af7e7-144">Percorso relativo</span><span class="sxs-lookup"><span data-stu-id="af7e7-144">Relative path</span></span>|<span data-ttu-id="af7e7-145">Percorso assoluto</span><span class="sxs-lookup"><span data-stu-id="af7e7-145">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="af7e7-146">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="af7e7-146">/abc/def/input.csv</span></span> |<span data-ttu-id="af7e7-147">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="af7e7-147">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="af7e7-148">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="af7e7-148">abc/def/input.csv</span></span>  |<span data-ttu-id="af7e7-149">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="af7e7-149">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="af7e7-150">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="af7e7-150">D:/abc/def/input.csv</span></span> |<span data-ttu-id="af7e7-151">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="af7e7-151">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="af7e7-152">Directory di lavoro</span><span class="sxs-lookup"><span data-stu-id="af7e7-152">Working directory</span></span>

<span data-ttu-id="af7e7-153">Quando si esegue uno script U-SQL hello in locale, una directory di lavoro viene creata durante la compilazione in directory di esecuzione corrente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-153">When running hello U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="af7e7-154">Inoltre toohello compilazione restituisce, hello necessari file di runtime per l'esecuzione locale sarà directory di lavoro toothis copia shadow.</span><span class="sxs-lookup"><span data-stu-id="af7e7-154">In addition toohello compilation outputs, hello needed runtime files for local execution will be shadow copied toothis working directory.</span></span> <span data-ttu-id="af7e7-155">Hello cartella radice di directory di lavoro viene chiamato "ScopeWorkDir" e il file hello in hello directory di lavoro sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="af7e7-155">hello working directory root folder is called "ScopeWorkDir" and hello files under hello working directory are as follows:</span></span>

|<span data-ttu-id="af7e7-156">Directory/File</span><span class="sxs-lookup"><span data-stu-id="af7e7-156">Directory/file</span></span>|<span data-ttu-id="af7e7-157">Directory/File</span><span class="sxs-lookup"><span data-stu-id="af7e7-157">Directory/file</span></span>|<span data-ttu-id="af7e7-158">Directory/File</span><span class="sxs-lookup"><span data-stu-id="af7e7-158">Directory/file</span></span>|<span data-ttu-id="af7e7-159">Definizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-159">Definition</span></span>|<span data-ttu-id="af7e7-160">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-160">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="af7e7-161">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="af7e7-161">C6A101DDCB470506</span></span>| | |<span data-ttu-id="af7e7-162">Stringa di hash della versione di runtime</span><span class="sxs-lookup"><span data-stu-id="af7e7-162">Hash string of runtime version</span></span>|<span data-ttu-id="af7e7-163">Copia shadow dei file di runtime necessari per l'esecuzione locale</span><span class="sxs-lookup"><span data-stu-id="af7e7-163">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="af7e7-164">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="af7e7-164">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="af7e7-165">Nome di script + stringa hash del percorso dello script</span><span class="sxs-lookup"><span data-stu-id="af7e7-165">Script name + hash string of script path</span></span>|<span data-ttu-id="af7e7-166">Output di compilazione e registrazione del passaggio di esecuzione</span><span class="sxs-lookup"><span data-stu-id="af7e7-166">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="af7e7-167">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="af7e7-167">\_script\_.abr</span></span>|<span data-ttu-id="af7e7-168">Output del compilatore</span><span class="sxs-lookup"><span data-stu-id="af7e7-168">Compiler output</span></span>|<span data-ttu-id="af7e7-169">File algebra</span><span class="sxs-lookup"><span data-stu-id="af7e7-169">Algebra file</span></span>|
| | |<span data-ttu-id="af7e7-170">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="af7e7-170">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="af7e7-171">Output del compilatore</span><span class="sxs-lookup"><span data-stu-id="af7e7-171">Compiler output</span></span>|<span data-ttu-id="af7e7-172">Codice gestito generato</span><span class="sxs-lookup"><span data-stu-id="af7e7-172">Generated managed code</span></span>|
| | |<span data-ttu-id="af7e7-173">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="af7e7-173">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="af7e7-174">Output del compilatore</span><span class="sxs-lookup"><span data-stu-id="af7e7-174">Compiler output</span></span>|<span data-ttu-id="af7e7-175">Codice nativo generato</span><span class="sxs-lookup"><span data-stu-id="af7e7-175">Generated native code</span></span>|
| | |<span data-ttu-id="af7e7-176">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="af7e7-176">referenced assemblies</span></span>|<span data-ttu-id="af7e7-177">Riferimento assembly</span><span class="sxs-lookup"><span data-stu-id="af7e7-177">Assembly reference</span></span>|<span data-ttu-id="af7e7-178">File assembly di riferimento</span><span class="sxs-lookup"><span data-stu-id="af7e7-178">Referenced assembly files</span></span>|
| | |<span data-ttu-id="af7e7-179">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="af7e7-179">deployed_resources</span></span>|<span data-ttu-id="af7e7-180">Distribuzione risorse</span><span class="sxs-lookup"><span data-stu-id="af7e7-180">Resource deployment</span></span>|<span data-ttu-id="af7e7-181">File di distribuzione risorse</span><span class="sxs-lookup"><span data-stu-id="af7e7-181">Resource deployment files</span></span>|
| | |<span data-ttu-id="af7e7-182">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="af7e7-182">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="af7e7-183">Log di esecuzione</span><span class="sxs-lookup"><span data-stu-id="af7e7-183">Execution log</span></span>|<span data-ttu-id="af7e7-184">Log dei passaggi di esecuzione</span><span class="sxs-lookup"><span data-stu-id="af7e7-184">Log of execution steps</span></span>|


## <a name="use-hello-sdk-from-hello-command-line"></a><span data-ttu-id="af7e7-185">Utilizzare hello SDK dalla riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="af7e7-185">Use hello SDK from hello command line</span></span>

### <a name="command-line-interface-of-hello-helper-application"></a><span data-ttu-id="af7e7-186">Interfaccia della riga di comando di un'applicazione hello helper</span><span class="sxs-lookup"><span data-stu-id="af7e7-186">Command-line interface of hello helper application</span></span>

<span data-ttu-id="af7e7-187">In SDK directory\build\runtime, LocalRunHelper.exe è un'applicazione hello helper della riga di comando che fornisce interfacce funzioni toomost di hello usata esecuzione locale.</span><span class="sxs-lookup"><span data-stu-id="af7e7-187">Under SDK directory\build\runtime, LocalRunHelper.exe is hello command-line helper application that provides interfaces toomost of hello commonly used local-run functions.</span></span> <span data-ttu-id="af7e7-188">Si noti che entrambi hello comandi e opzioni dell'argomento hello tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="af7e7-188">Note that both hello command and hello argument switches are case-sensitive.</span></span> <span data-ttu-id="af7e7-189">tooinvoke è:</span><span class="sxs-lookup"><span data-stu-id="af7e7-189">tooinvoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="af7e7-190">Eseguire LocalRunHelper.exe senza argomenti oppure con hello **Guida** passare le informazioni della Guida di hello tooshow:</span><span class="sxs-lookup"><span data-stu-id="af7e7-190">Run LocalRunHelper.exe without arguments or with hello **help** switch tooshow hello help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="af7e7-191">Informazioni sul supporto in hello:</span><span class="sxs-lookup"><span data-stu-id="af7e7-191">In hello help information:</span></span>

-  <span data-ttu-id="af7e7-192">**Comando** offre hello il nome del comando.</span><span class="sxs-lookup"><span data-stu-id="af7e7-192">**Command** gives hello command’s name.</span></span>  
-  <span data-ttu-id="af7e7-193">**Argomento richiesto** elenca gli argomenti che devono essere forniti.</span><span class="sxs-lookup"><span data-stu-id="af7e7-193">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="af7e7-194">**Argomento facoltativo** elenca gli argomenti facoltativi con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="af7e7-194">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="af7e7-195">Gli argomenti booleani facoltativi non dispongono di parametri e i relativi aspetti significa valore predefinito di tootheir negativo.</span><span class="sxs-lookup"><span data-stu-id="af7e7-195">Optional Boolean arguments don’t have parameters, and their appearances mean negative tootheir default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="af7e7-196">Valore restituito e registrazione</span><span class="sxs-lookup"><span data-stu-id="af7e7-196">Return value and logging</span></span>

<span data-ttu-id="af7e7-197">Restituisce un'applicazione Hello helper **0** per l'esito positivo e **-1** per errore.</span><span class="sxs-lookup"><span data-stu-id="af7e7-197">hello helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="af7e7-198">Per impostazione predefinita, il supporto di hello invia la console corrente tutti i messaggi toohello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-198">By default, hello helper sends all messages toohello current console.</span></span> <span data-ttu-id="af7e7-199">Tuttavia, la maggior parte dei comandi di hello supportano hello **- MessageOut percorso_file_registro** argomento facoltativo che reindirizza hello genera file di log tooa.</span><span class="sxs-lookup"><span data-stu-id="af7e7-199">However, most of hello commands support hello **-MessageOut path_to_log_file** optional argument that redirects hello outputs tooa log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="af7e7-200">Configurazione della variabile di ambiente</span><span class="sxs-lookup"><span data-stu-id="af7e7-200">Environment variable configuring</span></span>

<span data-ttu-id="af7e7-201">Per l'esecuzione locale di U-SQL è necessaria una radice di dati specificata come account di archiviazione locale, oltre a un percorso CppSDK specificato per le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="af7e7-201">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="af7e7-202">È possibile sia argomento hello impostato nella variabile di ambiente della riga di comando o è impostata per loro.</span><span class="sxs-lookup"><span data-stu-id="af7e7-202">You can both set hello argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="af7e7-203">Set hello **SCOPE_CPP_SDK** variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-203">Set hello **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="af7e7-204">Se si ottengono con Microsoft Visual C++ e SDK di Windows hello installando Data Lake Tools per Visual Studio, verificare di aver hello seguente cartella:</span><span class="sxs-lookup"><span data-stu-id="af7e7-204">If you get Microsoft Visual C++ and hello Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have hello following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="af7e7-205">Definire una nuova variabile di ambiente denominata **SCOPE_CPP_SDK** toopoint toothis directory.</span><span class="sxs-lookup"><span data-stu-id="af7e7-205">Define a new environment variable called **SCOPE_CPP_SDK** toopoint toothis directory.</span></span> <span data-ttu-id="af7e7-206">O copiare hello cartella toohello altro percorso e specificare **SCOPE_CPP_SDK** come che.</span><span class="sxs-lookup"><span data-stu-id="af7e7-206">Or copy hello folder toohello other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="af7e7-207">Nella variabile di ambiente hello toosetting aggiunta, è possibile specificare hello **- CppSDK** argomento quando si utilizza la riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-207">In addition toosetting hello environment variable, you can specify hello **-CppSDK** argument when you're using hello command line.</span></span> <span data-ttu-id="af7e7-208">Questo argomento sovrascrive la variabile di ambiente CppSDK predefinita.</span><span class="sxs-lookup"><span data-stu-id="af7e7-208">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="af7e7-209">Set hello **LOCALRUN_DATAROOT** variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-209">Set hello **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="af7e7-210">Definire una nuova variabile di ambiente denominata **LOCALRUN_DATAROOT** che punta toohello radice dei dati.</span><span class="sxs-lookup"><span data-stu-id="af7e7-210">Define a new environment variable called **LOCALRUN_DATAROOT** that points toohello data root.</span></span>

    <span data-ttu-id="af7e7-211">Nella variabile di ambiente hello toosetting aggiunta, è possibile specificare hello **- DataRoot** argomento con il percorso dati radice hello quando si utilizza una riga di comando.</span><span class="sxs-lookup"><span data-stu-id="af7e7-211">In addition toosetting hello environment variable, you can specify hello **-DataRoot** argument with hello data-root path when you're using a command line.</span></span> <span data-ttu-id="af7e7-212">Questo argomento sovrascrive la variabile di ambiente data-root predefinita.</span><span class="sxs-lookup"><span data-stu-id="af7e7-212">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="af7e7-213">È necessario tooadd questa riga di comando tooevery argomento, che si esegue in modo che è possibile sovrascrivere una variabile di ambiente hello predefinita dati radice per tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="af7e7-213">You need tooadd this argument tooevery command line you're running so that you can overwrite hello default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="af7e7-214">Esempi di uso della riga di comando SDK</span><span class="sxs-lookup"><span data-stu-id="af7e7-214">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="af7e7-215">Compila ed esegui</span><span class="sxs-lookup"><span data-stu-id="af7e7-215">Compile and run</span></span>

<span data-ttu-id="af7e7-216">Hello **eseguire** comando viene utilizzato toocompile hello script ed eseguire quindi i risultati compilati.</span><span class="sxs-lookup"><span data-stu-id="af7e7-216">hello **run** command is used toocompile hello script and then execute compiled results.</span></span> <span data-ttu-id="af7e7-217">Gli argomenti della riga di comando sono una combinazione degli argomenti di **compile** ed **execute**.</span><span class="sxs-lookup"><span data-stu-id="af7e7-217">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="af7e7-218">di seguito Hello sono argomenti facoltativi per **eseguire**:</span><span class="sxs-lookup"><span data-stu-id="af7e7-218">hello following are optional arguments for **run**:</span></span>


|<span data-ttu-id="af7e7-219">Argomento</span><span class="sxs-lookup"><span data-stu-id="af7e7-219">Argument</span></span>|<span data-ttu-id="af7e7-220">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="af7e7-220">Default value</span></span>|<span data-ttu-id="af7e7-221">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-221">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="af7e7-222">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="af7e7-222">-CodeBehind</span></span>|<span data-ttu-id="af7e7-223">False</span><span class="sxs-lookup"><span data-stu-id="af7e7-223">False</span></span>|<span data-ttu-id="af7e7-224">script Hello è CS code-behind</span><span class="sxs-lookup"><span data-stu-id="af7e7-224">hello script has .cs code behind</span></span>|
|<span data-ttu-id="af7e7-225">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="af7e7-225">-CppSDK</span></span>| |<span data-ttu-id="af7e7-226">Directory CppSDK</span><span class="sxs-lookup"><span data-stu-id="af7e7-226">CppSDK Directory</span></span>|
|<span data-ttu-id="af7e7-227">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="af7e7-227">-DataRoot</span></span>| <span data-ttu-id="af7e7-228">Variabile di ambiente DataRoot</span><span class="sxs-lookup"><span data-stu-id="af7e7-228">DataRoot environment variable</span></span>|<span data-ttu-id="af7e7-229">DataRoot per l'esecuzione locale, predefinito troppo variabile di ambiente 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="af7e7-229">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="af7e7-230">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="af7e7-230">-MessageOut</span></span>| |<span data-ttu-id="af7e7-231">Messaggi di dump nel file di console tooa</span><span class="sxs-lookup"><span data-stu-id="af7e7-231">Dump messages on console tooa file</span></span>|
|<span data-ttu-id="af7e7-232">-Parallel</span><span class="sxs-lookup"><span data-stu-id="af7e7-232">-Parallel</span></span>|<span data-ttu-id="af7e7-233">1</span><span class="sxs-lookup"><span data-stu-id="af7e7-233">1</span></span>|<span data-ttu-id="af7e7-234">Eseguire hello piano con hello specificato parallelism</span><span class="sxs-lookup"><span data-stu-id="af7e7-234">Run hello plan with hello specified parallelism</span></span>|
|<span data-ttu-id="af7e7-235">-References</span><span class="sxs-lookup"><span data-stu-id="af7e7-235">-References</span></span>| |<span data-ttu-id="af7e7-236">Elenco di assembly di riferimento per i percorsi tooextra o file di dati di code-behind, separato da ';'</span><span class="sxs-lookup"><span data-stu-id="af7e7-236">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="af7e7-237">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="af7e7-237">-UdoRedirect</span></span>|<span data-ttu-id="af7e7-238">False</span><span class="sxs-lookup"><span data-stu-id="af7e7-238">False</span></span>|<span data-ttu-id="af7e7-239">Genera la configurazione di reindirizzamento di assembly Udo</span><span class="sxs-lookup"><span data-stu-id="af7e7-239">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="af7e7-240">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="af7e7-240">-UseDatabase</span></span>|<span data-ttu-id="af7e7-241">master</span><span class="sxs-lookup"><span data-stu-id="af7e7-241">master</span></span>|<span data-ttu-id="af7e7-242">Database toouse per code-behind di registrazione assembly temporaneo</span><span class="sxs-lookup"><span data-stu-id="af7e7-242">Database toouse for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="af7e7-243">-Verbose</span><span class="sxs-lookup"><span data-stu-id="af7e7-243">-Verbose</span></span>|<span data-ttu-id="af7e7-244">False</span><span class="sxs-lookup"><span data-stu-id="af7e7-244">False</span></span>|<span data-ttu-id="af7e7-245">Mostrare gli output dettagliati dal runtime</span><span class="sxs-lookup"><span data-stu-id="af7e7-245">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="af7e7-246">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-246">-WorkDir</span></span>|<span data-ttu-id="af7e7-247">Directory corrente</span><span class="sxs-lookup"><span data-stu-id="af7e7-247">Current Directory</span></span>|<span data-ttu-id="af7e7-248">Directory per l'uso del compilatore e gli output</span><span class="sxs-lookup"><span data-stu-id="af7e7-248">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="af7e7-249">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="af7e7-249">-RunScopeCEP</span></span>|<span data-ttu-id="af7e7-250">0</span><span class="sxs-lookup"><span data-stu-id="af7e7-250">0</span></span>|<span data-ttu-id="af7e7-251">ScopeCEP modalità toouse</span><span class="sxs-lookup"><span data-stu-id="af7e7-251">ScopeCEP mode toouse</span></span>|
|<span data-ttu-id="af7e7-252">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="af7e7-252">-ScopeCEPTempPath</span></span>|<span data-ttu-id="af7e7-253">temp</span><span class="sxs-lookup"><span data-stu-id="af7e7-253">temp</span></span>|<span data-ttu-id="af7e7-254">Toouse percorso temporaneo per il flusso di dati</span><span class="sxs-lookup"><span data-stu-id="af7e7-254">Temp path toouse for streaming data</span></span>|
|<span data-ttu-id="af7e7-255">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="af7e7-255">-OptFlags</span></span>| |<span data-ttu-id="af7e7-256">Elenco delimitato da virgole con i flag di ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="af7e7-256">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="af7e7-257">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="af7e7-257">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="af7e7-258">Oltre a combinazione **compilare** e **eseguire**, è possibile compilare ed eseguire file eseguibili compilato hello separatamente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-258">Besides combining **compile** and **execute**, you can compile and execute hello compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="af7e7-259">Compilare uno script U-SQL</span><span class="sxs-lookup"><span data-stu-id="af7e7-259">Compile a U-SQL script</span></span>

<span data-ttu-id="af7e7-260">Hello **compilare** comando è tooexecutables script utilizzati toocompile U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-260">hello **compile** command is used toocompile a U-SQL script tooexecutables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="af7e7-261">di seguito Hello sono argomenti facoltativi per **compilare**:</span><span class="sxs-lookup"><span data-stu-id="af7e7-261">hello following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="af7e7-262">Argomento</span><span class="sxs-lookup"><span data-stu-id="af7e7-262">Argument</span></span>|<span data-ttu-id="af7e7-263">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-263">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="af7e7-264">-CodeBehind [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="af7e7-264">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="af7e7-265">script Hello è CS code-behind</span><span class="sxs-lookup"><span data-stu-id="af7e7-265">hello script has .cs code behind</span></span>|
| <span data-ttu-id="af7e7-266">-CppSDK [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="af7e7-266">-CppSDK [default value '']</span></span>|<span data-ttu-id="af7e7-267">Directory CppSDK</span><span class="sxs-lookup"><span data-stu-id="af7e7-267">CppSDK Directory</span></span>|
| <span data-ttu-id="af7e7-268">-DataRoot [valore predefinito 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="af7e7-268">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="af7e7-269">DataRoot per l'esecuzione locale, predefinito troppo variabile di ambiente 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="af7e7-269">DataRoot for local run, default too'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="af7e7-270">-MessageOut [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="af7e7-270">-MessageOut [default value '']</span></span>|<span data-ttu-id="af7e7-271">Messaggi di dump nel file di console tooa</span><span class="sxs-lookup"><span data-stu-id="af7e7-271">Dump messages on console tooa file</span></span>|
| <span data-ttu-id="af7e7-272">-References [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="af7e7-272">-References [default value '']</span></span>|<span data-ttu-id="af7e7-273">Elenco di assembly di riferimento per i percorsi tooextra o file di dati di code-behind, separato da ';'</span><span class="sxs-lookup"><span data-stu-id="af7e7-273">List of paths tooextra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="af7e7-274">-Shallow [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="af7e7-274">-Shallow [default value 'False']</span></span>|<span data-ttu-id="af7e7-275">Compilazione superficiale</span><span class="sxs-lookup"><span data-stu-id="af7e7-275">Shallow compile</span></span>|
| <span data-ttu-id="af7e7-276">-UdoRedirect [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="af7e7-276">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="af7e7-277">Genera la configurazione di reindirizzamento di assembly Udo</span><span class="sxs-lookup"><span data-stu-id="af7e7-277">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="af7e7-278">-UseDatabase [valore predefinito 'master']</span><span class="sxs-lookup"><span data-stu-id="af7e7-278">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="af7e7-279">Database toouse per code-behind di registrazione assembly temporaneo</span><span class="sxs-lookup"><span data-stu-id="af7e7-279">Database toouse for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="af7e7-280">-WorkDir [valore predefinito 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="af7e7-280">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="af7e7-281">Directory per l'uso del compilatore e gli output</span><span class="sxs-lookup"><span data-stu-id="af7e7-281">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="af7e7-282">-RunScopeCEP [valore predefinito '0']</span><span class="sxs-lookup"><span data-stu-id="af7e7-282">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="af7e7-283">ScopeCEP modalità toouse</span><span class="sxs-lookup"><span data-stu-id="af7e7-283">ScopeCEP mode toouse</span></span>|
| <span data-ttu-id="af7e7-284">-ScopeCEPTempPath [valore predefinito 'temp']</span><span class="sxs-lookup"><span data-stu-id="af7e7-284">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="af7e7-285">Toouse percorso temporaneo per il flusso di dati</span><span class="sxs-lookup"><span data-stu-id="af7e7-285">Temp path toouse for streaming data</span></span>|
| <span data-ttu-id="af7e7-286">-OptFlags [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="af7e7-286">-OptFlags [default value '']</span></span>|<span data-ttu-id="af7e7-287">Elenco delimitato da virgole con i flag di ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="af7e7-287">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="af7e7-288">Di seguito sono riportati alcuni esempi d'uso.</span><span class="sxs-lookup"><span data-stu-id="af7e7-288">Here are some usage examples.</span></span>

<span data-ttu-id="af7e7-289">Compilare uno script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="af7e7-289">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="af7e7-290">Compilare uno script U-SQL e impostare come cartella di dati radice hello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-290">Compile a U-SQL script and set hello data-root folder.</span></span> <span data-ttu-id="af7e7-291">Si noti che ciò comporterà la sovrascrittura hello set variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-291">Note that this will overwrite hello set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="af7e7-292">Compilare uno script U-SQL e impostare la directory di lavoro, un assembly di riferimento e un database:</span><span class="sxs-lookup"><span data-stu-id="af7e7-292">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="af7e7-293">Eseguire i risultati compilati</span><span class="sxs-lookup"><span data-stu-id="af7e7-293">Execute compiled results</span></span>

<span data-ttu-id="af7e7-294">Hello **eseguire** comando viene utilizzato tooexecute compilati risultati.</span><span class="sxs-lookup"><span data-stu-id="af7e7-294">hello **execute** command is used tooexecute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="af7e7-295">di seguito Hello sono argomenti facoltativi per **eseguire**:</span><span class="sxs-lookup"><span data-stu-id="af7e7-295">hello following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="af7e7-296">Argomento</span><span class="sxs-lookup"><span data-stu-id="af7e7-296">Argument</span></span>|<span data-ttu-id="af7e7-297">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-297">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="af7e7-298">-DataRoot [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="af7e7-298">-DataRoot [default value '']</span></span>|<span data-ttu-id="af7e7-299">Radice dei dati per l'esecuzione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="af7e7-299">Data root for metadata execution.</span></span> <span data-ttu-id="af7e7-300">Il valore predefinito è toohello **LOCALRUN_DATAROOT** variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="af7e7-300">It defaults toohello **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="af7e7-301">-MessageOut [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="af7e7-301">-MessageOut [default value '']</span></span>|<span data-ttu-id="af7e7-302">I messaggi nel file di tooa console hello di dump.</span><span class="sxs-lookup"><span data-stu-id="af7e7-302">Dump messages on hello console tooa file.</span></span>|
|<span data-ttu-id="af7e7-303">-Parallel [valore predefinito '1']</span><span class="sxs-lookup"><span data-stu-id="af7e7-303">-Parallel [default value '1']</span></span>|<span data-ttu-id="af7e7-304">Indicatore toorun hello generato esecuzione locale con hello specificato il livello di parallelismo.</span><span class="sxs-lookup"><span data-stu-id="af7e7-304">Indicator toorun hello generated local-run steps with hello specified parallelism level.</span></span>|
|<span data-ttu-id="af7e7-305">-Verbose [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="af7e7-305">-Verbose [default value 'False']</span></span>|<span data-ttu-id="af7e7-306">Indicatore tooshow dettagliato restituisce dal runtime.</span><span class="sxs-lookup"><span data-stu-id="af7e7-306">Indicator tooshow detailed outputs from runtime.</span></span>|

<span data-ttu-id="af7e7-307">Ecco un esempio d'uso:</span><span class="sxs-lookup"><span data-stu-id="af7e7-307">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a><span data-ttu-id="af7e7-308">Utilizzare hello SDK con interfacce di programmazione</span><span class="sxs-lookup"><span data-stu-id="af7e7-308">Use hello SDK with programming interfaces</span></span>

<span data-ttu-id="af7e7-309">interfacce di programmazione Hello si trovano in hello LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="af7e7-309">hello programming interfaces are all located in hello LocalRunHelper.exe.</span></span> <span data-ttu-id="af7e7-310">È possibile utilizzare le funzionalità di hello toointegrate di hello SDK U-SQL e hello tooscale framework di test c# test locale script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-310">You can use them toointegrate hello functionality of hello U-SQL SDK and hello C# test framework tooscale your U-SQL script local test.</span></span> <span data-ttu-id="af7e7-311">In questo articolo, si utilizzerà hello standard c# unit test progetto tooshow come toouse queste interfacce tootest script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-311">In this article, I will use hello standard C# unit test project tooshow how toouse these interfaces tootest your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="af7e7-312">Passaggio 1: Creare configurazione e progetto per unit test C#</span><span class="sxs-lookup"><span data-stu-id="af7e7-312">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="af7e7-313">Creare un progetto per unit test C# tramite File > Nuovo > Progetto > Visual C# > Test > Progetto unit test.</span><span class="sxs-lookup"><span data-stu-id="af7e7-313">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="af7e7-314">Aggiungere LocalRunHelper.exe come riferimento per il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="af7e7-314">Add LocalRunHelper.exe as a reference for hello project.</span></span> <span data-ttu-id="af7e7-315">Hello LocalRunHelper.exe si trova in \build\runtime\LocalRunHelper.exe nel pacchetto Nuget.</span><span class="sxs-lookup"><span data-stu-id="af7e7-315">hello LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Riferimento aggiunta dell'SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="af7e7-317">U-SQL SDK **solo** ambiente supporto x64, assicurarsi che tooset compilazione destinazione della piattaforma come x64.</span><span class="sxs-lookup"><span data-stu-id="af7e7-317">U-SQL SDK **only** support x64 environment, make sure tooset build platform target as x64.</span></span> <span data-ttu-id="af7e7-318">È possibile farlo da Proprietà progetto > Build > Piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="af7e7-318">You can set that through Project Property > Build > Platform target.</span></span>

    ![Progetto configurazione x64 SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="af7e7-320">Verificare che tooset l'ambiente di test come x64.</span><span class="sxs-lookup"><span data-stu-id="af7e7-320">Make sure tooset your test environment as x64.</span></span> <span data-ttu-id="af7e7-321">In Visual Studio è possibile impostarlo tramite Test > Impostazioni test > Architettura processore predefinita > x64.</span><span class="sxs-lookup"><span data-stu-id="af7e7-321">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Ambiente di testing configurazione x64 SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="af7e7-323">Verificare che toocopy tutti i file nella directory di lavoro tooproject NugetPackage\build\runtime\ che è in genere in ProjectFolder\bin\x64\Debug dipendenza.</span><span class="sxs-lookup"><span data-stu-id="af7e7-323">Make sure toocopy all dependency files under NugetPackage\build\runtime\ tooproject working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="af7e7-324">Passaggio 2: Creare test case per lo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="af7e7-324">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="af7e7-325">Di seguito è riportato il codice di esempio hello per test di script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="af7e7-325">Below is hello sample code for U-SQL script test.</span></span> <span data-ttu-id="af7e7-326">Per i test, è necessario tooprepare script, file di input e output previsto.</span><span class="sxs-lookup"><span data-stu-id="af7e7-326">For testing, you need tooprepare scripts, input files and expected output files.</span></span>

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="af7e7-327">Interfacce di programmazione in LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="af7e7-327">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="af7e7-328">LocalRunHelper.exe fornisce interfacce di programmazione per compilazione locale U-SQL, eseguire hello, interfacce hello e così via sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="af7e7-328">LocalRunHelper.exe provides hello programming interfaces for U-SQL local compile, run, etc. hello interfaces are listed as follows.</span></span>

<span data-ttu-id="af7e7-329">**Costruttore**</span><span class="sxs-lookup"><span data-stu-id="af7e7-329">**Constructor**</span></span>

<span data-ttu-id="af7e7-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="af7e7-330">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="af7e7-331">.</span><span class="sxs-lookup"><span data-stu-id="af7e7-331">Parameter</span></span>|<span data-ttu-id="af7e7-332">Tipo</span><span class="sxs-lookup"><span data-stu-id="af7e7-332">Type</span></span>|<span data-ttu-id="af7e7-333">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-333">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="af7e7-334">messageOutput</span><span class="sxs-lookup"><span data-stu-id="af7e7-334">messageOutput</span></span>|<span data-ttu-id="af7e7-335">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="af7e7-335">System.IO.TextWriter</span></span>|<span data-ttu-id="af7e7-336">per i messaggi di output, impostare toonull toouse Console</span><span class="sxs-lookup"><span data-stu-id="af7e7-336">for output messages, set toonull toouse Console</span></span>|

<span data-ttu-id="af7e7-337">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="af7e7-337">**Properties**</span></span>

|<span data-ttu-id="af7e7-338">Proprietà</span><span class="sxs-lookup"><span data-stu-id="af7e7-338">Property</span></span>|<span data-ttu-id="af7e7-339">Tipo</span><span class="sxs-lookup"><span data-stu-id="af7e7-339">Type</span></span>|<span data-ttu-id="af7e7-340">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-340">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="af7e7-341">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="af7e7-341">AlgebraPath</span></span>|<span data-ttu-id="af7e7-342">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-342">string</span></span>|<span data-ttu-id="af7e7-343">file di Hello percorso tooalgebra (file algebra è uno dei risultati della compilazione hello)</span><span class="sxs-lookup"><span data-stu-id="af7e7-343">hello path tooalgebra file (algebra file is one of hello compilation results)</span></span>|
|<span data-ttu-id="af7e7-344">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="af7e7-344">CodeBehindReferences</span></span>|<span data-ttu-id="af7e7-345">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-345">string</span></span>|<span data-ttu-id="af7e7-346">Se script hello dispone di ulteriori code-behind riferimenti, specificare i percorsi di hello separati da ';'</span><span class="sxs-lookup"><span data-stu-id="af7e7-346">If hello script has additional code behind references, specify hello paths separated with ';'</span></span>|
|<span data-ttu-id="af7e7-347">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-347">CppSdkDir</span></span>|<span data-ttu-id="af7e7-348">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-348">string</span></span>|<span data-ttu-id="af7e7-349">Directory CppSDK</span><span class="sxs-lookup"><span data-stu-id="af7e7-349">CppSDK directory</span></span>|
|<span data-ttu-id="af7e7-350">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-350">CurrentDir</span></span>|<span data-ttu-id="af7e7-351">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-351">string</span></span>|<span data-ttu-id="af7e7-352">La directory corrente</span><span class="sxs-lookup"><span data-stu-id="af7e7-352">Current directory</span></span>|
|<span data-ttu-id="af7e7-353">DataRoot</span><span class="sxs-lookup"><span data-stu-id="af7e7-353">DataRoot</span></span>|<span data-ttu-id="af7e7-354">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-354">string</span></span>|<span data-ttu-id="af7e7-355">Il percorso della radice dei dati</span><span class="sxs-lookup"><span data-stu-id="af7e7-355">Data root path</span></span>|
|<span data-ttu-id="af7e7-356">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="af7e7-356">DebuggerMailPath</span></span>|<span data-ttu-id="af7e7-357">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-357">string</span></span>|<span data-ttu-id="af7e7-358">Hello percorso toodebugger mailslot</span><span class="sxs-lookup"><span data-stu-id="af7e7-358">hello path toodebugger mailslot</span></span>|
|<span data-ttu-id="af7e7-359">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="af7e7-359">GenerateUdoRedirect</span></span>|<span data-ttu-id="af7e7-360">bool</span><span class="sxs-lookup"><span data-stu-id="af7e7-360">bool</span></span>|<span data-ttu-id="af7e7-361">Se lo si desidera il caricamento degli assembly toogenerate reindirizzamento esegue l'override di configurazione</span><span class="sxs-lookup"><span data-stu-id="af7e7-361">If we want toogenerate assembly loading redirection override config</span></span>|
|<span data-ttu-id="af7e7-362">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="af7e7-362">HasCodeBehind</span></span>|<span data-ttu-id="af7e7-363">bool</span><span class="sxs-lookup"><span data-stu-id="af7e7-363">bool</span></span>|<span data-ttu-id="af7e7-364">Se lo script hello è code-behind</span><span class="sxs-lookup"><span data-stu-id="af7e7-364">If hello script has code behind</span></span>|
|<span data-ttu-id="af7e7-365">InputDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-365">InputDir</span></span>|<span data-ttu-id="af7e7-366">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-366">string</span></span>|<span data-ttu-id="af7e7-367">La directory per i dati di input</span><span class="sxs-lookup"><span data-stu-id="af7e7-367">Directory for input data</span></span>|
|<span data-ttu-id="af7e7-368">MessagePath</span><span class="sxs-lookup"><span data-stu-id="af7e7-368">MessagePath</span></span>|<span data-ttu-id="af7e7-369">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-369">string</span></span>|<span data-ttu-id="af7e7-370">Il percorso del file dump del messaggio</span><span class="sxs-lookup"><span data-stu-id="af7e7-370">Message dump file path</span></span>|
|<span data-ttu-id="af7e7-371">OutputDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-371">OutputDir</span></span>|<span data-ttu-id="af7e7-372">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-372">string</span></span>|<span data-ttu-id="af7e7-373">La directory per i dati di output</span><span class="sxs-lookup"><span data-stu-id="af7e7-373">Directory for output data</span></span>|
|<span data-ttu-id="af7e7-374">Parallelismo</span><span class="sxs-lookup"><span data-stu-id="af7e7-374">Parallelism</span></span>|<span data-ttu-id="af7e7-375">int</span><span class="sxs-lookup"><span data-stu-id="af7e7-375">int</span></span>|<span data-ttu-id="af7e7-376">Algebra hello toorun di parallelismo</span><span class="sxs-lookup"><span data-stu-id="af7e7-376">Parallelism toorun hello algebra</span></span>|
|<span data-ttu-id="af7e7-377">ParentPid</span><span class="sxs-lookup"><span data-stu-id="af7e7-377">ParentPid</span></span>|<span data-ttu-id="af7e7-378">int</span><span class="sxs-lookup"><span data-stu-id="af7e7-378">int</span></span>|<span data-ttu-id="af7e7-379">PID del padre hello in cui hello servizio controlla tooexit, set too0 o tooignore negativo</span><span class="sxs-lookup"><span data-stu-id="af7e7-379">PID of hello parent on which hello service monitors tooexit, set too0 or negative tooignore</span></span>|
|<span data-ttu-id="af7e7-380">ResultPath</span><span class="sxs-lookup"><span data-stu-id="af7e7-380">ResultPath</span></span>|<span data-ttu-id="af7e7-381">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-381">string</span></span>|<span data-ttu-id="af7e7-382">Il percorso del file dump del risultato</span><span class="sxs-lookup"><span data-stu-id="af7e7-382">Result dump file path</span></span>|
|<span data-ttu-id="af7e7-383">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-383">RuntimeDir</span></span>|<span data-ttu-id="af7e7-384">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-384">string</span></span>|<span data-ttu-id="af7e7-385">La directory di runtime</span><span class="sxs-lookup"><span data-stu-id="af7e7-385">Runtime directory</span></span>|
|<span data-ttu-id="af7e7-386">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="af7e7-386">ScriptPath</span></span>|<span data-ttu-id="af7e7-387">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-387">string</span></span>|<span data-ttu-id="af7e7-388">Dove toofind hello script</span><span class="sxs-lookup"><span data-stu-id="af7e7-388">Where toofind hello script</span></span>|
|<span data-ttu-id="af7e7-389">Shallow</span><span class="sxs-lookup"><span data-stu-id="af7e7-389">Shallow</span></span>|<span data-ttu-id="af7e7-390">bool</span><span class="sxs-lookup"><span data-stu-id="af7e7-390">bool</span></span>|<span data-ttu-id="af7e7-391">Indica se la compilazione è superficiale o no</span><span class="sxs-lookup"><span data-stu-id="af7e7-391">Shallow compile or not</span></span>|
|<span data-ttu-id="af7e7-392">TempDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-392">TempDir</span></span>|<span data-ttu-id="af7e7-393">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-393">string</span></span>|<span data-ttu-id="af7e7-394">Directory Temp</span><span class="sxs-lookup"><span data-stu-id="af7e7-394">Temp directory</span></span>|
|<span data-ttu-id="af7e7-395">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="af7e7-395">UseDataBase</span></span>|<span data-ttu-id="af7e7-396">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-396">string</span></span>|<span data-ttu-id="af7e7-397">Specificare hello database toouse per code-behind di registrazione di assembly temporaneo, master per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="af7e7-397">Specify hello database toouse for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="af7e7-398">WorkDir</span><span class="sxs-lookup"><span data-stu-id="af7e7-398">WorkDir</span></span>|<span data-ttu-id="af7e7-399">string</span><span class="sxs-lookup"><span data-stu-id="af7e7-399">string</span></span>|<span data-ttu-id="af7e7-400">La directory di lavoro preferita</span><span class="sxs-lookup"><span data-stu-id="af7e7-400">Preferred working directory</span></span>|


<span data-ttu-id="af7e7-401">**Metodo**</span><span class="sxs-lookup"><span data-stu-id="af7e7-401">**Method**</span></span>

|<span data-ttu-id="af7e7-402">Metodo</span><span class="sxs-lookup"><span data-stu-id="af7e7-402">Method</span></span>|<span data-ttu-id="af7e7-403">Descrizione</span><span class="sxs-lookup"><span data-stu-id="af7e7-403">Description</span></span>|<span data-ttu-id="af7e7-404">Return</span><span class="sxs-lookup"><span data-stu-id="af7e7-404">Return</span></span>|<span data-ttu-id="af7e7-405">.</span><span class="sxs-lookup"><span data-stu-id="af7e7-405">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="af7e7-406">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="af7e7-406">public bool DoCompile()</span></span>|<span data-ttu-id="af7e7-407">Compilare script di hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="af7e7-407">Compile hello U-SQL script</span></span>|<span data-ttu-id="af7e7-408">Se l'esito è positivo, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="af7e7-408">True on success</span></span>| |
|<span data-ttu-id="af7e7-409">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="af7e7-409">public bool DoExec()</span></span>|<span data-ttu-id="af7e7-410">Esecuzione del risultato hello compilato</span><span class="sxs-lookup"><span data-stu-id="af7e7-410">Execute hello compiled result</span></span>|<span data-ttu-id="af7e7-411">Se l'esito è positivo, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="af7e7-411">True on success</span></span>| |
|<span data-ttu-id="af7e7-412">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="af7e7-412">public bool DoRun()</span></span>|<span data-ttu-id="af7e7-413">Eseguire script hello U-SQL (compilazione + Execute)</span><span class="sxs-lookup"><span data-stu-id="af7e7-413">Run hello U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="af7e7-414">Se l'esito è positivo, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="af7e7-414">True on success</span></span>| |
|<span data-ttu-id="af7e7-415">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="af7e7-415">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="af7e7-416">Verificare se un determinato percorso hello è il percorso di runtime valido</span><span class="sxs-lookup"><span data-stu-id="af7e7-416">Check if hello given path is valid runtime path</span></span>|<span data-ttu-id="af7e7-417">Se è valido, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="af7e7-417">True for valid</span></span>|<span data-ttu-id="af7e7-418">percorso di Hello della directory di runtime</span><span class="sxs-lookup"><span data-stu-id="af7e7-418">hello path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="af7e7-419">Domande frequenti sui problemi comuni</span><span class="sxs-lookup"><span data-stu-id="af7e7-419">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="af7e7-420">Errore 1:</span><span class="sxs-lookup"><span data-stu-id="af7e7-420">Error 1:</span></span>
<span data-ttu-id="af7e7-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span><span class="sxs-lookup"><span data-stu-id="af7e7-421">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="af7e7-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span><span class="sxs-lookup"><span data-stu-id="af7e7-422">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="af7e7-423">modulo specificato Hello non trovato.</span><span class="sxs-lookup"><span data-stu-id="af7e7-423">hello specified module could not be found.</span></span>

<span data-ttu-id="af7e7-424">Verificare i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="af7e7-424">Please check hello following:</span></span>

- <span data-ttu-id="af7e7-425">Assicurarsi di avere un ambiente x64.</span><span class="sxs-lookup"><span data-stu-id="af7e7-425">Make sure you have x64 environment.</span></span> <span data-ttu-id="af7e7-426">piattaforma di destinazione di compilazione Hello e ambiente di test hello deve essere x64, fare riferimento troppo**passaggio 1: c# creare unit test del progetto e la configurazione** sopra.</span><span class="sxs-lookup"><span data-stu-id="af7e7-426">hello build target platform and hello test environment should be x64, refer too**Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="af7e7-427">Assicurarsi di che aver copiato tutti i file nella directory di lavoro tooproject NugetPackage\build\runtime\ dipendenza.</span><span class="sxs-lookup"><span data-stu-id="af7e7-427">Make sure you have copied all dependency files under NugetPackage\build\runtime\ tooproject working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="af7e7-428">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="af7e7-428">Next steps</span></span>

* <span data-ttu-id="af7e7-429">toolearn U-SQL, vedere [Guida introduttiva di Azure Data Lake Analitica U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="af7e7-429">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="af7e7-430">informazioni di diagnostica toolog, vedere [accesso ai log di diagnostica per Azure Data Lake Analitica](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="af7e7-430">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="af7e7-431">toosee una query più complessa, vedere [analizzare i log di sito Web usando Azure Data Lake Analitica](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="af7e7-431">toosee a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="af7e7-432">vedere i dettagli dei processi, tooview [Browser di processo di utilizzo e visualizzazione dei processi per i processi di Azure Data Lake Analitica](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="af7e7-432">tooview job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="af7e7-433">visualizzazione di esecuzione vertice hello toouse, vedere [hello utilizzare Visualizzazione esecuzione vertice in Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="af7e7-433">toouse hello vertex execution view, see [Use hello Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
