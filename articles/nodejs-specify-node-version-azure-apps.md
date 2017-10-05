---
title: Specifica di una versione di Node.js
description: Informazioni su come specificare la versione di Node. js usata da Siti Web e Servizi cloud di Azure
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
ms.openlocfilehash: 89627e6a877c9f65a5216c55f58f1c707ea25d44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a><span data-ttu-id="2c1a8-103">Specifica di una versione di Node.js in un'applicazione Azure</span><span class="sxs-lookup"><span data-stu-id="2c1a8-103">Specifying a Node.js version in an Azure application</span></span>
<span data-ttu-id="2c1a8-104">Quando si ospita un'applicazione Node.js, può essere necessario assicurarsi che utilizzi una versione specifica di Node.js.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-104">When hosting a Node.js application, you may want to ensure that your application uses a specific version of Node.js.</span></span> <span data-ttu-id="2c1a8-105">Questa operazione può essere eseguita in vari modi per le applicazioni ospitate in Azure.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-105">There are several ways to accomplish this for applications hosted on Azure.</span></span>

## <a name="default-versions"></a><span data-ttu-id="2c1a8-106">Versioni predefinite</span><span class="sxs-lookup"><span data-stu-id="2c1a8-106">Default versions</span></span>
<span data-ttu-id="2c1a8-107">Le versioni di Node.js fornite da Azure vengono aggiornate costantemente.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-107">The Node.js versions provided by Azure are constantly updated.</span></span> <span data-ttu-id="2c1a8-108">Se non diversamente specificato, verrà usata la versione predefinita specificata nella variabile di ambiente `WEBSITE_NODE_DEFAULT_VERSION` .</span><span class="sxs-lookup"><span data-stu-id="2c1a8-108">Unless otherwise specified, the default version that is specified in the `WEBSITE_NODE_DEFAULT_VERSION` environment variable will be used.</span></span> <span data-ttu-id="2c1a8-109">Per eseguire l'override di questo valore predefinito, seguire i passaggi disponibili nelle sezioni seguenti di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-109">To override this default value, follow the steps in following sections of this article</span></span>

> [!NOTE]
> <span data-ttu-id="2c1a8-110">Se l'applicazione è ospitata in un servizio cloud di Azure (ruolo di lavoro o Web) ed è la prima volta che si distribuisce l'applicazione, Azure tenterà di usare la stessa versione di Node.js installata nell'ambiente di sviluppo, se questa corrisponde a une delle versioni predefinite disponibili.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-110">If you are hosting your application in an Azure Cloud Service (web or worker role,) and it is the first time you have deployed the application, Azure will attempt to use the same version of Node.js as you have installed on your development environment if it matches one of the default versions available on Azure.</span></span>
>
>

## <a name="versioning-with-packagejson"></a><span data-ttu-id="2c1a8-111">Controllo delle versioni con package.json</span><span class="sxs-lookup"><span data-stu-id="2c1a8-111">Versioning with package.json</span></span>
<span data-ttu-id="2c1a8-112">È possibile specificare la versione di Node.js da usare aggiungendo il codice seguente al file **package.json** :</span><span class="sxs-lookup"><span data-stu-id="2c1a8-112">You can specify the version of Node.js to be used by adding the following to your **package.json** file:</span></span>

    "engines":{"node":version}

<span data-ttu-id="2c1a8-113">Dove *version* è lo specifico numero di versione da usare.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-113">Where *version* is the specific version number to use.</span></span> <span data-ttu-id="2c1a8-114">È possibile specificare condizioni più complesse per la versione, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2c1a8-114">You can specify more complex conditions for version, such as:</span></span>

    "engines":{"node": "0.6.22 || 0.8.x"}

<span data-ttu-id="2c1a8-115">Poiché la 0.6.22 non è una delle versioni disponibili nell'ambiente host, verrà utilizzata la versione più recente della serie 0.8 disponibile, ovvero la 0.8.4.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-115">Since 0.6.22 is not one of the versions available in the hosting environment, the highest version of the 0.8 series that is available will be used instead - 0.8.4.</span></span>

## <a name="versioning-websites-with-app-settings"></a><span data-ttu-id="2c1a8-116">Controllo delle versioni di Siti Web con Impostazioni app</span><span class="sxs-lookup"><span data-stu-id="2c1a8-116">Versioning Websites with App Settings</span></span>
<span data-ttu-id="2c1a8-117">Se si ospita l'applicazione in un sito Web, è possibile impostare la variabile di ambiente **WEBSITE_NODE_DEFAULT_VERSION** sulla versione desiderata.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-117">If you are hosting the application in a Website, you can set the environment variable **WEBSITE_NODE_DEFAULT_VERSION** to the desired version.</span></span>

