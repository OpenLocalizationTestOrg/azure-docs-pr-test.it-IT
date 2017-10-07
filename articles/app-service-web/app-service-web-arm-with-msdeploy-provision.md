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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Distribuire un'app Web con MSDeploy, il nome host personalizzato e il certificato SSL
Questa guida vengono illustrati la creazione di una distribuzione end-to-end per un'App Web di Azure, sfruttando MSDeploy nonché di aggiunta di un nome host personalizzato e un modello ARM toohello certificato SSL.

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Creare l'applicazione di esempio
Si distribuirà un'applicazione Web ASP.NET. toocreate una semplice applicazione web, è innanzitutto Hello (o è possibile scegliere toouse uno esistente, nel qual caso è possibile ignorare questo passaggio).

Aprire Visual Studio 2015 e scegliere File > Nuovo progetto. Nella finestra di dialogo hello visualizzata scegliere Web > applicazione Web ASP.NET. Nel riquadro Modelli scegliere Web e scegliere il modello MVC hello. Selezionare *Cambia tipo di autenticazione* troppo*Nessuna autenticazione*. Si tratta semplicemente toomake hello applicazione di esempio più semplice possibile.

A questo punto si avrà una base toouse pronto di ASP.Net web app come parte del processo di distribuzione.

### <a name="create-msdeploy-package"></a>Creare il pacchetto MSDeploy
Passaggio successivo è toocreate hello pacchetto toodeploy hello web app tooAzure. toodo, salvare il progetto e quindi eseguire l'esempio hello dalla riga di comando hello:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Verrà creato un pacchetto compresso nella cartella PackageLocation hello. Hello applicazione è ora pronto toobe distribuito, che è possibile ora creare un toodo modello di gestione risorse di Azure che.

### <a name="create-arm-template"></a>Creare il modello di Gestione risorse di Azure
Iniziare con un modello di Gestione risorse di Azure di base che creerà un'applicazione Web e un piano di hosting. Si noti che i parametri e le variabili non vengono visualizzati per brevità.

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

Successivamente, sarà necessario toomodify hello web app risorsa tootake una risorsa di MSDeploy annidata. Verrà consentire si tooreference hello pacchetto creato in precedenza e indicare a Gestione risorse di Azure toouse MSDeploy toodeploy hello pacchetto toohello WebApp di Azure. Hello seguente risorsa Microsoft.Web/sites hello risorsa di MSDeploy hello annidato:

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

Ora si noterà che hello MSDeploy risorsa accetta un **packageUri** proprietà che viene definito come segue:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Questo **packageUri** accetta hello uri di account di archiviazione che fa riferimento toohello account di archiviazione in cui verrà caricato il codice postale pacchetto a. Hello Azure Resource Manager userà [firme di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull un pacchetto di hello verso il basso in locale dall'account di archiviazione hello quando si distribuisce il modello di hello. Questo processo sarà automatizzato tramite uno script di PowerShell che verrà caricare il pacchetto di hello e chiamare le chiavi hello toocreate API di gestione di Azure hello necessarie e quelli nel modello hello passare come parametri (*_artifactsLocation* e *_artifactsLocationSasToken*). Sarà necessario toodefine parametri per la cartella hello e nome file pacchetto hello è contenitore di archiviazione hello toounder caricato.

È quindi necessario tooadd in un'altra risorsa annidata toosetup hello hostname associazioni tooleverage un dominio personalizzato. Sarà prima necessario tooensure, che proprietario hostname hello e configurarlo toobe verificato da Azure che si è proprietari, vedere [configurare un nome di dominio personalizzato in Azure App Service](app-service-web-tutorial-custom-domain.md). Al termine dell'operazione è possibile aggiungere hello seguente modello tooyour nella sezione delle risorse Microsoft.Web/sites hello:

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

Infine è necessario tooadd un'altra risorsa di primo livello, Microsoft.Web/certificates. Questa risorsa conterrà il certificato SSL e sarà presenti allo stesso livello dell'App web e hosting pianificare hello.

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

È necessario un certificato SSL valido nell'ordine tooset questa risorsa toohave. Dopo aver tale certificato è necessario byte di pfx hello tooextract sotto forma di stringa base64. Un'opzione tooextract tratta hello toouse comando PowerShell seguente:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

È quindi possibile passare questo come un modello di distribuzione di parametro tooyour ARM.

A questo punto il modello ARM hello è pronto.

### <a name="deploy-template"></a>Modello di distribuzione
Hello passaggi finali sono toopiece questo tutti insieme in una distribuzione completa end-to-end. distribuzione toomake più semplice è possibile sfruttare hello **deploy-azureresourcegroup.ps1** script di PowerShell che viene aggiunto quando si crea un progetto di gruppo di risorse di Azure in Visual Studio toohelp con il caricamento di tutti gli elementi necessari nel modello di Hello. È necessario toohave creato un account di archiviazione toouse anticipatamente. Per questo esempio, creato un account di archiviazione condivisa per hello package.zip toobe caricato. script Hello userà l'account di archiviazione toohello AzCopy tooupload hello pacchetto. Si passa il percorso della cartella dell'elemento e script hello vengono caricati automaticamente tutti i file all'interno di tale toohello directory denominato contenitore di archiviazione. Dopo aver chiamato deploy-azureresourcegroup.ps1 è toothen aggiornamento hello SSL associazioni toomap hello nome host personalizzato con il certificato SSL.

Hello seguente mostra PowerShell hello hello chiamante distribuzione completa Distribuisci-AzureResourceGroup.ps1:

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

A questo punto l'applicazione è necessario aver distribuito e dovrebbe essere in grado di toobrowse tooit tramite https://www.yourcustomdomain.com

