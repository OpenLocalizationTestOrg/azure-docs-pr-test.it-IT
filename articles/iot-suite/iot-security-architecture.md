---
title: Architettura di sicurezza aaaIoT | Documenti Microsoft
description: Considerazioni e indicazioni sull'architettura di sicurezza IoT
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 18ed3eb0-9406-44e1-8a3a-93dc6726c7ac
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: yurid
ms.openlocfilehash: 5b59133f6b1b45573318c3bd5b621d27b147d71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-architecture"></a>Architettura di sicurezza di Internet delle cose
Quando si progetta un sistema, è importante toounderstand minacce potenziali di hello toothat sistema e add difese appropriate di conseguenza, sistema di hello è progettato e architettura. È particolarmente importante poiché la comprensione di come un utente malintenzionato potrebbe essere in grado di toocompromise un sistema consente di verificare che le misure di attenuazione appropriate siano soddisfatti dall'inizio di hello, toodesign hello prodotto dall'inizio hello con particolare attenzione alla sicurezza. 

## <a name="security-starts-with-a-threat-model"></a>La sicurezza inizia con un modello di rischio
Microsoft è lunga utilizzato modelli di rischio per i propri prodotti e ha reso disponibile pubblicamente di processo di modellazione delle minacce della società hello. Hello società esperienza dimostra che disponga di modellazione hello imprevisti vantaggi oltre hello immediata comprensione delle minacce sono hello la maggior parte delle relative. Ad esempio, crea inoltre un vettore per una discussione aperta con altri utenti all'esterno di team di sviluppo hello, che possono causare toonew idee e miglioramenti nel prodotto hello.

obiettivo di Hello di modellazione delle minacce è toounderstand come un utente malintenzionato potrebbe essere in grado di toocompromise un sistema e quindi verificare che le misure di attenuazione appropriate siano soddisfatti. La modellazione delle minacce impone le misure di attenuazione di hello progettazione team tooconsider come sistema di hello è progettato anziché dopo aver distribuito un sistema. Ciò è estremamente importante, perché non è applicabile, adattamento numerose tooa di difese per la sicurezza dei dispositivi nel campo hello soggetta a errori e lascia i clienti a rischio.

Molti team di sviluppo per eseguire un lavoro eccellente acquisizione hello funzionale dei requisiti di sistema hello che traggono vantaggio ai clienti. Tuttavia, l'identificazione modi meno evidenti che un utente potrebbe usare impropriamente sistema hello è più complessa. La modellazione delle minacce può aiutare i team di sviluppo a comprendere cosa potrebbe fare un utente malintenzionato e perché. La modellazione delle minacce è un processo strutturato che crea una discussione sulla sicurezza hello decisioni di progettazione nel sistema di hello, nonché progettazione toohello le modifiche apportate in modo hello influire sulla sicurezza. Mentre un modello di minaccia è semplicemente un documento, questa documentazione rappresenta anche una soluzione ideale continuità tooensure della Knowledge Base, conservazione delle lezioni apprese e consentono di caricare il nuovo team rapidamente. Infine, un risultato di una modellazione delle minacce è tooenable si tooconsider altri aspetti di sicurezza, ad esempio quali impegni di sicurezza, si vuole tooprovide tooyour clienti. Queste operazioni, in combinazione con la modellazione delle minacce, condurranno all'esecuzione di un test informato della soluzione Internet delle cose (IoT).

