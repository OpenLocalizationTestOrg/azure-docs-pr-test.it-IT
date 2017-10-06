---
title: procedure consigliate di sicurezza rete aaaAzure | Documenti Microsoft
description: "Informazioni su che alcune delle funzionalità chiave hello disponibili in Azure toohelp creare ambienti di rete sicura"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Servizi cloud Microsoft e sicurezza di rete
I Servizi cloud Microsoft offrono servizi e infrastruttura su scala elevata, capacità di livello aziendale e molte opzioni per la connettività ibrida. I clienti possono scegliere tooaccess questi servizi tramite Internet hello o con Azure ExpressRoute, che fornisce la connettività di rete privata. piattaforma Microsoft Azure Hello consente ai clienti tooseamlessly estendere la propria infrastruttura nel cloud hello e compilare le architetture a più livelli. Inoltre, le terze parti possono abilitare capacità avanzate offrendo servizi di sicurezza e appliance virtuali. Questo white paper offre una panoramica dei problemi relativi a sicurezza e architettura che i clienti dovrebbero tenere in considerazione quando usano i Servizi cloud Microsoft con accesso tramite ExpressRoute. Il documento illustra anche come creare servizi più sicuri sulle reti virtuali di Azure.

## <a name="fast-start"></a>Avvio veloce
Hello seguente grafico logica può indirizzare si tooa esempio specifico di hello numerose tecniche di sicurezza con hello piattaforma Azure. Per riferimento rapido, trovare l'esempio hello più adatto al caso. Per una spiegazione espansa, continuare la lettura tramite carta hello.
[![0]][0]

