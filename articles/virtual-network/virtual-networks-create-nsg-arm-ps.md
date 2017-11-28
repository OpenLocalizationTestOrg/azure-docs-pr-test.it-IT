---
title: Creare gruppi di sicurezza di rete - Azure PowerShell | Documentazione Microsoft
description: Informazioni su come creare e distribuire i gruppi di sicurezza di rete mediante PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 26fe67b43d63c6685d8ae7644dd7df6931a4d2a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="0d2dd-103">Creare gruppi di sicurezza di rete mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d2dd-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="0d2dd-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0d2dd-105">Microsoft consiglia di creare le risorse tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="0d2dd-106">Per altre informazioni sulle differenze tra i due modelli, leggere l'articolo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="0d2dd-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="0d2dd-107">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="0d2dd-108">È anche possibile creare gruppi di sicurezza di rete con il [modello di distribuzione classica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0d2dd-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="0d2dd-109">I comandi di esempio PowerShell riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="0d2dd-110">Se si desidera eseguire i comandi così come sono visualizzati in questo documento, creare innanzitutto l'ambiente di test distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), fare clic su **Distribuisci in Azure**, sostituire i valori di parametro predefiniti, se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="0d2dd-111">Come creare il gruppo di sicurezza di rete per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="0d2dd-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="0d2dd-112">Per creare un gruppo di sicurezza di rete denominato *NSG-FrontEnd* in base allo scenario, seguire la procedura riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="0d2dd-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="0d2dd-113">Se è la prima volta che si utilizza Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni fino al termine della procedura per accedere ad Azure e selezionare la sottoscrizione desiderata.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="0d2dd-114">Creare una regola di sicurezza che consente l'accesso alla porta 3389 da Internet.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-114">Create a security rule allowing access from the Internet to port 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="0d2dd-115">Creare una regola di sicurezza che consente l'accesso da Internet alla porta 80.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-115">Create a security rule allowing access from the Internet to port 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="0d2dd-116">Aggiungere le regole create in precedenza a un nuovo gruppo di sicurezza di rete denominato **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="0d2dd-117">Selezionare le regole create nel gruppo di sicurezza di rete digitando:</span><span class="sxs-lookup"><span data-stu-id="0d2dd-117">Check the rules created in the NSG by typing the following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="0d2dd-118">L'output che mostra solo le regole di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="0d2dd-118">Output showing just the security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="0d2dd-119">Associare il gruppo di sicurezza di rete creato in precedenza per la subnet *front-end* .</span><span class="sxs-lookup"><span data-stu-id="0d2dd-119">Associate the NSG created above to the *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="0d2dd-120">Output che mostra solo le impostazioni della subnet *FrontEnd* , notare il valore per la proprietà **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="0d2dd-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="0d2dd-121">L'output per il comando precedente mostra il contenuto per l'oggetto di configurazione della rete virtuale, che esiste solo nei computer in cui si esegue PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="0d2dd-122">È necessario eseguire il cmdlet `Set-AzureRmVirtualNetwork` per salvare queste impostazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span></span>
   > 
   > 
7. <span data-ttu-id="0d2dd-123">Salvare le nuove impostazioni di rete virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-123">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="0d2dd-124">L'output che mostra solo la parte NSG:</span><span class="sxs-lookup"><span data-stu-id="0d2dd-124">Output showing just the NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="0d2dd-125">Come creare il gruppo di sicurezza di rete per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="0d2dd-125">How to create the NSG for the back-end subnet</span></span>
<span data-ttu-id="0d2dd-126">Per creare un gruppo di sicurezza di rete denominato *NSG-BackEnd* in base allo scenario precedente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0d2dd-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="0d2dd-127">Creare una regola di sicurezza che consente l'accesso dalla subnet front-end per la porta 1433 (porta predefinita usata da SQL Server).</span><span class="sxs-lookup"><span data-stu-id="0d2dd-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="0d2dd-128">Creare una regola di sicurezza che blocca l'accesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-128">Create a security rule blocking access to the Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="0d2dd-129">Aggiungere le regole create in precedenza a un nuovo gruppo di sicurezza di rete denominato **NSG-BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="0d2dd-130">Associare il gruppo di sicurezza di rete creato in precedenza per la subnet *BackEnd* .</span><span class="sxs-lookup"><span data-stu-id="0d2dd-130">Associate the NSG created above to the *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="0d2dd-131">Output che mostra solo le impostazioni della subnet *BackEnd* , notare il valore per la proprietà **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="0d2dd-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="0d2dd-132">Salvare le nuove impostazioni di rete virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-132">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-to-remove-an-nsg"></a><span data-ttu-id="0d2dd-133">Come rimuovere un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="0d2dd-133">How to remove an NSG</span></span>
<span data-ttu-id="0d2dd-134">Per eliminare un gruppo di sicurezza di rete esistente, denominato *NSG-Frontend* in questo caso, attenersi a questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0d2dd-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span></span>

<span data-ttu-id="0d2dd-135">Eseguire il comando **Remove- AzureRmNetworkSecurityGroup** illustrato di seguito e assicurarsi di includere il gruppo di risorse in cui si trova il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="0d2dd-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

