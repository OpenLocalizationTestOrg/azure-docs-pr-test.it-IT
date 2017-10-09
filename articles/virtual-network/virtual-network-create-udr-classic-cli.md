---
title: routing aaaControl classica una rete virtuale di Azure - CLI - | Documenti Microsoft
description: Informazioni su come toocontrol routing in reti virtuali mediante hello CLI di Azure nel modello di distribuzione classica hello
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a>Routing di controllo e l'utilizzo di dispositivi virtuali (classici) utilizzare hello CLI di Azure

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-create-udr-arm-cli.md)
> * [Modello](virtual-network-create-udr-arm-template.md)
> * [PowerShell (versione classica)](virtual-network-create-udr-classic-ps.md)
> * [Interfaccia della riga di comando (versione classica)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [controllare il routing e utilizzare i dispositivi di rete nel modello di distribuzione di gestione risorse di hello](virtual-network-create-udr-arm-cli.md).

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare nell'ambiente di hello [creare una rete virtuale (classico) mediante Azure CLI hello](virtual-networks-create-vnet-classic-cli.md).

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Creare hello UDR per subnet front-end hello
tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.

1. Eseguire hello modalità tooclassic tooswitch dei comandi seguenti:

    ```azurecli
    azure config mode asm
    ```

    Output:

        info:    New mode is asm

2. Eseguire hello successivo comando toocreate una tabella di route per la subnet front-end hello:

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    Output:
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    Parametri
   
   * **-l (o --location)**. Area di Azure in cui hello nuovo gruppo verrà creato. Per questo scenario, *westus*.
   * **-n (o --nome)**. Nome per hello nuovo gruppo. Per questo scenario, *NSG-FrontEnd*.
3. Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    Output:
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    Parametri
   
   * **-r (o --route-table-name)**. Nome della tabella di routing hello in cui verrà aggiunti route hello. Per questo scenario, *UDR-FrontEnd*.
   * **-a (o --address-prefix)**. Prefisso dell'indirizzo per subnet hello in cui i pacchetti sono destinati a. Per questo scenario, *192.168.2.0/24*.
   * **-t (o --next-hop-type)**. Tipo di oggetto al quale verrà inviato il traffico. I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.
   * **-p (o --next-hop-ip-address**). Indirizzo IP per l'hop successivo. Per questo scenario, *192.168.0.4*.
4. Comando che segue hello esecuzione tabella di route hello tooassociate creata con hello **front-end** subnet:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    Output:
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    Parametri
   
   * **-t (o --vnet-name)**. Nome della rete virtuale in cui si trova subnet hello hello. Per questo scenario, *TestVNet*.
   * **-n (o --subnet-name**. Verrà aggiunto al nome della tabella di routing hello subnet hello. Per questo scenario, *FrontEnd*.

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Creare hello UDR per subnet back-end hello
tabella di route toocreate hello e route necessarie per la subnet di back-end hello a seconda dello scenario hello, hello completo alla procedura seguente:

1. Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

