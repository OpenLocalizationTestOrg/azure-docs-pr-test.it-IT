---
title: toomicroservices aaaIntroduction in Azure | Documenti Microsoft
description: "Panoramica del motivo per cui è importante per lo sviluppo di applicazioni moderne applicazioni cloud con un approccio di microservizi e come Azure Service Fabric fornisce una piattaforma tooachieve questo."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: fae2be85-0ab4-4cd3-9d1f-e0d95fe1959b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell
ms.openlocfilehash: b11920b9105e7575390e8fcf0d1ef6ab3c632978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="why-a-microservices-approach-toobuilding-applications"></a>Motivo per cui un microservizi approccio toobuilding applicazioni?
Per gli sviluppatori di software non c'è nulla di nuovo nel modo di considerare la fattorizzazione di un'applicazione nelle parti che la compongono. È un paradigma di centrale hello di orientamento agli oggetti, le astrazioni di software e la creazione dei componenti. Attualmente, questo GPO tende modulo hello tootake di classi e interfacce tra i livelli di tecnologia e le librerie condivise. In genere viene adottato un approccio su più livelli con un archivio nel back-end, la logica di business al livello intermedio e l'interfaccia utente (UI) nel front-end. Cosa *è* modificare hello ultimi anni è che, come gli sviluppatori, stiamo creando applicazioni distribuite che sono per cloud hello e dovute business hello.

Hello esigenze di business sono:

* Un servizio che viene compilato e opera, ad esempio, i clienti tooreach scala in aree geografiche di nuovo.
* Recapito più veloce di caratteristiche e funzionalità toobe toorespond in grado di toocustomer le richieste in modo flessibile.
* Migliorate costi tooreduce utilizzo delle risorse.

Queste esigenze aziendali incidono sul *modo* di compilare le applicazioni.

