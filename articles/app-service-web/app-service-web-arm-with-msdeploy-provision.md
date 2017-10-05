---
title: Distribuire un'app Web usando MSDeploy con il nome host personalizzato e il certificato SSL
description: Usare un modello di Gestione risorse di Azure per distribuire un'app Web usando MSDeploy e configurando il nome host personalizzato e un certificato SSL
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="1cf48-103">Distribuire un'app Web con MSDeploy, il nome host personalizzato e il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="1cf48-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="1cf48-104">Questa guida illustra la creazione di una distribuzione end-to-end per un'app Web di Azure, usando MSDeploy e aggiungendo un nome host personalizzato e un certificato SSL al modello di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf48-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="1cf48-105">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1cf48-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="1cf48-106">Creare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="1cf48-106">Create Sample Application</span></span>
<span data-ttu-id="1cf48-107">Si distribuirà un'applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1cf48-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="1cf48-108">Il primo passaggio prevede la creazione di una semplice applicazione Web. Se invece si sceglie di usarne una esistente, è possibile saltare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="1cf48-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="1cf48-109">Aprire Visual Studio 2015 e scegliere File > Nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="1cf48-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="1cf48-110">Nella finestra di dialogo visualizzata scegliere Web > Applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1cf48-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="1cf48-111">In Modelli scegliere Web e quindi il modello MVC.</span><span class="sxs-lookup"><span data-stu-id="1cf48-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="1cf48-112">Impostare *Change authentication type* (Cambia tipo di autenticazione) su *Nessuna autenticazione*.</span><span class="sxs-lookup"><span data-stu-id="1cf48-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="1cf48-113">In questo modo l'applicazione di esempio sarà il più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="1cf48-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="1cf48-114">A questo punto si avrà un'app Web ASP.Net di base da usare durante il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="1cf48-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="1cf48-115">Creare il pacchetto MSDeploy</span><span class="sxs-lookup"><span data-stu-id="1cf48-115">Create MSDeploy package</span></span>
<span data-ttu-id="1cf48-116">Il prossimo passaggio prevede la creazione del pacchetto per distribuire l'app Web in Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf48-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="1cf48-117">A questo scopo, salvare il progetto e quindi eseguire quanto segue dalla riga di comando:</span><span class="sxs-lookup"><span data-stu-id="1cf48-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="1cf48-118">Verrà creato un pacchetto compresso nella cartella PackageLocation.</span><span class="sxs-lookup"><span data-stu-id="1cf48-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="1cf48-119">L'applicazione ora è pronta per la distribuzione che è possibile eseguire compilando un modello di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf48-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="1cf48-120">Creare il modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1cf48-120">Create ARM Template</span></span>
<span data-ttu-id="1cf48-121">Iniziare con un modello di Gestione risorse di Azure di base che creerà un'applicazione Web e un piano di hosting. Si noti che i parametri e le variabili non vengono visualizzati per brevità.</span><span class="sxs-lookup"><span data-stu-id="1cf48-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

<span data-ttu-id="1cf48-122">Sarà quindi necessario modificare la risorsa app Web per poter accettare una risorsa MSDeploy annidata.</span><span class="sxs-lookup"><span data-stu-id="1cf48-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="1cf48-123">Questo consentirà di fare riferimento al pacchetto creato in precedenza e di indicare a Gestione risorse di Azure di usare MSDeploy per distribuire il pacchetto nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf48-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="1cf48-124">Il codice seguente mostra la risorsa Microsoft.Web/sites con la risorsa MSDeploy annidata:</span><span class="sxs-lookup"><span data-stu-id="1cf48-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

