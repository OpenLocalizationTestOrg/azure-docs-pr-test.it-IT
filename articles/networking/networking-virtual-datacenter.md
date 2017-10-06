---
title: aaaMicrosoft virtuale Data Center di Azure | Documenti Microsoft
description: Informazioni su come toobuild centro dati virtuali in Azure
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Data center virtuale di Microsoft Azure
**Microsoft Azure**: maggiore velocità, risparmi sui costi e possibilità di integrare app e dati in locale

## <a name="overview"></a>Panoramica
La migrazione tooAzure applicazioni locali, anche senza modifiche significative (approccio noto come "sollevare e spostare"), offre alle organizzazioni hello vantaggi di un'infrastruttura protetta e conveniente. Tuttavia, toomake hello più di flessibilità hello possibili con il cloud computing, le aziende deve essere aggiornato a proprio vantaggio tootake architetture di funzionalità di Azure. Microsoft Azure offre servizi e infrastruttura su scala elevata, capacità e affidabilità di livello aziendale e molte opzioni per la connettività ibrida. Clienti possono scegliere tooaccess questi cloud services tramite hello Internet o con Azure ExpressRoute, che offre connettività di rete privata. piattaforma Microsoft Azure Hello consente ai clienti tooseamlessly estendere la propria infrastruttura nel cloud hello e compilare le architetture a più livelli. Inoltre, i partner Microsoft forniscono funzionalità avanzate tramite l'offerta di servizi di sicurezza e dispositivi virtuali che sono ottimizzati toorun in Azure.

In questo articolo viene fornita una panoramica dei modelli e strutture che possono essere utilizzati toosolve hello fattori di scala, prestazioni e sicurezza architettura che molti clienti devono affrontare quando si pensa di spostamento concatenarle toohello cloud. Panoramica di come toofit organizzazione IT ruoli diversi in Gestione hello e governance del sistema hello viene illustrato anche, con i requisiti di enfasi toosecurity e ottimizzazione di costo.

## <a name="what-is-a-virtual-data-center"></a>Che cos'è un data center virtuale?
In hello soluzioni di cloud agli inizi, sono stati progettati toohost applicazioni relativamente isolata,, nello spettro pubblica hello. Questo approccio è andato bene per alcuni anni, Tuttavia, come vantaggi hello del cloud è diventato evidente soluzioni e più carichi di lavoro su larga scala sono stati ospitati nel cloud hello, indirizzamento di sicurezza, affidabilità e prestazioni e costo problemi delle distribuzioni in uno o più aree è diventato essenziale in tutto hello ciclo di vita del servizio cloud hello.

Hello cloud distribuzione diagramma seguente illustra alcuni esempi di gap di sicurezza (casella rossa) e spazio per i dispositivi virtuali di rete di ottimizzazione in carichi di lavoro (casella di colore giallo).

[![0]][0]

nato Hello virtuale Data Center (controller di dominio virtuale) da tale necessità per carichi di lavoro aziendali toosupport la scala e hello necessario toodeal con problemi di hello introdotti quando il supporto di applicazioni su larga scala nel cloud pubblico hello.

Un controller di dominio virtuale non è sufficiente hello applicazione carichi di lavoro nel cloud hello, ma anche rete hello, sicurezza, gestione e infrastruttura (ad esempio, DNS e servizi di Directory). In genere fornisce inoltre un tooan back-connessione privata rete data center o in locale. Quando più carichi di lavoro Sposta tooAzure, è importante toothink su hello che supporta l'infrastruttura e gli oggetti che questi carichi di lavoro vengono inseriti in. Considerare con attenzione la struttura delle risorse è possibile evitare la proliferazione di hello di centinaia di "isole di carico di lavoro" che devono essere gestite separatamente con flusso di dati indipendenti, modelli di sicurezza e problemi di conformità.

Un data center virtuale è fondamentalmente una raccolta di entità separate, ma correlate, con funzioni, funzionalità e infrastruttura di supporto comuni. Visualizzando i carichi di lavoro come un controller di dominio virtuale integrato, è possibile ottenere una riduzione dei costi dovuto tooeconomies della scala, con ottimizzazione per la protezione tramite componente e dati di flusso di centralizzazione, insieme a operazioni più semplice, la gestione e i controlli di conformità.

> [!NOTE]
> È importante toounderstand che hello vDC **non** un prodotto Azure discreto, ma la combinazione hello varie caratteristiche e funzionalità troppo soddisfa i requisiti esatti. controller di dominio virtuale è un modo valutando i carichi di lavoro e di Azure-utilizzo toomaximize le risorse e funzionalità nel cloud hello. Hello controller di dominio virtuale viene pertanto un approccio modulare sul toobuild dei servizi IT in Azure, rispettando organizzativi ruoli e responsabilità hello.

vDC Hello consente alle aziende di ottenere carichi di lavoro e le applicazioni in Azure per hello seguenti scenari:

-   Hosting di più carichi di lavoro correlati
-   La migrazione dei carichi di lavoro da un tooAzure ambiente locale
-   Implementazione di requisiti di sicurezza e accesso condivisi o centralizzati nei carichi di lavoro
-   Combinazione di DevOps e IT centralizzato in modo appropriato per un'organizzazione di grandi dimensioni

