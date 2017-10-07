---
title: aaaAzure SQL Database Azure Case Study - Snelstart | Documenti Microsoft
description: "Informazioni sulle modalità di espansione delle SnelStart utilizza Database SQL toorapidly i servizi di business con una frequenza di 1.000 nuovi database di SQL Azure al mese"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Grazie ad Azure, SnelStart ha rapidamente ampliato i servizi aziendali con una frequenza di 1.000 nuovi database SQL di Azure al mese
![SnelStartLogo](./media/sql-database-implementation-snelstart/snelstartlogo.png)

Paesi Bassi hello SnelStart rende diffusi finanziari e business-software di gestione per le piccole e medie imprese (SMB). I 55.000 clienti sono serviti da un organico composto da 110 dipendenti, tra cui 35 esperti del reparto IT. Spostando dall'offerta di software-as-a-service (SaaS) tooa software desktop basato su Azure, effettuata hello più SnelStart di servizi integrati, automatizzare la gestione tramite l'ambiente familiare in c# e l'ottimizzazione delle prestazioni e scalabilità da nessuna delle due over - o l'underprovisioning le aziende che utilizzano il pool elastico. L'uso di Azure offre fluidità hello SnelStart dello spostamento clienti tra sedi locali e hello cloud.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>Motivo per cui SnelStart estesi servizi dal cloud toohello desktop hello
> "Utilizzo di Azure significa che è possibile fornire più rapidamente il software, rapidamente rispondono toocustomer richieste e scalare le soluzioni in aumento di richieste."
> 
> - Henry Been, progettista software
> 
> 

SnelStart ha gestito per anni un'azienda di successo nella produzione di software tramite un modello di sviluppo tradizionale: codice, pacchetto, spedizione e ripetizione. Nel corso del tempo, hello in base alla velocità di modifica aumento delle dimensioni più veloce e più velocemente. Normative modificati di frequente e clienti necessari più dati finanziari di modi tooprocess e collaborano con i relativi contabili e government tookeep backup con tali modifiche.

"Shipping toocustomers software è costoso e limitazione," in base tooHenry stato, architetti software. "I costi di produzione, imballo e spedizione limitavano la frequenza di rilascio di nuovi software. Abbiamo toopackage aggiornamenti per le spedizioni periodiche, ma che apportate toomeet reali dei clienti la modifica è necessario. È stato possibile mai certezza che i clienti aggiornato toohello la versione più recente del prodotto hello. Pertanto, abbiamo toosupport più versioni, rendendo hello supportano anche processo molto difficile toodo."

Stato aggiunge, "Desideravamo modo tooprogram e rilascio aggiornamenti un'accelerazione alla velocità, in modo che è stato possibile innovazione più velocemente e creare nuovi servizi per i clienti. Desideravamo anche tooautomate un modo più processi in ordine toosimplify esigenze di amministrazione di business dei clienti."

Per SnelStart, hello soluzione è stata tooextend relativi servizi ad acquisire un provider di SaaS basato su cloud. piattaforma di Database SQL di Azure Hello consentito SnelStart sfruttarla senza l'overhead dovuto all'hello principali IT che richiede una soluzione infrastructure-as-a-service (IaaS).

modello di cloud Hello inoltre consente SnelStart toofix bug e offre nuove funzionalità rapidamente, senza i clienti che necessitano di toodownload e aggiornamento software. Secondo tooBeen, "servizi cloud di Azure tramite consente act tooquickly in seguito alla modifica di requisiti di terze parti. Anziché tooship un toothousands versione nuova di clienti, è possibile adattare le informazioni inviate dai formati di applicazione desktop toonew richiesto da terze parti."

## <a name="a-modern-company-with-traditional-roots"></a>Un'azienda moderna con radici tradizionali
SnelStart è un moderno, agile e ad alta tecnologia business con radici modesto risalenti too1964, quando fondatori hello avviata società hello come un costruttore di parti strumento musicale. cuore Hello di hello business software SnelStart avviato molto elevati in hello 1980s, durante la proliferazione di hello di hello personal computer. società Hello è necessario un software di contabilità toohello alternativa migliore disponibile in fase di hello, pertanto impiegato questioni nelle proprie mani. In 1982, società hello creato foundation hello del software per la contabilità SnelStart infine che costituiranno. Dall'inizio di hello, software hello è stata ammirato per la semplicità e la velocità, tanto in modo che società hello infine modificato lo stato attivo e se stesso riprogettato in una società di software.

