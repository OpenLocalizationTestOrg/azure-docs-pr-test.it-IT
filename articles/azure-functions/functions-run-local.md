---
title: aaaDevelop e Azure esecuzione funzioni localmente | Documenti Microsoft
description: Informazioni su come toocode e test di Azure funziona nel computer locale prima di eseguire funzioni di Azure.
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
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="f606d-103">Scrivere codice per le funzioni di Azure e testarle in locale</span><span class="sxs-lookup"><span data-stu-id="f606d-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="f606d-104">Durante la hello [portale di Azure] fornisce una procedura completa di set di strumenti per lo sviluppo e test funzioni di Azure, molti sviluppatori preferiscono un'esperienza di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="f606d-105">Funzioni di Azure rende facile toouse i Preferiti codice editor e toodevelop strumenti di sviluppo locale e testare le funzioni nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="f606d-106">Le funzioni possono attivare gli eventi in Azure ed è possibile eseguire il debug delle funzioni JavaScript e C# nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="f606d-107">Se si sviluppatori di Visual Studio C#, Funzioni di Azure [si integra anche con Visual Studio 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="f606d-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="f606d-108">Installare strumenti di base delle funzioni di hello Azure</span><span class="sxs-lookup"><span data-stu-id="f606d-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="f606d-109">Strumenti di base di funzioni di Azure è una versione locale del runtime di Azure funzioni hello che è possibile eseguire nel computer locale di Windows.</span><span class="sxs-lookup"><span data-stu-id="f606d-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="f606d-110">Non è un emulatore o simulatore.</span><span class="sxs-lookup"><span data-stu-id="f606d-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="f606d-111">È hello runtime stesso che supporta le funzioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="f606d-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="f606d-112">Hello [strumenti di base di Azure funzioni] viene fornito come un pacchetto npm.</span><span class="sxs-lookup"><span data-stu-id="f606d-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="f606d-113">È innanzitutto necessario [installare NodeJS](https://docs.npmjs.com/getting-started/installing-node), che include npm.</span><span class="sxs-lookup"><span data-stu-id="f606d-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="f606d-114">In questo momento, pacchetto di strumenti di Azure funzioni principali di hello può essere installato solo nei computer Windows.</span><span class="sxs-lookup"><span data-stu-id="f606d-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="f606d-115">Questa restrizione è a causa di limitazione temporanea tooa host funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="f606d-116">[strumenti di base di Azure funzioni] aggiunge hello alias di comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f606d-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="f606d-117">**func**</span><span class="sxs-lookup"><span data-stu-id="f606d-117">**func**</span></span>
* <span data-ttu-id="f606d-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="f606d-118">**azfun**</span></span>
* <span data-ttu-id="f606d-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="f606d-119">**azurefunctions**</span></span>

<span data-ttu-id="f606d-120">Tutti questi alias può essere usati al posto di `func` illustrato negli esempi di hello in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="f606d-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="f606d-121">Creare un progetto Funzioni locale</span><span class="sxs-lookup"><span data-stu-id="f606d-121">Create a local Functions project</span></span>

