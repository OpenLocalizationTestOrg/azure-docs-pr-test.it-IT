---
title: -i gruppi di sicurezza di rete aaaCreate il modello di gestione risorse di Azure | Documenti Microsoft
description: Informazioni su come toocreate e distribuire i gruppi di sicurezza di rete utilizzando un modello di gestione risorse di Azure.
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
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a><span data-ttu-id="1d38b-103">Creare gruppi di sicurezza di rete mediante il modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d38b-103">Create network security groups using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="1d38b-104">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="1d38b-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="1d38b-105">È anche possibile [creare NSGs nel modello di distribuzione classica hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1d38b-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a><span data-ttu-id="1d38b-106">Risorse NSG in un file di modello</span><span class="sxs-lookup"><span data-stu-id="1d38b-106">NSG resources in a template file</span></span>
<span data-ttu-id="1d38b-107">È possibile visualizzare e scaricare hello [modello di esempio](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span><span class="sxs-lookup"><span data-stu-id="1d38b-107">You can view and download hello [sample template](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).</span></span>

<span data-ttu-id="1d38b-108">Hello nella sezione seguente viene illustrata hello definizione di hello NSG front-end, a seconda dello scenario di hello.</span><span class="sxs-lookup"><span data-stu-id="1d38b-108">hello following section shows hello definition of hello front-end NSG, based on hello scenario.</span></span>

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
<span data-ttu-id="1d38b-109">tooassociate hello NSG toohello front-end subnet, è la definizione di subnet hello toochange nel modello hello e utilizzare hello di id di riferimento per hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="1d38b-109">tooassociate hello NSG toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello NSG.</span></span>

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

<span data-ttu-id="1d38b-110">Si noti hello stesso fatta per hello back-end NSG e hello subnet back-end nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="1d38b-110">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="1d38b-111">Distribuire il modello ARM hello utilizzando fare clic su toodeploy</span><span class="sxs-lookup"><span data-stu-id="1d38b-111">Deploy hello ARM template by using click toodeploy</span></span>
<span data-ttu-id="1d38b-112">modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="1d38b-112">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="1d38b-113">toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="1d38b-113">toodeploy this template using click toodeploy, follow [this link](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-arm-template-by-using-powershell"></a><span data-ttu-id="1d38b-114">Distribuire il modello ARM hello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d38b-114">Deploy hello ARM template by using PowerShell</span></span>
<span data-ttu-id="1d38b-115">modello ARM hello toodeploy scaricato tramite PowerShell, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="1d38b-115">toodeploy hello ARM template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="1d38b-116">Se non si è mai usato Azure PowerShell, attenersi alle istruzioni hello hello [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) tooinstall e configurarlo.</span><span class="sxs-lookup"><span data-stu-id="1d38b-116">If you have never used Azure PowerShell, follow hello instructions in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) tooinstall and configure it.</span></span>
2. <span data-ttu-id="1d38b-117">Eseguire hello  **`New-AzureRmResourceGroup`**  toocreate cmdlet un gruppo di risorse utilizzando hello modello.</span><span class="sxs-lookup"><span data-stu-id="1d38b-117">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="1d38b-118">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="1d38b-118">Expected output:</span></span>

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

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a><span data-ttu-id="1d38b-119">Distribuire il modello di ARM hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="1d38b-119">Deploy hello ARM template by using hello Azure CLI</span></span>
<span data-ttu-id="1d38b-120">modello ARM hello toodeploy utilizzando hello CLI di Azure, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="1d38b-120">toodeploy hello ARM template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="1d38b-121">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1d38b-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="1d38b-122">Eseguire hello  **`azure config mode`**  tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1d38b-122">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="1d38b-123">di seguito Hello è output di hello previsto per il comando hello:</span><span class="sxs-lookup"><span data-stu-id="1d38b-123">hello following is hello expected output for hello command:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="1d38b-124">Eseguire hello  **`azure group deployment create`**  cmdlet toodeploy hello nuova rete virtuale utilizzando il modello di hello e parametro file scaricato e modificato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1d38b-124">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="1d38b-125">elenco di Hello visualizzato dopo l'output di hello illustrati parametri di hello utilizzati.</span><span class="sxs-lookup"><span data-stu-id="1d38b-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    <span data-ttu-id="1d38b-126">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="1d38b-126">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="1d38b-127">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="1d38b-127">**-n (or --name)**.</span></span> <span data-ttu-id="1d38b-128">Nome di hello toobe di gruppo di risorse creato.</span><span class="sxs-lookup"><span data-stu-id="1d38b-128">Name of hello resource group toobe created.</span></span>
   * <span data-ttu-id="1d38b-129">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="1d38b-129">**-l (or --location)**.</span></span> <span data-ttu-id="1d38b-130">Area di Azure in cui verrà creato il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="1d38b-130">Azure region where hello resource group will be created.</span></span>
   * <span data-ttu-id="1d38b-131">**-f (o --template-file)**.</span><span class="sxs-lookup"><span data-stu-id="1d38b-131">**-f (or --template-file)**.</span></span> <span data-ttu-id="1d38b-132">Percorso file di modello ARM tooyour.</span><span class="sxs-lookup"><span data-stu-id="1d38b-132">Path tooyour ARM template file.</span></span>
   * <span data-ttu-id="1d38b-133">**-e (o --parameters-file)**.</span><span class="sxs-lookup"><span data-stu-id="1d38b-133">**-e (or --parameters-file)**.</span></span> <span data-ttu-id="1d38b-134">File dei parametri di percorso tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="1d38b-134">Path tooyour ARM parameters file.</span></span>

