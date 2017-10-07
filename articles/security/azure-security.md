---
title: aaaIntroduction tooAzure sicurezza | Documenti Microsoft
description: Informazioni sulla sicurezza in Azure, sui relativi servizi e sul funzionamento.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/03/2017
ms.author: TomSh
ms.openlocfilehash: 2d42057e9586a0b6ce16a1582db3b3af842297af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security"></a>Introduzione tooAzure, sicurezza
## <a name="overview"></a>Panoramica
Sappiamo che sicurezza processo cloud hello e come sia importante che trovare informazioni accurate e aggiornate sulla sicurezza di Azure. Uno dei toouse delle ragioni migliore Azure di hello per le applicazioni e servizi è tootake sfruttare la sua vasta gamma di funzionalità e strumenti di sicurezza. Questi strumenti e funzionalità rendono toocreate possibili soluzioni di protezione sulla piattaforma Azure sicura hello. Microsoft Azure garantisce la riservatezza, l'integrità e la disponibilità dei dati dei clienti, assicurando anche al tempo stesso una rendicontazione trasparente.

toohelp è comprendere meglio insieme hello dei controlli di sicurezza implementata in Microsoft Azure da prospettive del cliente hello sia le operazioni di Microsoft, questo white paper "Introduzione tooAzure sicurezza", viene scritto tooprovide un analisi completa sicurezza hello disponibile con Microsoft Azure.

### <a name="azure-platform"></a>Piattaforma Azure
Azure è una piattaforma di servizi cloud pubblici che supporta un'ampia gamma di sistemi operativi, linguaggi di programmazione, framework, strumenti, database e dispositivi. Può eseguire contenitori Linux con integrazione con Docker, compilare app con JavaScript, Python, .NET, PHP, Java e Node.js e creare back-end per dispositivi iOS, Android e Windows.

Servizi cloud pubblico di Azure supportano hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile. Quando si compila, o eseguire la migrazione di risorse IT a, un provider di servizi di cloud pubblico ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli di hello e servizi hello assicurano toomanage hello del basato su cloud Asset.

Infrastruttura di Azure è progettato da tooapplications funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende possono soddisfare i requisiti di sicurezza.

Inoltre, Azure offre un'ampia gamma di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni dell'organizzazione. Questo documento consente di comprendere come le funzionalità di sicurezza di Azure consentono di soddisfare tali requisiti.

> [!Note]
> obiettivo principale di Hello di questo documento è sui controlli per i clienti che è possibile utilizzare toocustomize e aumentare la sicurezza per le applicazioni e servizi.
>
> È fornire alcune informazioni di panoramica, ma per informazioni dettagliate su come Microsoft protegge hello piattaforma Azure, vedere le informazioni fornite in hello [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/default.aspx).

### <a name="abstract"></a>Sunto
Inizialmente, le migrazioni di cloud pubblico sono dovute tooinnovate risparmi e flessibilità di costo. Per un certo periodo, la sicurezza è stata un'importante fonte di preoccupazione e anche un deterrente alla migrazione a cloud pubblici. Tuttavia, protezione cloud pubblico è passata dallo principale preoccupazione tooone dei driver hello per la migrazione di cloud. Hello motivazioni questo sono possibilità di superiore hello cloud pubblico di grandi dimensioni provider tooprotect di applicazioni di servizio e i dati di hello di risorse basato su cloud.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende grado di soddisfare le esigenze di sicurezza. Inoltre, Azure offre un'ampia gamma di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare requisiti univoci hello toomeet di sicurezza del toomeet distribuzioni IT criteri di controllo e rispettare tooexternal normative.

In questo documento descrive toosecurity approccio di Microsoft all'interno della piattaforma cloud di Microsoft Azure hello:
* Funzionalità di sicurezza implementata da Microsoft hello toosecure dell'infrastruttura di Azure, i dati dei clienti e le applicazioni.
* Azure servizi e alla sicurezza funzionalità tooyou disponibili toomanage hello sicurezza dei servizi di hello e i dati all'interno delle sottoscrizioni di Azure.

## <a name="summary-azure-security-capabilities"></a>Riepilogo delle funzionalità di sicurezza di Azure
seguenti tabella Hello forniscono una breve descrizione delle funzionalità di sicurezza hello implementata da Microsoft hello toosecure dell'infrastruttura di Azure, i dati dei clienti e applicazioni sicure.
### <a name="security-features-implemented-toosecure-hello-azure-platform"></a>Sicurezza funzionalità implementate tooSecure hello piattaforma Azure:
caratteristiche di Hello elencate di seguito sono funzionalità, che è possibile esaminare garanzia hello tooprovide tale hello che piattaforma Azure viene gestita in modo sicuro. I collegamenti disponibili consentono di approfondire come Microsoft affronta gli aspetti della protezione dei clienti in quattro aree: sicurezza della piattaforma, privacy e controlli, conformità e trasparenza.


