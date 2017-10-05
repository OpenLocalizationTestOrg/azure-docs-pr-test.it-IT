---
title: Ridimensionare esecuzione e test locali di U-SQL con l'SDK U-SQL di Azure Data Lake | Microsoft Docs
description: Informazioni su come usare l'SDK U-SQL di Azure Data Lake per ridimensionare l'esecuzione e il test locali di processi U-SQL con le interfacce di programmazione e della riga di comando nella workstation locale.
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
ms.openlocfilehash: 55242bcf644ca0e7f30cfe7eada2130451c36e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="a6294-103">Ridimensionare esecuzione e test locali di U-SQL con l'SDK U-SQL di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a6294-103">Scale U-SQL local run and test with Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="a6294-104">Durante lo sviluppo di script U-SQL, è comune eseguire e testare a livello locale gli script U-SQL prima di inviarli al cloud.</span><span class="sxs-lookup"><span data-stu-id="a6294-104">When developing U-SQL script, it is common to run and test U-SQL script locally before submit it to cloud.</span></span> <span data-ttu-id="a6294-105">Per questo scenario, Azure Data Lake offre un pacchetto NuGet, denominato SDK U-SQL di Azure Data Lake, tramite cui è possibile ridimensionare facilmente l'esecuzione e il test locali di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6294-105">Azure Data Lake provides a Nuget package called Azure Data Lake U-SQL SDK for this scenario, through which you can easily scale U-SQL local run and test.</span></span> <span data-ttu-id="a6294-106">È inoltre possibile integrare questo test di U-SQL con il sistema CI (Continuous Integration, integrazione continua) per automatizzare la compilazione e il test.</span><span class="sxs-lookup"><span data-stu-id="a6294-106">It is also possible to integrate this U-SQL test with CI (Continuous Integration) system to automate the compile and test.</span></span>

<span data-ttu-id="a6294-107">Per capire come eseguire in locale manualmente ed eseguire il debug di uno script U-SQL con gli strumenti della GUI, è possibile usare gli Strumenti Azure Data Lake per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a6294-107">If you care about how to manually local run and debug U-SQL script with GUI tooling, then you can use Azure Data Lake Tools for Visual Studio for that.</span></span> <span data-ttu-id="a6294-108">Altre informazioni sono disponibili [qui](data-lake-analytics-data-lake-tools-local-run.md).</span><span class="sxs-lookup"><span data-stu-id="a6294-108">You can learn more from [here](data-lake-analytics-data-lake-tools-local-run.md).</span></span>

## <a name="install-azure-data-lake-u-sql-sdk"></a><span data-ttu-id="a6294-109">Installare l'SDK U-SQL di Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a6294-109">Install Azure Data Lake U-SQL SDK</span></span>

<span data-ttu-id="a6294-110">È possibile ottenere l'SDK U-SQL di Azure Data Lake [qui](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) su Nuget.org.</span><span class="sxs-lookup"><span data-stu-id="a6294-110">You can get the Azure Data Lake U-SQL SDK [here](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) on Nuget.org.</span></span> <span data-ttu-id="a6294-111">Prima di usarlo, è necessario assicurarsi di avere le dipendenze indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="a6294-111">And before using it, you need to make sure you have dependencies as follows.</span></span>

### <a name="dependencies"></a><span data-ttu-id="a6294-112">Dipendenze</span><span class="sxs-lookup"><span data-stu-id="a6294-112">Dependencies</span></span>

<span data-ttu-id="a6294-113">L'SDK U-SQL di Data Lake richiede le dipendenze seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6294-113">The Data Lake U-SQL SDK requires the following dependencies:</span></span>

