---
title: aaaBuild un'app con in Azure | Documenti Microsoft
description: Informazioni su come toouse diversi servizi Azure toomaximize hello delle prestazioni di un'applicazione ASP.NET in Azure.
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
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="c023d-103">Creare un'app Web con iperscalabilità in Azure</span><span class="sxs-lookup"><span data-stu-id="c023d-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="c023d-104">Questa esercitazione viene illustrato come tooscale un'App web ASP.NET in Azure toomaximize utente richieste.</span><span class="sxs-lookup"><span data-stu-id="c023d-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="c023d-105">Prima di iniziare questa esercitazione, assicurarsi che [hello CLI di Azure è installato](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) nel computer.</span><span class="sxs-lookup"><span data-stu-id="c023d-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="c023d-106">Inoltre, è necessario [Visual Studio](https://www.visualstudio.com/vs/) sull'applicazione di esempio hello toorun computer locale.</span><span class="sxs-lookup"><span data-stu-id="c023d-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="c023d-107">Passaggio 1: applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="c023d-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="c023d-108">In questo passaggio, impostare il progetto ASP.NET locale di hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="c023d-109">Repository di applicazione hello clone</span><span class="sxs-lookup"><span data-stu-id="c023d-109">Clone hello application repository</span></span>

<span data-ttu-id="c023d-110">Terminal della riga di comando di hello aperto di propria scelta e `CD` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c023d-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="c023d-111">Quindi, seguente hello esecuzione comandi tooclone l'applicazione di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="c023d-112">Eseguire l'applicazione di esempio hello in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c023d-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="c023d-113">Aprire la soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c023d-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="c023d-114">Tipo `F5` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="c023d-115">Questa applicazione web ASP.NET di esempio proviene dal modello predefinito hello e persiste utente sessioni e utilizza hello cache di output.</span><span class="sxs-lookup"><span data-stu-id="c023d-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="c023d-116">Vedere `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="c023d-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="c023d-117">Hello `Index()` metodo aggiunge una parte della sessione toohello dati.</span><span class="sxs-lookup"><span data-stu-id="c023d-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="c023d-118">Hello e `About()` e `Contact()` metodi di memorizzare nella cache l'output.</span><span class="sxs-lookup"><span data-stu-id="c023d-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="c023d-119">Passaggio 2: distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="c023d-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="c023d-120">In questo passaggio, creare un'app web di Azure e distribuire il tooit applicazione ASP.NET di esempio.</span><span class="sxs-lookup"><span data-stu-id="c023d-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="c023d-121">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c023d-121">Create a resource group</span></span>   
<span data-ttu-id="c023d-122">Utilizzare [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) toocreate un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) nell'area Europa occidentale hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="c023d-123">È di un gruppo di risorse in cui inserire tutti hello risorse di Azure che si desidera toomanage insieme, ad esempio hello web app e tutti i Database SQL back-end.</span><span class="sxs-lookup"><span data-stu-id="c023d-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="c023d-124">toosee i possibili valori da utilizzare per `---location`, utilizzare hello [az appservice elenco posizioni](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) comando.</span><span class="sxs-lookup"><span data-stu-id="c023d-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="c023d-125">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="c023d-125">Create an App Service plan</span></span>
<span data-ttu-id="c023d-126">Utilizzare [crea piano di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [piano di servizio App](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c023d-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="c023d-127">Un piano di servizio App è un'unità di scala, che può includere qualsiasi numero di applicazioni che si desidera tooscale o out over insieme hello stessa infrastruttura di servizio App.</span><span class="sxs-lookup"><span data-stu-id="c023d-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="c023d-128">A ogni piano viene inoltre assegnato un [piano tariffario](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="c023d-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="c023d-129">I piani tariffari superiori includono un hardware migliore e più caratteristiche, ad esempio un numero maggiore di istanze di scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="c023d-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="c023d-130">Per questa esercitazione, B1 è livello minimo di hello che consente la scalabilità orizzontale toothree istanze.</span><span class="sxs-lookup"><span data-stu-id="c023d-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="c023d-131">È sempre possibile spostare l'app verso l'alto o verso il basso hello piano tariffario in un secondo momento eseguendo [aggiornamento piani di az appservice](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="c023d-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="c023d-132">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="c023d-132">Create a web app</span></span>
<span data-ttu-id="c023d-133">Utilizzare [web appservice az creare](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate un'app web con un nome univoco in `$appName`.</span><span class="sxs-lookup"><span data-stu-id="c023d-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="c023d-134">Reimpostare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="c023d-134">Set deployment credentials</span></span>
<span data-ttu-id="c023d-135">Utilizzare [az appservice web distribuzione utente set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset credenziali la distribuzione a livello di account di servizio App.</span><span class="sxs-lookup"><span data-stu-id="c023d-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="c023d-136">Configurare la distribuzione Git</span><span class="sxs-lookup"><span data-stu-id="c023d-136">Configure Git deployment</span></span>
<span data-ttu-id="c023d-137">Utilizzare [az appservice web controllo del codice sorgente config-locale-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) distribuzione Git locale tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c023d-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="c023d-138">Questo comando consente un output simile al seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c023d-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="c023d-139">Hello utilizzare restituito tooconfigure URL il Git remote.</span><span class="sxs-lookup"><span data-stu-id="c023d-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="c023d-140">Hello comando che segue utilizza hello precedente esempio di output.</span><span class="sxs-lookup"><span data-stu-id="c023d-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="c023d-141">Distribuire l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="c023d-141">Deploy hello sample application</span></span>
<span data-ttu-id="c023d-142">Si sono ora pronti toodeploy l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="c023d-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="c023d-143">Eseguire `git push`.</span><span class="sxs-lookup"><span data-stu-id="c023d-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="c023d-144">Quando viene richiesta la password, utilizzare password hello specificato al momento dell'esecuzione `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="c023d-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="c023d-145">Sfoglia tooAzure web app</span><span class="sxs-lookup"><span data-stu-id="c023d-145">Browse tooAzure web app</span></span>
<span data-ttu-id="c023d-146">Utilizzare [Sfoglia web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee l'app in esecuzione in tempo reale in Azure, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="c023d-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="c023d-147">Passaggio 3: connettere tooRedis</span><span class="sxs-lookup"><span data-stu-id="c023d-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="c023d-148">In questo passaggio è Cache Redis di Azure come applicazione web di Azure tooyour cache esterna, con percorso condiviso.</span><span class="sxs-lookup"><span data-stu-id="c023d-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="c023d-149">È possibile utilizzare rapidamente Redis toocache l'output delle pagine.</span><span class="sxs-lookup"><span data-stu-id="c023d-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="c023d-150">In più, quando si scalano orizzontalmente le app Web in un secondo momento, Redis aiuta a mantenere le sessioni degli utenti su più istanze in maniera affidabile.</span><span class="sxs-lookup"><span data-stu-id="c023d-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="c023d-151">Creare una cache Redis di Azure</span><span class="sxs-lookup"><span data-stu-id="c023d-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="c023d-152">Utilizzare [redis az creare](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un Azure Redis Cache e di salvataggio hello output JSON.</span><span class="sxs-lookup"><span data-stu-id="c023d-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="c023d-153">Usare un nome univoco in `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="c023d-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="c023d-154">Configurare l'applicazione di hello toouse Redis</span><span class="sxs-lookup"><span data-stu-id="c023d-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="c023d-155">Formato stringa di connessione hello per la cache.</span><span class="sxs-lookup"><span data-stu-id="c023d-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="c023d-156">seconda riga Hello deve fornire un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c023d-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="c023d-157">In Visual Studio, creare un file di configurazione web nella radice del progetto denominato `redis.config` e Incolla hello seguente codice al suo interno.</span><span class="sxs-lookup"><span data-stu-id="c023d-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="c023d-158">In `value`, utilizzare la stringa di connessione hello da hello output di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c023d-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="c023d-159">Se si osserva hello `.gitignore` file del repository Git, si noterà che il file è stato escluso dal controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="c023d-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="c023d-160">In questo modo le informazioni riservate vengono protette.</span><span class="sxs-lookup"><span data-stu-id="c023d-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="c023d-161">Aprire `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="c023d-161">Open `Web.config`.</span></span> <span data-ttu-id="c023d-162">Hello preavviso `<appSettings file="redis.config">` elemento, che ottiene l'impostazione di hello è stato creato in `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="c023d-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="c023d-163">Trovare hello commentato sezione che include `<sessionState>` e `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="c023d-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="c023d-164">Rimuovere il commento in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c023d-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="c023d-165">Questo codice esegue la ricerca di stringa di connessione Redis hello è definito in `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="c023d-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="c023d-166">A questo punto l'applicazione utilizza le sessioni toomanage di Redis e la memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="c023d-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="c023d-167">Tipo `F5` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="c023d-168">Se si desidera, è possibile scaricare un Redis gestione client toovisualize hello dati ora salvati toohello cache.</span><span class="sxs-lookup"><span data-stu-id="c023d-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="c023d-169">Configurare la stringa di connessione hello in Azure</span><span class="sxs-lookup"><span data-stu-id="c023d-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="c023d-170">Per toowork l'applicazione in Azure, è necessario tooconfigure hello stessa stringa di connessione Redis nell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c023d-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="c023d-171">Poiché `redis.config` non viene mantenuto nel controllo del codice sorgente, non è distribuito tooAzure quando si esegue la distribuzione Git.</span><span class="sxs-lookup"><span data-stu-id="c023d-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="c023d-172">Utilizzare [az appservice web configurazione appsettings aggiornare](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) stringa di connessione hello tooadd con hello stesso nome (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="c023d-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="c023d-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c023d-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="c023d-174">Tenere presente che `$connstring` contiene la stringa di connessione hello formattato.</span><span class="sxs-lookup"><span data-stu-id="c023d-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="c023d-175">Ridistribuire tooAzure applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c023d-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="c023d-176">Utilizzare toopush comandi Git tooAzure le modifiche</span><span class="sxs-lookup"><span data-stu-id="c023d-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="c023d-177">Quando viene richiesta la password, utilizzare password hello specificato al momento dell'esecuzione `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="c023d-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="c023d-178">Sfoglia toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="c023d-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="c023d-179">Utilizzare [Sfoglia web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) modifiche hello toosee risiedono in Azure.</span><span class="sxs-lookup"><span data-stu-id="c023d-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="c023d-180">Passaggio 4: istanze toomultiple scala</span><span class="sxs-lookup"><span data-stu-id="c023d-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="c023d-181">piano di servizio App Hello è l'unità di scala hello per le app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c023d-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="c023d-182">tooscale all'app web, è la scalabilità hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="c023d-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="c023d-183">Utilizzare [aggiornamento piani di az appservice](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale istanze di toothree piano di servizio App hello, che è il numero massimo consentito dal piano tariffario di hello B1 di hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="c023d-184">Tenere presente che B1 hello tariffario scelto al momento della creazione piano di servizio App in precedenza hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="c023d-185">Passaggio 5: scalare geograficamente</span><span class="sxs-lookup"><span data-stu-id="c023d-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="c023d-186">Quando si ridimensiona geograficamente, si esegue l'app in più aree di hello cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="c023d-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="c023d-187">Questo programma di installazione di bilanciamento del carico dell'app ulteriormente in base a geography e riduce il tempo di risposta hello inserendo browser tooclient più vicino di app.</span><span class="sxs-lookup"><span data-stu-id="c023d-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="c023d-188">In questo passaggio si modifica la scala ASP.NET web app tooa secondo paese con [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="c023d-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="c023d-189">Alla fine di hello del passaggio di hello, si avrà un'app web in esecuzione in Europa occidentale (già creato) e un'app web in esecuzione in Asia sudorientale (non ancora creato).</span><span class="sxs-lookup"><span data-stu-id="c023d-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="c023d-190">Verranno utilizzate entrambe le app da hello stesso URL di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="c023d-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="c023d-191">Applicare la scalabilità verticale hello livello tooStandard di app Europa</span><span class="sxs-lookup"><span data-stu-id="c023d-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="c023d-192">Nel servizio App, integrazione con gestione traffico di Azure richiede il livello di prezzo Standard di hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="c023d-193">Utilizzare [aggiornamento piani di az appservice](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale backup il tooS1 piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="c023d-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="c023d-194">Creare un profilo di Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="c023d-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="c023d-195">Utilizzare [Crea profilo di gestione traffico di rete az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate un traffico di gestione del profilo e aggiungere il gruppo di risorse tooyour.</span><span class="sxs-lookup"><span data-stu-id="c023d-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="c023d-196">Usare un nome DNS univoco in $dnsName.</span><span class="sxs-lookup"><span data-stu-id="c023d-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="c023d-197">`--routing-method Performance`Specifica che il profilo [instrada endpoint più vicino di utente traffico toohello](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="c023d-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="c023d-198">Ottenere l'ID di risorsa hello di hello Europa app</span><span class="sxs-lookup"><span data-stu-id="c023d-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="c023d-199">Utilizzare [per web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello ID di risorsa dell'app web.</span><span class="sxs-lookup"><span data-stu-id="c023d-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="c023d-200">Aggiungere un endpoint di gestione traffico per app di hello Europa</span><span class="sxs-lookup"><span data-stu-id="c023d-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="c023d-201">Utilizzare [creare endpoint di gestione traffico di rete az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un profilo di gestione traffico di tooyour endpoint e l'ID di risorsa di hello di utilizzo dell'app web come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="c023d-202">Ottenere l'URL dell'endpoint di gestione traffico hello</span><span class="sxs-lookup"><span data-stu-id="c023d-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="c023d-203">Profilo di Traffic Manager dispone ora di un endpoint che punti tooyour esistente web app.</span><span class="sxs-lookup"><span data-stu-id="c023d-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="c023d-204">Utilizzare [az rete gestione traffico profilo visualizzare](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget il relativo URL.</span><span class="sxs-lookup"><span data-stu-id="c023d-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="c023d-205">Copia output di hello nel browser.</span><span class="sxs-lookup"><span data-stu-id="c023d-205">Copy hello output into your browser.</span></span> <span data-ttu-id="c023d-206">Dovrebbe essere visualizzata nuovamente l'app Web.</span><span class="sxs-lookup"><span data-stu-id="c023d-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="c023d-207">Creare una cache Redis di Azure in Asia</span><span class="sxs-lookup"><span data-stu-id="c023d-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="c023d-208">A questo punto, si replica l'area geografica di Azure web app toohello Asia sudorientale.</span><span class="sxs-lookup"><span data-stu-id="c023d-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="c023d-209">toostart, utilizzare [redis az creare](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un secondo Cache Redis di Azure in Asia sudorientale.</span><span class="sxs-lookup"><span data-stu-id="c023d-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="c023d-210">Questa cache deve toobe installato con l'app in Asia.</span><span class="sxs-lookup"><span data-stu-id="c023d-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="c023d-211">`--name $cacheName-asia`Consente di hello Nome hello della cache di hello cache Europa occidentale, con hello `-asia` suffisso.</span><span class="sxs-lookup"><span data-stu-id="c023d-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="c023d-212">Creare un piano di servizio app in Asia</span><span class="sxs-lookup"><span data-stu-id="c023d-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="c023d-213">Utilizzare [crea piano di servizio App az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate un servizio App secondo piano nell'area Asia sudorientale hello, utilizzando hello S1 stesso livello del piano di hello Europa occidentale.</span><span class="sxs-lookup"><span data-stu-id="c023d-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="c023d-214">Creare un'app Web in Asia</span><span class="sxs-lookup"><span data-stu-id="c023d-214">Create a web app in Asia</span></span>
<span data-ttu-id="c023d-215">Utilizzare [web appservice az creare](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate un'app web di secondo.</span><span class="sxs-lookup"><span data-stu-id="c023d-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="c023d-216">`--name $appName-asia`Consente di hello Nome hello app di app hello Europa occidentale, con hello `-asia` suffisso.</span><span class="sxs-lookup"><span data-stu-id="c023d-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="c023d-217">Configurare la stringa di connessione hello per Redis</span><span class="sxs-lookup"><span data-stu-id="c023d-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="c023d-218">Utilizzare [az appservice web configurazione appsettings aggiornare](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connessione per hello cache Asia sudorientale.</span><span class="sxs-lookup"><span data-stu-id="c023d-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="c023d-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c023d-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="c023d-220">Configurare la distribuzione Git per app Asia hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="c023d-221">Utilizzare [az appservice web controllo del codice sorgente config-locale-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure la distribuzione Git locale per l'app web secondo hello.</span><span class="sxs-lookup"><span data-stu-id="c023d-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="c023d-222">Questo comando consente un output simile al seguente hello:</span><span class="sxs-lookup"><span data-stu-id="c023d-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="c023d-223">Hello utilizzare restituito tooconfigure URL un secondo Git remoto per il repository locale.</span><span class="sxs-lookup"><span data-stu-id="c023d-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="c023d-224">Hello comando che segue utilizza hello precedente esempio di output.</span><span class="sxs-lookup"><span data-stu-id="c023d-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="c023d-225">Distribuire l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="c023d-225">Deploy your sample application</span></span>
<span data-ttu-id="c023d-226">Eseguire `git push` toodeploy remoto Git secondo l'esempio applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="c023d-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="c023d-227">Quando viene richiesta la password, utilizzare password hello specificato al momento dell'esecuzione `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="c023d-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="c023d-228">Esplorare app Asia toohello</span><span class="sxs-lookup"><span data-stu-id="c023d-228">Browse toohello Asia app</span></span>
<span data-ttu-id="c023d-229">Utilizzare [Sfoglia web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify l'app è in esecuzione in tempo reale in Azure.</span><span class="sxs-lookup"><span data-stu-id="c023d-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="c023d-230">Ottenere l'ID di risorsa hello di hello Asia app</span><span class="sxs-lookup"><span data-stu-id="c023d-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="c023d-231">Utilizzare [per web di servizio App az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello ID di risorsa dell'app web in Asia sudorientale.</span><span class="sxs-lookup"><span data-stu-id="c023d-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="c023d-232">Aggiungere un endpoint di gestione traffico per app Asia hello</span><span class="sxs-lookup"><span data-stu-id="c023d-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="c023d-233">Utilizzare [creare endpoint di gestione traffico di rete az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un toohello endpoint secondo profilo di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="c023d-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="c023d-234">Aggiungere App tooweb identificatore di area</span><span class="sxs-lookup"><span data-stu-id="c023d-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="c023d-235">Utilizzare [az appservice web configurazione appsettings aggiornare](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd una variabile di ambiente specifiche.</span><span class="sxs-lookup"><span data-stu-id="c023d-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="c023d-236">Il codice dell'applicazione usa già questa impostazione.</span><span class="sxs-lookup"><span data-stu-id="c023d-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="c023d-237">Vedere `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="c023d-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="c023d-238">Operazione completata</span><span class="sxs-lookup"><span data-stu-id="c023d-238">Complete!</span></span>

<span data-ttu-id="c023d-239">A questo punto, provare a tooaccess hello URL del profilo di Traffic Manager da parte dei browser in aree geografiche diverse.</span><span class="sxs-lookup"><span data-stu-id="c023d-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="c023d-240">I browser client situati in Europa dovrebbero mostrare "ASP.NET Europa occidentale", mentre quelli in Asia dovrebbero mostrare "ASP.NET Asia sud-orientale".</span><span class="sxs-lookup"><span data-stu-id="c023d-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="c023d-241">Altre risorse</span><span class="sxs-lookup"><span data-stu-id="c023d-241">More resources</span></span>