Nel 1995, SnelStart rilascia la prima applicazione di contabilità per Windows. un'applicazione Hello, compilata nel database di Microsoft Visual Basic 1.0 e Microsoft Access, consente di aumentare hello toomore base di clienti di 5.000 utenti.

Oggi, SnelStart è un importante fornitore di applicazioni line-of-business (LOB) e di amministrazione aziendale per le piccole e medie imprese e per gli imprenditori autonomi dei Paesi Bassi. Come Carlo Kuip, architetti IT, viene visualizzato, "il nostro obiettivo è tooprovide al 100% automazione dei servizi di amministrazione di business per i clienti".

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>Ottimizzazione delle prestazioni e dei costi con i pool elastici
SnelStart è stata un pioniere globale nell'adozione di pool elastici. Il pool elastico dei costi di limite società hello e gestione i requisiti di prestazioni in modo più efficiente. In base tooBeen, "tramite i pool elastici, che è possibile ottimizzare le prestazioni in base alle esigenze di hello dei clienti, senza eseguire un provisioning eccessivo. Se si è verificato in base al carico di picco tooprovision, sarebbe molto costoso. In alternativa, hello risorse tooshare opzione tra più database di scarso utilizzo consente una soluzione che offre prestazioni soddisfacenti ed è conveniente toocreate. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>I database SQL di Azure aiutano a containerizzare i dati a scopo di isolamento e sicurezza
Database SQL di Azure consente SnelStart tooeasily e spostare in modo trasparente tooAzure di dati di business-amministrazione locali dei clienti. Hello Database SQL di Azure è un contenitore semplice che fornisce l'isolamento, un limite per l'autenticazione, autorizzazione e funzionalità di backup e ripristino semplice. I database offrono un modello concettuale ideale per l'amministrazione aziendale. Secondo tooCarlo Kuip, architetti IT, "elementi all'interno di questo limite contenitore contengono dati riservati che sono fondamentale tooa business e l'archiviazione di tali elementi in mantiene un database isolato li ben protetti. È possibile gestire l'autorizzazione a livello di database hello e automatizzare anche la gestione di hello e scalabilità orizzontale di questi database senza richiedere agli amministratori di database (DBA) sul personale".

Inoltre, Azure SQL Data Warehouse svolge un ruolo nella storia di sicurezza e la gestione di SnelStart hello grazie alla possibilità di società hello raccogliere dati di telemetria, ad esempio il rilevamento delle intrusioni, la registrazione dell'attività utente e la connettività.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure elimina i sovraccarichi in modo che gli sviluppatori possano dedicare più tempo alla creazione di iniziative di valore
modello di piattaforma Azure Hello rimosso un sovraccarico di infrastruttura e abilitato le distribuzioni di tooautomate SnelStart usando le raccolte di gestione di c#. Kuip, come indicato "è stato in grado di toogrow le nostre operazioni corrente con una piccola personale durante il ripristino di emergenza, velocità e scalabilità contemporaneamente a incremento opzioni per i client. sviluppo di Hello MAIUSC tooservices liberato risorse toofocus nuovi servizi e funzionalità, anziché semplicemente aggiornando backup tookeep codice esistente con nuovi codici normative o fiscali." Aggiunge, "L'automazione della gestione e utilizzando offerta SaaS hello, siamo in grado di toodeliver più il valore per i nostri clienti senza investimenti di grandi dimensioni toomake nello staff operativo". Ad esempio, tramite il pool elastico e di Azure, SnelStart è stato in grado di tooadd un'ampia gamma di nuove funzionalità, inclusa l'integrazione di dati dei clienti più affidabile con banche, fatturazione nuovi servizi, i controlli di sfondo per piccole aziende e servizi di posta elettronica.

> "Hello solo primi mesi del 2016, è espanso il nostro le distribuzioni di Database SQL di Azure da circa 5.500 toomore rispetto a 12.000 e aggiungiamo attualmente circa 1.000 database al mese".
> 
> - Henry Been, progettista software
> 
> 

Gestione di database è ulteriormente automatizzato tramite funzionalità di processi elastico hello. Kuip, come indicato "elevata grazie per l'individuazione automatica dei database in un'istanza del database di SQL Server [server] hello." In questo modo SnelStart tooexecute operazioni di gestione tra il cliente in modo dinamico crescente base senza alcun costo aggiuntivo.

