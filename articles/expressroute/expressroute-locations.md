---
title: "Località e provider di connettività: Azure ExpressRoute | Documentazione Microsoft"
description: "In questo articolo fornisce una panoramica dettagliata dei percorsi in cui vengono offerti i servizi e come tooconnect tooAzure aree. Ordinamento per provider di connettività."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: c878513a-d594-42ad-8b0e-403efd0c4b25
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: df906ae6ff4e149c9cab4aa46ab78c8dd6aa4366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>Partner e località di peering per ExpressRoute

> [!div class="op_single_selector"]
> * [Località per provider](expressroute-locations.md)
> * [Provider per località](expressroute-locations-providers.md)


Hello nelle tabelle di questo articolo è fornire informazioni sui provider di connettività di ExpressRoute, ExpressRoute geografico, servizi cloud Microsoft supportati tramite ExpressRoute e integratori di ExpressRoute (SIs).

## <a name="partners"></a>Provider di connettività ExpressRoute
ExpressRoute è supportato in tutte le aree e le località di Azure. Hello mappa seguente fornisce un elenco di aree di Azure e i percorsi di ExpressRoute. Percorsi di ExpressRoute, vedere toothose in cui Microsoft peer con diversi provider di servizi.

![Mappa delle località][0]

Se si è connessi tooat almeno una posizione di ExpressRoute nell'area di natura geopolitica hello, sarà necessario servizi di accesso tooAzure di tutte le aree all'interno di un'area di natura geopolitica.

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Percorsi di tooExpressRoute aree di Azure all'interno di un'area di natura geopolitica.
Hello nella tabella seguente fornisce una mappa delle aree di Azure tooExpressRoute posizioni all'interno di un'area di natura geopolitica.

| **Area geopolitica** | **Aree di Azure** | **Località per ExpressRoute** |
| --- | --- | --- |
| **America del Nord** |Stati Uniti orientali, Stati Uniti occidentali, Stati Uniti orientali 2, Stati Uniti occidentali 2, Stati Uniti centrali, Stati Uniti centro-meridionali, Stati Uniti centro-settentrionali, Stati Uniti centro-occidentali, Canada centrale, Canada orientale |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Miami, New York, San Antonio, Seattle, Silicon Valley, Washington DC, Montreal, Quebec City, Toronto |
| **America del Sud** |Brasile meridionale |Sao Paulo |
| **Europa** |Europa settentrionale, Europa occidentale, Regno Unito occidentale, Regno Unito meridionale |Amsterdam, Dublino, Londra, Newport (Galles), Parigi |
| **Asia** |Asia orientale, Asia sudorientale |Hong Kong, Singapore |
| **Giappone** |Giappone occidentale, Giappone orientale |Osaka, Tokyo |
| **Australia** |Australia sudorientale, Australia orientale |Melbourne, Sydney |
| **India** |India occidentale, India centrale, India Meridionale |Chennai, Mumbai |
| **Corea del Sud** |Corea centrale, Corea meridionale |Busan, Seoul |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Aree e confini geopolitici per cloud nazionali
tabella Hello seguente fornisce informazioni sulle aree e i limiti di natura geopolitici per cloud nazionale.

| **Area geopolitica** | **Aree di Azure** | **Località per ExpressRoute** |
| --- | --- | --- |
| **Cloud del governo degli Stati Uniti** |US Gov Iowa, US Gov Virginia, US DoD Central, US DoD East  |Chicago, Dallas, New York, Seattle, Silicon Valley, Washington DC |
| **Cina** |Cina meridionale, Cina orientale |Pechino, Shanghai |
| **Germania** |Germania centrale, Germania orientale |Berlino, Francoforte |

Non è supportata la connettività tra le aree di natura geopolitiche sullo standard hello SKU ExpressRoute. Sarà necessario tooenable hello ExpressRoute premium componente aggiuntivo toosupport globale la connettività. Ambienti di cloud toonational connettività non è supportata. È possibile utilizzare il provider di connettività in caso di necessità.

## <a name="locations"></a>Località dei provider di connettività

