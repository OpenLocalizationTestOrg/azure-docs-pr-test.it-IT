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
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="f240d-103">Distribuire un'app di scalabilità automatica usando un modello</span><span class="sxs-lookup"><span data-stu-id="f240d-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="f240d-104">[Modelli di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) sono un ottimo modo toodeploy gruppi di risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="f240d-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="f240d-105">In questa esercitazione si basa su [distribuire un set di scalabilità semplice](virtual-machine-scale-sets-mvss-start.md) e viene descritto come toodeploy il ridimensionamento automatico semplice su una scala da impostare in un'applicazione utilizzando un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f240d-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="f240d-106">È inoltre possibile impostare la scalabilità automatica tramite PowerShell, CLI o portale hello.</span><span class="sxs-lookup"><span data-stu-id="f240d-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="f240d-107">Per altre informazioni, vedere la [panoramica del ridimensionamento automatico](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f240d-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="f240d-108">Due modelli di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="f240d-108">Two quickstart templates</span></span>
<span data-ttu-id="f240d-109">Quando si distribuisce un set di scalabilità, è possibile installare nuovo software in un'immagine della piattaforma usando un'[estensione della macchina virtuale](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="f240d-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="f240d-110">Le estensioni della macchina virtuale sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione nelle macchine virtuali di Azure, come ad esempio la distribuzione di un'app.</span><span class="sxs-lookup"><span data-stu-id="f240d-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="f240d-111">Sono disponibili due modelli di campionamento diversa [Azure/azure-Guida introduttiva: modelli](https://github.com/Azure/azure-quickstart-templates) che mostrano come un'applicazione per la scalabilità automatica su una scala toodeploy impostare utilizzando le estensioni di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f240d-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="f240d-112">Server HTTP Python in Linux</span><span class="sxs-lookup"><span data-stu-id="f240d-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="f240d-113">Hello [server HTTP Python in Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modello di esempio consente di distribuire un'applicazione semplice per la scalabilità automatica in esecuzione in un set di scalabilità di Linux.</span><span class="sxs-lookup"><span data-stu-id="f240d-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="f240d-114">[Bottiglia](http://bottlepy.org/docs/dev/), un framework di web Python e un server HTTP semplice vengono distribuiti in ogni macchina virtuale nella scala hello impostata utilizzando uno script personalizzato per estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f240d-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="f240d-115">Scale scala Hello configurato durante l'utilizzo medio della CPU tra tutte le macchine virtuali è maggiore di 60% e il ridimensionamento quando hello medio della CPU è inferiore al 30%.</span><span class="sxs-lookup"><span data-stu-id="f240d-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="f240d-116">Inoltre toohello set di scalabilità di risorsa, hello *azuredeploy.json* modello di esempio dichiara inoltre rete virtuale, indirizzo IP pubblico, bilanciamento del carico e le risorse delle impostazioni di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="f240d-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="f240d-117">Per altre informazioni sulla creazione di queste risorse in un modello, vedere [Set di scalabilità Linux con scalabilità automatica](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f240d-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="f240d-118">In hello *azuredeploy.json* modello, hello `extensionProfile` proprietà di hello `Microsoft.Compute/virtualMachineScaleSets` risorsa specifica un'estensione script personalizzato.</span><span class="sxs-lookup"><span data-stu-id="f240d-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="f240d-119">`fileUris`Specifica il percorso di script hello.</span><span class="sxs-lookup"><span data-stu-id="f240d-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="f240d-120">In questo caso, i due file: *workserver.py*, che definisce un server HTTP semplice, e *installserver.sh*, che installa Bottle e avvia hello server HTTP.</span><span class="sxs-lookup"><span data-stu-id="f240d-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="f240d-121">`commandToExecute`Specifica hello comando toorun dopo la distribuzione di set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="f240d-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="f240d-122">Applicazione ASP.NET MVC in Windows</span><span class="sxs-lookup"><span data-stu-id="f240d-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="f240d-123">Hello [applicazione MVC ASP.NET in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modello di esempio consente di distribuire una semplice applicazione MVC ASP.NET in esecuzione in IIS nel set di scalabilità di Windows.</span><span class="sxs-lookup"><span data-stu-id="f240d-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="f240d-124">IIS e hello app MVC vengono distribuiti hello [(DSC) la configurazione dello stato desiderato tramite PowerShell](virtual-machine-scale-sets-dsc.md) estensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f240d-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="f240d-125">scala Hello imposta Scale (nell'istanza di macchina virtuale in un momento) quando l'utilizzo della CPU è superiore al 50% per 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="f240d-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="f240d-126">Inoltre toohello set di scalabilità di risorsa, hello *azuredeploy.json* modello di esempio dichiara inoltre rete virtuale, indirizzo IP pubblico, bilanciamento del carico e le risorse delle impostazioni di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="f240d-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="f240d-127">Questo modello illustra anche l'aggiornamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f240d-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="f240d-128">Per altre informazioni sulla creazione di queste risorse in un modello, vedere [Set di scalabilità Windows con scalabilità automatica](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f240d-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="f240d-129">In hello *azuredeploy.json* modello, hello `extensionProfile` proprietà di hello `Microsoft.Compute/virtualMachineScaleSets` risorsa specifica un [configurazione dello stato desiderato (DSC)](virtual-machine-scale-sets-dsc.md) estensione che consente di installare IIS e il valore predefinito app Web da un pacchetto WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="f240d-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="f240d-130">Hello *IISInstall.ps1* script nella macchina virtuale hello, viene installato IIS e si trova in hello *DSC* cartella.</span><span class="sxs-lookup"><span data-stu-id="f240d-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="f240d-131">applicazione web MVC di Hello è presente in hello *WebDeploy* cartella.</span><span class="sxs-lookup"><span data-stu-id="f240d-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="f240d-132">script di installazione toohello percorsi Hello e app web hello sono definiti nel hello `powershelldscZip` e `webDeployPackage` parametri hello *azuredeploy.parameters.json* file.</span><span class="sxs-lookup"><span data-stu-id="f240d-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-hello-template"></a><span data-ttu-id="f240d-133">Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="f240d-133">Deploy hello template</span></span>
<span data-ttu-id="f240d-134">hello toodeploy modo più semplice di Hello [server HTTP Python in Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [applicazione MVC ASP.NET in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modello è hello toouse **distribuire tooAzure** pulsante trovato in hello nel file Leggimi di hello in GitHub.</span><span class="sxs-lookup"><span data-stu-id="f240d-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="f240d-135">È inoltre possibile utilizzare modelli di esempio hello toodeploy PowerShell o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="f240d-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="f240d-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f240d-136">PowerShell</span></span>
<span data-ttu-id="f240d-137">Hello copia [server HTTP Python in Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) o [applicazione MVC ASP.NET in Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) file nella cartella tooa repository GitHub hello nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="f240d-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="f240d-138">Aprire hello *azuredeploy.parameters.json* file e aggiornare valori predefiniti di hello di hello `vmssName`, `adminUsername`, e `adminPassword` parametri.</span><span class="sxs-lookup"><span data-stu-id="f240d-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="f240d-139">Salvare lo script di PowerShell seguente troppo hello*deploy.ps1* in hello stessa cartella hello *azuredeploy.json* modello.</span><span class="sxs-lookup"><span data-stu-id="f240d-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="f240d-140">hello di modello eseguire esempio hello toodeploy *deploy.ps1* script da una finestra di comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f240d-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="f240d-141">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f240d-141">Azure CLI</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f240d-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f240d-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
