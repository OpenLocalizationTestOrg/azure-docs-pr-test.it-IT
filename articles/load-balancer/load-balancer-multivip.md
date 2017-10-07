---
title: aaaMutiple VIP per un servizio cloud
description: "Panoramica di più indirizzi VIP e come tooset più indirizzi VIP in un servizio cloud"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Configurare più indirizzi VIP per un servizio cloud

È possibile accedere a servizi cloud di Azure su hello rete Internet pubblica utilizzando un indirizzo IP fornito da Azure. Questo indirizzo IP pubblico è tooas di cui si fa riferimento un indirizzo VIP (virtual IP) perché è collegata toohello Azure bilanciamento del carico e non hello istanze di macchina virtuale (VM) all'interno del servizio cloud hello. È possibile accedere a qualsiasi istanza di macchina virtuale in un servizio cloud usando un singolo indirizzo VIP.

Tuttavia, esistono scenari in cui potrebbe essere necessario più di un indirizzo VIP come un toohello del punto di ingresso stesso servizio cloud. Ad esempio, il servizio cloud può ospitare più siti Web che richiedono una connettività SSL Usa hello porta predefinita 443, ogni sito è ospitato per un altro cliente o del tenant. In questo scenario, è necessario toohave un diverso indirizzo IP pubblico per ogni sito Web. Hello diagramma seguente viene illustrato un tipico web multi-tenant che ospita con la necessità per certificati SSL multiple in hello stessa porta pubblica.

![Scenario SSL con più indirizzi VIP](./media/load-balancer-multivip/Figure1.png)

Nell'esempio riportato sopra, tutti gli indirizzi VIP utilizzare hello hello stessa porta pubblica (443) e il traffico viene reindirizzato tooone o più carico bilanciate macchine virtuali su una porta privata univoca per l'indirizzo IP interno hello del servizio cloud hello hello tutti i siti Web di hosting.

> [!NOTE]
> Utilizzare hello di un'altra situazione che richiede hello più indirizzi VIP ospita più listener del gruppo di disponibilità AlwaysOn SQL in hello stesso insieme di macchine virtuali.

Gli indirizzi VIP sono dinamici per impostazione predefinita, il che significa che l'indirizzo IP effettivo hello assegnato servizio cloud toohello potrebbe cambiare nel tempo. tooprevent che accada, è possibile riservare un indirizzo VIP per il servizio. toolearn ulteriori informazioni su indirizzi VIP riservati, vedere [indirizzo IP pubblico riservato](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Per informazioni sui prezzi di indirizzi VIP e IP riservati, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/) .

È possibile utilizzare PowerShell tooverify hello VIP utilizzato dai servizi cloud, nonché aggiungere e rimuovere gli indirizzi VIP, associare un endpoint tooan VIP e configurare uno specifico VIP bilanciamento del carico.

## <a name="limitations"></a>Limitazioni

A questo punto, funzionalità di più VIP è limitato toohello seguenti scenari:

* **Solo IaaS**. È possibile abilitare più indirizzi VIP per servizi cloud che contengono le macchine virtuali. Non è possibile usare più indirizzi VIP negli scenari PaaS con le istanze del ruolo.
* **Solo PowerShell**. È possibile gestire più indirizzi VIP solo con PowerShell.

Queste limitazioni sono temporanee e possono cambiare in qualsiasi momento. Consentire toorevisit che questa pagina tooverify eventuali modifiche future.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Come servizio cloud tooa tooadd un indirizzo VIP
servizio tooyour tooadd un indirizzo VIP, eseguire il comando PowerShell seguente hello:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Questo comando Visualizza un toohello simile di risultati seguente esempio:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Come tooremove un indirizzo IP virtuale da un servizio cloud
hello tooremove VIP aggiunto tooyour servizio nell'esempio hello sopra, hello esecuzione comando PowerShell seguente:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> È possibile rimuovere un indirizzo VIP solo se non dispone di alcun tooit endpoint associato.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Come tooretrieve VIP informazioni da un servizio Cloud
hello tooretrieve VIP associata a un servizio cloud, eseguire lo script di PowerShell seguente hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

script Hello Visualizza un toohello simile di risultati seguente esempio:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

In questo esempio, un servizio cloud hello è 3 VIP:

* **Vip1** è hello VIP predefinito, si è certi che perché hello IsDnsProgrammedName è impostato tootrue.
* **Vip2** e **Vip3** non sono in uso in quanto non dispongono di indirizzi IP. Poter essere utilizzati solo se si associa un toohello endpoint VIP.

> [!NOTE]
> Gli indirizzi VIP aggiuntivi verranno addebitati alla sottoscrizione solo dopo essere stati associati a un endpoint. Per altre informazioni sui prezzi, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Come endpoint tooan tooassociate un indirizzo VIP

tooassociate un indirizzo IP virtuale nel cloud tooan endpoint del servizio eseguire hello comando PowerShell seguente:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

comando Hello crea un endpoint denominato toohello collegato VIP *Vip2* sulla porta *80*e lo collega toohello macchina virtuale denominata *myVM1* in un servizio cloud denominato  *myService* utilizzando *TCP* sulla porta *8080*.

configurazione di hello tooverify, eseguire il comando PowerShell seguente hello:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

output di Hello è simile toohello esempio seguente:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Come tooenable il bilanciamento del carico in un indirizzo IP virtuale specifico

È possibile associare un singolo indirizzo VIP a più macchine virtuali per scopi di bilanciamento del carico. Si supponga, ad esempio, di disporre di un servizio cloud denominato *myService* e di due macchine virtuali denominate *myVM1* e *myVM2*. Il servizio cloud dispone di più indirizzi VIP, uno dei quali è denominato *Vip2*. Se si desidera che tutto il traffico tooport tooensure *81* su *Vip2* viene bilanciato tra *myVM1* e *myVM2* sulla porta *8181* eseguire hello seguente script di PowerShell:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

È inoltre possibile aggiornare toouse di bilanciamento del carico un VIP diverso. Ad esempio, se si esegue hello comando PowerShell riportato di seguito, si modificherà set toouse un VIP denominato Vip1 di bilanciamento del carico di hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Passaggi successivi

[Log Analytics per Azure Load Balancer](load-balancer-monitor-log.md)

[Panoramica del bilanciamento del carico Internet](load-balancer-internet-overview.md)

[Introduzione al bilanciamento del carico Internet](load-balancer-get-started-internet-arm-ps.md)

[Panoramica di Rete virtuale.](../virtual-network/virtual-networks-overview.md)

[API REST di IP riservati](https://msdn.microsoft.com/library/azure/dn722420.aspx)
