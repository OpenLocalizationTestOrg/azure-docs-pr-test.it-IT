---
title: aaaSecuring il Internet delle cose da hello messa a terra backup | Documenti Microsoft
description: "Questo articolo descrive le funzionalità di sicurezza incorporati hello di Microsoft Azure IoT Suite hello"
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 10252dfa-8313-4a97-9bd6-a3f1345dd3be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: a97e8cea753641e1e3c895f44e3fde1e5739d665
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-from-hello-ground-up"></a>Sicurezza di Internet delle cose da hello messa a terra
Hello Internet delle cose (IoT) pone univoco sicurezza, privacy e conformità sfide toobusinesses in tutto il mondo. A differenza di tecnologia informatica tradizionale in cui questi problemi riguardano software e la relativa implementazione, IoT riguarda cosa accade quando cyber hello e mondi fisico hello convergono. Per proteggere IoT soluzioni, è necessario garantire un provisioning sicuro dei dispositivi, la connettività protetta tra questi dispositivi e cloud hello e protezione dei dati nel cloud hello durante l'elaborazione e archiviazione. A sfavore di queste funzionalità, tuttavia, giocano fattori quali dispositivi con risorse limitate, la distribuzione geografica delle implementazioni e un numero elevato di dispositivi all'interno di un'unica soluzione.

In questo articolo illustra come hello Microsoft Azure IoT Suite offre una soluzione di cloud privata e protetta di Internet delle cose. Hello Azure IoT Suite offre una soluzione end-to-end completa, con la protezione incorporata in ogni fase da hello messa a terra. Microsoft, lo sviluppo di software protetto fa parte di pratica di progettazione del software hello, impostato come radice in nostro decenni tempo esperienza di sviluppo di software protetto. tooensure, Security Development Lifecycle (SDL) è metodologia di sviluppo fondamentali hello, insieme a un host di servizi di sicurezza a livello di infrastruttura quali garanzia di sicurezza operativo (OSA) e Digital Crimes Unit hello Microsoft Security Response Center e Microsoft Malware Protection Center. 

Hello Azure IoT Suite offerte esclusive caratteristiche, effettuare il provisioning, la connessione a e l'archiviazione dei dati dai dispositivi IoT semplici e trasparenti e la maggior parte di tutti, secure. In questo articolo è esaminare le funzionalità di sicurezza di Azure IoT Suite hello e vengono descritte le strategie tooensure sicurezza, privacy e conformità problemi legati alla distribuzione. 

## <a name="introduction"></a>Introduzione
Hello Internet delle cose (IoT) è wave hello di hello futura, che offre alle aziende immediate e i costi tooreduce opportunità del mondo reale, aumentare i ricavi e trasformare i loro attività aziendali. Molte aziende, tuttavia, sono propense toodeploy IoT nelle proprie organizzazioni scadenza tooconcerns sulla sicurezza, privacy e conformità. Un punto principale problematiche proviene da univocità hello dell'infrastruttura di IoT hello, che unisce cyber hello e mondi fisici insieme, singoli rischi inerenti ad questi due mondi di composizione. Sicurezza di IoT relativo integrità hello tooensuring di codice in esecuzione su dispositivi, l'autenticazione di utenti e dispositivi, la definizione di deselezionare la proprietà di dispositivi (così come dati generati da tali dispositivi) ed è toocyber resilienti e attacchi fisici. 

Quindi, si verifica il problema di hello di privacy. Le società richiedono trasparenza nella raccolta dei dati, nella tipologia e nel motivo per cui i dati sono raccolti, negli utenti che accedono ai dati e che controllano gli accessi, e così via. Infine, esistono problemi di sicurezza generale delle apparecchiature hello insieme a persone di hello operativo li e di mantenere gli standard di settore di conformità.

Dato hello sicurezza, privacy, trasparenza e problemi di conformità, la scelta di provider di soluzioni IoT destra hello rimane una sfida. Unione di singole parti di IoT software e servizi forniti da un'ampia gamma di fornitori introduce lacune nella sicurezza, privacy, trasparenza e conformità, che può essere toodetect disco rigido, tanto risolvere. scelta di Hello del diritto di hello IoT software e il provider è basato sulla ricerca di provider che hanno l'ampia esperienza di esecuzione di servizi che interessano verticali e aree geografiche, ma sono anche in grado di tooscale in modo sicuro e trasparente. Analogamente, è utile per hello selezionato provider toohave decenni di esperienza con lo sviluppo sicuro del software in esecuzione su miliardi di computer in tutto il mondo e è panorama delle minacce hello tooappreciate possibilità hello rappresentato da questo nuovo ambiente di hello Internet di Cose.

