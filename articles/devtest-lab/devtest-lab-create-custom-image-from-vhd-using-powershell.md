---
title: aaaCreate un'immagine personalizzata Azure DevTest Labs da un file di disco rigido virtuale mediante PowerShell | Documenti Microsoft
description: Automatizzare la creazione di un'immagine personalizzata in Azure DevTest Labs da un file VHD usando PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>Creare un'immagine personalizzata da un file VHD usando PowerShell

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Istruzioni dettagliate

Hello passaggi seguenti consentono di eseguire la creazione di un'immagine personalizzata da un file di disco rigido virtuale con PowerShell:

1. Al prompt di PowerShell, accedi tooyour account Azure con hello seguente chiamata toohello **accesso AzureRmAccount** cmdlet.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Seleziona hello desiderati sottoscrizione di Azure dal chiamante hello **selezionare AzureRmSubscription** cmdlet. Sostituire i seguenti segnaposto per hello hello **$subscriptionId** variabile con un ID sottoscrizione di Azure valida. 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  Ottenere l'oggetto lab hello dal chiamante hello **Get-AzureRmResource** cmdlet. Sostituire i seguenti segnaposto per hello hello **$labRg** e **$labName** variabili con hello valori appropriati per l'ambiente. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Ottenere account di archiviazione lab hello e account di archiviazione lab valori di chiave dall'oggetto lab hello. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Sostituire i seguenti segnaposto per hello hello **$vhdUri** variabile con hello URI tooyour caricamento del file di disco rigido virtuale. È possibile ottenere l'URI del file di disco rigido virtuale hello dal Pannello di blob dell'account di archiviazione hello in hello portale di Azure.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Creare hello immagine personalizzata utilizzando hello **New AzureRmResourceGroupDeployment** cmdlet. Sostituire i seguenti segnaposto per hello hello **$customImageName** e **$customImageDescription** nomi toomeaningful variabili per l'ambiente.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>Script di PowerShell toocreate un'immagine personalizzata da un file VHD

Hello lo script di PowerShell seguente può essere utilizzato toocreate un'immagine personalizzata da un file VHD. Sostituire i segnaposto hello (iniziando e terminando con parentesi angolari) con valori appropriati di hello per le proprie esigenze. 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a>Post di blog correlati

- [Custom images or formulas? (Immagini personalizzate o formule?)](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Passaggi successivi

- [Aggiungere un ambiente lab tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