Per ulteriori informazioni sull'approccio hello toomicroservices Azure, leggere [Microservizi: revolution un'applicazione basata su cloud hello](https://azure.microsoft.com/blog/microservices-an-application-revolution-powered-by-the-cloud/).

## <a name="monolithic-vs-microservice-design-approach"></a>Approccio alla progettazione monolitico o con microservizi
Tutte le applicazioni si evolvono con il trascorrere del tempo. Applicazioni evolvono poiché toopeople utile. Le applicazioni che invece non hanno successo non si evolvono e alla fine vengono deprecate. Hello chiedersi: la quantità, è possibile sapere sui requisiti di oggi, e quali verranno in futuro hello? Si supponga, ad esempio, di dover realizzare un'applicazione per la creazione di report per un reparto. Si è certi che un'applicazione hello rimane nell'ambito di hello dell'azienda e che i report di hello sono di breve durati. La scelta dell'approccio è diversa da, ad esempio, la creazione di un servizio che offre tootens contenuto video di milioni di clienti. 

In alcuni casi, un elemento out sportello hello come modello di prova costituisce un fattore determinante hello, mentre si è certi che un'applicazione hello può essere riprogettata in un secondo momento. C'è poco senso nella sovraprogettazione di qualcosa che non verrà mai usato. Di hello consuete engineering compromesso. In hello altra parte, quando le società parlare di compilazione per hello cloud, si prevede di hello è la crescita e utilizzo. problema di Hello è che l'aumento delle dimensioni e la scala sono imprevedibili. Desideriamo tooprototype in grado di toobe rapidamente sapendo inoltre che si presenti in un percorso toodeal con successo. Questo approccio avvio snella hello è: compilare, misure, informazioni ed eseguire l'iterazione.

Durante l'era di hello client-server, è riflettendo toofocus sulla compilazione di applicazioni a più livelli utilizzando le tecnologie specifiche in ogni livello. il termine Hello *monolitico* applicazione è apparsa per questi approcci. interfacce Hello riflettendo toobe tra i livelli di hello, e viene utilizzata una struttura più accoppiamento tra componenti all'interno di ogni livello. Gli sviluppatori progettavano ed eseguivano il factoring delle classi compilate in librerie e collegate insieme in pochi file eseguibili e DLL. 

Esistono vantaggi toosuch un approccio di progettazione monolitica. È spesso più semplice toodesign e ha più veloce chiamate tra componenti, perché queste chiamate sono spesso su IPC (interprocess communication). Inoltre, tutti gli utenti test di un singolo prodotto, che tende a toobe altre persone risorse efficiente. svantaggio Hello è che vi sia un accoppiamento stretto tra livelli a più livelli è possibile ridimensionare i singoli componenti. Se è necessario tooperform correzioni o aggiornamenti, è necessario toowait per altri toofinish dei test. È più difficile toobe agile.

Microservizi indirizzo questi svantaggi e più strettamente allinearlo hello precedente i requisiti aziendali, ma dispongono anche i vantaggi e le responsabilità. vantaggi di Hello di microservizi sono che ognuno include in genere più semplice funzionalità di business, ridimensionare verso l'alto o verso il basso, test, distribuire e gestire in modo indipendente. Un importante vantaggio offerto un approccio microservizio è che i team sono dovuti più scenari di utilizzo di tecnologia, che hello approccio a più livelli incoraggia gli utenti. In pratica, team più piccoli sviluppano un microservizio sulla base di uno scenario del cliente, usando le tecnologie che preferiscono. 

In altre parole, organizzazione hello non necessario delle applicazioni toostandardize tech toomaintain microservizio. Team singoli servizi personalizzati eseguibili che cos'è significativa per base dell'esperienza di team o problema di hello toosolve più appropriato. In pratica, è preferibile avere un set di tecnologie consigliate, ad esempio un particolare archivio NoSQL o un framework di applicazioni Web.

svantaggio Hello di microservizi è disponibile in Gestione hello aumentato numero di entità separate e la gestione di controllo delle versioni e le distribuzioni più complessi. Traffico di rete tra microservizi hello aumenta e le latenze di rete corrispondente hello. La presenza di una grande quantità di servizi frammentati e granulari non può che dare origine a problemi di prestazioni. Senza strumenti toohelp visualizzare queste dipendenze, è difficile troppo intero sistema hello "vedere". 

Standard di utilizzo approccio microservizio hello da accettano come toocommunicate e la tolleranza di errore solo operazioni di hello è necessario un servizio, piuttosto che i contratti rigida. È importante toodefine progettano tali contratti di hello, poiché servizi aggiornare indipendentemente uno da altro. Un'altra descrizione coniata per la progettazione con approccio basato su microservizi è "SOA (Service Oriented Architecture) con granularità fine".

***Nella forma più semplice, hello microservizi approccio di progettazione è su una federazione di servizi per la comunicazione con le modifiche indipendenti apportate tooeach e concordato standard separata.***

Altre applicazioni basate su cloud vengono prodotti, persone scoperto che questo scomposizione di hello complessivo app nei servizi indipendenti, con stato attivo di scenario è un approccio migliore a lungo termine.

## <a name="comparison-between-application-development-approaches"></a>Confronto tra approcci allo sviluppo di applicazioni
![Sviluppo di applicazioni per la piattaforma Service Fabric][Image1]

1) Un'app monolitica include funzionalità specifiche del dominio e normalmente è divisa per livelli di funzionalità, ad esempio Web, business e dati.

2) Per la scalabilità di un'app monolitica, occorre clonarla in più server/macchine virtuali/contenitori.

3) Un'applicazione di microservizi separa le funzionalità in servizi più piccoli distinti.

4) Hello microservizi approccio scale out tramite la distribuzione di ogni servizio in modo indipendente, la creazione di istanze di questi servizi in macchine virtuali o i server/contenitori.

Progettazione di un microservizio approccio non rappresenta la soluzione per tutti i progetti, ma allineare più da vicino agli obiettivi aziendali hello descritti in precedenza. A partire da un approccio monolitico potrebbe essere accettabile se si conosce che sarà necessario codice toorework hello opportunità di hello in seguito a un progetto di microservizi. Più comunemente, iniziare con un'applicazione monolitica sia lenta suddividerla in più fasi, a partire da aree funzionali hello necessarie toobe più scalabile o agile.