## <a name="secure-infrastructure-from-hello-ground-up"></a>Infrastruttura sicura da hello messa a terra
Hello [Microsoft Cloud](https://www.microsoft.com/enterprise/microsoftcloud/default.aspx#fbid=WzBsRQi6aGk) infrastruttura supporta i clienti di più di un miliardo in 127 paesi. Il disegno su esperienza decenni prolungata compilazione software aziendali e l'esecuzione di alcune delle hello più grandi servizi online in HelloWorld, forniamo livelli più elevati di sicurezza avanzata, riservatezza, conformità e minaccia consigliate attenuazione maggiore di quanto la maggior parte dei clienti potrebbe ottenere in modo autonomo.

Il nostro [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/) fornisce un processo di sviluppo obbligatoria a livello aziendale che incorpora i requisiti di sicurezza in hello tutto il ciclo di vita. toohelp assicurarsi che le attività operative seguano hello stesso livello delle procedure di sicurezza, utilizziamo linee guida di sicurezza severe disposti nel processo garanzia di sicurezza operativo (OSA). È inoltre possibile utilizzare gli imprese di controllo di terze parti per la verifica in corso che soddisfatto l'obbligo di conformità e si effettuano gli sforzi protetto tramite la creazione di hello dei centri di eccellenza, tra cui hello Digital Crimes Unit Microsoft Security Risposta Center e Microsoft Malware Protection Center.

## <a name="microsoft-azure---secure-iot-infrastructure-for-your-business"></a>Microsoft Azure: protezione dell'infrastruttura IoT aziendale
Microsoft Azure offre una soluzione completa di cloud, che combina una raccolta in continua crescita di servizi cloud integrata: analitica, l'apprendimento, archiviazione, sicurezza, rete e web, con una protezione di toohello impegno leader del settore e la privacy dei dati. Il nostro [presuppongono violazione](https://azure.microsoft.com/blog/red-teaming-using-cutting-edge-threat-simulation-to-harden-the-microsoft-enterprise-cloud/) strategia utilizza un "red team dedicato" degli esperti di sicurezza software che simulare attacchi, test non consente hello Azure toodetect, protezione contro le minacce e il recupero da violazioni della sicurezza. Il nostro [risposta agli eventi imprevisti globale](https://www.microsoft.com/TrustCenter/Security/DesignOpSecurity) risolve team di hello clock effetti hello toomitigate di attacchi e attività dannose. team Hello segue le procedure stabilite per la gestione degli eventi imprevisti, la comunicazione e ripristino e vengono utilizzate interfacce individuabile e stimabili con partner interni ed esterni.

I sistemi offrono prevenzione e rilevamento intrusione continui, prevenzione da attacchi ai servizi, test di penetrazione regolari e strumenti forensi che permettono di identificare e mitigare le minacce. [Autenticazione a più fattori](../multi-factor-authentication/multi-factor-authentication.md) fornisce un ulteriore livello di sicurezza per gli utenti finali tooaccess hello rete. E per un'applicazione hello e provider di hosting hello, offriamo controllo di accesso, il monitoraggio, anti-malware, analisi delle vulnerabilità, patch e la gestione della configurazione.

Microsoft Azure IoT Suite Hello sfrutta i vantaggi di sicurezza hello e sulla privacy incorporata hello piattaforma Azure con i processi SDL e Analizzatore installazione OEM per lo sviluppo sicuro e l'operazione di tutti i software Microsoft. Queste procedure forniscono protezione dell'infrastruttura, protezione di rete e gestione delle identità e sicurezza toohello fondamentali caratteristiche di qualsiasi soluzione. 

Hello [IoT Hub Azure](../iot-hub/iot-hub-what-is-iot-hub.md) all'interno di hello [IoT Suite](iot-suite-what-is-azure-iot.md) offre un servizio completamente gestito che consente la comunicazione bidirezionale affidabile e sicura tra i dispositivi IoT e servizi di Azure, ad esempio [Azure Machine Learning](../machine-learning/machine-learning-what-is-machine-learning.md) e [Azure flusso Analitica](../stream-analytics/stream-analytics-introduction.md) utilizzando le credenziali di sicurezza per ogni dispositivo e il controllo di accesso.

toobest comunicare le funzionalità di sicurezza e privacy incorporate in hello Azure IoT Suite, è stato suddiviso suite hello in tre aree di sicurezza primario hello. 

![Azure IoT Suite](media/securing-iot-ground-up/securing-iot-ground-up-fig3.png)

### <a name="secure-device-provisioning-and-authentication"></a>Proteggere il provisioning dei dispositivi e l'autenticazione
Hello Azure IoT Suite consente di proteggere i dispositivi mentre sono nel campo hello fornendo una chiave di identità univoca per ogni dispositivo, che può essere utilizzata da hello IoT infrastruttura toocommunicate con dispositivo hello mentre è nell'operazione. il processo di Hello è rapido e semplice tooset backup. Hello chiave generato con una base di hello form ID dispositivo selezionate dall'utente di un token utilizzato in tutte le comunicazioni tra il dispositivo di hello e hello Azure IoT Hub.

L'ID dispositivo può essere associato a un dispositivo durante la produzione (ad esempio all'interno del trust module dell'hardware) o può usare un'identità fissa esistente come proxy (ad esempio i numeri di serie della CPU). Poiché non è semplice modificare queste informazioni di identificazione nel dispositivo hello, è importante toointroduce gli ID di periferica logica nel caso in cui le modifiche di hello sottostante dispositivo hardware ma rimane impostato su un dispositivo logico hello hello stesso. In alcuni casi, l'associazione hello di un'identità del dispositivo può verificarsi in fase di distribuzione dispositivo (ad esempio un ingegnere autenticato fisicamente configura un nuovo dispositivo durante la comunicazione con back-end soluzione hello). Hello [registro identità Azure IoT Hub](../iot-hub/iot-hub-devguide.md) fornisce l'archiviazione sicura di identità di dispositivi e le chiavi di sicurezza per una soluzione. È possono aggiungere singoli o gruppi di identità dispositivo tooan consente di elenco o un elenco di blocco, abilitare il controllo completo sul dispositivo l'accesso.

Criteri di controllo accesso IoT Hub Azure nel cloud hello consentono l'attivazione e disattivazione qualsiasi identità del dispositivo, che fornisce un modo toodisassociate un dispositivo da una distribuzione di IoT quando richiesto. Associazione e dissociazione dei dispositivi sono basate su ogni identità dispositivo.

Le funzionalità di sicurezza aggiuntive del dispositivo includono seguente hello:

* I dispositivi non accettano connessioni di rete non richieste. I dispositivi stabiliscono tutte le connessioni e le route in modalità solo in uscita. Per un dispositivo tooreceive un comando dal back-end hello, dispositivo hello deve avviare una connessione toocheck per qualsiasi tooprocess comandi in sospeso. Una volta stabilita una connessione tra il dispositivo hello e IoT Hub in modo sicuro, messaggistica di hello cloud toohello e dispositivi e dispositivo toohello cloud può essere inviato in modo trasparente.  
* I dispositivi si connettono solo tooor stabilire servizi noti toowell route con cui vengono peering, ad esempio un IoT Hub di Azure.
* L'autorizzazione e l'autenticazione a livello di sistema usano le identità di ogni dispositivo; le credenziali e le autorizzazioni di accesso devono essere revocabili quasi immediatamente.

### <a name="secure-connectivity"></a>Proteggere la connettività
La durata delle comunicazioni è una caratteristica importante per qualsiasi soluzione IoT. Hello necessario toodurably recapitare i comandi e/o ricevere i dati dai dispositivi è sottolineato fatto hello che i dispositivi IoT sono connessi tramite Internet hello o altre reti simili che possono essere inaffidabili. IoT Hub Azure offre durabilità dello scambio di messaggi tra cloud e dispositivi tramite un sistema di riconoscimenti in risposta toomessages. Durabilità aggiuntiva per la messaggistica avviene tramite messaggi di memorizzazione nella cache nella hello IoT Hub per backup tooseven giorni per i dati di telemetria e due giorni per i comandi.

L'efficienza è importante tooensure conservazione delle risorse e l'operazione in un ambiente con risorse limitate. HTTPS (HTTP sicuro), versione protetta di hello standard del settore del protocollo http comuni hello, è supportato da IoT Hub di Azure, consentendo la comunicazione efficiente. I servizi Advanced Message Queuing Protocol (AMQP) e Message Queuing Telemetry Transport (MQTT), supportati dall'hub IoT di Azure, sono progettati non solo per una maggiore efficienza in termini di uso delle risorse, ma anche per il recapito affidabile dei messaggi. 

Scalabilità richiede hello possibilità toosecurely interagire con un'ampia gamma di dispositivi. Hub IoT Azure consente ai dispositivi con IP abilitato e non abilitato per IP tooboth di connessione protetta. Dispositivi IP sono toodirectly in grado di connettersi e comunicare con hello IoT Hub tramite una connessione sicura. I dispositivi non abilitati per IP non dispongono di risorse limitate e si connettono solo tramite protocolli di comunicazione a distanza breve, ad esempio Zwave, ZigBee e Bluetooth. Un campo gateway tooaggregate utilizzati questi dispositivi ed esegue protocollo traduzione tooenable sicura la comunicazione bidirezionale con il cloud hello.

Funzionalità di sicurezza aggiuntivi per la connessione includere hello informazioni seguenti:

* Hello percorso di comunicazione tra i dispositivi e IoT Hub di Azure o tra i gateway e IoT Hub di Azure, è protetto tramite standard del settore sicurezza TLS (Transport Layer) con l'IoT Hub Azure autenticati utilizzando il protocollo di x. 509.
* Nei dispositivi di tooprotect ordine da connessioni indesiderate in ingresso, l'IoT Hub Azure aprire la periferica di toohello qualsiasi connessione. dispositivo Hello Avvia tutte le connessioni. 
* IoT Hub Azure durevole archivia i messaggi per i dispositivi e attende tooconnect dispositivo hello. Questi comandi vengono archiviati per due giorni, questi comandi per abilitare i dispositivi connessi in alcuni casi, a causa di problemi di connettività o toopower, tooreceive. L'hub IoT di Azure mantiene una coda specifica per dispositivo.

### <a name="secure-processing-and-storage-in-hello-cloud"></a>Proteggere l'elaborazione e archiviazione nel cloud hello
Dai dati di tooprocessing comunicazioni crittografate nel cloud hello, hello Azure IoT Suite consente di proteggere i dati. Fornisce una crittografia aggiuntiva tooimplement flessibilità e la gestione delle chiavi di sicurezza. Tramite Azure Active Directory (AAD) per l'autenticazione e autorizzazione, Azure IoT Suite possibile fornire un modello di autorizzazione basata su criteri per i dati nel cloud hello, abilitare la gestione di un accesso semplice che può essere controllata e verificati. Questo modello consente inoltre di revoche di certificati quasi immediata dei toodata access nel cloud hello e dei dispositivi connessi toohello Azure IoT Suite.

Dopo aver aggiunto dati cloud hello, può essere elaborato e archiviato in qualsiasi flusso di lavoro definiti dall'utente. Parte tooeach accesso hello dei dati viene controllato con Azure Active Directory, a seconda di hello il servizio di archiviazione utilizzato.

Tutte le chiavi utilizzate dall'infrastruttura di IoT hello vengono archiviate nel cloud hello in un archivio protetto, con hello possibilità tooroll nel caso in cui le chiavi devono toobe rieffettuare il provisioning. Dati possono essere archiviati [Azure Cosmos DB](../documentdb/documentdb-introduction.md) o in [database SQL](../sql-database/sql-database-faq.md), l'abilitazione di definizione del livello di hello di protezione desiderato. Inoltre, Azure fornisce un modo toomonitor e controllare tutte accesso tooyour dati tooalert intrusioni o accessi non autorizzati.

## <a name="conclusion"></a>Conclusioni
Hello Internet of Things inizia con un, gli elementi, ovvero hello operazioni che è rilevante la maggior parte delle toobusinesses. IoT può fornire incredibile business tooa di valore, riducendo i costi, incremento dei profitti e la trasformazione di business. Esito positivo della trasformazione dipende in larga misura scelta hello destra IoT software e il provider. Ciò significa che la ricerca di un provider non solo catalizza questa trasformazione per comprendere le esigenze e i requisiti dell'azienda, ma fornisce anche servizi e software realizzati tenendo conto di aspetti di importanza fondamentale quali sicurezza, privacy, trasparenza e conformità. Microsoft ha vasta esperienza con lo sviluppo e distribuzione di servizi e software sicura e continua toobe leader in questa nuova età di Internet delle cose. 

Microsoft Azure IoT Suite Hello si basa di misure di sicurezza per impostazione predefinita, l'abilitazione del monitoraggio sicura di efficienza tooimprove asset, promuovere l'innovazione tooenable prestazioni operative, e utilizzano avanzate analitica dati tootransform aziende. Con il relativo approccio a più livelli per sicurezza e funzionalità di sicurezza più modelli di progettazione, Azure IoT Suite consente di distribuire un'infrastruttura che può essere tootransform attendibile qualsiasi azienda. 

## <a name="additional-information"></a>Informazioni aggiuntive
Ogni soluzione preconfigurata Azure IoT Suite crea istanze di servizi di Azure, come illustrato di seguito hello:

* [**IoT Hub Azure**](https://azure.microsoft.com/services/iot-hub/): il gateway che si connette cloud hello troppo "elementi". È possibile ridimensionare toomillions di connessioni per ogni hub e processo di grandi volumi di dati con supporto dell'autenticazione per ogni dispositivo che contribuisce a proteggere la soluzione.
* [**Azure DB Cosmos**](https://azure.microsoft.com/services/documentdb/): un servizio di database scalabile e completamente indicizzato per dati semistrutturati che gestisce i metadati per i dispositivi hello viene effettuato il provisioning, ad esempio gli attributi, la configurazione e le proprietà di sicurezza. Cosmos DB offre l'elaborazione ad alte prestazioni e velocità effettiva elevata, indicizzazione dei dati senza schema e una ricca interfaccia di query SQL.
* [**Azure Analitica flusso**](https://azure.microsoft.com/services/stream-analytics/): flusso in tempo reale di elaborazione nel cloud hello che consente di toorapidly sviluppare e distribuire informazioni in tempo reale di basso costo analitica soluzione toouncover da dispositivi, sensori, l'infrastruttura e applicazioni. dati Hello da questo servizio completamente gestito possono essere ridimensionati volume tooany comunque una velocità effettiva elevata, bassa latenza e resilienza.
* [**Servizi App Azure**](https://azure.microsoft.com/services/app-service/): web potente toobuild piattaforma cloud e App per dispositivi mobili che si connettono toodata in qualsiasi punto; nel cloud hello o in locale. Creare app per dispositivi mobili coinvolgenti per iOS, Android e Windows. Integrazione con il Software come servizio (SaaS) ed enterprise nelle applicazioni con connettività di casella toodozens di servizi basati su cloud e applicazioni aziendali. Codice nell'IDE e linguaggio preferito: .NET, Node.js, PHP, Python o Java: toobuild App web e le API più rapidamente che mai.
* [**Logica app**](https://azure.microsoft.com/services/app-service/logic/): hello logica App funzionalità di servizio App di Azure consente di integrare i sistemi di line-of-business esistenti IoT soluzione tooyour e automatizzare i processi del flusso di lavoro. Logica App consente agli sviluppatori toodesign i flussi di lavoro che iniziano da un trigger e quindi eseguire una serie di passaggi, regole e le azioni che utilizzano i connettori potente toointegrate con i processi di business. La logica App offre vasto ecosistema tooa connettività della casella di SaaS, basati su cloud e applicazioni locali.
* [**Archiviazione blob di Azure**](https://azure.microsoft.com/services/storage/): archiviazione cloud affidabile ed economico per i dati di hello che i dispositivi inviano toohello cloud.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sulla protezione soluzione IoT, vedere:

* [Procedure consigliate per la sicurezza IoT][lnk-security-best-practices]
* [Architettura della sicurezza IoT][lnk-security-architecture]
* [Proteggere la distribuzione di IoT][lnk-security-deployment]

[lnk-security-best-practices]: iot-security-best-practices.md
[lnk-security-architecture]: iot-security-architecture.md
[lnk-security-deployment]: iot-suite-security-deployment.md

È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Domande frequenti su IoT Suite][lnk-faq]

È possibile leggere sulla sicurezza di IoT Hub in [tooIoT accesso controllo Hub] [ lnk-devguide-security] nella Guida per sviluppatori di IoT Hub hello.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