<span data-ttu-id="1cf48-125">Si noterà ora che la risorsa MSDeploy include una proprietà **packageUri** definita come segue:</span><span class="sxs-lookup"><span data-stu-id="1cf48-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="1cf48-126">Questo **packageUri** include l'URI dell'account di archiviazione che punta all'account di archiviazione in cui si caricherà il file zip del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1cf48-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="1cf48-127">Gestione risorse di Azure userà le [firme di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) per effettuare il pull del pacchetto in locale verso il basso dall'account di archiviazione quando si distribuisce il modello.</span><span class="sxs-lookup"><span data-stu-id="1cf48-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="1cf48-128">Questo processo verrà automatizzato con uno script PowerShell che caricherà il pacchetto e chiamerà l'API Gestione di Azure per creare le chiavi necessarie e passarle nel modello come parametri (*_artifactsLocation* e *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="1cf48-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="1cf48-129">Sarà necessario definire i parametri per la cartella e il nome file in cui il pacchetto viene caricato nel contenitore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1cf48-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="1cf48-130">Ora è necessario aggiungere un'altra risorsa annidata per configurare le associazioni nome host per sfruttare un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="1cf48-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="1cf48-131">Sarà prima di tutto necessario assicurarsi di essere proprietari del nome host e configurarlo in modo che Azure ne verifichi il proprietario. Vedere [Configurare un nome di dominio personalizzato nel servizio app di Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="1cf48-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="1cf48-132">A questo punto è possibile aggiungere il codice seguente al modello nella sezione della risorsa Microsoft.Web/sites:</span><span class="sxs-lookup"><span data-stu-id="1cf48-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

<span data-ttu-id="1cf48-133">Infine è necessario aggiungere un'altra risorsa di primo livello, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="1cf48-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="1cf48-134">Questa risorsa conterrà il certificato SSL ed esisterà nello stesso livello dell'app Web e del piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="1cf48-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

<span data-ttu-id="1cf48-135">Per configurare questa risorsa, sarà necessario un certificato SSL valido.</span><span class="sxs-lookup"><span data-stu-id="1cf48-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="1cf48-136">Una volta disponibile il certificato valido, è necessario estrarre i byte pfx come stringa base64.</span><span class="sxs-lookup"><span data-stu-id="1cf48-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="1cf48-137">Per estrarli, è possibile usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="1cf48-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="1cf48-138">È quindi possibile passarli come parametro al modello di distribuzione di Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf48-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="1cf48-139">A questo punto il modello di Gestione risorse di Azure è pronto.</span><span class="sxs-lookup"><span data-stu-id="1cf48-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="1cf48-140">Modello di distribuzione</span><span class="sxs-lookup"><span data-stu-id="1cf48-140">Deploy Template</span></span>
<span data-ttu-id="1cf48-141">I passaggi finali consentono di realizzare una distribuzione end-to-end completa.</span><span class="sxs-lookup"><span data-stu-id="1cf48-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="1cf48-142">Per semplificare la distribuzione, è possibile sfruttare lo script PowerShell **Deploy-AzureResourceGroup.ps1** aggiunto quando si crea un progetto gruppo di risorse di Azure in Visual Studio per rendere più facile il caricamento degli elementi necessari nel modello.</span><span class="sxs-lookup"><span data-stu-id="1cf48-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="1cf48-143">È necessario creare in anticipo l'account di archiviazione che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="1cf48-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="1cf48-144">Per questo esempio, è stato creato un account di archiviazione condiviso per il file package.zip da caricare.</span><span class="sxs-lookup"><span data-stu-id="1cf48-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="1cf48-145">Lo script userà AzCopy per caricare il pacchetto nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1cf48-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="1cf48-146">Passando il percorso della cartella degli elementi, lo script caricherà automaticamente tutti i file di tale directory nel contenitore di archiviazione denominato.</span><span class="sxs-lookup"><span data-stu-id="1cf48-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="1cf48-147">Dopo avere chiamato Deploy-AzureResourceGroup.ps1, è necessario aggiornare le associazioni SSL per eseguire il mapping del nome host personalizzato al certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="1cf48-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="1cf48-148">Lo script PowerShell seguente illustra la distribuzione completa chiamando Deploy-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="1cf48-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="1cf48-149">A questo punto l'applicazione è stata distribuita ed è possibile accedervi tramite https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="1cf48-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

