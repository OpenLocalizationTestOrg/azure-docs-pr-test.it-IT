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
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="38184-103">Creare un'immagine personalizzata da un file VHD usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="38184-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="38184-104">Istruzioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="38184-104">Step-by-step instructions</span></span>

<span data-ttu-id="38184-105">Hello passaggi seguenti consentono di eseguire la creazione di un'immagine personalizzata da un file di disco rigido virtuale con PowerShell:</span><span class="sxs-lookup"><span data-stu-id="38184-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="38184-106">Al prompt di PowerShell, accedi tooyour account Azure con hello seguente chiamata toohello **accesso AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38184-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="38184-107">Seleziona hello desiderati sottoscrizione di Azure dal chiamante hello **selezionare AzureRmSubscription** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38184-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="38184-108">Sostituire i seguenti segnaposto per hello hello **$subscriptionId** variabile con un ID sottoscrizione di Azure valida.</span><span class="sxs-lookup"><span data-stu-id="38184-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="38184-109">Ottenere l'oggetto lab hello dal chiamante hello **Get-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38184-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="38184-110">Sostituire i seguenti segnaposto per hello hello **$labRg** e **$labName** variabili con hello valori appropriati per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="38184-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="38184-111">Ottenere account di archiviazione lab hello e account di archiviazione lab valori di chiave dall'oggetto lab hello.</span><span class="sxs-lookup"><span data-stu-id="38184-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="38184-112">Sostituire i seguenti segnaposto per hello hello **$vhdUri** variabile con hello URI tooyour caricamento del file di disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="38184-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="38184-113">È possibile ottenere l'URI del file di disco rigido virtuale hello dal Pannello di blob dell'account di archiviazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="38184-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="38184-114">Creare hello immagine personalizzata utilizzando hello **New AzureRmResourceGroupDeployment** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="38184-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="38184-115">Sostituire i seguenti segnaposto per hello hello **$customImageName** e **$customImageDescription** nomi toomeaningful variabili per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="38184-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="38184-116">Script di PowerShell toocreate un'immagine personalizzata da un file VHD</span><span class="sxs-lookup"><span data-stu-id="38184-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="38184-117">Hello lo script di PowerShell seguente può essere utilizzato toocreate un'immagine personalizzata da un file VHD.</span><span class="sxs-lookup"><span data-stu-id="38184-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="38184-118">Sostituire i segnaposto hello (iniziando e terminando con parentesi angolari) con valori appropriati di hello per le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="38184-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

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

## <a name="related-blog-posts"></a><span data-ttu-id="38184-119">Post di blog correlati</span><span class="sxs-lookup"><span data-stu-id="38184-119">Related blog posts</span></span>

- [<span data-ttu-id="38184-120">Custom images or formulas? (Immagini personalizzate o formule?)</span><span class="sxs-lookup"><span data-stu-id="38184-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="38184-121">Copying Custom Images between Azure DevTest Labs (Copia di immagini personalizzate tra istanze di Azure DevTest Labs)</span><span class="sxs-lookup"><span data-stu-id="38184-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="38184-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38184-122">Next steps</span></span>

- [<span data-ttu-id="38184-123">Aggiungere un ambiente lab tooyour VM</span><span class="sxs-lookup"><span data-stu-id="38184-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