<span data-ttu-id="f606d-122">Quando si esegue in locale, un progetto di funzioni è una directory con local.settings.json e host.json file hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="f606d-123">Questa directory è hello equivalente di un'app di funzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="f606d-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="f606d-124">toolearn ulteriori informazioni sulla struttura di cartelle di Azure funzioni, hello vedere hello [Guida per sviluppatori di Azure funzioni](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="f606d-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="f606d-125">Al prompt dei comandi eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f606d-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="f606d-126">output di Hello è simile hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f606d-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="f606d-127">tooopt fuori la creazione di un repository Git, utilizzare l'opzione hello `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="f606d-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="f606d-128">File di impostazioni locali</span><span class="sxs-lookup"><span data-stu-id="f606d-128">Local settings file</span></span>

<span data-ttu-id="f606d-129">local.settings.json file Hello archivia le impostazioni dell'app, le stringhe di connessione e le impostazioni per strumenti di base di funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="f606d-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="f606d-130">Dispone di hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="f606d-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="f606d-131">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f606d-131">Setting</span></span>      | <span data-ttu-id="f606d-132">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f606d-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="f606d-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="f606d-133">**IsEncrypted**</span></span> | <span data-ttu-id="f606d-134">Quando impostato troppo**true**, tutti i valori sono crittografati utilizzando una chiave del computer locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="f606d-135">Usato con i comandi `func settings`.</span><span class="sxs-lookup"><span data-stu-id="f606d-135">Used with `func settings` commands.</span></span> <span data-ttu-id="f606d-136">Il valore predefinito è **false**.</span><span class="sxs-lookup"><span data-stu-id="f606d-136">Default value is **false**.</span></span> |
| <span data-ttu-id="f606d-137">**Valori**</span><span class="sxs-lookup"><span data-stu-id="f606d-137">**Values**</span></span> | <span data-ttu-id="f606d-138">Raccolta di impostazioni dell'applicazione usate durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="f606d-139">Aggiungere l'oggetto toothis le impostazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f606d-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="f606d-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="f606d-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="f606d-141">Set di hello toohello di stringa di connessione account di archiviazione di Azure che viene utilizzata internamente dal runtime di Azure funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="f606d-142">account di archiviazione Hello supporta i trigger della funzione.</span><span class="sxs-lookup"><span data-stu-id="f606d-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="f606d-143">Questa impostazione di connessione per l'account di archiviazione è obbligatorio per tutte le funzioni ad eccezione delle funzioni attivate da HTTP.</span><span class="sxs-lookup"><span data-stu-id="f606d-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="f606d-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="f606d-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="f606d-145">Imposta hello connessione stringa toohello account di archiviazione Azure che viene utilizzato toostore hello funzione log.</span><span class="sxs-lookup"><span data-stu-id="f606d-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="f606d-146">Questo valore facoltativo rende accessibile portale hello hello registri.</span><span class="sxs-lookup"><span data-stu-id="f606d-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="f606d-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="f606d-147">**Host**</span></span> | <span data-ttu-id="f606d-148">Le impostazioni in questa sezione personalizzare processo host di funzioni hello durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="f606d-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="f606d-149">**LocalHttpPort**</span></span> | <span data-ttu-id="f606d-150">Set di hello porta predefinita utilizzata quando si esegue l'host di funzioni locali hello (`func host start` e `func run`).</span><span class="sxs-lookup"><span data-stu-id="f606d-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="f606d-151">Hello `--port` opzione della riga di comando ha la precedenza su questo valore.</span><span class="sxs-lookup"><span data-stu-id="f606d-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="f606d-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="f606d-152">**CORS**</span></span> | <span data-ttu-id="f606d-153">Definisce le entità Origin hello consentita per [risorse multiorigine (CORS) di condivisione](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="f606d-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="f606d-154">Le origini sono elencate in un elenco delimitato dalla virgola senza spazi.</span><span class="sxs-lookup"><span data-stu-id="f606d-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="f606d-155">valore di carattere jolly Hello (**\***) è supportata, che consente le richieste provenienti da qualsiasi origine.</span><span class="sxs-lookup"><span data-stu-id="f606d-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="f606d-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="f606d-156">**ConnectionStrings**</span></span> | <span data-ttu-id="f606d-157">Contiene le stringhe di connessione database hello per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="f606d-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="f606d-158">Le stringhe di connessione in questo oggetto vengono aggiunti ambiente toohello con tipo di provider di hello di **SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="f606d-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="f606d-159">La maggior parte dei trigger e le associazioni presentano un **connessione** proprietà che esegue il mapping toohello nome di un'impostazione di app o variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="f606d-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="f606d-160">Per ogni proprietà di connessione, deve essere definita un'impostazione dell'app nel file local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f606d-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="f606d-161">Queste impostazioni possono anche essere lette nel codice come variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="f606d-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="f606d-162">In C# usare [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) o [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f606d-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="f606d-163">In JavaScript usare `process.env`.</span><span class="sxs-lookup"><span data-stu-id="f606d-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="f606d-164">Le impostazioni specificate come una variabile di ambiente del sistema hanno la precedenza sui valori nel file local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="f606d-165">Le impostazioni nel file local.settings.json hello vengono utilizzate solo per gli strumenti di funzioni durante l'esecuzione in locale.</span><span class="sxs-lookup"><span data-stu-id="f606d-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="f606d-166">Per impostazione predefinita, queste impostazioni non vengono migrate automaticamente al progetto hello tooAzure pubblicato.</span><span class="sxs-lookup"><span data-stu-id="f606d-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="f606d-167">Hello utilizzare `--publish-local-settings` passare [quando si pubblica](#publish) toomake che queste impostazioni vengono aggiunti toohello funzione app in Azure.</span><span class="sxs-lookup"><span data-stu-id="f606d-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="f606d-168">Quando in cui non è impostata alcuna stringa di connessione di archiviazione valida per **AzureWebJobsStorage**, hello seguente messaggio di errore viene visualizzato:</span><span class="sxs-lookup"><span data-stu-id="f606d-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="f606d-169">Valore mancante per AzureWebJobsStorage in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f606d-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="f606d-170">È necessario per tutti i trigger diversi da HTTP.</span><span class="sxs-lookup"><span data-stu-id="f606d-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="f606d-171">È possibile eseguire "func azure functionary fetch-app-settings <functionAppName>" o specificare una stringa di connessione in local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f606d-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="f606d-172">Configurare le impostazioni applicazione</span><span class="sxs-lookup"><span data-stu-id="f606d-172">Configure app settings</span></span>

<span data-ttu-id="f606d-173">tooset un valore per le stringhe di connessione, è possibile eseguire una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="f606d-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="f606d-174">Immettere la stringa di connessione hello da [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f606d-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="f606d-175">Utilizzare uno dei seguenti comandi hello:</span><span class="sxs-lookup"><span data-stu-id="f606d-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="f606d-176">Entrambi i comandi richiedono si toofirst Accedi tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f606d-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="f606d-177">Creare una funzione</span><span class="sxs-lookup"><span data-stu-id="f606d-177">Create a function</span></span>

<span data-ttu-id="f606d-178">toocreate una funzione, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f606d-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="f606d-179">`func new`hello supporta gli argomenti facoltativi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f606d-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="f606d-180">Argomento</span><span class="sxs-lookup"><span data-stu-id="f606d-180">Argument</span></span>     | <span data-ttu-id="f606d-181">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f606d-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="f606d-182">modello di Hello programmazione linguaggio, ad esempio c#, F # o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f606d-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="f606d-183">nome del modello Hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="f606d-184">nome della funzione Hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-184">hello function name.</span></span> |

<span data-ttu-id="f606d-185">Ad esempio, toocreate un trigger di JavaScript HTTP, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f606d-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="f606d-186">toocreate una funzione di attivazione coda, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f606d-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="f606d-187">Eseguire funzioni localmente</span><span class="sxs-lookup"><span data-stu-id="f606d-187">Run functions locally</span></span>

<span data-ttu-id="f606d-188">toorun un progetto di funzioni, hello funzioni host eseguito.</span><span class="sxs-lookup"><span data-stu-id="f606d-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="f606d-189">host di Hello Abilita i trigger per tutte le funzioni nel progetto hello:</span><span class="sxs-lookup"><span data-stu-id="f606d-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="f606d-190">`func host start`hello supporta le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f606d-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="f606d-191">Opzione</span><span class="sxs-lookup"><span data-stu-id="f606d-191">Option</span></span>     | <span data-ttu-id="f606d-192">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f606d-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="f606d-193">Hello porta locale toolisten in.</span><span class="sxs-lookup"><span data-stu-id="f606d-193">hello local port toolisten on.</span></span> <span data-ttu-id="f606d-194">Valore predefinito: 7071.</span><span class="sxs-lookup"><span data-stu-id="f606d-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="f606d-195">opzioni di Hello sono `VSCode` e `VS`.</span><span class="sxs-lookup"><span data-stu-id="f606d-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="f606d-196">Un elenco delimitato dalla virgola di origini CORS, senza spazi.</span><span class="sxs-lookup"><span data-stu-id="f606d-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="f606d-197">porta Hello hello nodo debugger toouse.</span><span class="sxs-lookup"><span data-stu-id="f606d-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="f606d-198">Predefinito: un valore di launch.json o 5858.</span><span class="sxs-lookup"><span data-stu-id="f606d-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="f606d-199">livello di traccia console Hello (disattivato, verbose, info, warning o error).</span><span class="sxs-lookup"><span data-stu-id="f606d-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="f606d-200">Predefinito: Info.</span><span class="sxs-lookup"><span data-stu-id="f606d-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="f606d-201">Hello timeout per l'avvio di hello funzioni host t o, in secondi.</span><span class="sxs-lookup"><span data-stu-id="f606d-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="f606d-202">Impostazione predefinita: 20 secondi.</span><span class="sxs-lookup"><span data-stu-id="f606d-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="f606d-203">Associare toohttps://localhost: {porta} anziché toohttp://localhost: {porta}.</span><span class="sxs-lookup"><span data-stu-id="f606d-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="f606d-204">Per impostazione predefinita, questa opzione crea un certificato attendibile nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f606d-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="f606d-205">Sospendere un input aggiuntivo prima della chiusura processo hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="f606d-206">Utile quando si avvia Strumenti di base di Funzioni di Azure da un ambiente di sviluppo integrato (IDE).</span><span class="sxs-lookup"><span data-stu-id="f606d-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="f606d-207">Quando viene avviato l'host di hello funzioni, funzioni di attivazione HTTP di URL hello restituisce come output:</span><span class="sxs-lookup"><span data-stu-id="f606d-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="f606d-208">Eseguire il debug in Visual Studio Code o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f606d-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="f606d-209">tooattach un debugger, passare hello `--debug` argomento.</span><span class="sxs-lookup"><span data-stu-id="f606d-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="f606d-210">le funzioni JavaScript toodebug, utilizzare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="f606d-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="f606d-211">Per le funzioni C#, usare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f606d-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="f606d-212">le funzioni toodebug c#, utilizzare `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="f606d-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="f606d-213">È anche possibile usare [Strumenti di Visual Studio 2017 per Funzioni di Azure](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="f606d-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="f606d-214">toolaunch hello host e impostare il debug di JavaScript, eseguire:</span><span class="sxs-lookup"><span data-stu-id="f606d-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="f606d-215">Quindi, nel codice di Visual Studio, in hello **Debug** visualizzazione, selezionare **allegare tooAzure funzioni**.</span><span class="sxs-lookup"><span data-stu-id="f606d-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="f606d-216">È possibile associare punti di interruzione, controllare variabili ed eseguire il codice passo per passo.</span><span class="sxs-lookup"><span data-stu-id="f606d-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Debug di JavaScript con Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="f606d-218">Funzione tooa dati di test passaggio</span><span class="sxs-lookup"><span data-stu-id="f606d-218">Passing test data tooa function</span></span>