toosummarize, approccio microservizio hello è toocompose l'applicazione di molti servizi di piccole dimensioni. Hello servizi eseguiti in contenitori che vengono distribuiti in un cluster di macchine. Team di dimensioni ridotte sviluppare un servizio che è incentrato su uno scenario e in modo indipendente il test, versione, distribuzione e scalabilità di ogni servizio in modo che l'intera applicazione hello può evolvere.

## <a name="what-is-a-microservice"></a>Definizione di microservizio
Esistono diverse definizioni di microservizi. Se si esegue la ricerca hello Internet, sono disponibili molte risorse utili che forniscono i propri punti di visualizzazione e le definizioni. Tuttavia, la maggior parte delle seguenti caratteristiche di microservizi hello ampiamente concordata:

* Incapsulano uno scenario aziendale o del cliente. Qual è il problema di hello che si intende risolvere?
* Sono sviluppati da un piccolo team di progettazione.
* Sono scritti in qualsiasi linguaggio di programmazione e usano qualsiasi framework.
* Sono costituiti da codice e facoltativamente da uno stato, entrambi sottoposti al controllo delle versioni, distribuiti e ridimensionati in maniera indipendente.
* Interagiscono con altri microservizi tramite interfacce e protocolli ben definiti.
* Nomi univoci (URL) utilizzato tooresolve loro posizione.
* Rimangono coerenti e disponibile in presenza di hello di errori.

È possibile riepilogare queste caratteristiche come segue:

***Le applicazioni di microservizi sono costituite da piccoli servizi rivolti ai clienti, scalabili e sottoposti al controllo delle versioni indipendentemente, che comunicano tra di essi tramite protocolli standard e interfacce ben definite.***

Abbiamo parlato hello primi due punti hello precedente sezione e ora si espandono e chiarire hello ad altri utenti.

### <a name="written-in-any-programming-language-and-use-any-framework"></a>Sono scritti in qualsiasi linguaggio di programmazione e usano qualsiasi framework
Gli sviluppatori, dovrebbe essere disponibile toochoose una lingua o framework che si desidera che, a seconda dei competenze o esigenze hello del servizio hello. In alcuni servizi, si potrebbero valore prestazioni hello di C++ sopra tutti gli altri. In altri servizi, facilità di hello di sviluppo gestito in c# o Java potrebbe essere più importanti. In alcuni casi, potrebbe essere necessario toouse una libreria di partner specifico, la tecnologia di archiviazione dati, o mezzo di esposizione di hello tooclients di servizio.

Dopo aver scelto una tecnologia, si ha familiarità con toohello operativa o gestione del ciclo di vita e la scalabilità del servizio hello.

### <a name="allows-code-and-state-toobe-independently-versioned-deployed-and-scaled"></a>Consente di toobe codice e lo stato in modo indipendente con controllo delle versioni, distribuiti e ridimensionato
Tuttavia è scegliere toowrite le microservizi, codice hello e, facoltativamente, lo stato di hello deve in modo indipendente distribuire, aggiornare e scalare. Questo è effettivamente uno di hello toosolve di problemi più difficile, perché è un po' tooyour scelta delle tecnologie. Per la scalabilità, è difficile comprendere come toopartition (o partizione) sia hello codice e stato. Quando codice hello e lo stato utilizzare tecnologie separate, che è comune, script di distribuzione hello per le microservizio necessario toobe toocope in grado di con il ridimensionamento in entrambi. Ciò implica anche l'agilità e la flessibilità, in modo è possibile aggiornare alcuni hello microservizi senza tooupgrade tutti gli elementi in una sola volta.

Restituzione monolitico e approccio microservizio toohello per qualche istante, hello diagramma seguente mostra le differenze di hello nello stato di toostoring approccio hello.