[Esempio 1: Creare una rete perimetrale (nota anche come DMZ o subnet schermata) toohelp proteggere le applicazioni con rete sicurezza gruppi.](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Esempio 2: Creare un perimetro di rete toohelp proteggere le applicazioni con un firewall e NSGs.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Esempio 3: Creare un perimetro di rete toohelp proteggere reti con un firewall, una route definite dall'utente (UDR) e un gruppo.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Esempio 4: Aggiungere una connessione ibrida con un'appliance virtuale da sito a sito e con una rete virtuale privata (VPN).](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Esempio 5: Aggiungere una connessione ibrida con un gateway VPN di Azure da sito a sito.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Esempio 6: Aggiungere una connessione ibrida con ExpressRoute.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Esempi per l'aggiunta di connessioni tra reti virtuali, la disponibilità elevata e il concatenamento di servizi verranno aggiunti toothis documento su hello prossimi mesi.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Conformità Microsoft e protezione dell'infrastruttura
le organizzazioni toohelp conforme ai nazionali, regionali e requisiti specifici del settore che regolano hello raccolta e utilizzo dei dati degli utenti, Microsoft offre più di 40 certificazioni e le attestazioni. Hello più completo impostata di qualsiasi provider di servizi cloud.

Per ulteriori informazioni, vedere le informazioni sulla conformità hello in hello [Microsoft Trust Center][TrustCenter].

Microsoft ha un approccio completo tooprotect servizi dell'infrastruttura cloud necessario toorun hyper su scala globale. Infrastruttura cloud Microsoft include hardware, software, reti e amministrative e personale addetto alle operazioni, inoltre toohello fisica data center.

![2]

Questo approccio offre una base più sicura per i clienti toodeploy i propri servizi in cloud di Microsoft hello. passaggio successivo Hello è per i clienti toodesign e creare un tooprotect architettura di sicurezza di questi servizi.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Architetture di sicurezza tradizionali e reti perimetrali
Sebbene Microsoft investe frequentemente per la protezione dell'infrastruttura cloud hello, i clienti devono proteggere anche gruppi di risorse e i servizi cloud. Un approccio più livelli di toosecurity fornisce difesa hello. Un'area di sicurezza della rete perimetrale protegge le risorse di rete interne da una rete non attendibile. Una rete perimetrale fa riferimento toohello bordi o parti della rete hello che si trovano tra hello Internet e l'infrastruttura IT aziendale hello protetto.

Nelle reti aziendali tipiche, infrastruttura di base hello frequentemente viene aggiunto al perimetro di hello, con più livelli di dispositivi di sicurezza. limite Hello di ogni livello è costituito da dispositivi e i punti di imposizione dei criteri. Ogni livello può includere una combinazione di hello seguenti dispositivi di sicurezza di rete: firewall, prevenzione di tipo Denial of Service (DoS), il rilevamento delle intrusioni o sistemi di protezione (ID/IP) e i dispositivi VPN. Applicazione dei criteri può richiedere formato hello di criteri di firewall, elenchi di controllo di accesso (ACL) o di routing specifico. Hello prima difesa nella rete hello, accettando direttamente il traffico in ingresso da Internet, hello è una combinazione di questi meccanismi tooblock attacchi e il traffico dannoso, consentendo di ulteriori richieste legittime rete hello. Questo traffico indirizza direttamente tooresources nella rete perimetrale hello. La risorsa può quindi "parlare" tooresources più profondo nella rete hello, in transito successivo limite di hello per la convalida prima. livello più esterno Hello viene denominata rete perimetrale hello perché questa parte della rete hello è esposto toohello Internet, in genere con un modulo di protezione su entrambi i lati. Hello figura riportata di seguito viene illustrato un esempio di una rete perimetrale singola subnet in una rete aziendale, con due limiti di sicurezza.

![3]

Esistono molte architetture utilizzate tooimplement una rete perimetrale. Queste architetture possono variare da una rete di più subnet perimetrale tooa del servizio di bilanciamento carico semplice con diversi meccanismi di traffico di tooblock ogni limite e proteggere livelli più profondi di hello della rete aziendale hello. La modalità di compilazione rete perimetrale hello dipende dalle esigenze specifiche di hello dell'organizzazione di hello e la tolleranza al rischio complessivo.

Come i clienti spostano i cloud toopublic i carichi di lavoro, è critico toosupport funzionalità simili per l'architettura di rete perimetrale in Azure toomeet conformità e i requisiti di sicurezza. Questo documento offre indicazioni su come creare un ambiente di rete sicuro in Azure. Si concentra sulla rete perimetrale hello, ma include anche una trattazione completa di molti aspetti di sicurezza di rete. questa discussione vengono informati quando Hello seguenti domande:

* Come è possibile creare una rete perimetrale in Azure?
* Quali sono la rete perimetrale hello le funzionalità di Azure disponibili toobuild hello?
* Come è possibile proteggere i carichi di lavoro back-end?
* Quali sono i carichi di lavoro di Internet comunicazioni controllate toohello in Azure?
* Come possono essere protetti hello sulle reti locali da distribuzioni in Azure?
* Quando è consigliabile usare le funzionalità di sicurezza native di Azure invece di appliance o servizi di terze parti?

Hello seguente diagramma illustra i vari livelli di sicurezza di che Azure fornisce toocustomers. Tali livelli rappresentano nativa nella piattaforma Azure stesso hello e funzionalità definita dal cliente:

![4]

In ingresso da hello Internet, DDoS Azure consente di proteggere da attacchi su larga scala in Azure. livello successivo Hello è definito dal cliente gli indirizzi IP pubblici (endpoint), vengono utilizzati toodetermine possibile passare il tipo di traffico tramite rete virtuale toohello di hello servizio cloud. L'isolamento nativo della rete virtuale di Azure assicura l'isolamento completo da tutte le altre reti; consente anche il passaggio del flusso di traffico solo tramite percorsi e metodi configurati dall'utente. Questi percorsi e i metodi sono livello successivo hello, dove NSGs UDR e ai dispositivi di rete virtuale possono essere utilizzato toocreate sicurezza limiti tooprotect hello le distribuzioni di applicazioni nella rete hello protetto.

Nella sezione successiva Hello fornisce una panoramica delle reti virtuali di Azure. Queste reti virtuali di Azure vengono create dai clienti e i carichi di lavoro distribuiti dei clienti sono collegati ad esse. Le reti virtuali sono a base hello di tutte le funzionalità di sicurezza di rete hello necessari tooestablish un distribuzioni dei clienti tooprotect rete perimetrale in Azure.

## <a name="overview-of-azure-virtual-networks"></a>Panoramica delle reti virtuali di Azure
Prima di traffico Internet può ottenere toohello reti virtuali di Azure, sono disponibili due livelli di protezione inerenti toohello piattaforma Azure:

1.    **Protezione DDoS**: protezione DDoS è un livello di hello Azure rete fisica che consente di proteggere da attacchi basati su Internet su larga scala hello piattaforma Azure. Questi attacchi utilizzano più nodi di "bot" in un toooverwhelm tentativo di un servizio in Internet. Azure vanta una solida rete di protezione DDoS su tutta la connettività Internet in ingresso, in uscita e tra le aree di Azure. Questo livello di protezione DDoS dispone di attributi configurabili dall'utente e non è accessibile toohello cliente. livello di protezione DDoS Hello protegge Azure come piattaforma da attacchi su larga scala, viene inoltre monitorato il traffico tra Azure area e traffico in uscita. Usando dispositivi di rete virtuali nella rete virtuale hello, ulteriori livelli di resilienza possono essere configurati dal cliente hello da attacchi di scala più piccoli che non attivarsi protezione a livello di piattaforma hello. Un esempio di DDoS in azione. Se un indirizzo IP per internet è stato attaccato da un attacco DDoS su larga scala, Azure rilevi origini hello di attacchi di hello ed eseguire lo scrubbing hello danneggiata traffico prima ha raggiunto la destinazione prevista. Nella quasi totalità dei casi, hello attaccato endpoint non è influenzato da attacco hello. In casi rari hello che viene modificato un endpoint, nessun traffico è interessato tooother endpoint, solo l'endpoint hello ad attaccata. Pertanto altri clienti e servizi non subiranno alcun effetto di tale attacco. È toonote critici che Azure DDoS esegue la ricerca solo di attacchi su larga scala. È possibile che il servizio specifico può essere sovraccaricato prima vengono superate le soglie di protezione a livello di hello piattaforma. Ad esempio, un sito Web in un singolo server IIS A0 potrebbe essere danneggiato da un attacco DDoS prima che la protezione DDoS a livello di piattaforma di Azure rilevi la minaccia.

2.  **Gli indirizzi IP pubblici**: indirizzo IP pubblico indirizzi (abilitati tramite gli endpoint del servizio, gli indirizzi IP pubblici, Gateway applicazione e altre funzionalità di Azure che presentano una pubblico toohello internet indirizzato tooyour la risorsa indirizzo IP) consentono di servizi cloud o gli indirizzi IP Internet pubblici toohave e porte esposte gruppi di risorse. endpoint Hello Usa l'indirizzo interno toohello traffico tooroute Network Address Translation (NAT) e la porta su hello rete virtuale di Azure. Questo percorso è hello modalità principale con cui il traffico esterno toopass in rete virtuale hello. indirizzi IP pubblici Hello sono configurabili toodetermine viene passato il tipo di traffico e come e dove viene convertito in toohello di rete virtuale.

Quando il traffico di rete virtuale hello, sono disponibili molte funzionalità che entrano in gioco. Reti virtuali di Azure sono hello foundation per i clienti tooattach i carichi di lavoro e in cui si applica protezione a livello di rete di base. È una rete privata (un overlay della rete virtuale) in Azure per i clienti con hello seguenti funzionalità e caratteristiche:

* **Isolamento del traffico**: una rete virtuale è limite di isolamento del traffico hello in hello piattaforma Azure. Macchine virtuali (VM) in una rete virtuale non possono comunicare direttamente in una rete virtuale diversa, anche se entrambe le reti virtuali vengono create da tooVMs hello stesso cliente. L'isolamento è una proprietà essenziale che assicura che le macchine virtuali e le comunicazioni dei clienti rimangano private entro una rete virtuale.

>[!NOTE]
>Isolamento del traffico si riferisce solo tootraffic *in ingresso* toohello di rete virtuale. Per il traffico in uscita predefinito da toohello di rete virtuale hello internet è consentita, ma è possibile prevenire eventualmente NSGs.
>
>

* **Topologia a più livelli**: le reti virtuali consentono ai clienti topologia multilivello toodefine allocando le subnet e la designazione di spazi di indirizzi separati per diversi elementi o "livelli" dei rispettivi carichi di lavoro. Questi raggruppamenti logici topologie Abilita criteri di accesso diversi toodefine di clienti in base ai tipi di carico di lavoro hello e inoltre controllano i flussi di traffico tra i livelli di hello.
* **Connettività cross-premise**: i clienti possono stabilire la connettività cross-premise tra una rete virtuale e più siti locali o altre reti virtuali in Azure. tooconstruct una connessione, i clienti possono utilizzare Peering reti virtuali, il gateway VPN di Azure, dispositivi virtuali di rete di terze parti o ExpressRoute. Azure supporta VPN da sito a sito (S2S, site-to-site) mediante protocolli IPsec/IKE standard e la connettività privata di ExpressRoute.
* **GRUPPO** consente ai clienti regole toocreate (ACL) a livello di hello desiderato di granularità: subnet virtuali, singole macchine virtuali o le interfacce di rete. I clienti possono controllare l'accesso per consentire o negare la comunicazione tra i carichi di lavoro hello in una rete virtuale, da sistemi in reti tramite connettività cross-premise, o comunicazione Internet diretta.
* **UDR** e **l'inoltro IP** consentono ai clienti di percorsi di comunicazione hello toodefine tra i diversi livelli all'interno di una rete virtuale. I clienti possono distribuire un firewall, IDS/IPS e altre appliance virtuali e instradare il traffico di rete attraverso queste appliance di sicurezza per l'applicazione dei criteri relativi ai limiti di sicurezza, il controllo e l'ispezione.
* **Dispositivi di rete virtuale** in hello Azure Marketplace: dispositivi di sicurezza, ad esempio firewall, servizi di bilanciamento del carico e gli ID o gli indirizzi IP sono disponibili in Azure Marketplace hello e hello raccolta immagini di macchina virtuale. I clienti possono distribuire queste Appliance nelle loro reti virtuali e in particolare, l'ambiente di rete sicura sicurezza limiti (compresi subnet della rete perimetrale hello) toocomplete una a più livelli.

Con queste caratteristiche e funzionalità, un esempio di come è possibile costruire un'architettura di rete perimetrale in Azure è hello seguente diagramma:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Caratteristiche e requisiti della rete perimetrale
rete perimetrale Hello è hello front-end di rete hello, direttamente l'interazione di comunicazione da hello Internet. i pacchetti Hello in arrivo devono attraversare i dispositivi di sicurezza hello, ad esempio firewall hello, ID e gli indirizzi IP, prima di raggiungere i server back-end di hello. I pacchetti associati a Internet dai carichi di lavoro hello possono inoltre passare tramite dispositivi di sicurezza hello nella rete perimetrale hello per l'applicazione dei criteri, l'ispezione e controllo scopi, prima di lasciare la rete hello. Inoltre, rete perimetrale hello può ospitare gateway VPN cross-premise tra reti virtuali dei clienti e le reti locali.

### <a name="perimeter-network-characteristics"></a>Caratteristiche della rete perimetrale
Nella figura precedente hello di riferimento, alcune delle caratteristiche di hello di una rete perimetrale buona sono i seguenti:

* Connessione a Internet:
  * subnet della rete perimetrale Hello stesso è rivolto a Internet, direttamente la comunicazione con Internet hello.
  * Gli indirizzi IP pubblici, gli indirizzi VIP e/o gli endpoint del servizio passano i dispositivi e rete front-end toohello di traffico Internet.
  * Il traffico da Internet attraversa i dispositivi di sicurezza prima di altre risorse in rete front-end hello hello in ingresso.
  * Se è abilitata la sicurezza in uscita, il traffico passa attraverso i dispositivi di sicurezza, come passaggio finale hello, prima di passare toohello Internet.
* Rete protetta:
  * Non è un percorso diretto dall'infrastruttura di base toohello hello Internet.
  * Infrastruttura di base toohello canali deve attraversare tramite dispositivi di sicurezza, ad esempio NSGs, firewall o dispositivi VPN.
  * Altri dispositivi non devono effettuare il bridging Internet e hello infrastruttura di base.
  * Dispositivi di sicurezza sia hello con connessione Internet e hello rete protetta rivolti verso i limiti della rete perimetrale hello (ad esempio, hello due firewall icone illustrate nella figura precedente hello) potrebbe essere un singolo dispositivo virtuale con le regole differenziati o interfacce per ciascun limite. Ad esempio, un dispositivo fisico, logicamente separato, la gestione hello carico per i limiti della rete perimetrale hello.
* Altri vincoli e procedure comuni:
  * I carichi di lavoro non devono archiviare informazioni essenziali per l'azienda.
  * Le distribuzioni e le configurazioni di rete tooperimeter accesso e gli aggiornamenti sono gli amministratori tooonly limitato autorizzato.

### <a name="perimeter-network-requirements"></a>Requisiti della rete perimetrale
tooenable queste caratteristiche, seguire queste linee guida su tooimplement requisiti di rete virtuale una rete perimetrale ha esito positivo:

* **Architettura di subnet:** rete virtuale di hello specificare in modo che un'intera subnet dedicata come rete perimetrale hello, separato da altre subnet in hello stessa rete virtuale. Questa separazione assicura il traffico di hello tra rete perimetrale hello e gli altri flussi di livelli di subnet interna o privata attraverso un firewall o un dispositivo virtuale ID/IP.  Le route definite dall'utente sul limite di hello subnet sono necessari tooforward questo dispositivo virtuale toohello di traffico.
* **GRUPPO:** subnet della rete perimetrale hello stesso deve essere aperta tooallow comunicazione con hello Internet, ma non implica che i clienti devono essere ignorando NSGs. Seguire comuni sicurezza consigliate toominimize hello rete superfici esposte toohello Internet. Blocco di intervalli di indirizzi remoti hello consentito distribuzioni hello tooaccess o protocolli specifici dell'applicazione hello e porte aperte. In alcuni casi, tuttavia, non è possibile usare questa procedura. Ad esempio, se sono dotate di un sito Web esterno in Azure, rete perimetrale hello deve consentire hello richieste web provenienti da indirizzi IP pubblici, ma solo necessario aprire le porte di applicazione web di hello: TCP sulla porta 80 e/o TCP sulla porta 443.
* **Tabella di routing:** subnet della rete perimetrale hello stesso deve essere in grado di toocommunicate toohello Internet direttamente, ma non ne consente la comunicazione diretta tooand reti hello back-end o in locale senza passare attraverso un firewall o dispositivo di sicurezza.
* **Configurazione dello strumento di protezione:** tooroute e analizzare i pacchetti tra rete perimetrale hello e rest hello delle reti hello protetto, hello dispositivi di sicurezza, ad esempio firewall, ID, e i dispositivi di indirizzi IP possono essere multihomed. È possibile che i gruppi NIC separati per la rete perimetrale hello e subnet di back-end hello. le schede NIC Hello nella rete perimetrale hello comunicare direttamente tooand da hello Internet, con hello NSGs corrispondente e perimetrale hello tabella di routing di rete. NIC Hello connessione toohello subnet di back-end sono più limitati NSGs e tabelle di routing di subnet di back-end corrispondente hello.
* **Funzionalità del dispositivo protezione:** distribuiti nella rete perimetrale hello in genere dispositivi di sicurezza di hello eseguono hello seguenti funzionalità:
  * Firewall: Applicare le regole del firewall o criteri di controllo di accesso per le richieste in ingresso hello.
  * Rilevamento e la prevenzione delle minacce: il rilevamento e la risoluzione di attacchi di hello Internet.
  * Controllo e registrazione: gestione di log dettagliati per il controllo e l'analisi.
  * Il proxy inverso: reindirizzamento in ingresso hello richiede server back-end corrispondente toohello. Il reindirizzamento implica mapping e conversione indirizzi di destinazione hello nei dispositivi front-end hello, in genere i firewall, gli indirizzi di server back-end toohello.
  * Inoltrare proxy: fornendo NAT e l'esecuzione di controllo per la comunicazione avviata dall'interno di rete virtuale di hello toohello Internet.
  * Router: Inoltro del traffico in ingresso e tra subnet all'interno di rete virtuale hello.
  * Dispositivo VPN: funge da hello cross-premise gateway VPN per la connettività cross-premise VPN tra cliente sulle reti locali e reti virtuali di Azure.
  * Server VPN: accettazione dei client VPN connessione tooAzure le reti virtuali.

> [!TIP]
> Mantenere hello separato di due gruppi seguenti: persone hello tooaccess hello perimetrale rete sicurezza ingranaggio e hello utenti autorizzati autorizzati come gli amministratori di sviluppo, distribuzione o le operazioni di applicazione. Se si mantengono separati questi gruppi, sarà possibile separare nettamente i compiti e impedire a una singola persona di ignorare i controlli di sicurezza delle applicazioni e della rete.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Toobe domande frequenti durante la compilazione dei limiti di rete
In questa sezione, a meno che non indicato in particolare, il termine hello "reti" si riferisce tooprivate Azure reti virtuali create da un amministratore della sottoscrizione. Hello non riferirsi toohello reti fisiche sottostanti in Azure.

Inoltre, reti virtuali di Azure sono spesso utilizzati tooextend tradizionali sulle reti locali. È possibile tooincorporate site-to-site o ExpressRoute ibrida soluzioni con architetture di rete perimetrale di rete. Questo collegamento ibrido è un fattore da tenere in considerazione durante la creazione dei limiti di sicurezza della rete.

Hello tre domande seguenti sono tooanswer critici quando si crea una rete con una rete perimetrale e più i limiti di sicurezza.

#### <a name="1-how-many-boundaries-are-needed"></a>1) Quanti limiti servono?
il primo punto di decisione Hello è toodecide i limiti di sicurezza quanti sono necessari in uno scenario specifico:

* Un singolo limite: una rete perimetrale front-end hello, tra la rete virtuale di hello e hello Internet.
* Due limiti: una sul lato Internet della rete perimetrale hello hello e un altro tra subnet della rete perimetrale hello e le subnet di back-end hello hello reti virtuali di Azure.
* Tre limiti: uno sul lato Internet hello della rete perimetrale hello, uno tra una rete perimetrale hello e le subnet di back-end e uno tra le subnet di back-end hello e rete locale hello.
* Numero di limiti: variabile. A seconda dei requisiti di sicurezza, non sussiste alcuna limitazione del numero dei limiti di sicurezza che possono essere applicati in una determinata rete toohello.

Hello numero e tipo di limiti necessarie variano in base rischio per la tolleranza di errore e hello scenario specifico della società in fase di implementazione. Si tratta spesso di una decisione comune presa da più gruppi di un'organizzazione, spesso in collaborazione con un team responsabile dei rischi e della conformità, un team responsabile della rete e della piattaforma e un team responsabile dello sviluppo di applicazioni. Orientamento di sicurezza appropriato hello tooensure questa decisione per ogni implementazione devono includere una pronuncia persone con informazioni di sicurezza, i dati di hello coinvolti e le tecnologie di hello in uso.

> [!TIP]
> Utilizzare il numero più piccolo di hello di limiti che soddisfano i requisiti di sicurezza hello per una determinata situazione. Con i limiti della altre, operazioni e sulla risoluzione dei problemi può risultare più difficile, nonché hello gestione overhead coinvolti con gestione hello più criteri di limite nel tempo. Un numero insufficiente di limiti, tuttavia, comporta un aumento del rischio. Trovare un equilibrio hello è fondamentale.
>
>

![6]

Hello figura precedente viene illustrata una panoramica generale di una rete di limite di tre sicurezza. i limiti di Hello sono compresi tra hello rete perimetrale e Internet hello, hello Azure front-end e back-end subnet private e hello Azure subnet back-end e hello locale aziendale.

#### <a name="2-where-are-hello-boundaries-located"></a>2) in cui si trovano i limiti di hello?
Una volta che viene deciso al numero di hello di limiti, in cui li è tooimplement hello successivo punto di decisione. In genere, sono disponibili tre opzioni:

* Usare un servizio intermediario basato su Internet (ad esempio, un Web application firewall basato su cloud, non trattato in questo documento)
* Usare funzionalità native e/o appliance virtuali di rete in Azure
* Utilizzo di dispositivi fisici nella rete locale di hello

Nelle reti di Azure esclusivamente, opzioni di hello sono funzionalità native di Azure (ad esempio, Bilanciamento carico di Azure) o ai dispositivi di rete virtuale da hello ampio ecosistema partner di Azure (ad esempio, il punto di controllo firewall).

Se un limite è necessaria tra Azure e una rete locale, i dispositivi di sicurezza hello possono risiedere in entrambi i lati della connessione hello (o entrambi i lati). Una decisione di conseguenza deve essere effettuata in un dispositivo di sicurezza tooplace percorso hello.

Nella figura precedente hello hello Internet-a-perimetrale i limiti di hello front-to-back-end sono interamente contenuti in Azure e devono essere una funzionalità native di Azure o ai dispositivi di rete virtuale. Dispositivi di sicurezza su hello limite tra Azure (subnet back-end) e la rete aziendale hello potrebbe essere in hello lato Azure o sul lato locale di hello o una combinazione di dispositivi su entrambi i lati. Può essere vantaggi significativi e opzione tooeither svantaggi è necessario considerare seriamente.

Ad esempio, utilizzando il dispositivo di sicurezza fisica esistente su hello locale sul lato di rete ha il vantaggio di hello che non è necessaria alcuna nuova ingranaggio. È sufficiente la riconfigurazione dei dispositivi esistenti. Hello svantaggio, tuttavia, è che tutto il traffico deve tornare da Azure toohello locale rete toobe rilevato da ingranaggio sicurezza hello. In questo modo il traffico di Azure in Azure potrebbe causare una latenza significativa e influiscono sull'esperienza utente e le prestazioni di applicazioni, se è stato forzato toohello indietro per l'applicazione di criteri di sicurezza di rete locale.

#### <a name="3-how-are-hello-boundaries-implemented"></a>3) come vengono implementati i limiti di hello?
Ogni limite di sicurezza sarà probabilmente necessario requisiti di funzionalità diverso (ad esempio, gli ID e regole del firewall hello lato Internet della rete perimetrale hello, ma solo gli ACL tra una rete perimetrale hello e subnet back-end). Decidere quale dispositivo (o il numero di dispositivi) dipende toouse hello requisiti di scenario e sicurezza. Hello nella sezione seguente, gli esempi 1, 2 e 3 illustrano alcune opzioni che potrebbero essere usate. Verifica delle funzionalità di rete nativo Azure hello e dispositivi hello disponibili in Azure dall'ecosistema di partner hello Mostra hello innumerevoli opzioni disponibile toosolve praticamente a qualsiasi scenario.

Un altro punto di decisione di implementazione della chiave è la modalità tooconnect hello locale rete con Azure. È necessario utilizzare hello Azure gateway virtuale o un dispositivo di rete virtuale? Queste opzioni sono descritte più dettagliatamente in hello successiva sezione (esempi 4, 5 e 6).

Inoltre, potrebbe essere necessario consultare informazioni sul traffico tra reti virtuali all'interno di Azure. Questi scenari verranno aggiunto in futuro hello.

Dopo avere stabilito le risposte hello domande precedenti toohello, hello [avvio veloce](#fast-start) sezione consente di identificare quali esempi sono più appropriati per un determinato scenario.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Esempi: Creare limiti di sicurezza con le reti virtuali di Azure
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Esempio 1 compilazione un toohelp rete perimetrale proteggere le applicazioni con NSGs
[Eseguire il backup di start tooFast](#fast-start) | [Detailed compilare le istruzioni per questo esempio][Example1]

[![7]][7]

#### <a name="environment-description"></a>Descrizione dell'ambiente
In questo esempio, è associata una sottoscrizione che contiene hello seguenti risorse:

- Un unico gruppo di risorse
- Una rete virtuale con due subnet: front-end e back-end
- Un gruppo di sicurezza di rete che viene applicato tooboth subnet
- Un server Windows che rappresenta un server Web applicazioni ("IIS01")
- Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")
- Un server Windows che rappresenta un server DNS ("DNS01")
- Un indirizzo IP pubblico associato hello applicazione web server

Per gli script e un modello di gestione risorse di Azure, vedere hello [istruzioni di compilazione][Example1].

#### <a name="nsg-description"></a>Descrizione di un gruppo di sicurezza di rete
In questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono poi caricate sei regole.

> [!TIP]
> In generale, è necessario creare regole "Consenti" specifiche prima, seguita da più generico hello "Nega" le regole. Hello assegnata la priorità determina quali regole vengono valutate per prime. Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole. Regole di gruppo possono essere applicate uno hello direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).
>
>

In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:

1. Il traffico DNS interno (porta 53) è consentito.
2. È consentito il traffico RDP (porta 3389) da hello Internet tooany macchina virtuale.
3. È consentito il traffico HTTP (porta 80) dal server di tooweb Internet hello (IIS01).
4. Qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1 è consentita.
5. Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello intera rete virtuale (entrambi subnet) è stato negato.
6. Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello di hello subnet front-end è stato negato.

Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso dal server web toohello Internet hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata. Tuttavia, poiché la regola 3 ha una priorità maggiore, verrà applicata solo tale regola e la regola 5 non verrà presa in considerazione. Richiesta HTTP hello sarebbe è pertanto a server web toohello. Se il traffico stesso cercava server hello DNS01 tooreach, regola 5 (Nega) sarebbe hello tooapply primo e il traffico di hello non sarebbe consentito toopass toohello server. Regola 6 (Nega) blocchi hello subnet front-end dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4). Il set di regole protegge rete back-end hello nel caso in cui un utente malintenzionato compromette l'applicazione web hello in front-end hello. autore dell'attacco Hello sarebbe non dispongono di accesso toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).