| [Sicurezza della piattaforma](https://www.microsoft.com/en-us/trustcenter/Security/default.aspx)  | [Privacy e controlli](https://www.microsoft.com/en-us/trustcenter/Privacy/default.aspx)  |[Conformità](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)   | [Trasparenza](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| :-- | :-- | :-- | :-- |
| [Ciclo di sviluppo per la sicurezza](https://www.microsoft.com/en-us/sdl/), controlli interni | [Gestire i dati di tutti i tempi di hello](https://www.microsoft.com/en-us/trustcenter/Privacy/You-own-your-data) | [Centro protezione](https://www.microsoft.com/en-us/trustcenter/default.aspx) |[Come vengono protetti da Microsoft i dati dei clienti nei servizi di Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx) |
| [Formazione sulla sicurezza obbligatoria, controlli del background](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc) |  [Controllo sulla posizione dei dati](https://www.microsoft.com/en-us/trustcenter/Privacy/Where-your-data-is-located) |  [Common Controls Hub](https://www.microsoft.com/en-us/trustcenter/Common-Controls-Hub) |[Come viene gestita da Microsoft la posizione dei dati nei servizi di Azure](http://azuredatacentermap.azurewebsites.net/)|
| [Test di penetrazione](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwiwsOCpganRAhWqxVQKHUdiDsMQFghAMAE&url=https%3A%2F%2Fdownloads.cloudsecurityalliance.org%2Fstar%2Fself-assessment%2FStandardResponsetoRequestforInformationWindowsAzureSecurityPrivacy.docx&usg=AFQjCNEYvBky4zNeDQPN6YJGPFRZA7eeZg&sig2=2kkw1lOCP_kzLzgE9RS2Tg&bvm=bv.142059868,d.amc), [rilevamento delle intrusioni, DDoS](https://www.microsoft.com/en-us/trustcenter/Security/ThreatManagemen), [controlli e registrazione](https://www.microsoft.com/en-us/trustcenter/Security/AuditingAndLogging) | [Accesso ai dati in base ai propri termini](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms) |  [elenco di controllo Cloud Services scadenza molta attenzione Hello](https://www.microsoft.com/en-us/trustcenter/Compliance/Due-Diligence-Checklist) |[Personale Microsoft che ha accesso ai dati e in quali termini](https://www.microsoft.com/en-us/trustcenter/Privacy/Who-can-access-your-data-and-on-what-terms)|
| [Data center all'avanguardia](https://www.microsoft.com/en-us/cloud-platform/global-datacenters), sicurezza fisica, [rete protetta](https://docs.microsoft.com/en-us/azure/security/security-network-overview) | [Imposizione toolaw risponde](https://www.microsoft.com/en-us/trustcenter/Privacy/Responding-to-govt-agency-requests-for-customer-data) |  [Conformità in base al servizio, alla località e al settore](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx) |[Come vengono protetti da Microsoft i dati dei clienti nei servizi di Azure](https://www.microsoft.com/en-us/trustcenter/Transparency/default.aspx)|
|  [Risposta a eventi imprevisti di sicurezza](http://aka.ms/SecurityResponsepaper), [responsabilità condivisa](http://aka.ms/sharedresponsibility) |[Standard di privacy rigorosi](https://www.microsoft.com/en-us/TrustCenter/Privacy/We-set-and-adhere-to-stringent-standards) |  | [Certificazione di verifica per i servizi di Azure, hub per la trasparenza](https://www.microsoft.com/en-us/trustcenter/Compliance/default.aspx)|



### <a name="security-features-offered-by-azure-toosecure-data-and-application"></a>Funzionalità di sicurezza offerta da Azure tooSecure dati e di applicazione
In base al modello del servizio cloud, hello è variabile responsabilità di chi è responsabile della gestione della sicurezza hello di un'applicazione hello o un servizio. Sono disponibili funzionalità in tooassist piattaforma Azure hello è soddisfare tali responsabilità tramite funzionalità incorporate e tramite partner soluzioni che possono essere distribuite in una sottoscrizione di Azure.

funzionalità incorporate di Hello sono organizzate in aree funzionali di sei (6): le operazioni, applicazioni, archiviazione, rete, calcolo e identità. Dettagli aggiuntivi su hello caratteristiche e funzionalità disponibili nella piattaforma Azure in queste aree sei (6) hello vengono forniti tramite le informazioni di riepilogo.

## <a name="operations"></a>Operazioni
Questa sezione contiene informazioni aggiuntive sulle caratteristiche principali per le operazioni di sicurezza e informazioni di riepilogo su tali funzionalità.

### <a name="operations-management-suite-security-and-audit-dashboard"></a>Dashboard Sicurezza e controllo di Operations Management Suite
Hello [soluzioni OMS Security and Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) fornisce un quadro completo dell'organizzazione condizioni di sicurezza IT con [query di ricerca predefinite](https://blogs.technet.microsoft.com/msoms/2016/01/21/easy-microsoft-operations-management-suite-search-queries/) relative a problemi rilevanti che richiedono attenzione. Hello [Security and Audit](https://technet.microsoft.com/library/mt484091.aspx) dashboard è schermata iniziale di hello per tutti gli elementi correlati toosecurity in OMS. Fornisce ad alto livello approfondite hello stato protezione dei computer. Include inoltre hello possibilità tooview tutti gli eventi da hello ultime 24 ore, 7 giorni, o qualsiasi altro intervallo di tempo personalizzato.

Inoltre, è possibile configurare OMS sicurezza e conformità troppo[eseguire automaticamente azioni specifiche](https://blogs.technet.microsoft.com/robdavies/2016/04/20/simple-look-at-oms-alert-remediation-with-runbooks-part-1/) quando viene rilevato un evento specifico.

### <a name="azure-resource-manager"></a>Gestione risorse di Azure
[Gestione risorse di Azure ](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model) consente toowork con risorse hello nella soluzione come gruppo. È possibile distribuire, aggiornare o eliminare tutte le risorse di hello per la soluzione in un'operazione singola, coordinata. Per la distribuzione viene usato un [modello di Azure Resource Manager](https://blogs.technet.microsoft.com/canitpro/2015/06/29/devops-basics-infrastructure-as-code-arm-templates/) che può essere usato per diversi ambienti, ad esempio di testing, di staging e di produzione. Gestione risorse offre sicurezza, il controllo e assegnazione di tag toohelp funzionalità Gestione delle risorse dopo la distribuzione.

Distribuzioni basate su modelli di Azure Resource Manager migliorare la sicurezza hello delle soluzioni distribuite in Azure, in quanto standard di sicurezza, controllare le impostazioni che possono essere integrati nelle distribuzioni basate su modello standardizzate. In questo modo si riduce il rischio di hello di errori di configurazione di sicurezza che potrebbe essere eseguito durante la distribuzione manuale.

### <a name="application-insights"></a>Application Insights
[Application Insights](https://docs.microsoft.com/azure/application-insights/) è un servizio estendibile di gestione delle prestazioni delle applicazioni per sviluppatori Web, con cui è possibile monitorare le applicazioni Web live e rilevare automaticamente le anomalie nelle prestazioni. Include analitica potenti strumenti toohelp che consente di diagnosticare i problemi e toounderstand gli utenti che effettivamente svolgono con le applicazioni. Esegue il monitoraggio dell'applicazione è in esecuzione, sia durante il test e dopo aver pubblicato o distribuito, tutto il tempo hello.

Application Insights consente di creare grafici e tabelle cui viene illustrato, ad esempio, le ore del giorno, la maggior parte degli utenti, come app reattiva hello è e come servita da qualsiasi esterno anche i servizi dipende.

Se sono presenti arresti anomali del sistema, errori o problemi di prestazioni, è possibile cercare tra i dati di telemetria hello causa hello toodiagnose di dettaglio. E servizio hello invia messaggi di posta elettronica se sono state apportate modifiche nella disponibilità hello e le prestazioni dell'app. Application Insights diventa quindi uno strumento di protezione utile perché consente con disponibilità hello in triad sicurezza disponibilità, integrità e riservatezza hello.

### <a name="azure-monitor"></a>Monitoraggio di Azure
[Monitoraggio Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) offre una visualizzazione, query, routing, avvisi, scalabilità automatica e dati sia per l'automazione da hello dell'infrastruttura di Azure ([Log attività](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)) e ogni singola risorsa di Azure ([ I log di diagnostica](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)). È possibile utilizzare Monitor di Azure tooalert è per gli eventi relativi alla sicurezza che vengono generati nel log di Azure.

### <a name="log-analytics"></a>Log Analytics
[Log Analitica](https://azure.microsoft.com/documentation/services/log-analytics/) fa parte di [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite) : fornisce una soluzione di gestione IT per on-premise e infrastruttura basata su cloud di terze parti (ad esempio AWS) inoltre tooAzure risorse. I dati da monitoraggio di Azure possono essere indirizzati direttamente tooLog Analitica per visualizzare le metriche e i log per l'intero ambiente in un'unica posizione.

Log Analitica può essere uno strumento utile per scopi legali e altre analisi di sicurezza, come strumento hello attiva è tooquickly ricerca grandi quantità di voci relative alla sicurezza con un approccio di query flessibile. Inoltre, [i log di proxy e firewall locali possono essere esportati in Azure ed essere resi disponibili per l'analisi con Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-proxy-firewall).

### <a name="azure-advisor"></a>Azure Advisor
[Preparazione di Azure](https://docs.microsoft.com/azure/advisor/) è un consulente cloud personalizzate che consentono di toooptimize le distribuzioni di Azure. Analizza la configurazione e la telemetria delle risorse Consiglia quindi di soluzioni toohelp migliorare hello [prestazioni](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations), [sicurezza](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations), e [la disponibilità elevata](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations) delle risorse durante la ricerca di opportunità troppo[ridurre di Azure complessivo spesa](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations). Azure Advisor offre raccomandazioni sulla sicurezza che possono migliorare notevolmente lo stato di sicurezza complessivo delle soluzioni distribuite in Azure. Tali raccomandazioni vengono ricavate dall'analisi della sicurezza eseguita dal [Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro).

### <a name="azure-security-center"></a>Centro sicurezza di Azure
[Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sui hello protezione delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Il Centro sicurezza di Azure facilita anche le operazioni di sicurezza offrendo un unico dashboard che presenta avvisi e raccomandazioni su cui è possibile intervenire immediatamente. Spesso, si può risolvere i problemi con un solo clic nella console di hello Centro sicurezza di Azure.
## <a name="applications"></a>Applicazioni
sezione Hello fornisce informazioni aggiuntive relative alle funzionalità chiave nell'applicazione della protezione e informazioni di riepilogo su queste funzionalità.

### <a name="web-application-vulnerability-scanning"></a>Analisi delle vulnerabilità delle applicazioni Web
Uno dei tooget modi più semplici hello avviato con test per le vulnerabilità nel [app del servizio App](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is) è hello toouse [integrazione con Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) vulnerabilità di un solo clic tooperform l'analisi dei l'app. È possibile visualizzare i risultati dei test hello in un report per comprendere e informazioni su come toofix ogni vulnerabilità con istruzioni dettagliate.

### <a name="penetration-testing"></a>Test di penetrazione
Se si preferisce tooperform proprio penetrazione di test o desidera toouse suite scanner altro provider, è necessario seguire hello [Azure penetrazione approvazione](https://security-forms.azure.com/penetration-testing/terms) e ottenere penetrazione hello desiderato di tooperform preventiva approvazione test.

### <a name="web-application-firewall"></a>Web application firewall
Hello firewall applicazione web (WAF) in [Gateway applicazione Azure](https://azure.microsoft.com/services/application-gateway/) consente di proteggono le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e Hijack della sessione. È preconfigurato con la protezione dalle minacce identificate hello [aprire Web applicazione sicurezza progetto (OWASP) come hello le prime 10 vulnerabilità comuni](https://msdn.microsoft.com/library/).

### <a name="authentication-and-authorization-in-azure-app-service"></a>Autenticazione e autorizzazione nel servizio app di Azure
[L'autenticazione del servizio App / autorizzazione](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) è una funzionalità che offre un modo per toosign l'applicazione degli utenti in modo che non si dispone di codice toochange sul back-end app hello. Fornisce un modo semplice di tooprotect dell'applicazione e il lavoro con i dati per ogni utente.

### <a name="layered-security-architecture"></a>Architettura di sicurezza su più livelli
Dato che gli [ambienti del servizio app](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-intro) forniscono un ambiente di runtime isolato distribuito in una [rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview), gli sviluppatori possono creare un'architettura di sicurezza su più livelli offrendo livelli diversi di accesso alla rete per ogni livello applicazione. Un comune desiderio è toohide API back-end da accesso generale a Internet e consentire solo le API toobe chiamato dall'App web a monte. [Rete di sicurezza gruppi](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/) può essere utilizzato in subnet di rete virtuale di Azure contenente gli ambienti del servizio App toorestrict accesso pubblico tooAPI applicazioni.

### <a name="web-server-diagnostics-and-application-diagnostics"></a>Diagnostica del server Web e diagnostica applicazioni
Le applicazioni di servizio App web forniscono funzionalità di diagnostica per la registrazione delle informazioni dal server web hello e un'applicazione web hello. logicamente separate in [diagnostica server Web](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) e [diagnostica applicazioni](https://technet.microsoft.com/library/hh530058(v=sc.12).aspx). Il server Web include due importanti progressi per la diagnosi e la risoluzione dei problemi di siti e applicazioni.

la funzionalità di nuovo prima di Hello è informazioni sullo stato in tempo reale i processi di lavoro, pool di applicazioni, siti, domini applicazione e richieste in esecuzione. vantaggi di nuovo secondo Hello sono hello gli eventi di traccia dettagliate che tengono traccia di una richiesta durante l'intero processo di richiesta e risposta completa hello.

raccolta di hello tooenable di questi eventi di traccia, IIS 7 è possibile i log di traccia completo acquisizione tooautomatically configurato, in formato XML, per qualsiasi particolare richiesta in base ai codici di risposta di errore o tempo trascorso.

#### <a name="web-server-diagnostics"></a>Diagnostica del server Web
È possibile abilitare o disabilitare i seguenti tipi di registri hello:

-   Registrazione degli errori dettagliata: informazioni dettagliate sugli errori per i codici di stato HTTP che indicano un'operazione non riuscita (codice di stato 400 o superiore), Può contenere informazioni utili per determinare perché i server di hello ha restituito il codice di errore hello.

-   Richieste non riuscite - informazioni dettagliate sulle richieste non riuscite, tra cui una traccia di hello IIS componenti utilizzati tooprocess hello richiesta e tempo hello in ogni componente. Può essere utile se si siano tentando di prestazioni del sito tooincrease o isolare la causa un toobe specifico di errore HTTP restituito.

-   Informazioni sulle transazioni HTTP formato di file registro esteso W3C hello - registrazione del Server di Web. Ciò è utile quando si determinano le metriche di generale del sito, ad esempio il numero di hello di richieste gestite o il numero di richieste provengono da un indirizzo IP specifico.

#### <a name="application-diagnostics"></a>Diagnostica applicazioni
[Diagnostica applicazioni](https://docs.microsoft.com/azure/app-service-web/web-sites-enable-diagnostic-log) consente informazioni toocapture prodotte da un'applicazione web. Applicazioni ASP.NET possono usare hello [Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) classe toolog informazioni toohello application diagnostics log. In Application Diagnostics, sono disponibili due tipi principali di eventi, prestazioni tooapplication quelli relativi a e quelle relative a errori e problemi tooapplication. Hello gli errori possono essere suddivisi ulteriormente in problemi di connettività, sicurezza ed errori. Errori sono in genere correlati tooa problema con il codice dell'applicazione hello.

In Diagnostica applicazioni è possibile visualizzare gli eventi raggruppandoli nei modi seguenti:

-   Tutti (vengono visualizzati tutti gli eventi)
-   Errori dell'applicazione (vengono visualizzati gli eventi di eccezione)
-   Prestazioni (vengono visualizzati gli eventi prestazioni)

## <a name="storage"></a>Archiviazione
sezione Hello fornisce informazioni aggiuntive relative alle funzionalità chiave di archiviazione di Azure sicurezza e informazioni di riepilogo su queste funzionalità.

### <a name="role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo
È possibile proteggere l'account di archiviazione con il controllo degli accessi in base al ruolo. Limitazione dell'accesso basato su hello [necessario tooknow](https://en.wikipedia.org/wiki/Need_to_know) e [privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) principi di sicurezza è fondamentale per le organizzazioni che vogliono tooenforce criteri di sicurezza per l'accesso ai dati. Questi diritti di accesso vengono concesse tramite l'assegnazione di hello appropriato RBAC ruolo toogroups e alle applicazioni da un determinato ambito. È possibile utilizzare [ruoli RBAC incorporati](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles), ad esempio di collaboratore di Account di archiviazione, tooassign privilegi toousers. Accedere alle chiavi di archiviazione toohello per un account di archiviazione utilizzando hello [Azure Resource Manager](https://docs.microsoft.com/azure/storage/storage-security-guide) modello può essere controllato con controllo di accesso basato sui ruoli (RBAC).

### <a name="shared-access-signature"></a>Firma di accesso condiviso
Oggetto [firma di accesso condiviso (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) fornisce l'accesso delegato tooresources nell'account di archiviazione. Hello SAS significa che è possibile concedere a che un client limitato tooobjects autorizzazioni nell'account di archiviazione per un periodo specificato e con un set specificato di autorizzazioni. È possibile concedere queste autorizzazioni limitate senza tooshare le chiavi di accesso di account.

### <a name="encryption-in-transit"></a>Crittografia in transito
La crittografia in transito è un meccanismo di protezione dei dati durante la trasmissione tra le reti. Con Archiviazione di Azure è possibile proteggere i dati con:
-   [Crittografia a livello di trasporto](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), ad esempio HTTPS quando si trasferiscono dati all'interno o all'esterno di Archiviazione di Azure.

-   [Crittografia di rete](https://docs.microsoft.com/azure/storage/storage-security-guide#using-encryption-during-transit-with-azure-file-shares), ad esempio la [crittografia SMB 3.0](https://docs.microsoft.com/azure/storage/storage-security-guide) per le [condivisioni file di Azure](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files).

-   Crittografia client-side, dati di hello tooencrypt prima di essere trasferiti nell'account di archiviazione e i dati di hello toodecrypt dopo che viene trasferita all'esterno di archiviazione.

### <a name="encryption-at-rest"></a>Crittografia di dati inattivi
Per molte organizzazioni, la crittografia dei dati inattivi è un passaggio obbligatorio per assicurare la privacy dei dati, la conformità e la sovranità dei dati. Esistono tre funzionalità di sicurezza delle risorse di archiviazione di Azure che consentono di crittografare dati inattivi:

-   [La crittografia del servizio di archiviazione](https://docs.microsoft.com/azure/storage/storage-service-encryption) consente che il servizio di archiviazione hello crittografa automaticamente i dati durante la scrittura di archiviazione tooAzure toorequest.

-   [Crittografia client-side](https://docs.microsoft.com/azure/storage/storage-client-side-encryption) offre inoltre funzionalità hello di crittografia.

-   [Crittografia disco Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) consente tooencrypt hello del sistema operativo dischi e i dischi di dati utilizzati da una macchina virtuale IaaS.

### <a name="storage-analytics"></a>di Analisi archiviazione
L'[Analisi archiviazione di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) esegue la registrazione e restituisce i dati delle metriche per un account di archiviazione. È possibile usare questo richieste tootrace dati, analizzare le tendenze di utilizzo e diagnosticare i problemi con l'account di archiviazione. Archiviazione Analitica registra informazioni dettagliate sul servizio di archiviazione tooa richieste riuscite e non riuscite. Queste informazioni possono essere utilizzati toomonitor singole richieste e toodiagnose problemi con un servizio di archiviazione. Le richieste vengono registrate in base al massimo sforzo. viene registrato i seguenti tipi di richieste autenticate Hello:
-   Richieste riuscite

-   Richieste non riuscite, tra cui timeout, limitazione, rete, autorizzazione e altri errori

-   Richieste tramite una firma di accesso condiviso, incluse le richieste riuscite e non riuscite

-   Tooanalytics richiede i dati.

### <a name="enabling-browser-based-clients-using-cors"></a>Abilitazione dei client basati su browser con CORS
[Condivisione delle risorse Multiorigine (CORS)](https://docs.microsoft.com/rest/api/storageservices/fileservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) è un meccanismo che consente loro toogive domini dell'autorizzazione per accedere alle risorse di altro. Agente utente Hello invia tooensure intestazioni aggiuntive che il codice JavaScript hello caricato da un determinato dominio è consentito risorse tooaccess che si trova in un altro dominio. dominio di quest'ultimo Hello risponde quindi con intestazioni aggiuntive consentire o negare l'accesso al dominio originale hello tooits risorse.

Servizi di archiviazione di Azure ora supportano CORS in modo che dopo aver impostato le regole CORS hello per servizio hello, correttamente autenticata è una richiesta effettuata nel servizio hello da un altro dominio toodetermine valutato se è consentito in base a regole toohello che è specificato.
## <a name="networking"></a>Rete
sezione Hello fornisce informazioni aggiuntive relative alle funzionalità chiave nelle informazioni di riepilogo e di sicurezza di rete di Azure su queste funzionalità.

### <a name="network-layer-controls"></a>Controlli a livello rete
Controllo di accesso di rete è act hello limitare tooand connettività da subnet o dispositivi specifici e rappresenta hello core di sicurezza di rete. obiettivo di Hello del controllo di accesso di rete è toomake assicurarsi che le macchine virtuali e servizi sono accessibili tooonly utenti e dispositivi toowhich desiderati accessibile.

#### <a name="network-security-groups"></a>Gruppi di sicurezza di rete
Oggetto [gruppo di sicurezza (rete)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) è un pacchetto con stato base filtro firewall e è possibile toocontrol accedere in base a un [5 tuple](https://www.techopedia.com/definition/28190/5-tuple). Gli NSG non forniscono ispezione a livello dell'applicazione o controlli di accesso autenticato. Possono essere utilizzati traffico toocontrol lo spostamento tra le subnet all'interno di una rete virtuale di Azure e il traffico tra una rete virtuale di Azure e hello Internet.

#### <a name="route-control-and-forced-tunneling"></a>Controllo di route e tunneling forzato
Hello possibilità toocontrol routing comportamento le reti virtuali di Azure è una funzionalità di controllo di sicurezza critici di rete. Ad esempio, se si desidera assicurarsi che tutti tooand di traffico di rete virtuale di Azure passa attraverso il dispositivo di protezione virtuale toomake, è necessario toocontrol in grado di toobe e personalizzare il comportamento di routing. A tale scopo è possibile configurare route definite dall'utente in Azure.

[Le route definite dall'utente](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) consentono toocustomize i percorsi in ingresso e in uscita per il traffico di spostamento in e da singole macchine virtuali o subnet tooinsure hello più sicuro possibile di route. [Il tunneling forzato](https://www.petri.com/azure-forced-tunneling) è un meccanismo che è possibile utilizzare tooensure che i servizi non sono consentiti tooinitiate toodevices una connessione su hello Internet.

Questo comportamento è diverso e quindi blocca le connessioni in ingresso tooaccept in grado di toothem. Server web front-end devono toorequests toorespond dagli host Internet e pertanto è consentito il traffico Internet sourcing server web in ingresso toothese e i server web di hello possono rispondere.

Il tunneling forzato è comunemente utilizzati tooforce il traffico in uscita toohello Internet toogo tramite firewall e proxy di sicurezza locale.

#### <a name="virtual-network-security-appliances"></a>Appliance di sicurezza di rete virtuale
Mentre i gruppi di sicurezza di rete, le route definite dall'utente e il tunneling forzato offrono un livello di protezione a livelli di rete e di trasporto hello di hello [modello OSI](https://en.wikipedia.org/wiki/OSI_model), è possibile che si desideri tooenable protezione a livelli superiori di stack di Hello. È possibile accedere a queste funzionalità di sicurezza di rete avanzate usando una soluzione di appliance di sicurezza di rete dei partner di Azure. È possibile trovare soluzioni di sicurezza della rete partner Azure più recenti hello visitando hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) e cercare "sicurezza" e "sicurezza di rete".

### <a name="azure-virtual-network"></a>Rete virtuale di Azure

Una rete virtuale di Azure (VNet) è una rappresentazione della rete nel cloud hello. È un isolamento logico di hello sottoscrizione tooyour infrastruttura dedicata di rete di Azure. È possibile controllare completamente i blocchi di indirizzi IP hello, impostazioni DNS, i criteri di sicurezza e le tabelle di route all'interno di questa rete. La rete virtuale può essere segmentata in subnet e si possono inserire macchine virtuali (VM) IaaS di Azure e/o [servizi cloud (istanze del ruolo PaaS)](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) nelle reti virtuali di Azure.

Inoltre, è possibile connettersi rete locale tooyour rete virtuale hello utilizzando uno dei hello [opzioni di connettività](https://docs.microsoft.com/azure/vpn-gateway/) disponibili in Azure. In pratica, è possibile espandere le tooAzure di rete, con il controllo completo su blocchi di indirizzi IP con il vantaggio di hello di scala enterprise che fornisce Azure.

La rete di Azure supporta vari scenari di accesso remoto sicuro, tra cui:

-   [Connettere le singole workstation tooan rete virtuale di Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps)

-   [La connessione locale rete tooan rete virtuale di Azure con una connessione VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

-   [La connessione locale rete tooan rete virtuale di Azure con un collegamento WAN dedicato](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)

-   [Connettersi tooeach altre reti virtuali di Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vnet-vnet-rm-ps)

### <a name="vpn-gateway"></a>Gateway VPN
toosend il traffico di rete tra la rete virtuale di Azure e il sito locale, è necessario creare un gateway VPN per rete virtuale di Azure. Un [gateway VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) è un tipo di gateway di rete virtuale che invia traffico crittografato tramite una connessione pubblica. È inoltre possibile utilizzare il traffico VPN gateway toosend tra reti virtuali di Azure su hello dell'infrastruttura di rete di Azure.

### <a name="express-route"></a>Express Route
Microsoft Azure [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction) è un collegamento WAN dedicato che consente di estendere le reti locali nel cloud Microsoft hello su una connessione privata dedicata mediante un provider di connettività.

![Express Route](./media/azure-security/azure-security-fig1.png)

Con ExpressRoute, è possibile stabilire i servizi cloud di tooMicrosoft connessioni, come Microsoft Azure, Office 365 e CRM Online. La connettività può essere stabilita da una rete (IP VPN) any-to-any, da una rete Ethernet punto a punto o da una Cross Connection virtuale tramite un provider di connettività presso una struttura di condivisione del percorso.

Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica e pertanto può essere considerato più sicuro rispetto alle soluzioni basate su VPN. In questo modo toooffer connessioni ExpressRoute più affidabilità, velocità più elevate, minori latenze e una maggiore sicurezza rispetto alle connessioni tramite hello Internet.


### <a name="application-gateway"></a>gateway applicazione
Il [gateway applicazione di Microsoft Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) offre un servizio di [controller per la distribuzione di applicazioni](https://en.wikipedia.org/wiki/Application_delivery_controller) con numerose funzionalità di bilanciamento del carico di livello 7 per l'applicazione.

![gateway applicazione](./media/azure-security/azure-security-fig2.png)

Consente la produttività di toooptimize web farm tramite l'offload della CPU con utilizzo intensivo toohello di terminazione SSL Gateway applicazione (noto anche come "offload SSL" o "bridging SSL"). Fornisce inoltre altre funzionalità di routing di livello 7 inclusa distribuzione round-robin del traffico in ingresso, l'affinità di sessione basato su cookie, il routing basato sul percorso URL e hello possibilità toohost più siti Web protetti da un singolo Gateway applicazione. Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.

Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello.

L'applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni, tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload [SSL (Secure Sockets Layer)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-powershell), probe di integrità personalizzati, supporto per più siti e molte altre.

### <a name="web-application-firewall"></a>Web application firewall
Firewall applicazione Web è una funzionalità di [Gateway applicazione Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) tooweb applicazioni che usano gateway applicazione per le funzioni di controllo di recapito dell'applicazione (ADC) standard che fornisce la protezione. Firewall applicazione Web esegue questa operazione di protezione contro la maggior parte delle hello OWASP top 10 web vulnerabilità comuni.

![Web application firewall](./media/azure-security/azure-security-fig1.png)

-   Protezione dagli attacchi SQL injection

-   Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion

-   Protezione dalle violazioni del protocollo HTTP

-   Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header

-   Prevenzione contro robot, crawler e scanner

-   Rilevamento di errori di configurazione dell'applicazione comuni (ad esempio, Apache, IIS e così via)


Un tooprotect di firewall applicazione web centralizzata attacchi web rende molto più semplice la gestione della protezione e consente di migliorare l'applicazione toohello garanzia contro le minacce hello di intrusioni. Una soluzione WAF può inoltre riflettere minaccia alla sicurezza tooa più veloce per l'applicazione di patch una vulnerabilità nota in una posizione centrale e la protezione di ognuna delle singole applicazioni web. Applicazione esistente gateway possono essere convertito facilmente gateway applicazione tooan con firewall applicazione web.
### <a name="traffic-manager"></a>Gestione traffico
Microsoft [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) consente la distribuzione di hello toocontrol del traffico utente per gli endpoint di servizio in data center diversi. Gli endpoint di servizio supportati da Gestione traffico includono servizi cloud, app Web e VM di Azure. È anche possibile usare Gestione traffico con endpoint esterni, non di Azure. Gestione traffico Usa hello sistema DNS (Domain Name) toodirect client richiede un endpoint di toohello più appropriato in base a un [metodo di routing del traffico](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-routing-methods) e l'integrità di hello degli endpoint hello.

Traffic Manager fornisce una gamma di routing del traffico metodi toosuit le diverse esigenze applicative, integrità dell'endpoint [monitoraggio](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)e il failover automatico. Gestione traffico è toofailure resilienti, ad esempio hello malfunzionamento di un'intera regione di Azure.
### <a name="azure-load-balancer"></a>Azure Load Balancer
[Il bilanciamento del carico Azure](https://docs.microsoft.com/azure/load-balancer/load-balancer-overview) offre prestazioni elevate, disponibilità e la rete tooyour applicazioni. Si tratta di un servizio di bilanciamento del carico di livello 4 (TCP, UDP) che distribuisce il traffico in ingresso tra istanze integre di servizi definiti in un set con carico bilanciato. Azure Load Balancer può essere configurato per:

-   Caricare il saldo in ingresso Internet traffico toovirtual macchine. Questa configurazione è nota come [bilanciamento del carico Internet tra più macchine virtuali o servizi](https://docs.microsoft.com/azure/load-balancer/load-balancer-internet-overview).

-   Bilanciare il carico del traffico tra macchine virtuali in una rete virtuale, tra macchine virtuali nei servizi cloud o tra computer locali e macchine virtuali in una rete virtuale cross-premise. Questa configurazione è nota come [bilanciamento del carico interno](https://docs.microsoft.com/azure/load-balancer/load-balancer-internal-overview). 

- Macchina virtuale specifica di inoltrare il traffico esterno tooa

### <a name="internal-dns"></a>DNS interno
È possibile gestire l'elenco di hello del server DNS utilizzati in una rete virtuale nel portale di gestione di hello o nel file di configurazione di rete hello. Cliente è possibile aggiungere i server DNS too12 per ogni rete virtuale. Quando si specificano i server DNS, è importante tooverify che questi siano elencati i server DNS del cliente nell'ordine corretto di hello per l'ambiente del cliente. Gli elenchi dei server DNS non supportano il round robin. Vengono utilizzati in ordine di hello che sono state specificate. Se hello primo server DNS nell'elenco di hello è in grado di toobe raggiunto, hello utilizzerà il server DNS indipendentemente dal fatto se hello server funzioni correttamente o meno. hello toochange ordine dei server DNS per la rete virtuale del cliente, rimuovere i server DNS hello dall'elenco di hello e aggiungerli nuovamente nell'ordine di hello cliente vuole. DNS supporta aspetto disponibilità hello di triad di sicurezza "CIA" hello.

### <a name="azure-dns"></a>DNS di Azure
Hello [Domain Name System](https://technet.microsoft.com/library/bb629410.aspx), o DNS, è responsabile della conversione (o nel risolvere) un sito Web o servizio name tooits indirizzo IP. [DNS di Azure](https://docs.microsoft.com/azure/dns/dns-overview) è un servizio di hosting per domini DNS che fornisce la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure. Ospitando i domini in Azure, è possibile gestire il servizio DNS i record mediante hello credenziali, API, strumenti e fatturazione come altri servizi di Azure. DNS supporta aspetto disponibilità hello di triad di sicurezza "CIA" hello.
### <a name="log-analytics-nsgs"></a>Gruppi di sicurezza di rete in Log Analytics
È possibile abilitare hello seguenti categorie di log di diagnostica per NSGs:
-   Evento: Contiene le voci per il gruppo le regole sono applicate tooVMs e i ruoli di istanza in base all'indirizzo MAC. lo stato di Hello per queste regole verrà raccolti ogni 60 secondi.

-   Contatore di regole: contiene le voci per quante volte ogni regola di gruppo viene applicato toodeny o consentire il traffico.

### <a name="azure-security-center"></a>Centro sicurezza di Azure
Centro sicurezza PC consente di impedire, rilevare e rispondere toothreats e fornisce maggiori visibilità e controllo sulla, hello protezione delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri nelle sottoscrizioni di Azure, consente di rilevare minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza. Le raccomandazioni sulla rete sono incentrate su firewall, gruppi di sicurezza di rete, configurazione delle regole per il traffico in ingresso e altro ancora.

Sono disponibili le raccomandazioni sulla rete seguenti.

-   [Aggiungere un Firewall generazione successiva](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall) consiglia di aggiungere un Firewall di generazione successiva (NGFW) da un tooincrease partner Microsoft i meccanismi di protezione

-   [Indirizzare il traffico attraverso NGFW solo](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall#route-traffic-through-ngfw-only) consiglia di configurare regole di gruppo () di sicurezza che impongono il traffico in entrata tooyour VM tramite il NGFW di rete.

-   [Abilita i gruppi di sicurezza di rete nelle subnet/sulle macchine virtuali](https://docs.microsoft.com/azure/security-center/security-center-enable-network-security-groups): è consigliabile abilitare gruppi di sicurezza di rete nelle subnet o sulle VM.

-   [Limita l'accesso tramite un endpoint con connessione Internet](https://docs.microsoft.com/azure/security-center/security-center-restrict-access-through-internet-facing-endpoints): è consigliabile configurare regole per il traffico in ingresso per i gruppi di sicurezza di rete.


## <a name="compute"></a>Calcolo

sezione Hello fornisce informazioni aggiuntive relative alle funzionalità chiave in questa area e informazioni di riepilogo su queste funzionalità.

### <a name="antimalware--antivirus"></a>Antimalware e antivirus
IaaS di Azure, è possibile utilizzare il software antimalware di fornitori di sicurezza, ad esempio Microsoft, Symantec, Trend Micro, McAfee e Kaspersky tooprotect delle macchine virtuali dal file dannosi, adware e altre minacce. [Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) per Servizi cloud e Macchine virtuali di Azure è una funzionalità di protezione che consente di identificare e rimuovere virus, spyware e altro software dannoso. Microsoft Antimalware fornisce avvisi configurabili quando noto tooinstall di tentativi di software dannoso o indesiderato stesso o eseguito nei sistemi di Azure. Microsoft Antimalware può anche essere distribuito usando il Centro sicurezza di Azure.

### <a name="hardware-security-module"></a>Modulo di protezione hardware
A meno che non sono protetti hello tasti crittografia e autenticazione non migliorare la sicurezza. È possibile semplificare la gestione di hello e protezione delle chiavi e dei segreti critici archiviandole in [insieme credenziali chiavi Azure](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Insieme di credenziali chiave fornisce hello opzione toostore le chiavi di standard di livello 2 di 140-2 tooFIPS certificate di moduli di protezione hardware. Le chiavi di crittografia di SQL Server per backup o [Transparent Data Encryption](https://msdn.microsoft.com/library/bb934049.aspx) possono essere tutte archiviate nell'insieme di credenziali delle chiavi con qualsiasi chiave o segreto delle applicazioni. Le autorizzazioni e accedere agli elementi di toothese protetti viene gestiti tramite [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

### <a name="virtual-machine-backup"></a>Backup di una macchina virtuale
[Backup di Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) è una soluzione che protegge i dati delle applicazioni senza investimenti di capitale e con costi operativi minimi. Errori dell'applicazione possono danneggiare i dati e gli errori di risorse umane possono introdurre bug nelle applicazioni che possono causare problemi toosecurity. Con Backup di Azure, le macchine virtuali che eseguono Windows e Linux sono protette.

### <a name="azure-site-recovery"></a>Azure Site Recovery
Una parte importante della propria organizzazione [business continuity/ripristino di emergenza (BCDR)](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) strategia è capire come si verificano tookeep carichi di lavoro aziendali e App di backup e in esecuzione quando pianificato e interruzioni non pianificate. [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) consente di orchestrare la replica, il failover e il ripristino di carichi di lavoro e app in modo che siano disponibili da una località secondaria in caso di inattività di quella primaria.

### <a name="sql-vm-tde"></a>TDE in VM SQL
[Transparent Data Encryption (TDE)](https://docs.microsoft.com/azure/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-ps-sql-keyvault) e la crittografia a livello di colonna sono funzionalità di crittografia di SQL Server Questa forma di crittografia richiede l'archiviazione e i clienti toomanage hello le chiavi di crittografia utilizzate per la crittografia.

Hello servizio insieme di credenziali chiave di Azure (insieme) è progettata tooimprove hello sicurezza e la gestione di queste chiavi in una posizione sicura e altamente disponibile. Hello connettore SQL Server consente di SQL Server toouse queste chiavi dall'insieme di credenziali chiave di Azure.

Se si esegue SQL Server con il computer locale, esistono è possibile attenersi alla procedura tooaccess insieme credenziali chiavi Azure dal computer di SQL Server locale. Ma per SQL Server in macchine virtuali di Azure, è possibile risparmiare tempo con funzionalità di integrazione dell'insieme di credenziali chiave di Azure hello. Con alcuni tooenable i cmdlet di Azure PowerShell è possibile automatizzare questa funzionalità, hello credenziali delle chiavi di configurazione necessarie per tooaccess una VM SQL.

### <a name="vm-disk-encryption"></a>Crittografia dei dischi delle VM
[Crittografia dischi di Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) è una nuova funzionalità che consente di crittografare i dischi delle macchine virtuali IaaS Windows e Linux. Si applica hello settore caratteristica standard di BitLocker di Windows e funzionalità di data mining Crypt hello Linux tooprovide della crittografia del volume per hello del sistema operativo e i dischi dati hello. soluzione hello è integrato con insieme credenziali chiavi Azure toohelp è controllare e gestire i segreti e tutte le chiavi di crittografia del disco hello nella sottoscrizione di insieme di credenziali chiave. soluzione Hello assicura anche che tutti i dati nei dischi di macchina virtuale hello vengono crittografati a riposo nell'archiviazione Azure.

### <a name="virtual-networking"></a>Reti virtuali
La connettività di rete è indispensabile per le macchine virtuali. toosupport tale requisito, Azure richiede toobe macchine virtuali connesse tooan rete virtuale di Azure. Una rete virtuale di Azure è un costrutto logico basato sull'infrastruttura di rete di Azure fisica hello. Ogni [rete virtuale di Azure](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) logica è isolata da tutte le altre reti virtuali di Azure. Questo isolamento contribuisce a garantire che il traffico di rete nelle distribuzioni non è accessibile tooother i clienti di Microsoft Azure.

### <a name="patch-updates"></a>Patch di aggiornamento
L'installazione degli aggiornamenti fornire hello basi per la ricerca e risoluzione di potenziali problemi e semplificare il processo hello di gestione aggiornamenti software, riducendo il numero di hello degli aggiornamenti software, che è necessario distribuire nell'organizzazione e aumentando la capacità toomonitor conformità.

### <a name="security-policy-management-and-reporting"></a>Gestione e reporting dei criteri di sicurezza
[Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) consente di impedire, rilevare e rispondere toothreats e offre maggiore visibilità e controllare i sicurezza hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri nelle sottoscrizioni di Azure, consente di rilevare minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

### <a name="azure-security-center"></a>Centro sicurezza di Azure
Centro sicurezza PC consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sulla protezione hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni di Azure, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

## <a name="identify-and-access-management"></a>Gestione delle identità e dell'accesso

I controlli di accesso basati sull'identità sono il punto di partenza della protezione di sistemi, applicazioni e dati. Hello identità e accessi Gestione funzionalità integrate di prodotti e servizi Microsoft business consentono di proteggere le informazioni personali e aziendale dall'accesso non autorizzato durante la creazione degli utenti toolegitimate disponibile ogni volta che hanno bisogno.

### <a name="secure-identity"></a>Proteggere l'identità
Microsoft utilizza più tecnologie e procedure consigliate di sicurezza tra i propri prodotti e identità toomanage services e l'accesso.
-   [Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication/) richiede agli utenti toouse più metodi per l'accesso, locale e nel cloud hello. Offre autenticazione avanzata con diverse facili opzioni di verifica, garantendo al tempo stesso agli utenti un processo di accesso semplice.

-   [Microsoft Authenticator](https://aka.ms/authenticator) semplifica l'uso di Multi-Factor Authentication, è applicabile ad account sia Microsoft che Microsoft Azure Active Directory e include il supporto per dispositivi indossabili e approvazioni basate sull'impronta digitale.

-   [Applicazione dei criteri password](https://azure.microsoft.com/documentation/articles/active-directory-passwords-policy/) aumenta hello protezione delle password tradizionali imponendo requisiti di lunghezza e complessità, la rotazione periodica, forzati e tenta di blocco account dopo l'autenticazione non riuscita.

-   L'[autenticazione basata su token](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) consente l'autenticazione tramite Active Directory Federation Services (AD FS) o sistemi di token di sicurezza di terze parti.

-   [Controllo di accesso basato sui ruoli (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/) toogrant accesso basato su utente di hello Abilita ruolo, semplificando l'importo solo hello toogive semplice agli utenti di accesso hanno bisogno di tooperform compiti relativi al processo. È possibile personalizzare il controllo degli accessi in base al ruolo per il modello aziendale e la tolleranza al rischio dell'organizzazione.

-   [Gestione di identità (identità ibrida) integrata](https://azure.microsoft.com/documentation/articles/active-directory-hybrid-identity-design-considerations-overview/) consente toomaintain controllo di accesso degli utenti tra le piattaforme i Data Center e cloud interne, la creazione di una singola identità utente per l'autenticazione e autorizzazione tooall risorse.

### <a name="secure-apps-and-data"></a>Proteggere app e dati
[Azure Active Directory](https://azure.microsoft.com/services/active-directory/), un'identità e accessi gestione soluzione cloud, consente di proteggere l'accesso toodata nelle applicazioni nel sito e nel cloud hello e semplifica la gestione di hello di utenti e gruppi. Combina servizi directory di base, avanzate governance delle identità, sicurezza e gestione di accesso dell'applicazione e consente agli sviluppatori toobuild basato su criteri di gestione delle identità nelle loro applicazioni. tooenhance Azure Active Directory, è possibile aggiungere funzionalità a pagamento usando le edizioni di Azure Active Directory Basic Premium P1 e P2 Premium hello.

| Funzionalità comuni/gratuite     | Funzionalità Basic    |Funzionalità Premium P1 |Funzionalità Premium P2 | Aggiunta ad Azure Active Directory - Solo funzionalità correlate a Windows 10|
| :------------- | :------------- |:------------- |:------------- |:------------- |
|   [Oggetti directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#directory-objects), [utente/gruppo di gestione (aggiunta/aggiornamento/eliminazione) / basato su utente provisioning, registrazione dispositivo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#usergroup-management-addupdatedelete-user-based-provisioning-device-registration), [Single Sign-On (SSO)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#single-sign-on-sso), [Self-Service Modifica della password per gli utenti del cloud](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-change-for-cloud-users), [Connect (motore di sincronizzazione che si estende in locale tooAzure di directory Active Directory)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-sync-engine-that-extends-on-premises-directories-to-azure-active-directory), [sicurezza / report di utilizzo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#securityusage-reports)       |     [Provisioning/gestione dell'accesso basato sul gruppo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#group-based-access-managementprovisioning), [Reimpostazione delle password self-service per gli utenti cloud](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-reset-for-cloud-users), [Personalizzazione aziendale (pagine di accesso/personalizzazione del pannello di accesso)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#company-branding-logon-pagesaccess-panel-customization), [Proxy dell'applicazione](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#application-proxy), [Contratti di servizio del 99,9%](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#sla-999) |  [Gestione self-service dei gruppi e delle app, aggiunta self-service di applicazioni, gruppi dinamici](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-group), [Reimpostazione, modifica, sblocco con writeback in locale delle password in modalità self-service](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#self-service-password-resetchangeunlock-with-on-premises-write-back), [Multi-Factor Authentication, cloud e in locale (server MFA)](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#multi-factor-authentication-cloud-and-on-premises-mfa-server), [Licenze CAL MIM e server MIM](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mim-cal-mim-server), [Cloud App Discovery](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#cloud-app-discovery), [Connect Health](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#connect-health), [Rollover automatico delle password per account di gruppo](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#automatic-password-rollover-for-group-accounts)|     [Identity Protection](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-identityprotection), [Privileged Identity Management](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-privileged-identity-management-configure)|    [Aggiungere un dispositivo tooAzure AD, SSO Desktop, Microsoft Passport per Azure AD, il ripristino di Bitlocker amministratore](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#join-a-device-to-azure-ad-desktop-sso-microsoft-passport-for-azure-ad-administrator-bitlocker-recovery), [MDM-registrazione automatica, il ripristino di Bitlocker Self-Service, dispositivi tooWindows 10 altri amministratori locale tramite Azure Aggiunta AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-editions#mdm-auto-enrollment)|


- [Cloud App Discovery](https://docs.microsoft.com/azure/active-directory/active-directory-cloudappdiscovery-whatis) è una funzionalità premium di Azure Active Directory che consente applicazioni cloud tooidentify utilizzati dai dipendenti hello all'interno dell'organizzazione.

- [Azure Active Directory Identity Protection](https://azure.microsoft.com/documentation/articles/active-directory-identityprotection/) è un servizio di sicurezza che usa Azure Active Directory anomalie rilevamento funzionalità tooprovide una visualizzazione consolidata di rischi e potenziali vulnerabilità che potrebbero interessare il identità dell'organizzazione.

- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds/) consente toojoin macchine virtuali di Azure tooa dominio senza hello necessario toodeploy i controller di dominio. Gli utenti accedere toothese macchine virtuali utilizzando le credenziali aziendali di Active Directory e possano accedere facilmente alle risorse.

- [Azure B2C Directory attiva](https://azure.microsoft.com/services/active-directory-b2c/) è un servizio di gestione di identità globale, a disponibilità elevata per le App per consumatori che scalare toohundreds di milioni di identità e integrare tra dispositivi mobili e web piattaforme. I clienti possono accedere tooall App attraverso esperienze di personalizzabile che utilizzano gli account esistenti di social networking, oppure è possibile creare nuove credenziali autonomo.

- [Collaborazione di Azure attivo B2B Directory](https://aka.ms/aad-b2b-collaboration) è una soluzione di integrazione partner sicura che supporta le relazioni tra società consentendo ai partner tooaccess applicazioni aziendale e dati in modo selettivo usando la gestione indipendente identità.

- [Azure Active Directory Join](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/) consente tooextend cloud funzionalità tooWindows 10 i dispositivi per la gestione centralizzata. Rende possibile per gli utenti tooconnect toohello aziendale o dell'organizzazione cloud tramite Azure Active Directory e semplifica l'accesso tooapps e risorse.

- Il [proxy di applicazione di Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/) fornisce l'accesso remoto sicuro e SSO per le applicazioni Web ospitate in locale.

## <a name="next-steps"></a>Passaggi successivi
- [Introduzione alla sicurezza in Microsoft Azure](https://docs.microsoft.com/azure/security/azure-security-getting-started)

Servizi di Azure e funzionalità che è possibile usare toohelp proteggere i servizi e i dati all'interno di Azure

- [Centro sicurezza di Azure](https://azure.microsoft.com/services/security-center/)

Impedire, rilevare e rispondere toothreats con l'aumento della visibilità e controllo sulla protezione hello delle risorse di Azure

- [Monitoraggio dell'integrità della sicurezza nel Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-monitoring)

Hello funzionalità di monitoraggio in conformità toomonitor Centro sicurezza di Azure con i criteri.