Hello nella tabella seguente mostra i percorsi da provider di servizi. Se si desidera tooview provider disponibili dalla località, vedere [provider dall'indirizzo](expressroute-locations-providers.md#locations).


### <a name="production-azure"></a>Produzione Azure
| **Provider di servizi** | **Microsoft Azure** | **Office 365 e Dynamics 365** | **Località** |
| --- | --- | --- | --- |
| **[AARNet](https://www.aarnet.edu.au/network-and-services/cloud-services-applications/azure-expressroute/)** |Supportato |Supportato |Melbourne, Sydney |
| **[Airtel](http://www.airtel.in/business/connexion)** | Supportato | Supportato | Chennai, Mumbai |
| **[Aryaka Networks](http://www.aryaka.com/)** |Supportato |Supportato |Amsterdam, Dallas, Hong Kong, Silicon Valley, Singapore, Tokyo, Washington DC |
| **[Ascenty Data Centers](https://ascenty.com/solucoes/conectividade-e-interconexoes/Microsoft-express-route/)** |Presto disponibile |Presto disponibile |Sao Paulo |
| **[AT&T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |Supportato |Supportato |Amsterdam, Chicago, Dallas, Londra, Silicon Valley, Singapore, Sydney, Tokyo, Toronto, Washington DC |
| **[Bell Canada](https://business.bell.ca/shop/enterprise/cloud-connect-access-to-cloud-partner-services)** |Supportato |Supportato |Montreal, Toronto |
| **[British Telecom](http://www.globalservices.bt.com/uk/en/news/bt_to_provide_connectivity_to_microsoft_azure)** |Supportato |Supportato |Amsterdam, Hong Kong, Londra, Silicon Valley, Singapore, Sydney, Tokyo, Washington DC |
| **[CenturyLink](http://www.centurylink.com/business/enterprise/services/data-network/mpls-vpn.html)** |Presto disponibile |Presto disponibile |Silicon Valley |
| **China Telecom Global** |Supportato |Non supportato |Hong Kong |
| **[Cologix](http://www.cologix.com/solutions/cloud-connect/public-clouds/microsoft-cloud/)** |Supportato |Supportato |Dallas, Montreal, Toronto |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |Supportato |Supportato |Amsterdam, Dublino, Londra, Parigi, Tokyo |
| **Comcast** |Supportato |Supportato |Chicago, Silicon Valley, Washington DC |
| **[Console](https://www.consoleconnect.com/partners/cloudsaas/)**| Supportato | Supportato |Silicon Valley, Toronto |
| **[CoreSite](http://www.coresite.com/solutions/cloud-services/public-cloud-providers/microsoft-azure-expressroute)** |Supportato |Supportato |Denver, Los Angeles, New York |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |Supportato |Supportato |Amsterdam, Atlanta, Chicago, Dallas, Hong Kong, Londra, Los Angeles, Melbourne, New York, Osaka, Parigi, San Paolo, Seattle, Silicon Valley, Singapore, Sydney, Tokyo, Toronto, Washington DC |
| **euNetworks** |Supportato |Supportato |Amsterdam |
| **GÉANT** |Supportato |Supportato |Amsterdam |
| **[Global Cloud Xchange (GCX)] (http://globalcloudxchange.com/cloud-platform/cloud-x-fusion/cloud-x-fusion-for-azure/)** | Supportato| Supportato | Chennai |
| **[InterCloud](https://www.intercloud.com/)** |Supportato |Supportato |Amsterdam, Londra, Singapore, Washington DC |
| **[Internet Initiative Japan Inc. - IIJ](http://www.iij.ad.jp/en/news/pressrelease/2015/1216-2.html)** |Supportato |Supportato |Osaka, Tokyo |
| **Internet Solutions - Cloud Connect** |Supportato |Supportato |Amsterdam, Londra |
| **[Interxion](http://www.interxion.com/why-interxion/colocate-with-the-clouds/Microsoft-Azure/)** |Supportato |Supportato |Amsterdam, Dublino, Londra, Parigi |
| **Jisc** |Supportato |Supportato |Londra |
| **KINX** |Supportato |Supportato |Seul |
| **[KPN](http://www.kpn.com/cloudconnect)** | Supportato | Supportato | Amsterdam | 
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |Supportato |Supportato |Amsterdam, Chicago, Dallas, Las Vegas, Londra, San Paolo, Seattle, Silicon Valley, Singapore, Washington DC |
| **LG CNS** |Supportato |Supportato |Busan, Seoul |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Supportato |Supportato |Amsterdam, Chicago, Dallas, Hong Kong, Las Vegas, Londra, Los Angeles, Melbourne, Miami, New York, Quebec City, San Antonio, Seattle, Silicon Valley, Singapore, Sydney, Toronto, Washington DC |
| **MTN** |Supportato |Supportato |Londra |
| **[Neutrona Networks](http://www.neutrona.com/index.php/services#cloud-connect)** |Supportato |Supportato |Miami, Sao Paulo |
| **[Dati di nuova generazione](http://www.nextgenerationdata.co.uk/ngd-cloud-gateway/)** |Supportato |Supportato |Newport(Wales) |
| **NEXTDC** |Supportato |Supportato |Melbourne, Sydney |
| **[NTT Communications](http://www.ntt.com/en/services/network/virtual-private-network.html)** |Supportato |Supportato |Londra, Los Angeles, Osaka, Singapore, Tokyo, Washington DC |
| **[NTT SmartConnect](http://cloud.nttsmc.com/cxc/azure.html)** |Supportato |Supportato |Osaka |
| **[Orange](http://www.orange-business.com/en/products/business-vpn-galerie)** |Supportato |Supportato |Amsterdam, Hong Kong, Londra, Parigi, Silicon Valley, Singapore, Sydney, Washington DC |
| **PCCW Global Limited** |Supportato |Supportato |Hong Kong - R.A.S. |
| **Sejong Telecom** |Supportato |Supportato |Seul |
| **[SIFY](http://telecom.sify.com/azure-expressroute.html)** |Supportato |Supportato |Chennai |
| **[SingTel](http://info.singtel.com/about-us/news-releases/singtel-provide-secure-private-access-microsoft-azure-public-cloud)** |Supportato |Supportato |Singapore |
| **[Softbank](http://www.softbank.jp/biz/cloud/cloud_access/direct_access_for_az/)** |Supportato |Supportato |Osaka, Tokyo |
| **[Tata Communications](http://www.tatacommunications.com/lp/izo/azure/azure_index.html)** |Supportato |Supportato |Amsterdam, Chennai, Hong Kong, Londra, Mumbai, Silicon Valley, Singapore, Washington DC |
| **[TeleCity Group](http://www.telecitygroup.com/investor-centre/news_details.htm?locid=03100500400b00d&xml)** |Supportato |Supportato |Amsterdam, Dublino, Londra |
| **[Telefonica](https://www.business-solutions.telefonica.com/es/enterprise/solutions/efficient-infrastructure/managed-voice-data-connectivity/)** |Supportato |Supportato |Amsterdam, San Paolo |
| **[Telehouse - KDDI](http://www.telehouse.net/solutions/cloud-services/cloud-link)** |Supportato |Supportato |Londra |
| **Telenor** |Supportato |Supportato |Amsterdam, Londra |
| **[Telstra Corporation](http://www.telstra.com.au/business-enterprise/network-services/networks/cloud-direct-connect/)** |Supportato |Supportato |Melbourne, Sydney |
| **[Telus](http://www.telus.com)** |Supportato |Supportato |Toronto |
| **[UOLDIVEO](http://www.uoldiveo.com.br/solucoes/cloud.html#rmcl)** |Supportato |Supportato |Sao Paulo |
| **[Verizon](http://www.verizonenterprise.com/products/networking/secure-cloud-interconnect/)** |Supportato |Supportato |Amsterdam, Chicago, Dallas, Hong Kong, Londra, Silicon Valley, Singapore, Sydney, Tokyo, Washington DC |
| **[Vodafone](http://www.vodafone.com/business/global-enterprise/global-connectivity/vodafone-ip-vpn-cloud-connect)** |Supportato |Non supportato |Londra |
| **[Zayo Group](http://www.zayo.com/solutions/industries/cloud-connectivity/microsoft-expressroute)** |Supportato |Supportato |Amsterdam, Chicago, Dallas+, Londra+, Los Angeles, New York, Silicon Valley, Toronto, Washington DC |

 **+** indica disponibile a breve

### <a name="national-cloud-environment"></a>Ambiente cloud nazionale

### <a name="us-government-cloud"></a>Cloud del governo degli Stati Uniti
| **Provider di servizi** | **Microsoft Azure** | **Office 365** | **Località** |
| --- | --- | --- | --- |
| **[AT&amp;T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |Supportato |Supportato |Chicago, Washington DC |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |Supportato |Supportato |Chicago, Dallas, New York, Seattle, Silicon Valley, Washington DC |
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |Supportato |Supportato |Chicago, New York+, Silicon Valley, Washington DC |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Supportato | Supportato | Chicago, Dallas |
| **[Verizon](http://news.verizonenterprise.com/2014/04/secure-cloud-interconnect-solutions-enterprise/)** |Supportato |Supportato |Chicago, Dallas, New York, Washington DC |

### <a name="china"></a>Cina
| **Provider di servizi** | **Microsoft Azure** | **Office 365** | **Località** |
| --- | --- | --- | --- |
| **China Telecom** |Supportato |Non supportato |Pechino, Shanghai |

vedere, più toolearn [ExpressRoute in Cina](http://www.windowsazure.cn/home/features/expressroute/).

### <a name="germany"></a>Germania
| **Provider di servizi** | **Microsoft Azure** | **Office 365** | **Località** |
| --- | --- | --- | --- |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |Supportato |Non supportato |Berlino+, Francoforte |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |Supportato |Non supportato |Francoforte |
| **[e-shelter](https://www.e-shelter.de/en/microsoft-expressroutetm)** |Supportato |Non supportato |Berlino |
| **Interxion** |Supportato |Non supportato |Francoforte |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Supportato  | Non supportato | Berlino |
| **T-Systems** |Supportato |Non supportato |Berlino |

## <a name="connectivity-through-exchange-providers"></a>Connettività con provider di scambio

Se il provider di connettività non è incluso nelle sezioni precedenti, sarà comunque possibile creare una connessione.

* Se sono connessi tooany di scambi di hello nella precedente tabella hello, verificare con il toosee di provider di connettività. È possibile verificare l'esempio hello collega toogather ulteriori informazioni sui servizi offerti dai provider di exchange. Diversi provider di connettività sono già connessi tooEthernet scambi.
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [Interxion](http://www.interxion.com/products/interconnection/cloud-connect/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [NEXTDC](http://www.nextdc.com/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* Dispone il provider di servizi di estendere il percorso di peering toohello rete di scelta.
  * Assicurarsi che il provider di connettività estenda la connettività con disponibilità elevata, in modo che non siano presenti singoli punti di errore.
* Ordinare un circuito ExpressRoute con exchange hello come provider di connettività tooconnect tooMicrosoft.
  * Seguire i passaggi in [creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) tooset della connettività.

## <a name="connectivity-through-additional-service-providers"></a>Connettività con provider di servizi aggiuntivi

| **Provider di connettività** | **Exchange** | **Località** |
| --- | --- | --- |
| **[1CLOUDSTAR](http://www.1cloudstar.com/service/cloudconnect-azure-expressroute/)** |Equinix |Singapore |
| **[Airgate Technologies, Inc.](http://airgate.ca/cloud-express/)** | Equinix, Cologix | Toronto, Montreal |
| **[Alaska Communications](http://www.alaskacommunications.com/For-Your-Business/Direct-Cloud-Service)** |Equinix |Seattle |
| **[Altice Business](https://golightpath.com/transport)** |Equinix |New York, Washington DC |
| **[Arteria Networks Corporation](https://arteria-net.com/business/service/cloud_access/sca/)** |Equinix |Tokyo |
| **[Bezeq International Ltd.](https://www.bezeqint.net/english)** | euNetworks | Londra |
| **[BroadBand Tower, Inc.](http://www.bbtower.co.jp/product-service/data-center/network/dcconnect-for-azure/)** | Equinix | Tokyo |
| **[C3ntro Telecom](http://www.c3ntro.com/data/cloud-conectivity/)** | Equinix, Megaport | Dallas |
| **[Cogeco Peer 1](https://www.cogecopeer1.com/en/)**| Equinix | Montreal, Toronto |
| **[Cox Business](https://www.cox.com/business/networking/cloud-connectivity.html)** | Equinix | Dallas, Silicon Valley, Washington DC | 
| **[Data Foundry](https://www.datafoundry.com/services/cloud-connect)** | Megaport | Dallas |
| **[Epsilon Telecommunications Limited](http://www.epsilontel.com/data-connectivity/cloud-access/)** | Equinix | Londra, Singapore, Washington DC |
| **[Eurofiber](https://eurofiber.nl/microsoft-azure/)** | Equinix | Amsterdam |
| **[Esponenziale E](http://www.exponential-e.com/services/connectivity-services/cloud-connect-exchange)** | Equinix | Londra |
| **[Fastweb S.p.A](http://www.fastweb.it/grandi-aziende/connessione-voce-e-wifi/scheda-prodotto/rete-privata-virtuale/)** | Equinix | Amsterdam |
| **[Gtt Communications Inc](https://www.gtt.net/wp-content/uploads/2017/04/EtherCloud-Data-Sheet.pdf)** |Equinix | Washington DC |
| **[HSO](http://www.hso.co.uk/products/cloud-direct)** |Equinix | Londra, Slough |
| **LGA Telecom** |Equinix |Singapore|
| **[Lightower](http://www.lightower.com/network-solutions/cloud-connect/#microsoft-azure)** |Equinix | Chicago, New York, Washington DC |
| **[Macroview Telecom](http://www.macroview.com/en/scripts/catitem.php?catid=solution&sectionid=expressroute)** |Equinix |Hong Kong - R.A.S. |
| **[Macquarie Telecom Group](https://macquariegovernment.com/secure-cloud/secure-cloud-exchange/)** | Megaport | Sydney |
| **[Masergy](https://www.masergy.com/solutions/hybrid-networking/cloud-marketplace/microsoft-azure)** | Equinix | Washington DC |
| **[NexGen Networks](http://www.nexgen-net.com/nexgen-networks-direct-connect-microsoft-azure-expressroute.html)** | Interxion | Londra |
| **[Nianet](https://nianet.dk/produkter/internet/microsoft-expressroute)** |Telecity | Amsterdam, Francoforte |  
| **[QSC AG](https://www.qsc.de/de/produkte-loesungen/cloud-services-und-it-outsourcing/pure-enterprise-cloud/multi-cloud-management/azure-expressroute/)** |Interxion | Francoforte |  
| **Rogers** | Cologix, Equinix | Montreal, Toronto |
| **[Tamares Telecom](http://www.tamarestelecom.com/our-services/#Connectivity)** | Telecity | Londra | 
| **[ThinkTel](http://www.thinktel.ca/services/agile-ix-data/expressroute/)** | Equinix | Toronto | 
| **[Transtelco](http://www.transtelco.net/tcloud/microsoft)** |Equinix | Dallas, Los Angeles |  
| **[United Information Highway (UIH)](https://www.uih.co.th/en/internet-solution/cloud-direct/uih-cloud-direct-for-microsoft-azure-expressroute)**| Equinix | Singapore |
| **[Webair](https://www.webair.com/microsoft-express-route-partnership/)**| Megaport | New York |
| **[Windstream](http://www.windstreambusiness.com/solutions/cloud-services/cloud-and-managed-hosting-services)**| Equinix | Chicago, Silicon Valley, Washington DC |
| **Zain** |Equinix |Londra|
| **[Zertia](http://www.zertia.es/index.php/novedades)**| Level 3 | Madrid |
| **[Zirro](https://zirro.com/services/)**| Equinix | Montreal, Toronto |

## <a name="connectivity-through-datacenter-providers"></a>Connettività con provider di data center
| **Provider** | **Exchange** |
| --- | --- |
| **[Cyrus One](https://cyrusone.com/enterprise-data-center-services/connectivity-and-interconnection/cloud-connectivity-reaching-amazon-microsoft-google-and-more/microsoft-azure-expressroute/?doing_wp_cron=1498512235.6733090877532958984375)** | Megaport |
| **[Digital Realty](https://www.digitalrealty.com/services/interconnection/service-exchange/)** | Megaport |
| **[EdgeConnex](http://www.edgeconnex.com/services/edge-data-centers-proximity-matters/)** | Megaport |
| **[RagingWire Data Centers](http://www.ragingwire.com/wholesale/wholesale-data-centers-worldwide-nexcenters)** | Console |
| **[T5 Datacenters](http://t5datacenters.com/network-cloud-connect/)** | Console |

## <a name="connectivity-through-national-research-and-education-networks-nren"></a>Connettività con le reti nazionali per la ricerca e l'istruzione

| **Provider**|
| --- |
| **AARNET**| 
| **DeIC, tramite GÉANT**|
| **GARR, tramite GÉANT**|
| **GÉANT**|
| **HEAnet, tramite GÉANT**|
| **JISC**|
| **RedIRIS, tramite GÉANT**|
| **SINET**|
| **Surfnet, tramite GÉANT**|

* Se il provider di connettività non è elencato, verificare toosee se sono connessi tooany di hello che expressroute Exchange partner elencati in precedenza.

## <a name="expressroute-system-integrators"></a>Integratori di sistemi ExpressRoute
Abilitazione toofit connettività privata che possono essere difficile le proprie esigenze, in base alla scala di hello della rete. Si può funzionare con qualsiasi di hello integratori di sistema elencati nella seguente tabella tooassist hello è con tooExpressRoute onboarding.

| **Integratore di sistemi** | **Continente** |
| --- | --- |
| **[Altogee](http://www.altogee.be/expressroute)** | Europa |
| **[Avanade Inc.](http://www.avanade.com/)** | Asia, Europa, America del Nord, America del Sud |
| **[Bright Skies GmbH](http://bskies.io/expressroute)** | Europa
| **[Ensyst](http://www.ensyst.com.au)** | Asia
| **[Equinix Professional Services](http://www.equinix.com/services/consulting/)** | America del Nord |
| **[FlexManage](http://www.flexmanage.com/cloud)** | America del Nord |
| **[Inframon](http://www.inframon.com/partner/microsoft/)** | Europa |
| **[Hello gruppo consulenza IT](http://itconsult.com.au/microsoft-expressroute)** | Australia |
| **[MOQdigital](http://www.moqdigital.com.au/insights/technical/network-connectivity-options-for-azure)** | Australia |
| **[MSG Services](https://www.msg-services.de/it-services/managed-services/cloud-outsourcing/)** | Europa (Germania) |
| **[Nelite](http://nelite.com/)** | Europa |
| **[New Signature](https://www.newsignature.co.uk/)** | Europa |
| **[OneAs1a](http://www.oneas1a.com/express-connect-any-cloud-ecac)** | Asia |
| **[Orange Networks](https://orange-networks.com/blog/88-azureexpressroute)** | Europa |
| **[Perficient](http://www.perficient.com/Partners/Microsoft/Cloud/Azure-ExpressRoute)** | America del Nord |
| **[Presidio](http://info.presidio.com/microsoft-azure-expressroute)** | America del Nord |
| **[sol-tec](http://www.sol-tec.com/Technologies)** | Europa |
| **[Vigilant.IT](https://vigilant.it/expressroute)** | Australia |


## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
* Verificare che vengano soddisfatti tutti i prerequisiti. Vedere [Prerequisiti per ExpressRoute](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Mappa delle località"