È una regola in uscita predefinita che consente il traffico in uscita toohello Internet. Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita. toolock verso il basso il traffico in entrambe le direzioni, routing definito dall'utente è obbligatorio (vedere l'esempio 3).

#### <a name="conclusion"></a>Conclusioni
Questo esempio è un modo relativamente semplice e diretto di isolamento di subnet di back-end hello dal traffico in ingresso. Per ulteriori informazioni, vedere hello [istruzioni di compilazione][Example1]. Le istruzioni includono:

* Come toobuild questo perimetrale della rete con gli script di PowerShell classici.
* Come toobuild questo perimetrale della rete con un modello di gestione risorse di Azure.
* Descrizioni dettagliate di ogni comando del gruppo di sicurezza di rete
* Scenari dettagliati del flusso di traffico che illustrano il modo in cui il traffico viene consentito o negato su ogni livello


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Compilazione di esempio 2 un toohelp rete perimetrale proteggere le applicazioni con un firewall e NSGs
[Eseguire il backup di start tooFast](#fast-start) | [Detailed compilare le istruzioni per questo esempio][Example2]

[![8]][8]

#### <a name="environment-description"></a>Descrizione dell'ambiente
In questo esempio, è associata una sottoscrizione che contiene hello seguenti risorse:

* Un unico gruppo di risorse
* Una rete virtuale con due subnet: front-end e back-end
* Un gruppo di sicurezza di rete che viene applicato tooboth subnet
* Un accessorio virtuale di rete, in questo caso un firewall, connesso subnet front-end toohello
* Un server Windows che rappresenta un server Web applicazioni ("IIS01")
* Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01")

Per gli script e un modello di gestione risorse di Azure, vedere hello [istruzioni di compilazione][Example2].

#### <a name="nsg-description"></a>Descrizione di un gruppo di sicurezza di rete
In questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono poi caricate sei regole.

> [!TIP]
> In generale, è necessario creare regole "Consenti" specifiche prima, seguita da più generico hello "Nega" le regole. Hello assegnata la priorità determina quali regole vengono valutate per prime. Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole. Regole di gruppo possono essere applicate uno hello direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).
>
>