- <span data-ttu-id="a6294-114">[Microsoft .NET Framework 4.6 o versione successiva](https://www.microsoft.com/download/details.aspx?id=17851).</span><span class="sxs-lookup"><span data-stu-id="a6294-114">[Microsoft .NET Framework 4.6 or newer](https://www.microsoft.com/download/details.aspx?id=17851).</span></span>
- <span data-ttu-id="a6294-115">Microsoft Visual C++ 14 e Windows SDK 10.0.10240.0 o versione successiva (CppSDK in questo articolo).</span><span class="sxs-lookup"><span data-stu-id="a6294-115">Microsoft Visual C++ 14 and Windows SDK 10.0.10240.0 or newer (which is called CppSDK in this article).</span></span> <span data-ttu-id="a6294-116">Esistono due modi per ottenerlo:</span><span class="sxs-lookup"><span data-stu-id="a6294-116">There are two ways to get CppSDK:</span></span>

    - <span data-ttu-id="a6294-117">Installare [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span><span class="sxs-lookup"><span data-stu-id="a6294-117">Install [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou).</span></span> <span data-ttu-id="a6294-118">Sarà presente la cartella \Windows Kits\10 sotto la cartella Programmi, ad esempio C:\Programmi (x86)\Windows Kits\10.</span><span class="sxs-lookup"><span data-stu-id="a6294-118">You'll have a \Windows Kits\10 folder under the Program Files folder--for example, C:\Program Files (x86)\Windows Kits\10\.</span></span> <span data-ttu-id="a6294-119">Sarà disponibile anche la versione Windows 10 SDK in \Windows Kits\10\Lib.</span><span class="sxs-lookup"><span data-stu-id="a6294-119">You'll also find the Windows 10 SDK version under \Windows Kits\10\Lib.</span></span> <span data-ttu-id="a6294-120">Se queste cartelle non sono presenti, reinstallare Visual Studio e selezionare Windows 10 SDK durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="a6294-120">If you don’t see these folders, reinstall Visual Studio and be sure to select the Windows 10 SDK during the installation.</span></span> <span data-ttu-id="a6294-121">Se è installato con Visual Studio, verrà trovato automaticamente dal compilatore locale U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6294-121">If you have this installed with Visual Studio, the U-SQL local compiler will find it automatically.</span></span>

    ![Windows 10 SDK ad esecuzione locale degli strumenti di Data Lake per Visual Studio](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - <span data-ttu-id="a6294-123">Installare [Strumenti Data Lake per Visual Studio](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="a6294-123">Install [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="a6294-124">I file di Windows SDK e Visual C++ preassemblati sono disponibili in C:\Programmi (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span><span class="sxs-lookup"><span data-stu-id="a6294-124">You can find the prepackaged Visual C++ and Windows SDK files at C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK.</span></span> <span data-ttu-id="a6294-125">In questo caso il compilazione locale di U-SQL non è in grado di trovare le dipendenze automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a6294-125">In this case, the U-SQL local compiler cannot find the dependencies automatically.</span></span> <span data-ttu-id="a6294-126">È necessario specificare il relativo percorso CppSDK.</span><span class="sxs-lookup"><span data-stu-id="a6294-126">You need to specify the CppSDK path for it.</span></span> <span data-ttu-id="a6294-127">È possibile copiare i file in un altro percorso o usarli così come sono.</span><span class="sxs-lookup"><span data-stu-id="a6294-127">You can either copy the files to another location or use it as is.</span></span>

## <a name="understand-basic-concepts"></a><span data-ttu-id="a6294-128">Comprendere i concetti di base</span><span class="sxs-lookup"><span data-stu-id="a6294-128">Understand basic concepts</span></span>

### <a name="data-root"></a><span data-ttu-id="a6294-129">Radice dei dati</span><span class="sxs-lookup"><span data-stu-id="a6294-129">Data root</span></span>

<span data-ttu-id="a6294-130">La cartella data-root è un "archivio locale" per l'account di calcolo locale,</span><span class="sxs-lookup"><span data-stu-id="a6294-130">The data-root folder is a "local store" for the local compute account.</span></span> <span data-ttu-id="a6294-131">equivalente all'account di Azure Data Lake Store di un account Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6294-131">It's equivalent to the Azure Data Lake Store account of a Data Lake Analytics account.</span></span> <span data-ttu-id="a6294-132">Il passaggio a un'altra cartella data-root è identico al passaggio a un account archivio differente.</span><span class="sxs-lookup"><span data-stu-id="a6294-132">Switching to a different data-root folder is just like switching to a different store account.</span></span> <span data-ttu-id="a6294-133">Se si vuole accedere a dati comunemente condivisi con cartelle data-root diverse, è necessario usare percorsi assoluti negli script.</span><span class="sxs-lookup"><span data-stu-id="a6294-133">If you want to access commonly shared data with different data-root folders, you must use absolute paths in your scripts.</span></span> <span data-ttu-id="a6294-134">In alternativa è possibile creare collegamenti simbolici del file system (ad esempio **mklink** in un sistema NTFS) nella cartella data-root che puntino ai dati condivisi.</span><span class="sxs-lookup"><span data-stu-id="a6294-134">Or, create file system symbolic links (for example, **mklink** on NTFS) under the data-root folder to point to the shared data.</span></span>

<span data-ttu-id="a6294-135">La cartella data-root viene usata per:</span><span class="sxs-lookup"><span data-stu-id="a6294-135">The data-root folder is used to:</span></span>

- <span data-ttu-id="a6294-136">Archiviare i metadati locali, inclusi database, tabelle, funzioni con valori di tabella e assembly.</span><span class="sxs-lookup"><span data-stu-id="a6294-136">Store local metadata, including databases, tables, table-valued functions (TVFs), and assemblies.</span></span>
- <span data-ttu-id="a6294-137">Cercare i percorsi di input e output che sono definiti come percorsi relativi in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6294-137">Look up the input and output paths that are defined as relative paths in U-SQL.</span></span> <span data-ttu-id="a6294-138">L'uso di percorsi relativi semplifica la distribuzione dei progetti di U-SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6294-138">Using relative paths makes it easier to deploy your U-SQL projects to Azure.</span></span>

### <a name="file-path-in-u-sql"></a><span data-ttu-id="a6294-139">Percorso dei file in U-SQL</span><span class="sxs-lookup"><span data-stu-id="a6294-139">File path in U-SQL</span></span>

<span data-ttu-id="a6294-140">Negli script U-SQL è possibile usare sia un percorso relativo sia un percorso assoluto locale.</span><span class="sxs-lookup"><span data-stu-id="a6294-140">You can use both a relative path and a local absolute path in U-SQL scripts.</span></span> <span data-ttu-id="a6294-141">Il percorso relativo è relativo al percorso della cartella data-root specificato.</span><span class="sxs-lookup"><span data-stu-id="a6294-141">The relative path is relative to the specified data-root folder path.</span></span> <span data-ttu-id="a6294-142">È consigliabile usare "/" come separatore del percorso per rendere gli script compatibili con il lato server.</span><span class="sxs-lookup"><span data-stu-id="a6294-142">We recommend that you use "/" as the path separator to make your scripts compatible with the server side.</span></span> <span data-ttu-id="a6294-143">Di seguito sono riportati alcuni esempi di percorsi relativi e dei loro percorsi assoluti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="a6294-143">Here are some examples of relative paths and their equivalent absolute paths.</span></span> <span data-ttu-id="a6294-144">In questi esempi la cartella data-root è C:\LocalRunDataRoot.</span><span class="sxs-lookup"><span data-stu-id="a6294-144">In these examples, C:\LocalRunDataRoot is the data-root folder.</span></span>

|<span data-ttu-id="a6294-145">Percorso relativo</span><span class="sxs-lookup"><span data-stu-id="a6294-145">Relative path</span></span>|<span data-ttu-id="a6294-146">Percorso assoluto</span><span class="sxs-lookup"><span data-stu-id="a6294-146">Absolute path</span></span>|
|-------------|-------------|
|<span data-ttu-id="a6294-147">/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="a6294-147">/abc/def/input.csv</span></span> |<span data-ttu-id="a6294-148">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="a6294-148">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="a6294-149">abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="a6294-149">abc/def/input.csv</span></span>  |<span data-ttu-id="a6294-150">C:\LocalRunDataRoot\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="a6294-150">C:\LocalRunDataRoot\abc\def\input.csv</span></span>|
|<span data-ttu-id="a6294-151">D:/abc/def/input.csv</span><span class="sxs-lookup"><span data-stu-id="a6294-151">D:/abc/def/input.csv</span></span> |<span data-ttu-id="a6294-152">D:\abc\def\input.csv</span><span class="sxs-lookup"><span data-stu-id="a6294-152">D:\abc\def\input.csv</span></span>|

### <a name="working-directory"></a><span data-ttu-id="a6294-153">Directory di lavoro</span><span class="sxs-lookup"><span data-stu-id="a6294-153">Working directory</span></span>

<span data-ttu-id="a6294-154">Quando si esegue lo script U-SQL localmente, durante la compilazione viene creata una directory di lavoro nella directory di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="a6294-154">When running the U-SQL script locally, a working directory is created during compilation under current running directory.</span></span> <span data-ttu-id="a6294-155">Oltre agli output di compilazione, nella directory di lavoro verrà creata una copia shadow dei file di runtime necessari per l'esecuzione locale.</span><span class="sxs-lookup"><span data-stu-id="a6294-155">In addition to the compilation outputs, the needed runtime files for local execution will be shadow copied to this working directory.</span></span> <span data-ttu-id="a6294-156">La cartella radice della directory di lavoro è denominata "ScopeWorkDir" e i file nella directory di lavoro sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6294-156">The working directory root folder is called "ScopeWorkDir" and the files under the working directory are as follows:</span></span>

|<span data-ttu-id="a6294-157">Directory/File</span><span class="sxs-lookup"><span data-stu-id="a6294-157">Directory/file</span></span>|<span data-ttu-id="a6294-158">Directory/File</span><span class="sxs-lookup"><span data-stu-id="a6294-158">Directory/file</span></span>|<span data-ttu-id="a6294-159">Directory/File</span><span class="sxs-lookup"><span data-stu-id="a6294-159">Directory/file</span></span>|<span data-ttu-id="a6294-160">Definizione</span><span class="sxs-lookup"><span data-stu-id="a6294-160">Definition</span></span>|<span data-ttu-id="a6294-161">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-161">Description</span></span>|
|--------------|--------------|--------------|----------|-----------|
|<span data-ttu-id="a6294-162">C6A101DDCB470506</span><span class="sxs-lookup"><span data-stu-id="a6294-162">C6A101DDCB470506</span></span>| | |<span data-ttu-id="a6294-163">Stringa di hash della versione di runtime</span><span class="sxs-lookup"><span data-stu-id="a6294-163">Hash string of runtime version</span></span>|<span data-ttu-id="a6294-164">Copia shadow dei file di runtime necessari per l'esecuzione locale</span><span class="sxs-lookup"><span data-stu-id="a6294-164">Shadow copy of runtime files needed for local execution</span></span>|
| |<span data-ttu-id="a6294-165">Script_66AE4909AA0ED06C</span><span class="sxs-lookup"><span data-stu-id="a6294-165">Script_66AE4909AA0ED06C</span></span>| |<span data-ttu-id="a6294-166">Nome di script + stringa hash del percorso dello script</span><span class="sxs-lookup"><span data-stu-id="a6294-166">Script name + hash string of script path</span></span>|<span data-ttu-id="a6294-167">Output di compilazione e registrazione del passaggio di esecuzione</span><span class="sxs-lookup"><span data-stu-id="a6294-167">Compilation outputs and execution step logging</span></span>|
| | |<span data-ttu-id="a6294-168">\_script\_.abr</span><span class="sxs-lookup"><span data-stu-id="a6294-168">\_script\_.abr</span></span>|<span data-ttu-id="a6294-169">Output del compilatore</span><span class="sxs-lookup"><span data-stu-id="a6294-169">Compiler output</span></span>|<span data-ttu-id="a6294-170">File algebra</span><span class="sxs-lookup"><span data-stu-id="a6294-170">Algebra file</span></span>|
| | |<span data-ttu-id="a6294-171">\_ScopeCodeGen\_.*</span><span class="sxs-lookup"><span data-stu-id="a6294-171">\_ScopeCodeGen\_.*</span></span>|<span data-ttu-id="a6294-172">Output del compilatore</span><span class="sxs-lookup"><span data-stu-id="a6294-172">Compiler output</span></span>|<span data-ttu-id="a6294-173">Codice gestito generato</span><span class="sxs-lookup"><span data-stu-id="a6294-173">Generated managed code</span></span>|
| | |<span data-ttu-id="a6294-174">\_ScopeCodeGenEngine\_.*</span><span class="sxs-lookup"><span data-stu-id="a6294-174">\_ScopeCodeGenEngine\_.*</span></span>|<span data-ttu-id="a6294-175">Output del compilatore</span><span class="sxs-lookup"><span data-stu-id="a6294-175">Compiler output</span></span>|<span data-ttu-id="a6294-176">Codice nativo generato</span><span class="sxs-lookup"><span data-stu-id="a6294-176">Generated native code</span></span>|
| | |<span data-ttu-id="a6294-177">referenced assemblies</span><span class="sxs-lookup"><span data-stu-id="a6294-177">referenced assemblies</span></span>|<span data-ttu-id="a6294-178">Riferimento assembly</span><span class="sxs-lookup"><span data-stu-id="a6294-178">Assembly reference</span></span>|<span data-ttu-id="a6294-179">File assembly di riferimento</span><span class="sxs-lookup"><span data-stu-id="a6294-179">Referenced assembly files</span></span>|
| | |<span data-ttu-id="a6294-180">deployed_resources</span><span class="sxs-lookup"><span data-stu-id="a6294-180">deployed_resources</span></span>|<span data-ttu-id="a6294-181">Distribuzione risorse</span><span class="sxs-lookup"><span data-stu-id="a6294-181">Resource deployment</span></span>|<span data-ttu-id="a6294-182">File di distribuzione risorse</span><span class="sxs-lookup"><span data-stu-id="a6294-182">Resource deployment files</span></span>|
| | |<span data-ttu-id="a6294-183">xxxxxxxx.xxx[1..n]\_\*.*</span><span class="sxs-lookup"><span data-stu-id="a6294-183">xxxxxxxx.xxx[1..n]\_\*.*</span></span>|<span data-ttu-id="a6294-184">Log di esecuzione</span><span class="sxs-lookup"><span data-stu-id="a6294-184">Execution log</span></span>|<span data-ttu-id="a6294-185">Log dei passaggi di esecuzione</span><span class="sxs-lookup"><span data-stu-id="a6294-185">Log of execution steps</span></span>|


## <a name="use-the-sdk-from-the-command-line"></a><span data-ttu-id="a6294-186">Usare l'SDK dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="a6294-186">Use the SDK from the command line</span></span>

### <a name="command-line-interface-of-the-helper-application"></a><span data-ttu-id="a6294-187">Interfaccia della riga di comando dell'applicazione helper</span><span class="sxs-lookup"><span data-stu-id="a6294-187">Command-line interface of the helper application</span></span>

<span data-ttu-id="a6294-188">In SDK directory\build\runtime, LocalRunHelper.exe è l'applicazione helper della riga di comando che offre interfacce alla maggior parte delle funzioni di esecuzione locale di uso comune.</span><span class="sxs-lookup"><span data-stu-id="a6294-188">Under SDK directory\build\runtime, LocalRunHelper.exe is the command-line helper application that provides interfaces to most of the commonly used local-run functions.</span></span> <span data-ttu-id="a6294-189">Entrambe le opzioni di comandi e argomenti fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="a6294-189">Note that both the command and the argument switches are case-sensitive.</span></span> <span data-ttu-id="a6294-190">Per richiamarle:</span><span class="sxs-lookup"><span data-stu-id="a6294-190">To invoke it:</span></span>

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

<span data-ttu-id="a6294-191">Eseguire LocalRunHelper.exe senza argomenti o con l'interruttore **Guida** per mostrare le informazioni della Guida:</span><span class="sxs-lookup"><span data-stu-id="a6294-191">Run LocalRunHelper.exe without arguments or with the **help** switch to show the help information:</span></span>

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile the script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

<span data-ttu-id="a6294-192">Nelle informazioni di aiuto:</span><span class="sxs-lookup"><span data-stu-id="a6294-192">In the help information:</span></span>

-  <span data-ttu-id="a6294-193">**Comando** indica il nome del comando.</span><span class="sxs-lookup"><span data-stu-id="a6294-193">**Command** gives the command’s name.</span></span>  
-  <span data-ttu-id="a6294-194">**Argomento richiesto** elenca gli argomenti che devono essere forniti.</span><span class="sxs-lookup"><span data-stu-id="a6294-194">**Required Argument** lists arguments that must be supplied.</span></span>  
-  <span data-ttu-id="a6294-195">**Argomento facoltativo** elenca gli argomenti facoltativi con i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="a6294-195">**Optional Argument** lists arguments that are optional, with default values.</span></span>  <span data-ttu-id="a6294-196">Gli argomenti Boolean facoltativi non hanno parametri e la loro comparsa ha un significato negativo per il loro valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="a6294-196">Optional Boolean arguments don’t have parameters, and their appearances mean negative to their default value.</span></span>

### <a name="return-value-and-logging"></a><span data-ttu-id="a6294-197">Valore restituito e registrazione</span><span class="sxs-lookup"><span data-stu-id="a6294-197">Return value and logging</span></span>

<span data-ttu-id="a6294-198">L'applicazione helper restituisce **0** in caso di successo e **-1** in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="a6294-198">The helper application returns **0** for success and **-1** for failure.</span></span> <span data-ttu-id="a6294-199">Per impostazione predefinita, l'helper invia tutti i messaggi alla console corrente.</span><span class="sxs-lookup"><span data-stu-id="a6294-199">By default, the helper sends all messages to the current console.</span></span> <span data-ttu-id="a6294-200">Tuttavia, la maggior parte dei comandi supporta l'argomento facoltativo**-MessageOut path_to_log_file** che reindirizza gli output in un file di log.</span><span class="sxs-lookup"><span data-stu-id="a6294-200">However, most of the commands support the **-MessageOut path_to_log_file** optional argument that redirects the outputs to a log file.</span></span>

### <a name="environment-variable-configuring"></a><span data-ttu-id="a6294-201">Configurazione della variabile di ambiente</span><span class="sxs-lookup"><span data-stu-id="a6294-201">Environment variable configuring</span></span>

<span data-ttu-id="a6294-202">Per l'esecuzione locale di U-SQL è necessaria una radice di dati specificata come account di archiviazione locale, oltre a un percorso CppSDK specificato per le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="a6294-202">U-SQL local run needs a specified data root as local storage account, as well as a specified CppSDK path for dependencies.</span></span> <span data-ttu-id="a6294-203">È possibile impostare l'argomento nella riga di comando o impostare la variabile dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="a6294-203">You can both set the argument in command-line or set environment variable for them.</span></span>

- <span data-ttu-id="a6294-204">Impostare la variabile di ambiente **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="a6294-204">Set the **SCOPE_CPP_SDK** environment variable.</span></span>

    <span data-ttu-id="a6294-205">Se si ottiene Microsoft Visual C++ e Windows SDK dall'installazione di Strumenti di Data Lake per Visual Studio, verificare di avere la cartella seguente:</span><span class="sxs-lookup"><span data-stu-id="a6294-205">If you get Microsoft Visual C++ and the Windows SDK by installing Data Lake Tools for Visual Studio, verify that you have the following folder:</span></span>

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    <span data-ttu-id="a6294-206">Definire una nuova variabile di ambiente denominata **SCOPE_CPP_SDK** che punti a questa directory.</span><span class="sxs-lookup"><span data-stu-id="a6294-206">Define a new environment variable called **SCOPE_CPP_SDK** to point to this directory.</span></span> <span data-ttu-id="a6294-207">In alternativa copiare la cartella in un'altra posizione e specificare **SCOPE_CPP_SDK**.</span><span class="sxs-lookup"><span data-stu-id="a6294-207">Or copy the folder to the other location and specify **SCOPE_CPP_SDK** as that.</span></span>

    <span data-ttu-id="a6294-208">Oltre a impostare la variabile di ambiente, è possibile specificare l'argomento **-CppSDK** quando si usa la riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a6294-208">In addition to setting the environment variable, you can specify the **-CppSDK** argument when you're using the command line.</span></span> <span data-ttu-id="a6294-209">Questo argomento sovrascrive la variabile di ambiente CppSDK predefinita.</span><span class="sxs-lookup"><span data-stu-id="a6294-209">This argument overwrites your default CppSDK environment variable.</span></span>

- <span data-ttu-id="a6294-210">Impostare la variabile di ambiente **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="a6294-210">Set the **LOCALRUN_DATAROOT** environment variable.</span></span>

    <span data-ttu-id="a6294-211">Definire una nuova variabile di ambiente denominata **LOCALRUN_DATAROOT** che punta alla cartella data-root.</span><span class="sxs-lookup"><span data-stu-id="a6294-211">Define a new environment variable called **LOCALRUN_DATAROOT** that points to the data root.</span></span>

    <span data-ttu-id="a6294-212">Oltre a impostare la variabile di ambiente, è possibile specificare l'argomento **-DataRoot** con il percorso di data-root quando si usa la riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a6294-212">In addition to setting the environment variable, you can specify the **-DataRoot** argument with the data-root path when you're using a command line.</span></span> <span data-ttu-id="a6294-213">Questo argomento sovrascrive la variabile di ambiente data-root predefinita.</span><span class="sxs-lookup"><span data-stu-id="a6294-213">This argument overwrites your default data-root environment variable.</span></span> <span data-ttu-id="a6294-214">È necessario aggiungere questo argomento a ogni riga di comando eseguita, così da poter sovrascrivere la variabile di ambiente data-root predefinita per tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="a6294-214">You need to add this argument to every command line you're running so that you can overwrite the default data-root environment variable for all operations.</span></span>

### <a name="sdk-command-line-usage-samples"></a><span data-ttu-id="a6294-215">Esempi di uso della riga di comando SDK</span><span class="sxs-lookup"><span data-stu-id="a6294-215">SDK command line usage samples</span></span>

#### <a name="compile-and-run"></a><span data-ttu-id="a6294-216">Compila ed esegui</span><span class="sxs-lookup"><span data-stu-id="a6294-216">Compile and run</span></span>

<span data-ttu-id="a6294-217">Il comando **run** viene usato per compilare lo script ed eseguire i risultati compilati.</span><span class="sxs-lookup"><span data-stu-id="a6294-217">The **run** command is used to compile the script and then execute compiled results.</span></span> <span data-ttu-id="a6294-218">Gli argomenti della riga di comando sono una combinazione degli argomenti di **compile** ed **execute**.</span><span class="sxs-lookup"><span data-stu-id="a6294-218">Its command-line arguments are a combination of those from **compile** and **execute**.</span></span>

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="a6294-219">Di seguito sono indicati gli argomenti facoltativi per **run**:</span><span class="sxs-lookup"><span data-stu-id="a6294-219">The following are optional arguments for **run**:</span></span>


|<span data-ttu-id="a6294-220">Argomento</span><span class="sxs-lookup"><span data-stu-id="a6294-220">Argument</span></span>|<span data-ttu-id="a6294-221">Valore predefinito</span><span class="sxs-lookup"><span data-stu-id="a6294-221">Default value</span></span>|<span data-ttu-id="a6294-222">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-222">Description</span></span>|
|--------|-------------|-----------|
|<span data-ttu-id="a6294-223">-CodeBehind</span><span class="sxs-lookup"><span data-stu-id="a6294-223">-CodeBehind</span></span>|<span data-ttu-id="a6294-224">False</span><span class="sxs-lookup"><span data-stu-id="a6294-224">False</span></span>|<span data-ttu-id="a6294-225">Lo script ha code-behind con estensione cs</span><span class="sxs-lookup"><span data-stu-id="a6294-225">The script has .cs code behind</span></span>|
|<span data-ttu-id="a6294-226">-CppSDK</span><span class="sxs-lookup"><span data-stu-id="a6294-226">-CppSDK</span></span>| |<span data-ttu-id="a6294-227">Directory CppSDK</span><span class="sxs-lookup"><span data-stu-id="a6294-227">CppSDK Directory</span></span>|
|<span data-ttu-id="a6294-228">-DataRoot</span><span class="sxs-lookup"><span data-stu-id="a6294-228">-DataRoot</span></span>| <span data-ttu-id="a6294-229">Variabile di ambiente DataRoot</span><span class="sxs-lookup"><span data-stu-id="a6294-229">DataRoot environment variable</span></span>|<span data-ttu-id="a6294-230">DataRoot per l'esecuzione locale, impostazione predefinita su variabile di ambiente 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="a6294-230">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
|<span data-ttu-id="a6294-231">-MessageOut</span><span class="sxs-lookup"><span data-stu-id="a6294-231">-MessageOut</span></span>| |<span data-ttu-id="a6294-232">Messaggi dump sulla console a un file</span><span class="sxs-lookup"><span data-stu-id="a6294-232">Dump messages on console to a file</span></span>|
|<span data-ttu-id="a6294-233">-Parallel</span><span class="sxs-lookup"><span data-stu-id="a6294-233">-Parallel</span></span>|<span data-ttu-id="a6294-234">1</span><span class="sxs-lookup"><span data-stu-id="a6294-234">1</span></span>|<span data-ttu-id="a6294-235">Esegue il piano con il parallelismo specificato</span><span class="sxs-lookup"><span data-stu-id="a6294-235">Run the plan with the specified parallelism</span></span>|
|<span data-ttu-id="a6294-236">-References</span><span class="sxs-lookup"><span data-stu-id="a6294-236">-References</span></span>| |<span data-ttu-id="a6294-237">Elenco di percorsi agli assembly di riferimento aggiuntivi o a file di dati code-behind, separati da ";"</span><span class="sxs-lookup"><span data-stu-id="a6294-237">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
|<span data-ttu-id="a6294-238">-UdoRedirect</span><span class="sxs-lookup"><span data-stu-id="a6294-238">-UdoRedirect</span></span>|<span data-ttu-id="a6294-239">False</span><span class="sxs-lookup"><span data-stu-id="a6294-239">False</span></span>|<span data-ttu-id="a6294-240">Genera la configurazione di reindirizzamento di assembly Udo</span><span class="sxs-lookup"><span data-stu-id="a6294-240">Generate Udo assembly redirect config</span></span>|
|<span data-ttu-id="a6294-241">-UseDatabase</span><span class="sxs-lookup"><span data-stu-id="a6294-241">-UseDatabase</span></span>|<span data-ttu-id="a6294-242">master</span><span class="sxs-lookup"><span data-stu-id="a6294-242">master</span></span>|<span data-ttu-id="a6294-243">Database da usare per la registrazione di assembly temporanei code-behind</span><span class="sxs-lookup"><span data-stu-id="a6294-243">Database to use for code behind temporary assembly registration</span></span>|
|<span data-ttu-id="a6294-244">-Verbose</span><span class="sxs-lookup"><span data-stu-id="a6294-244">-Verbose</span></span>|<span data-ttu-id="a6294-245">False</span><span class="sxs-lookup"><span data-stu-id="a6294-245">False</span></span>|<span data-ttu-id="a6294-246">Mostrare gli output dettagliati dal runtime</span><span class="sxs-lookup"><span data-stu-id="a6294-246">Show detailed outputs from runtime</span></span>|
|<span data-ttu-id="a6294-247">-WorkDir</span><span class="sxs-lookup"><span data-stu-id="a6294-247">-WorkDir</span></span>|<span data-ttu-id="a6294-248">Directory corrente</span><span class="sxs-lookup"><span data-stu-id="a6294-248">Current Directory</span></span>|<span data-ttu-id="a6294-249">Directory per l'uso del compilatore e gli output</span><span class="sxs-lookup"><span data-stu-id="a6294-249">Directory for compiler usage and outputs</span></span>|
|<span data-ttu-id="a6294-250">-RunScopeCEP</span><span class="sxs-lookup"><span data-stu-id="a6294-250">-RunScopeCEP</span></span>|<span data-ttu-id="a6294-251">0</span><span class="sxs-lookup"><span data-stu-id="a6294-251">0</span></span>|<span data-ttu-id="a6294-252">Modalità ScopeCEP da usare</span><span class="sxs-lookup"><span data-stu-id="a6294-252">ScopeCEP mode to use</span></span>|
|<span data-ttu-id="a6294-253">-ScopeCEPTempPath</span><span class="sxs-lookup"><span data-stu-id="a6294-253">-ScopeCEPTempPath</span></span>|<span data-ttu-id="a6294-254">temp</span><span class="sxs-lookup"><span data-stu-id="a6294-254">temp</span></span>|<span data-ttu-id="a6294-255">Percorso temporaneo da usare per lo streaming di dati</span><span class="sxs-lookup"><span data-stu-id="a6294-255">Temp path to use for streaming data</span></span>|
|<span data-ttu-id="a6294-256">-OptFlags</span><span class="sxs-lookup"><span data-stu-id="a6294-256">-OptFlags</span></span>| |<span data-ttu-id="a6294-257">Elenco delimitato da virgole con i flag di ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="a6294-257">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="a6294-258">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a6294-258">Here's an example:</span></span>

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

<span data-ttu-id="a6294-259">Oltre a combinare i comandi **compile** ed **execute**, è possibile compilare ed eseguire separatamente i file eseguibili compilati.</span><span class="sxs-lookup"><span data-stu-id="a6294-259">Besides combining **compile** and **execute**, you can compile and execute the compiled executables separately.</span></span>

#### <a name="compile-a-u-sql-script"></a><span data-ttu-id="a6294-260">Compilare uno script U-SQL</span><span class="sxs-lookup"><span data-stu-id="a6294-260">Compile a U-SQL script</span></span>

<span data-ttu-id="a6294-261">Il comando **compile** viene usato per compilare uno script di U-SQL in file eseguibili.</span><span class="sxs-lookup"><span data-stu-id="a6294-261">The **compile** command is used to compile a U-SQL script to executables.</span></span>

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

<span data-ttu-id="a6294-262">Di seguito sono indicati gli argomenti facoltativi per il comando **compile**:</span><span class="sxs-lookup"><span data-stu-id="a6294-262">The following are optional arguments for **compile**:</span></span>


|<span data-ttu-id="a6294-263">Argomento</span><span class="sxs-lookup"><span data-stu-id="a6294-263">Argument</span></span>|<span data-ttu-id="a6294-264">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-264">Description</span></span>|
|--------|-----------|
| <span data-ttu-id="a6294-265">-CodeBehind [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="a6294-265">-CodeBehind [default value 'False']</span></span>|<span data-ttu-id="a6294-266">Lo script ha code-behind con estensione cs</span><span class="sxs-lookup"><span data-stu-id="a6294-266">The script has .cs code behind</span></span>|
| <span data-ttu-id="a6294-267">-CppSDK [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="a6294-267">-CppSDK [default value '']</span></span>|<span data-ttu-id="a6294-268">Directory CppSDK</span><span class="sxs-lookup"><span data-stu-id="a6294-268">CppSDK Directory</span></span>|
| <span data-ttu-id="a6294-269">-DataRoot [valore predefinito 'DataRoot environment variable']</span><span class="sxs-lookup"><span data-stu-id="a6294-269">-DataRoot [default value 'DataRoot environment variable']</span></span>|<span data-ttu-id="a6294-270">DataRoot per l'esecuzione locale, impostazione predefinita su variabile di ambiente 'LOCALRUN_DATAROOT'</span><span class="sxs-lookup"><span data-stu-id="a6294-270">DataRoot for local run, default to 'LOCALRUN_DATAROOT' environment variable</span></span>|
| <span data-ttu-id="a6294-271">-MessageOut [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="a6294-271">-MessageOut [default value '']</span></span>|<span data-ttu-id="a6294-272">Messaggi dump sulla console a un file</span><span class="sxs-lookup"><span data-stu-id="a6294-272">Dump messages on console to a file</span></span>|
| <span data-ttu-id="a6294-273">-References [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="a6294-273">-References [default value '']</span></span>|<span data-ttu-id="a6294-274">Elenco di percorsi agli assembly di riferimento aggiuntivi o a file di dati code-behind, separati da ";"</span><span class="sxs-lookup"><span data-stu-id="a6294-274">List of paths to extra reference assemblies or data files of code behind, separated by ';'</span></span>|
| <span data-ttu-id="a6294-275">-Shallow [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="a6294-275">-Shallow [default value 'False']</span></span>|<span data-ttu-id="a6294-276">Compilazione superficiale</span><span class="sxs-lookup"><span data-stu-id="a6294-276">Shallow compile</span></span>|
| <span data-ttu-id="a6294-277">-UdoRedirect [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="a6294-277">-UdoRedirect [default value 'False']</span></span>|<span data-ttu-id="a6294-278">Genera la configurazione di reindirizzamento di assembly Udo</span><span class="sxs-lookup"><span data-stu-id="a6294-278">Generate Udo assembly redirect config</span></span>|
| <span data-ttu-id="a6294-279">-UseDatabase [valore predefinito 'master']</span><span class="sxs-lookup"><span data-stu-id="a6294-279">-UseDatabase [default value 'master']</span></span>|<span data-ttu-id="a6294-280">Database da usare per la registrazione di assembly temporanei code-behind</span><span class="sxs-lookup"><span data-stu-id="a6294-280">Database to use for code behind temporary assembly registration</span></span>|
| <span data-ttu-id="a6294-281">-WorkDir [valore predefinito 'Current Directory']</span><span class="sxs-lookup"><span data-stu-id="a6294-281">-WorkDir [default value 'Current Directory']</span></span>|<span data-ttu-id="a6294-282">Directory per l'uso del compilatore e gli output</span><span class="sxs-lookup"><span data-stu-id="a6294-282">Directory for compiler usage and outputs</span></span>|
| <span data-ttu-id="a6294-283">-RunScopeCEP [valore predefinito '0']</span><span class="sxs-lookup"><span data-stu-id="a6294-283">-RunScopeCEP [default value '0']</span></span>|<span data-ttu-id="a6294-284">Modalità ScopeCEP da usare</span><span class="sxs-lookup"><span data-stu-id="a6294-284">ScopeCEP mode to use</span></span>|
| <span data-ttu-id="a6294-285">-ScopeCEPTempPath [valore predefinito 'temp']</span><span class="sxs-lookup"><span data-stu-id="a6294-285">-ScopeCEPTempPath [default value 'temp']</span></span>|<span data-ttu-id="a6294-286">Percorso temporaneo da usare per lo streaming di dati</span><span class="sxs-lookup"><span data-stu-id="a6294-286">Temp path to use for streaming data</span></span>|
| <span data-ttu-id="a6294-287">-OptFlags [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="a6294-287">-OptFlags [default value '']</span></span>|<span data-ttu-id="a6294-288">Elenco delimitato da virgole con i flag di ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="a6294-288">Comma-separated list of optimizer flags</span></span>|


<span data-ttu-id="a6294-289">Di seguito sono riportati alcuni esempi d'uso.</span><span class="sxs-lookup"><span data-stu-id="a6294-289">Here are some usage examples.</span></span>

<span data-ttu-id="a6294-290">Compilare uno script U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a6294-290">Compile a U-SQL script:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql

<span data-ttu-id="a6294-291">Compilare uno script U-SQL e impostare la cartella data-root.</span><span class="sxs-lookup"><span data-stu-id="a6294-291">Compile a U-SQL script and set the data-root folder.</span></span> <span data-ttu-id="a6294-292">Si noti la variabile di ambiente impostata verrà sovrascritta.</span><span class="sxs-lookup"><span data-stu-id="a6294-292">Note that this will overwrite the set environment variable.</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

<span data-ttu-id="a6294-293">Compilare uno script U-SQL e impostare la directory di lavoro, un assembly di riferimento e un database:</span><span class="sxs-lookup"><span data-stu-id="a6294-293">Compile a U-SQL script and set a working directory, reference assembly, and database:</span></span>

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a><span data-ttu-id="a6294-294">Eseguire i risultati compilati</span><span class="sxs-lookup"><span data-stu-id="a6294-294">Execute compiled results</span></span>

<span data-ttu-id="a6294-295">Il comando **execute** viene usato per eseguire i risultati compilati.</span><span class="sxs-lookup"><span data-stu-id="a6294-295">The **execute** command is used to execute compiled results.</span></span>   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

<span data-ttu-id="a6294-296">Di seguito sono indicati gli argomenti facoltativi per il comando **execute**:</span><span class="sxs-lookup"><span data-stu-id="a6294-296">The following are optional arguments for **execute**:</span></span>

|<span data-ttu-id="a6294-297">Argomento</span><span class="sxs-lookup"><span data-stu-id="a6294-297">Argument</span></span>|<span data-ttu-id="a6294-298">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-298">Description</span></span>|
|--------|-----------|
|<span data-ttu-id="a6294-299">-DataRoot [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="a6294-299">-DataRoot [default value '']</span></span>|<span data-ttu-id="a6294-300">Radice dei dati per l'esecuzione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="a6294-300">Data root for metadata execution.</span></span> <span data-ttu-id="a6294-301">Il valore predefinito è la variabile di ambiente **LOCALRUN_DATAROOT**.</span><span class="sxs-lookup"><span data-stu-id="a6294-301">It defaults to the **LOCALRUN_DATAROOT** environment variable.</span></span>|
|<span data-ttu-id="a6294-302">-MessageOut [valore predefinito '']</span><span class="sxs-lookup"><span data-stu-id="a6294-302">-MessageOut [default value '']</span></span>|<span data-ttu-id="a6294-303">Esecuzione del dump dei messaggi della console in un file.</span><span class="sxs-lookup"><span data-stu-id="a6294-303">Dump messages on the console to a file.</span></span>|
|<span data-ttu-id="a6294-304">-Parallel [valore predefinito '1']</span><span class="sxs-lookup"><span data-stu-id="a6294-304">-Parallel [default value '1']</span></span>|<span data-ttu-id="a6294-305">Indica di eseguire i passaggi di esecuzione locale generati con il livello di parallelismo specificato.</span><span class="sxs-lookup"><span data-stu-id="a6294-305">Indicator to run the generated local-run steps with the specified parallelism level.</span></span>|
|<span data-ttu-id="a6294-306">-Verbose [valore predefinito 'False']</span><span class="sxs-lookup"><span data-stu-id="a6294-306">-Verbose [default value 'False']</span></span>|<span data-ttu-id="a6294-307">Indica di visualizzare output dettagliati dal runtime.</span><span class="sxs-lookup"><span data-stu-id="a6294-307">Indicator to show detailed outputs from runtime.</span></span>|

<span data-ttu-id="a6294-308">Ecco un esempio d'uso:</span><span class="sxs-lookup"><span data-stu-id="a6294-308">Here's a usage example:</span></span>

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-the-sdk-with-programming-interfaces"></a><span data-ttu-id="a6294-309">Uso dell'SDK con interfacce di programmazione</span><span class="sxs-lookup"><span data-stu-id="a6294-309">Use the SDK with programming interfaces</span></span>

<span data-ttu-id="a6294-310">Le interfacce di programmazione si trovano tutte in LocalRunHelper.exe.</span><span class="sxs-lookup"><span data-stu-id="a6294-310">The programming interfaces are all located in the LocalRunHelper.exe.</span></span> <span data-ttu-id="a6294-311">È possibile usarle per integrare le funzionalità dell'SDK U-SQL e il framework di test di C# per scalare il test locale dello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6294-311">You can use them to integrate the functionality of the U-SQL SDK and the C# test framework to scale your U-SQL script local test.</span></span> <span data-ttu-id="a6294-312">In questo articolo verrà usato il progetto di unit test C# standard per mostrare come usare queste interfacce per testare lo script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6294-312">In this article, I will use the standard C# unit test project to show how to use these interfaces to test your U-SQL script.</span></span>

### <a name="step-1-create-c-unit-test-project-and-configuration"></a><span data-ttu-id="a6294-313">Passaggio 1: Creare configurazione e progetto per unit test C#</span><span class="sxs-lookup"><span data-stu-id="a6294-313">Step 1: Create C# unit test project and configuration</span></span>

- <span data-ttu-id="a6294-314">Creare un progetto per unit test C# tramite File > Nuovo > Progetto > Visual C# > Test > Progetto unit test.</span><span class="sxs-lookup"><span data-stu-id="a6294-314">Create a C# unit test project through File > New > Project > Visual C# > Test > Unit Test Project.</span></span>
- <span data-ttu-id="a6294-315">Aggiungere LocalRunHelper.exe come riferimento per il progetto.</span><span class="sxs-lookup"><span data-stu-id="a6294-315">Add LocalRunHelper.exe as a reference for the project.</span></span> <span data-ttu-id="a6294-316">LocalRunHelper.exe si trova in \build\runtime\LocalRunHelper.exe nel pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="a6294-316">The LocalRunHelper.exe is located at \build\runtime\LocalRunHelper.exe in Nuget package.</span></span>

    ![Riferimento aggiunta dell'SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- <span data-ttu-id="a6294-318">L'SDK U-SQL supporta **solo** l'ambiente x64, quindi è necessario assicurarsi di impostare la piattaforma di destinazione della compilazione come x64.</span><span class="sxs-lookup"><span data-stu-id="a6294-318">U-SQL SDK **only** support x64 environment, make sure to set build platform target as x64.</span></span> <span data-ttu-id="a6294-319">È possibile farlo da Proprietà progetto > Build > Piattaforma di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a6294-319">You can set that through Project Property > Build > Platform target.</span></span>

    ![Progetto configurazione x64 SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- <span data-ttu-id="a6294-321">Assicurarsi di impostare l'ambiente di testing come x64.</span><span class="sxs-lookup"><span data-stu-id="a6294-321">Make sure to set your test environment as x64.</span></span> <span data-ttu-id="a6294-322">In Visual Studio è possibile impostarlo tramite Test > Impostazioni test > Architettura processore predefinita > x64.</span><span class="sxs-lookup"><span data-stu-id="a6294-322">In Visual Studio, you can set it through Test > Test Settings > Default Processor Architecture > x64.</span></span>

    ![Ambiente di testing configurazione x64 SDK U-SQL di Azure Data Lake](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- <span data-ttu-id="a6294-324">Assicurarsi di copiare tutti i file di dipendenza in NugetPackage\build\runtime\ nella directory di lavoro del progetto che generalmente si trova in ProjectFolder\bin\x64\Debug.</span><span class="sxs-lookup"><span data-stu-id="a6294-324">Make sure to copy all dependency files under NugetPackage\build\runtime\ to project working directory which is usually under ProjectFolder\bin\x64\Debug.</span></span>

### <a name="step-2-create-u-sql-script-test-case"></a><span data-ttu-id="a6294-325">Passaggio 2: Creare test case per lo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="a6294-325">Step 2: Create U-SQL script test case</span></span>

<span data-ttu-id="a6294-326">Di seguito è riportato il codice di esempio per il test dello script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="a6294-326">Below is the sample code for U-SQL script test.</span></span> <span data-ttu-id="a6294-327">Per i test, è necessario preparare script, file di input e file di output previsti.</span><span class="sxs-lookup"><span data-stu-id="a6294-327">For testing, you need to prepare scripts, input files and expected output files.</span></span>

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
                //Specify the local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure the DateRoot path, Script Path and CPPSDK path
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

                //Don't forget to close MessageOutput to get logs into file
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


### <a name="programming-interfaces-in-localrunhelperexe"></a><span data-ttu-id="a6294-328">Interfacce di programmazione in LocalRunHelper.exe</span><span class="sxs-lookup"><span data-stu-id="a6294-328">Programming interfaces in LocalRunHelper.exe</span></span>

<span data-ttu-id="a6294-329">LocalRunHelper.exe offre le interfacce di programmazione per la compilazione e l'esecuzione locale di U-SQL e così via. Le interfacce sono elencate come di seguito.</span><span class="sxs-lookup"><span data-stu-id="a6294-329">LocalRunHelper.exe provides the programming interfaces for U-SQL local compile, run, etc. The interfaces are listed as follows.</span></span>

<span data-ttu-id="a6294-330">**Costruttore**</span><span class="sxs-lookup"><span data-stu-id="a6294-330">**Constructor**</span></span>

<span data-ttu-id="a6294-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span><span class="sxs-lookup"><span data-stu-id="a6294-331">public LocalRunHelper([System.IO.TextWriter messageOutput = null])</span></span>

|<span data-ttu-id="a6294-332">.</span><span class="sxs-lookup"><span data-stu-id="a6294-332">Parameter</span></span>|<span data-ttu-id="a6294-333">Tipo</span><span class="sxs-lookup"><span data-stu-id="a6294-333">Type</span></span>|<span data-ttu-id="a6294-334">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-334">Description</span></span>|
|---------|----|-----------|
|<span data-ttu-id="a6294-335">messageOutput</span><span class="sxs-lookup"><span data-stu-id="a6294-335">messageOutput</span></span>|<span data-ttu-id="a6294-336">System.IO.TextWriter</span><span class="sxs-lookup"><span data-stu-id="a6294-336">System.IO.TextWriter</span></span>|<span data-ttu-id="a6294-337">per i messaggi di output, impostato su null per usare Console</span><span class="sxs-lookup"><span data-stu-id="a6294-337">for output messages, set to null to use Console</span></span>|

<span data-ttu-id="a6294-338">**Proprietà**</span><span class="sxs-lookup"><span data-stu-id="a6294-338">**Properties**</span></span>

|<span data-ttu-id="a6294-339">Proprietà</span><span class="sxs-lookup"><span data-stu-id="a6294-339">Property</span></span>|<span data-ttu-id="a6294-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="a6294-340">Type</span></span>|<span data-ttu-id="a6294-341">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-341">Description</span></span>|
|--------|----|-----------|
|<span data-ttu-id="a6294-342">AlgebraPath</span><span class="sxs-lookup"><span data-stu-id="a6294-342">AlgebraPath</span></span>|<span data-ttu-id="a6294-343">string</span><span class="sxs-lookup"><span data-stu-id="a6294-343">string</span></span>|<span data-ttu-id="a6294-344">Il percorso al file algebra (il file algebra è uno dei risultati della compilazione)</span><span class="sxs-lookup"><span data-stu-id="a6294-344">The path to algebra file (algebra file is one of the compilation results)</span></span>|
|<span data-ttu-id="a6294-345">CodeBehindReferences</span><span class="sxs-lookup"><span data-stu-id="a6294-345">CodeBehindReferences</span></span>|<span data-ttu-id="a6294-346">string</span><span class="sxs-lookup"><span data-stu-id="a6294-346">string</span></span>|<span data-ttu-id="a6294-347">Se lo script contiene riferimenti code-behind aggiuntivi, specificare i percorsi separati da ';'</span><span class="sxs-lookup"><span data-stu-id="a6294-347">If the script has additional code behind references, specify the paths separated with ';'</span></span>|
|<span data-ttu-id="a6294-348">CppSdkDir</span><span class="sxs-lookup"><span data-stu-id="a6294-348">CppSdkDir</span></span>|<span data-ttu-id="a6294-349">string</span><span class="sxs-lookup"><span data-stu-id="a6294-349">string</span></span>|<span data-ttu-id="a6294-350">Directory CppSDK</span><span class="sxs-lookup"><span data-stu-id="a6294-350">CppSDK directory</span></span>|
|<span data-ttu-id="a6294-351">CurrentDir</span><span class="sxs-lookup"><span data-stu-id="a6294-351">CurrentDir</span></span>|<span data-ttu-id="a6294-352">string</span><span class="sxs-lookup"><span data-stu-id="a6294-352">string</span></span>|<span data-ttu-id="a6294-353">La directory corrente</span><span class="sxs-lookup"><span data-stu-id="a6294-353">Current directory</span></span>|
|<span data-ttu-id="a6294-354">DataRoot</span><span class="sxs-lookup"><span data-stu-id="a6294-354">DataRoot</span></span>|<span data-ttu-id="a6294-355">string</span><span class="sxs-lookup"><span data-stu-id="a6294-355">string</span></span>|<span data-ttu-id="a6294-356">Il percorso della radice dei dati</span><span class="sxs-lookup"><span data-stu-id="a6294-356">Data root path</span></span>|
|<span data-ttu-id="a6294-357">DebuggerMailPath</span><span class="sxs-lookup"><span data-stu-id="a6294-357">DebuggerMailPath</span></span>|<span data-ttu-id="a6294-358">string</span><span class="sxs-lookup"><span data-stu-id="a6294-358">string</span></span>|<span data-ttu-id="a6294-359">Il percorso alla porta di inserimento/espulsione del debugger</span><span class="sxs-lookup"><span data-stu-id="a6294-359">The path to debugger mailslot</span></span>|
|<span data-ttu-id="a6294-360">GenerateUdoRedirect</span><span class="sxs-lookup"><span data-stu-id="a6294-360">GenerateUdoRedirect</span></span>|<span data-ttu-id="a6294-361">bool</span><span class="sxs-lookup"><span data-stu-id="a6294-361">bool</span></span>|<span data-ttu-id="a6294-362">Se si vuole generare il reindirizzamento di caricamento dell'assembly eseguire l'override della configurazione</span><span class="sxs-lookup"><span data-stu-id="a6294-362">If we want to generate assembly loading redirection override config</span></span>|
|<span data-ttu-id="a6294-363">HasCodeBehind</span><span class="sxs-lookup"><span data-stu-id="a6294-363">HasCodeBehind</span></span>|<span data-ttu-id="a6294-364">bool</span><span class="sxs-lookup"><span data-stu-id="a6294-364">bool</span></span>|<span data-ttu-id="a6294-365">Indica se lo script ha code-behind</span><span class="sxs-lookup"><span data-stu-id="a6294-365">If the script has code behind</span></span>|
|<span data-ttu-id="a6294-366">InputDir</span><span class="sxs-lookup"><span data-stu-id="a6294-366">InputDir</span></span>|<span data-ttu-id="a6294-367">string</span><span class="sxs-lookup"><span data-stu-id="a6294-367">string</span></span>|<span data-ttu-id="a6294-368">La directory per i dati di input</span><span class="sxs-lookup"><span data-stu-id="a6294-368">Directory for input data</span></span>|
|<span data-ttu-id="a6294-369">MessagePath</span><span class="sxs-lookup"><span data-stu-id="a6294-369">MessagePath</span></span>|<span data-ttu-id="a6294-370">string</span><span class="sxs-lookup"><span data-stu-id="a6294-370">string</span></span>|<span data-ttu-id="a6294-371">Il percorso del file dump del messaggio</span><span class="sxs-lookup"><span data-stu-id="a6294-371">Message dump file path</span></span>|
|<span data-ttu-id="a6294-372">OutputDir</span><span class="sxs-lookup"><span data-stu-id="a6294-372">OutputDir</span></span>|<span data-ttu-id="a6294-373">string</span><span class="sxs-lookup"><span data-stu-id="a6294-373">string</span></span>|<span data-ttu-id="a6294-374">La directory per i dati di output</span><span class="sxs-lookup"><span data-stu-id="a6294-374">Directory for output data</span></span>|
|<span data-ttu-id="a6294-375">Parallelismo</span><span class="sxs-lookup"><span data-stu-id="a6294-375">Parallelism</span></span>|<span data-ttu-id="a6294-376">int</span><span class="sxs-lookup"><span data-stu-id="a6294-376">int</span></span>|<span data-ttu-id="a6294-377">Il parallelismo per eseguire l'algebra</span><span class="sxs-lookup"><span data-stu-id="a6294-377">Parallelism to run the algebra</span></span>|
|<span data-ttu-id="a6294-378">ParentPid</span><span class="sxs-lookup"><span data-stu-id="a6294-378">ParentPid</span></span>|<span data-ttu-id="a6294-379">int</span><span class="sxs-lookup"><span data-stu-id="a6294-379">int</span></span>|<span data-ttu-id="a6294-380">Il PID dell'entità principale in cui il servizio esegue il monitoraggio per uscire, impostato su 0 o su un numero negativo se va ignorato</span><span class="sxs-lookup"><span data-stu-id="a6294-380">PID of the parent on which the service monitors to exit, set to 0 or negative to ignore</span></span>|
|<span data-ttu-id="a6294-381">ResultPath</span><span class="sxs-lookup"><span data-stu-id="a6294-381">ResultPath</span></span>|<span data-ttu-id="a6294-382">string</span><span class="sxs-lookup"><span data-stu-id="a6294-382">string</span></span>|<span data-ttu-id="a6294-383">Il percorso del file dump del risultato</span><span class="sxs-lookup"><span data-stu-id="a6294-383">Result dump file path</span></span>|
|<span data-ttu-id="a6294-384">RuntimeDir</span><span class="sxs-lookup"><span data-stu-id="a6294-384">RuntimeDir</span></span>|<span data-ttu-id="a6294-385">string</span><span class="sxs-lookup"><span data-stu-id="a6294-385">string</span></span>|<span data-ttu-id="a6294-386">La directory di runtime</span><span class="sxs-lookup"><span data-stu-id="a6294-386">Runtime directory</span></span>|
|<span data-ttu-id="a6294-387">ScriptPath</span><span class="sxs-lookup"><span data-stu-id="a6294-387">ScriptPath</span></span>|<span data-ttu-id="a6294-388">string</span><span class="sxs-lookup"><span data-stu-id="a6294-388">string</span></span>|<span data-ttu-id="a6294-389">Indica dove trovare lo script</span><span class="sxs-lookup"><span data-stu-id="a6294-389">Where to find the script</span></span>|
|<span data-ttu-id="a6294-390">Shallow</span><span class="sxs-lookup"><span data-stu-id="a6294-390">Shallow</span></span>|<span data-ttu-id="a6294-391">bool</span><span class="sxs-lookup"><span data-stu-id="a6294-391">bool</span></span>|<span data-ttu-id="a6294-392">Indica se la compilazione è superficiale o no</span><span class="sxs-lookup"><span data-stu-id="a6294-392">Shallow compile or not</span></span>|
|<span data-ttu-id="a6294-393">TempDir</span><span class="sxs-lookup"><span data-stu-id="a6294-393">TempDir</span></span>|<span data-ttu-id="a6294-394">string</span><span class="sxs-lookup"><span data-stu-id="a6294-394">string</span></span>|<span data-ttu-id="a6294-395">Directory Temp</span><span class="sxs-lookup"><span data-stu-id="a6294-395">Temp directory</span></span>|
|<span data-ttu-id="a6294-396">UseDataBase</span><span class="sxs-lookup"><span data-stu-id="a6294-396">UseDataBase</span></span>|<span data-ttu-id="a6294-397">string</span><span class="sxs-lookup"><span data-stu-id="a6294-397">string</span></span>|<span data-ttu-id="a6294-398">Specifica il database da usare per la registrazione di assembly temporanei code-behind; master per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="a6294-398">Specify the database to use for code behind temporary assembly registration, master by default</span></span>|
|<span data-ttu-id="a6294-399">WorkDir</span><span class="sxs-lookup"><span data-stu-id="a6294-399">WorkDir</span></span>|<span data-ttu-id="a6294-400">string</span><span class="sxs-lookup"><span data-stu-id="a6294-400">string</span></span>|<span data-ttu-id="a6294-401">La directory di lavoro preferita</span><span class="sxs-lookup"><span data-stu-id="a6294-401">Preferred working directory</span></span>|


<span data-ttu-id="a6294-402">**Metodo**</span><span class="sxs-lookup"><span data-stu-id="a6294-402">**Method**</span></span>

|<span data-ttu-id="a6294-403">Metodo</span><span class="sxs-lookup"><span data-stu-id="a6294-403">Method</span></span>|<span data-ttu-id="a6294-404">Descrizione</span><span class="sxs-lookup"><span data-stu-id="a6294-404">Description</span></span>|<span data-ttu-id="a6294-405">Return</span><span class="sxs-lookup"><span data-stu-id="a6294-405">Return</span></span>|<span data-ttu-id="a6294-406">.</span><span class="sxs-lookup"><span data-stu-id="a6294-406">Parameter</span></span>|
|------|-----------|------|---------|
|<span data-ttu-id="a6294-407">public bool DoCompile()</span><span class="sxs-lookup"><span data-stu-id="a6294-407">public bool DoCompile()</span></span>|<span data-ttu-id="a6294-408">Consente di compilare lo script U-SQL</span><span class="sxs-lookup"><span data-stu-id="a6294-408">Compile the U-SQL script</span></span>|<span data-ttu-id="a6294-409">Se l'esito è positivo, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="a6294-409">True on success</span></span>| |
|<span data-ttu-id="a6294-410">public bool DoExec()</span><span class="sxs-lookup"><span data-stu-id="a6294-410">public bool DoExec()</span></span>|<span data-ttu-id="a6294-411">Esegue il risultato compilato</span><span class="sxs-lookup"><span data-stu-id="a6294-411">Execute the compiled result</span></span>|<span data-ttu-id="a6294-412">Se l'esito è positivo, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="a6294-412">True on success</span></span>| |
|<span data-ttu-id="a6294-413">public bool DoRun()</span><span class="sxs-lookup"><span data-stu-id="a6294-413">public bool DoRun()</span></span>|<span data-ttu-id="a6294-414">Esegue lo script U-SQL (compile + execute)</span><span class="sxs-lookup"><span data-stu-id="a6294-414">Run the U-SQL script (Compile + Execute)</span></span>|<span data-ttu-id="a6294-415">Se l'esito è positivo, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="a6294-415">True on success</span></span>| |
|<span data-ttu-id="a6294-416">public bool IsValidRuntimeDir(string path)</span><span class="sxs-lookup"><span data-stu-id="a6294-416">public bool IsValidRuntimeDir(string path)</span></span>|<span data-ttu-id="a6294-417">Controlla se il percorso specificato è un percorso di runtime valido</span><span class="sxs-lookup"><span data-stu-id="a6294-417">Check if the given path is valid runtime path</span></span>|<span data-ttu-id="a6294-418">Se è valido, restituisce il valore true</span><span class="sxs-lookup"><span data-stu-id="a6294-418">True for valid</span></span>|<span data-ttu-id="a6294-419">Il percorso della directory di runtime</span><span class="sxs-lookup"><span data-stu-id="a6294-419">The path of runtime directory</span></span>|


## <a name="faq-about-common-issue"></a><span data-ttu-id="a6294-420">Domande frequenti sui problemi comuni</span><span class="sxs-lookup"><span data-stu-id="a6294-420">FAQ about common issue</span></span>

### <a name="error-1"></a><span data-ttu-id="a6294-421">Errore 1:</span><span class="sxs-lookup"><span data-stu-id="a6294-421">Error 1:</span></span>
<span data-ttu-id="a6294-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span><span class="sxs-lookup"><span data-stu-id="a6294-422">E_CSC_SYSTEM_INTERNAL: Internal error!</span></span> <span data-ttu-id="a6294-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span><span class="sxs-lookup"><span data-stu-id="a6294-423">Could not load file or assembly 'ScopeEngineManaged.dll' or one of its dependencies.</span></span> <span data-ttu-id="a6294-424">The specified module could not be found. (E_CSC_SYSTEM_INTERNAL: errore interno. Impossibile caricare il file o l'assembly 'ScopeEngineManaged.dll' o una delle sue dipendenze. Impossibile trovare il modulo specificato.)</span><span class="sxs-lookup"><span data-stu-id="a6294-424">The specified module could not be found.</span></span>

<span data-ttu-id="a6294-425">Verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="a6294-425">Please check the following:</span></span>

- <span data-ttu-id="a6294-426">Assicurarsi di avere un ambiente x64.</span><span class="sxs-lookup"><span data-stu-id="a6294-426">Make sure you have x64 environment.</span></span> <span data-ttu-id="a6294-427">La piattaforma di destinazione di compilazione e l'ambiente di testing devono essere x64; fare riferimento alla sezione **Passaggio 1: Creare configurazione e progetto per unit test C#** sopra.</span><span class="sxs-lookup"><span data-stu-id="a6294-427">The build target platform and the test environment should be x64, refer to **Step 1: Create C# unit test project and configuration** above.</span></span>
- <span data-ttu-id="a6294-428">Assicurarsi di aver copiato nella directory di lavoro tutti i file di dipendenza presenti in NugetPackage\build\runtime\.</span><span class="sxs-lookup"><span data-stu-id="a6294-428">Make sure you have copied all dependency files under NugetPackage\build\runtime\ to project working directory.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a6294-429">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6294-429">Next steps</span></span>

* <span data-ttu-id="a6294-430">Per informazioni su U-SQL, vedere [Introduzione al linguaggio U-SQL di Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a6294-430">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="a6294-431">Per registrare informazioni di diagnostica, vedere [Accesso ai log di diagnostica per Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="a6294-431">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md).</span></span>
* <span data-ttu-id="a6294-432">Per visualizzare una query più complessa, vedere [Analizzare i log dei siti Web con Analisi Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="a6294-432">To see a more complex query, see [Analyze website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a6294-433">Per visualizzare i dettagli del processo, vedere [Usare Job Browser e Job View (Visualizzazione processo) per i processi di Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a6294-433">To view job details, see [Use Job Browser and Job View for Azure Data Lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md).</span></span>
* <span data-ttu-id="a6294-434">Per usare la visualizzazione esecuzioni vertici, vedere [Usare la visualizzazione esecuzioni vertici in Azure Data Lake Tools per Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span><span class="sxs-lookup"><span data-stu-id="a6294-434">To use the vertex execution view, see [Use the Vertex Execution View in Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).</span></span>
