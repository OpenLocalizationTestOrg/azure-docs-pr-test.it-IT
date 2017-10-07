---
title: "aaaDeploy un'app web che è collegato il repository di GitHub tooa | Documenti Microsoft"
description: Utilizzare un toodeploy modello di gestione risorse di Azure un'app web che contiene un progetto da un repository di GitHub.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="7cc4f-103">Distribuire un repository di GitHub tooa collegato app web</span><span class="sxs-lookup"><span data-stu-id="7cc4f-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="7cc4f-104">In questo argomento si apprenderà come toocreate un modello di gestione risorse di Azure che consente di distribuire un'app web che è collegato tooa progetto in un repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="7cc4f-105">Si apprenderà come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="7cc4f-106">È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="7cc4f-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7cc4f-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="7cc4f-108">Per il modello di hello completo, vedere [Web App collegato tooGitHub modello](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="7cc4f-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="7cc4f-109">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="7cc4f-109">What you will deploy</span></span>
<span data-ttu-id="7cc4f-110">Con questo modello verrà distribuito un'app web che contiene il codice hello da un progetto in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="7cc4f-111">toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:</span><span class="sxs-lookup"><span data-stu-id="7cc4f-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="7cc4f-112">[![Distribuire tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7cc4f-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="7cc4f-113">parameters</span><span class="sxs-lookup"><span data-stu-id="7cc4f-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="7cc4f-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="7cc4f-114">repoURL</span></span>
<span data-ttu-id="7cc4f-115">Hello URL per il repository di GitHub che contiene toodeploy progetto hello.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="7cc4f-116">Questo parametro contiene un valore predefinito, ma questo valore è solo tooshow previsto è come tooprovide hello URL per il repository.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="7cc4f-117">È possibile utilizzare questo valore quando test modello hello ma si desidererà tooprovide hello URL proprio repository quando si utilizza il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="7cc4f-118">ramo</span><span class="sxs-lookup"><span data-stu-id="7cc4f-118">branch</span></span>
<span data-ttu-id="7cc4f-119">ramo Hello di hello repository toouse quando si distribuisce un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="7cc4f-120">valore predefinito di Hello è il database master, ma è possibile specificare il nome di hello di qualsiasi ramo nel repository di hello che si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="7cc4f-121">Risorse toodeploy</span><span class="sxs-lookup"><span data-stu-id="7cc4f-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="7cc4f-122">App Web</span><span class="sxs-lookup"><span data-stu-id="7cc4f-122">Web app</span></span>
<span data-ttu-id="7cc4f-123">Crea app web hello del progetto toohello collegato in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="7cc4f-124">Specificare il nome di hello dell'app web hello tramite hello **siteName** parametro e la posizione di hello dell'app web hello tramite hello **siteLocation** parametro.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="7cc4f-125">In hello **dependsOn** elemento modello hello definisce hello web app come dipende dal servizio hello piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="7cc4f-126">Poiché è dipende dal piano di hosting hello, hello web app non viene creato fino a quando non hello piano di hosting è stata completata la creazione.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="7cc4f-127">Hello **dependsOn** elemento è utilizzato toospecify solo ordine di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="7cc4f-128">Se non si contrassegna hello web app come dipende dal piano di hosting hello, Azure Resource Manager tenterà toocreate entrambe le risorse in hello stesso tempo e potrebbe essere visualizzato un errore se l'app web hello venga creato prima di hello piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="7cc4f-129">app web Hello dispone anche di una risorsa figlio che è definita in **risorse** sezione riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="7cc4f-130">Risorsa figlio che definisce il codice sorgente per il progetto hello distribuito con hello web app.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="7cc4f-131">In questo modello di controllo del codice sorgente hello è collegato tooa particolare repository di GitHub.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="7cc4f-132">repository di GitHub Hello è definito con codice hello **"URL repository": "https://github.com/davidebbo-test/Mvc52Application.git"** è possibile codificare hello URL del repository quando si desidera toocreate un modello che consente di distribuire più volte un singolo progetto richiedere numero minimo di hello di parametri.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="7cc4f-133">Anziché a livello di codice hello URL del repository, è possibile aggiungere un parametro per l'URL del repository hello e utilizzare tale valore per hello **URL repository** proprietà.</span><span class="sxs-lookup"><span data-stu-id="7cc4f-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="7cc4f-134">Comandi toorun distribuzione</span><span class="sxs-lookup"><span data-stu-id="7cc4f-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="7cc4f-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7cc4f-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="7cc4f-136">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7cc4f-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="7cc4f-137">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="7cc4f-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="7cc4f-138">Per il contenuto del file JSON di hello parametri, vedere [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="7cc4f-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

