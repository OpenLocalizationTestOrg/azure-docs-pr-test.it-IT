---
title: domande frequenti per Azure applicazione Gateway aaaFrequently | Documenti Microsoft
description: Questa pagina vengono fornite le risposte toofrequently domande frequenti sul Gateway applicazione Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Domande frequenti sul gateway applicazione

## <a name="general"></a>Generale

**D. Che cos'è il gateway applicazione?**

Il gateway applicazione di Azure è un servizio di controller per la distribuzione di applicazioni (ADC) con numerose funzionalità di bilanciamento del carico di livello 7. Offre un servizio altamente disponibile e scalabile completamente gestito da Azure.

**D. Quali funzionalità supporta il gateway applicazione?**

Gateway applicazione supporta SSL tooend end e di offload SSL, Web Application Firewall, affinità di sessione basato su cookie, url basato sul percorso routing, hosting di più siti e altri utenti. Per un elenco completo delle funzionalità supportate, visitare [tooApplication introduzione Gateway](application-gateway-introduction.md)

**D. Qual è la differenza hello tra il Gateway di applicazione e servizio di bilanciamento del carico di Azure?**

Il gateway applicazione è un servizio di bilanciamento del carico di livello 7 e funziona quindi solo con il traffico Web (HTTP/HTTPS/WebSocket). Supporta funzionalità come terminazione SSL, affinità di sessione basata su cookie e round robin per il bilanciamento del carico del traffico. Load Balancer esegue il bilanciamento del carico del traffico al livello 4 (TCP/UDP).

**D. Quali protocolli supporta il gateway applicazione?**

Il gateway applicazione supporta HTTP, HTTPS e WebSocket.

**D. Quali risorse sono supportate oggi nell'ambito del pool back-end?**

I pool back-end possono essere costituiti da schede di interfaccia di rete, set di scalabilità di macchine virtuali, indirizzi IP pubblici, indirizzi IP interni, nomi di dominio completi (FQDN) e back-end multi-tenant come App Web di Azure. Gateway applicazione non sono membri del pool back-end legati tooan set di disponibilità. I membri del pool back-end possono trovarsi tra cluster, data center o all'esterno di Azure, purché abbiano connettività IP.

**D. Le aree è disponibile nel servizio di hello?**