#### <a name="state-storage-between-application-styles"></a>Archiviazione dello stato tra stili dell'applicazione
![Archiviazione dello stato della piattaforma Service Fabric][Image2]

***approccio monolitico Hello hello sinistra ha un singolo database e i livelli di tecnologie specifiche.***

***approccio microservizi Hello hello destra è un grafico di microservizi interconnesse in cui lo stato è in genere con ambito toohello microservizio e vengono usate diverse tecnologie.***

In un approccio monolitico, in genere un'applicazione hello utilizza un singolo database. Il vantaggio di Hello consiste nel fatto che è un'unica posizione, che rende facile toodeploy. Ogni componente può disporre di una singola tabella toostore il relativo stato. I team devono toostrictly stato separato, che rappresenta una sfida. Inevitabilmente esistono temptations tooadd una nuova colonna tooan cliente tabella esistente, non un join tra tabelle e creare le dipendenze a livello di archiviazione hello. In questo caso, non sarà possibile ridimensionare i singoli componenti. 

Nell'approccio microservizi hello, ogni servizio gestisce e archivia il proprio stato. Ogni servizio è responsabile per la scalabilità delle richieste di hello toomeet insieme sia il codice dello stato del servizio hello. Un svantaggio è che quando è presente un toocreate necessità viste o query, dei dati dell'applicazione, è necessario tooquery in stato di diversi archivi. In genere, questo problema si risolve con un microservizio separato che crea una visualizzazione della raccolta di microservizi. Se è necessario tooperform più improvvisate query sui dati hello, ogni microservizio deve si consiglia di scrivere il servizio warehouse di dati tooa dati per analitica in linea.

Controllo delle versioni è specifico toohello distribuito versione di un microservizio in modo che più versioni diverse di distribuire ed eseguire side-by-side. Controllo delle versioni sono illustrati gli scenari di hello in cui una versione più recente di un microservizio. si verifica un errore durante l'aggiornamento e deve tooan indietro tooroll versione precedente. Hello altro scenario per il controllo delle versioni è in esecuzione di test, in cui gli utenti diversi esperienza diverse versioni del servizio hello A/B-style. Ad esempio, è comune tooupgrade un microservizio per un set specifico di nuove funzionalità di clienti tootest prima di distribuirlo più ampiamente. Dopo il ciclo di vita gestione di microservizi, a questo punto siamo arrivati toocommunication tra di essi.

### <a name="interacts-with-other-microservices-over-well-defined-interfaces-and-protocols"></a>Interagiscono con altri microservizi tramite interfacce ben definite e protocolli.
In questo argomento deve grande attenzione, perché la documentazione completa sull'architettura orientata ai servizi che è stata pubblicata su hello negli ultimi 10 anni descrive i modelli di comunicazione. In genere, la comunicazione dei servizi utilizza un approccio REST con i protocolli HTTP e TCP e XML o JSON come formato di serializzazione hello. Dal punto di vista dell'interfaccia, sta adottando l'approccio di progettazione web hello. Nulla vieta tuttavia di usare protocolli binari o formati di dati personalizzati. Essere preparati per persone toohave difficoltà utilizzando il microservizi se apertamente disponibili.

### <a name="has-a-unique-name-url-used-tooresolve-its-location"></a>Ha utilizzato un nome univoco (URL) tooresolve posizione
Ricordare come si continuiamo indicante che l'approccio microservizio hello è ad esempio hello web? Ad esempio hello web, del microservizio deve toobe indirizzabile ogni volta che è in esecuzione. Se si inizia a chiedersi quale computer esegue un determinato microservizio, presto inizieranno le difficoltà. 

In hello stesso modo che DNS risolve una determinata macchina particolare tooa di URL, del microservizio deve toohave un nome univoco in modo che la posizione corrente è individuabile. Microservizi necessario indirizzabili nomi che li rendono indipendente dall'infrastruttura di hello che vengono eseguiti in. Ciò implica che vi sia un'interazione tra la modalità di distribuzione del servizio e come viene individuato, perché è necessario toobe un registro di sistema del servizio. Allo stesso modo, quando un computer non riesce, servizio Registro di sistema hello deve sapere in cui è in esecuzione il servizio di hello. 

