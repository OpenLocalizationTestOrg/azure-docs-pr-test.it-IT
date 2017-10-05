---
title: Sviluppare ed eseguire localmente le funzioni di Azure | Documentazione Microsoft
description: Informazioni su come scrivere codice per le funzioni di Azure e testarle nel computer locale prima di eseguirle in Funzioni di Azure.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="62eb5-103">Scrivere codice per le funzioni di Azure e testarle in locale</span><span class="sxs-lookup"><span data-stu-id="62eb5-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="62eb5-104">Sebbene il [portale di Azure] offra un set di strumenti completo per lo sviluppo e il test delle funzioni di Azure, molti sviluppatori preferiscono un'esperienza di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="62eb5-105">Funzioni di Azure semplifica l'uso dell'editor di codice e degli strumenti di sviluppo locale preferiti per sviluppare e testare le funzioni nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="62eb5-106">Le funzioni possono attivare gli eventi in Azure ed è possibile eseguire il debug delle funzioni JavaScript e C# nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="62eb5-107">Se si sviluppatori di Visual Studio C#, Funzioni di Azure [si integra anche con Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="62eb5-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="62eb5-108">Installare gli strumenti di base per Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="62eb5-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="62eb5-109">Strumenti di base di Funzioni di Azure è una versione locale del runtime di Funzioni di Azure che è possibile eseguire nel computer Windows locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="62eb5-110">Non è un emulatore o simulatore.</span><span class="sxs-lookup"><span data-stu-id="62eb5-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="62eb5-111">Si tratta dello stesso runtime presente in Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="62eb5-112">Gli [strumenti di base di Funzioni di Azure] vengono offerti come pacchetto npm.</span><span class="sxs-lookup"><span data-stu-id="62eb5-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="62eb5-113">È innanzitutto necessario [installare NodeJS](https://docs.npmjs.com/getting-started/installing-node), che include npm.</span><span class="sxs-lookup"><span data-stu-id="62eb5-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="62eb5-114">A questo punto, il pacchetto degli strumenti di base di Funzioni di Azure può essere installato solo nei computer Windows.</span><span class="sxs-lookup"><span data-stu-id="62eb5-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="62eb5-115">Questa restrizione è dovuta a una limitazione temporanea nell'host di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="62eb5-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="62eb5-116">[strumenti di base di Funzioni di Azure] aggiunge gli alias di comando seguenti:</span><span class="sxs-lookup"><span data-stu-id="62eb5-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="62eb5-117">**func**</span><span class="sxs-lookup"><span data-stu-id="62eb5-117">**func**</span></span>
* <span data-ttu-id="62eb5-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="62eb5-118">**azfun**</span></span>
* <span data-ttu-id="62eb5-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="62eb5-119">**azurefunctions**</span></span>

<span data-ttu-id="62eb5-120">Tutti questi alias possono essere usati al posto di `func` illustrato negli esempi di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="62eb5-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="62eb5-121">Creare un progetto Funzioni locale</span><span class="sxs-lookup"><span data-stu-id="62eb5-121">Create a local Functions project</span></span>

<span data-ttu-id="62eb5-122">Quando è eseguito in locale, un progetto Funzioni è una directory che presenta i file host.json e local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="62eb5-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="62eb5-123">Questa directory è l'equivalente di un'app per le funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="62eb5-124">Per altre informazioni sulla struttura delle cartelle di Funzioni di Azure, vedere la [Guida per sviluppatori di Funzioni di Azure](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="62eb5-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="62eb5-125">Al prompt dei comandi, eseguire il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="62eb5-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="62eb5-126">L'output ha un aspetto simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="62eb5-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="62eb5-127">Per rifiutare esplicitamente la creazione di un repository Git, usare l'opzione `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="62eb5-128">File di impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="62eb5-128">Local settings file</span></span>