SnelStart sta anche sviluppando un'API che funge da broker tra i dati dei clienti e le applicazioni compilate da produttori di software di terze parti. Come stati Kuip, "questa API consentirà altri software di tooour funzionalità tooadd fornitori, ad esempio eliminando i dati immessi per le fatture e altri documenti." I clienti non disporrà più fatture di tipo toomanually nel software di contabilità per piccole aziende; Hello SnelStart software si scambieranno direttamente le informazioni necessarie hello. Questo consente ai clienti toojoin loro amministrazione aziendale attività con l'ecosistema di hello di informazioni che la trasformazione digitale nel settore hello.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Come i servizi Azure abilitano SaaS per SnelStart
Tramite Azure, SnelStart può essere utilizzato dai propri clienti e i relativi contabili più facilmente nel cloud di hello. Ad esempio, sia i clienti che i contabili possono condividere informazioni accedendo direttamente all'API client di SnelStart, ospitata in Azure. Gli stati Kuip, "questi servizi riutilizzabili sono disponibili tooour orientati ai clienti web App e forniscono comuni dell'infrastruttura e funzioni di amministrazione di toobusiness tooallow accesso per i clienti e il software di terze parti toothird utilizzati dai clienti. Tra queste, funzionalità di configurazione del prodotto, gestione delle regole del firewall e gestione dei processi a esecuzione prolungata come i backup".

> L'obiettivo è tooprovide al 100% automazione dei servizi di amministrazione di business per i clienti". 
> 
> - Carlo Kuip, progettista IT
> 
> 

Inoltre, i servizi web SnelStart consentono ai clienti e accedere ai dati di contabilità tooeasily nel pool elastico di Database SQL di Azure. Questo modello SaaS, insieme all'elasticità del database e a Azure Resource Manager, fornisce a SnelStart funzionalità di scalabilità che completano ogni distribuzione di Azure. implementazione di Hello è completamente automatizzata utilizzando le raccolte di gestione di c#.

![Architettura di SnelStart](./media/sql-database-implementation-snelstart/figure1.png)

Figura 1. A partire da giugno 2016, SnelStart dispone di oltre 11.000 database e di oltre 50 pool elastici

## <a name="simplicity-from-hello-cloud"></a>Semplicità dal cloud hello
Dopo lo spostamento di tooan soluzione Azure basato su cloud, SnelStart è stata la crescita rapida cliente toosupport in grado di offrendo servizi e funzionalità innovative. In base tooBeen, "con Azure, possiamo offrire aggiornamenti quasi continua per i clienti, senza il personale addetto alle operazioni di espansione. Si otterrà hello tutte le altre importanti funzionalità di Azure, come la scalabilità e ripristino di emergenza, ovvero aggregati in. "

> "Quando è stato effettivamente su Redmond... Si riceve una chiamata da uno sviluppatore in paesi bassi hello, collegarsi a me su uno specifico problema. Ci sono stati in grado di tooget Microsoft toodeliver una modifica nel proprio ambiente di produzione all'interno di 48 ore toosolve il problema. "
> 
> - Henry Been, progettista software
> 
> 

SnelStart anche ringrazia gli utenti di stretta collaborazione hello sviluppate con il team di database SQL di Microsoft Azure hello. Come stati Kuip, "Abbiamo discussioni sulle funzionalità e la tecnologia toouse, ovvero un elemento apprezzato su entrambi i lati."
obiettivo immediato Hello SnelStart è tookeep aumento delle dimensioni di base relativi clienti soddisfatti. Come è stato indicato, "Senza hello tecnico e i limiti delle risorse che si è verificato in qualità di ISV, non si è toohow alcun limite molto accompagnare".

## <a name="more-information"></a>Altre informazioni
* toolearn ulteriori informazioni sui pool elastici Azure, vedere [pool elastici](sql-database-elastic-pool.md).
* toolearn ulteriori informazioni sui ruoli Web e ruoli di lavoro, vedere [i ruoli di lavoro](../fundamentals-introduction-to-azure.md#compute).    
* toolearn ulteriori informazioni su Azure SQL Data Warehouse, vedere [SQL Data Warehouse](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* vedere toolearn ulteriori informazioni su SnelStart, [SnelStart](http://www.snelstart.nl).

