---
title: Creare una macchina virtuale Windows usando un modello di Azure | Documentazione Microsoft
description: Usare un modello di Resource Manager e PowerShell per creare facilmente una nuova macchina virtuale Windows.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19129d61-8c04-4aa9-a01f-361a09466805
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ddab80262fe27c1f5995858ec7de75d7c46df081
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="418e5-103">Creare una macchina virtuale Windows usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="418e5-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="418e5-104">Questo articolo descrive come distribuire un modello di Azure Resource Manager tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="418e5-104">This article shows you how to deploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="418e5-105">Il modello creato consente di distribuire una singola macchina virtuale che esegue Windows Server in una nuova rete virtuale con un'unica subnet.</span><span class="sxs-lookup"><span data-stu-id="418e5-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="418e5-106">Per una descrizione dettagliata della risorsa macchina virtuale, vedere [Virtual machines in an Azure Resource Manager template](template-description.md) (Macchine virtuali in un modello di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="418e5-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="418e5-107">Per altre informazioni su tutte le risorse in un modello, vedere [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) (Procedura dettagliata sui modelli di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="418e5-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="418e5-108">L'esecuzione della procedura illustrata in questo articolo richiede circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="418e5-108">It should take about five minutes to do the steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="418e5-109">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="418e5-109">Install Azure PowerShell</span></span>

<span data-ttu-id="418e5-110">Per informazioni su come installare la versione più recente di Azure PowerShell, selezionare la sottoscrizione e accedere all'account, vedere [Come installare e configurare Azure PowerShell](../../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="418e5-110">See [How to install and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="418e5-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="418e5-111">Create a resource group</span></span>

<span data-ttu-id="418e5-112">Tutte le risorse devono essere distribuite in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="418e5-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="418e5-113">Ottenere un elenco di località disponibili in cui possono essere create le risorse.</span><span class="sxs-lookup"><span data-stu-id="418e5-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="418e5-114">Creare il gruppo di risorse nella località selezionata.</span><span class="sxs-lookup"><span data-stu-id="418e5-114">Create the resource group in the location that you select.</span></span> <span data-ttu-id="418e5-115">Questo esempio descrive la creazione di un gruppo di risorse denominato **myResourceGroup** nella località **Stati Uniti occidentali**:</span><span class="sxs-lookup"><span data-stu-id="418e5-115">This example shows the creation of a resource group named **myResourceGroup** in the **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-the-files"></a><span data-ttu-id="418e5-116">Creare i file</span><span class="sxs-lookup"><span data-stu-id="418e5-116">Create the files</span></span>

<span data-ttu-id="418e5-117">In questo passaggio si crea un file di modello che consente di distribuire le risorse e un file di parametri che fornisce i valori dei parametri nel modello.</span><span class="sxs-lookup"><span data-stu-id="418e5-117">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="418e5-118">È possibile anche creare un file di autorizzazione da usare per eseguire operazioni in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="418e5-118">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="418e5-119">Creare un file denominato *CreateVMTemplate.json* e aggiungervi questo codice JSON:</span><span class="sxs-lookup"><span data-stu-id="418e5-119">Create a file named *CreateVMTemplate.json* and add this JSON code to it:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

2. <span data-ttu-id="418e5-120">Creare un file denominato *Parameters.json* e aggiungervi questo codice JSON:</span><span class="sxs-lookup"><span data-stu-id="418e5-120">Create a file named *Parameters.json* and add this JSON code to it:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

3. <span data-ttu-id="418e5-121">Creare un nuovo account di archiviazione e un nuovo contenitore:</span><span class="sxs-lookup"><span data-stu-id="418e5-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="418e5-122">Caricare i file nell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="418e5-122">Upload the files to the storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="418e5-123">Cambiare i percorsi -File nella posizione in cui sono stati archiviati i file.</span><span class="sxs-lookup"><span data-stu-id="418e5-123">Change the -File paths to the location where you stored the files.</span></span>

## <a name="create-the-resources"></a><span data-ttu-id="418e5-124">Creare le risorse</span><span class="sxs-lookup"><span data-stu-id="418e5-124">Create the resources</span></span>

<span data-ttu-id="418e5-125">Distribuire il modello usando i parametri:</span><span class="sxs-lookup"><span data-stu-id="418e5-125">Deploy the template using the parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="418e5-126">È inoltre possibile distribuire modelli e parametri da file locali.</span><span class="sxs-lookup"><span data-stu-id="418e5-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="418e5-127">Per altre informazioni, vedere [Uso di Azure PowerShell con Archiviazione di Azure](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="418e5-127">To learn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="418e5-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="418e5-128">Next Steps</span></span>

- <span data-ttu-id="418e5-129">Se si sono verificati problemi con la distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="418e5-129">If there were issues with the deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="418e5-130">Informazioni su come creare e gestire una macchina virtuale sono disponibili in [Creare e gestire macchine virtuali di Windows con il modulo Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="418e5-130">Learn how to create and manage a virtual machine in [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

