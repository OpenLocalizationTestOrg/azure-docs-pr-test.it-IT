---
title: Accessori aaaControl di routing e virtuali in Azure - modello | Documenti Microsoft
description: Informazioni su come Appliance virtuale e routing toocontrol utilizzando un modello di gestione risorse di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 832c7831-d0e9-449b-b39c-9a09ba051531
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: 781340593541784d2d9772d310c041ad4a5c3101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-a-template"></a><span data-ttu-id="cfe2c-103">Creare route definite dall'utente (UDR) mediante un modello</span><span class="sxs-lookup"><span data-stu-id="cfe2c-103">Create User-Defined Routes (UDR) using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cfe2c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfe2c-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="cfe2c-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="cfe2c-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="cfe2c-106">Modello</span><span class="sxs-lookup"><span data-stu-id="cfe2c-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="cfe2c-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="cfe2c-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="cfe2c-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="cfe2c-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

> [!IMPORTANT]
> <span data-ttu-id="cfe2c-109">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="cfe2c-110">È importante comprendere i [modelli e strumenti di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="cfe2c-111">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="cfe2c-112">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-112">This article covers hello Resource Manager deployment model.</span></span> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

## <a name="udr-resources-in-a-template-file"></a><span data-ttu-id="cfe2c-113">Risorse UDR in un file di modello</span><span class="sxs-lookup"><span data-stu-id="cfe2c-113">UDR resources in a template file</span></span>
<span data-ttu-id="cfe2c-114">È possibile visualizzare e scaricare hello [modello di esempio](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR).</span><span class="sxs-lookup"><span data-stu-id="cfe2c-114">You can view and download hello [sample template](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR).</span></span>

<span data-ttu-id="cfe2c-115">Hello nella sezione seguente viene illustrata hello definizione di hello UDR front-end in hello **azuredeploy-vnet-nsg-udr.json** file per uno scenario di hello:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-115">hello following section shows hello definition of hello front-end UDR in hello **azuredeploy-vnet-nsg-udr.json** file for hello scenario:</span></span>

    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/routeTables",
    "name": "[parameters('frontEndRouteTableName')]",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "UDR - FrontEnd"   
    },
    "properties": {
      "routes": [
        {
          "name": "RouteToBackEnd",
          "properties": {
            "addressPrefix": "[parameters('backEndSubnetPrefix')]",
            "nextHopType": "VirtualAppliance",
            "nextHopIpAddress": "[parameters('vmaIpAddress')]"
          }
        }
      ]

<span data-ttu-id="cfe2c-116">tooassociate hello UDR toohello front-end subnet, è la definizione di subnet hello toochange nel modello hello e utilizzare hello di id di riferimento per hello UDR.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-116">tooassociate hello UDR toohello front-end subnet, you have toochange hello subnet definition in hello template, and use hello reference id for hello UDR.</span></span>

    "subnets": [
        "name": "[parameters('frontEndSubnetName')]",
        "properties": {
          "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
          "networkSecurityGroup": {
            "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
          },
          "routeTable": {
              "id": "[resourceId('Microsoft.Network/routeTables', parameters('frontEndRouteTableName'))]"
          }
        },

<span data-ttu-id="cfe2c-117">Si noti hello stesso fatta per hello back-end NSG e hello subnet back-end nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-117">Notice hello same being done for hello back-end NSG and hello back-end subnet in hello template.</span></span>

<span data-ttu-id="cfe2c-118">È inoltre necessario tooensure tale hello **FW1** macchina virtuale è abilitata nella scheda di rete che verrà utilizzato tooreceive e inoltrare pacchetti hello di proprietà di inoltro dell'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-118">You also need tooensure that hello **FW1** VM has hello IP forwarding property enabled on hello NIC that will be used tooreceive and forward packets.</span></span> <span data-ttu-id="cfe2c-119">sezione Hello definizione hello Mostra di hello NIC per FW1 nel file azuredeploy-nsg-udr.json hello, a seconda dello scenario hello precedente.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-119">hello section below shows hello definition of hello NIC for FW1 in hello azuredeploy-nsg-udr.json file, based on hello scenario above.</span></span>

    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DMZ"
    },
    "name": "[concat(variables('fwVMSettings').nicName, copyindex(1))]",
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('fwVMSettings').pipName, copyindex(1))]",
      "[concat('Microsoft.Resources/deployments/', 'vnetTemplate')]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "enableIPForwarding": true,
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat('192.168.0.',copyindex(4))]",
            "publicIPAddress": {
              "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('fwVMSettings').pipName, copyindex(1)))]"
            },
            "subnet": {
              "id": "[variables('dmzSubnetRef')]"
            }
          }
        }
      ]
    },
    "copy": {
      "name": "fwniccount",
      "count": "[parameters('fwCount')]"
    }

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="cfe2c-120">Distribuire il modello di hello utilizzando fare clic su toodeploy</span><span class="sxs-lookup"><span data-stu-id="cfe2c-120">Deploy hello template by using click toodeploy</span></span>
<span data-ttu-id="cfe2c-121">modello di Hello esempio disponibile nel repository pubblico hello utilizza un file di parametro contenente hello predefiniti i valori utilizzati toogenerate hello lo scenario descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-121">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="cfe2c-122">toodeploy questo modello utilizzando fare clic su toodeploy, seguire [questo collegamento](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR), fare clic su **distribuire tooAzure**, sostituire i valori di parametro predefiniti hello se necessario e seguire le istruzioni di hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-122">toodeploy this template using click toodeploy, follow [this link](https://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

1. <span data-ttu-id="cfe2c-123">Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-123">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="cfe2c-124">Eseguire un gruppo di risorse di hello toocreate di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-124">Run hello following command toocreate a resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location westus
    ```

3. <span data-ttu-id="cfe2c-125">Eseguire hello modello hello toodeploy di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-125">Run hello following command toodeploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployUDR -ResourceGroupName TestRG `
        -TemplateUri https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json
    ```

    <span data-ttu-id="cfe2c-126">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-126">Expected output:</span></span>
   
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
                            ASFW                Microsoft.Compute/availabilitySets       westus  
                            ASSQL               Microsoft.Compute/availabilitySets       westus  
                            ASWEB               Microsoft.Compute/availabilitySets       westus  
                            FW1                 Microsoft.Compute/virtualMachines        westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            WEB1                Microsoft.Compute/virtualMachines        westus  
                            WEB2                Microsoft.Compute/virtualMachines        westus  
                            NICFW1              Microsoft.Network/networkInterfaces      westus  
                            NICSQL1             Microsoft.Network/networkInterfaces      westus  
                            NICSQL2             Microsoft.Network/networkInterfaces      westus  
                            NICWEB1             Microsoft.Network/networkInterfaces      westus  
                            NICWEB2             Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            PIPFW1              Microsoft.Network/publicIPAddresses      westus  
                            PIPSQL1             Microsoft.Network/publicIPAddresses      westus  
                            PIPSQL2             Microsoft.Network/publicIPAddresses      westus  
                            PIPWEB1             Microsoft.Network/publicIPAddresses      westus  
                            PIPWEB2             Microsoft.Network/publicIPAddresses      westus  
                            UDR-BackEnd         Microsoft.Network/routeTables            westus  
                            UDR-FrontEnd        Microsoft.Network/routeTables            westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus

        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="cfe2c-127">Distribuire il modello di hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="cfe2c-127">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="cfe2c-128">modello ARM toodeploy hello utilizzando hello CLI di Azure, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-128">toodeploy hello ARM template by using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="cfe2c-129">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-129">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="cfe2c-130">Eseguire hello seguenti modalità di gestione tooResource tooswitch comando:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-130">Run hello following command tooswitch tooResource Manager mode:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="cfe2c-131">Ecco l'output di hello previsto per comando hello sopra indicato:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-131">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="cfe2c-132">Dal browser, passare troppo**https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json**, copiare il contenuto di hello del file json hello e incollare in un nuovo file il computer.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-132">From your browser, navigate too**https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.parameters.json**, copy hello contents of hello json file, and paste into a new file in your computer.</span></span> <span data-ttu-id="cfe2c-133">Per questo scenario, si sarebbero copiando i valori hello sotto tooa file denominato **c:\udr\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-133">For this scenario, you would be copying hello values below tooa file named **c:\udr\azuredeploy.parameters.json**.</span></span>

    ```json
        {
          "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "fwCount": {
              "value": 1
            },
            "webCount": {
              "value": 2
            },
            "sqlCount": {
              "value": 2
            }
          }
        }
    ```

4. <span data-ttu-id="cfe2c-134">Eseguire hello toodeploy hello nuova rete virtuale tramite i file modello/parametro hello è stato scaricato e modificato di sopra di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-134">Run hello following command toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above:</span></span>

    ```azurecli
    azure group create -n TestRG -l westus --template-uri 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/IaaS-NSG-UDR/azuredeploy.json' -e 'c:\udr\azuredeploy.parameters.json'
    ```

    <span data-ttu-id="cfe2c-135">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-135">Expected output:</span></span>
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Updating resource group TestRG
        info:    Updated resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription Id]/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK

5. <span data-ttu-id="cfe2c-136">Eseguire hello seguendo le risorse di hello tooview comando create nel nuovo gruppo di risorse hello:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-136">Run hello following command tooview hello resources created in hello new resource group:</span></span>

    ```azurecli
    azure group show TestRG
    ```

    <span data-ttu-id="cfe2c-137">Risultato previsto:</span><span class="sxs-lookup"><span data-stu-id="cfe2c-137">Expected result:</span></span>

            info:    Executing command group show
            info:    Listing resource groups
            info:    Listing resources for hello group
            data:    Id:                  /subscriptions/[Subscription Id]/resourceGroups/TestRG
            data:    Name:                TestRG
            data:    Location:            westus
            data:    Provisioning State:  Succeeded
            data:    Tags: null
            data:    Resources:
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASFW
            data:      Name    : ASFW
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASSQL
            data:      Name    : ASSQL
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/availabilitySets/ASWEB
            data:      Name    : ASWEB
            data:      Type    : availabilitySets
            data:      Location: westus
            data:      Tags    : displayName=AvailabilitySet - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1
            data:      Name    : FW1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/SQL1
            data:      Name    : SQL1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/SQL2
            data:      Name    : SQL2
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WEB1
            data:      Name    : WEB1
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WEB2
            data:      Name    : WEB2
            data:      Type    : virtualMachines
            data:      Location: westus
            data:      Tags    : displayName=VMs - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
                data:      Name    : NICFW1
        data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1
            data:      Name    : NICSQL1
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2
            data:      Name    : NICSQL2
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1
            data:      Name    : NICWEB1
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2
            data:      Name    : NICWEB2
            data:      Type    : networkInterfaces
            data:      Location: westus
            data:      Tags    : displayName=NetworkInterfaces - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd
            data:      Name    : NSG-BackEnd
            data:      Type    : networkSecurityGroups
            data:      Location: westus
            data:      Tags    : displayName=NSG - Front End
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
            data:      Name    : NSG-FrontEnd
            data:      Type    : networkSecurityGroups
            data:      Location: westus
            data:      Tags    : displayName=NSG - Remote Access
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1
            data:      Name    : PIPFW1
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - DMZ
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPSQL1
            data:      Name    : PIPSQL1
                data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPSQL2
            data:      Name    : PIPSQL2
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - SQL
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPWEB1
            data:      Name    : PIPWEB1
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPWEB2
            data:      Name    : PIPWEB2
            data:      Type    : publicIPAddresses
            data:      Location: westus
            data:      Tags    : displayName=PublicIPAddresses - Web
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd
            data:      Name    : UDR-BackEnd
            data:      Type    : routeTables
            data:      Location: westus
            data:      Tags    : displayName=Route Table - Back End
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd
            data:      Name    : UDR-FrontEnd
            data:      Type    : routeTables
            data:      Location: westus
            data:      Tags    : displayName=UDR - FrontEnd
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
            data:      Name    : TestVNet
            data:      Type    : virtualNetworks
            data:      Location: westus
            data:      Tags    : displayName=VNet
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Storage/storageAccounts/testvnetstorageprm
            data:      Name    : testvnetstorageprm
            data:      Type    : storageAccounts
            data:      Location: westus
            data:      Tags    : displayName=Storage Account - Premium
            data:    
            data:      Id      : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Storage/storageAccounts/testvnetstoragestd
            data:      Name    : testvnetstoragestd
            data:      Type    : storageAccounts
            data:      Location: westus
            data:      Tags    : displayName=Storage Account - Simple
            data:    
            data:    Permissions:
            data:      Actions: *
            data:      NotActions: 
            data:
            info:    group show command OK

> [!TIP]
> <span data-ttu-id="cfe2c-138">Se non è possibile visualizzare tutte le risorse di hello, eseguire hello `azure group deployment show` comando tooensure hello lo stato della distribuzione hello di provisioning è *riuscita*.</span><span class="sxs-lookup"><span data-stu-id="cfe2c-138">If you do not see all hello resources, run hello `azure group deployment show` command tooensure hello provisioning state of hello deployment is *Succeded*.</span></span>
> 
