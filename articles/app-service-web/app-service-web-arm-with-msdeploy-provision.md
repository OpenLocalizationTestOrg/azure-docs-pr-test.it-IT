---
title: aaaDeploy un'app web utilizzando MSDeploy con certificato ssl e nome host
description: Usare un'app web con MSDeploy e la configurazione di nome host personalizzato e un certificato SSL di un toodeploy modello di gestione risorse di Azure
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
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="4a6d5-103">Distribuire un'app Web con MSDeploy, il nome host personalizzato e il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="4a6d5-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="4a6d5-104">Questa guida vengono illustrati la creazione di una distribuzione end-to-end per un'App Web di Azure, sfruttando MSDeploy nonché di aggiunta di un nome host personalizzato e un modello ARM toohello certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="4a6d5-105">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4a6d5-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="4a6d5-106">Creare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="4a6d5-106">Create Sample Application</span></span>
<span data-ttu-id="4a6d5-107">Si distribuirà un'applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="4a6d5-108">toocreate una semplice applicazione web, è innanzitutto Hello (o è possibile scegliere toouse uno esistente, nel qual caso è possibile ignorare questo passaggio).</span><span class="sxs-lookup"><span data-stu-id="4a6d5-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="4a6d5-109">Aprire Visual Studio 2015 e scegliere File > Nuovo progetto.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="4a6d5-110">Nella finestra di dialogo hello visualizzata scegliere Web > applicazione Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="4a6d5-111">Nel riquadro Modelli scegliere Web e scegliere il modello MVC hello.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="4a6d5-112">Selezionare *Cambia tipo di autenticazione* troppo*Nessuna autenticazione*.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="4a6d5-113">Si tratta semplicemente toomake hello applicazione di esempio più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="4a6d5-114">A questo punto si avrà una base toouse pronto di ASP.Net web app come parte del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="4a6d5-115">Creare il pacchetto MSDeploy</span><span class="sxs-lookup"><span data-stu-id="4a6d5-115">Create MSDeploy package</span></span>
<span data-ttu-id="4a6d5-116">Passaggio successivo è toocreate hello pacchetto toodeploy hello web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="4a6d5-117">toodo, salvare il progetto e quindi eseguire l'esempio hello dalla riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="4a6d5-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="4a6d5-118">Verrà creato un pacchetto compresso nella cartella PackageLocation hello.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="4a6d5-119">Hello applicazione è ora pronto toobe distribuito, che è possibile ora creare un toodo modello di gestione risorse di Azure che.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="4a6d5-120">Creare il modello di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="4a6d5-120">Create ARM Template</span></span>
<span data-ttu-id="4a6d5-121">Iniziare con un modello di Gestione risorse di Azure di base che creerà un'applicazione Web e un piano di hosting. Si noti che i parametri e le variabili non vengono visualizzati per brevità.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="4a6d5-122">Successivamente, sarà necessario toomodify hello web app risorsa tootake una risorsa di MSDeploy annidata.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="4a6d5-123">Verrà consentire si tooreference hello pacchetto creato in precedenza e indicare a Gestione risorse di Azure toouse MSDeploy toodeploy hello pacchetto toohello WebApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="4a6d5-124">Hello seguente risorsa Microsoft.Web/sites hello risorsa di MSDeploy hello annidato:</span><span class="sxs-lookup"><span data-stu-id="4a6d5-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="4a6d5-125">Ora si noterà che hello MSDeploy risorsa accetta un **packageUri** proprietà che viene definito come segue:</span><span class="sxs-lookup"><span data-stu-id="4a6d5-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="4a6d5-126">Questo **packageUri** accetta hello uri di account di archiviazione che fa riferimento toohello account di archiviazione in cui verrà caricato il codice postale pacchetto a.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="4a6d5-127">Hello Azure Resource Manager userà [firme di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull un pacchetto di hello verso il basso in locale dall'account di archiviazione hello quando si distribuisce il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="4a6d5-128">Questo processo sarà automatizzato tramite uno script di PowerShell che verrà caricare il pacchetto di hello e chiamare le chiavi hello toocreate API di gestione di Azure hello necessarie e quelli nel modello hello passare come parametri (*_artifactsLocation* e *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="4a6d5-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="4a6d5-129">Sarà necessario toodefine parametri per la cartella hello e nome file pacchetto hello è contenitore di archiviazione hello toounder caricato.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="4a6d5-130">È quindi necessario tooadd in un'altra risorsa annidata toosetup hello hostname associazioni tooleverage un dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="4a6d5-131">Sarà prima necessario tooensure, che proprietario hostname hello e configurarlo toobe verificato da Azure che si è proprietari, vedere [configurare un nome di dominio personalizzato in Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="4a6d5-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="4a6d5-132">Al termine dell'operazione è possibile aggiungere hello seguente modello tooyour nella sezione delle risorse Microsoft.Web/sites hello:</span><span class="sxs-lookup"><span data-stu-id="4a6d5-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="4a6d5-133">Infine è necessario tooadd un'altra risorsa di primo livello, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="4a6d5-134">Questa risorsa conterrà il certificato SSL e sarà presenti allo stesso livello dell'App web e hosting pianificare hello.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="4a6d5-135">È necessario un certificato SSL valido nell'ordine tooset questa risorsa toohave.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="4a6d5-136">Dopo aver tale certificato è necessario byte di pfx hello tooextract sotto forma di stringa base64.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="4a6d5-137">Un'opzione tooextract tratta hello toouse comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="4a6d5-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="4a6d5-138">È quindi possibile passare questo come un modello di distribuzione di parametro tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="4a6d5-139">A questo punto il modello ARM hello è pronto.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="4a6d5-140">Modello di distribuzione</span><span class="sxs-lookup"><span data-stu-id="4a6d5-140">Deploy Template</span></span>
<span data-ttu-id="4a6d5-141">Hello passaggi finali sono toopiece questo tutti insieme in una distribuzione completa end-to-end.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="4a6d5-142">distribuzione toomake più semplice è possibile sfruttare hello **deploy-azureresourcegroup.ps1** script di PowerShell che viene aggiunto quando si crea un progetto di gruppo di risorse di Azure in Visual Studio toohelp con il caricamento di tutti gli elementi necessari nel modello di Hello.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="4a6d5-143">È necessario toohave creato un account di archiviazione toouse anticipatamente.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="4a6d5-144">Per questo esempio, creato un account di archiviazione condivisa per hello package.zip toobe caricato.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="4a6d5-145">script Hello userà l'account di archiviazione toohello AzCopy tooupload hello pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="4a6d5-146">Si passa il percorso della cartella dell'elemento e script hello vengono caricati automaticamente tutti i file all'interno di tale toohello directory denominato contenitore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="4a6d5-147">Dopo aver chiamato deploy-azureresourcegroup.ps1 è toothen aggiornamento hello SSL associazioni toomap hello nome host personalizzato con il certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="4a6d5-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="4a6d5-148">Hello seguente mostra PowerShell hello hello chiamante distribuzione completa Distribuisci-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="4a6d5-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="4a6d5-149">A questo punto l'applicazione è necessario aver distribuito e dovrebbe essere in grado di toobrowse tooit tramite https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="4a6d5-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

