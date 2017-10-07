---
title: aaaSpecifying una versione di Node. js
description: Informazioni su come toospecify hello versione di Node. js utilizzato da siti Web di Azure e servizi Cloud
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="b1c0f-103">Specifica di una versione di Node.js in un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="b1c0f-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="b1c0f-104">Quando si ospita un'applicazione Node.js, è consigliabile che l'applicazione usa una versione specifica di Node.js tooensure.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-104">When hosting a Node.js application, you may want tooensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="b1c0f-105">Esistono diversi modi tooaccomplish ciò per le applicazioni ospitate in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-105">There are several ways tooaccomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="b1c0f-106">Versioni predefinite</span><span class="sxs-lookup"><span data-stu-id="b1c0f-106">Default versions</span></span>
<span data-ttu-id="b1c0f-107">versioni di Node.js Hello fornite da Azure vengono aggiornate continuamente.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-107">hello Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="b1c0f-108">Se non diversamente specificato, hello versione predefinita specificata nella hello `WEBSITE_NODE_DEFAULT_VERSION` variabile di ambiente da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-108">Unless otherwise specified, hello default version that is specified in hello `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="b1c0f-109">toooverride il valore predefinito, seguire la procedura seguente hello nelle sezioni seguenti di questo articolo</span><span class="sxs-lookup"><span data-stu-id="b1c0f-109">toooverride this default value, follow hello steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="b1c0f-110">Se si ospitano l'applicazione in un servizio Cloud di Azure (ruolo web o di lavoro) ed è hello prima volta che è stato distribuito l'applicazione hello, Azure tenterà toouse hello stessa versione di Node. js, come è stato installato l'ambiente di sviluppo se si corrisponde a una delle versioni di hello predefinite disponibili in Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is hello first time you have deployed hello application, Azure will attempt toouse hello same version of Node.js as you have installed on your development environment if it matches one of hello default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="b1c0f-111">Controllo delle versioni con package.json</span><span class="sxs-lookup"><span data-stu-id="b1c0f-111">Versioning with package.json</span></span>
<span data-ttu-id="b1c0f-112">È possibile specificare una versione di hello di Node.js toobe utilizzata aggiungendo hello seguente tooyour **package. JSON** file:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-112">You can specify hello version of Node.js toobe used by adding hello following tooyour **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="b1c0f-113">Dove *versione* è toouse numero versione specifica di hello.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-113">Where *version* is hello specific version number toouse.</span></span> <span data-ttu-id="b1c0f-114">È possibile specificare condizioni più complesse per la versione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="b1c0f-115">Poiché 0.6.22 non è una delle versioni di hello disponibili nell'ambiente di hosting hello, hello versione più recente di hello 0,8 serie disponibile sarà utilizzato - 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-115">Since 0.6.22 is not one of hello versions available in hello hosting environment, hello highest version of hello 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="b1c0f-116">Controllo delle versioni di Siti Web con Impostazioni app</span><span class="sxs-lookup"><span data-stu-id="b1c0f-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="b1c0f-117">Se si ospita un'applicazione hello in un sito Web, è possibile impostare la variabile di ambiente hello **WEBSITE_NODE_DEFAULT_VERSION** versione desiderata di toohello.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-117">If you are hosting hello application in a Website, you can set hello environment variable **WEBSITE_NODE_DEFAULT_VERSION** toohello desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="b1c0f-118">Controllo delle versioni dei servizi cloud con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1c0f-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="b1c0f-119">Se si ospita un'applicazione hello in un servizio Cloud e si distribuisce un'applicazione hello con Azure PowerShell, è possibile eseguire l'override di versione di Node. js hello predefinita utilizzando hello **Set AzureServiceProjectRole** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-119">If you are hosting hello application in a Cloud Service, and are deploying hello application using Azure PowerShell, you can override hello default Node.js version by using hello **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="b1c0f-120">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="b1c0f-121">Parametri di hello nota in hello sopra istruzione maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-121">Note hello parameters in hello above statement are case-sensitive.</span></span>  <span data-ttu-id="b1c0f-122">È possibile verificare versione corretta di hello di Node.js è stata selezionata per il controllo hello **motori** proprietà del ruolo **package. JSON**.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-122">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="b1c0f-123">È inoltre possibile utilizzare hello **Get AzureServiceProjectRoleRuntime** tooretrieve un elenco delle versioni di Node.js disponibili per le applicazioni ospitate come un servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-123">You can also use hello **Get-AzureServiceProjectRoleRuntime** tooretrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="b1c0f-124">Verificare sempre la versione di hello di Node.js dipende il progetto in questo elenco.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-124">Always verify hello version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="b1c0f-125">Uso di una versione personalizzata con i siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="b1c0f-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="b1c0f-126">Sebbene Azure fornisce le diverse versioni predefinite di Node.js, è consigliabile toouse una versione che non viene fornita per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-126">While Azure provides several default versions of Node.js, you may want toouse a version that is not provided by default.</span></span> <span data-ttu-id="b1c0f-127">Se l'applicazione è ospitato come un sito Web di Azure, è possibile effettuare questa operazione utilizzando hello **iisnode.yml** file.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-127">If your application is hosted as an Azure Website, you can accomplish this by using hello **iisnode.yml** file.</span></span> <span data-ttu-id="b1c0f-128">Hello passaggi seguenti descrivono il processo di hello di utilizzo di una versione personalizzata di Node. js con un sito Web di Azure:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-128">hello following steps walk through hello process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="b1c0f-129">Creare una nuova directory e quindi creare un **server.js** file all'interno di directory hello.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-129">Create a new directory, and then create a **server.js** file within hello directory.</span></span> <span data-ttu-id="b1c0f-130">Hello **server.js** file deve contenere i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-130">hello **server.js** file should contain hello following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="b1c0f-131">Verrà visualizzata una versione di Node. js hello utilizzata durante l'esplorazione del sito Web hello.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-131">This will display hello Node.js version being used when you browse hello website.</span></span>
2. <span data-ttu-id="b1c0f-132">Creare un nuovo sito Web e il nome del sito hello hello della nota.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-132">Create a new Website and note hello name of hello site.</span></span> <span data-ttu-id="b1c0f-133">Ad esempio, il seguente hello Usa hello [gli strumenti da riga di comando di Azure] toocreate un nuovo sito Web Azure denominato **mywebsite**e quindi abilitare un repository Git per il sito Web di hello.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-133">For example, hello following uses hello [Azure Command-line tools] toocreate a new Azure Website named **mywebsite**, and then enable a Git repository for hello website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="b1c0f-134">Creare una nuova directory denominata **bin** come elemento figlio della directory hello contenente hello **server.js** file.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-134">Create a new directory named **bin** as a child of hello directory containing hello **server.js** file.</span></span>
4. <span data-ttu-id="b1c0f-135">Scaricare una versione specifica di hello di **node.exe** (versione di Windows hello) che si desidera toouse con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-135">Download hello specific version of **node.exe** (hello Windows version) that you wish toouse with your application.</span></span> <span data-ttu-id="b1c0f-136">Ad esempio, hello seguenti utilizza **curl** versione toodownload 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-136">For example, hello following uses **curl** toodownload version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="b1c0f-137">Salvare hello **node.exe** file hello **bin** cartella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-137">Save hello **node.exe** file into hello **bin** folder created previously.</span></span>
5. <span data-ttu-id="b1c0f-138">Creare un **iisnode.yml** file hello stessa directory come hello **server.js** file e quindi aggiungere hello seguente toohello contenuto **iisnode.yml** file:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-138">Create an **iisnode.yml** file in hello same directory as hello **server.js** file, and then add hello following content toohello **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="b1c0f-139">Questo percorso è dove hello **node.exe** file all'interno del progetto sarà posizionato dopo aver pubblicato il toohello applicazione sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-139">This path is where hello **node.exe** file within your project will be located once you have published your application toohello Azure Website.</span></span>
6. <span data-ttu-id="b1c0f-140">Pubblicare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-140">Publish your application.</span></span> <span data-ttu-id="b1c0f-141">Ad esempio, poiché è stata creata in precedenza un nuovo sito Web con il parametro - git hello, hello comandi riportati di seguito verranno aggiungere hello applicazione file toomy repository Git locale e quindi inviarli repository del sito Web toohello:</span><span class="sxs-lookup"><span data-stu-id="b1c0f-141">For example, since I created a new website with hello --git parameter earlier, hello following commands will add hello application files toomy local Git repository, and then push them toohello website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="b1c0f-142">Dopo aver pubblicato l'applicazione hello, Apri sito Web di hello in un browser.</span><span class="sxs-lookup"><span data-stu-id="b1c0f-142">After hello application has published, open hello website in a browser.</span></span> <span data-ttu-id="b1c0f-143">Dovrebbe essere visualizzato il messaggio "Hello from Azure running node version: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="b1c0f-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1c0f-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1c0f-144">Next Steps</span></span>
<span data-ttu-id="b1c0f-145">Dopo aver compreso come versione di hello toospecify di Node.js utilizzati dall'applicazione, consultare come troppo[funzionano con i moduli], [compilare e distribuire un sito Web Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [come toouse hello Azure Strumenti da riga di comando per Mac e Linux].</span><span class="sxs-lookup"><span data-stu-id="b1c0f-145">Now that you understand how toospecify hello version of Node.js used by your application, learn how too[work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How toouse hello Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="b1c0f-146">Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b1c0f-146">For more information, see hello [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

[come toouse hello Azure Strumenti da riga di comando per Mac e Linux]:cli-install-nodejs.md
[gli strumenti da riga di comando di Azure]:cli-install-nodejs.md
[funzionano con i moduli]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
