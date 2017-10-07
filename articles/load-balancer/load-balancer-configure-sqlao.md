---
title: bilanciamento del carico aaaConfigure per SQL AlwaysOn | Documenti Microsoft
description: Configurare toowork bilanciamento di carico con SQL sempre e come tooleverage powershell toocreate bilanciamento del carico per implementazione SQL hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Configurare il bilanciamento del carico per SQL AlwaysOn

I gruppi di disponibilità AlwaysOn di SQL Server ora possono essere eseguiti con ILB. Un gruppo di disponibilità è la soluzione principale di SQL Server per il ripristino di emergenza e la disponibilità elevata. Hello listener del gruppo di disponibilità consente alle applicazioni client tooseamlessly connettersi toohello la replica primaria, indipendentemente dal numero di hello di repliche hello nella configurazione di hello.

nome del listener (DNS) di Hello è l'indirizzo IP mappato tooa con bilanciata del carico e bilanciamento del carico di Azure indirizza il server primario di hello in arrivo traffico tooonly hello nel set di repliche hello.

È possibile usare il supporto ILB per gli endpoint di SQL Server AlwaysOn (listener). È ora possibile controllare accessibilità hello del listener hello e scegliere l'indirizzo IP con bilanciamento del carico hello da una subnet specifica nella rete virtuale (VNet).

Con bilanciamento del carico interno listener hello, hello endpoint SQL server (ad esempio Server = tcp:ListenerName, 1433; Database = DatabaseName) è accessibile solo da:

* Servizi e macchine virtuali nella stessa rete virtuale di hello
* Servizi e VM dalla rete locale connessa
* Servizi e VM da reti virtuali interconnesse

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Figura 1 - SQL AlwaysOn configurato con bilanciamento del carico con connessione Internet

## <a name="add-internal-load-balancer-toohello-service"></a>Aggiungere il servizio di bilanciamento del carico interno toohello

1. Nel seguente esempio di hello, è possibile configurare una rete virtuale che contiene una subnet denominata "Subnet-1":

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Aggiungere gli endpoint con carico bilanciato per ILB in ogni macchina virtuale

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    Nell'esempio hello sopra, si dispone di 2 VM chiamato "sqlsvc1" e "sqlsvc2" esecuzione del servizio nel cloud hello "Sqlsvc". Dopo la creazione di hello ILB con `DirectServerReturn` passa, si aggiungono carico bilanciato endpoint toohello ILB tooallow SQL tooconfigure hello listener per gruppi di disponibilità hello.

Per altre informazioni su SQL AlwaysOn, vedere [Configurare un servizio di bilanciamento del carico interno per un gruppo di disponibilità AlwaysOn in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Vedere anche
[Introduzione alla configurazione del bilanciamento del carico Internet](load-balancer-get-started-internet-arm-ps.md)

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurare una modalità di distribuzione del bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