In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:

1. Il traffico DNS interno (porta 53) è consentito.
2. È consentito il traffico RDP (porta 3389) da hello Internet tooany macchina virtuale.
3. Internet (tutte le porte) traffico toohello dispositivi di rete virtuali (firewall) sono consentito.
4. Qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1 è consentita.
5. Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello intera rete virtuale (entrambi subnet) è stato negato.
6. Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello di hello subnet front-end è stato negato.

Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso da toohello Windows firewall, hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata. Tuttavia, poiché la regola 3 ha una priorità maggiore, verrà applicata solo tale regola e la regola 5 non verrà presa in considerazione. In questo modo la richiesta HTTP hello sia possibile usare toohello firewall. Se il traffico stesso cercava server hello IIS01 tooreach, anche se è nella subnet front-end hello, regola 5 (Nega) si applicano, e il traffico di hello non sarebbe consentito toopass toohello server. Regola 6 (Nega) blocchi hello subnet front-end dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4). Il set di regole protegge rete back-end hello nel caso in cui un utente malintenzionato compromette l'applicazione web hello in front-end hello. autore dell'attacco Hello sarebbe non dispongono di accesso toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).

È una regola in uscita predefinita che consente il traffico in uscita toohello Internet. Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita. toolock verso il basso il traffico in entrambe le direzioni, routing definito dall'utente è obbligatorio (vedere l'esempio 3).