Questo ci porta argomento successivo toohello: resilienza e coerenza.

### <a name="remains-consistent-and-available-in-hello-presence-of-failures"></a>Rimane coerente e disponibile in presenza di hello di errori
La gestione di errori imprevisti è uno dei più difficili toosolve problemi di hello, in particolare in un sistema distribuito. Gran parte del codice hello scritto come gli sviluppatori è la gestione delle eccezioni, si tratta inoltre dove hello la maggior parte delle viene impiegato il tempo durante i test. problema di Hello è più complessa rispetto alla scrittura di codice toohandle errori. Cosa accade quando ha esito negativo macchina hello in cui è in esecuzione microservizio hello? Non solo è necessario toodetect questo errore microservizio (un problema difficile autonomamente), ma è necessario anche un elemento toorestart del microservizio. 

Un microservizio deve toofailures resilienti toobe e riavviare spesso in un altro computer per motivi di disponibilità. Include anche verso il basso toohello stato salvato per conto di hello microservizio, hello microservizio possibile ripristinare questo stato da e se microservizio hello è in grado di toorestart correttamente. In altre parole, è necessaria la resilienza toobe nel calcolo hello (riavvii processo hello) nonché resilienza nello stato di hello o dati (nessuna perdita di dati o dati hello rimangono coerenti).

problemi di Hello di resilienza sono complica durante altri scenari, ad esempio quando gli errori verificarsi durante l'aggiornamento dell'applicazione. Hello microservizio, utilizzo di sistema di distribuzione hello, non deve necessariamente toorecover. Toothen ma è necessario anche decidere se è possibile continuare versione più recente di inoltro toohello toomove o eseguirne il rollback tooa precedente versione toomaintain uno stato coerente. Domande, ad esempio se numero sufficiente di computer sono disponibili tookeep lo spostamento in avanti e in che modo le versioni precedenti di toorecover di hello microservizio necessario toobe considerati. Questa operazione richiede hello microservizio tooemit integrità informazioni toobe in grado di toomake tali decisioni.

### <a name="reports-health-and-diagnostics"></a>Segnalano integrità e diagnostica
Anche se è un concetto apparentemente ovvio e spesso trascurato, un microservizio deve segnalare il proprio stato di integrità e fornire dati di diagnostica. In caso contrario, saranno disponibili pochi dettagli da un punto di vista operativo. Correlazione di eventi di diagnostica in un set di servizi indipendenti e affrontare gli sfasamenti dell'orologio macchina senso toomake dell'ordine degli eventi di hello è difficile. In hello allo stesso modo di interagire con un microservizio concordato protocolli e i dati formattati, si Emerge necessità di standardizzazione in modalità toolog integrità e gli eventi di diagnostica che infine finire in un evento di archiviano per l'esecuzione di query e la visualizzazione. In un approccio basato su microservizi, è fondamentale che i diversi team concordino un unico formato di registrazione. È necessario toobe un approccio coerente tooviewing gli eventi di diagnostica nell'applicazione hello nel suo complesso.

L'integrità è diversa dalla diagnostica. Integrità riguarda il microservizio hello reporting le azioni appropriate di tootake lo stato corrente. Un buon esempio collabora con la disponibilità toomaintain di meccanismi di aggiornamento e la distribuzione. Anche se un servizio può essere attualmente non integro a causa di arresto anomalo del processo tooa o il riavvio del computer, servizio hello potrebbe ancora essere operativa. ultima operazione Hello è necessario è toomake questo peggiorando eseguendo un aggiornamento. approccio migliore Hello è toodo un'indagine o attendere il tempo toorecover microservizio hello. Gli eventi di integrità di un microservizio consentono di prendere decisioni informate e favoriscono in effetti la creazione di servizi con funzionalità di riparazione automatica.

