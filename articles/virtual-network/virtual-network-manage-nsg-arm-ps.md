---
title: -i gruppi di sicurezza di rete aaaManage Azure PowerShell | Documenti Microsoft
description: Informazioni su come toomanage rete gruppi di sicurezza tramite PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a>Gestire i gruppi di sicurezza di rete mediante PowerShell

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a>Recuperare le informazioni
È possibile visualizzare i gruppi di sicurezza di rete (NSG, Network Security Group) esistenti, recuperare le regole relative a un NSG esistente e trovare le risorse a cui un NSG è associato.

### <a name="view-existing-nsgs"></a>Visualizzare NSG esistenti
tooview tutti NSGs esistente in una sottoscrizione, eseguire hello `Get-AzureRmNetworkSecurityGroup` cmdlet.

Risultato previsto:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


elenco di hello tooview di NSGs in un gruppo di risorse specifico, eseguire hello `Get-AzureRmNetworkSecurityGroup` cmdlet.

Output previsto:

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a>Elencare tutte le regole per un NSG
le regole di hello tooview di un gruppo denominato **front-end di NSG**, immettere hello comando seguente:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

Output previsto:

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> È inoltre possibile utilizzare `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` regole predefinite di hello toolist da hello **front-end di NSG** gruppo.
> 

### <a name="view-nsgs-associations"></a>Visualizzare le associazioni di NSG
tooview hello quali risorse **front-end di NSG** NSG è associato alla, hello esecuzione comando riportato di seguito:

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

Cercare hello **NetworkInterfaces** e **subnet** proprietà come illustrato di seguito:

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

Nell'esempio precedente hello hello gruppo non è associato tooany interfacce di rete (NIC); è associato tooa subnet denominata **front-end**.

## <a name="manage-rules"></a>Gestire le regole
È possibile aggiungere regole tooan gruppo esistente, modificare le regole esistenti e rimuovere le regole.

### <a name="add-a-rule"></a>Aggiungere una regola
tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, hello completo alla procedura seguente:

1. Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Eseguire hello successivo comando tooadd toohello una regola gruppo:

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello modifiche toohello NSG, eseguire hello comando seguente:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    Output previsto con hello solo le regole di sicurezza:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a>Modificare una regola
regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** solo, seguire i passaggi di hello riportati di seguito.

1. Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Eseguire hello comando con le nuove impostazioni regola hello seguente:

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. toosave hello modifiche toohello NSG, eseguire hello comando seguente:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Output previsto con hello solo le regole di sicurezza:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a>Eliminare una regola
1. Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Comando che segue di hello esecuzione regola hello tooremove da hello gruppo:

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. Salvare le modifiche apportate di hello toohello NSG, eseguendo hello comando seguente:

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    Output previsto con hello solo regole di sicurezza, si noti hello **regola https** non viene più elencata:
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a>Gestire le associazioni
È possibile associare un gruppo toosubnets e schede di rete. È anche possibile annullare l'associazione tra un NSG e qualsiasi risorsa a cui è associato.

### <a name="associate-an-nsg-tooa-nic"></a>Associare un tooa gruppo NIC
hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, hello completo alla procedura seguente:

1. Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. Eseguire hello successivo comando tooretrieve hello esistente NIC e archiviarlo in una variabile:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. Set hello **sicurezza di rete** proprietà di hello **NIC** valore variabile toohello hello **NSG** variabile, immettendo hello comando seguente:

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. toosave hello modifiche toohello NIC, eseguire hello comando seguente:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Hello solo di output previsto con **sicurezza di rete** proprietà:
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a>Annullare l'associazione tra un NSG e una NIC
hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, hello completo alla procedura seguente:

1. Eseguire hello successivo comando tooretrieve hello esistente NIC e archiviarlo in una variabile:

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. Set hello **sicurezza di rete** proprietà di hello **NIC** variabile troppo**$null** eseguendo hello comando seguente:

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. toosave hello modifiche toohello NIC, eseguire hello comando seguente:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    Hello solo di output previsto con **sicurezza di rete** proprietà:
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a>Annullare l'associazione tra un NSG e una subnet
hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, hello completo alla procedura seguente:

1. Eseguire hello successivo comando tooretrieve hello esistente di rete virtuale e archiviarla in una variabile:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Esecuzione hello seguenti comando tooretrieve hello **front-end** subnet e archiviarlo in una variabile:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Set hello **sicurezza di rete** proprietà di hello **subnet** variabile troppo**$null** immettendo hello comando seguente:

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. toosave hello modifiche toohello subnet, eseguire hello comando seguente:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Output previsto mostrando solo le proprietà di hello di hello **front-end** subnet. Si noti che non esiste una proprietà per **NetworkSecurityGroup**:
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a>Associare una subnet tooa NSG
hello tooassociate **front-end di NSG** NSG toohello **FronEnd** subnet nuovamente, hello completo alla procedura seguente:

1. Eseguire hello successivo comando tooretrieve hello esistente di rete virtuale e archiviarla in una variabile:

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. Esecuzione hello seguenti comando tooretrieve hello **front-end** subnet e archiviarlo in una variabile:

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. Eseguire hello successivo comando tooretrieve hello gruppo esistente e archiviarlo in una variabile:

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. Set hello **sicurezza di rete** proprietà di hello **subnet** variabile troppo**$null** eseguendo hello comando seguente:

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. toosave hello modifiche toohello subnet, eseguire hello comando seguente:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    Hello solo di output previsto con **sicurezza di rete** proprietà di hello **front-end** subnet:
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a>Eliminare un gruppo di sicurezza di rete
È possibile eliminare un gruppo solo se non è associata la risorsa tooany. un gruppo, toodelete procedura hello riportata di seguito.

1. risorse di hello toocheck associati tooan NSG, eseguire hello `azure network nsg show` come illustrato nella [NSGs visualizzazione associazioni](#View-NSGs-associations).
2. Se hello NSG è associato tooany schede di rete, eseguire hello `azure network nic set` come illustrato nella [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC) per ogni scheda di rete. 
3. Se hello gruppo subnet tooany associate, eseguire hello `azure network vnet subnet set` come illustrato nella [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet) per ogni subnet.
4. hello toodelete NSG, eseguire hello comando seguente:

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > Hello `-Force` parametro assicura che non è necessario l'eliminazione di hello tooconfirm.
   > 

## <a name="next-steps"></a>Passaggi successivi
* [Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.

