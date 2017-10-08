---
title: -i gruppi di sicurezza di rete aaaManage 2.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come gruppi di sicurezza di rete toomanage utilizzando hello Azure interfaccia della riga di comando (CLI) 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed17d314-07e6-4c7f-bcf1-a8a2535d7c14
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3036b465e1e4049cba00e5e13ce1b479a2301d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-20"></a>Gestire gruppi di sicurezza di rete utilizzando hello Azure CLI 2.0

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI 

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello: 

- [Azure CLI 1.0](virtual-network-manage-nsg-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione 
- [Azure CLI 2.0](#View-existing-NSGs) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)


[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo di modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché il modello di distribuzione classica hello.
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="prerequisite"></a>Prerequisito
Se non hai ancora, installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login). 


## <a name="view-existing-nsgs"></a>Visualizzare NSG esistenti
elenco di hello tooview di NSGs in un gruppo di risorse specifico, eseguire hello [elenco gruppo di rete az](/cli/azure/network/nsg#list) comando con un `-o table` formato di output:

```azurecli
az network nsg list -g RG-NSG -o table
```

Output previsto:

    Location    Name          ProvisioningState    ResourceGroup    ResourceGuid
    ----------  ------------  -------------------  ---------------  ------------------------------------
    centralus   NSG-BackEnd   Succeeded            RG-NSG           <guid>
    centralus   NSG-FrontEnd  Succeeded            RG-NSG           <guid>

## <a name="list-all-rules-for-an-nsg"></a>Elencare tutte le regole per un NSG
le regole di hello tooview di un gruppo denominato **front-end di NSG**hello eseguire [Mostra nsg di rete az](/cli/azure/network/nsg#show) comando mediante un [filtro query JMESPATH](/cli/azure/query-az-cli2) hello e `-o table` formato di output:

```azurecli
    az network nsg show \
    --resource-group RG-NSG \
    --name NSG-FrontEnd \
    --query '[defaultSecurityRules[],securityRules[]][].{Name:name,Desc:description,Access:access,Direction:direction,DestPortRange:destinationPortRange,DestAddrPrefix:destinationAddressPrefix,SrcPortRange:sourcePortRange,SrcAddrPrefix:sourceAddressPrefix}' \
    -o table
```

Output previsto:

    Name                           Desc                                                    Access    Direction    DestPortRange    DestAddrPrefix    SrcPortRange    SrcAddrPrefix
    -----------------------------  ------------------------------------------------------  --------  -----------  ---------------  ----------------  --------------  -----------------
    AllowVnetInBound               Allow inbound traffic from all VMs in VNET              Allow     Inbound      *                VirtualNetwork    *               VirtualNetwork
    AllowAzureLoadBalancerInBound  Allow inbound traffic from azure load balancer          Allow     Inbound      *                *                 *               AzureLoadBalancer
    DenyAllInBound                 Deny all inbound traffic                                Deny      Inbound      *                *                 *               *
    AllowVnetOutBound              Allow outbound traffic from all VMs tooall VMs in VNET  Allow     Outbound     *                VirtualNetwork    *               VirtualNetwork
    AllowInternetOutBound          Allow outbound traffic from all VMs tooInternet         Allow     Outbound     *                Internet          *               *
    DenyAllOutBound                Deny all outbound traffic                               Deny      Outbound     *                *                 *               *
    rdp-rule                                                                               Allow     Inbound      3389             *                 *               Internet
    web-rule                                                                               Allow     Inbound      80               *                 *               Internet
> [!NOTE]
> È inoltre possibile utilizzare [elenco delle regole az rete nsg](/cli/azure/network/nsg/rule#list) toolist solo hello regole personalizzate di un gruppo.
>

## <a name="view-nsg-associations"></a>Visualizzare le associazioni di NSG

tooview hello quali risorse **front-end di NSG** NSG è associato alla, eseguire hello `az network nsg show` comando come illustrato di seguito. 

```azurecli
az network nsg show -g RG-NSG -n nsg-frontend --query '[subnets,networkInterfaces]'
```

Cercare hello **networkInterfaces** e **subnet** proprietà come illustrato di seguito:

```json
[
  [
    {
      "addressPrefix": null,
      "etag": null,
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
      "ipConfigurations": null,
      "name": null,
      "networkSecurityGroup": null,
      "provisioningState": null,
      "resourceGroup": "RG-NSG",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  null
]
```

Nell'esempio hello sopra, hello gruppo non è associata tooany interfacce di rete (NIC) ed è associato tooa subnet denominata **front-end**.

## <a name="add-a-rule"></a>Aggiungere una regola
tooadd una regola che concede **in ingresso** traffico tooport **443** da qualsiasi toohello macchina **front-end di NSG** NSG, immettere hello comando seguente:

```azurecli
az network nsg rule create  \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd  \
--name allow-https \
--description "Allow access tooport 443 for HTTPS" \
--access Allow \
--protocol Tcp  \
--direction Inbound \
--priority 102 \
--source-address-prefix "*"  \
--source-port-range "*"  \
--destination-address-prefix "*" \
--destination-port-range "443"
```

Output previsto:

```json
{
  "access": "Allow",
  "description": "Allow access tooport 443 for HTTPS",
  "destinationAddressPrefix": "*",
  "destinationPortRange": "443",
  "direction": "Inbound",
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
  "name": "allow-https",
  "priority": 102,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

## <a name="change-a-rule"></a>Modificare una regola
regola di hello toochange creato in precedenza tooallow il traffico da hello in ingresso **Internet** solo eseguire hello [aggiornamento regola gruppo di rete az](/cli/azure/network/nsg/rule#update) comando:

```azurecli
az network nsg rule update \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https \
--source-address-prefix Internet
```

Output previsto:

```json
{
"access": "Allow",
"description": "Allow access tooport 443 for HTTPS",
"destinationAddressPrefix": "*",
"destinationPortRange": "443",
"direction": "Inbound",
"etag": "W/\"<guid>\"",
"id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https",
"name": "allow-https",
"priority": 102,
"protocol": "Tcp",
"provisioningState": "Succeeded",
"resourceGroup": "RG-NSG",
"sourceAddressPrefix": "Internet",
"sourcePortRange": "*"
}
```

## <a name="delete-a-rule"></a>Eliminare una regola
regola di hello toodelete creato in precedenza, eseguire hello comando seguente:

```azurecli
az network nsg rule delete \
--resource-group RG-NSG \
--nsg-name NSG-FrontEnd \
--name allow-https
```


## <a name="associate-an-nsg-tooa-nic"></a>Associare un tooa gruppo NIC
hello tooassociate **front-end di NSG** NSG toohello **TestNICWeb1** NIC, utilizzare hello [aggiornamento nic di rete az](/cli/azure/network/nic#update) comando:

```azurecli
az network nic update \
--resource-group RG-NSG \
--name TestNICWeb1 \
--network-security-group NSG-FrontEnd    
```

Output previsto:

```json
{
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": [],
    "internalDnsNameLabel": null,
    "internalDomainNameSuffix": "k0wkaguidnqrh0ud.gx.internal.cloudapp.net",
    "internalFqdn": null
  },
  "enableAcceleratedNetworking": false,
  "enableIpForwarding": false,
  "etag": "W/\"<guid>\"",
  "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1",
  "ipConfigurations": [
    {
      "applicationGatewayBackendAddressPools": null,
      "etag": "W/\"<guid>\"",
      "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1",
      "loadBalancerBackendAddressPools": null,
      "loadBalancerInboundNatRules": null,
      "name": "ipconfig1",
      "primary": true,
      "privateIpAddress": "192.168.1.6",
      "privateIpAddressVersion": "IPv4",
      "privateIpAllocationMethod": "Static",
      "provisioningState": "Succeeded",
      "publicIpAddress": null,
      "resourceGroup": "RG-NSG",
      "subnet": {
        "addressPrefix": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
        "ipConfigurations": null,
        "name": null,
        "networkSecurityGroup": null,
        "provisioningState": null,
        "resourceGroup": "RG-NSG",
        "resourceNavigationLinks": null,
        "routeTable": null
      }
    }
  ],
  "location": "centralus",
  "macAddress": "00-0D-3A-91-A9-60",
  "name": "TestNICWeb1",
  "networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/<guid>/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  },
  "primary": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "RG-NSG",
  "resourceGuid": "<guid>",
  "tags": {},
  "type": "Microsoft.Network/networkInterfaces",
  "virtualMachine": null
}
```

## <a name="dissociate-an-nsg-from-a-nic"></a>Annullare l'associazione tra un NSG e una NIC

hello toodissociate **front-end di NSG** NSG da hello **TestNICWeb1** NIC, eseguire hello [aggiornamento regola gruppo di rete az](/cli/azure/network/nsg/rule#update) comando nuovamente ma sostituire hello `--network-security-group` argomento con una stringa vuota (`""`).

```azurecli
az network nic update --resource-group RG-NSG --name TestNICWeb3 --network-security-group ""
```

Nell'output di hello hello `networkSecurityGroup` chiave toonull è impostata.

## <a name="dissociate-an-nsg-from-a-subnet"></a>Annullare l'associazione tra un NSG e una subnet
hello toodissociate **front-end di NSG** NSG da hello **front-end** subnet, eseguire di nuovo hello [aggiornamento regola gruppo di rete az](/cli/azure/network/nsg/rule#update) comando nuovamente ma sostituire hello `--network-security-group` argomento con una stringa vuota (`""`).

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group ""
```

Nell'output di hello hello `networkSecurityGroup` chiave toonull è impostata.

## <a name="associate-an-nsg-tooa-subnet"></a>Associare una subnet tooa NSG
hello tooassociate **front-end di NSG** NSG toohello **front-end** subnet eseguito nuovamente, hello comando seguente:

```azurecli
az network vnet subnet update \
--resource-group RG-NSG \
--vnet-name testvnet \
--name FrontEnd \
--network-security-group NSG-FrontEnd
```

Nell'output di hello hello `networkSecurityGroup` chiave ha un comportamento simile per valore hello:

```json
"networkSecurityGroup": {
    "defaultSecurityRules": null,
    "etag": null,
    "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
    "location": null,
    "name": null,
    "networkInterfaces": null,
    "provisioningState": null,
    "resourceGroup": "RG-NSG",
    "resourceGuid": null,
    "securityRules": null,
    "subnets": null,
    "tags": null,
    "type": null
  }
  ```

## <a name="delete-an-nsg"></a>Eliminare un gruppo di sicurezza di rete
È possibile eliminare un gruppo solo se non è associata la risorsa tooany. un gruppo, toodelete procedura hello riportata di seguito.

1. risorse di hello toocheck associati tooan NSG, eseguire hello `azure network nsg show` come illustrato nella [NSGs visualizzazione associazioni](#View-NSGs-associations).
2. Se hello NSG è associato tooany schede di rete, eseguire hello `azure network nic set` come illustrato nella [annullare l'associazione di un gruppo da una scheda di rete](#Dissociate-an-NSG-from-a-NIC) per ogni scheda di rete. 
3. Se hello gruppo subnet tooany associate, eseguire hello `azure network vnet subnet set` come illustrato nella [annullare l'associazione di un gruppo da una subnet](#Dissociate-an-NSG-from-a-subnet) per ogni subnet.
4. hello toodelete NSG, eseguire hello comando seguente:

    ```azurecli
    az network nsg delete --resource-group RG-NSG --name NSG-FrontEnd
    ```
## <a name="next-steps"></a>Passaggi successivi
* [Abilitare la registrazione](virtual-network-nsg-manage-log.md) per gli NSG.

