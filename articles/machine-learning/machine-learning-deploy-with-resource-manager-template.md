---
title: un'area di lavoro di Machine Learning con Azure Resource Manager aaaDeploy | Documenti Microsoft
description: Come toodeploy un'area di lavoro per Azure Machine Learning che usano il modello di gestione risorse di Azure
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a>Distribuire un'area di lavoro di Machine Learning con Azure Resource Manager
## <a name="introduction"></a>Introduzione
Utilizzando un gestore delle risorse Azure modello di distribuzione consente di risparmiare tempo fornendo un modo scalabile di toodeploy interconnessi componenti con un meccanismo di convalida e riprovare. tooset le aree di lavoro di Azure Machine Learning, ad esempio, è necessario configurare un account di archiviazione di Azure e quindi distribuire l'area di lavoro di toofirst. Si immagini di doverlo fare manualmente per centinaia di aree di lavoro. Un'alternativa più semplice è toouse un toodeploy modello di gestione risorse di Azure un'area di lavoro di Azure Machine Learning e tutte le relative dipendenze. Questo articolo illustra il processo in dettaglio. Per una panoramica generale di Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

## <a name="step-by-step-create-a-machine-learning-workspace"></a>Procedura dettagliata: Creare un'area di lavoro di Machine Learning
Verrà creato un gruppo di risorse di Azure, quindi verranno distribuiti un nuovo account di archiviazione di Azure e una nuova area di lavoro di Azure Machine Learning usando un modello di Resource Manager. Una volta completata la distribuzione di hello, si verrà stampato informazioni importanti sulle aree di lavoro hello creati (chiave primaria hello Idareadilavoro hello e dell'area di lavoro di hello URL toohello).

### <a name="create-an-azure-resource-manager-template"></a>Creare un modello di Azure Resource Manager
Un'area di lavoro di Machine Learning richiede un set di dati collegato tooit di archiviazione di Azure account toostore hello.
Hello modello seguente utilizza il nome di hello del hello Nome gruppo di risorse toogenerate hello storage account e il nome dell'area di lavoro hello.  Utilizza inoltre nome account di archiviazione hello come una proprietà durante la creazione dell'area di lavoro di hello.

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
Salvare questo modello come file mlworkspace.json in c:\temp\.

### <a name="deploy-hello-resource-group-based-on-hello-template"></a>Distribuire il gruppo di risorse hello, basato sul modello hello
* Aprire PowerShell
* Installare i moduli per Azure Resource Manager e Azure Service Management  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   Questi passaggi scaricare e installare i passaggi rimanenti hello hello moduli toocomplete necessarie. Questa operazione deve solo toobe eseguito una volta nell'ambiente di hello in cui si siano eseguendo i comandi di PowerShell hello.   

* L'autenticazione tooAzure  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
Questo passaggio è necessario toobe ripetuto per ogni sessione. Una volta eseguita l'autenticazione, verranno visualizzate le informazioni sulla sottoscrizione.

![Account Azure][1]

Ora che si dispone di accesso tooAzure, possiamo creare il gruppo di risorse hello.

* Creare un gruppo di risorse

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

Verificare che il gruppo di risorse hello viene correttamente eseguito il provisioning. **ProvisioningState** deve essere "Succeeded".
nome del gruppo di risorse Hello viene utilizzato dal nome account di archiviazione di hello modello toogenerate hello. nome account di archiviazione Hello deve essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare numeri e lettere minuscole solo.

![Gruppo di risorse][2]

* Mediante la distribuzione di gruppo di risorse hello, distribuire una nuova area di Machine Learning.

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

Al termine della distribuzione di hello, risulta semplice tooaccess proprietà dell'area di lavoro hello che è stato distribuito. Ad esempio, è possibile accedere hello Token di chiave primaria.

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

Un altro token di tooretrieve modo dell'area di lavoro esistente è hello toouse comando Invoke-AzureRmResourceAction. Ad esempio, è possibile elencare i token primario e secondario hello di tutte le aree di lavoro.

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
Dopo il provisioning dell'area di lavoro di hello, è inoltre possibile automatizzare molte attività di Azure Machine Learning Studio usando hello [modulo PowerShell per Azure Machine Learning](http://aka.ms/amlps).

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sulla [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). 
* Osservare hello [archivio modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates). 
* Guardare questo video su [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39). 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
