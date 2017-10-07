---
title: aaaCreate un bilanciamento del carico interno per servizi Cloud di Azure | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico con PowerShell nel modello di distribuzione classica hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) per i servizi cloud

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Servizi cloud](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Configurare il servizio di bilanciamento del carico interno per i servizi cloud

Il servizio di bilanciamento del carico interno è supportato sia per le macchine virtuali che per i servizi cloud. Un endpoint di servizio di bilanciamento carico interno creato in un servizio cloud di fuori di una rete virtuale regionale sarà accessibile solo all'interno del servizio cloud hello.

configurazione di bilanciamento del carico interno Hello è toobe impostato durante la creazione di hello di distribuzione prima di hello nel servizio cloud hello, come illustrato nell'esempio hello riportato di seguito.

> [!IMPORTANT]
> Una procedura di hello toorun prerequisiti riportata di seguito è una rete virtuale già creata per la distribuzione cloud hello toohave. Sarà necessario hello rete virtuale nome e la subnet nome toocreate hello bilanciamento del carico interno.

### <a name="step-1"></a>Passaggio 1

Aprire file di configurazione servizio hello (. cscfg) per la distribuzione cloud in Visual Studio e aggiungere hello seguente ultima sezione toocreate hello bilanciamento del carico interno in hello "`</Role>`" elemento di configurazione di rete hello.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Aggiungere i valori hello per hello rete configurazione file tooshow l'aspetto. Nell'esempio di hello si supponga che creare una rete virtuale denominata "test_vnet" con un 10.0.0.0/24 subnet denominata test_subnet e un indirizzo IP statico 10.0.0.4. servizio di bilanciamento del carico Hello verrà denominato testLB.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Per ulteriori informazioni sullo schema di bilanciamento carico di hello, vedere [Aggiungi servizio di bilanciamento del carico](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>Passaggio 2

Modificare gli endpoint hello servizio definizione (con estensione csdef) file tooadd toohello con bilanciamento del carico interno. momento di Hello viene creata un'istanza del ruolo, file di definizione del servizio hello aggiungerà hello toohello di istanze di ruolo bilanciamento del carico interno.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

In seguito hello stesso valori nell'esempio hello precedente, aggiungere file di definizione del servizio toohello valori hello.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

il traffico di rete Hello sarà con carico bilanciato con bilanciamento del carico di testLB hello utilizza la porta 80 per le richieste in ingresso, l'invio di tooworker le istanze del ruolo anche sulla porta 80.

## <a name="next-steps"></a>Passaggi successivi

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)