## <a name="versioning-cloud-services-with-powershell"></a><span data-ttu-id="2c1a8-118">Controllo delle versioni dei servizi cloud con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c1a8-118">Versioning Cloud Services with PowerShell</span></span>
<span data-ttu-id="2c1a8-119">Se l'applicazione è ospitata in un servizio cloud e si sta distribuendo l'applicazione utilizzando Azure PowerShell, è possibile sostituire la versione predefinita di Node.js utilizzando il cmdlet di PowerShell **Set-AzureServiceProjectRole** .</span><span class="sxs-lookup"><span data-stu-id="2c1a8-119">If you are hosting the application in a Cloud Service, and are deploying the application using Azure PowerShell, you can override the default Node.js version by using the **Set-AzureServiceProjectRole** PowerShell cmdlet.</span></span> <span data-ttu-id="2c1a8-120">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2c1a8-120">For example:</span></span>

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

<span data-ttu-id="2c1a8-121">Si noti che i parametri nell'istruzione precedente fanno la distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-121">Note the parameters in the above statement are case-sensitive.</span></span>  <span data-ttu-id="2c1a8-122">È possibile verificare di aver selezionato la versione corretta di Node.js controllando la proprietà **engines** nel **package.json** del ruolo.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-122">You can verify the correct version of Node.js has been selected by checking the **engines** property in your role's **package.json**.</span></span>

<span data-ttu-id="2c1a8-123">È inoltre possibile usare **Get-AzureServiceProjectRoleRuntime** per recuperare un elenco delle versioni di Node.js disponibili per le applicazioni ospitate come servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-123">You can also use the **Get-AzureServiceProjectRoleRuntime** to retrieve a list of Node.js versions available for applications hosted as a Cloud Service.</span></span>  <span data-ttu-id="2c1a8-124">Verificare sempre che la versione di Node. js dipenda da se il progetto è incluso nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-124">Always verify the version of Node.js your project depends on is in this list.</span></span>

## <a name="using-a-custom-version-with-azure-websites"></a><span data-ttu-id="2c1a8-125">Uso di una versione personalizzata con i siti Web di Azure</span><span class="sxs-lookup"><span data-stu-id="2c1a8-125">Using a custom version with Azure Websites</span></span>
<span data-ttu-id="2c1a8-126">Anche se in Azure sono disponibili svariate versioni predefinite di Node.js, potrebbe essere necessario utilizzare una versione non disponibile per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-126">While Azure provides several default versions of Node.js, you may want to use a version that is not provided by default.</span></span> <span data-ttu-id="2c1a8-127">Se l'applicazione è ospitata come sito Web di Azure, è possibile eseguire l'operazione usando il file **iisnode.yml** .</span><span class="sxs-lookup"><span data-stu-id="2c1a8-127">If your application is hosted as an Azure Website, you can accomplish this by using the **iisnode.yml** file.</span></span> <span data-ttu-id="2c1a8-128">I passaggi successivi illustrano la procedura per l'uso di una versione personalizzata di Node.Js con un sito Web di Azure:</span><span class="sxs-lookup"><span data-stu-id="2c1a8-128">The following steps walk through the process of using a custom version of Node.Js with an Azure Website:</span></span>

1. <span data-ttu-id="2c1a8-129">Creare una nuova directory e quindi creare un file **server.js** al suo interno.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-129">Create a new directory, and then create a **server.js** file within the directory.</span></span> <span data-ttu-id="2c1a8-130">Il contenuto del file deve essere il seguente **server.js** :</span><span class="sxs-lookup"><span data-stu-id="2c1a8-130">The **server.js** file should contain the following:</span></span>

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    <span data-ttu-id="2c1a8-131">Questo consentirà di visualizzare la versione di Node.js utilizzata durante l'esplorazione del sito Web.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-131">This will display the Node.js version being used when you browse the website.</span></span>
2. <span data-ttu-id="2c1a8-132">Creare un nuovo sito Web e prendere nota del nome del sito.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-132">Create a new Website and note the name of the site.</span></span> <span data-ttu-id="2c1a8-133">Nel comando seguente, ad esempio, gli [strumenti da riga di comando di Azure] vengono utilizzati per creare un nuovo sito Web di Azure denominato **mywebsite**e quindi per abilitare un repository Git per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-133">For example, the following uses the [Azure Command-line tools] to create a new Azure Website named **mywebsite**, and then enable a Git repository for the website.</span></span>

        azure site create mywebsite --git
