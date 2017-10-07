---
title: una rete virtuale utilizzando aaaCreate hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come una rete virtuale utilizzando toocreate hello Azure CLI 1.0 | Gestore delle risorse.
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a>Creare una rete virtuale usando hello CLI di Azure

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica. Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello. altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.

## <a name="cli-versions-toocomplete-hello-task"></a>Attività hello toocomplete versioni CLI
È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:

- [Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello
- [Azure CLI 1.0](#create-a-virtual-network) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>Crea rete virtuale

una rete virtuale utilizzando toocreate hello CLI di Azure, hello completo alla procedura seguente:

1. Installare e configurare Azure CLI da hello seguente passaggi hello in hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md) articolo.

2. Creare una rete virtuale e subnet:

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    Output previsto:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    Parametri utilizzati:

   * **--vnet**. Nome di hello toobe di rete virtuale creata. Per questo scenario, *TestVNet*
   * **-e (o --address-space)**. Spazio degli indirizzi della rete virtuale. Per questo scenario, *192.168.0.0*
   * **-i (o -cidr)**. Maschera di rete nel formato CIDR. Per questo scenario, *16*
   * **- n (o --subnet-name**). Nome della subnet prima hello. Per questo scenario, *FrontEnd*.
   * **-p (or --subnet-start-ip)**. Indirizzo IP iniziale per la subnet o spazio di indirizzi della subnet. Per questo scenario, *192.168.1.0*
   * **-r (o --subnet-cidr)**. Maschera di rete nel formato CIDR per la subnet. Per questo scenario, *24*
   * **-l (o --location)**. Area di Azure in cui è stato creato hello rete virtuale. Per questo scenario, *Central US*.

3. Creare una subnet:

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    Output previsto:

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    Parametri utilizzati:

   * **-t (o --vnet-name**. Nome della rete virtuale in cui verrà creata la subnet hello hello. Per questo scenario, *TestVNet*.
   * **-n (o --nome)**. Nome della nuova subnet hello. Per questo scenario, *BackEnd*.
   * **-a (o --address-prefix)**. Blocco CIDR della subnet. Per questo scenario, *192.168.2.0/24*.
   
4. proprietà hello tooview di hello nuova rete virtuale:

    ```azurecli
    azure network vnet show
    ```
   
    Output previsto:
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooconnect:

- Una rete virtuale tooa di macchina virtuale (VM) leggendo hello [creare una VM Linux](../virtual-machines/linux/quick-create-cli.md) articolo. Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.
- Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) articolo.
- rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute. Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
