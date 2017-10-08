---
title: Appliance virtuale e routing aaaControl utilizzando hello Azure CLI 2.0 | Documenti Microsoft
description: Informazioni su come Appliance virtuale e routing toocontrol utilizzando hello CLI di Azure 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a>Creare le route definite dall'utente (UDR) utilizzando hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-create-udr-arm-cli.md)
> * [Modello](virtual-network-create-udr-arm-template.md)
> * [PowerShell (distribuzione classica)](virtual-network-create-udr-classic-ps.md)
> * [Interfaccia della riga di comando (distribuzione classica)](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI 

È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello: 

- [Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione 
- [Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale.


## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Creare hello UDR per subnet front-end hello
tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.

1. Creare una tabella di route per la subnet front-end hello con hello [-tabella di route az rete creare](/cli/azure/network/route-table#create) comando:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    Output:

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. Creare una route che invia tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) utilizzando hello [creare route della tabella di route di rete az](/cli/azure/network/route-table/route#create) comando:

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    Output:

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    Parametri

    * **--route-table-name**. Nome della tabella di routing hello in cui verrà aggiunti route hello. Per questo scenario, *UDR-FrontEnd*.
    * **--address-prefix**. Prefisso dell'indirizzo per subnet hello in cui i pacchetti sono destinati a. Per questo scenario, *192.168.2.0/24*.
    * **--next-hop-type**. Tipo di oggetto al quale verrà inviato il traffico. I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.
    * **--next-hop-ip-address**. Indirizzo IP per l'hop successivo. Per questo scenario, *192.168.0.4*.

3. Eseguire hello [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update) tabella di routing di comandi tooassociate hello creato in precedenza con hello **front-end** subnet:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    Output:

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    Parametri
    
    * **--vnet-name**. Nome della rete virtuale in cui si trova subnet hello hello. Per questo scenario, *TestVNet*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Creare hello UDR per subnet back-end hello

hello toocreate tabella di route e indirizzare necessari per la subnet di back-end hello a seconda dello scenario di hello sopra, hello completo alla procedura seguente:

1. Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a>Abilitare l'inoltro dell'indirizzo IP su FW1

inoltro dell'indirizzo IP nella scheda di rete utilizzata da hello tooenable **FW1**completa hello i passaggi seguenti:

1. Eseguire hello [Mostra scheda di rete az](/cli/azure/network/nic#show) comando con un hello toodisplay filtro JMESPATH corrente **inoltro dell'indirizzo ip enable** valore per **inoltro IP abilitare**. Deve essere impostato troppo*false*.

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    Output:

        false

2. Eseguire hello inoltro dell'indirizzo IP tooenable comando seguente:

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    È possibile esaminare console toohello con flusso di output hello, o semplicemente nuovamente per hello specifico **enableIpForwarding** valore:

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    Output:

        true

    Parametri

    **--ip-forwarding**: *true* o *false*.

