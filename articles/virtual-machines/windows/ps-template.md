---
title: una macchina virtuale Windows da un modello in Azure aaaCreate | Documenti Microsoft
description: Utilizzare un modello di gestione delle risorse e PowerShell tooeasily creare una nuova macchina virtuale di Windows.
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
ms.openlocfilehash: 630111482c7dc046091632e2ed458ac143325d59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a><span data-ttu-id="94412-103">Creare una macchina virtuale Windows usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="94412-103">Create a Windows virtual machine from a Resource Manager template</span></span>

<span data-ttu-id="94412-104">In questo articolo illustra come un gestore delle risorse Azure toodeploy modello di utilizzo di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="94412-104">This article shows you how toodeploy an Azure Resource Manager template using PowerShell.</span></span> <span data-ttu-id="94412-105">modello Hello creato consente di distribuire una singola macchina virtuale che esegue Windows Server in una nuova rete virtuale con una singola subnet.</span><span class="sxs-lookup"><span data-stu-id="94412-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="94412-106">Per una descrizione dettagliata della risorsa di macchina virtuale hello, vedere [macchine virtuali in un modello di gestione risorse di Azure](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="94412-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="94412-107">Per ulteriori informazioni su tutte le risorse di hello in un modello, vedere [procedura dettagliata di modello di gestione risorse di Azure](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="94412-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="94412-108">Richiede circa cinque minuti hello toodo i passaggi in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="94412-108">It should take about five minutes toodo hello steps in this article.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="94412-109">Installare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="94412-109">Install Azure PowerShell</span></span>

<span data-ttu-id="94412-110">Vedere [come tooinstall e configurare Azure PowerShell](../../powershell-install-configure.md) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.</span><span class="sxs-lookup"><span data-stu-id="94412-110">See [How tooinstall and configure Azure PowerShell](../../powershell-install-configure.md) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="94412-111">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="94412-111">Create a resource group</span></span>

<span data-ttu-id="94412-112">Tutte le risorse devono essere distribuite in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94412-112">All resources must be deployed in a [resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="94412-113">Ottenere un elenco di località disponibili in cui possono essere create le risorse.</span><span class="sxs-lookup"><span data-stu-id="94412-113">Get a list of available locations where resources can be created.</span></span>
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. <span data-ttu-id="94412-114">Creare il gruppo di risorse hello in percorso hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="94412-114">Create hello resource group in hello location that you select.</span></span> <span data-ttu-id="94412-115">Questo esempio illustra la creazione di hello di un gruppo di risorse denominato **myResourceGroup** in hello **Stati Uniti occidentali** percorso:</span><span class="sxs-lookup"><span data-stu-id="94412-115">This example shows hello creation of a resource group named **myResourceGroup** in hello **West US** location:</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a><span data-ttu-id="94412-116">Creare file hello</span><span class="sxs-lookup"><span data-stu-id="94412-116">Create hello files</span></span>

<span data-ttu-id="94412-117">In questo passaggio si crea un file di modello che consente di distribuire risorse hello e un file di parametri che fornisce modelli di toohello valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="94412-117">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="94412-118">È inoltre possibile creare un file di autorizzazione che è utilizzati tooperform le operazioni di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="94412-118">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

1. <span data-ttu-id="94412-119">Creare un file denominato *CreateVMTemplate.json* e aggiungere questo tooit codice JSON:</span><span class="sxs-lookup"><span data-stu-id="94412-119">Create a file named *CreateVMTemplate.json* and add this JSON code tooit:</span></span>

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

2. <span data-ttu-id="94412-120">Creare un file denominato *Parameters.json* e aggiungere questo tooit codice JSON:</span><span class="sxs-lookup"><span data-stu-id="94412-120">Create a file named *Parameters.json* and add this JSON code tooit:</span></span>

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

3. <span data-ttu-id="94412-121">Creare un nuovo account di archiviazione e un nuovo contenitore:</span><span class="sxs-lookup"><span data-stu-id="94412-121">Create a new storage account and container:</span></span>

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. <span data-ttu-id="94412-122">Caricare l'account di archiviazione toohello file hello:</span><span class="sxs-lookup"><span data-stu-id="94412-122">Upload hello files toohello storage account:</span></span>

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    <span data-ttu-id="94412-123">Modifica hello - percorso del File toohello percorsi in cui sono archiviati i file hello.</span><span class="sxs-lookup"><span data-stu-id="94412-123">Change hello -File paths toohello location where you stored hello files.</span></span>

## <a name="create-hello-resources"></a><span data-ttu-id="94412-124">Creare risorse hello</span><span class="sxs-lookup"><span data-stu-id="94412-124">Create hello resources</span></span>

<span data-ttu-id="94412-125">Distribuire il modello di hello utilizzando parametri hello:</span><span class="sxs-lookup"><span data-stu-id="94412-125">Deploy hello template using hello parameters:</span></span>

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> <span data-ttu-id="94412-126">È inoltre possibile distribuire modelli e parametri da file locali.</span><span class="sxs-lookup"><span data-stu-id="94412-126">You can also deploy templates and parameters from local files.</span></span> <span data-ttu-id="94412-127">vedere, più toolearn [tramite Azure PowerShell con l'archiviazione di Azure](../../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="94412-127">toolearn more, see [Using Azure PowerShell with Azure Storage](../../storage/common/storage-powershell-guide-full.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="94412-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94412-128">Next Steps</span></span>

- <span data-ttu-id="94412-129">Se si sono verificati problemi con la distribuzione di hello, si potrebbe dare un'occhiata [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="94412-129">If there were issues with hello deployment, you might take a look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
- <span data-ttu-id="94412-130">Informazioni su come toocreate e gestire una macchina virtuale in [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="94412-130">Learn how toocreate and manage a virtual machine in [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