## <a name="service-fabric-as-a-microservices-platform"></a>Service Fabric come piattaforma di microservizi
Azure Service Fabric è emersa da una transizione da Microsoft dai prodotti casella, in genere monolitici in stile, toodelivering servizi di distribuzione. esperienza di Hello di creare e gestire servizi di grandi dimensioni, ad esempio Database SQL di Azure e Azure Cosmos DB, la forma di Service Fabric. piattaforma Hello si evolve nel tempo adottato più servizi. Inoltre, Service Fabric era toorun non solo in Azure, ma anche nelle distribuzioni di Windows Server autonomo.

***obiettivo di Hello di Service Fabric è toosolve problemi di compilazione e l'esecuzione di un servizio hello e utilizzano le risorse di infrastruttura in modo efficiente, in modo che i team di risolvere i problemi di business utilizzando un approccio di microservizi.***

Service Fabric fornisce tre aree ampie toohelp si compilano applicazioni che utilizzano un approccio di microservizi:

* Una piattaforma che fornisce toodeploy di servizi di sistema, eseguire l'aggiornamento, rilevare e riavviare i servizi non riusciti, individuare i servizi, indirizzare i messaggi, gestire lo stato e monitorare l'integrità. Questi servizi di sistema, in effetti, abilitare molte delle caratteristiche di hello di microservizi descritto in precedenza.
* Applicazioni toodeploy possibilità entrambi in esecuzione in contenitori o come elabora. Service Fabric è una struttura per la gestione di contenitori e processi.
* API di programmazione produttive, toohelp si compilano applicazioni come microservizi: [ASP.NET Core e Reliable Actors servizi affidabili](service-fabric-choose-framework.md). È possibile scegliere qualsiasi toobuild codice del microservizio. Queste API processo hello rendere più semplici, ma vengono integrate con la piattaforma di hello a un livello più profondo. forniscono, ad esempio, informazioni su integrità e diagnostica o consentono di sfruttare la disponibilità elevata predefinita.

***Service Fabric è indipendente dalla modalità di compilazione del servizio, quindi è possibile usare qualsiasi tecnologia. Tuttavia, fornisce le API di programmazione predefinite che rendono più semplice toobuild microservizi.***

### <a name="migrating-existing-applications-tooservice-fabric"></a>Migrazione tooService applicazioni esistenti dell'infrastruttura
TooService un approccio chiave dell'infrastruttura è codice tooreuse esistente, quindi può essere moderno e con nuova microservizi. Esistono cinque fasi tooapplication modernizzazione ed è possibile avviare e arrestare in una delle fasi di hello. Si tratta di:

1) Esecuzione di un'applicazione monolitica tradizionale.
2) Accuratezza e MAIUSC - utilizzare contenitori o codice esistente toohost file eseguibili di guest nell'infrastruttura del servizio.
3) Modernizzazione: nuovi microservizi aggiunti al codice esistente in contenitori. 
4) Innovazione - violare hello monolitico microservizi esclusivamente in base alle esigenze.
5) Trasformata microservizi - trasformazione hello di applicazioni monolitiche esistente o creare nuove applicazioni di base.

![Migrazione tooMicroservices][Image3]

È importante tooemphasis nuovamente, che è possibile **avviare e arrestare qualsiasi di queste fasi**, non si è costretta toomoved toohello successiva fase. Di seguito sono elencati esempi per ogni fase.

**Spostare** : un numero elevato di società è sollevamento e spostamento applicazioni monolitiche esistenti in contenitori toofor due motivi;

- Riduzione dei costi, a causa di tooconsolidation e la rimozione delle applicazioni esistenti di hardware o di esecuzione maggiore densità. 
- Contratti di distribuzione uniforme tra i settori sviluppo e operazioni.

