---
title: -i gruppi di sicurezza di rete aaaCreate Azure PowerShell | Documenti Microsoft
description: Informazioni su come toocreate e distribuire i gruppi di sicurezza di rete con PowerShell.
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
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="1f3cd-103">Creare gruppi di sicurezza di rete mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f3cd-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="1f3cd-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1f3cd-105">Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="1f3cd-106">altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="1f3cd-107">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="1f3cd-108">È anche possibile [creare NSGs nel modello di distribuzione classica hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="1f3cd-109">esempio Hello PowerShell comandi riportati di seguito prevedono un ambiente semplice già creato in base hello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="1f3cd-110">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="1f3cd-111">Come toocreate hello NSG per hello subnet front-end</span><span class="sxs-lookup"><span data-stu-id="1f3cd-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="1f3cd-112">un gruppo denominato toocreate *front-end di NSG* a seconda dello scenario di hello, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="1f3cd-113">Se non si è mai usato Azure PowerShell, vedere [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) e seguire le istruzioni di hello tutti hello modo toohello terminare toosign in Azure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="1f3cd-114">Creare una regola di sicurezza che consente l'accesso da hello Internet tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="1f3cd-115">Creare una regola di sicurezza che consente l'accesso da hello Internet tooport 80.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="1f3cd-116">Aggiungere regole hello create in precedenza tooa nuovo gruppo denominato **front-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="1f3cd-117">Controllare le regole di hello create nel gruppo hello digitando hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="1f3cd-118">Le regole di sicurezza solo hello che mostra l'output:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-118">Output showing just hello security rules:</span></span>
   
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
6. <span data-ttu-id="1f3cd-119">Associare hello gruppo creato in precedenza toohello *front-end* subnet.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="1f3cd-120">Hello solo di output che mostra *front-end* impostazioni subnet, valore hello informativa per hello **sicurezza di rete** proprietà:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
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
   > <span data-ttu-id="1f3cd-121">output di Hello per comando hello precedente mostra il contenuto di hello per l'oggetto configurazione di rete virtuale di hello che esiste solo nel computer di hello in cui si esegue PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="1f3cd-122">È necessario hello toorun `Set-AzureRmVirtualNetwork` toosave cmdlet tooAzure queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="1f3cd-123">Salvare hello nuovo tooAzure le impostazioni di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="1f3cd-124">L'output che mostra solo parte NSG hello:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="1f3cd-125">Come toocreate hello gruppo per le subnet di back-end hello</span><span class="sxs-lookup"><span data-stu-id="1f3cd-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="1f3cd-126">un gruppo denominato toocreate *back-end di NSG* a seconda dello scenario hello precedente, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="1f3cd-127">Creare una regola di sicurezza che consente l'accesso da hello subnet front-end tooport 1433 (porta predefinita utilizzata da SQL Server).</span><span class="sxs-lookup"><span data-stu-id="1f3cd-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="1f3cd-128">Creare una regola di sicurezza blocco toohello accesso Internet.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="1f3cd-129">Aggiungere regole hello create in precedenza tooa nuovo gruppo denominato **back-end di NSG**.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="1f3cd-130">Associare hello gruppo creato in precedenza toohello *back-end* subnet.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="1f3cd-131">Hello solo di output che mostra *back-end* impostazioni subnet, valore hello informativa per hello **sicurezza di rete** proprietà:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
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
5. <span data-ttu-id="1f3cd-132">Salvare hello nuovo tooAzure le impostazioni di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="1f3cd-133">Come tooremove un gruppo</span><span class="sxs-lookup"><span data-stu-id="1f3cd-133">How tooremove an NSG</span></span>
<span data-ttu-id="1f3cd-134">toodelete un gruppo esistente, denominata *front-end di NSG* in questo caso, attenersi alla seguente passaggio hello:</span><span class="sxs-lookup"><span data-stu-id="1f3cd-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="1f3cd-135">Eseguire hello **Remove AzureRmNetworkSecurityGroup** illustrato di seguito e che hello di gruppo di risorse hello, tooinclude gruppo si trova in.</span><span class="sxs-lookup"><span data-stu-id="1f3cd-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

