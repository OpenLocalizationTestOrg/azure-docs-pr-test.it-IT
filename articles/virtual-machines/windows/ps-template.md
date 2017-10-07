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
# <a name="create-a-windows-virtual-machine-from-a-resource-manager-template"></a>Creare una macchina virtuale Windows usando un modello di Resource Manager

In questo articolo illustra come un gestore delle risorse Azure toodeploy modello di utilizzo di PowerShell. modello Hello creato consente di distribuire una singola macchina virtuale che esegue Windows Server in una nuova rete virtuale con una singola subnet.

Per una descrizione dettagliata della risorsa di macchina virtuale hello, vedere [macchine virtuali in un modello di gestione risorse di Azure](template-description.md). Per ulteriori informazioni su tutte le risorse di hello in un modello, vedere [procedura dettagliata di modello di gestione risorse di Azure](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Richiede circa cinque minuti hello toodo i passaggi in questo articolo.

## <a name="install-azure-powershell"></a>Installare Azure PowerShell

Vedere [come tooinstall e configurare Azure PowerShell](../../powershell-install-configure.md) per informazioni sull'installazione hello la versione più recente di Azure PowerShell, selezionando la sottoscrizione e la firma nell'account tooyour.

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Tutte le risorse devono essere distribuite in un [gruppo di risorse](../../azure-resource-manager/resource-group-overview.md).

1. Ottenere un elenco di località disponibili in cui possono essere create le risorse.
   
    ```powershell   
    Get-AzureRmLocation | sort DisplayName | Select DisplayName
    ```

2. Creare il gruppo di risorse hello in percorso hello selezionato. Questo esempio illustra la creazione di hello di un gruppo di risorse denominato **myResourceGroup** in hello **Stati Uniti occidentali** percorso:

    ```powershell   
    New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
    ```

## <a name="create-hello-files"></a>Creare file hello

In questo passaggio si crea un file di modello che consente di distribuire risorse hello e un file di parametri che fornisce modelli di toohello valori di parametro. È inoltre possibile creare un file di autorizzazione che è utilizzati tooperform le operazioni di gestione risorse di Azure.

1. Creare un file denominato *CreateVMTemplate.json* e aggiungere questo tooit codice JSON:

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

2. Creare un file denominato *Parameters.json* e aggiungere questo tooit codice JSON:

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

3. Creare un nuovo account di archiviazione e un nuovo contenitore:

    ```powershell
    $storageName = "st" + (Get-Random)
    New-AzureRmStorageAccount -ResourceGroupName "myResourceGroup" -AccountName $storageName -Location "West US" -SkuName "Standard_LRS" -Kind Storage
    $accountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName myResourceGroup -Name $storageName).Value[0]
    $context = New-AzureStorageContext -StorageAccountName $storageName -StorageAccountKey $accountKey 
    New-AzureStorageContainer -Name "templates" -Context $context -Permission Container
    ```

4. Caricare l'account di archiviazione toohello file hello:

    ```powershell
    Set-AzureStorageBlobContent -File "C:\templates\CreateVMTemplate.json" -Context $context -Container "templates"
    Set-AzureStorageBlobContent -File "C:\templates\Parameters.json" -Context $context -Container templates
    ```

    Modifica hello - percorso del File toohello percorsi in cui sono archiviati i file hello.

## <a name="create-hello-resources"></a>Creare risorse hello

Distribuire il modello di hello utilizzando parametri hello:

```powershell
$templatePath = "https://" + $storageName + ".blob.core.windows.net/templates/CreateVMTemplate.json"
$parametersPath = "https://" + $storageName + ".blob.core.windows.net/templates/Parameters.json"
New-AzureRmResourceGroupDeployment -ResourceGroupName "myResourceGroup" -Name "myDeployment" -TemplateUri $templatePath -TemplateParameterUri $parametersPath 
```

> [!NOTE]
> È inoltre possibile distribuire modelli e parametri da file locali. vedere, più toolearn [tramite Azure PowerShell con l'archiviazione di Azure](../../storage/common/storage-powershell-guide-full.md).

## <a name="next-steps"></a>Passaggi successivi

- Se si sono verificati problemi con la distribuzione di hello, si potrebbe dare un'occhiata [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
- Informazioni su come toocreate e gestire una macchina virtuale in [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