### <a name="when-toothreat-model"></a>Quando il modello toothreat
[La modellazione delle minacce](http://www.microsoft.com/security/sdl/adopt/threatmodeling.aspx) offerte hello valore più grande se è incorporato nella fase di progettazione hello. Quando si progetta, occorre hello maggiore flessibilità toomake modifiche tooeliminate minacce. Eliminando minacce per impostazione predefinita è il risultato desiderato hello. È molto più semplice rispetto all'aggiunta e al test di misure preventive, oltre che al garantire che rimangano correnti; per di più, tale eliminazione non è sempre possibile. Diventa più difficile tooeliminate minacce come un prodotto diventa più maturo e a sua volta infine richiederà più lavoro e gli svantaggi spiegati molto più difficili di modellazione nella fase iniziale di sviluppo hello.

### <a name="what-toothreat-model"></a>Il modello toothreat
È consigliabile thread soluzione hello del modello come un intero e anche lo stato attivo in hello seguenti aree:

* funzionalità di sicurezza e privacy Hello
* funzionalità di Hello i cui errori sono pertinenti alla sicurezza
* funzionalità di Hello che riguardano un limite di trust 

### <a name="who-threat-models"></a>Chi implementa la modellazione delle minacce
La modellazione delle minacce è un processo come qualsiasi altro.  Si tratta di un documento di modello buona tootreat hello minaccia come qualsiasi altro componente della soluzione hello e convalidarlo. Molti team di sviluppo per eseguire un lavoro eccellente acquisizione hello funzionale dei requisiti di sistema hello che traggono vantaggio ai clienti. Tuttavia, l'identificazione modi meno evidenti che un utente potrebbe usare impropriamente sistema hello è più complessa. La modellazione delle minacce può aiutare i team di sviluppo a comprendere cosa potrebbe fare un utente malintenzionato e perché.

### <a name="how-toothreat-model"></a>Come modello toothreat
processo di modellazione energia Hello è composto da quattro passaggi. Hello passaggi:

* Applicazione hello modello
* Enumerazione delle minacce
* Attenuazione delle minacce
* Convalidare le misure di attenuazione hello

#### <a name="hello-process-steps"></a>passaggi del processo Hello
Tre regole tookeep presente quando si compila un modello di rischio:

1. Creare un diagramma basato sull'architettura di riferimento. 
2. Iniziare con la ricerca in ampiezza. Ottenere una panoramica e comprendere sistema hello nel suo complesso, prima di illustrare completo.  Questo contribuisce a garantire che si approfondita in hello destra effettua.
3. Unità processo hello, non lasciare che il processo di hello è l'unità. Se si riscontra un problema in fase di modellazione hello e si desidera tooexplore passare per tale!  Non è necessario slavishly toofollow questi passaggi.  

#### <a name="threats"></a>Minacce
Hello quattro elementi di base di un modello di rischio sono:

* Processi (servizi web, servizi di Win32, * nix daemon e così via). Si noti che alcune entità complesse (ad esempio, i sensori e i gateway sul campo) possono essere astratte come processo quando non è possibile eseguire un drill-down tecnico in queste aree.
* Archivi di dati (qualsiasi punto in cui sono memorizzati dati, ad esempio un file di configurazione o un database)
* Flusso di dati (in cui i dati vengono inviati altri elementi in un'applicazione hello)
* Le entità esterne (tutto ciò che interagisce con il sistema di hello, ma non è nel controllo del codice dell'applicazione hello hello, ad esempio utenti e satellite feed)

Tutti gli elementi nel diagramma dell'architettura hello sono minacce toovarious soggetto; tasto di scelta STRIDE hello verrà utilizzato. Lettura [minaccia modellazione nuovamente, STRIDE](https://blogs.msdn.microsoft.com/larryosterman/2007/09/04/threat-modeling-again-stride/) tooknow ulteriori informazioni sugli elementi STRIDE hello.

Diversi elementi del diagramma applicazioni hello sono minacce STRIDE toocertain di interesse:

* I processi sono soggetto tooSTRIDE
* Flussi di dati sono soggetto tooTID
* Archivi dati sono soggetto tooTID e, talvolta, R, se gli archivi dati hello sono file di log.
* Le entità esterne vengono tooSRD soggetto

## <a name="security-in-iot"></a>Sicurezza in IoT
I dispositivi connessi speciale hanno un numero significativo di potenziali aree di superficie di attacco di interazione e modelli di interazione, ognuno dei quali deve essere considerato tooprovide un framework per la protezione dell'accesso digitale toothose dispositivi. il termine di Hello "accesso digitale" è toodistinguish qui utilizzato da tutte le operazioni vengono eseguite tramite l'interazione diretta di dispositivi di sicurezza dall'accesso in cui avviene tramite il controllo di accesso fisico. Inserire, ad esempio, dispositivo hello in una chat con un blocco sulla porta hello. Durante l'accesso fisico non può essere negato tramite software e hardware, può misure tooprevent accesso fisico dei principali toosystem interferenze. 

Esplorare i modelli di interazione hello, verranno esaminati "controllo dispositivo" e "dati del dispositivo" con hello dello stesso livello di attenzione. "Controllo dispositivo" può essere classificata come le informazioni fornite tooa dispositivo da qualsiasi parte con obiettivo hello di modifica o che influenzano il comportamento verso lo stato o stato hello del proprio ambiente. "Dati del dispositivo" possono essere classificati come qualsiasi informazione che un dispositivo crea tooany controparte sullo stato e hello osservata lo stato del proprio ambiente.

In ordine toooptimize procedure ottimali di protezione, è consigliabile che un'architettura tipica di IoT essere suddivisi in diverse aree di componente o come parte della modellazione hello esercizio. Queste zone sono descritte dettagliatamente in questa sezione e includono:

* Dispositivo
* Gateway sul campo
* Gateway cloud
* Servizi

Le zone sono ampie toosegment modo una soluzione. ciascuna area sono spesso presenti requisiti dati, autenticazione e autorizzazione. Le zone possono anche essere utilizzati tooisolation danni e limitare l'impatto di hello delle aree di attendibilità bassa nelle aree di attendibilità superiore.

Ciascuna zona è separato da un confine di Trust, cui viene indicato come hello con linea rossa nel seguente diagramma hello punti. Rappresenta una transizione di informativo o di dati da un'origine tooanother. Durante questa transizione, informativo o hello dati potrebbe essere soggetto tooSpoofing, manomissione, ripudio, diffusione di informazioni, Denial of Service e l'elevazione dei privilegi (STRIDE).

![Aree di sicurezza IoT](media/iot-security-architecture/iot-security-architecture-fig1.png) 

Hello rappresentati all'interno di ogni limite sono anche componenti sottoposti tooSTRIDE, l'abilitazione di un completo 360 vista della soluzione hello di modellazione. Hello nelle sezioni seguenti vengono elaborano in ognuno dei componenti di hello e problemi di sicurezza specifici e le soluzioni che devono essere inserite sul posto.

Nelle sezioni successive Hello parlerà componenti standard, in genere presenti in queste aree.

### <a name="hello-device-zone"></a>Hello fuso del dispositivo
ambiente del dispositivo Hello è spazio fisico immediato hello intorno dispositivo hello in cui l'accesso fisico e/o firma digitale peer-to-peer "rete" accesso toohello dispositivo è fattibile. Una rete"locale" equivale a toobe una rete distinti e isolati; ma potenzialmente collegati tramite bridge di rete Internet pubblica troppo: hello, che include qualsiasi tecnologia onde radio wireless che consente la comunicazione peer-to-peer di dispositivi. Caso *non* includono qualsiasi tecnologia di virtualizzazione di rete creare illusione hello della rete locale e inoltre non include reti operatore pubblico che richiedono qualsiasi toocommunicate due dispositivi di spazio di rete pubblica Se si trattasse di relazione di comunicazione tooenter un peer-to-peer.

### <a name="hello-field-gateway-zone"></a>Hello zona Gateway campo
Un gateway sul campo è un dispositivo o un software per server di uso generico che agisce come componente che abilita la comunicazione e, potenzialmente, come sistema di controllo dei dispositivi e hub di elaborazione dei dati dei dispositivi. Nell'area campi gateway Hello include hello campo gateway e tutti i dispositivi che sono collegati tooit. Come suggerisce il nome di hello, gateway campo agiscono strutture esterno dedicato l'elaborazione dei dati, sono in genere percorso associato, è potenzialmente intrusione toophysical soggetto e sarà limitata ridondanza operativa. Tutti toosay che generalmente è un gateway campo una cosa uno possa toccare e il sabotaggio sapendo che cos'è la funzione. 

Un gateway sul campo è diverso da un semplice router di traffico, perché ha avuto un ruolo attivo nella gestione dell'accesso e del flusso di informazioni. In altre parole, è un'entità orientata alle applicazioni e un terminale di sessione o di connessione di rete. I dispositivi o i firewall NAT, al contrario, non sono idonei come gateway sul campo perché non sono terminali di sessione o di connessione espliciti, ma piuttosto inoltrano (o bloccano) le connessioni o le sessioni che li attraversano. gateway campo Hello ha due aree distinte di superficie di attacco. Uno è rivolto dispositivi hello tooit collegato e rappresenta hello all'interno di zona hello e hello altri deve affrontare tutte le entità esterne e hello bordo della zona hello.   

### <a name="hello-cloud-gateway-zone"></a>zona di gateway di Hello cloud
Gateway del cloud è un sistema che consente la comunicazione remota di e gateway toodevices o un campo da più siti diversi in spazio di rete pubblica, in genere verso un basato su cloud controllo e dati sistema di analisi, una federazione di tali sistemi. In alcuni casi, un gateway del cloud può agevolare immediatamente accedere ai dispositivi toospecial scopo dai terminali, ad esempio Tablet o telefoni. Nel contesto di hello descritto in questo caso, "cloud" è stato progettato sistema di elaborazione dati toorefer tooa dedicato che non è associato toohello stesso sito come hello collegato dispositivi o ai gateway di campo. Anche in una zona, Cloud operational misure impediscono l'accesso fisico di destinazione e non sono necessariamente esposto tooa dell'infrastruttura di "cloud pubblico".  

Un gateway del cloud potrebbe potenzialmente essere mappate in un sovrapposizione tooinsulate hello cloud gateway di virtualizzazione rete e tutti i relativi dispositivi collegati o qualsiasi altro traffico di rete per gateway campo. gateway del cloud Hello stesso è un sistema di controllo dispositivo né un elaborazione né la funzionalità di archiviazione per i dati di dispositivo. tali funzionalità dell'interfaccia con gateway del cloud hello. zona di gateway di Hello cloud include hello gateway del cloud stesso insieme a tutti i gateway di campo e i dispositivi direttamente o indirettamente collegato tooit. bordo Hello della zona hello è una superficie distinta in cui tutte le entità esterne comunicano tramite.

### <a name="hello-services-zone"></a>zona servizi Hello
Un "servizio" è definito per questo contesto come qualsiasi componente software o modulo che si interfaccia con i dispositivi attraverso un gateway sul campo o cloud per la raccolta e l'analisi dei dati, nonché per il controllo e il comando.  I servizi sono mediatori, Agire con la propria identità verso i gateway e gli altri sottosistemi, archiviare e analizzare i dati, autonomo toodevices comandi problema in base alle pianificazioni o comprensione dei dati e di esporre informazioni e gli utenti finali di tooauthorized funzionalità di controllo.

### <a name="information-devices-vs-special-purpose-devices"></a>Confronto tra dispositivi informativi e dispositivi per scopi specifici
PC, telefoni e tablet sono principalmente dispositivi informativi interattivi. Telefoni e tablet sono ottimizzati in modo esplicito per massimizzare la durata della batteria, Essi preferibilmente disattivare parzialmente quando non è immediatamente l'interazione con una persona o quando non fornisce servizi come musica o guidando proprietari tooa determinata posizione. Dal punto di vista sistemico, questi dispositivi IT fungono principalmente da delegato verso le persone: sono "attuatori di persone" che suggeriscono azioni e "sensori di persone" che raccolgono input. 

Dispositivi speciale, dalle semplici temperatura sensori toocomplex factory produzione righe con migliaia di componenti all'interno di esse, sono diversi. Questi dispositivi sono molto più di un ambito nello scopo e anche se si fornisce un tipo di interfaccia utente, sono in gran parte con ambito toointerfacing con o essere integrati nell'asset in HelloWorld fisico. Tali strumenti misurano e segnalano condizioni ambientali, girano valvole, controllano servomotori, fanno suonare allarmi, accendono luci ed eseguono molti altri compiti. Consentono di toodo di lavoro per cui un dispositivo di informazioni è troppo generici, troppo costoso, troppo grande o troppo fragile. scopo concreta Hello immediatamente determina le tecniche di progettazione come hello e valuta il budget disponibile per la produzione e l'operazione di durata pianificata. combinazione di Hello di questi due fattori chiavi vincola hello disponibile operational budget energia footprint fisico e pertanto spazio di archiviazione disponibile, calcolo e funzionalità di sicurezza.  

Se un elemento "si errato" dispositivi controllabile automatica o remota, ad esempio, difetti fisici o toowillful difetti della logica di controllo non autorizzato delle intrusioni e la modifica. possibile che venga eliminato un numero elevato di produzione Hello edifici può anche essere looted o masterizzati verso il basso e utenti potrebbero essere danneggiata o persino della matrice. Si tratta, ovviamente, di una classe di danno del tutto differente dal superamento del limite di spesa con una carta di credito trafugata. spostare Hello barra di sicurezza per i dispositivi che semplificare e anche per i dati del sensore che infine risultati in quelli che generano operazioni toomove, deve essere maggiore di e-commerce o uno scenario di servizi bancari. 

### <a name="device-control-and-device-data-interactions"></a>Interazioni tra controllo del dispositivo e dati del dispositivo
I dispositivi connessi speciale hanno un numero significativo di potenziali aree di superficie di attacco di interazione e modelli di interazione, ognuno dei quali deve essere considerato tooprovide un framework per la protezione dell'accesso digitale toothose dispositivi. il termine di Hello "accesso digitale" è toodistinguish qui utilizzato da tutte le operazioni vengono eseguite tramite l'interazione diretta di dispositivi di sicurezza dall'accesso in cui avviene tramite il controllo di accesso fisico. Inserire, ad esempio, dispositivo hello in una chat con un blocco sulla porta hello. Durante l'accesso fisico non può essere negato tramite software e hardware, può misure tooprevent accesso fisico dei principali toosystem interferenze. 

Esplorare i modelli di interazione hello, verranno esaminati "controllo dispositivo" e "dati del dispositivo" con hello dello stesso livello di attenzione durante la modellazione delle minacce. "Controllo dispositivo" può essere classificata come le informazioni fornite tooa dispositivo da qualsiasi parte con obiettivo hello di modifica o che influenzano il comportamento verso lo stato o stato hello del proprio ambiente. "Dati del dispositivo" possono essere classificati come qualsiasi informazione che un dispositivo crea tooany controparte sullo stato e hello osservata lo stato del proprio ambiente. 

## <a name="threat-modeling-hello-azure-iot-reference-architecture"></a>Architettura di riferimento di hello Azure IoT di modellazione
Microsoft utilizza framework hello descritte in precedenza toodo di modellazione per Azure IoT. Nella seguente sezione hello è pertanto necessario utilizzare hello esempio concreto di architettura di riferimento di Azure IoT toodemonstrate come toothink sulla modellazione per IoT e come tooaddress hello minacce identificate. In questo caso, sono state identificate quattro aree principali di interesse:

* Dispositivi e origini dati
* Trasporto dei dati
* Elaborazione di dispositivi ed eventi
* Presentazione

![Modellazione delle minacce per Azure IoT](media/iot-security-architecture/iot-security-architecture-fig2.png) 

diagramma di Hello seguente fornisce una visuale semplificata di IoT architettura Microsoft tramite un modello di diagramma di flusso di dati che viene utilizzato lo strumento Microsoft Threat modellazione hello:

![Modellazione delle minacce per Azure IoT con l'apposito strumento Microsoft](media/iot-security-architecture/iot-security-architecture-fig3.png)

È importante toonote che hello architettura separa le funzionalità di dispositivo e gateway hello. In questo modo hello utente tooleverage dispositivi gateway che sono più sicuri: sono in grado di comunicare con gateway del cloud hello con protocolli sicuri, che in genere richiede maggiore overhead di elaborazione che un dispositivo nativo, ad esempio un termostato - Impossibile fornire il proprio. Nell'area di servizi di Azure hello, si presuppone che hello che gateway del Cloud è rappresentato da hello servizio IoT Hub di Azure.

### <a name="device-and-data-sourcesdata-transport"></a>Dispositivo e origini dati/trasporto dei dati
In questa sezione Esplora architettura hello descritta in precedenza tramite obiettivo hello della modellazione delle minacce e viene fornita una panoramica di come parlerà alcuni dei problemi inerenti hello. Si concentra sugli elementi di base hello di un modello di rischio:

* Processi (quelli sotto il controllo degli utenti e gli elementi esterni)
* Comunicazione (o flusso di dati)
* Archiviazione (o archivi di dati)

#### <a name="processes"></a>Processi
In ciascuna delle categorie di hello descritte nell'architettura di Azure IoT hello, si tenta presente in un numero di minacce diversi tra i dati nelle diverse fasi di hello/informazioni toomitigate: processo, la comunicazione e archiviazione. Di seguito viene fornita una panoramica di hello quelle più comuni per categoria "processo" hello, seguito da una panoramica di come questi può essere contrastati migliore: 

**Lo spoofing degli indirizzi (S)**: un utente malintenzionato può estrarre materiale della chiave di crittografia da un dispositivo, a livello di software o hardware hello e successivamente l'accesso ai sistema hello con un altro dispositivo fisico o virtuale con identità hello di hello dispositivo hello materiale della chiave è stato usato da. Un buon esempio sono i telecomandi che possono accendere qualsiasi televisore e sono popolari strumenti per burloni.

**Denial of Service (D)**: un dispositivo potrebbe essere messo fuori uso o reso incapace di comunicare tramite interferenza con le frequenze radio o taglio dei cavi. Ad esempio, una videocamera di sorveglianza a cui sia stata intenzionalmente interrotta l'alimentazione o la connessione di rete non segnalerà alcun dato.

**Manomissione (T)**: un utente malintenzionato può sostituire parzialmente o totalmente software hello in esecuzione sul dispositivo hello, consentendo potenzialmente hello sostituito software tooleverage hello autenticità dell'identità del dispositivo hello se hello materiale della chiave o hello crittografia strutture che contiene materiale chiave sono stati programma evitato toohello disponibili. Ad esempio, un utente malintenzionato potrebbe sfruttare estratti toointercept materiale chiave Elimina i dati dal dispositivo hello nel percorso di comunicazione hello e sostituirlo con i dati false viene autenticati con il materiale della chiave hello rubato.

**La diffusione di informazioni (I)**: se il dispositivo hello è in esecuzione software modificato, tale software modificato può causare una perdita parti toounauthorized dati. Ad esempio, un utente malintenzionato potrebbe sfruttare estratti chiave materiale tooinject stesso nel percorso di comunicazione hello tra il dispositivo di hello e un gateway controller o un campo o nel cloud toosiphon gateway informazioni.

**Elevazione dei privilegi (E)**: un dispositivo che esegue una funzione specifica può essere forzato toodo con un altro. Ad esempio, una valvola che tooopen programmati metà modo può essere indotto tooopen tutti hello modo.

| **Componente** | **Minaccia** | **Attenuazione** | **Rischio** | **Implementazione** |
| --- | --- | --- | --- | --- |
| Dispositivo |S |Assegnazione di identità toohello dispositivo e l'autenticazione dispositivo hello |Sostituzione di dispositivo o parte del dispositivo hello con un altro dispositivo. Come è possibile sapere che quanto dispositivo corretto toohello? |L'autenticazione dispositivo hello, usando Transport Layer Security (TLS) o IPSec. L'infrastruttura deve supportare l'uso di una chiave precondivisa (PSK) nei dispositivi che non riescono a gestire la crittografia asimmetrica completa. Usare Azure AD, [OAuth](http://www.rfc-editor.org/in-notes/internet-drafts/draft-ietf-ace-oauth-authz-01.txt) |
| TRID |Applicare dispositivo toohello meccanismi di chiusura, ad esempio rendendo molto difficile tooimpossible tooextract chiavi e altro materiale di crittografia dal dispositivo hello. |il rischio di Hello è se un utente è la manomissione dispositivo hello (interferenze fisiche). Come è possibile accertarsi che il dispositivo non sia stato manomesso. |attenuazione più efficace Hello è una funzionalità di trusted platform module (TPM) che consente l'archiviazione delle chiavi in un circuito del chip speciale da quale hello non è possibile leggere le chiavi, ma possono essere utilizzate solo per le operazioni di crittografia che usano la chiave hello ma mai divulgare chiave hello . Crittografia di memoria del dispositivo hello. Gestione delle chiavi per il dispositivo hello. Firma del codice hello. | |
| E |Se il controllo di accesso del dispositivo hello. Schema di autorizzazione. |Se il dispositivo di hello consente per singole operazioni toobe eseguita in base ai comandi da un'origine esterna, o anche compromesso sensori, sarà possibile attacco hello tooperform operazioni non è accessibile in caso contrario. |Con lo schema di autorizzazione per il dispositivo hello | |
| Gateway sul campo |S |L'autenticazione hello campo gateway tooCloud Gateway (basata sul certificato, PSK, attestazione basata,...) |Se qualcuno riesce a effettuare lo spoofing del gateway sul campo, questo potrà presentarsi come qualsiasi dispositivo. |TLS RSA/PSK, IPSec, [RFC 4279](https://tools.ietf.org/html/rfc4279). Tutti hello stessa risorsa di archiviazione chiave e i problemi di un'attestazione di dispositivi in generale: migliore dei casi è utilizzare TPM. Estensione 6LowPAN IPSec toosupport Wireless sensore reti (WSN). |
| TRID |Evitare la manomissione di (TPM?) hello Gateway campo |Lo spoofing degli attacchi di ingannare gateway del cloud hello pensiero che stia comunicando toofield gateway potrebbe causare la divulgazione di informazioni e la manomissione dei dati |Crittografia della memoria, TPM, autenticazione. | |
| E |Meccanismo di controllo di accesso per il gateway sul campo | | | |

Ecco alcuni esempi di minacce in questa categoria:

Lo spoofing degli indirizzi: Un utente malintenzionato può estrarre materiale della chiave di crittografia da un dispositivo, sia a livello di software o hardware hello e, successivamente, l'accesso è stato sistema hello con un altro dispositivo fisico o virtuale con identità hello hello dispositivo hello materiale della chiave prelevati.

**Denial of Service**: un dispositivo potrebbe essere messo fuori uso o reso incapace di comunicare tramite interferenza con le frequenze radio o taglio dei cavi. Ad esempio, una videocamera di sorveglianza a cui sia stata intenzionalmente interrotta l'alimentazione o la connessione di rete non segnalerà alcun dato.

**Manomissione**: un utente malintenzionato può sostituire parzialmente o totalmente software hello in esecuzione sul dispositivo hello, consentendo potenzialmente hello sostituito software tooleverage hello autenticità dell'identità del dispositivo hello se hello materiale della chiave o hello crittografia strutture che contiene materiale chiave sono stati programma evitato toohello disponibili.

**Manomissione**: una telecamera di sorveglianza che mostra l'immagine dello spettro visibile di un corridoio vuoto potrebbe essere puntata su una foto dello stesso corridoio. Un sensore di fumo o antincendio potrebbe segnalare una persona che tiene un accendino acceso al di sotto dello stesso. In entrambi i casi, hello dispositivo potrebbe non essere tecnicamente completamente attendibile verso il sistema di hello, ma segnala informazioni modificate.

**Manomissione**: un utente malintenzionato potrebbe sfruttare estratti toointercept materiale chiave ed elimina i dati dal dispositivo hello nel percorso di comunicazione hello e sostituirlo con i dati false viene autenticati con il materiale della chiave hello rubato.

**Manomissione**: un utente malintenzionato può sostituire completamente o parzialmente software hello in esecuzione sul dispositivo hello, consentendo potenzialmente hello sostituito software tooleverage hello autenticità dell'identità del dispositivo hello se hello materiale della chiave o hello crittografia strutture che contiene materiale chiave sono stati programma evitato toohello disponibili.

**La diffusione di informazioni**: se il dispositivo hello è in esecuzione software modificato, tale software modificato può causare una perdita parti toounauthorized dati.

**La diffusione di informazioni**: un utente malintenzionato potrebbe sfruttare estratti chiave materiale tooinject stesso nel percorso di comunicazione hello tra il dispositivo di hello e un gateway controller o un campo o gateway toosiphon informazioni cloud.

**Attacco Denial of Service**: dispositivo hello può essere disattivato o attivato in una modalità in cui non è possibile (ovvero intenzionale in molte macchine industriali) comunicazione.

**Manomissione**: dispositivo hello può essere riconfigurato toooperate in uno stato sconosciuto toohello controllare system (all'esterno di parametri di calibrazione noti) e quindi fornire i dati che possono essere erroneamente interpretati

**L'elevazione dei privilegi**: un dispositivo che esegue una funzione specifica può essere forzato toodo con un altro. Ad esempio, una valvola che tooopen programmati metà modo può essere indotto tooopen tutti hello modo.

**Attacco Denial of Service**: dispositivo hello può essere convertito in uno stato in cui non è possibile la comunicazione.

**Manomissione**: dispositivo hello può essere riconfigurato toooperate in uno stato sconosciuto toohello controllare system (all'esterno di parametri di calibrazione noti) e quindi fornire i dati che possono essere erroneamente interpretati.

**Lo spoofing, Tampering/ripudio**: se non è protetto (ovvero raramente case hello con controlli remoti consumer) un utente malintenzionato è possibile modificare lo stato di hello di un dispositivo in modo anonimo. Un buon esempio sono i telecomandi che possono accendere qualsiasi televisore e sono popolari strumenti per burloni.

#### <a name="communication"></a>Comunicazione
Minacce presenti nel percorso di comunicazione tra dispositivi, dispositivi e gateway sul campo e dispositivo e gateway cloud. Hello nella tabella riportata di seguito è alcune indicazioni intorno socket aperti hello dispositivo/VPN:

| **Componente** | **Minaccia** | **Attenuazione** | **Rischio** | **Implementazione** |
| --- | --- | --- | --- | --- |
| Dispositivo - Hub IoT |TID |(D) Traffico di hello tooencrypt TLS (PSK/RSA) |Intercettazione o interferire la comunicazione tra il dispositivo di hello e gateway hello hello |Sicurezza a livello di protocollo hello. Con un protocolli personalizzati, è necessario toofigure come tooprotect li. Nella maggior parte dei casi, la comunicazione hello avviene da hello dispositivo toohello IoT Hub (dispositivo avvia connessione hello). |
| Dispositivo - dispositivo |TID |(D) Traffico di hello tooencrypt TLS (PSK/RSA). |Lettura dei dati in transito tra i dispositivi. Manomissione dei dati di hello. L'overload dispositivo hello con le nuove connessioni |Sicurezza a livello di protocollo hello (MQTT/AMQP o HTTP/CoAP. Con un protocolli personalizzati, è necessario toofigure come tooprotect li. ridurlo Hello hello minacce DoS toopeer dispositivi tramite un gateway cloud o un campo e che li hanno act solo come client verso la rete hello. Hello peering può comportare una connessione diretta tra peer hello dopo avere stato negoziata dal gateway hello |
| Entità esterna - dispositivo |TID |L'associazione complessa del dispositivo di toohello hello entità esterne |Dispositivo di intercettazione hello connessione toohello. Comunicazione hello interferenza con dispositivo hello |Associazione in modo sicuro dispositivo toohello di entità esterne hello LE NFC/Bluetooth. Controllo del pannello operativo di hello del dispositivo hello (fisica) |
| Gateway sul campo - Gateway cloud |TID |Traffico di hello tooencrypt TLS (PSK/RSA). |Intercettazione o interferire la comunicazione tra il dispositivo di hello e gateway hello hello |Sicurezza a livello di protocollo hello (MQTT/AMQP o HTTP/CoAP). Con un protocolli personalizzati, è necessario toofigure come tooprotect li. |
| Dispositivo - Gateway cloud |TID |Traffico di hello tooencrypt TLS (PSK/RSA). |Intercettazione o interferire la comunicazione tra il dispositivo di hello e gateway hello hello |Sicurezza a livello di protocollo hello (MQTT/AMQP o HTTP/CoAP). Con un protocolli personalizzati, è necessario toofigure come tooprotect li. |

Ecco alcuni esempi di minacce in questa categoria:

**Attacco Denial of Service**: vincolati dispositivi sono in genere in pericolo DoS quando sono attivamente in ascolto per le connessioni in ingresso o indesiderati datagrammi in una rete, poiché un utente malintenzionato può aprire un numero di connessioni in parallelo e non li del servizio o del servizio li molto lenta o hello dispositivo può essere di traffico. In entrambi i casi, il dispositivo hello può in modo efficace inutilizzabile nel rete hello.

**Lo spoofing, divulgazione**: i dispositivi vincolati e speciale hanno spesso le funzionalità di sicurezza one-per-all come password o protezione di PIN o dipendono interamente trusting rete hello, vale a dire che consente l'accesso tooinformation quando un dispositivo si trova su hello stessa rete e tale rete spesso solo è protetto da una chiave condivisa. Ciò significa che quando hello shared secret toodevice o divulgata rete, è possibile toocontrol hello dispositivo o osservare i dati inviati dal dispositivo hello.  

**Lo spoofing degli indirizzi**: un utente malintenzionato può intercettare o parzialmente override hello broadcast e truffa hello iniziatore (man centro hello)

**Manomissione**: un utente malintenzionato può intercettare o parzialmente l'override di trasmissione hello e inviare informazioni false 

**Diffusione di informazioni:** un utente malintenzionato può intercettare in una trasmissione e ottenere informazioni senza autorizzazione **Denial of Service:** un utente malintenzionato potrebbe inserire hello segnale e Nega la distribuzione di informazioni

#### <a name="storage"></a>Archiviazione
Ogni gateway dispositivo e il campo contiene un tipo di archiviazione (temporaneo per i dati di Accodamento messaggi hello, archiviazione di immagini del sistema operativo (sistema operativo)).

| **Componente** | **Minaccia** | **Attenuazione** | **Rischio** | **Implementazione** |
| --- | --- | --- | --- | --- |
| Archiviazione nel dispositivo |TRID |Crittografia di archiviazione, la firma hello log |Lettura dei dati dall'archiviazione hello (dati PII), manomissione dei dati di telemetria. Manomissione dei dati di controllo del comando in coda o memorizzati nella cache. Manomissione di pacchetti di aggiornamento del firmware o di configurazione mentre memorizzato nella cache o in coda in locale può causare componenti tooOS e/o di sistema venga compromessi |Crittografia, codice di autenticazione messaggi (MAC) o firma digitale. Laddove possibile, un controllo di accesso complesso attraverso elenchi di controllo di accesso (ACL) o autorizzazioni. |
| Immagine del sistema operativo del dispositivo |TRID | |Manomissione del sistema operativo / sostituzione dei componenti di hello del sistema operativo |Partizione del sistema operativo di sola lettura, immagine del sistema operativo firmata, crittografia |
| Archiviazione Gateway campo (Accodamento messaggi hello dati) |TRID |Crittografia di archiviazione, la firma hello log |Lettura dei dati dall'archiviazione hello (dati PII), manomissione dei dati di telemetria, manomissione accodata o memorizzati nella cache i dati di controllo del comando. Manomissione di pacchetti di aggiornamento del firmware o di configurazione (destinati a dispositivi o gateway campo) mentre memorizzato nella cache o in coda in locale può causare componenti tooOS e/o di sistema venga compromessi |BitLocker |
| Immagine del sistema operativo Gateway sul campo |TRID | |Manomissione del sistema operativo / sostituzione dei componenti di hello del sistema operativo |Partizione del sistema operativo di sola lettura, immagine del sistema operativo firmata, crittografia |

### <a name="device-and-event-processingcloud-gateway-zone"></a>Elaborazione di dispositivi ed eventi/zona gateway cloud
Un gateway del cloud è di sistema che consente la comunicazione remota di e gateway toodevices o un campo da più siti diversi in spazio di rete pubblica, in genere verso un basato su cloud controllo e dati sistema di analisi, una federazione di tali sistemi. In alcuni casi, un gateway del cloud può agevolare immediatamente accedere ai dispositivi toospecial scopo dai terminali, ad esempio Tablet o telefoni. Nel contesto di hello descritto in questo caso, "cloud" si intende sistema di elaborazione dati toorefer tooa dedicato che non è associato toohello come hello collegato dispositivi o ai gateway di campo e impediscono misurazioni operative accesso fisico di destinazione ma non è dello stesso sito necessariamente infrastruttura tooa "cloud pubblico".  Un gateway del cloud potrebbe potenzialmente essere mappate in un sovrapposizione tooinsulate hello cloud gateway di virtualizzazione rete e tutti i relativi dispositivi collegati o qualsiasi altro traffico di rete per gateway campo. gateway del cloud Hello stesso è un sistema di controllo dispositivo né un elaborazione né la funzionalità di archiviazione per i dati di dispositivo. tali funzionalità dell'interfaccia con gateway del cloud hello. zona di gateway di Hello cloud include hello gateway del cloud stesso insieme a tutti i gateway di campo e i dispositivi direttamente o indirettamente collegato tooit.

Gateway del cloud è principalmente personalizzati compilati componente software in esecuzione come servizio gateway di campo toowhich gli endpoint esposti e dispositivi di connettersi. Di conseguenza deve essere progettato tenendo presente la sicurezza. Seguire il processo [SDL](http://www.microsoft.com/sdl) per la progettazione e la creazione di questo servizio. 

#### <a name="services-zone"></a>Zona Servizi
Un sistema di controllo (o controller) è una soluzione software che si interfaccia con un dispositivo, una gateway campo oppure a scopo di hello di controllo di uno o più dispositivi e/o toocollect e/o archivio gateway del cloud e/o analizza i dati del dispositivo per la presentazione, o a scopo di controllo successivi. Sistemi di controllo sono solo le entità hello nell'ambito di hello di questa discussione che potrebbe immediatamente facilitano l'interazione con altri utenti. eccezione Hello è intermedie superfici controllo fisiche su dispositivi, ad esempio un'opzione che consente a un utente dispositivo hello tooturn off o modificare altre proprietà e per cui è disponibile un equivalente funzionale che è possibile accedere con firma digitale. 

Superfici controllo fisiche intermedie sono quelle in cui una sorta di che regolano la logica vincola la funzione hello dell'area di controllo fisico hello in modo che una funzione equivalente può essere avviata in modalità remota o di input è in conflitto con input remoto può essere evitato: questo tipo transitano superfici di controllo sono il sistema di controllo locale tooa concettualmente collegati che si basa su hello sottostante funzionerà come qualsiasi altro sistema di controllo remoto che hello dispositivo può essere collegato tooin parallelo. Cloud toohello pericoli calcolo può essere letta in [Alliance protezione Cloud (CSA)](https://cloudsecurityalliance.org/research/top-threats/) pagina.

## <a name="additional-resources"></a>Risorse aggiuntive
Fare riferimento toohello seguenti articoli per ulteriori informazioni:

* [SDL Threat Modeling Tool](https://www.microsoft.com/sdl/adopt/threatmodeling.aspx) (Strumento per la modellazione di minacce SDL)
* [Architettura di riferimento di Microsoft Azure IoT](https://azure.microsoft.com/updates/microsoft-azure-iot-reference-architecture-available/)

## <a name="see-also"></a>Vedere anche
toolearn più sulla protezione soluzione IoT, vedere [proteggere la distribuzione di IoT][lnk-security-deployment].

È anche possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Domande frequenti su IoT Suite][lnk-faq]

È possibile leggere sulla sicurezza di IoT Hub in [tooIoT accesso controllo Hub] [ lnk-devguide-security] nella Guida per sviluppatori di IoT Hub hello.

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md

[lnk-security-deployment]: iot-suite-security-deployment.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md