<span data-ttu-id="f606d-219">È inoltre possibile richiamare una funzione direttamente tramite `func run <FunctionName>` e fornire i dati di input per la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="f606d-220">Questo comando è simile toorunning una funzione che usa hello **Test** scheda hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f606d-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="f606d-221">Questo comando Avvia host funzioni intera hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="f606d-222">`func run`hello supporta le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f606d-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="f606d-223">Opzione</span><span class="sxs-lookup"><span data-stu-id="f606d-223">Option</span></span>     | <span data-ttu-id="f606d-224">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f606d-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="f606d-225">Contenuto inline.</span><span class="sxs-lookup"><span data-stu-id="f606d-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="f606d-226">Collegare un processo host del debugger toohello prima di eseguire la funzione hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="f606d-227">Toowait tempo (in secondi) fino a quando l'host di funzioni locali hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="f606d-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="f606d-228">Hello toouse nome file come contenuto.</span><span class="sxs-lookup"><span data-stu-id="f606d-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="f606d-229">Non richiede input.</span><span class="sxs-lookup"><span data-stu-id="f606d-229">Does not prompt for input.</span></span> <span data-ttu-id="f606d-230">Utile per scenari di automazione.</span><span class="sxs-lookup"><span data-stu-id="f606d-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="f606d-231">Ad esempio, toocall una funzione di attivazione HTTP e corpo del contenuto di passaggio, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f606d-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="f606d-232"><a name="publish"></a>Pubblicare tooAzure</span><span class="sxs-lookup"><span data-stu-id="f606d-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="f606d-233">un'app di funzione funzioni tooa progetto in Azure, utilizzare hello toopublish `publish` comando:</span><span class="sxs-lookup"><span data-stu-id="f606d-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="f606d-234">È possibile utilizzare hello le opzioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f606d-234">You can use hello following options:</span></span>

