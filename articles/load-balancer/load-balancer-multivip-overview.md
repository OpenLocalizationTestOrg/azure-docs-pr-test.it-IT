---
title: aaaMultiple VIP di bilanciamento del carico di Azure | Documenti Microsoft
description: "Panoramica di più indirizzi VIP in Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Più indirizzi VIP per Azure Load Balancer

Bilanciamento del carico di Azure consente di bilanciare i servizi tooload su più porte, più indirizzi IP o entrambi. È possibile utilizzare flussi bilanciamento di carico pubblici e interni del servizio di bilanciamento definizioni tooload in un set di macchine virtuali.

Questo articolo descrive i principi fondamentali di hello di questa possibilità, i concetti importanti e vincoli. Se si intendono solo servizi tooexpose un indirizzo IP, è possibile trovare istruzioni semplificate per [pubblica](load-balancer-get-started-internet-portal.md) o [interno](load-balancer-get-started-ilb-arm-portal.md) caricare le configurazioni di bilanciamento del carico. Aggiunta di più indirizzi VIP è una configurazione VIP singolo tooa incrementale. Usa concetti hello in questo articolo, è possibile espandere una configurazione semplificata in qualsiasi momento.

Quando si definisce un'istanza di Azure Load Balancer, vengono connessi un front-end e un back-end con regole. probe di integrità a cui fa riferimento la regola hello Hello è usato toodetermine di nuovi flussi inviati tooa nodo nel pool back-end hello. front-end Hello è definito da un IP virtuale (VIP), che è una tupla con 3 elementi formata da un indirizzo IP (pubblico o interno), un protocollo di trasporto (UDP o TCP) e un numero di porta. Un DIP è che un indirizzo IP su una scheda di rete virtuale Azure associata tooa macchina virtuale in pool back-end hello.

Hello nella tabella seguente contiene alcune configurazioni di server front-end di esempio:

| Indirizzo VIP | Indirizzo IP | protocol | port |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

tabella Hello Mostra quattro server di front-end diversi. I front-end 1, 2 e 3 rappresentano un unico indirizzo VIP con più regole. Hello stesso indirizzo IP viene utilizzato anche hello porta o protocollo diverso per ogni server front-end. Server front-end n. 1 e &#4; sono un esempio di più indirizzi VIP, in cui hello stesso protocollo front-end e la porta vengono riutilizzati in più indirizzi VIP.

Bilanciamento del carico di Azure fornisce flessibilità nella definizione di regole di bilanciamento del carico di hello. Una regola dichiara come un indirizzo e porta del server front-end hello toohello mappato l'indirizzo di destinazione e la porta sul back-end hello. Se le porte di back-end vengono riutilizzate attraverso le regole dipende dal tipo di hello della regola hello. Ogni tipo di regola presenta requisiti specifici che possono influire sulla configurazione degli host e la progettazione dei probe. Esistono due tipi di regole:

1. riutilizzare regola predefinita Hello con nessuna porta back-end
2. regola di IP mobile Hello in cui vengono riutilizzate porte back-end

Bilanciamento del carico di Azure consente toomix entrambi i tipi di regola su hello stessa configurazione di bilanciamento del carico. bilanciamento del carico Hello poterle usare contemporaneamente per una macchina virtuale specificata o qualsiasi combinazione, purché si attengano ai vincoli di hello della regola hello. Quale tipo di regola scelto dipende dai requisiti di hello l'applicazione e hello nella complessità di supportare tale configurazione. È necessario valutare quali tipi di regole siano più adatti allo scenario.

Vengono illustrati questi scenari ulteriormente a partire dal comportamento predefinito di hello.

## <a name="rule-type-1-no-backend-port-reuse"></a>Regola di tipo 1: nessun riutilizzo delle porte back-end