#### <a name="firewall-rule-description"></a>Descrizione della regola del firewall
Firewall hello, regole di inoltro devono essere creata. Poiché questo esempio solo le route del traffico Internet in entrata toohello firewall e server web toohello quindi, solo uno di inoltro rete Network address translation () non è necessario regola.

regola di inoltro Hello accetta qualsiasi indirizzo di origine in ingresso che colpisce firewall hello tentativo tooreach HTTP (porta 80 o 443 per HTTPS). Dispone di inviati all'esterno dell'interfaccia locale del firewall hello e reindirizzato toohello server web con indirizzo IP del 10.0.1.5 hello.

#### <a name="conclusion"></a>Conclusioni
Questo esempio è un modo relativamente semplice di protezione delle applicazioni con un firewall e l'isolamento di subnet di back-end hello dal traffico in ingresso. Per ulteriori informazioni, vedere hello [istruzioni di compilazione][Example2]. Le istruzioni includono:

* Come toobuild questo perimetrale della rete con gli script di PowerShell classici.
* Come toobuild in questo esempio con un modello di gestione risorse di Azure.
* Descrizioni dettagliate di ogni comando del gruppo di sicurezza di rete e di ogni regola del firewall
* Scenari dettagliati del flusso di traffico che illustrano il modo in cui il traffico viene consentito o negato su ogni livello

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Esempio 3 compilazione un toohelp rete perimetrale proteggere reti e un firewall e UDR NSG
[Eseguire il backup di start tooFast](#fast-start) | [Detailed compilare le istruzioni per questo esempio][Example3]

[![9]][9]

#### <a name="environment-description"></a>Descrizione dell'ambiente
In questo esempio, è associata una sottoscrizione che contiene hello seguenti risorse:

* Un unico gruppo di risorse
* Una rete virtuale con tre subnet: "SecNet", "FrontEnd" e "BackEnd"
* Un accessorio virtuale di rete, in questo caso un firewall, connesso toohello SecNet subnet
* Un server Windows che rappresenta un server Web applicazioni ("IIS01")
* Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01")

Per gli script e un modello di gestione risorse di Azure, vedere hello [istruzioni di compilazione][Example3].

#### <a name="udr-description"></a>Descrizione delle route definite dall'utente (UDR)
Per impostazione predefinita, hello seguendo le route di sistema è definito come:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hello VNETLocal è sempre uno o più prefissi di indirizzo definita che costituiscono la rete virtuale di hello per tale rete specifico (ovvero, vengono modificate da rete toovirtual di rete virtuale, a seconda della modalità di definizione di ogni rete virtuale specifica). le route di sistema rimanenti Hello sono statiche e predefinito come indicato nella tabella hello.

In questo esempio vengono creati due tabelle di routing, rispettivamente per la subnet front-end e back-end di hello. Ogni tabella viene caricato con routing statico appropriato per hello subnet specificato. In questo esempio, ogni tabella dispone di tre route indirizzare tutto il traffico (0.0.0.0/0) attraverso il firewall hello (hop successivo = indirizzo IP dell'accessorio virtuale):

1. Traffico della subnet locale con nessun Hop successivo definito tooallow subnet locale il traffico toobypass hello firewall.
2. Traffico della rete virtuale con la definizione di un hop successivo come firewall, L'hop successivo esegue l'override regola predefinita hello che consente di direttamente tooroute il traffico di rete virtuale locale.
3. Il traffico rimanente tutti (0 o 0) con un Hop successivo è definito come hello firewall.

> [!TIP]
> Indisponibilità di voce di subnet locale hello in hello UDR interruzioni subnet locale comunicazioni.
>
> * In questo esempio, è fondamentale che punta tooVNETLocal 10.0.1.0/24! Senza di esso, lasciando hello Server Web (10.0.1.4) destinati a tooanother locale server, ad esempio, 10.0.1.25 pacchetto avrà esito negativo come verranno inviati toohello NVA. Hello NVA invierà ad esso toohello subnet e subnet hello verrà inviarlo toohello NVA in un ciclo infinito.
> * possibilità di Hello di un loop di routing sono in genere più elevati in dispositivi con più schede di rete che sono connessi tooseparate subnet, che è spesso dei dispositivi locale tradizionale.
>
>

Una volta create le tabelle di routing hello, devono essere associati tootheir subnet. Hello subnet front-end, tabella di routing, una volta creata e associata toohello subnet, sarà simile a questo output:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR ora possono essere applicati toohello subnet del gateway ExpressRoute quali hello è connesso il circuito.
>
> Negli esempi 3 e 4 sono illustrati esempi di come tooenable il perimetro della rete con ExpressRoute o di rete da sito a sito.
>
>

#### <a name="ip-forwarding-description"></a>Descrizione dell'inoltro IP
L'inoltro IP è un tooUDR funzionalità complementare. L'inoltro IP è un'impostazione in un dispositivo virtuale che consente di tooreceive il traffico indirizzato non specificamente toohello dispositivo e quindi inoltra destinazione finale di tooits tale traffico.

Ad esempio, se AppVM01 il server DNS01 toohello richiesta, UDR indirizza il traffico toohello firewall. Con l'inoltro IP abilitato, il traffico di hello per destinazione DNS01 hello (10.0.2.4) è accettato dal dispositivo hello (10.0.0.4) e quindi vengono inoltrato da destinazione finale tooits (10.0.2.4). Senza l'inoltro IP abilitate sul firewall hello, il traffico verrebbe non accettato dal dispositivo hello anche se la tabella di route hello dispone di firewall hello come hop successivo hello. toouse appliance virtuale, è inoltro insieme UDR dell'indirizzo IP tooenable tooremember critici.

#### <a name="nsg-description"></a>Descrizione di un gruppo di sicurezza di rete
In questo esempio viene creato un gruppo di sicurezza di rete, in cui viene poi caricata una singola regola. Questo gruppo viene quindi associato solo toohello front-end e back-end nelle subnet (non hello SecNet). Viene compilato in modo dichiarativo hello seguente regola:

* Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello intera rete virtuale (tutte le subnet) è stato negato.

Anche se in questo esempio vengono usati i gruppi di sicurezza di rete: lo scopo principale consiste nel creare un secondo livello di difesa contro errori di configurazione manuale. Hello obiettivo è tooblock tutto il traffico in ingresso da hello Internet tooeither hello subnet front-end o back-end. Il traffico solo flusso firewall hello SecNet subnet toohello (e quindi, se necessario, le subnet front-end o back-end toohello). Inoltre, con regole UDR hello sul posto, tutto il traffico che in hello subnet front-end o back-end sarebbe indirizzato out toohello firewall (grazie tooUDR). firewall Hello visualizzare il traffico come un flusso asimmetrico e riduzione in caso di traffico in uscita hello. In questo modo sono disponibili tre livelli di sicurezza protezione subnet hello:

* Nessun indirizzo IP pubblico su qualsiasi scheda di interfaccia di rete front-end o back-end.
* NSGs negando traffico hello Internet.
* traffico asimmetrica eliminazione firewall Hello.

Un punto di interesse riguardanti hello gruppo in questo esempio è che contenga una sola regola, ovvero toodeny Internet traffico toohello intera rete virtuale, inclusi subnet sicurezza hello. Tuttavia, poiché hello che è solo di gruppo associata toohello front-end e subnet di back-end, la regola hello non viene elaborata sul traffico in ingresso toohello subnet di sicurezza. Di conseguenza, il traffico passa toohello subnet di sicurezza.

#### <a name="firewall-rules"></a>Regole del firewall
Firewall hello, regole di inoltro devono essere creata. Poiché il firewall hello di blocco o inoltro tutto in ingresso, uscita e il traffico di rete virtuale all'interno della stessa, sono necessarie numerose regole del firewall. Inoltre, tutto il traffico in ingresso raggiunge l'indirizzo IP pubblico del servizio di sicurezza hello (su porte diverse), toobe elaborati dal firewall hello. È consigliabile creare i flussi logici toodiagram hello prima di configurare le subnet hello e regole del firewall, tooavoid rielaborare in un secondo momento. Hello nella figura seguente è una vista logica hello regole del firewall per questo esempio:

![10]

> [!NOTE]
> In base a hello che Appliance virtuale di rete utilizzato, porte di gestione di hello variano. In questo esempio si fa riferimento a Barracuda NextGen Firewall, che usa le porte 22, 801 e 807. Consultare hello accessorio fornitore documentazione toofind hello esatta porte utilizzate per la gestione dei dispositivi hello in uso.
>
>

#### <a name="firewall-rules-description"></a>Descrizione delle regole del firewall
Nel precedente diagramma logico di hello, subnet sicurezza hello non viene visualizzato perché firewall hello è l'unica risorsa di hello subnet. regole del firewall hello e come logicamente consentire o negare i flussi di traffico, non hello indirizzato percorso effettivo, viene visualizzato il diagramma Hello. Inoltre, due ottetti dell'indirizzo IP locale hello per facilitarne la lettura dell'ultima porte hello selezionate per il traffico RDP hello sono porte nell'intervallo superiore (8014 – 8026) e sono stati selezionati tooloosely allinearlo hello (ad esempio, il server locale 10.0.1.4 è associato l'indirizzo con una porta esterna 8014). È tuttavia possibile usare qualsiasi porta superiore non in conflitto.

Per questo esempio, sono necessari sette tipi di regole:

* Regole esterne (per il traffico in ingresso):
  1. Regola di gestione del firewall: regole di reindirizzamento di questa App consente il traffico toopass toohello porte di gestione del dispositivo di hello rete virtuale.
  2. Le regole RDP (per ogni server di Windows): questi quattro regole, una per ogni server, consentono la gestione di hello singoli server tramite RDP. quattro regole RDP Hello potrebbero anche essere compressi in una regola, a seconda delle funzionalità di hello del dispositivo virtuale rete hello in uso.
  3. Regole del traffico di applicazione: sono presenti due di queste regole, hello prima per il traffico web front-end hello e hello secondo per il traffico di back-end hello (ad esempio server toodata livello web). configurazione Hello di queste regole dipende dall'architettura di rete hello (in cui vengono collocati i server) e flussi di traffico (il tipo di traffico hello direzione flussi e le porte utilizzate).
     * prima regola Hello consente hello effettivo traffico tooreach hello applicazione server applicazioni. Sebbene hello altre regole consentono per la gestione e sicurezza, le regole del traffico dell'applicazione sono cosa consentono tooaccess utenti o servizi esterni alle applicazioni di hello. In questo esempio è presente un singolo server Web sulla porta 80. Pertanto una singola applicazione regola del firewall reindirizza il traffico in entrata toohello IP esterno, indirizzo IP interno di toohello web server. verrà convertita sessione traffico Hello reindirizzato tramite NAT toohello interno del server.
     * seconda regola Hello è hello regola back-end tooallow hello tootalk toohello AppVM01 server del server web (ma non AppVM02) tramite qualsiasi porta.
* Regole interne (per il traffico tra le reti virtuali)
  1. Regola in uscita tooInternet: questa regola consente il traffico da qualsiasi rete toopass toohello selezionato reti. Questa regola è in genere una regola predefinita già installati nel firewall hello, ma in uno stato disabilitato. È consigliabile abilitarla per questo esempio.
  2. Regola DNS: questa regola consente solo DNS (porta 53) traffico toopass toohello server DNS. Per questo ambiente, la maggior parte del traffico dal back-end di hello front-end toohello è bloccato. Questa regola consente in modo specifico il traffico DNS da qualsiasi subnet locale.
  3. Regola toosubnet subnet: la regola è tooallow qualsiasi server nel server di hello subnet back-end tooconnect tooany nella subnet front-end hello (ma non hello inversa).
* Regola alternativo (per il traffico che non soddisfa uno qualsiasi dei hello precedente):
  1. Tutto il traffico regola di negazione: questa regola di negazione deve essere sempre regola finale di hello (in termini di priorità) e di conseguenza se un flusso di traffico non toomatch una delle regole precedenti hello viene eliminato da questa regola. La regola è predefinita, in genere sul posto e attiva, Nessuna modifica è in genere necessario toothis regola.

> [!TIP]
> In hello seconda applicazione traffico regola, toosimplify in questo esempio, è consentita qualsiasi porta. In uno scenario reale, intervalli di porte e indirizzi più specifici hello devono essere utilizzato tooreduce superficie di attacco hello di questa regola.
>
>

Una volta create le regole precedenti hello, è importante priorità hello tooreview del traffico di tooensure ogni regola è consentita o negata in base alle esigenze. Per questo esempio, le regole di hello sono in ordine di priorità.

#### <a name="conclusion"></a>Conclusioni
Questo esempio è più complesso ma completare modalità di protezione e isolamento rete hello di hello esempi precedenti. (Esempio 2 protegge solo un'applicazione hello ed esempio 1 isola solo subnet). Questa struttura consente il monitoraggio del traffico in entrambe le direzioni e non solo i server di applicazioni in ingresso hello protegge ma vengono applicati i criteri di sicurezza di rete per tutti i server nella rete. Inoltre, a seconda utilizzato accessorio hello, il controllo completo del traffico e riconoscimento può essere ottenute. Per ulteriori informazioni, vedere hello [istruzioni di compilazione][Example3]. Le istruzioni includono:

* Come toobuild perimetrale in questo esempio di rete con gli script di PowerShell classici.
* Come toobuild in questo esempio con un modello di gestione risorse di Azure.
* Descrizioni dettagliate di ogni route definita dall'utente, ogni comando del gruppo di sicurezza di rete e ogni regola del firewall
* Scenari dettagliati del flusso di traffico che illustrano il modo in cui il traffico viene consentito o negato su ogni livello

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Esempio 4: Aggiungere una connessione ibrida con un'appliance virtuale da sito a sito e con una rete virtuale privata (VPN)
[Eseguire il backup di start tooFast](#fast-start) | Istruzioni di compilazione disponibili dettagliate appena

[![11]][11]

#### <a name="environment-description"></a>Descrizione dell'ambiente
Rete ibrida tramite un accessorio virtuale di rete (NVA) può essere aggiunti tooany dei tipi di rete perimetrale hello descritto negli esempi 1, 2 o 3.

Come illustrato nella figura precedente hello, una connessione VPN su Internet (site-to-site) hello è usato tooconnect tooan di rete rete virtuale di Azure tramite un NVA un locale.

> [!NOTE]
> Se si usa ExpressRoute hello Peering pubblico di Azure opzione è abilitata, è necessario creare una route statica. Questa route statica deve indirizzare toohello l'indirizzo IP VPN della vulnerabilità della rete aziendale Internet e non tramite hello connessione ExpressRoute. Hello NAT necessario hello Azure ExpressRoute Peering pubblico opzione possibile interrompere una sessione VPN hello.
>
>

Dopo aver hello VPN è presente, hello NVA diventa hub centrale di hello per tutte le reti e le subnet. le regole di inoltro di firewall Hello determinano il tipo di traffico consentiti flussi, vengono convertite tramite NAT, vengono reindirizzati o vengono eliminati (anche per i flussi di traffico tra Azure e di rete locale hello).

Flussi di traffico da considerare con attenzione, perché possono essere ottimizzati o ridotto da questo schema progettuale, a seconda delle specifiche di hello caso d'uso.

Usando l'ambiente hello compilato nell'esempio 3 e quindi aggiungendo una connessione VPN da sito a sito di rete ibrida, produce hello seguente struttura:

[![12]][12]

router locale Hello o altri dispositivi di rete compatibile con il NVA per VPN, sarebbe client VPN hello. Il dispositivo fisico sarà responsabile per l'inizializzazione e la gestione connessione VPN hello con il NVA.

Logicamente toohello NVA, rete hello è simile a quattro separato "aree di protezione" con le regole di hello sulla hello NVA hello primario direttore il traffico tra queste aree:

![13]

#### <a name="conclusion"></a>Conclusioni
aggiunta di Hello di un tooan connessione site-to-site VPN ibrida rete rete virtuale di Azure è possibile estendere rete locale hello in Azure in modo sicuro. Utilizzando una connessione VPN, il traffico viene crittografato e instrada tramite hello Internet. Hello NVA in questo esempio fornisce una posizione centrale di tooenforce e gestire i criteri di sicurezza hello. Per ulteriori informazioni, vedere hello dettagliata compilare istruzioni (misura). Le istruzioni includono:

* Come toobuild perimetrale in questo esempio di rete con gli script di PowerShell.
* Come toobuild in questo esempio con un modello di gestione risorse di Azure.
* Scenari dettagliati di flussi di traffico che illustrano il modo in cui il traffico scorre nella struttura.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Esempio 5: Aggiungere una connessione ibrida con un gateway VPN di Azure da sito a sito
[Eseguire il backup di start tooFast](#fast-start) | Istruzioni di compilazione disponibili dettagliate appena

[![14]][14]

#### <a name="environment-description"></a>Descrizione dell'ambiente
Rete ibrida tramite un gateway VPN di Azure è possibile aggiungere il tipo di rete perimetrale tooeither descritto negli esempi 1 o 2.

Come illustrato nella figura precedente hello, una connessione VPN su Internet (site-to-site) hello è tooconnect usato un tooan di rete locale rete virtuale di Azure tramite un gateway VPN di Azure.

> [!NOTE]
> Se si usa ExpressRoute hello Peering pubblico di Azure opzione è abilitata, è necessario creare una route statica. Questa route statica deve indirizzare toohello l'indirizzo IP VPN della vulnerabilità della rete Internet aziendale e non tramite hello ExpressRoute WAN. Hello NAT necessario hello Azure ExpressRoute Peering pubblico opzione possibile interrompere una sessione VPN hello.
>
>

Hello nella figura seguente mostra hello due bordi di rete in questo esempio. Sul lato prima hello, hello NVA e NSGs controllare i flussi di traffico per le reti di Azure all'interno e tra Azure e hello Internet. bordo secondo Hello è il gateway VPN di Azure hello, ovvero un bordo di rete separata e isolate tra sedi locali e Azure.

Flussi di traffico da considerare con attenzione, perché possono essere ottimizzati o ridotto da questo schema progettuale, a seconda delle specifiche di hello caso d'uso.

Usando l'ambiente hello compilato nell'esempio 1 e quindi aggiungendo una connessione VPN da sito a sito di rete ibrida, produce hello seguente struttura:

[![15]][15]

#### <a name="conclusion"></a>Conclusioni
aggiunta di Hello di un tooan connessione site-to-site VPN ibrida rete rete virtuale di Azure è possibile estendere rete locale hello in Azure in modo sicuro. Usa gateway VPN di Azure native hello, il traffico crittografato IPSec e lo instrada tramite hello Internet. Inoltre, con gateway VPN di Azure hello, è possibile fornire un'opzione a basso costo (non una licenza aggiuntiva costo come con NVAs di terze parti). Questa soluzione risulta estremamente conveniente nell'esempio 1, in cui non vengono usate appliance virtuali di rete. Per ulteriori informazioni, vedere hello dettagliata compilare istruzioni (misura). Le istruzioni includono:

* Come toobuild perimetrale in questo esempio di rete con gli script di PowerShell.
* Come toobuild in questo esempio con un modello di gestione risorse di Azure.
* Scenari dettagliati di flussi di traffico che illustrano il modo in cui il traffico scorre nella struttura.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>Esempio 6: Aggiungere una connessione ibrida con ExpressRoute
[Eseguire il backup di start tooFast](#fast-start) | Istruzioni di compilazione disponibili dettagliate appena

[![16]][16]

#### <a name="environment-description"></a>Descrizione dell'ambiente
Rete ibrida tramite ExpressRoute connessione peering privata può essere aggiunto il tipo di rete perimetrale tooeither descritto negli esempi 1 o 2.

Come illustrato nella figura precedente hello, ExpressRoute di peering privato fornisce una connessione diretta tra la rete locale e hello rete virtuale di Azure. Il traffico passa solo hello servizio provider rete e della rete di Microsoft Azure hello, non tocca mai hello Internet.

> [!TIP]
> Uso di ExpressRoute mantiene il traffico di rete aziendali off hello Internet. agevolando contratti di servizio dal provider ExpressRoute. Gateway Azure Hello può passare i Gbps too10 con ExpressRoute, mentre con connessioni VPN da sito a sito, la velocità effettiva massima di Gateway Azure hello è 200 Mbps.
>
>

Come illustrato nel seguente diagramma hello, con questo hello opzione ambiente ora dispone di due bordi di rete. Hello NVA e gruppo controllo flussi di traffico per le reti di Azure all'interno e tra Azure e hello Internet, mentre il gateway hello è un bordo di rete separata e isolate tra sedi locali e Azure.

Flussi di traffico da considerare con attenzione, perché possono essere ottimizzati o ridotto da questo schema progettuale, a seconda delle specifiche di hello caso d'uso.

Usando l'ambiente hello compilato nell'esempio 1 e quindi aggiungendo una connessione di rete ibrida ExpressRoute, produce hello seguente struttura:

[![17]][17]

#### <a name="conclusion"></a>Conclusioni
aggiunta di Hello di una connessione di rete di Peering ExpressRoute privato è possibile estendere rete locale hello in Azure in una latenza protetta, inferiore e superiore esecuzione modo. Inoltre, utilizzando hello native Azure Gateway, come nel seguente esempio, opzione fornisce un basso costo (non di licenza aggiuntivo come con NVAs di terze parti). Per ulteriori informazioni, vedere hello dettagliata compilare istruzioni (misura). Le istruzioni includono:

* Come toobuild perimetrale in questo esempio di rete con gli script di PowerShell.
* Come toobuild in questo esempio con un modello di gestione risorse di Azure.
* Scenari dettagliati di flussi di traffico che illustrano il modo in cui il traffico scorre nella struttura.

## <a name="references"></a>Riferimenti
### <a name="helpful-websites-and-documentation"></a>Siti Web e documentazione utili
* Accedere ad Azure tramite Azure Resource Manager:
* Accesso ad Azure con PowerShell: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Documentazione sulle reti virtuali: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Documentazione sui gruppi di sicurezza di rete: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Documentazione sul routing definito dall'utente: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Gateway virtuali di Azure: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* VPN da sito a sito: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* Documentazione di ExpressRoute (essere toocheck che le sezioni di hello "Getting Started" e "Procedura"): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Diagramma di flusso sulle opzioni di sicurezza"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "Funzionalità di sicurezza di Azure"
[3]: ./media/best-practices-network-security/dmzcorporate.png "Rete perimetrale in una rete aziendale"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "Architettura di sicurezza di Azure"
[5]: ./media/best-practices-network-security/dmzazure.png "Rete perimetrale in una rete virtuale di Azure"
[6]: ./media/best-practices-network-security/dmzhybrid.png "Rete ibrida con tre limiti di sicurezza"
[7]: ./media/best-practices-network-security/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"
[8]: ./media/best-practices-network-security/example2design.png "Rete perimetrale in ingresso con appliance virtuale di rete e gruppo di sicurezza di rete"
[9]: ./media/best-practices-network-security/example3design.png "Rete perimetrale bidirezionale con appliance virtuale di rete, gruppo di sicurezza di rete e routing definito dall'utente"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "vista logica di hello regole del Firewall"
[11]: ./media/best-practices-network-security/example3designoptions.png "Rete perimetrale con appliance virtuale di rete connesso tramite rete ibrida"
[12]: ./media/best-practices-network-security/example4designs2s.png "Rete perimetrale con appliance virtuale di rete connesso tramite VPN da sito a sito"
[13]: ./media/best-practices-network-security/example4networklogical.png "Rete logica dal punto di vista dell'appliance virtuale di rete"
[14]: ./media/best-practices-network-security/example5designoptions.png "Rete perimetrale con gateway di Azure connesso tramite rete ibrida da sito a sito"
[15]: ./media/best-practices-network-security/example5designs2s.png "Rete perimetrale con gateway di Azure che usa la VPN da sito a sito"
[16]: ./media/best-practices-network-security/example6designoptions.png "Rete perimetrale con gateway di Azure connesso tramite rete ibrida ExpressRoute"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "Rete perimetrale con gateway di Azure che usa una connessione ExpressRoute"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
