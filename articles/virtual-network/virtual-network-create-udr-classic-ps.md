---
title: routing aaaControl classica una rete virtuale di Azure - PowerShell - | Documenti Microsoft
description: Informazioni su come toocontrol routing in reti virtuali mediante PowerShell | Classica
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>Controllare il routing e usare dispositivi virtuali di rete (distribuzione classica) mediante PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Interfaccia della riga di comando di Azure](virtual-network-create-udr-arm-cli.md)
> * [Modello](virtual-network-create-udr-arm-template.md)
> * [PowerShell (versione classica)](virtual-network-create-udr-classic-ps.md)
> * [Interfaccia della riga di comando (versione classica)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica. È importante comprendere i [modelli e strumenti di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) prima di lavorare con le risorse di Azure. È possibile visualizzare la documentazione di hello per diversi strumenti selezionando un'opzione nella parte superiore di hello di questo articolo. Questo articolo descrive il modello di distribuzione classica hello.
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

esempio Hello Azure PowerShell comandi riportati di seguito prevedono un ambiente semplice già creato in base hello scenario precedente. Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare nell'ambiente di hello [creare una rete virtuale (versione classica) con PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>Creare hello UDR per subnet front-end hello
tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.

1. Eseguire hello successivo comando toocreate una tabella di route per la subnet front-end hello:

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **front-end** subnet:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>Creare hello UDR per subnet back-end hello
tabella di route toocreate hello e route necessarie per il backup di hello terminare subnet in base a uno scenario di hello, completare hello alla procedura seguente:

1. Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>Attivare l'inoltro IP in hello FW1 VM

inoltro dell'indirizzo IP tooenable in hello FW1 VM, hello completo alla procedura seguente:

1. Eseguire hello seguente lo stato del comando toocheck hello dell'inoltro IP:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Comando che segue hello esecuzione tooenable inoltro dell'indirizzo IP per hello *FW1* VM:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