<span data-ttu-id="62eb5-129">Il file local.settings.json archivia le impostazioni di app, le stringhe di connessione e le impostazioni per Strumenti di base di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="62eb5-130">Presenta la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="62eb5-130">It has the following structure:</span></span>

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| <span data-ttu-id="62eb5-131">Impostazione</span><span class="sxs-lookup"><span data-stu-id="62eb5-131">Setting</span></span>      | <span data-ttu-id="62eb5-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62eb5-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="62eb5-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="62eb5-133">**IsEncrypted**</span></span> | <span data-ttu-id="62eb5-134">Se impostato su **true**, tutti i valori sono crittografati tramite una chiave del computer locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="62eb5-135">Usato con i comandi `func settings`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-135">Used with `func settings` commands.</span></span> <span data-ttu-id="62eb5-136">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="62eb5-136">Default value is **false**.</span></span> |
| <span data-ttu-id="62eb5-137">**Valori**</span><span class="sxs-lookup"><span data-stu-id="62eb5-137">**Values**</span></span> | <span data-ttu-id="62eb5-138">Raccolta di impostazioni dell'applicazione usate durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="62eb5-139">Aggiungere le impostazioni dell'applicazione a questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="62eb5-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="62eb5-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="62eb5-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="62eb5-141">Consente di impostare la stringa di connessione all'account di archiviazione di Azure usato internamente dal runtime di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="62eb5-142">L'account di archiviazione supporta i trigger della funzione.</span><span class="sxs-lookup"><span data-stu-id="62eb5-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="62eb5-143">Questa impostazione di connessione per l'account di archiviazione è obbligatorio per tutte le funzioni ad eccezione delle funzioni attivate da HTTP.</span><span class="sxs-lookup"><span data-stu-id="62eb5-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="62eb5-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="62eb5-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="62eb5-145">Consente di impostare la stringa di connessione all'account di archiviazione di Azure usato per archiviare i log della funzione.</span><span class="sxs-lookup"><span data-stu-id="62eb5-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="62eb5-146">Questo valore facoltativo rende accessibili i log dal portale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="62eb5-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="62eb5-147">**Host**</span></span> | <span data-ttu-id="62eb5-148">Le impostazioni in questa sezione consentono di personalizzare il processo host di Funzioni durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="62eb5-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="62eb5-149">**LocalHttpPort**</span></span> | <span data-ttu-id="62eb5-150">Consente di impostare la porta predefinita usata durante l'esecuzione nell'host locale di Funzioni, ovvero `func host start` e `func run`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="62eb5-151">L'opzione `--port` della riga di comando ha la precedenza su questo valore.</span><span class="sxs-lookup"><span data-stu-id="62eb5-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="62eb5-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="62eb5-152">**CORS**</span></span> | <span data-ttu-id="62eb5-153">Definisce le origini consentite per la [condivisione di risorse tra le origini (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="62eb5-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="62eb5-154">Le origini sono elencate in un elenco delimitato dalla virgola senza spazi.</span><span class="sxs-lookup"><span data-stu-id="62eb5-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="62eb5-155">È supportato il valore del carattere jolly (**\***) che consente le richieste provenienti da qualsiasi origine.</span><span class="sxs-lookup"><span data-stu-id="62eb5-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="62eb5-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="62eb5-156">**ConnectionStrings**</span></span> | <span data-ttu-id="62eb5-157">Contiene le stringhe di connessione del database per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="62eb5-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="62eb5-158">Le stringhe di connessione in questo oggetto vengono aggiunte all'ambiente con il tipo di provider di **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="62eb5-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="62eb5-159">La maggior parte dei trigger e delle associazioni presentano una proprietà **Connection** che mappa il nome di una variabile di ambiente o di un'impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="62eb5-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="62eb5-160">Per ogni proprietà di connessione, deve essere definita un'impostazione dell'app nel file local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="62eb5-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="62eb5-161">Queste impostazioni possono anche essere lette nel codice come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="62eb5-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="62eb5-162">In C# usare [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) o [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="62eb5-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="62eb5-163">In JavaScript usare `process.env`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="62eb5-164">Le impostazioni specificate come variabile di ambiente di sistema hanno la precedenza sui valori nel file local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="62eb5-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="62eb5-165">Le impostazioni nel file local.settings.json vengono usate solo per gli strumenti delle funzioni durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="62eb5-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="62eb5-166">Per impostazione predefinita, queste impostazioni non vengono migrate automaticamente quando il progetto viene pubblicato in Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="62eb5-167">Utilizzare lo switch `--publish-local-settings` [durante la pubblicazione](#publish) per assicurarsi che queste impostazioni vengano aggiunte all'app della funzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="62eb5-168">Quando non è impostata alcuna stringa di connessione di archiviazione valida per **AzureWebJobsStorage**, viene visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="62eb5-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="62eb5-169">Valore mancante per AzureWebJobsStorage in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="62eb5-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="62eb5-170">È necessario per tutti i trigger diversi da HTTP.</span><span class="sxs-lookup"><span data-stu-id="62eb5-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="62eb5-171">È possibile eseguire "func azure functionary fetch-app-settings <functionAppName>" o specificare una stringa di connessione in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="62eb5-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="62eb5-172">Configurare le impostazioni applicazione</span><span class="sxs-lookup"><span data-stu-id="62eb5-172">Configure app settings</span></span>

<span data-ttu-id="62eb5-173">Per impostare un valore per le stringhe di connessione, è possibile eseguire una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="62eb5-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="62eb5-174">Immettere la stringa di connessione da [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="62eb5-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="62eb5-175">Usare uno di questi comandi:</span><span class="sxs-lookup"><span data-stu-id="62eb5-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="62eb5-176">Per entrambi i comandi è necessario innanzitutto accedere ad Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="62eb5-177">Creare una funzione</span><span class="sxs-lookup"><span data-stu-id="62eb5-177">Create a function</span></span>

<span data-ttu-id="62eb5-178">Eseguire il comando seguente per creare una funzione:</span><span class="sxs-lookup"><span data-stu-id="62eb5-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="62eb5-179">`func new` supporta gli argomenti opzionali seguenti:</span><span class="sxs-lookup"><span data-stu-id="62eb5-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="62eb5-180">Argomento</span><span class="sxs-lookup"><span data-stu-id="62eb5-180">Argument</span></span>     | <span data-ttu-id="62eb5-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62eb5-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="62eb5-182">Il linguaggio di programmazione del modello, come C#, F# o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="62eb5-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="62eb5-183">Il nome del modello.</span><span class="sxs-lookup"><span data-stu-id="62eb5-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="62eb5-184">Il nome della funzione.</span><span class="sxs-lookup"><span data-stu-id="62eb5-184">The function name.</span></span> |

<span data-ttu-id="62eb5-185">Ad esempio, per creare un trigger HTTP JavaScript, eseguire:</span><span class="sxs-lookup"><span data-stu-id="62eb5-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="62eb5-186">Per creare una funzione attivata dalla coda, eseguire:</span><span class="sxs-lookup"><span data-stu-id="62eb5-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="62eb5-187">Eseguire funzioni localmente</span><span class="sxs-lookup"><span data-stu-id="62eb5-187">Run functions locally</span></span>

<span data-ttu-id="62eb5-188">Per eseguire un progetto Funzioni, eseguire l'host di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="62eb5-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="62eb5-189">L'host abilita i trigger per tutte le funzioni del progetto:</span><span class="sxs-lookup"><span data-stu-id="62eb5-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="62eb5-190">`func host start` supporta le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="62eb5-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="62eb5-191">Opzione</span><span class="sxs-lookup"><span data-stu-id="62eb5-191">Option</span></span>     | <span data-ttu-id="62eb5-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62eb5-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="62eb5-193">La porta locale su cui ascoltare.</span><span class="sxs-lookup"><span data-stu-id="62eb5-193">The local port to listen on.</span></span> <span data-ttu-id="62eb5-194">Valore predefinito: 7071.</span><span class="sxs-lookup"><span data-stu-id="62eb5-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="62eb5-195">Le opzioni sono `VSCode` e `VS`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="62eb5-196">Un elenco delimitato dalla virgola di origini CORS, senza spazi.</span><span class="sxs-lookup"><span data-stu-id="62eb5-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="62eb5-197">La porta per il debugger di nodo da usare.</span><span class="sxs-lookup"><span data-stu-id="62eb5-197">The port for the node debugger to use.</span></span> <span data-ttu-id="62eb5-198">Predefinito: un valore di launch.json o 5858.</span><span class="sxs-lookup"><span data-stu-id="62eb5-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="62eb5-199">Il livello di traccia della console (off, verbose, info, warning o error).</span><span class="sxs-lookup"><span data-stu-id="62eb5-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="62eb5-200">Predefinito: Info.</span><span class="sxs-lookup"><span data-stu-id="62eb5-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="62eb5-201">Il timeout per l'host di Funzioni t da avviare, in secondi.</span><span class="sxs-lookup"><span data-stu-id="62eb5-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="62eb5-202">Impostazione predefinita: 20 secondi.</span><span class="sxs-lookup"><span data-stu-id="62eb5-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="62eb5-203">Associare https://localhost:{port} anziché http://localhost:{port}.</span><span class="sxs-lookup"><span data-stu-id="62eb5-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="62eb5-204">Per impostazione predefinita, questa opzione crea un certificato attendibile nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="62eb5-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="62eb5-205">Sospendere per l'input aggiuntivo prima dell'uscita dal processo.</span><span class="sxs-lookup"><span data-stu-id="62eb5-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="62eb5-206">Utile quando si avvia Strumenti di base di Funzioni di Azure da un ambiente di sviluppo integrato (IDE).</span><span class="sxs-lookup"><span data-stu-id="62eb5-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="62eb5-207">Quando viene avviato l'host di Funzioni, restituisce come output l'URL delle funzioni attivate da HTTP:</span><span class="sxs-lookup"><span data-stu-id="62eb5-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="62eb5-208">Eseguire il debug in Visual Studio Code o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="62eb5-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="62eb5-209">Per associare un debugger, passare l'argomento `--debug`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="62eb5-210">Per eseguire il debug di funzioni JavaScript, usare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="62eb5-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="62eb5-211">Per le funzioni C#, usare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="62eb5-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="62eb5-212">Per eseguire il debug di funzioni C#, usare `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="62eb5-213">È anche possibile usare [Strumenti di Visual Studio 2017 per Funzioni di Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="62eb5-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="62eb5-214">Per avviare l'host e configurare il debug di JavaScript, eseguire:</span><span class="sxs-lookup"><span data-stu-id="62eb5-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="62eb5-215">Quindi, in Visual Studio Code, nella visualizzazione **Debug**, selezionare **Attach to Azure Functions** (Associa a Funzioni di Azure).</span><span class="sxs-lookup"><span data-stu-id="62eb5-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="62eb5-216">È possibile associare punti di interruzione, controllare variabili ed eseguire il codice passo per passo.</span><span class="sxs-lookup"><span data-stu-id="62eb5-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Debug di JavaScript con Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="62eb5-218">Passaggio di dati di test a una funzione</span><span class="sxs-lookup"><span data-stu-id="62eb5-218">Passing test data to a function</span></span>

<span data-ttu-id="62eb5-219">È anche possibile richiamare una funzione direttamente tramite `func run <FunctionName>` e offrire dati di input per la funzione.</span><span class="sxs-lookup"><span data-stu-id="62eb5-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="62eb5-220">Questo comando è simile all'esecuzione di una funzione con la scheda **Test** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="62eb5-221">Questo comando avvia l'intero host di Funzioni.</span><span class="sxs-lookup"><span data-stu-id="62eb5-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="62eb5-222">`func run` supporta le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="62eb5-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="62eb5-223">Opzione</span><span class="sxs-lookup"><span data-stu-id="62eb5-223">Option</span></span>     | <span data-ttu-id="62eb5-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62eb5-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="62eb5-225">Contenuto inline.</span><span class="sxs-lookup"><span data-stu-id="62eb5-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="62eb5-226">Associare un debugger al processo host prima di eseguire la funzione.</span><span class="sxs-lookup"><span data-stu-id="62eb5-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="62eb5-227">Tempo di attesa (in secondi) fino a quando l'host locale di Funzioni è pronto.</span><span class="sxs-lookup"><span data-stu-id="62eb5-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="62eb5-228">Il nome del file da usare come contenuto.</span><span class="sxs-lookup"><span data-stu-id="62eb5-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="62eb5-229">Non richiede input.</span><span class="sxs-lookup"><span data-stu-id="62eb5-229">Does not prompt for input.</span></span> <span data-ttu-id="62eb5-230">Utile per scenari di automazione.</span><span class="sxs-lookup"><span data-stu-id="62eb5-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="62eb5-231">Ad esempio, per chiamare una funzione attivata da HTTP e passare il corpo del contenuto, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="62eb5-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="62eb5-232"><a name="publish"></a> Pubblicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="62eb5-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="62eb5-233">Per pubblicare un progetto Funzioni in un'app per le funzioni in Azure, usare il comando `publish`:</span><span class="sxs-lookup"><span data-stu-id="62eb5-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="62eb5-234">È possibile usare le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="62eb5-234">You can use the following options:</span></span>

| <span data-ttu-id="62eb5-235">Opzione</span><span class="sxs-lookup"><span data-stu-id="62eb5-235">Option</span></span>     | <span data-ttu-id="62eb5-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="62eb5-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="62eb5-237">Pubblicare le impostazioni di local.settings.json in Azure, suggerendo di sovrascrivere eventuali impostazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="62eb5-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="62eb5-238">Deve essere usato con `-i`.</span><span class="sxs-lookup"><span data-stu-id="62eb5-238">Must be used with `-i`.</span></span> <span data-ttu-id="62eb5-239">Sovrascrive AppSettings in Azure con il valore locale se diverso.</span><span class="sxs-lookup"><span data-stu-id="62eb5-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="62eb5-240">Viene suggerito il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="62eb5-240">Default is prompt.</span></span>|

<span data-ttu-id="62eb5-241">Il comando `publish` carica il contenuto della directory del progetto Funzioni.</span><span class="sxs-lookup"><span data-stu-id="62eb5-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="62eb5-242">Se si eliminano i file in locale, il comando `publish` non li elimina da Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb5-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="62eb5-243">È possibile eliminare i file in Azure usando lo [strumento Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) nel [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="62eb5-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="62eb5-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="62eb5-244">Next steps</span></span>

<span data-ttu-id="62eb5-245">Strumenti di base di Funzioni di Azure è [open source ed è ospitato su GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="62eb5-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="62eb5-246">Per registrare una richiesta per un bug o una funzionalità [aprire un problema di GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="62eb5-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[strumenti di base di Funzioni di Azure]: https://www.npmjs.com/package/azure-functions-core-tools
[portale di Azure]: https://portal.azure.com 
