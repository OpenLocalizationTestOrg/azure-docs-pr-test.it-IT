---
title: aaaMove una macchina virtuale (classico) o una subnet tooa diversi istanza ruolo Servizi Cloud - Azure PowerShell | Documenti Microsoft
description: Informazioni su come toomove macchine virtuali (classico) e istanze del ruolo di servizi Cloud tooa subnet diversa utilizzando PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Spostare una macchina virtuale (classico) o i servizi Cloud ruolo istanza tooa subnet diversa utilizzando PowerShell
È possibile utilizzare le macchine virtuali (classico) da una subnet tooanother toomove di PowerShell in hello stessa rete virtuale (VNet). Le istanze del ruolo possono essere spostate con la modifica di file CSCFG hello, anziché tramite PowerShell.

> [!NOTE]
> Questo articolo spiega come macchine virtuali toomove distribuito tramite solo modello di distribuzione classica hello.
> 
> 

Motivi per cui spostare le macchine virtuali tooanother subnet? La migrazione è utile quando la subnet meno recente hello è troppo piccola e non può essere espansa a causa di tooexisting macchine virtuali in esecuzione in quella subnet. In tal caso, è possibile creare una nuova subnet più grande e la migrazione nuova subnet hello macchine virtuali toohello, quindi al termine della migrazione, è possibile eliminare vecchia subnet ormai vuota hello.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>Come toomove tooanother subnet VM
toomove una macchina virtuale, eseguire i cmdlet di PowerShell Set-AzureSubnet hello, utilizzando l'esempio hello riportato di seguito come modello. Nell'esempio hello seguente, TestVM viene spostata dalla subnet corrente, tooSubnet-2. Essere tooreflect di esempio hello tooedit che l'ambiente. Si noti che quando si esegue cmdlet Update-AzureVM hello come parte di una stored procedure, verrà riavviato la macchina virtuale come parte del processo di aggiornamento hello.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Se è stato specificato un indirizzo IP privato interno statico per la macchina virtuale, sarà necessario tooclear tale impostazione prima di poter spostare nuova subnet tooa VM hello. In tal caso, utilizzare il seguente di hello:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove una subnet tooanother istanza di ruolo
toomove un'istanza del ruolo, modificare il file CSCFG hello. Nell'esempio hello riportato di seguito "Role0" viene spostato nella rete virtuale *VNETName* dalla subnet corrente troppo*Subnet-2*. Poiché l'istanza del ruolo hello era già stata distribuita, sarà solo necessario impostare il nome di Subnet hello = Subnet-2. Essere tooreflect di esempio hello tooedit che l'ambiente.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
