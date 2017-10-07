---
title: NAT per Azure ExpressRoute | Microsoft Docs
description: Questa pagina illustra i requisiti dettagliati per la configurazione e la gestione del routing per i circuiti ExpressRoute.
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 7a8b760df90b545b5fbde2f614aef62dd3985bb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nat-for-expressroute"></a>NAT per ExpressRoute

tooconnect tooMicrosoft servizi cloud tramite ExpressRoute è sarà necessario tooset backup e la gestione del routing. Alcuni provider di connettività offrono la configurazione e la gestione del routing come servizio gestito. Verificare con il toosee di provider di connettività se offrono questo servizio. In caso contrario, è necessario rispettare toohello seguenti requisiti. 

Fare riferimento toohello [circuiti e domini di routing](expressroute-circuit-peerings.md) articolo per una descrizione di routing hello sessioni necessarie toobe di impostare la connettività toofacilitate.

> [!NOTE]
> Microsoft non supporta alcun protocollo di ridondanza router (ad esempio, HSRP e VRRP) per le configurazioni con disponibilità elevata. Per la disponibilità elevata, Microsoft si avvale invece di una coppia ridondante di sessioni BGP per peering.
> 
> 

## <a name="ip-addresses-used-for-peerings"></a>Indirizzi IP usati per i peering

È necessario tooreserve alcuni blocchi di IP indirizzi tooconfigure routing tra la rete e i router di Microsoft Enterprise edge (MSEEs). In questa sezione fornisce un elenco di requisiti e le regole hello come questi indirizzi IP devono essere acquisiti e utilizzati.

### <a name="ip-addresses-used-for-azure-private-peering"></a>Indirizzi IP usati per il peering privato di Azure

È possibile utilizzare gli indirizzi IP privati o pubblici peering di hello tooconfigure di indirizzi IP. intervallo di indirizzi Hello utilizzato per la configurazione delle route non deve sovrapporsi a indirizzo intervalli utilizzati toocreate reti virtuali in Azure. 

