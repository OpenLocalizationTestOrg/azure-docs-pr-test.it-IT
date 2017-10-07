---
title: Cenni preliminari sulle connessioni aaaHybrid | Documenti Microsoft
description: Informazioni sulle connessioni ibride, sulla sicurezza, sulle porte TCP e sulle configurazioni supportate. MABS, WABS.
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: 216e4927-6863-46e7-aa7c-77fec575c8a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: f092c6019aae761e1e73f13d1af8446a896515c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-connections-overview"></a>Panoramica delle connessioni ibride

> [!IMPORTANT]
> La funzionalità Connessioni ibride di BizTalk è stata ritirata e sostituita dalla funzionalità Connessioni ibride del Servizio app. Per ulteriori informazioni, incluso come toomanage le connessioni ibride di BizTalk esistente, vedere [le connessioni ibride di servizio App di Azure](../app-service/app-service-hybrid-connections.md).

Introduzione tooHybrid connessioni, vengono elencate le configurazioni di hello è supportato e gli elenchi di hello porte TCP richieste.

## <a name="what-is-a-hybrid-connection"></a>Informazioni sulle connessioni ibride
La funzionalità Connessioni ibride è inclusa in Servizi BizTalk di Azure. Le connessioni ibride forniscono una funzionalità di App Web semplice e pratico tooconnect hello in Azure App Service (in precedenza i siti Web) e funzionalità di App per dispositivi mobili hello le risorse locali tooon di servizio App di Azure (precedentemente noti come servizi mobili) dietro il firewall.

![connessioni ibride][HCImage]

Vantaggi della funzionalità Connessioni ibride:

* App Web e app per dispositivi mobili possono accedere ai dati e ai servizi locali esistenti in modo sicuro.
* Più applicazioni Web o App per dispositivi mobili possono condividere un tooaccess connessione ibrida una risorsa locale.
* Porte TCP minimo sono necessari tooaccess della rete.
* Le applicazioni mediante connessioni ibride accedere solo i risorsa locale specifico hello pubblicata tramite la connessione ibrida hello.
* Possibile connettere una risorsa locale tooany che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e la maggior parte dei servizi Web personalizzati.
  
  > [!NOTE]
  > I servizi basati su TCP che usano porte dinamiche, ad esempio la modalità FTP passiva o la modalità passiva estesa, non sono attualmente supportati. Anche LDAP non è supportato. LDAP usa una porta TCP statica, ma può anche usare UDP. Di conseguenza, non è supportato.
  > 
  > 
* È possibile usare la funzionalità con tutti i framework supportati da App Web (.NET, PHP, Java, Python, Node.js) e App per dispositivi mobili (Node.js, .NET).
* Le applicazioni Web e App per dispositivi mobili possono accedere alle risorse locali esattamente hello stesso modo come se hello Web o App per dispositivi mobili si trova nella rete locale. Ad esempio, hello stessa stringa di connessione locale utilizzati possono essere utilizzati anche in Azure.

Le connessioni ibride forniscono anche gli amministratori dell'organizzazione con un controllo e visibilità alle risorse aziendali hello accede applicazioni ibride, tra cui:

* Impostazioni dei criteri di gruppo, gli amministratori possono consentire le connessioni ibride rete hello e inoltre definire le risorse che è possibile accedere tramite applicazioni ibride.
* I registri eventi e di controllo nella rete aziendale hello forniscono visibilità risorse hello a cui accedono le connessioni ibride.

## <a name="example-scenarios"></a>Scenari di esempio
Le connessioni ibride supportano hello seguenti combinazioni di applicazione e di framework:

* .NET framework accesso tooSQL Server
* Servizi di .NET framework accesso tooHTTP/HTTPS con WebClient
* PHP accesso tooSQL Server, MySQL
* Java accesso tooSQL Server, MySQL e Oracle
* Servizi di linguaggio accesso tooHTTP/HTTPS

Quando le connessioni ibride tooaccess utilizzando SQL Server locale, prendere in considerazione seguente hello:

