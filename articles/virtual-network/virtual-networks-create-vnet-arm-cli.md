---
title: una rete virtuale - CLI di Azure 2.0 aaaCreate | Documenti Microsoft
description: Informazioni su come una rete virtuale utilizzando toocreate hello CLI di Azure 2.0.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Creare una rete virtuale usando hello Azure CLI 2.0

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica. Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello. altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione
- [Azure CLI 2.0](#create-a-virtual-network) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)'
 
    È anche possibile creare una rete virtuale tramite Gestione risorse di usare altri strumenti o creare una rete virtuale tramite il modello di distribuzione classica hello selezionando un'opzione diversa da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Modello](virtual-networks-create-vnet-arm-template-click.md)
> * [Portale (versione classica)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (versione classica)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [Interfaccia della riga di comando (versione classica)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Crea rete virtuale

una rete virtuale utilizzando toocreate hello CLI di Azure 2.0, hello completo alla procedura seguente:

1. Installare e configurare più recente hello [CLI di Azure 2.0](/cli/azure/install-az-cli2) e accedere con un account Azure tooan [accesso az](/cli/azure/#login).

2. Creare un gruppo di risorse per una rete virtuale usando hello [gruppo az creare](/cli/azure/group#create) con hello `--name` e `--location` argomenti:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. Creare una rete virtuale e subnet:

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Output previsto:
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    Parametri utilizzati:

    - `--name TestVNet`: Nome di hello toobe di rete virtuale creata.
    - `--resource-group TestRG`: # hello Nome gruppo di risorse che controlla la risorsa hello. 
    - `--location centralus`: posizione in cui toodeploy hello.
    - `--address-prefix 192.168.0.0/16`: hello prefisso dell'indirizzo e blocco.  
    - `--subnet-name FrontEnd`: nome hello della subnet di hello.
    - `--subnet-prefix 192.168.1.0/24`: hello prefisso dell'indirizzo e blocco.

    toouse di informazioni di base toolist hello in hello successivo comando, è possibile eseguire query tramite rete virtuale hello un [filtro query](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Che produce hello seguente output:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Creare una subnet:

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Output previsto:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    Parametri utilizzati:

    - `--address-prefix 192.168.2.0/24`: blocco CIDR della subnet.
    - `--name BackEnd`: Nome della nuova subnet hello.
    - `--resource-group TestRG`: il gruppo di risorse hello.
    - `--vnet-name TestVNet`: nome hello di hello proprietario rete virtuale.

5. Proprietà hello query di hello nuova rete virtuale:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Output previsto:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Eseguire query su proprietà hello di subnet hello:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Output previsto:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooconnect:

- Una rete virtuale tooa di macchina virtuale (VM) leggendo hello [creare una VM Linux](../virtual-machines/linux/quick-create-cli.md) articolo. Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.
- Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) articolo.
- rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute. Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