* È necessario riservare una subnet /29 o due subnet /30 per le interfacce di routing.
* subnet Hello utilizzata per il routing può essere indirizzi IP privati o gli indirizzi IP pubblici.
* subnet Hello non deve essere in conflitto con l'intervallo di hello riservato da parte del cliente per l'uso nel cloud di Microsoft hello hello.
* Se viene usata una subnet /29, questa verrà divisa in due subnet /30. 
  * Hello innanzitutto/30 subnet verrà utilizzato per collegamento primario hello e hello /30 secondo subnet sarà usata per collegamento secondario hello.
  * Per ogni subnet hello /30, è necessario utilizzare hello primo indirizzo IP del subnet hello /30 sul router. Microsoft utilizzerà secondo indirizzo IP hello di hello /30 subnet tooset una sessione BGP.
  * È necessario impostare entrambe le sessioni BGP per il nostro [SLA sulla disponibilità](https://azure.microsoft.com/support/legal/sla/) toobe valido.  

#### <a name="example-for-private-peering"></a>Esempio per il peering privato

Se si sceglie toouse a.b.c.d/29 tooset backup hello peering, verrà suddiviso in due /30 subnet. Nell'esempio hello riportato di seguito, verranno esaminati utilizzo subnet a.b.c.d/29 hello. 

a.b.c.d/29 verrà tooa.b.c.d/30 split e a.b.c.d+4/30 e trasmessi tooMicrosoft tramite le API di provisioning hello. Si utilizzerà a.b.c.d+1 come hello VRF IP per hello PE primario e Microsoft utilizzerà a.b.c.d+2 come hello IP VRF per hello MSEE primario. Si utilizzerà a.b.c.d+5 come hello VRF IP per hello secondario PE e Microsoft utilizzerà a.b.c.d+6 come hello IP VRF per hello MSEE secondario.

Si consideri il caso in cui si seleziona tooset 192.168.100.128/29 di peering privato. 192.168.100.128/29 sono inclusi gli indirizzi da 192.168.100.128 too192.168.100.135, tra cui:

* verrà assegnato 192.168.100.128/30 toolink1, con provider mediante 192.168.100.129 e Microsoft mediante 192.168.100.130.
* verrà assegnato 192.168.100.132/30 toolink2, con provider mediante 192.168.100.133 e Microsoft mediante 192.168.100.134.

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a>Indirizzi IP usati per il peering Microsoft e il peering pubblico di Azure

È necessario utilizzare indirizzi IP pubblici a cui si è proprietari per la configurazione di sessioni BGP hello. Microsoft deve essere di proprietà hello tooverify in grado di indirizzi IP hello tramite Routing registri Internet e i registri di Routing Internet. 

* È necessario utilizzare un univoco/29 subnet o tooset due /30 subnet backup hello BGP peer per ogni peering per il circuito ExpressRoute (se si dispone di più di uno). 
* Se viene usata una subnet /29, questa verrà divisa in due subnet /30. 
  * Hello innanzitutto/30 subnet verrà utilizzato per collegamento primario hello e hello /30 secondo subnet sarà usata per collegamento secondario hello.
  * Per ogni subnet hello /30, è necessario utilizzare hello primo indirizzo IP del subnet hello /30 sul router. Microsoft utilizzerà secondo indirizzo IP hello di hello /30 subnet tooset una sessione BGP.
  * È necessario impostare entrambe le sessioni BGP per il nostro [SLA sulla disponibilità](https://azure.microsoft.com/support/legal/sla/) toobe valido.

## <a name="public-ip-address-requirement"></a>Requisito dell'indirizzo IP pubblico

### <a name="private-peering"></a>Peering privato

È possibile scegliere toouse gli indirizzi IPv4 pubblici o privati per il peering privato. Offriamo un isolamento end-to-end del traffico di modo che la sovrapposizione degli indirizzi con altri clienti non si verifica in caso di peering privato. Questi indirizzi non sono tooInternet annunciato. 

### <a name="public-peering"></a>Peering pubblico

percorso di peering pubblico Azure Hello consente si tooconnect tooall servizi ospitati in Azure tramite i relativi indirizzi IP pubblici. Sono inclusi i servizi elencati nella hello [domande frequenti su ExpessRoute](expressroute-faqs.md) e tutti i servizi ospitati da parte degli ISV in Microsoft Azure. Connettività tooMicrosoft Azure servizi pubblici peering viene sempre avviato dalla rete nella rete di Microsoft hello. È necessario utilizzare indirizzi IP pubblici per rete di tooMicrosoft destinati hello del traffico.

### <a name="microsoft-peering"></a>Peering Microsoft

percorso di peering Microsoft Hello consente di connettersi ai servizi cloud tooMicrosoft che non sono supportati tramite hello Azure percorso di peering pubblico. elenco di Hello dei servizi include servizi di Office 365, ad esempio Exchange Online, SharePoint Online, Skype for Business e Dynamics 365. Microsoft supporta una connettività bidirezionale nel peering Microsoft hello. Servizi cloud di traffico tooMicrosoft devono utilizzare validi indirizzi IPv4 pubblici prima immette rete Microsoft hello.

Assicurarsi che l'indirizzo IP e come numero sono registrati tooyou in uno dei registri hello elencati di seguito.

* [ARIN](https://www.arin.net/)
* [APNIC](https://www.apnic.net/)
* [AFRINIC](https://www.afrinic.net/)
* [LACNIC](http://www.lacnic.net/)
* [RIPENCC](https://www.ripe.net/)
* [RADB](http://www.radb.net/)
* [ALTDB](http://altdb.net/)

> [!IMPORTANT]
> Indirizzo IP pubblico indirizzi annunciati tooMicrosoft expressroute non può essere annunciato toohello Internet. Questo è possibile interrompere i servizi di integrazione applicativa tooother Microsoft. Tuttavia, gli indirizzi IP pubblici usati dai server nella rete che comunica con gli endpoint di Office 365 nell'ambiente Microsoft possono essere annunciati tramite ExpressRoute. 
> 
> 

## <a name="dynamic-route-exchange"></a>Scambio di route dinamico

Lo scambio di routing avviene tramite il protocollo eBGP. Vengono stabilite sessioni EBGP tra MSEEs hello e ai router. L'autenticazione delle sessioni eBGP non è un requisito. Se necessario, è possibile configurare un hash MD5. Vedere hello [Configura routing](expressroute-howto-routing-classic.md) e [Circuit provisioning flussi di lavoro e circuit stati](expressroute-workflows.md) per informazioni sulla configurazione delle sessioni BGP.

## <a name="autonomous-system-numbers"></a>Numeri AS (Autonomous System)

Microsoft userà il numero AS 12076 per il peering pubblico di Azure, il peering privato di Azure e il peering Microsoft. È stato riservato ASN da 65515 too65520 per uso interno. Sono supportati sia i numeri AS a 16 bit che a 32 bit.

Non sono previsti requisiti per la simmetria del trasferimento dei dati. i percorsi di inoltro e restituito Hello debba attraversare coppie di router diverso. Le route identiche devono essere annunciate da entrambi i lati in più coppie di circuiti appartenenti all'utente. Le metriche di route non sono necessari toobe identici.

## <a name="route-aggregation-and-prefix-limits"></a>Limiti per i prefissi e l'aggregazione di route

Un sostegno backup too4000 prefissi annunciati toous tramite hello peering privato di Azure. Questo valore può essere aumentato di too10, prefissi 000 se il componente aggiuntivo di hello ExpressRoute premium è abilitato. Vengono accettati i prefissi di too200 per ogni sessione BGP per Azure pubblico e peering Microsoft. 

sessione BGP Hello verrà eliminata se il numero di hello di prefissi supera il limite di hello. Vengono accettati route predefinite su solo collegamento peering privato hello. Provider deve escludere route predefinita e gli indirizzi IP privati (RFC 1918) da hello Azure pubblico e percorsi di peering di Microsoft. 

## <a name="transit-routing-and-cross-region-routing"></a>Routing di transito e routing tra aree

Non è possibile configurare ExpressRoute come router di transito. Sarà necessario toorely per il provider di connettività per servizi di routing di transito.

## <a name="advertising-default-routes"></a>Annuncio delle route predefinite

Le route predefinite sono consentite solo nelle sessioni di peering privato di Azure. In tal caso, si indirizza tutto il traffico dalla rete di tooyour hello reti virtuali associate. Annuncio delle route predefinite in peering privato comporterà percorso internet hello da Azure bloccate. È necessario basarsi su traffico da tooroute aziendale e toohello internet per i servizi ospitati in Azure. 

 tooenable connettività tooother Azure servizi e i servizi di infrastruttura, è necessario verificare che uno dei seguenti elementi hello sia sul posto:

* Peering pubblico di Azure viene abilitato tooroute traffico toopublic endpoint
* Utilizzare definito dall'utente routing tooallow la connettività a internet per la connettività Internet che richiedono ogni subnet.

> [!NOTE]
> L'annuncio delle route predefinite interromperà l'attivazione della licenza di Windows e di altre macchine virtuali. Seguire le istruzioni [qui](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) toowork il problema.
> 
> 

## <a name="support-for-bgp-communities-preview"></a>Supporto per BGP Community (anteprima)

Questa sezione fornisce una panoramica che illustra come vengono usate le community BGP con ExpressRoute. Microsoft verrà annunciare le route hello pubblico e i percorsi di peering Microsoft route contrassegnate valori appropriati della community. Hello spiegazione logica per questa operazione e i dettagli di seguito vengono descritti i valori alla community di hello. Microsoft, tuttavia, non rispetteranno le community valori tag tooroutes annunciati tooMicrosoft.

Se ci si connette tooMicrosoft tramite ExpressRoute in qualsiasi posizione di peering uno all'interno di un'area geopolitica, si avrà accesso tooall Microsoft cloud services tutte le regioni entro i limiti di natura geopolitica hello. 

Ad esempio, se si è connessi tramite ExpressRoute tooMicrosoft Amsterdam, sarà necessario servizi di accesso tooall Microsoft cloud ospitati in Europa settentrionale ed Europa occidentale. 

Fare riferimento toohello [ExpressRoute partner e località di peering](expressroute-locations.md) pagina per un elenco dettagliato delle aree geopolitiche, aree di Azure associate ed ExpressRoute corrispondente peering percorsi.

È possibile acquistare più di un circuito ExpressRoute per area geopolitica. Disporre di più connessioni offre vantaggi significativi sulla disponibilità elevata ridondanza toogeo scadenza. Nei casi in cui si dispone di più circuiti ExpressRoute, si riceverà hello stesso set di prefissi annunciati da Microsoft sul peering pubblico hello e Microsoft peering percorsi. Questo significa che saranno disponibili più percorsi dalla propria rete a Microsoft. Ciò può causare potenzialmente ottimali toobe decisioni routing apportate all'interno della rete. Di conseguenza, possono verificarsi servizi toodifferent esperienze di connettività non ottimale. 

Microsoft verrà tag i prefissi pubblicati tramite il peering pubblico e Microsoft peering con valori appropriati per il protocollo BGP community che indica i prefissi di hello area hello sono ospitati in. È possibile basarsi su hello community valori toomake appropriato routing decisioni toooffer [toocustomers routing ottimale](expressroute-optimize-routing.md).

| **Area geopolitica** | **Area di Microsoft Azure** | **Valore della community BGP** |
| --- | --- | --- |
| **America del Nord** | | |
| Stati Uniti orientali |12076:51004 | |
| Stati Uniti orientali 2 |12076:51005 | |
| Stati Uniti occidentali |12076:51006 | |
| Stati Uniti occidentali 2 |12076:51026 | |
| Stati Uniti centro-occidentali |12076:51027 | |
| Stati Uniti centro-settentrionali |12076:51007 | |
| Stati Uniti centro-meridionali |12076:51008 | |
| Stati Uniti centrali |12076:51009 | |
| Canada centrale |12076:51020 | |
| Canada orientale |12076:51021 | |
| **America del Sud** | | |
| Brasile meridionale |12076:51014 | |
| **Europa** | | |
| Europa settentrionale |12076:51003 | |
| Europa occidentale |12076:51002 | |
| **Asia Pacifico** | | |
| Asia orientale |12076:51010 | |
| Asia sudorientale |12076:51011 | |
| **Giappone** | | |
| Giappone orientale |12076:51012 | |
| Giappone occidentale |12076:51013 | |
| **Australia** | | |
| Australia orientale |12076:51015 | |
| Australia sudorientale |12076:51016 | |
| **India** | | |
| India meridionale |12076:51019 | |
| India occidentale |12076:51018 | |
| India centrale |12076:51017 | |

Tutte le route annunciate dal Microsoft verranno contrassegnate con il valore di hello community appropriato. 

> [!IMPORTANT]
> I prefissi globali verranno contrassegnati con un valore della community appropriato e saranno annunciati solo quando è abilitato il componente aggiuntivo ExpressRoute Premium.
> 
> 

Inoltre toohello precedente, Microsoft verrà anche tag prefissi basati sul servizio hello che cui appartengono. Si applica solo toohello Microsoft peering. tabella Hello seguente fornisce un mapping del valore di community tooBGP di servizio.

| **Servizio** | **Valore della community BGP** |
| --- | --- |
| **Exchange** |12076:5010 |
| **SharePoint** |12076:5020 |
| **Skype For Business** |12076:5030 |
| **Dynamics 365** |12076:5040 |
| **Altri servizi di Office 365** |12076:5100 |

> [!NOTE]
> Microsoft non soddisfa tutti i valori della community BGP è impostato su hello le route annunciate tooMicrosoft.
> 
> 

## <a name="next-steps"></a>Passaggi successivi

* Configurare la connessione ExpressRoute.
  
  * [Creare un circuito ExpressRoute per il modello di distribuzione classica hello](expressroute-howto-circuit-classic.md) o [creare e modificare un circuito ExpressRoute tramite Gestione risorse di Azure](expressroute-howto-circuit-arm.md)
  * [Configurare il routing per il modello di distribuzione classica hello](expressroute-howto-routing-classic.md) o [configurare il routing per modello di distribuzione di gestione risorse di hello](expressroute-howto-routing-arm.md)
  * [Collegare un classico tooan di rete virtuale circuito ExpressRoute](expressroute-howto-linkvnet-classic.md) o [collegare un circuito ExpressRoute di tooan VNet Gestione risorse](expressroute-howto-linkvnet-arm.md)

