---
title: "aaaDeploy un'app su un set di scalabilità della macchina virtuale di Azure | Documenti Microsoft"
description: "Informazioni su toodeploy un'applicazione semplice per la scalabilità automatica su una scala di macchina virtuale impostata utilizzando un modello di gestione risorse di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Distribuire un'app di scalabilità automatica usando un modello

[Modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) sono un ottimo modo toodeploy gruppi di risorse correlate. In questa esercitazione si basa su [distribuire un set di scalabilità semplice](virtual-machine-scale-sets-mvss-start.md) e viene descritto come toodeploy il ridimensionamento automatico semplice su una scala da impostare in un'applicazione utilizzando un modello di gestione risorse di Azure.  È inoltre possibile impostare la scalabilità automatica tramite PowerShell, CLI o portale hello. Per altre informazioni, vedere la [panoramica del ridimensionamento automatico](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Due modelli di avvio rapido
Quando si distribuisce un set di scalabilità, è possibile installare nuovo software in un'immagine della piattaforma usando un'[estensione della macchina virtuale](../virtual-machines/virtual-machines-windows-extensions-features.md). Le estensioni della macchina virtuale sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione nelle macchine virtuali di Azure, come ad esempio la distribuzione di un'app. Sono disponibili due modelli di campionamento diversa [Azure/azure-Guida introduttiva: modelli](https://github.com/Azure/azure-quickstart-templates) che mostrano come un'applicazione per la scalabilità automatica su una scala toodeploy impostare utilizzando le estensioni di macchina virtuale.

### <a name="python-http-server-on-linux"></a>Server HTTP Python in Linux
Hello [server HTTP Python in Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modello di esempio consente di distribuire un'applicazione semplice per la scalabilità automatica in esecuzione in un set di scalabilità di Linux.  [Bottiglia](http://bottlepy.org/docs/dev/), un framework di web Python e un server HTTP semplice vengono distribuiti in ogni macchina virtuale nella scala hello impostata utilizzando uno script personalizzato per estensione della macchina virtuale. Scale scala Hello configurato durante l'utilizzo medio della CPU tra tutte le macchine virtuali è maggiore di 60% e il ridimensionamento quando hello medio della CPU è inferiore al 30%.

Inoltre toohello set di scalabilità di risorsa, hello *azuredeploy.json* modello di esempio dichiara inoltre rete virtuale, indirizzo IP pubblico, bilanciamento del carico e le risorse delle impostazioni di scalabilità automatica.  Per altre informazioni sulla creazione di queste risorse in un modello, vedere [Set di scalabilità Linux con scalabilità automatica](virtual-machine-scale-sets-linux-autoscale.md).

In hello *azuredeploy.json* modello, hello `extensionProfile` proprietà di hello `Microsoft.Compute/virtualMachineScaleSets` risorsa specifica un'estensione script personalizzato. `fileUris`Specifica il percorso di script hello. In questo caso, i due file: *workserver.py*, che definisce un server HTTP semplice, e *installserver.sh*, che installa Bottle e avvia hello server HTTP. `commandToExecute`Specifica hello comando toorun dopo la distribuzione di set di scalabilità hello.

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a>Applicazione ASP.NET MVC in Windows
Hello [applicazione MVC ASP.NET in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modello di esempio consente di distribuire una semplice applicazione MVC ASP.NET in esecuzione in IIS nel set di scalabilità di Windows.  IIS e hello app MVC vengono distribuiti hello [(DSC) la configurazione dello stato desiderato tramite PowerShell](virtual-machine-scale-sets-dsc.md) estensione della macchina virtuale.  scala Hello imposta Scale (nell'istanza di macchina virtuale in un momento) quando l'utilizzo della CPU è superiore al 50% per 5 minuti. 

Inoltre toohello set di scalabilità di risorsa, hello *azuredeploy.json* modello di esempio dichiara inoltre rete virtuale, indirizzo IP pubblico, bilanciamento del carico e le risorse delle impostazioni di scalabilità automatica. Questo modello illustra anche l'aggiornamento dell'applicazione.  Per altre informazioni sulla creazione di queste risorse in un modello, vedere [Set di scalabilità Windows con scalabilità automatica](virtual-machine-scale-sets-windows-autoscale.md).

In hello *azuredeploy.json* modello, hello `extensionProfile` proprietà di hello `Microsoft.Compute/virtualMachineScaleSets` risorsa specifica un [configurazione dello stato desiderato (DSC)](virtual-machine-scale-sets-dsc.md) estensione che consente di installare IIS e il valore predefinito app Web da un pacchetto WebDeploy.  Hello *IISInstall.ps1* script nella macchina virtuale hello, viene installato IIS e si trova in hello *DSC* cartella.  applicazione web MVC di Hello è presente in hello *WebDeploy* cartella.  script di installazione toohello percorsi Hello e app web hello sono definiti nel hello `powershelldscZip` e `webDeployPackage` parametri hello *azuredeploy.parameters.json* file. 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a>Distribuire il modello di hello
hello toodeploy modo più semplice di Hello [server HTTP Python in Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [applicazione MVC ASP.NET in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modello è hello toouse **distribuire tooAzure** pulsante trovato in hello nel file Leggimi di hello in GitHub.  È inoltre possibile utilizzare modelli di esempio hello toodeploy PowerShell o CLI di Azure.

### <a name="powershell"></a>PowerShell
Hello copia [server HTTP Python in Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [applicazione MVC ASP.NET in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) file nella cartella tooa repository GitHub hello nel computer locale.  Aprire hello *azuredeploy.parameters.json* file e aggiornare valori predefiniti di hello di hello `vmssName`, `adminUsername`, e `adminPassword` parametri. Salvare lo script di PowerShell seguente troppo hello*deploy.ps1* in hello stessa cartella hello *azuredeploy.json* modello. hello di modello eseguire esempio hello toodeploy *deploy.ps1* script da una finestra di comando di PowerShell.

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