Riduzione dei costi sono comprensibili e all'interno di Microsoft in un numero elevato di applicazioni esistenti contenitore semplicemente toomillions di dollari. Distribuzione uniforme è più difficile tooevaluate, ma ugualmente importante. Dichiara che gli sviluppatori possono ancora essere la tecnologia gratuito toochoose hello che gruppi di loro, ma le operazioni di hello solo accetterà toodeploy una modalità singola e gestire tali applicazioni. Limita le operazioni di hello dalla presenza di toodeal con una complessità di hello delle numerose tecnologie diverse o imporre agli sviluppatori tooonly scegliere alcuni. In termini semplici, ogni applicazione viene inserita in un'immagine di distribuzione autonoma.

Per molte organizzazioni il processo termina qui. Dispongono già di vantaggi hello di contenitori e Service Fabric esperienza di gestione completa hello dalla distribuzione, gli aggiornamenti, controllo delle versioni, rollback e così via monitoraggio di integrità.

**Modernizzazione** -è hello aggiunta di nuovi servizi insieme il codice esistente nei contenitori. Se si intende toowrite nuovo codice, è migliori passaggi più piccoli in tootake toodecide verso il basso il percorso di microservizi hello. Questo approccio può corrispondere all'aggiunta di un nuovo endpoint API REST o di nuova logica di business. In questo modo, si avvia in viaggio hello di microservizi nuova compilazione e procedure consigliate di sviluppo e sulla relativa distribuzione.

**Innovazione** -ricordare tali originale esigenze di business all'avvio di hello di questo articolo, che determinano l'approccio di microservizi hello? Decisione hello questa fase è, sono avviene toomy corrente applicazione e in tal caso, è necessario toostart suddivisione monolito hello o innovazione. Ad esempio è possibile che un database diventi un collo di bottiglia a livello di elaborazione perché è usato come coda del flusso di lavoro. Numero di hello di richieste di flusso di lavoro aumentare hello collaborare toobe esigenze distribuita per la scala. Pertanto per quel particolare parte dell'applicazione hello non scalabilità, oppure è necessario tooupdate più frequentemente, dividere la natura un microservizio e l'innovazione. 

**Trasformazione in microservizi**: in questa fase l'applicazione è totalmente composta da (o scomposta in) microservizi. tooreach qui, è stata apportata viaggio microservizi hello. È possibile avviare in questo caso, ma toodo questo senza un toohelp piattaforma microservizi è un investimento significativo. 

### <a name="are-microservices-right-for-my-application"></a>I microservizi sono appropriati per l'applicazione in uso?
È possibile. Si sono verificati durante come più team di Microsoft è stata iniziata toobuild per cloud hello per ragioni aziendali, molti di essi realizzato vantaggi hello di adottare un approccio di tipo microservizio. Bing, ad esempio, sviluppa microservizi di ricerca da anni. Per altri team, approccio microservizi hello è nuovo. Sono stati trovati team che non vi sono problemi toosolve esterni alle aree di base del livello di attendibilità. Ecco perché Service Fabric acquisita trazione come tecnologia di hello ideale per la creazione di servizi.

obiettivo di Hello di Service Fabric è complessità hello tooreduce della compilazione di applicazioni con un approccio microservizio, in modo che non si dispone toogo tramite come molte costose ridefinizione. Iniziare quando necessario, deprecare i servizi, aggiungerne di nuovi e le evolvere con cliente utilizzo è l'approccio di hello. Sappiamo che non esistono molti altri problemi ancora toobe risolto microservizi toomake più accessibile per gli sviluppatori. Contenitori e modello di programmazione attore hello sono esempi di passaggi più piccoli nella direzione specificata, e si è certi che altre innovazioni emergeranno toomake questo più semplice.
 
<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Passaggi successivi
* [Panoramica della terminologia di Service Fabric](service-fabric-technical-overview.md)
* [Microservizi: Un revolution applicazione basata su cloud hello](https://azure.microsoft.com/en-us/blog/microservices-an-application-revolution-powered-by-the-cloud/)

[Image1]: media/service-fabric-overview-microservices/monolithic-vs-micro.png
[Image2]: media/service-fabric-overview-microservices/statemonolithic-vs-micro.png
[Image3]: media/service-fabric-overview-microservices/microservices-migration.png