salve vantaggi hello chiave toounlock del controller di dominio virtuale, è una topologia centralizzata (hub e spoke) con una combinazione di funzionalità di Azure: [rete virtuale di Azure][VNet], [NSGs] [ NSG], [Peering reti virtuali][VNetPeering], [route definite dall'utente (UDR)][UDR]e l'identità di Azure con [ Controllo di accesso di Base di ruoli (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>A chi serve un data center virtuale?
I clienti di Azure che deve toomove più di un paio di carichi di lavoro in Azure può trarre vantaggio da riflettere sull'utilizzo delle risorse comuni. A seconda della grandezza hello, persino di singole applicazioni possono trarre vantaggio dall'utilizzo dei modelli di hello e i componenti utilizzati toobuild un controller di dominio virtuale.

Se l'organizzazione dispone di una sicurezza IT, rete, centralizzata e/o reparto/conformità team, un controller di dominio virtuale consente di applicare la separazione di servizio, i punti di criteri e garantire l'uniformità di hello sottostante componenti comuni durante il passaggio più i team delle applicazioni libertà e il controllo è appropriato per le proprie esigenze.

Le organizzazioni che desiderano tooDevOps possono utilizzare i concetti di controller di dominio virtuale hello tooprovide autorizzato gruppi di risorse di Azure e garantire che dispongano di un controllo totale all'interno di tale gruppo (sottoscrizione o risorse in una sottoscrizione comune), ma rete hello e i limiti di sicurezza garantire la conformi definiti da un criteri centralizzati in un hub di rete virtuale e un gruppo di risorse.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Considerazioni sull'implementazione di un data center virtuale
Quando si progetta un controller di dominio virtuale, esistono diversi problemi fondamentale tooconsider:

-   Identità e servizi directory
-   Infrastruttura di sicurezza
-   Cloud toohello connettività
-   Connettività all'interno di cloud hello

##### <a name="identity-and-directory-service"></a>*Identità e servizi directory*
Servizi di identità e Directory sono un aspetto chiave di tutti i dati Center, sia in locale e nel cloud hello. L'identità è tooservices di accesso e l'autorizzazione all'interno di hello vDC gli aspetti correlati tooall. toohelp assicurarsi che solo gli utenti autorizzati e i processi di accedere all'Account Azure e risorse, Azure utilizza diversi tipi di credenziali per l'autenticazione. Tra cui le password (tooaccess hello account di Azure), le chiavi di crittografia, firme digitali e certificati. [*Azure Multi-Factor Authentication* (MFA)][MFA] è un ulteriore livello di sicurezza per l'accesso ai servizi di Azure. Azure MFA fornisce autenticazione avanzata con una gamma di opzioni di verifica semplice, ovvero telefonata, SMS o notifica dell'app mobile e consentono ai clienti metodo hello toochoose preferito.

Qualsiasi azienda di grandi dimensioni è necessario un processo di gestione di identità che descrive gestione hello delle singole identità loro autenticazione, autorizzazione, ruoli e privilegi all'interno o tra controller di dominio virtuale hello toodefine. gli obiettivi di Hello di questo processo devono essere produttività e sicurezza tooincrease diminuendo il costo, i tempi di inattività e le attività manuali ripetitive.

Le aziende/organizzazioni possono richiedere una combinazione complessa di servizi per le diverse line-of-business (LOB) e i dipendenti spesso hanno ruoli diversi a seconda del progetto in cui sono coinvolti. Un controller di dominio virtuale richiede una buona collaborazione tra team diversi, ognuno con definizioni di ruolo specifico, tooget sistemi con buona gestione. Matrice di Hello di responsabilità, l'accesso e dei diritti può essere estremamente complessa. La gestione delle identità nel data center virtuale viene implementata tramite [*Azure Active Directory* (AAD)][AAD] e il controllo degli accessi in base al ruolo.

Un servizio directory è un'infrastruttura di informazioni condivisa per individuare, gestire, amministrare e organizzare quotidianamente elementi e risorse di rete. Queste risorse possono includere volumi, cartelle, file, stampanti, utenti, gruppi, dispositivi e altri oggetti. Ciascuna risorsa di rete hello viene considerato un oggetto dal server di directory hello. Le informazioni su una risorsa vengono archiviate come raccolta di attributi associati a tale risorsa o oggetto.

Tutti i servizi aziendali online di Microsoft si basano su Azure Active Directory (AAD) per le esigenze di gestione delle identità e degli accessi. Azure Active Directory è una soluzione cloud completa di gestione di identità e accessi ad alta disponibilità che riunisce servizi di directory di base, governance delle identità avanzata e gestione dell'accesso alle applicazioni. Azure ad può essere integrato con locale di Active Directory tooenable single sign-on per basato su cloud e localmente ospitate applicazioni (locale). gli attributi utente Hello di Active Directory locale possono essere tooAAD automaticamente sincronizzate.

Un unico amministratore globale è non necessario tooassign tutte le autorizzazioni in un controller di dominio virtuale. Ma ogni reparto specifico (o un gruppo di utenti o ai servizi nel servizio Directory hello) può avere hello le autorizzazioni necessarie toomanage le proprie risorse all'interno di un controller di dominio virtuale. La struttura delle autorizzazioni deve essere ben bilanciata. Troppe autorizzazioni possono ostacolare le prestazioni, mentre autorizzazioni non sufficienti o approssimative possono aumentare i rischi per la sicurezza. Azure Role-Based Access controllo (RBAC) consente di tooaddress questo problema, offrendo la gestione di accesso granulare per le risorse di controller di dominio virtuale.

##### <a name="security-infrastructure"></a>*Infrastruttura di sicurezza*
Infrastruttura di sicurezza nel contesto di hello di un controller di dominio virtuale, è principalmente correlate toohello separazione del traffico in del hello vDC segmento di rete virtuale specifica e la modalità di scorrimento in tutto hello vDC toocontrol ingresso e in uscita. Azure si basa sull'architettura multi-tenant che impedisce il traffico non autorizzato e accidentale tra le distribuzioni, usando l'isolamento della rete virtuale, gli elenchi di controllo di accesso (ACL), i servizi di bilanciamento del carico e i filtri IP, oltre ai criteri del flusso di traffico. Network Address Translation (NAT) separa il traffico di rete interno dal traffico esterno.

Hello infrastruttura di Azure alloca le risorse di infrastruttura tootenant i carichi di lavoro e gestisce le comunicazioni tooand da macchine virtuali (VM). Hello Azure hypervisor applica la memoria e processo di separazione tra le macchine virtuali e, in modo sicuro i tenant tooguest del sistema operativo il traffico di rete le route.

##### <a name="connectivity-toohello-cloud"></a>*Cloud toohello connettività*
controller di dominio virtuale Hello necessita della connettività con reti esterne toooffer servizi toocustomers, partner e/o dagli utenti interni. Connettività significa non solo toohello Internet, ma anche tooon locale reti e data center.

I clienti possono compilare le loro toocontrol di criteri di sicurezza e come servizi specifici controller di dominio virtuale ospitato sono accessibili a/da hello Internet utilizzando criteri di routing personalizzati e ai dispositivi di rete virtuale (con filtro e il traffico di controllo) e (filtro di rete Routing definito dall'utente e gruppi di sicurezza di rete).

Le organizzazioni devono spesso tooconnect VDC tooon locale centri dati o altre risorse. connettività Hello tra le reti locali e Azure è un aspetto fondamentale quando si progetta un'architettura efficace. Le aziende sono due modi diversi toocreate un'interconnessione tra controller di dominio virtuale e in locale in Azure: transito su hello Internet e/o da connessioni dirette private.

Un [ **Azure VPN Site-to-Site** ] [ VPN] è un servizio di interconnessione su hello Internet tra le reti locali e crittografato hello vDC, stabilito tramite la protezione connessioni (tunnel IPsec/IKE). Connessione da sito a sito di Azure è flessibile e rapido toocreate e non richiede approvvigionamento qualsiasi ulteriore, perché tutte le connessioni si connettono tramite hello internet.

[**ExpressRoute** ] [ ExR] è un servizio di Azure di connettività che consente di creare connessioni private tra i controller di dominio virtuale e hello reti locali. Le connessioni ExpressRoute non venga più hello rete Internet pubblica e offrono una maggiore sicurezza, affidabilità e velocità più elevate (backup too10 Gbps) insieme a latenza coerente. ExpressRoute è molto utile per VDC, come i clienti possono ottenere vantaggi hello delle regole di conformità associate connessioni private ExpressRoute.

Per distribuire le connessioni ExpressRoute, è necessario un provider di servizi ExpressRoute. Per i clienti che necessitano di toostart rapidamente, è frequente tooinitially connettività tooestablish VPN da sito a sito tra le risorse locali e i controller di dominio virtuale hello e quindi eseguire la migrazione tooExpressRoute connessione.

##### <a name="connectivity-within-hello-cloud"></a>*Connettività all'interno di cloud hello*
[Le reti virtuali] [ VNet] e [Peering reti virtuali] [ VNetPeering] è hello base connettività ai servizi di rete all'interno di un controller di dominio virtuale. Una rete virtuale garantisce un limite di isolamento per le risorse vDC naturale e peering reti virtuali consente scale tra reti virtuali diverse all'interno di hello stessa area di Azure. Controllo del traffico all'interno di una rete virtuale e tra reti virtuali è necessario toomatch regole di un gruppo di sicurezza specificato tramite elenchi di controllo di accesso ([Network Security Group][NSG]), [ai dispositivi di rete virtuale ] [ NVA]e le tabelle di routing personalizzate ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>Panoramica del data center virtuale

### <a name="topology"></a>Topologia
Hello estesa virtuale Data Center in una singola regione di Azure del modello hub e spoke

[![1]][1]

hub di Hello è fuso centrale di hello che controlla e analizza il traffico in ingresso e/o in uscita tra aree diverse: Internet, in locale, e hello spoke. topologia hub e spoke Hello hello reparto IT fornisce criteri di sicurezza tooenforce un modo efficace in una posizione centrale, riducendo il rischio di hello di errore di configurazione e l'esposizione.

hub di Hello contiene hello comuni componenti del servizio utilizzati da hello spoke. Ecco alcuni esempi tipici di servizi centrali comuni:

-   infrastruttura di Active Directory di Windows Hello (con hello correlati del servizio ad FS) necessarie per l'autenticazione di terze parti, l'accesso da reti non attendibili prima di ottenere accesso toohello i carichi di lavoro in hello spoke
-   Un servizio tooresolve la denominazione DNS per il carico di lavoro di hello in hello spoke, tooaccess risorse locali e su Internet hello
-   Un'infrastruttura PKI, tooimplement single sign-on sul carichi di lavoro
-   Controllo di flusso (TCP/UDP) tra spoke hello e Internet
-   Controllo di flusso tra spoke hello e locale
-   Se necessario, controllo dei flussi tra uno spoke e un altro

Hello vDC riduce costi complessivi tramite l'infrastruttura di hello hub condiviso tra più server.

ruolo di Hello di ogni spoke possa essere toohost diversi tipi di carichi di lavoro. Hello spoke possono anche offrire un approccio modulare per le distribuzioni ripetibile (ad esempio, sviluppo e test, test di accettazione utente, pre-produzione e produzione) di hello carichi di lavoro. Hello spoke possono anche essere toosegregate utilizzato e abilitare diversi gruppi all'interno dell'organizzazione (ad esempio, i gruppi di DevOps). All'interno di uno spoke, è possibile toodeploy un carico di lavoro di base o complessi carichi di lavoro a più livelli con il traffico di controllo tra i livelli di hello.

##### <a name="subscription-limits-and-multiple-hubs"></a>Limiti della sottoscrizione e hub multipli
In Azure, ogni componente, indipendentemente dal tipo di hello, viene distribuito in una sottoscrizione di Azure. isolamento Hello dei componenti di Azure in diverse sottoscrizioni di Azure consente di soddisfare requisiti di hello di diversi oggetti LOB, ad esempio l'impostazione dei livelli differenziati di accesso e autorizzazione.

Un singolo controller di dominio virtuale possibile scalare in verticale toolarge svariate spoke, anche se, come con tutti i sistemi IT, non esistono limiti di piattaforme. distribuzione di hub Hello è tooa associato specifica sottoscrizione di Azure, che presenta le restrizioni e limiti (ad esempio, un numero massimo di peering di reti virtuali, vedere [sottoscrizione di Azure e limiti dei servizi, quote e vincoli] [ Limits] per informazioni dettagliate). In casi in cui i limiti possono essere un problema, è possibile ridimensionare l'architettura di hello fino ulteriormente estendendo il modello di hello da un cluster di tooa singolo hub-spoke di hub e spoke. Più hub in una o più aree di Azure possono essere interconnessi usando Express Route o una VPN da sito a sito.

[![2]][2]

Aumenta sforzo hello di costo e la gestione del sistema hello Hello introduzione di più hub e verrebbe giustificati solo per la scalabilità (esempi: limiti di sistema o di ridondanza) e replica internazionale (esempi: ripristino di emergenza o di prestazioni gestito dall'utente). In scenari che richiedono più hub, tutti gli hub di hello devono cercare hello toooffer stesso insieme di servizi per semplicità operativa.

##### <a name="interconnection-between-spokes"></a>Interconnessione tra spoke
All'interno di un singolo spoke, è possibile tooimplement complesse a più livelli i carichi di lavoro. Le configurazioni a più livelli possono essere implementate utilizzando subnet (uno per ogni livello) nella stessa rete virtuale e filtro hello flussi utilizzando NSGs hello.

In hello invece, un architetto potrebbe volere toodeploy un carico di lavoro a più livelli tra più reti virtuali. Utilizza peering reti virtuali, spoke possono connettersi tooother spoke in hello stesso hub o hub diverso. Un esempio tipico di questo scenario è il caso hello in cui il server di elaborazione dell'applicazione si trovano in uno spoke (VNet), mentre hello database viene distribuito in un diverso spoke (VNet). In questo caso, è facile toointerconnect spoke hello con peering reti virtuali insieme in modo da evitare trasmessi tramite hub hello. Un attento esame di architettura e la protezione deve essere eseguita tooensure che ignorando hub hello non ignora sicurezza importanti o che possono esistere solo nell'hub hello i punti di controllo.

[![3]][3]

Spoke possono anche essere spoke tooa interconnessi che funge da hub. Questo approccio consente di creare una gerarchia a due livelli: hub di hello hello spoke nel livello superiore di hello (livello 0) diventano di spoke inferiore (livello 1) della gerarchia hello. spoke Hello del controller di dominio virtuale necessario tooforward hello traffico toohello hub centrale tooreach rete locale toohello o internet. Un'architettura a due livelli di hub introduce complessi di routing che rimuove i vantaggi di hello di una relazione semplice hub-spoke.

Azure consente topologie complesse, con uno dei principi di base hello del concetto di controller di dominio virtuale hello è ripetibilità e alla semplicità. toominimize allo scopo di gestione, progettazione hub-spoke semplice hello è hello consigliato vDC l'architettura di riferimento.

### <a name="components"></a>Componenti
Un data center virtuale è costituito da quattro tipi di componenti di base: **infrastruttura**, **reti perimetrali**, **carichi di lavoro** e **monitoraggio**.

Ogni tipo di componente è costituito da diverse funzionalità e risorse di Azure. Il controller di dominio virtuale è costituito da istanze di più tipi di componenti e più varianti di hello stesso tipo di componente. È possibile, ad esempio, avere più istanze di carico di lavoro diverse separate in modo logico che rappresentano applicazioni diverse. Usare questi diversi tipi di componente e istanze tooultimately compilare vDC hello.

[![4]][4]

Hello architettura di alto livello precedente di un controller di dominio virtuale mostra diversi tipi di componenti utilizzati in diverse aree della topologia hub-spoke hello. componenti dell'infrastruttura Hello illustrata nelle varie parti dell'architettura di hello.

È consigliabile (per un data center locale o un data center virtuale) che i diritti e i privilegi di accesso siano basati sui gruppi. Gestire gruppi, invece di singoli utenti, consente di assicurare la coerenza dei criteri di accesso tra i team e di ridurre al minimo gli errori di configurazione. Tooand l'assegnazione e la rimozione di utenti da gruppi appropriati consente di mantenere aggiornati i privilegi di hello di un utente specifico.

Ogni gruppo di ruolo deve contenere un prefisso univoco ai nomi rende facile tooidentify il gruppo a cui è associato il carico di lavoro. Un carico di lavoro che ospita un servizio di autenticazione, ad esempio, potrebbe avere gruppi denominati *AuthServiceNetOps, AuthServiceSecOps, AuthServiceDevOps e AuthServiceInfraOps*. Allo stesso modo per centralizzata ruoli, o non tooa specifico servizio correlato, potrebbe essere preceduti da "Corp", *CorpNetOps* ad esempio.

Molte organizzazioni utilizzano una variante di hello gruppi tooprovide una suddivisione dei ruoli principale seguenti:

-   Hello *gruppo IT centrale (Corp)* dispone di componenti di infrastruttura (ad esempio sicurezza e di rete) toocontrol diritti proprietà hello e pertanto ruolo hello toohave di collaboratore della sottoscrizione hello (e che abbia il controllo hub di Hello) e i diritti di collaboratore in hello spoke di rete. Le grandi imprese spesso suddividono queste responsabilità di gestione tra più team, ad esempio un gruppo per le operazioni di rete (CorpNetOps), dedicato esclusivamente alle rete, e un gruppo per le operazioni di sicurezza (CorpSecOps), responsabile del firewall e dei criteri di sicurezza. In questo caso specifico, due diversi gruppi necessario toobe creato per l'assegnazione di questi ruoli personalizzati.
-   Hello *dev & gruppo di test (AppDevOps)* è hello responsabilità toodeploy i carichi di lavoro (servizi o App). Questo gruppo accetta hello del collaboratore alla macchina virtuale per le distribuzioni IaaS e/o a uno o ruoli più PaaS Collaboratore (vedere [ruoli predefiniti per gestire il controllo di accesso][Roles]). Facoltativamente hello dev & team di test potrebbe essere necessario toohave visibilità in Criteri di sicurezza (NSGs) e criteri di routing (UDR) all'interno di hello hub o uno spoke specifico. Di conseguenza, nei ruoli toohello di aggiunta di collaboratore per carichi di lavoro, questo gruppo sarà inoltre necessario ruolo hello del lettore di rete.
-   Hello *operazioni e manutenzione gruppo (CorpInfraOps o AppInfraOps)* hanno la responsabilità di hello di gestione dei carichi di lavoro nell'ambiente di produzione. Questo gruppo è necessario toobe un collaboratore alla sottoscrizione sui carichi di lavoro in qualsiasi sottoscrizione di produzione. Alcune organizzazioni potrebbero anche valutare se è necessario un gruppo di team di supporto aggiuntive dell'escalation dei blocchi con ruolo hello del collaboratore alla sottoscrizione nell'ambiente di produzione e nella sottoscrizione di un hub centrale hello, in ordine toofix potenziali problemi di configurazione nell'ambiente di produzione hello ambiente.

Un controller di dominio virtuale è strutturato in modo che i gruppi creati per i gruppi IT centrali hello gestione hub hello è gruppi corrispondenti a livello di carico di lavoro hello. Inoltre toomanaging hub solo hello centrale IT gruppi di risorse sarebbe in grado di toocontrol l'accesso esterno e le autorizzazioni di livello superiore per sottoscrizione hello. Tuttavia, i gruppi di carico di lavoro sarebbe toocontrol in grado di risorse e le autorizzazioni di loro rete virtuale in modo indipendente su IT centrale.

Hello vDC esigenze toobe partizionata host toosecurely più progetti diversi riga-di-business (LOB). Tutti i progetti richiedono ambienti isolati diversi (sviluppo, test di accettazione utente, produzione). Sottoscrizioni di Azure separate per ognuno di questi ambienti offrono un naturale isolamento.

[![5]][5]

Hello diagramma precedente mostra hello una relazione tra progetti dell'organizzazione, gli utenti, gruppi e ambienti di hello in hello Azure componenti vengono distribuiti.

Nell'ambito IT un ambiente (o livello) è in genere un sistema in cui vengono distribuite ed eseguite più applicazioni. Le grandi imprese usano un ambiente di sviluppo (in cui le modifiche vengono apportate e testate per la prima volta) e un ambiente di produzione (usato dall'utente finale). Questi ambienti sono separati, spesso con diversi ambienti di gestione temporanea tra di loro distribuzione tooallow fasi (implementazione), test e rollback in caso di problemi. Architetture di distribuzione variano notevolmente, ma comunque vengono in genere il processo di base hello di inizio in fase di sviluppo (DEV) e di fine in fase di produzione (produzione).

Un'architettura comune per questi tipi di ambienti multilivello è costituita dagli ambienti DevOps (sviluppo e test), test di accettazione utente (staging) e produzione. Le organizzazioni possono sfruttare singolo o Azure AD più tenant ambienti di toothese toodefine accesso e diritti. Hello diagramma precedente viene illustrato un caso in cui due diversi tenant di Azure AD vengono utilizzati: uno per DevOps e UAT e hello altri esclusivamente per la produzione.

Hello presenza di Azure AD diversi tenant applica la separazione di hello tra ambienti. Hello stesso gruppo di utenti (ad esempio, IT centrale) tooauthenticate utilizzando un diverso tooaccess URI un tenant di Active Directory diverso è necessario modificare i ruoli di hello o le autorizzazioni di hello sia DevOps o ambienti di produzione di un progetto. presenza di Hello ambienti diversi, tooaccess autenticazione utente diversi riduce possibili interruzioni e altri problemi causati da errori umani.

#### <a name="component-type-infrastructure"></a>Tipo di componente: infrastruttura
Questo tipo di componente è in cui si trova la maggior parte delle hello infrastruttura di supporto. e a cui i team di IT centralizzato, sicurezza e/o conformità dedicano la maggior parte del tempo.

[![6]][6]

Componenti dell'infrastruttura di forniscono un'interconnessione tra diversi componenti di un controller di dominio virtuale di hello e sono presenti hub hello sia hello spoke. Hello responsabilità di gestione e manutenzione di componenti dell'infrastruttura hello viene in genere assegnata toohello centrale IT e/o del team di sicurezza.

Una delle attività principali di hello del team dell'infrastruttura IT hello è coerenza hello tooguarantee degli schemi di indirizzo IP azienda hello. Hello private IP indirizzo spazio assegnato toohello vDC deve toobe coerente e non sovrapposte con indirizzi IP privati assegnati nelle reti locali.

Mentre in Azure gli ambienti consentono di evitare conflitti di indirizzi IP o NAT su hello locale router perimetrali, aggiunge i componenti dell'infrastruttura tooyour complessità. Semplicità di gestione è uno degli obiettivi principali di hello del controller di dominio virtuale, quindi tramite NAT toohandle IP problemi non è una soluzione consigliata.

Componenti dell'infrastruttura contengono hello seguenti funzionalità:

-   [**Identità e servizi directory**][AAD]. Tipo di risorsa tooevery accesso in Azure è controllato da un'identità archiviata in un servizio di directory. gli archivi del servizio directory di Hello non solo hello elenco di utenti, ma anche hello tooresources diritti di accesso in una sottoscrizione di Azure specifica. Questi servizi possono esistere solo nel cloud o essere sincronizzati con l'identità locale archiviata in Active Directory.
-   [**Rete virtuale**][VPN]. Reti virtuali sono uno dei principali componenti di un controller di dominio virtuale e abilitare si toocreate un limite di isolamento del traffico su hello piattaforma Azure. Una rete virtuale è costituita da uno o più segmenti di rete virtuale, ognuno con un prefisso di rete IP specifico (una subnet). Rete virtuale Hello definisce un'area di perimetrale interno in cui le macchine virtuali IaaS e PaaS servizi possono stabilire comunicazioni private. Macchine virtuali (e i servizi PaaS) in una rete virtuale può comunicare direttamente tooVMs (e i servizi PaaS) in una rete virtuale diversa, anche se entrambe le reti virtuali vengono create da hello stesso cliente, in hello stessa sottoscrizione. L'isolamento è una proprietà essenziale che assicura che le macchine virtuali e le comunicazioni dei clienti rimangano private entro una rete virtuale.
-   [**Routing definito dall'utente**][UDR]. Per impostazione predefinita basata sulla tabella di routing sistema hello, viene indirizzato il traffico in una rete virtuale. Un'utente di definire Route è una tabella di routing personalizzata che gli amministratori di rete è possono associare tooone o il comportamento di hello toooverwrite subnet altre della tabella di routing sistema hello e definire un percorso di comunicazione all'interno di una rete virtuale. presenza di Hello di UDRs garantisce che il traffico in uscita da hello spoke transito specifiche macchine virtuali personalizzate e/o dispositivi di rete virtuali e servizi di bilanciamento del carico presente nell'hub hello e spoke hello.
-   [**Gruppo di sicurezza di rete**][NSG]. Un gruppo di sicurezza di rete è un elenco di regole di sicurezza che funge da filtro del traffico in origini IP, destinazione IP, protocolli, porte di origine IP e porte di destinazione IP. Hello gruppo può essere applicato tooa subnet, una scheda di rete virtuale associata a una macchina virtuale di Azure o entrambi. Hello NSGs sono essenziali tooimplement un controllo di flusso corretto nell'hub hello e hello spoke. livello di Hello di offerte dall'hello gruppo di sicurezza è una funzione di cui si apre le porte e il loro scopo. I clienti devono applicare filtri aggiuntivi per ogni VM con i firewall basato su host, ad esempio IPtables o hello Windows Firewall.
-   **DNS**. risoluzione dei nomi di risorse in reti virtuali di un controller di dominio virtuale hello Hello viene fornita tramite DNS. ambito di Hello di risoluzione dei nomi predefinito hello DNS è limitato toohello rete virtuale. In genere, un servizio DNS personalizzato deve toobe distribuito nell'hub hello come parte dei servizi comuni, ma i consumer principale hello dei servizi DNS risiedono in spoke hello. Se necessario, ai clienti di creare una struttura gerarchica di DNS con la delega di spoke toohello di zone DNS.
-   [**Sottoscrizione][SubMgmt] e [gestione dei gruppi di risorse][RGMgmt]. Una sottoscrizione definisce un limite naturale di toocreate più gruppi di risorse in Azure. Le risorse in una sottoscrizione vengono assemblate in contenitori logici denominati gruppi di risorse. Gruppo di risorse Hello rappresenta una risorsa di hello tooorganize gruppo logico di un controller di dominio virtuale.
-   [**Controllo degli accessi in base al ruolo**][RBAC]. Tramite RBAC, è possibile toomap ruolo dell'organizzazione con diritti tooaccess specifiche risorse di Azure, consentendo di toorestrict utenti tooonly un determinato subset di azioni. Con RBAC, è possibile concedere l'accesso tramite l'assegnazione toousers ruolo appropriato di hello, gruppi e applicazioni nell'ambito di hello pertinente. ambito Hello un'assegnazione di ruolo può essere una sottoscrizione di Azure, un gruppo di risorse o una singola risorsa. Il controllo degli accessi in base al ruolo consente l'ereditarietà delle autorizzazioni. Un ruolo assegnato a un ambito padre concede l'accesso anche elementi figlio toohello in esso contenuti. Usa tale controllo, è possibile separare i compiti e concedere solo quantità di hello di accesso toousers necessarie tooperform i processi. Ad esempio, un dipendente di usare RBAC toolet gestire le macchine virtuali in una sottoscrizione, mentre un altro può gestire i database di SQL all'interno di hello stessa sottoscrizione.
-   [**Peering reti virtuali**][VNetPeering]. Hello funzionalità fondamentali utilizzate toocreate hello infrastruttura di un controller di dominio virtuale è Peering reti virtuali, un meccanismo che collega due reti virtuali (Vnet) in hello stessa area geografica tramite la rete hello di hello data center di Azure.

#### <a name="component-type-perimeter-networks"></a>Tipo di componente: reti perimetrali
[Rete perimetrale] [ DMZ] componenti (noto anche come una rete Perimetrale) consentono la connettività di rete tooprovide con il locali o reti centro dati fisico, insieme a qualsiasi tooand connettività da hello Internet. Sono anche i componenti a cui probabilmente i team responsabili della rete e della sicurezza dedicano più tempo.

Flusso dei pacchetti in ingresso tramite i dispositivi di sicurezza hello nell'hub hello, ad esempio firewall hello, ID e gli indirizzi IP, prima di raggiungere i server back-end hello hello spoke. I pacchetti associati a Internet dai carichi di lavoro hello anche flusso tramite dispositivi di sicurezza hello nella rete perimetrale hello per l'applicazione dei criteri, l'ispezione e controllo scopi, prima di lasciare la rete hello.

I componenti di rete perimetrale forniscono hello seguenti caratteristiche:

-   [Reti virtuali][VNet], [routing definito dall'utente][UDR], [gruppo di sicurezza di rete][NSG]
-   [Appliance virtuale di rete][NVA]
-   [Bilanciamento del carico][ALB]
-   [Gateway applicazione][AppGW] / [WAF][WAF]
-   [IP pubblici][PIP]

In genere, hello centrale IT e i team di sicurezza hanno la responsabilità di definizione di requisiti e le operazioni di reti perimetrali hello.

[![7]][7]

Hello precedente viene illustrata l'applicazione hello del due perimetro con accesso toohello internet e locale di rete, entrambi residenti nell'hub hello. In un singolo hub toointernet di rete perimetrale hello può applicare la scalabilità verticale toosupport un numero elevato di oggetti LOB, utilizza più farm Web Application firewall (WAFs) e/o firewall.

[**Reti virtuali** ] [ VNet] hub hello in genere si basa su una rete virtuale con più subnet toohost hello tipo diverso di servizi di filtro ed esaminare il traffico tooor da hello internet tramite NVAs, WAFs, e i gateway applicazione Azure.

[**Routing definito dall'utente**][UDR] Usando il routing definito dall'utente, i clienti possono distribuire firewall, IDS/IPS e altre appliance virtuali e instradare il traffico di rete attraverso queste appliance di sicurezza per l'applicazione dei criteri relativi ai limiti di sicurezza, il controllo e l'ispezione. È possibile creare UDRs in entrambi hub e hello tooguarantee raggi di hello che transiti il traffico attraverso hello specifiche macchine virtuali personalizzate, dispositivi di rete virtuali e servizi di bilanciamento del carico utilizzati dal controller di dominio virtuale hello. tooguarantee che il traffico generato da macchine virtuali residenti in hello spoke transito toohello corretto Appliance virtuali, una UDR toobe è necessario impostare subnet hello di spoke hello impostando hello front-end l'indirizzo IP del bilanciamento del carico interno hello come hop successivo hello. servizio di bilanciamento del carico interno Hello distribuisce hello traffico interno toohello dispositivi di rete (pool back-end di bilanciamento del carico).

[![8]][8]

[**Dispositivi di rete virtuale** ] [ NVA] nell'hub hello hello rete perimetrale con toohello accesso internet viene in genere gestita mediante una farm di firewall e/o firewall applicazione Web (WAFs).

LOB diversi utilizzano in genere molte applicazioni web e queste applicazioni tendono toosuffer da varie vulnerabilità e potenziali attacchi. I firewall di applicazioni Web sono che una generazione speciale del prodotto usate toodetect attacchi applicazioni web (HTTP/HTTPS) in modo più approfondito rispetto a un firewall generico. Confrontato con la tecnologia firewall tradizione, WAFs dispongono di un set di server web interno tooprotect di funzionalità specifiche da eventuali minacce.

Una farm di firewall è di tipo gruppo di firewall operano in tandem in hello comuni di amministrazione stesso, con una serie di carichi di lavoro di protezione regole tooprotect hello ospitati in spoke hello e le reti locali tooon di accesso di controllo. Una farm di firewall ha meno specializzato software confrontato con un WAF, ma dispone di una vasta gamma di applicazioni ambito toofilter e controllare qualsiasi tipo di traffico in ingresso e in uscita. Farm di firewall in genere vengono implementate in Azure tramite rete virtuale su (NVAs), che sono disponibili in hello Azure marketplace.

È consigliabile set toouse uno di NVAs per il traffico di origine nei hello Internet e un altro per il traffico proveniente locale. Uso di un solo set di NVAs per entrambe è un rischio per la sicurezza, poiché non fornisce alcun perimetro di sicurezza tra due set di hello del traffico di rete. Utilizzando NVAs separato riduce la complessità di hello di regole di sicurezza di controllo e consente di cancellare le regole corrispondono toowhich richiesta di rete in ingresso.

La maggior parte delle grandi imprese gestisce più domini. DNS di Azure può essere utilizzato toohost hello DNS record per un particolare dominio. Esempio hello indirizzo di IP virtuale (VIP) del servizio di bilanciamento del carico esterno Azure hello (o WAFs hello) può essere registrato in record A hello di un record DNS di Azure.

[**Azure Load Balancer**][ALB] Azure Load Balancer offre un servizio a disponibilità elevata di livello 4 (TCP, UDP), che consente di distribuire il traffico in ingresso tra le istanze del servizio definite in set con carico bilanciato. Il traffico inviato a bilanciamento del carico toohello dagli endpoint front-end (endpoint IP pubblici o privati endpoint IP) può essere ridistribuito con o senza set tooa traduzione di indirizzi del pool di indirizzi IP back-end (esempi da; Dispositivi di rete virtuali o le macchine virtuali).

Bilanciamento del carico di Azure può probe di integrità hello di hello nonché diverse istanze del server e quando un probe ha esito negativo si arresta servizio di bilanciamento carico hello toorespond l'invio di istanza di tipo non integro toohello di traffico. In un controller di dominio virtuale, è necessaria la presenza di hello di un servizio di bilanciamento del carico esterno nell'hub hello (ad esempio, saldo hello traffico tooNVAs) e in spoke hello (attività tooperform come bilanciamento del carico del traffico tra diverse macchine virtuali di un'applicazione multilivello).

[**Gateway applicazione**][AppGW] Il gateway applicazione di Microsoft Azure è un'appliance virtuale dedicata che offre un servizio di controller per la distribuzione di applicazioni con varie funzionalità di bilanciamento del carico di livello 7 per l'applicazione. Consente la produttività di toooptimize web farm tramite l'offload di gateway di CPU intensiva SSL terminazione toohello applicazione. Fornisce inoltre altre funzionalità di routing layer 7 tra cui la distribuzione round robin di traffico in ingresso, l'affinità di sessione basato su cookie, il routing basato sul percorso URL e hello possibilità toohost più siti Web protetti da un singolo Gateway applicazione. Firewall applicazione web (WAF) viene inoltre fornito come parte del gateway applicazione hello WAF SKU. SKU offre una protezione di applicazioni tooweb vulnerabilità web e gli attacchi comuni. Il gateway applicazione può essere configurato come gateway con connessione Internet, come gateway solo interno o come una combinazione di queste due opzioni. 

[**Gli indirizzi IP pubblici** ] [ PIP] hello di abilitare le funzionalità Azure alcune si tooassociate servizio endpoint tooa indirizzo IP pubblico che consente di tooyour risorse toobe accessibile da internet. Questo endpoint Usa l'indirizzo interno toohello traffico tooroute Network Address Translation (NAT) e la porta su hello rete virtuale di Azure. Questo percorso è hello modalità principale con cui il traffico esterno toopass in rete virtuale hello. indirizzi IP pubblici Hello possono essere configurato toodetermine viene passato il tipo di traffico e come e dove viene convertito in toohello di rete virtuale.

#### <a name="component-type-monitoring"></a>Tipo di componente: monitoraggio
Monitoraggio componenti forniscono visibilità e avvisi da tutti gli altri tipi di componenti di hello. Tutti i team avranno accesso toomonitoring per i componenti di hello e servizi hanno accesso. Se si dispone di un centralizzato consentono ai team di operazioni o tecnico, devono toohello di toohave integrato accedere ai dati forniti da questi componenti.

Risorse ospitate di Azure offre diversi tipi di registrazione e monitoraggio comportamento hello tootrack di servizi di Azure. Governance e controllo dei carichi di lavoro in Azure è basato su dati del log non solo nella raccolta, ma anche le informazioni di hello possibilità tootrigger azioni in base a specifici eventi segnalati.

In Azure sono disponibili due tipi principali di lo:

-   [**Log attività** ] [ ActLog] (noto anche come "Registro operativo") forniscono informazioni sulle operazioni hello eseguite sulle risorse in hello sottoscrizione di Azure. Questi log segnalano gli eventi di controllo piano hello per le sottoscrizioni. Ogni risorsa di Azure genera log di controllo.

-   [**I log di diagnostica Azure** ] [ DiagLog] sono registri generati da una risorsa che forniscono dati completo e frequenti sull'operazione di hello di tale risorsa. contenuto Hello di questi log varia in base al tipo di risorsa.

[![9]][9]

In un controller di dominio virtuale, è estremamente importante tootrack hello NSGs log, in particolare queste informazioni:

-   [**I registri eventi**][NSGLog]: vengono fornite informazioni sulle regole di gruppo siano applicati tooVMs e i ruoli di istanza in base all'indirizzo MAC.
-   [**Registri contatori**][NSGLog]: tiene traccia di quante volte, ogni gruppo di regole è stato eseguito toodeny o consentire il traffico.

Tutti i log possono essere archiviati negli account di archiviazione di Azure a scopo di controllo, analisi statica o backup. Quando i log di hello vengono archiviati in un account di archiviazione di Azure, i clienti possono utilizzare tipi diversi di Framework tooretrieve, Prepara, analizzare e visualizzare questo stato di hello tooreport di dati e l'integrità delle risorse cloud.

Le grandi aziende dovrebbero già possedere una struttura standard per il monitoraggio dei sistemi locali e può estendere che registri toointegrate framework generati dalle distribuzioni di cloud. Per le organizzazioni che desiderano tookeep tutti hello registrazione nel cloud hello, [Microsoft Operations Management Suite (OMS)] [ OMS] rappresenta un'ottima scelta. Poiché OMS viene implementato come servizio basato sul cloud, è possibile renderlo operativo rapidamente con un investimento minimo nei servizi di infrastruttura. OMS può essere integrato con i componenti di System Center, ad esempio System Center Operations Manager tooextend gli investimenti esistenti di gestione nel cloud hello.

Analitica di Log di OMS è un componente di hello OMS framework toohelp raccogliere, sono correlate, ricerca e agire sui dati delle prestazioni e log generati da sistemi operativi, applicazioni, cloud infrastruttura componenti. Offre ai clienti informazioni operative in tempo reale mediante ricerca integrata e dashboard personalizzati tooanalyze tutti i record di hello in tutti i carichi di lavoro in un controller di dominio virtuale.

#### <a name="component-type-workloads"></a>Tipo di componente: carichi di lavoro
Nei componenti di tipo carico di lavoro si trovano le applicazioni e i servizi effettivi. Sono anche i componenti a cui i team di sviluppo di applicazioni dedicano più tempo.

Hello del carico di lavoro sono realmente infinito. di seguito Hello sono solo alcuni dei tipi di carico di lavoro possibili hello:

**Applicazioni line-of-business interne**

Le applicazioni line-of-business sono operazione in corso toohello critici applicazioni del computer dell'organizzazione. Le applicazioni line-of-business presentano alcune caratteristiche comuni:

-   **Sono interattive**. Le applicazioni line-of-business sono interattive per natura: vengono immessi dati e vengono restituiti risultati/report.
-   **Sono basate sui dati**. Le applicazioni LOB sono con utilizzo intensivo con database toohello frequenti o altro dispositivo di archiviazione di dati.
-   **Sono integrate**. Integrazione di offerta di applicazioni con altri sistemi all'interno o all'esterno dell'organizzazione hello dati LOB.

**Siti web (versione con connessione Internet o per uso interno) cliente** la maggior parte delle applicazioni che interagiscono con hello Internet sono siti web. Azure offre hello funzionalità toorun un sito web in una VM IaaS o da un [App Web di Azure] [ WebApps] sito (PaaS). Le app Web di Azure supporta l'integrazione con le reti virtuali che consentono la distribuzione di hello di hello App Web in spoke hello di un controller di dominio virtuale. Con hello integrazione della rete virtuale, non è necessario un endpoint Internet tooexpose per le applicazioni ma possono usare hello risorse internet non instradabile indirizzo privato da una rete privata virtuale.

**Dati di grandi dimensioni/Analitica** quando i dati devono tooscale tooa molto elevato volume, database potrebbero non applicare la scalabilità verticale in modo corretto. Tecnologia di Hadoop offre un sistema toorun distribuita query in parallelo su un numero elevato di nodi. I clienti hanno hello opzione toorun i carichi di lavoro in macchine virtuali IaaS o PaaS ([HDInsight][HDI]). HDInsight supporta la distribuzione in una rete virtuale in base alla posizione, può essere distribuito tooa cluster in un raggio di controller di dominio virtuale hello.

**Eventi e messaggistica**
[Hub eventi di Azure][EventHubs] è un servizio di inserimento di dati di telemetria su vastissima scala che raccoglie, trasforma e archivia milioni di eventi. Come piattaforma di streaming distribuita, offre a bassa latenza e la conservazione di tempo configurabile, consentendo tooingest grandi quantità di dati di telemetria in Azure e leggere i dati da più applicazioni. Con Hub eventi, un solo flusso può supportare pipeline sia in tempo reale che basate su batch.

Un servizio di messaggistica cloud altamente affidabile tra applicazioni e servizi può essere implementato tramite il [bus di servizio di Azure][ServiceBus] che offre la messaggistica negoziata asincrona tra il client e il server, insieme a funzionalità di messaggistica e pubblicazione/sottoscrizione FIFO (First-In-First-Out) strutturate.

[![10]][10]

### <a name="multiple-vdc"></a>Data center virtuali multipli
Finora, in questo articolo è occupata principalmente su un singolo vDC, che descrive i componenti di base di hello e architettura che contribuiscono vDC resilienti tooa. Le funzionalità di Azure, ad esempio set di disponibilità del servizio di bilanciamento, NVAs, carico di Azure, il set di scalabilità, insieme ad altri meccanismi di collaborazione tooa sistema che consentono di organizzare toobuild a tinta unita livelli di contratto di servizio in servizi di produzione.

Tuttavia, un singolo controller di dominio virtuale è ospitato in una singola regione e toomajor vulnerabile interruzione che possono influire sull'intera area. I clienti che desidera tooachieve elevate contratti di servizio devono servizi hello tooprotect attraverso le distribuzioni di hello stesso progetto in VDC due (o più), inseriti in aree diverse.

In problemi tooSLA aggiunta, sono disponibili diversi scenari comuni in cui la distribuzione di più VDC ha senso:

-   Presenza a livello di area/globale
-   Ripristino di emergenza
-   Traffico di toodivert meccanismo tra controller di dominio

#### <a name="regionalglobal-presence"></a>Presenza a livello di area/globale
I data center di Azure sono presenti in molte aree in tutto il mondo. Quando si selezionano più data center di Azure, i clienti devono tooconsider due fattori correlati: geografiche e la latenza. I clienti devono distanza geografica di hello tooevaluate tra VDC hello e distanza hello tra controller di dominio virtuale hello e gli utenti finali di hello, toooffer hello migliore esperienza utente.

Area di Azure in cui sono ospitati VDC Hello è inoltre necessario tooconform con requisiti normativi stabiliti da qualsiasi giurisdizione in cui opera l'organizzazione.

#### <a name="disaster-recovery"></a>Ripristino di emergenza
implementazione di Hello di un piano di ripristino di emergenza è strettamente correlati toohello tipo di carico di lavoro in questione e lo stato hello possibilità toosynchronize hello del carico di lavoro tra VDC diversi. Idealmente, la maggior parte dei clienti desiderano toosynchronize dati dell'applicazione tra le distribuzioni in esecuzione in due diversi VDC tooimplement un failover rapido meccanismo. La maggior parte delle applicazioni sono sensibili toolatency e che può causare timeout potenziali e il ritardo nella sincronizzazione dei dati.

Per il monitoraggio della sincronizzazione o dell'heartbeat in data center virtuali diversi, è necessario che i data center comunichino tra loro. Due data center virtuali in aree diverse possono essere connessi tramite:

-   Peering privato ExpressRoute quando gli hub di controller di dominio virtuale hello sono connesso toohello stesso circuito ExpressRoute
-   più circuiti ExpressRoute connessi tramite il backbone aziendale e la mesh vDC circuiti ExpressRoute toohello connesso
-   Connessioni VPN da sito a sito tra gli hub dei data center virtuali in ogni area di Azure

In genere hello connessione ExpressRoute è il meccanismo preferito hello scadenza maggiore larghezza di banda e latenza coerente quando trasmessi tramite hello backbone di Microsoft.

Non sussiste alcun toovalidate recipe magiche un'applicazione distribuita tra due (o più) VDC diverse che si trova in aree diverse. I clienti dovrebbero eseguire latenza di rete qualificazione test tooverify hello e larghezza di banda di connessioni hello e di destinazione è appropriata di replica sincrona o asincrona dei dati e quale obiettivo del tempo di recupero ottimale hello (RTO) per il carichi di lavoro.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>Traffico di toodivert meccanismo tra controller di dominio
Una tecnica efficace toodivert hello il traffico in ingresso in un controller di dominio tooanother si basa su DNS. [Azure Traffic Manager] [ TM] utilizza hello sistema DNS (Domain Name) meccanismo toodirect hello dell'utente finale traffico toohello più appropriato endpoint pubblico in un controller di dominio virtuale specifico. Tramite probe, Traffic Manager controlla periodicamente lo stato di servizio hello di endpoint pubblici in VDC diversi e, in caso di errore di tali endpoint, viene instradato automaticamente vDC secondario toohello.

Gestione traffico funziona su endpoint pubblici di Azure e può essere utilizzato opportuno, ad esempio, toocontrol/deviare traffico tooAzure macchine virtuali e applicazioni Web in hello controller di dominio virtuale. Gestione traffico sia resiliente anche in faccia hello del failover intera area di Azure e può controllare la distribuzione di hello del traffico utente per gli endpoint di servizio in VDC diversi in base a diversi criteri (ad esempio, un errore di un servizio in un controller di dominio virtuale specifico, o la selezione Hello vDC con latenza di rete più bassa di hello per client hello).

### <a name="conclusion"></a>Conclusioni
Hello virtuale Data Center è una migrazione di center toodata approccio in cloud hello che utilizza una combinazione di caratteristiche e funzionalità toocreate un'architettura scalabile in Azure che ottimizza l'utilizzo delle risorse cloud, riducendo i costi e semplificare sistema governance. il concetto di controller di dominio virtuale Hello è basato su una topologia hub-spoke, che fornisce servizi condivisi comuni nell'hub hello e consentendo di specifiche applicazioni o carichi di lavoro in hello spoke. Struttura hello dei ruoli di società, in cui diversi reparti (IT centrale, DevOps, operazioni e manutenzione) interagiscono, ognuno con un elenco specifico di ruoli e compiti corrisponde a un controller di dominio virtuale. Un controller di dominio virtuale soddisfa i requisiti di hello per una migrazione "Sollevare e MAIUSC", ma fornisce anche le distribuzioni di cloud toonative numerosi vantaggi.

## <a name="references"></a>Riferimenti
Hello seguenti caratteristiche sono stato trattato in questo documento. Fare clic su hello collegamenti toolearn altre.

| | | |
|-|-|-|
|Funzionalità di rete|Bilanciamento del carico.|Connettività|
|[Reti virtuali di Azure][VNet]</br>[Gruppi di sicurezza di rete][NSG]</br>[Log per i gruppi di sicurezza di rete][NSGLog]</br>[Routing definito dall'utente][UDR]</br>[Network Virtual Appliances][NVA] (Appliance virtuali di rete)</br>[Indirizzi IP pubblici][PIP]|[Azure Load Balancer (L3) ][ALB]</br>[Gateway applicazione (L7) ][AppGW]</br>[Web application firewall][WAF]</br>[Gestione traffico di Azure][TM] |[Peering reti virtuali][VNetPeering]</br>[Rete privata virtuale][VPN]</br>[ExpressRoute][ExR]
|Identità</br>|Monitoraggio</br>|Procedure consigliate</br>|
|[Azure Active Directory][AAD]</br>[Multi-Factor Authentication][MFA]</br>[Controlli degli accessi in base ai ruoli][RBAC]</br>[Ruoli predefiniti AAD][Roles] |[Log attività][ActLog]</br>[Log di diagnostica][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[Procedure consigliate per le reti perimetrali][DMZ]</br>[Gestione sottoscrizioni][SubMgmt]</br>[Gestione di gruppi di risorse][RGMgmt]</br>[Limiti delle sottoscrizioni di Azure][Limits] |
|Altri servizi di Azure|
|[App Web di Azure][WebApps]</br>[HDInsights (Hadoop) ][HDI]</br>[Hub eventi][EventHubs]</br>[Bus di servizio][ServiceBus]|



## <a name="next-steps"></a>Passaggi successivi
 - Esplorare [Peering reti virtuali][VNetPeering], hello tecnologia supplementare per controller di dominio virtuale hub e spoke progettazioni
 - Implementare [AAD] [ AAD] tooget introduttiva [RBAC] [ RBAC] esplorazione
 - Sviluppare un modello di gestione sottoscrizione e della risorsa e RBAC struttura hello toomeet, requisiti, modello e i criteri dell'organizzazione. pianificazione di attività più importanti Hello. Da un punto di vista pratico, è consigliabile pianificare riorganizzazioni, fusioni, nuove linee di prodotti e così via.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Esempi di sovrapposizione di componenti" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Esempio generale di data center virtuale con hub e spoke"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Cluster di hub e spoke"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Da spoke a spoke"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Diagramma livello di blocco di hello vDC"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Utenti, gruppi, sottoscrizioni e progetti"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Diagramma dell'infrastruttura generale"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Diagramma dell'infrastruttura generale"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "Peering reti virtuali e reti perimetrali"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "Diagramma generale per il monitoraggio"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "Diagramma generale per il carico di lavoro"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