![Illustrazione di più indirizzi VIP](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

In questo scenario, front-end hello VIP sono configurate come indicato di seguito:

| Indirizzo VIP | Indirizzo IP | protocol | port |
| --- | --- | --- | --- |
| ![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Hello DIP è destinazione hello hello in ingresso del flusso. Nel pool back-end hello, ogni macchina virtuale espone servizio hello desiderata su una porta univoca in un DIP. Questo servizio è associato a hello server front-end tramite una definizione della regola.

Si definiscono due regole:

| Regola | Mapping frontend | pool toobackend |
| --- | --- | --- |
| 1 |![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

mapping di completo Hello nel bilanciamento del carico di Azure è ora il seguente:

| Regola | Indirizzo IP VIP | protocol | port | Destination | port |
| --- | --- | --- | --- | --- | --- |
| ![Regola](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Indirizzo IP DIP |80 |
| ![Regola](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Indirizzo IP DIP |81 |

Ogni regola deve produrre un flusso con una combinazione univoca di indirizzo IP di destinazione e porta di destinazione. Dalla porta di destinazione hello variabili del flusso di hello, più regole possono recapitare i flussi toohello DIP stesso su porte diverse.

Probe di integrità sono sempre toohello diretto DIP di una macchina virtuale. È necessario che il probe riflette integrità hello di hello macchina virtuale.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Regola di tipo 2: riutilizzo delle porte back-end tramite indirizzo IP mobile

Il bilanciamento del carico Azure flessibilità hello porta front-end di tooreuse hello in più indirizzi VIP indipendentemente dal tipo di regola hello utilizzato. Inoltre, alcuni scenari di applicazione preferiscano o richiedono hello stessa porta utilizzata da più istanze dell'applicazione in una singola macchina virtuale nel pool back-end hello toobe. Esempi comuni di riutilizzo delle porte includono il clustering per la disponibilità elevata, le appliance virtuali di rete e l'esposizione di più endpoint TLS senza rieseguire la crittografia di rete.

Se si desidera porta back-end di hello tooreuse tra più regole, è necessario abilitare l'indirizzo IP mobile nella definizione della regola hello.

L'indirizzo IP mobile è una parte di ciò che è noto come Direct Server Return (DSR). Il DSR è costituito da due parti: una topologia di flussi e uno schema di mappatura degli indirizzi IP. A livello di piattaforma, Azure Load Balancer viene sempre eseguito in una topologia di flussi DSR indipendentemente dal fatto che l'indirizzo IP mobile sia abilitato o meno. Ciò significa che parte in uscita di hello di un flusso è sempre origine toohello direttamente indietro tooflow riscritto in modo corretto.

Con tipo di regola predefinita hello Azure espone schema di mapping di indirizzi IP per facilitare l'utilizzo di bilanciamento del carico tradizionale. L'abilitazione di IP mobile modifica tooallow lo schema di mapping di indirizzi IP hello per una maggiore flessibilità, come illustrato di seguito.

Hello seguente diagramma viene illustrata questa configurazione:

![Illustrazione di più indirizzi VIP](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

Per questo scenario, ogni macchina virtuale nel pool back-end hello dispone di tre interfacce di rete:

* DIP: una NIC virtuale associata a hello macchina virtuale (configurazione IP della risorsa di rete di Azure)
* VIP1: un'interfaccia di loopback all'interno del sistema operativo guest configurato con l'indirizzo IP di VIP1
* VIP2: un'interfaccia di loopback all'interno del sistema operativo guest configurato con l'indirizzo IP di VIP2

> [!IMPORTANT]
> configurazione di Hello di interfacce logiche hello viene eseguita all'interno del sistema operativo guest hello. Questa configurazione non viene eseguita o gestita da Azure. Senza questa configurazione, le regole di hello non funzionerà. Le definizioni dei probe di integrità usano hello DIP di hello VM anziché di hello VIP logico. Pertanto, il servizio deve fornire le risposte di probe su una porta DIP che riflettono lo stato di hello del servizio hello disponibile in hello logico VIP.

Si supponga ad esempio hello stessa configurazione front-end come nello scenario precedente hello:

| Indirizzo VIP | Indirizzo IP | protocol | port |
| --- | --- | --- | --- |
| ![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Si definiscono due regole:

| Regola | Mapping frontend | pool toobackend |
| --- | --- | --- |
| 1 |![Regola](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (in VM1 e VM2) |
| 2 |![Regola](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![back-end](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (in VM1 e VM2) |

Hello nella tabella seguente mostra il mapping completo hello nel servizio di bilanciamento del carico hello:

| Regola | Indirizzo IP VIP | protocol | port | Destination | port |
| --- | --- | --- | --- | --- | --- |
| ![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |come indirizzo VIP (65.52.0.1) |come indirizzo VIP (80) |
| ![Indirizzo VIP](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |come indirizzo VIP (65.52.0.2) |come indirizzo VIP (80) |

destinazione Hello di hello flusso in ingresso è l'indirizzo VIP hello sull'interfaccia di loopback hello in hello VM. Ogni regola deve produrre un flusso con una combinazione univoca di indirizzo IP di destinazione e porta di destinazione. Da vari hello indirizzo IP di destinazione del flusso di hello, è possibile sul riutilizzo delle porte hello stessa macchina virtuale. Il servizio è servizio di bilanciamento del carico toohello esposto mediante l'associazione dell'indirizzo VIP toohello indirizzo IP e porta dell'interfaccia di loopback rispettivi hello.

Si noti che in questo esempio non modifica la porta di destinazione hello. Anche se si tratta di uno scenario di IP mobile, bilanciamento del carico di Azure supporta anche la definizione di una porta di destinazione regola toorewrite hello back-end e toomake è diversa dalla porta di destinazione hello front-end.

il tipo di regola di IP mobile Hello è foundation hello più modelli di configurazione del servizio di bilanciamento di carico. Un esempio che è attualmente disponibile è hello [AlwaysOn SQL con più listener](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configurazione. Altri scenari di questo tipo verranno documentati nel tempo.

## <a name="limitations"></a>Limitazioni

* Più configurazioni di indirizzi VIP sono supportate solo con le macchine virtuali IaaS.
* Con una regola di IP mobile hello, l'applicazione deve usare hello DIP per i flussi in uscita. Se l'applicazione associa indirizzo VIP toohello configurato sull'interfaccia di loopback hello nel sistema operativo guest hello, quindi SNAT non è disponibile toorewrite flusso in uscita di hello e flusso hello non riesce.
* Gli indirizzi IP pubblici hanno un effetto sulla fatturazione. Per altre informazioni, vedere [Prezzi per gli indirizzi IP](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Si applicano i limiti delle sottoscrizioni. Per altre informazioni, vedere i [limiti del servizio](../azure-subscription-service-limits.md#networking-limits) .