3. <span data-ttu-id="2c1a8-134">Creare una nuova directory denominata **bin** come figlio della directory che contiene il file **server.js**.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-134">Create a new directory named **bin** as a child of the directory containing the **server.js** file.</span></span>
4. <span data-ttu-id="2c1a8-135">Scaricare la specifica versione di **node.exe** (per Windows) che si desidera utilizzare con l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-135">Download the specific version of **node.exe** (the Windows version) that you wish to use with your application.</span></span> <span data-ttu-id="2c1a8-136">Nell'esempio seguente viene usato **curl** per scaricare la versione 0.8.1:</span><span class="sxs-lookup"><span data-stu-id="2c1a8-136">For example, the following uses **curl** to download version 0.8.1:</span></span>

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    <span data-ttu-id="2c1a8-137">Salvare il file **node.exe** nella cartella **bin** creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-137">Save the **node.exe** file into the **bin** folder created previously.</span></span>
5. <span data-ttu-id="2c1a8-138">Creare un file **iisnode.yml** nella stessa directory del file **server.js** e quindi aggiungere il contenuto seguente al file **iisnode.yml**:</span><span class="sxs-lookup"><span data-stu-id="2c1a8-138">Create an **iisnode.yml** file in the same directory as the **server.js** file, and then add the following content to the **iisnode.yml** file:</span></span>

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    <span data-ttu-id="2c1a8-139">Questo percorso corrisponde alla posizione in cui sarà situato il file **node.exe** all'interno del progetto dopo la pubblicazione dell'applicazione nel sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-139">This path is where the **node.exe** file within your project will be located once you have published your application to the Azure Website.</span></span>
6. <span data-ttu-id="2c1a8-140">Pubblicare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-140">Publish your application.</span></span> <span data-ttu-id="2c1a8-141">Ad esempio, poiché in precedenza è stato creato un nuovo sito Web con il parametro --git, i comandi seguenti consentiranno di aggiungere i file dell'applicazione al repository Git locale e quindi di effettuarne il push nel repository del sito Web:</span><span class="sxs-lookup"><span data-stu-id="2c1a8-141">For example, since I created a new website with the --git parameter earlier, the following commands will add the application files to my local Git repository, and then push them to the website repository:</span></span>

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    <span data-ttu-id="2c1a8-142">Dopo la pubblicazione dell'applicazione, aprire il sito Web in un browser.</span><span class="sxs-lookup"><span data-stu-id="2c1a8-142">After the application has published, open the website in a browser.</span></span> <span data-ttu-id="2c1a8-143">Dovrebbe essere visualizzato il messaggio "Hello from Azure running node version: v0.8.1".</span><span class="sxs-lookup"><span data-stu-id="2c1a8-143">You should see a message stating "Hello from Azure running node version: v0.8.1".</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c1a8-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c1a8-144">Next Steps</span></span>
<span data-ttu-id="2c1a8-145">Dopo avere appreso come specificare la versione di Node.js usata dall'applicazione, per altre informazioni vedere gli articoli che illustrano come [usare i moduli], [creare e distribuire un sito Web Node.js](app-service-web/app-service-web-get-started-nodejs.md) e [usare gli strumenti da riga di comando di Azure per Mac e Linux].</span><span class="sxs-lookup"><span data-stu-id="2c1a8-145">Now that you understand how to specify the version of Node.js used by your application, learn how to [work with modules], [build and deploy a Node.js Web Site](app-service-web/app-service-web-get-started-nodejs.md), and [How to use the Azure Command-Line Tools for Mac and Linux].</span></span>

<span data-ttu-id="2c1a8-146">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Node.js](https://azure.microsoft.com/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="2c1a8-146">For more information, see the [Node.js Developer Center](https://azure.microsoft.com/develop/nodejs/).</span></span>

<span data-ttu-id="2c1a8-147">[usare gli strumenti da riga di comando di Azure per Mac e Linux]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="2c1a8-147">[How to use the Azure Command-Line Tools for Mac and Linux]:cli-install-nodejs.md</span></span>
<span data-ttu-id="2c1a8-148">[strumenti da riga di comando di Azure]:cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="2c1a8-148">[Azure Command-line tools]:cli-install-nodejs.md</span></span>
<span data-ttu-id="2c1a8-149">[usare i moduli]: nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="2c1a8-149">[work with modules]: nodejs-use-node-modules-azure-apps.md</span></span>
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