* Denominato istanze di SQL Express deve essere configurato toouse le porte statiche. Per impostazione predefinita, le istanze denominate di SQL Express usano le porte dinamiche.
* Le istanze predefinite di SQL Express usano porte statiche, ma è necessario abilitare il protocollo TCP. Per impostazione predefinita, il protocollo TCP non è abilitato.
* Quando si usa Clustering o gruppi di disponibilità, hello `MultiSubnetFailover=true` modalità attualmente non è supportata.
* Hello `ApplicationIntent=ReadOnly` non è attualmente supportato.
* L'autenticazione di SQL potrebbe essere necessario come metodo di autorizzazione end-to-end hello supportato dall'applicazione Azure hello e hello on-premise SQL server.

## <a name="security-and-ports"></a>Sicurezza e porte
Le connessioni ibride utilizzano connessioni hello toosecure autorizzazione di firma di accesso condiviso (SAS) da hello Azure hello e applicazioni in locale la connessione ibrida toohello Hybrid Connection Manager. Vengono create le chiavi di connessione separata per un'applicazione hello e hello locale di Hybrid Connection Manager. È possibile eseguire il rollover e revocare queste chiavi di connessione in modo indipendente.

Le connessioni ibride forniscono per la distribuzione sicura e uniforme di applicazioni di toohello chiavi hello e hello locale di Hybrid Connection Manager.

Vedere [Creare e gestire connessioni ibride](integration-hybrid-connection-create-manage.md).

*Autorizzazione dell'applicazione è separata dalla connessione ibrida hello*. È possibile usare qualsiasi metodo di autorizzazione appropriato. metodo di autorizzazione Hello dipende da metodi di autorizzazione end-to-end di hello in hello cloud di Azure e i componenti locali hello è supportati. Si supponga, ad esempio, che l'applicazione Azure acceda a un'istanza di SQL Server locale. In questo scenario, autorizzazione SQL può essere hello autorizzazione metodo supportati end-to-end.

#### <a name="tcp-ports"></a>Porte TCP
La funzionalità Connessioni ibride richiede solo la connettività TCP o HTTP in uscita dalla rete privata. Non si necessita di porte firewall tooopen o modificare il tooallow di configurazione di rete perimetrale qualsiasi connessione in ingresso nella rete.

Hello porte TCP seguenti viene utilizzato dalle connessioni ibride:

| Porta | Perché sono necessari |
| --- | --- |
| 9350 - 9354 |Queste porte vengono usate per la trasmissione dei dati. gestione di inoltro di Service Bus Hello le ricerche porta 9350 toodetermine se è disponibile la connettività TCP. Se è disponibile, presuppone che sia disponibile anche la porta 9352. Il traffico dati passerà per la porta 9352. <br/><br/>Consentire le connessioni in uscita porte toothese. |
| 5671 |Quando 9352 porta usata per il traffico di dati, come canale di controllo hello viene utilizzata la porta 5671. <br/><br/>Consentire le connessioni in uscita toothis porta. |
| 80, 443 |Queste porte vengono utilizzate per alcuni tooAzure le richieste di dati. Inoltre, se le porte 9352 e 5671 non sono utilizzabili, *quindi* porte 80 e 443 siano presenti porte di fallback hello utilizzate per la trasmissione dei dati e il canale di controllo di hello.<br/><br/>Consentire le connessioni in uscita porte toothese. <br/><br/>**Nota** non è consigliabile toouse questi hello porte fallback al posto di hello altre porte TCP. Hello HTTP o WebSocket viene utilizzato come protocollo di hello anziché TCP nativo per i canali di dati. Può comportare prestazioni ridotte. |

## <a name="next-steps"></a>Passaggi successivi
[Create and manage Hybrid Connections](integration-hybrid-connection-create-manage.md)<br/>
[Connettere le app Web di Azure tooan risorsa locale](../app-service-web/web-sites-hybrid-connection-get-started.md)<br/>
[Connettersi a SQL Server locale tooon da un'app web di Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)<br/>

## <a name="see-also"></a>Vedere anche
[REST API for Managing BizTalk Services on Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)
 (API REST per la gestione dei servizi BizTalk in Microsoft Azure)[Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md)<br/>
[Creazione di servizi BizTalk tramite il portale di Azure](biztalk-provision-services.md)<br/>
[Servizi BizTalk: schede Dashboard, Monitora e Scala](biztalk-dashboard-monitor-scale-tabs.md)<br/>

[HCImage]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionImage.png
[HybridConnectionTab]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-overview/WABS_HybridConnectionManageConn.png