| <span data-ttu-id="f606d-235">Opzione</span><span class="sxs-lookup"><span data-stu-id="f606d-235">Option</span></span>     | <span data-ttu-id="f606d-236">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f606d-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="f606d-237">Le impostazioni di pubblicazione in tooAzure local.settings.json, chiedere al toooverwrite se hello impostazione già esiste.</span><span class="sxs-lookup"><span data-stu-id="f606d-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="f606d-238">Deve essere usato con `-i`.</span><span class="sxs-lookup"><span data-stu-id="f606d-238">Must be used with `-i`.</span></span> <span data-ttu-id="f606d-239">Sovrascrive AppSettings in Azure con il valore locale se diverso.</span><span class="sxs-lookup"><span data-stu-id="f606d-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="f606d-240">Viene suggerito il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="f606d-240">Default is prompt.</span></span>|

<span data-ttu-id="f606d-241">Hello `publish` comando Carica il contenuto di hello della directory di progetto funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="f606d-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="f606d-242">Se si eliminano i file localmente, hello `publish` comando non vengono eliminati da Azure.</span><span class="sxs-lookup"><span data-stu-id="f606d-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="f606d-243">È possibile eliminare i file in Azure utilizzando hello [strumento Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="f606d-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f606d-244">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f606d-244">Next steps</span></span>

<span data-ttu-id="f606d-245">Strumenti di base di Funzioni di Azure è [open source ed è ospitato su GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="f606d-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="f606d-246">una richiesta di bug o funzionalità toofile [aprire un problema di GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="f606d-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[strumenti di base di Azure funzioni]: https://www.npmjs.com/package/azure-functions-core-tools
[portale di Azure]: https://portal.azure.com 