Il gateway applicazione è disponibile in tutte le aree di Azure globale. È anche disponibile in [Azure Cina](https://www.azure.cn/) e [Azure per enti pubblici](https://azure.microsoft.com/en-us/overview/clouds/government/)

**D. Si tratta di una distribuzione dedicata per la sottoscrizione o è condivisa tra clienti?**

Il gateway applicazione è una distribuzione dedicata nella rete virtuale.

**D. È supportato il reindirizzamento HTTP->HTTPS?**

Il reindirizzamento è supportato. Visitare [Panoramica di reindirizzamento Gateway applicazione](application-gateway-redirect-overview.md) toolearn altre.

**D. In quale ordine vengono elaborati i listener?**

I listener vengono elaborati in ordine di hello che vengono visualizzati. Per tale motivo, se un listener di base corrisponde a una richiesta in ingresso, questa viene elaborata per prima.  Multisito listener devono essere configurate prima un traffico tooensure base listener è indirizzato toohello corretto back-end.

**D. Dove è possibile trovare IP e DNS del gateway applicazione?**

Quando si utilizza un indirizzo IP pubblico come un endpoint, queste informazioni sono reperibile nella risorsa di indirizzo IP pubblica hello o nella pagina di panoramica hello per hello Gateway applicazione nel portale di hello. Per gli indirizzi IP interni, si trova nella pagina di panoramica hello.

**D. Hello IP o DNS modifica nel corso della durata di Gateway applicazione hello hello?**

Hello VIP può cambiare se gateway hello viene arrestato e avviato dal cliente hello. Hello DNS associato al Gateway applicazione non cambia nel ciclo di vita di hello del gateway hello. Per questo motivo, è consigliabile toouse un alias CNAME e indirizzarlo toohello dell'indirizzo DNS del Gateway applicazione hello.

**D. Il gateway applicazione supporta l'IP statico?**

No, il gateway applicazione non supporta indirizzi IP pubblici statici, ma supporta indirizzi IP interni statici.

**D. Gateway applicazione supporta più indirizzi IP pubblici nel gateway hello?**

Il gateway applicazione supporta un solo indirizzo IP pubblico.

**D. Il gateway applicazione supporta le intestazioni x-forwarded-for?**

Sì, Gateway applicazione inserisce x-inoltrati-per, proto inoltrati x e porta inoltrati x di intestazioni nella richiesta di hello inoltrati toohello di back-end. formato di Hello per l'intestazione x-inoltrati-per è un elenco delimitato da virgole di creato. i valori validi di Hello per proto inoltrati x sono http o https. Porta inoltrati X specifica porta hello quali richiesta hello raggiunto al Gateway applicazione hello.

**D. Quanto tempo occorre toodeploy un Gateway applicazione? Il gateway applicazione funziona durante l'aggiornamento?**

Nuove distribuzioni di Gateway applicazione possono richiedere too20 minuti tooprovision. Le modifiche tooinstance di conteggio/dimensioni non siano distruttive e gateway hello rimane attiva durante l'operazione.

## <a name="configuration"></a>Configurazione

**D. Il gateway applicazione viene sempre distribuito in una rete virtuale?**

Sì, il gateway applicazione viene sempre distribuito in una subnet di rete virtuale. Questa subnet può contenere solo gateway applicazione.

**D. Gateway applicazione possono comunicare con tooinstances all'esterno della rete virtuale?**

Gateway applicazione in grado di comunicare tooinstances all'esterno di rete virtuale hello in esso contenuto, purché vi sia connettività IP. Se si prevede di toouse richiede indirizzi IP interni come membri del pool back-end, verrà [Peering reti VIRTUALI](../virtual-network/virtual-network-peering-overview.md) o [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**D. È possibile distribuire qualsiasi altro elemento nella subnet del Gateway applicazione hello?**

No, ma è possibile distribuire altri gateway applicazione nella subnet hello.

**D. Gruppi di sicurezza di rete sono supportati nella subnet del Gateway applicazione hello?**

Gruppi di sicurezza di rete sono supportati nella subnet del Gateway applicazione hello con hello seguenti restrizioni:

* Le eccezioni devono essere inserite per il traffico in ingresso sulle porte 65503 65534 per toowork integrità back-end in modo corretto.

* La connettività Internet in uscita non può essere bloccata.

* È necessario consentire il traffico proveniente da hello tag AzureLoadBalancer.

**D. Quali sono i limiti di hello gateway applicazione? È possibile aumentare questi limiti?**

Visitare [limiti di Gateway applicazione](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limiti.

**D. È possibile usare il gateway applicazione per il traffico interno ed esterno contemporaneamente?**

Sì, il gateway applicazione supporta un indirizzo IP interno e un indirizzo IP esterno.

**D. Il peering reti virtuali è supportato?**

Sì, il peering reti virtuali è supportato ed è utile per il bilanciamento del carico del traffico in altre reti virtuali.

**D. È possibile contattare i server locali tooon quando sono connessi da tunnel VPN o ExpressRoute?**

Sì, se il traffico è consentito.

**D. È possibile avere un pool back-end che serve molte applicazioni su porte diverse?**

L'architettura di microservizi è supportata. Occorre più tooprobe configurate impostazioni di http su porte diverse.

**D. I probe personalizzati supportano caratteri jolly o regex nei dati di risposta?**

I probe personalizzati non supportano caratteri jolly o regex nei dati di risposta. 

**D. Come vengono elaborate le regole?**

Le regole vengono elaborate nell'ordine di hello che sono configurati. È consigliabile che le regole di multi-sito siano configurate prima possibilità di hello tooreduce regole di base che il traffico viene instradato back-end inappropriato toohello come regola di base hello corrisponderebbe traffico in base alla regola di porta multisito toohello precedente viene valutato.

**D. Come vengono elaborate le regole?**

Le regole vengono elaborate in ordine di hello che sono stati creati. È consigliabile configurare le regole multisito prima delle regole di base. Configurando innanzitutto listener multisito, questa configurazione riduce il possibilità hello che il traffico sia indirizzato toohello inappropriato backend. Come regola di base hello corrisponderebbe traffico in base alla regola di porta multisito toohello precedente viene valutata, può verificarsi questo problema di routing.

**D. Cosa indicano il campo Host hello per le ricerche personalizzate?**

Il campo host specifica hello Nome toosend hello probe. Applicabile solo quando vengono configurati più siti nel gateway applicazione. In caso contrario, usare "127.0.0.1". Questo valore è diverso dal nome host della VM ed è nel formato \<protocollo\>://\<host\>:\<porta\>\<percorso\>.

**D. È possibile whitelist Gateway applicazione accesso tooa alcuni indirizzi IP di origine?**

Questo scenario è possibile usando gruppi di sicurezza di rete nella subnet del gateway applicazione. nella subnet hello in hello all'ordine di priorità, è necessario inserire Hello seguenti restrizioni:

* Consentire il traffico in ingresso dall'intervallo di IP/IP di origine.

* Consentire le richieste in ingresso da tutte le origini tooports 65503 65534 per [comunicazione integrità back-end](application-gateway-diagnostics.md).

* Consentire hello in arrivo probe di bilanciamento del carico di Azure (tag AzureLoadBalancer) e traffico di rete virtuale in ingresso (tag VirtualNetwork) [NSG](../virtual-network/virtual-networks-nsg.md).

* Bloccare tutto il traffico in ingresso con una regola Nega tutto.

* Consentire il traffico in uscita toohello internet per tutte le destinazioni.

## <a name="performance"></a>Prestazioni

**D. In che modo il gateway applicazione supporta la disponibilità elevata e la scalabilità?**

Il gateway applicazione supporta scenari di disponibilità elevata se sono presenti due o più istanze distribuite. Azure distribuisce tali istanze tra tooensure di domini di aggiornamento e di errore che tutte le istanze non viene in hello contemporaneamente. Gateway applicazione supporta la scalabilità mediante l'aggiunta di più istanze di hello stesso carico di hello tooshare gateway.

**D. Come si ottiene uno scenario di ripristino di emergenza tra data center con un gateway applicazione?**

I clienti possono utilizzare toodistribute Traffic Manager il traffico tra più applicazioni gateway in diversi Data Center.

**D. La scalabilità automatica è supportata?**

No, ma Gateway applicazione dispone di una metrica di velocità effettiva che può essere utilizzato tooalert quando viene raggiunta una soglia. Manualmente le istanze di aggiunta o modifica delle dimensioni non viene riavviato gateway hello e non influisce sulla traffico esistente.

**D. Il ridimensionamento manuale causa tempi di inattività?**

Non si verificano tempi di inattività, le istanze vengono distribuite tra domini di aggiornamento e domini di errore.

**D. È possibile modificare le dimensioni di istanza da medium toolarge senza interruzioni?**

Sì, Azure distribuisce le istanze in tooensure di domini di aggiornamento e di errore che tutte le istanze non viene in hello contemporaneamente. Supporta il Gateway applicazione ridimensionamento aggiungendo più istanze di hello stesso carico di hello tooshare gateway.

## <a name="ssl-configuration"></a>Configurazione SSL

**D. Quali certificati sono supportati dal gateway applicazione?**

Sono supportati certificati autofirmati, certificati della CA e certificati con caratteri jolly. I certificati di convalida estesa non sono supportati.

**D. Quali sono hello corrente pacchetti di crittografia supportati dal Gateway applicazione?**

di seguito Hello sono hello corrente pacchetti di crittografia supportati dal gateway applicazione. Visita: [Configura SSL le versioni dei criteri e i pacchetti di crittografia nel Gateway applicazione](application-gateway-configure-ssl-policy-powershell.md) toolearn come opzioni SSL toocustomize.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**D. Gateway applicazione supporta inoltre la riesecuzione della crittografia di back-end toohello traffico?**

Sì, offload SSL di Gateway applicazione supporta e fine tooend SSL, che crittografa nuovamente hello back-end toohello di traffico.

**D. È possibile configurare le versioni protocollo SSL toocontrol dei criteri SSL?**

Sì, è possibile configurare il Gateway applicazione toodeny TLS 1.0, TLS 1.1 e TLS 1.2. SSL 2.0 e 3.0 sono già disabilitati per impostazione predefinita e non sono configurabili.

**D. È possibile configurare l'ordine dei pacchetti di crittografia e dei criteri?**

Sì, la [configurazione dei pacchetti di crittografia](application-gateway-ssl-policy-overview.md) è supportata. Quando si definisce un criterio personalizzato, almeno uno dei seguenti pacchetti di crittografia hello deve essere abilitato. Gateway applicazione utilizza la gestione di back-end toofor SHA256.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**D. Quanti certificati SSL sono supportati?**

Configurazione SSL too20 sono supportati i certificati.

**D. Quanti certificati di autenticazione sono supportati per la ripetizione della crittografia nel back-end?**

Backup too10 certificati di autenticazione sono supportati con un valore predefinito è 5.

**D. Il gateway applicazione si integra con Azure Key Vault in modo nativo?**

No, non è integrato con Azure Key Vault.

## <a name="web-application-firewall-waf-configuration"></a>Configurazione del Web application firewall (WAF)

**D. Hello SKU WAF offre tutte le funzionalità di hello disponibili con hello SKU Standard?**

Sì, WAF supporta tutte le funzionalità di hello hello SKU Standard.

**D. Qual è la versione di hello CRS che supporta Gateway applicazione?**

Il gateway applicazione supporta CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**D. Come si monitora il Web application firewall?**

Il Web application firewall viene monitorato tramite la registrazione diagnostica. Per altre informazioni sulla registrazione diagnostica, vedere [Integrità back-end, registrazione diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md)

**D. La modalità di rilevamento blocca il traffico?**

No, la modalità di rilevamento registra solo il traffico che ha attivato una regola del Web application firewall.

**D. Come si personalizzano le regole del Web application firewall?**

Sì, le regole di WAF sono personalizzabili, per ulteriori informazioni su come essi toocustomize visitare [WAF personalizzare regole e gruppi di regole](application-gateway-customize-waf-rules-portal.md)

**D. Quali regole sono attualmente disponibili?**

WAF supporta attualmente CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), che forniscono la protezione di base con la maggior parte delle hello vulnerabilità primi 10 identificata da hello aprire Web applicazione sicurezza progetto (OWASP) fare clic qui [OWASP le prime 10 vulnerabilità](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* Protezione dagli attacchi SQL injection

* Protezione dagli attacchi di scripting intersito

* Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion

* Protezione dalle violazioni del protocollo HTTP

* Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header

* Prevenzione contro robot, crawler e scanner

* Rilevamento di errori di configurazione dell'applicazione comuni (ad esempio, Apache, IIS e così via)

**D. Il WAF supporta anche la prevenzione DDoS?**

No, non fornisce la prevenzione DDoS.

## <a name="diagnostics-and-logging"></a>Diagnostica e registrazione

**D. Quali tipi di log sono disponibili con il gateway applicazione?**

Sono disponibili tre log con il gateway applicazione. Per altre informazioni su questi log e altre funzionalità di diagnostica, vedere [Integrità back-end, log di diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** -log di accesso hello contiene ogni richiesta inviata front-end di Gateway applicazione toohello. dati Hello includono IP del chiamante hello, URL richiesto, latenza nella risposta, codice restituito, byte e la disconnessione. Il log di accesso viene raccolto ogni 300 secondi. Il log contiene un record per ogni istanza del gateway applicazione.
- **ApplicationGatewayPerformanceLog** -log delle prestazioni hello acquisisce informazioni sulle prestazioni per ogni istanza incluso richiesta totale servita, velocità effettiva in byte, numero totale di richieste servite, numero di richieste non riuscite, corretti e non corretti numero di istanze di back-end.
- **ApplicationGatewayFirewallLog** -log firewall hello contiene le richieste che vengono registrate tramite la modalità di rilevamento o prevenzione di un gateway di applicazione che viene configurato con firewall applicazione web.

**D. Come è possibile sapere se i membri del pool back-end sono integri?**

È possibile utilizzare i cmdlet di PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` o verificare l'integrità tramite il portale di hello visitando [diagnostica del Gateway applicazione](application-gateway-diagnostics.md)

**D. Che cos'è il criterio di conservazione hello nei log di diagnostica hello?**

Account di archiviazione di flusso toohello clienti di log di diagnostica e se è possono impostare i criteri di conservazione hello in base alle loro specificate. I log di diagnostica possono anche essere inviati tooan Hub eventi o Log Analitica. Vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md) per altri dettagli.

**D. Come si ottengono i log di controllo per il gateway applicazione?**

Sono disponibili log di controllo per il gateway applicazione. Nel portale di hello, fare clic su **Log attività** nel pannello menu hello di un log di controllo di Gateway applicazione tooaccess hello. 

**D. È possibile impostare avvisi con il gateway applicazione?**

Sì, il gateway applicazione supporta gli avvisi, che vengono configurati in base alle metriche.  Gateway applicazione dispone attualmente di una metrica di "trasmissione", che può essere configurato tooalert. toolearn informazioni su avvisi, visitare [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**D. L'integrità back-end restituisce uno stato sconosciuto. Quale potrebbe essere la causa?**

la causa più comune di Hello è back-end toohello di accesso è stato bloccato da un gruppo o un DNS personalizzato. Visitare [back-end integrità, la registrazione diagnostica e metriche per il Gateway applicazione](application-gateway-diagnostics.md) toolearn altre.

## <a name="next-steps"></a>Passaggi successivi

informazioni sul Gateway applicazione visitare toolearn [tooApplication introduzione Gateway](application-gateway-introduction.md).
