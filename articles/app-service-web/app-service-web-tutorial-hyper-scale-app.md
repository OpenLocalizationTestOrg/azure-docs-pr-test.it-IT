---
title: "Creare un'app con iperscalabilità in Azure | Microsoft Docs"
description: Informazioni su come usare i diversi servizi di Azure per ottimizzare le prestazioni di un'applicazione ASP.NET in Azure.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="a017b-103">Creare un'app Web con iperscalabilità in Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="a017b-104">Questa esercitazione illustra come scalare orizzontalmente un'app Web ASP.NET in Azure per ottimizzare le richieste degli utenti.</span><span class="sxs-lookup"><span data-stu-id="a017b-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="a017b-105">Prima di iniziare, verificare che nel computer sia [installata l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a017b-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="a017b-106">È necessario anche disporre di [Visual Studio](https://www.visualstudio.com/vs/) sul computer locale per eseguire l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="a017b-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="a017b-107">Passaggio 1: applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="a017b-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="a017b-108">In questo passaggio si imposta il progetto ASP.NET locale.</span><span class="sxs-lookup"><span data-stu-id="a017b-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="a017b-109">Clonare il repository di applicazione</span><span class="sxs-lookup"><span data-stu-id="a017b-109">Clone the application repository</span></span>

<span data-ttu-id="a017b-110">Aprire il terminale della riga di comando desiderato ed eseguire `CD` in una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a017b-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="a017b-111">Eseguire quindi i comandi seguenti per clonare l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="a017b-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="a017b-112">Eseguire l'applicazione in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a017b-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="a017b-113">Aprire la soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a017b-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="a017b-114">Digitare `F5` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a017b-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="a017b-115">Questa app Web ASP.NET di esempio deriva dal modello predefinito, mantiene le sessioni degli utenti e usa la cache di output.</span><span class="sxs-lookup"><span data-stu-id="a017b-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="a017b-116">Vedere `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="a017b-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="a017b-117">Il metodo `Index()` aggiunge una parte di dati alla sessione.</span><span class="sxs-lookup"><span data-stu-id="a017b-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="a017b-118">I metodi `About()` e `Contact()` memorizzano il relativo output nella cache.</span><span class="sxs-lookup"><span data-stu-id="a017b-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="a017b-119">Passaggio 2: distribuire in Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="a017b-120">In questo passaggio si crea un'app Web di Azure, per poi distribuire in essa l'applicazione ASP.NET di esempio.</span><span class="sxs-lookup"><span data-stu-id="a017b-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="a017b-121">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="a017b-121">Create a resource group</span></span>   
<span data-ttu-id="a017b-122">Usare il comando [az group create](https://docs.microsoft.com/cli/azure/group#create) per creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) nell'area Europa occidentale.</span><span class="sxs-lookup"><span data-stu-id="a017b-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="a017b-123">In un gruppo di risorse si inseriranno tutte le risorse che si vogliono gestire insieme, ad esempio l'app Web e il back-end del database SQL.</span><span class="sxs-lookup"><span data-stu-id="a017b-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="a017b-124">Per visualizzare i possibili valori utilizzabili per `---location`, usare il comando [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="a017b-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="a017b-125">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="a017b-125">Create an App Service plan</span></span>
<span data-ttu-id="a017b-126">Usare il comando [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) per creare un [piano di servizio app](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) "B1".</span><span class="sxs-lookup"><span data-stu-id="a017b-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="a017b-127">Un piano di servizio app è un'unità di scala, che può includere il numero desiderato di app da scalare verticalmente oppure orizzontalmente, oltre alla medesima infrastruttura del servizio app.</span><span class="sxs-lookup"><span data-stu-id="a017b-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="a017b-128">A ogni piano viene inoltre assegnato un [piano tariffario](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a017b-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="a017b-129">I piani tariffari superiori includono un hardware migliore e più caratteristiche, ad esempio un numero maggiore di istanze di scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="a017b-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="a017b-130">Per questa esercitazione, B1 è il livello minimo che consente la scalabilità orizzontale in tre istanze.</span><span class="sxs-lookup"><span data-stu-id="a017b-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="a017b-131">È sempre possibile modificare il piano tariffario dell'app in un secondo momento eseguendo il comando [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="a017b-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="a017b-132">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="a017b-132">Create a web app</span></span>
<span data-ttu-id="a017b-133">Usare il comando [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) per creare un'app Web con un nome univoco in `$appName`.</span><span class="sxs-lookup"><span data-stu-id="a017b-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="a017b-134">Reimpostare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="a017b-134">Set deployment credentials</span></span>
<span data-ttu-id="a017b-135">Usare il comando [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) per impostare le credenziali di distribuzione a livello di account per il servizio app.</span><span class="sxs-lookup"><span data-stu-id="a017b-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="a017b-136">Configurare la distribuzione Git</span><span class="sxs-lookup"><span data-stu-id="a017b-136">Configure Git deployment</span></span>
<span data-ttu-id="a017b-137">Usare il comando [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) per configurare la distribuzione Git locale.</span><span class="sxs-lookup"><span data-stu-id="a017b-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="a017b-138">Questo comando fornisce un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a017b-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="a017b-139">Usare l'URL restituito per configurare Git remoto.</span><span class="sxs-lookup"><span data-stu-id="a017b-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="a017b-140">Il comando seguente usa l'esempio di output precedente.</span><span class="sxs-lookup"><span data-stu-id="a017b-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="a017b-141">Distribuire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="a017b-141">Deploy the sample application</span></span>
<span data-ttu-id="a017b-142">È ora possibile distribuire l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="a017b-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="a017b-143">Eseguire `git push`.</span><span class="sxs-lookup"><span data-stu-id="a017b-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="a017b-144">Quando viene richiesta la password, usare quella specificata all'esecuzione di `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="a017b-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="a017b-145">Passare all'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-145">Browse to Azure web app</span></span>
<span data-ttu-id="a017b-146">Usare il comando [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) per osservare l'app in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="a017b-147">Passaggio 3: connettersi a Redis</span><span class="sxs-lookup"><span data-stu-id="a017b-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="a017b-148">In questo passaggio si configura una cache Redis di Azure come una cache esterna con percorso condiviso nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="a017b-149">È possibile usare rapidamente Redis per memorizzare nella cache l'output della pagina.</span><span class="sxs-lookup"><span data-stu-id="a017b-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="a017b-150">In più, quando si scalano orizzontalmente le app Web in un secondo momento, Redis aiuta a mantenere le sessioni degli utenti su più istanze in maniera affidabile.</span><span class="sxs-lookup"><span data-stu-id="a017b-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="a017b-151">Creare una cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="a017b-152">Usare il comando [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) per creare una cache Redis di Azure e salvare l'output JSON.</span><span class="sxs-lookup"><span data-stu-id="a017b-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="a017b-153">Usare un nome univoco in `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="a017b-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="a017b-154">Configurare l'applicazione per l'uso di Redis</span><span class="sxs-lookup"><span data-stu-id="a017b-154">Configure the application to use Redis</span></span>
<span data-ttu-id="a017b-155">Formattare la stringa di connessione per la cache.</span><span class="sxs-lookup"><span data-stu-id="a017b-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="a017b-156">La seconda riga dovrebbe mostrare un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a017b-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="a017b-157">In Visual Studio creare un file di configurazione Web nella radice del progetto denominato `redis.config` e incollarvi il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="a017b-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="a017b-158">In `value` usare la stringa di connessione dall'output di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a017b-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="a017b-159">Se si osserva il file `.gitignore` nel repository Git, si noterà che è escluso dal controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="a017b-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="a017b-160">In questo modo le informazioni riservate vengono protette.</span><span class="sxs-lookup"><span data-stu-id="a017b-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="a017b-161">Aprire `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="a017b-161">Open `Web.config`.</span></span> <span data-ttu-id="a017b-162">Si noti l'elemento `<appSettings file="redis.config">`, che riceve l'impostazione creata in `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="a017b-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="a017b-163">Individuare la sezione commentata che include `<sessionState>` e `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="a017b-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="a017b-164">Rimuovere il commento in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="a017b-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="a017b-165">Questo codice cerca la stringa di connessione a Redis definita in `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="a017b-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="a017b-166">Ora l'applicazione usa Redis per gestire sessioni e memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="a017b-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="a017b-167">Digitare `F5` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a017b-167">Type `F5` to run the application.</span></span> <span data-ttu-id="a017b-168">Se si desidera, è possibile scaricare un client di gestione di Redis per visualizzare i dati salvati nella cache.</span><span class="sxs-lookup"><span data-stu-id="a017b-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="a017b-169">Configurare la stringa di connessione in Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="a017b-170">Per far funzionare l'applicazione in Azure è necessario configurare la medesima stringa di connessione a Redis nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="a017b-171">Poiché `redis.config` non viene mantenuto nel controllo del codice sorgente, non viene distribuito in Azure quando si esegue la distribuzione Git.</span><span class="sxs-lookup"><span data-stu-id="a017b-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="a017b-172">Usare il comando [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) per aggiungere la stringa di connessione con lo stesso nome (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="a017b-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="a017b-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a017b-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="a017b-174">Tenere presente che `$connstring` contiene la stringa di connessione formattata.</span><span class="sxs-lookup"><span data-stu-id="a017b-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="a017b-175">Ridistribuire l'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="a017b-176">Usare i comandi di Git per inviare le modifiche in Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="a017b-177">Quando viene richiesta la password, usare quella specificata all'esecuzione di `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="a017b-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="a017b-178">Passare all'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="a017b-178">Browse to the Azure web app</span></span>
<span data-ttu-id="a017b-179">Usare il comando [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) per visualizzare le modifiche pubblicate in Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="a017b-180">Passaggio 4: scalare in più istanze</span><span class="sxs-lookup"><span data-stu-id="a017b-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="a017b-181">Il piano di servizio app è l'unità di scala per le app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="a017b-182">Per scalare orizzontalmente l'app Web, è necessario scalare il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a017b-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="a017b-183">Usare il comando [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) per scalare orizzontalmente il piano di servizio app in tre istanze, ovvero il numero massimo consentito dal piano tariffario B1.</span><span class="sxs-lookup"><span data-stu-id="a017b-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="a017b-184">Tenere presente che B1 è il piano tariffario scelto quando in precedenza si è creato il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a017b-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="a017b-185">Passaggio 5: scalare geograficamente</span><span class="sxs-lookup"><span data-stu-id="a017b-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="a017b-186">Durante la scalabilità geografica, si esegue l'app in più aree del cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="a017b-187">Questa configurazione bilancia ulteriormente il carico dell'app in base all'area geografica e riduce i tempi di risposta posizionandola più vicina ai browser client.</span><span class="sxs-lookup"><span data-stu-id="a017b-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="a017b-188">In questo passaggio si scala l'app Web ASP.NET in una seconda area con [Gestione traffico di Azure](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="a017b-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="a017b-189">Al termine del passaggio, si otterrà un'app Web in esecuzione in Europa occidentale (già creata) e un'app Web in esecuzione in Asia sud-orientale (non ancora creata).</span><span class="sxs-lookup"><span data-stu-id="a017b-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="a017b-190">Entrambe le app verranno servite dallo stesso URL di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="a017b-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="a017b-191">Scalare l'app Europa al livello Standard</span><span class="sxs-lookup"><span data-stu-id="a017b-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="a017b-192">Nel servizio app l'integrazione con Gestione traffico di Azure richiede il piano tariffario Standard.</span><span class="sxs-lookup"><span data-stu-id="a017b-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="a017b-193">Usare il comando [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) per far passare a S1 il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="a017b-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="a017b-194">Creare un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="a017b-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="a017b-195">Usare il comando [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) per creare un profilo di Gestione traffico e aggiungerlo al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a017b-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="a017b-196">Usare un nome DNS univoco in $dnsName.</span><span class="sxs-lookup"><span data-stu-id="a017b-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="a017b-197">`--routing-method Performance` specifica che questo profilo [instrada il traffico utente all'endpoint più vicino](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="a017b-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="a017b-198">Ottenere l'ID risorsa dell'app Europa</span><span class="sxs-lookup"><span data-stu-id="a017b-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="a017b-199">Usare il comando [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) per ottenere l'ID risorsa dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="a017b-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="a017b-200">Aggiungere un endpoint di Gestione traffico per l'app Europa</span><span class="sxs-lookup"><span data-stu-id="a017b-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="a017b-201">Usare il comando [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) per aggiungere un endpoint al profilo di Gestione traffico e usare l'ID risorsa dell'app Web come destinazione.</span><span class="sxs-lookup"><span data-stu-id="a017b-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="a017b-202">Ottenere l'URL dell'endpoint di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="a017b-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="a017b-203">Ora il profilo di Gestione traffico dispone di un endpoint che punta all'app Web esistente.</span><span class="sxs-lookup"><span data-stu-id="a017b-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="a017b-204">Usare il comando [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) per ottenere l'URL.</span><span class="sxs-lookup"><span data-stu-id="a017b-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="a017b-205">Copiare l'output nel browser.</span><span class="sxs-lookup"><span data-stu-id="a017b-205">Copy the output into your browser.</span></span> <span data-ttu-id="a017b-206">Dovrebbe essere visualizzata nuovamente l'app Web.</span><span class="sxs-lookup"><span data-stu-id="a017b-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="a017b-207">Creare una cache Redis di Azure in Asia</span><span class="sxs-lookup"><span data-stu-id="a017b-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="a017b-208">Ora si vedrà come replicare l'app Web di Azure nell'area Asia sud-orientale.</span><span class="sxs-lookup"><span data-stu-id="a017b-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="a017b-209">Per iniziare, usare il comando [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) per creare una seconda cache Redis di Azure in Asia sud-orientale.</span><span class="sxs-lookup"><span data-stu-id="a017b-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="a017b-210">Questa cache deve disporre di un percorso condiviso con l'app in Asia.</span><span class="sxs-lookup"><span data-stu-id="a017b-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="a017b-211">`--name $cacheName-asia` fornisce alla cache il nome della cache in Europa occidentale, con il suffisso `-asia`.</span><span class="sxs-lookup"><span data-stu-id="a017b-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="a017b-212">Creare un piano di servizio app in Asia</span><span class="sxs-lookup"><span data-stu-id="a017b-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="a017b-213">Usare il comando [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) per creare un secondo piano di servizio app nell'area Asia sud-orientale, usando il medesimo piano tariffario dell'area Europa occidentale (S1).</span><span class="sxs-lookup"><span data-stu-id="a017b-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="a017b-214">Creare un'app Web in Asia</span><span class="sxs-lookup"><span data-stu-id="a017b-214">Create a web app in Asia</span></span>
<span data-ttu-id="a017b-215">Usare il comando [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) per creare una seconda app Web.</span><span class="sxs-lookup"><span data-stu-id="a017b-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="a017b-216">`--name $appName-asia` fornisce all'app il nome dell'app in Europa occidentale, con il suffisso `-asia`.</span><span class="sxs-lookup"><span data-stu-id="a017b-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="a017b-217">Configurare la stringa di connessione per Redis</span><span class="sxs-lookup"><span data-stu-id="a017b-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="a017b-218">Usare il comando [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) per aggiungere la stringa di connessione per la cache in Asia sud-orientale all'app Web.</span><span class="sxs-lookup"><span data-stu-id="a017b-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="a017b-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a017b-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="a017b-220">Configurare la distribuzione Git per l'app in Asia.</span><span class="sxs-lookup"><span data-stu-id="a017b-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="a017b-221">Usare il comando [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) per configurare la distribuzione Git locale per la seconda app Web.</span><span class="sxs-lookup"><span data-stu-id="a017b-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="a017b-222">Questo comando fornisce un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a017b-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="a017b-223">Usare l'URL restituito per configurare un secondo Git remoto per il repository locale.</span><span class="sxs-lookup"><span data-stu-id="a017b-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="a017b-224">Il comando seguente usa l'esempio di output precedente.</span><span class="sxs-lookup"><span data-stu-id="a017b-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="a017b-225">Distribuire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="a017b-225">Deploy your sample application</span></span>
<span data-ttu-id="a017b-226">Eseguire `git push` per distribuire l'applicazione di esempio nel secondo Git remoto.</span><span class="sxs-lookup"><span data-stu-id="a017b-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="a017b-227">Quando viene richiesta la password, usare quella specificata all'esecuzione di `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="a017b-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="a017b-228">Passare all'app Asia</span><span class="sxs-lookup"><span data-stu-id="a017b-228">Browse to the Asia app</span></span>
<span data-ttu-id="a017b-229">Usare il comando [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) per accertarsi che l'app sia in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="a017b-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="a017b-230">Ottenere l'ID risorsa dell'app Asia</span><span class="sxs-lookup"><span data-stu-id="a017b-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="a017b-231">Usare il comando [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) per ottenere l'ID risorsa dell'app Web in Asia sud-orientale.</span><span class="sxs-lookup"><span data-stu-id="a017b-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="a017b-232">Aggiungere un endpoint di Gestione traffico per l'app Asia</span><span class="sxs-lookup"><span data-stu-id="a017b-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="a017b-233">Usare il comando [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) per aggiungere un secondo endpoint al profilo di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="a017b-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="a017b-234">Aggiungere un identificatore di area alle app Web</span><span class="sxs-lookup"><span data-stu-id="a017b-234">Add region identifier to web apps</span></span>
<span data-ttu-id="a017b-235">Usare il comando [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) per aggiungere una variabile di ambiente specifica per l'area.</span><span class="sxs-lookup"><span data-stu-id="a017b-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="a017b-236">Il codice dell'applicazione usa già questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="a017b-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="a017b-237">Vedere `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="a017b-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="a017b-238">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="a017b-238">Complete!</span></span>

<span data-ttu-id="a017b-239">A questo punto, provare ad accedere all'URL del profilo di Gestione traffico da browser in aree geografiche diverse.</span><span class="sxs-lookup"><span data-stu-id="a017b-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="a017b-240">I browser client situati in Europa dovrebbero mostrare "ASP.NET Europa occidentale", mentre quelli in Asia dovrebbero mostrare "ASP.NET Asia sud-orientale".</span><span class="sxs-lookup"><span data-stu-id="a017b-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="a017b-241">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="a017b-241">More resources</span></span>
