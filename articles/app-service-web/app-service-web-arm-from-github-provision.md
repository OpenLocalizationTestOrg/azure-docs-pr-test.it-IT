---
title: Distribuire un'app Web collegata a un repository GitHub | Documentazione Microsoft
description: Usare un modello di Gestione risorse di Azure per distribuire un'app Web che contiene un progetto da un repository GitHub.
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="974dd-103">Distribuire un'app Web collegata a un repository GitHub</span><span class="sxs-lookup"><span data-stu-id="974dd-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="974dd-104">In questo argomento si apprenderà come creare un modello di gestione risorse di Azure che consente di distribuire un'app Web collegata a un progetto in un repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="974dd-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="974dd-105">Verrà illustrato come definire le risorse da distribuire e i parametri specificati quando viene eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="974dd-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="974dd-106">È possibile usare questo modello per le proprie distribuzioni o personalizzarlo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="974dd-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="974dd-107">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="974dd-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="974dd-108">Per il modello completo, vedere [App Web collegata al modello GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="974dd-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="974dd-109">Elementi distribuiti</span><span class="sxs-lookup"><span data-stu-id="974dd-109">What you will deploy</span></span>
<span data-ttu-id="974dd-110">Con questo modello verrà distribuita un'app Web che contiene il codice da un progetto in GitHub.</span><span class="sxs-lookup"><span data-stu-id="974dd-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="974dd-111">Per eseguire automaticamente la distribuzione, fare clic sul pulsante seguente:</span><span class="sxs-lookup"><span data-stu-id="974dd-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="974dd-112">[![Distribuzione in Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="974dd-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="974dd-113">Parametri</span><span class="sxs-lookup"><span data-stu-id="974dd-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="974dd-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="974dd-114">repoURL</span></span>
<span data-ttu-id="974dd-115">L'URL del repository GitHub che contiene il progetto da distribuire.</span><span class="sxs-lookup"><span data-stu-id="974dd-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="974dd-116">Questo parametro contiene un valore predefinito, ma questo valore è destinato solo a illustrare come specificare l'URL del repository.</span><span class="sxs-lookup"><span data-stu-id="974dd-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="974dd-117">È possibile usare questo valore quando si esegue il test del modello, ma è possibile specificare l'URL del proprio repository quando si utilizza il modello.</span><span class="sxs-lookup"><span data-stu-id="974dd-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="974dd-118">ramo</span><span class="sxs-lookup"><span data-stu-id="974dd-118">branch</span></span>
<span data-ttu-id="974dd-119">Ramo dell'archivio da usare per la distribuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="974dd-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="974dd-120">Il valore predefinito è il database master, ma è possibile specificare il nome di un ramo nel repository da distribuire.</span><span class="sxs-lookup"><span data-stu-id="974dd-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="974dd-121">Risorse da distribuire</span><span class="sxs-lookup"><span data-stu-id="974dd-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="974dd-122">App Web</span><span class="sxs-lookup"><span data-stu-id="974dd-122">Web app</span></span>
<span data-ttu-id="974dd-123">Crea l'app Web collegata al progetto in GitHub.</span><span class="sxs-lookup"><span data-stu-id="974dd-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="974dd-124">Il nome dell'app Web viene specificato tramite il parametro **siteName** e il percorso dell'app Web tramite il parametro **siteLocation**.</span><span class="sxs-lookup"><span data-stu-id="974dd-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="974dd-125">Nell'elemento **dependsOn** il modello consente di definire l'app Web dipendente dal piano di hosting del servizio.</span><span class="sxs-lookup"><span data-stu-id="974dd-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="974dd-126">Dipendendo dal piano di hosting, l'app Web non viene creata prima del termine della creazione del piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="974dd-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="974dd-127">L'elemento **dependsOn** viene usato solo per specificare l'ordine di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="974dd-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="974dd-128">Se non si contrassegna l'app Web come dipendente dal piano di hosting, Gestione risorse di Azure tenterà di creare entrambe le risorse contemporaneamente. È possibile che si verifichi un errore se l'app Web viene creata prima del piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="974dd-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="974dd-129">L'app Web dispone anche di una risorsa figlio che viene definita nella sezione delle **risorse** riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="974dd-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="974dd-130">Questa risorsa figlio consente di definire il controllo del codice sorgente per il progetto distribuito con l'app Web.</span><span class="sxs-lookup"><span data-stu-id="974dd-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="974dd-131">In questo modello, il controllo del codice sorgente è collegato a un determinato repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="974dd-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="974dd-132">Il repository GitHub viene definito con il codice **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** È possibile impostare come hardcoded l'URL del repository, se si desidera creare un modello che distribuisce ripetutamente un progetto singolo richiedendo il numero minimo di parametri.</span><span class="sxs-lookup"><span data-stu-id="974dd-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="974dd-133">Anziché impostare come hardcoded l'URL del repository, è possibile aggiungere un parametro per l'URL del repository e usare tale valore per la proprietà **RepoUrl** .</span><span class="sxs-lookup"><span data-stu-id="974dd-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="974dd-134">Comandi per eseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="974dd-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="974dd-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="974dd-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="974dd-136">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="974dd-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="974dd-137">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="974dd-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="974dd-138">Per il contenuto del file JSON dei parametri, vedere [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="974dd-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

