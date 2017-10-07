---
title: risorse di Azure Service Bus aaaCreate utilizzando i modelli di gestione risorse di Azure | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure creazione hello tooautomate di modelli di risorse Bus di servizio
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Creare risorse del bus di servizio usando i modelli di Azure Resource Manager

Questo articolo viene descritto come toocreate e distribuire le risorse di Service Bus con modelli di gestione risorse di Azure, PowerShell e provider di risorse Bus di servizio hello.

Modelli di gestione risorse di Azure consentono di definire hello toodeploy di risorse per una soluzione e toospecify parametri e variabili che consentono valori tooinput per ambienti diversi. modello Hello è costituito da JSON e le espressioni che è possibile utilizzare valori tooconstruct per la distribuzione. Per informazioni dettagliate sulla scrittura di modelli di gestione risorse di Azure e una descrizione del formato di modello hello, vedere [struttura e la sintassi dei modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> Hello come negli esempi contenuti in questa presentazione articolo toouse Azure Resource Manager toocreate uno spazio dei nomi del Bus di servizio e la messaggistica entità (coda). Per altri esempi di modello, visitare hello [raccolta di modelli di avvio rapido di Azure] [ Azure Quickstart Templates gallery] e cercare "Bus di servizio".
>
>

## <a name="service-bus-resource-manager-templates"></a>Modelli di Resource Manager per il bus di servizio

I modelli di Azure Resource Manager del bus di servizio sono disponibili per il download e la distribuzione. Fare clic su hello seguenti collegamenti per informazioni dettagliate su ciascuno di essi, con i modelli di toohello collegamenti in GitHub:

* [Creare uno spazio dei nomi del bus di servizio](service-bus-resource-manager-namespace.md)
* [Creare uno spazio dei nomi del bus di servizio con coda](service-bus-resource-manager-namespace-queue.md)
* [Creare uno spazio dei nomi del bus di servizio con argomento e sottoscrizione](service-bus-resource-manager-namespace-topic.md)
* [Creare uno spazio dei nomi del bus di servizio con coda e regola di autorizzazione](service-bus-resource-manager-namespace-auth-rule.md)
* [Creare uno spazio dei nomi del bus di servizio con argomento, sottoscrizione e regola](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Distribuire con PowerShell

Hello procedura riportata di seguito viene descritto come toouse PowerShell toodeploy un modello di gestione risorse di Azure che crea un **Standard** livello dello spazio dei nomi Service Bus e una coda nello spazio dei nomi. Questo esempio è basato sul hello [creare uno spazio dei nomi del Bus di servizio con coda](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) modello. flusso di lavoro approssimativo Hello è indicato di seguito:

1. Installare PowerShell.
2. Creare un modello di hello e, facoltativamente, un file di parametri.
3. In PowerShell, accedi tooyour account Azure.
4. Se non esiste, creare un nuovo gruppo di risorse.
5. Testare la distribuzione hello.
6. Se si desidera, impostare la modalità di distribuzione hello.
7. Distribuire il modello di hello.

Per informazioni più complete sulla distribuzione dei modelli di Azure Resource Manager, vedere [Distribuire le risorse con i modelli di Azure Resource Manager][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>Installare PowerShell

Installare Azure PowerShell seguendo le istruzioni hello [Introduzione a Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Creare un modello

Clone o copia hello [201-bus di servizio-creare-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) modello da GitHub:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Creare un file di parametri (facoltativo)

toouse un file di parametri facoltativi, hello copia [201-bus di servizio-creare-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file. Sostituire il valore di hello di `serviceBusNamespaceName` con nome hello dello spazio dei nomi Service Bus hello desiderato toocreate in questa distribuzione e sostituire il valore di hello di `serviceBusQueueName` con nome hello della coda di hello da toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Per ulteriori informazioni, vedere hello [parametri](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) argomento.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Accedi tooAzure e impostare hello sottoscrizione di Azure

Da un prompt di PowerShell, eseguire hello comando seguente:

```powershell
Login-AzureRmAccount
```

Si è richiesta toolog su tooyour account Azure. Dopo l'accesso, eseguire hello successivo comando tooview le sottoscrizioni disponibili.

```powershell
Get-AzureRMSubscription
```

Questo comando restituisce un elenco delle sottoscrizioni di Azure disponibili. Scegliere una sottoscrizione per hello sessione corrente eseguendo hello comando seguente. Sostituire `<YourSubscriptionId>` con hello GUID per la sottoscrizione di Azure hello desiderate toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Gruppo di risorse hello set

Se non è una risorsa esistente di gruppo, creare un nuovo gruppo di risorse con hello * * New-AzureRmResourceGroup * * comando. Specificare il nome di hello del gruppo di risorse hello e il percorso toouse. ad esempio:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

Se ha esito positivo, viene visualizzato un riepilogo del nuovo gruppo di risorse hello.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Distribuzione di prova hello

Convalida della distribuzione eseguendo hello `Test-AzureRmResourceGroupDeployment` cmdlet. Durante il test di distribuzione di hello, specificare i parametri, esattamente come quando si esegue la distribuzione di hello.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Crea distribuzione hello

toocreate hello nuova distribuzione, eseguire hello `New-AzureRmResourceGroupDeployment` cmdlet e parametri di hello necessari quando viene richiesto di fornire. parametri di Hello includono un nome per la distribuzione, nome hello del gruppo di risorse e il percorso di hello o file di modello di URL toohello. Se hello **modalità** parametro viene omesso, il valore predefinito di hello **incrementale** viene utilizzato. Per altre informazioni, vedere [Distribuzioni incrementali e complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Hello seguenti al prompt dei comandi è per i parametri nella finestra di PowerShell hello hello tre:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify file dei parametri utilizzare hello comando seguente.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

È anche possibile utilizzare parametri inline quando si esegue il cmdlet di distribuzione hello. comando Hello è come segue:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun un [completo](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) distribuzione, hello set **modalità** parametro troppo**completa**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Verificare la distribuzione di hello
Se le risorse di hello vengano distribuite correttamente, viene visualizzato un riepilogo della distribuzione hello nella finestra di PowerShell hello:

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Passaggi successivi
Abbiamo visto flusso di lavoro base hello e i comandi per la distribuzione di un modello di gestione risorse di Azure. Per informazioni più dettagliate, visitare hello seguenti collegamenti:

* [Panoramica di Azure Resource Manager][Azure Resource Manager overview]
* [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
