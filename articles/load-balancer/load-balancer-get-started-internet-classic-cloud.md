---
title: bilanciamento del carico aaaCreate con una connessione Internet per i servizi cloud di Azure | Documenti Microsoft
description: Informazioni su come una connessione Internet toocreate bilanciamento del carico in modello di distribuzione classica per i servizi cloud
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Introduzione alla creazione del servizio di bilanciamento del carico Internet per i servizi cloud

> [!div class="op_single_selector"]
> * [Portale di Azure classico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interfaccia della riga di comando di Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servizi cloud di Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica. È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure. È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo. Questo articolo descrive il modello di distribuzione classica hello. È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

Servizi cloud vengono configurati automaticamente con un bilanciamento del carico e possono essere personalizzati tramite il modello di servizio hello.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Creare un bilanciamento del carico utilizzando file di definizione del servizio hello

È possibile sfruttare hello Azure SDK per .NET 2.5 tooupdate il servizio cloud. Le impostazioni di endpoint per servizi cloud vengono eseguite in hello [definizione servizio](https://msdn.microsoft.com/library/azure/gg557553.aspx) file con estensione csdef.

Hello esempio seguente viene illustrato come un file servicedefinition. csdef per una distribuzione cloud configurato:

Controllo di frammento hello per file con estensione csdef hello generato da una distribuzione cloud, è possibile visualizzare hello endpoint esterno configurato toouse porte HTTP sulla porta 10000 e 10001 10002.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Controllo dello stato di integrità del servizio di bilanciamento del carico per i servizi cloud

Hello Ecco un esempio di un probe di integrità:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Hello bilanciamento del carico combina hello informazioni dell'endpoint hello e hello di hello probe toocreate un URL nel formato hello `http://{DIP of VM}:80/Probe.aspx` che può essere utilizzato tooquery hello integrità del servizio hello.

servizio Hello rileva probe periodiche da hello stesso indirizzo IP. Si tratta di richiesta di probe di integrità hello provenienti dall'host di hello del nodo hello in cui è in esecuzione macchine virtuali di hello. servizio Hello è toorespond con codice di stato HTTP 200 per tooassume del servizio di bilanciamento carico di hello che servizio hello è integro. Qualsiasi altro tipo di stato HTTP (ad esempio 503) il codice direttamente accetta hello macchina virtuale dalla rotazione.

definizione di tipo probe Hello controlla anche la frequenza di hello del probe hello. In questo caso precedente, bilanciamento del carico hello è probing endpoint hello ogni 5 secondi. Se nessuna risposta positiva viene ricevuta per 10 secondi (due intervalli di probe), si presuppone che il probe hello verso il basso e macchina virtuale hello viene escluso dalla rotazione. Analogamente, se il servizio di hello è dalla rotazione e viene ricevuta una risposta positiva, servizio hello viene reinserita toorotation immediatamente. Se il servizio hello sta fluttuando. potete tra integro e non corretti, bilanciamento del carico hello può decidere reintroduzione hello toodelay di hello servizio back-toorotation fino a quando non è stato integro per un numero di probe.

Verifica dello schema di definizione del servizio di hello per hello [probe di integrità](https://msdn.microsoft.com/library/azure/jj151530.aspx) per ulteriori informazioni.

## <a name="next-steps"></a>Passaggi successivi

[Introduzione alla configurazione del bilanciamento del carico interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)

