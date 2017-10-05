---
title: Creare gruppi di sicurezza di rete - Modello di Azure Resource Manager | Documentazione Microsoft
description: Informazioni su come creare e distribuire i gruppi di sicurezza di rete mediante il modello di Azure Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88f7e5b2144daee7bf1c8e7312ba98e6fa967899
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="45847-103">Creare gruppi di sicurezza di rete mediante il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45847-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="45847-104">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="45847-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="45847-105">È anche possibile creare gruppi di sicurezza di rete con il [modello di distribuzione classica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="45847-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="45847-106">Risorse NSG in un file di modello</span><span class="sxs-lookup"><span data-stu-id="45847-106">NSG resources in a template file</span></span>
<span data-ttu-id="45847-107">È possibile visualizzare e scaricare il [modello di esempio](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="45847-107">You can view and download the [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="45847-108">La sezione seguente illustra la definizione di gruppo di sicurezza di rete front-end in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="45847-108">The following section shows the definition of the front-end NSG, based on the scenario.</span></span>

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
<span data-ttu-id="45847-109">Per associare il gruppo di sicurezza di rete alla subnet front-end, è necessario modificare la definizione della subnet nel modello e usare l'id di riferimento per il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="45847-109">To associate the NSG to the front-end subnet, you have to change the subnet definition in the template, and use the reference id for the NSG.</span></span>

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

<span data-ttu-id="45847-110">Si noti che va effettuata la stessa operazione per il gruppo di sicurezza di rete back-end e la subnet back-end nel modello.</span><span class="sxs-lookup"><span data-stu-id="45847-110">Notice the same being done for the back-end NSG and the back-end subnet in the template.</span></span>

## <a name="deploy-the-arm-template-by-using-click-to-deploy"></a><span data-ttu-id="45847-111">Distribuire il modello ARM tramite clic per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="45847-111">Deploy the ARM template by using click to deploy</span></span>
<span data-ttu-id="45847-112">Il modello di esempio disponibile nel repository pubblico usa un file di parametro che contiene i valori predefiniti usati per generare lo scenario descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45847-112">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="45847-113">Distribuire [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG)tramite clic per la distribuzione, fare clic su **Distribuisci in Azure**, sostituire i valori del parametro predefinito se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="45847-113">To deploy this template using click to deploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-arm-template-by-using-powershell"></a><span data-ttu-id="45847-114">Distribuire il modello ARM tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="45847-114">Deploy the ARM template by using PowerShell</span></span>
<span data-ttu-id="45847-115">Per distribuire il modello ARM scaricato tramite PowerShell, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="45847-115">To deploy the ARM template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="45847-116">Se si usa Azure PowerShell per la prima volta, vedere [How to Install and Configure Azure PowerShell](/powershell/azure/overview) (Come installare e configurare Azure PowerShell) per l'installazione e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="45847-116">If you have never used Azure PowerShell, follow the instructions in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) to install and configure it.</span></span>
2. <span data-ttu-id="45847-117">Eseguire il cmdlet **`New-AzureRmResourceGroup`** per creare un gruppo di risorse usando il modello.</span><span class="sxs-lookup"><span data-stu-id="45847-117">Run the **`New-AzureRmResourceGroup`** cmdlet to create a resource group using the template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="45847-118">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="45847-118">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-the-arm-template-by-using-the-azure-cli"></a><span data-ttu-id="45847-119">Distribuire il modello ARM tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="45847-119">Deploy the ARM template by using the Azure CLI</span></span>
<span data-ttu-id="45847-120">Per distribuire il modello ARM tramite l'interfaccia della riga di comando di Azure, seguire la procedura di seguito.</span><span class="sxs-lookup"><span data-stu-id="45847-120">To deploy the ARM template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="45847-121">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45847-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="45847-122">Eseguire il comando **`azure config mode`** per passare alla modalità Gestione risorse, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="45847-122">Run the **`azure config mode`** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="45847-123">Di seguito è riportato l'output previsto per il comando:</span><span class="sxs-lookup"><span data-stu-id="45847-123">The following is the expected output for the command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="45847-124">Eseguire il cmdlet **`azure group deployment create`** per distribuire la nuova rete virtuale usando il modello e i file dei parametri scaricati e modificati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45847-124">Run the **`azure group deployment create`** cmdlet to deploy the new VNet by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="45847-125">Nell'elenco riportato dopo l'output sono indicati i parametri usati.</span><span class="sxs-lookup"><span data-stu-id="45847-125">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="45847-126">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="45847-126">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * <span data-ttu-id="45847-127">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="45847-127">**-n (or --name)**.</span></span> <span data-ttu-id="45847-128">Nome del gruppo di risorse da creare.</span><span class="sxs-lookup"><span data-stu-id="45847-128">Name of the resource group to be created.</span></span>
   * <span data-ttu-id="45847-129">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="45847-129">**-l (or --location)**.</span></span> <span data-ttu-id="45847-130">L'area di Azure in cui verrà creato il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="45847-130">Azure region where the resource group will be created.</span></span>
   * <span data-ttu-id="45847-131">**-f (o --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="45847-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="45847-132">Percorso del file di modello ARM.</span><span class="sxs-lookup"><span data-stu-id="45847-132">Path to your ARM template file.</span></span>
   * <span data-ttu-id="45847-133">**-e (o --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="45847-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="45847-134">Percorso del file di parametri ARM.</span><span class="sxs-lookup"><span data-stu-id="45847-134">Path to your ARM parameters file.</span></span>

