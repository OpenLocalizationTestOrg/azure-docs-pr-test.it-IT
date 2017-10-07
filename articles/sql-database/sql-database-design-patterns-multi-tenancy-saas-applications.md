---
title: modelli di aaaDesign per applicazioni SaaS multi-tenant e Database SQL di Azure | Documenti Microsoft
description: "In questo articolo illustra i requisiti di hello e i modelli di architettura di dati comuni delle applicazioni di database multi-tenant in esecuzione in un ambiente cloud tooconsider e hello diversi svantaggi con questi modelli. Illustra anche l'utilità del database SQL di Azure, con i relativi pool e strumenti elastici, per soddisfare questi requisiti senza dover scendere a compromessi."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Schemi progettuali per le applicazioni SaaS multi-tenant e il database SQL di Azure
In questo articolo viene sui requisiti di hello e i modelli di architettura di dati comuni di multi-tenant software come applicazioni di database un servizio (SaaS) in esecuzione in un ambiente cloud. Vengono inoltre illustrati i fattori di hello necessari tooconsider e hello vantaggi e svantaggi dei modelli di progettazione diverse. I pool e gli strumenti elastici nel database SQL di Azure consentono di soddisfare requisiti specifici senza compromettere altri obiettivi.

In alcuni casi, gli sviluppatori di effettuano scelte che funzionano con i relativi interessi migliore a lungo termine quando si progettano i modelli di tenancy per i livelli dati hello di applicazioni multi-tenant. Inizialmente, almeno, uno sviluppatore potrebbe percepiscono la semplicità di sviluppo e riduzione dei costi di provider del servizio cloud come più importante della scalabilità di isolamento o hello tenant di un'applicazione. Questa scelta può causare problemi di soddisfazione toocustomer e una correzione di corso costosa in un secondo momento.

Un'applicazione multi-tenant è un'applicazione ospitata in un ambiente cloud e che fornisce hello stesso insieme di servizi toohundreds o migliaia di tenant che ha non condividere o visualizzare i dati di altro. Un esempio è un'applicazione SaaS che offre servizi tootenants in un ambiente ospitato su cloud.

## <a name="multi-tenant-applications"></a>Applicazioni multi-tenant
Nelle applicazioni multi-tenant i dati e il carico di lavoro possono essere facilmente partizionati. È possibile partizionare i dati e carico di lavoro, ad esempio, lungo i limiti di tenant, perché la maggior parte delle richieste entro confini hello di un tenant. Tale proprietà è implicita nei dati hello e carico di lavoro hello e Ottimizza per i modelli di applicazione hello descritti in questo articolo.

Gli sviluppatori utilizzano questo tipo di applicazione attraverso l'intera gamma di hello applicazioni basate su cloud, tra cui:

* Applicazioni di database partner che stanno toohello transizione cloud come applicazioni SaaS
* Applicazioni SaaS compilate per cloud hello da hello messa a terra
* Applicazioni rivolte direttamente ai clienti
* Applicazioni aziendali per i dipendenti

Applicazioni SaaS che sono progettate per il cloud hello e quelli con radici come applicazioni di database di partner sono in genere applicazioni multi-tenant. Queste applicazioni SaaS offrono un'applicazione software specifico come tenant di tootheir un servizio. I tenant possono accedere a servizio dell'applicazione hello e la proprietà completa di dati associati, archiviati come parte di un'applicazione hello. Ma tootake sfruttare i vantaggi di hello di SaaS, i tenant deve cedere alcuni controllo sui propri dati. Si considerino reciprocamente attendibili hello SaaS servizio provider tookeep i propri dati sicuri e isolati dai dati degli altri tenant. Esempi di questo tipo di applicazione SaaS multi-tenant sono MYOB, SnelStart e Salesforce.com. Ognuna di queste applicazioni può essere partizionata lungo i limiti di tenant e i modelli di progettazione delle applicazioni di supporto hello che vengono discussi in questo articolo.

Le applicazioni che forniscono un servizio diretto toocustomers o tooemployees all'interno dell'organizzazione (gli utenti a cui si fa spesso riferimento tooas, piuttosto che i tenant) sono un'altra categoria spettro di hello applicazione multi-tenant. I clienti Iscriviti toohello servizio e non si è proprietari raccoglie dati hello hello provider di servizi e le archivia. Provider di servizi hanno meno severe tookeep requisiti dei dati dei clienti isolati una da altra oltre in materia di privacy obbligatoria per enti pubblici. Provider di contenuti multimediali come Netflix, Spotify e Xbox LIVE sono alcuni esempi di questo tipo di applicazione multi-tenant per i clienti. Altri esempi di applicazioni facilmente partizionabili sono le applicazioni per Internet per i clienti o le applicazioni Internet delle cose (IoT), in cui ogni cliente o dispositivo può essere usato come partizione. È possibile tracciare limiti delle partizioni per separare diversi utenti o dispositivi.

Non tutte le applicazioni tuttavia sono facilmente partizionabili in base a una singola proprietà, ad esempio il tenant, il cliente, l'utente o il dispositivo. Un esempio è un'applicazione ERP (Enterprise Resource Planning) complessa con prodotti, ordini e clienti. In genere ha uno schema complesso con migliaia di tabelle altamente interconnesse.

Alcuna strategia di singola partizione può applicare tooall tabelle e di lavoro in carico di lavoro di un'applicazione. Questo articolo è incentrato sulle applicazioni multi-tenant con carichi di lavoro e dati facilmente partizionabili.

## <a name="multi-tenant-application-design-trade-offs"></a>Compromessi nella progettazione di applicazioni multi-tenant
modello di progettazione Hello che uno sviluppatore di applicazioni multi-tenant sceglie in genere si basa su una considerazione di hello seguenti fattori:

* **Isolamento dei tenant**. Hello sviluppatore tooensure che tenant non contenga i dati di accesso non autorizzato tooother dei tenant. requisiti di isolamento Hello estende tooother proprietà, ad esempio fornendo la protezione da altre istanze rumore, da toorestore in grado di dati di un tenant e implementare personalizzazioni specifico del tenant.
* **Costo delle risorse cloud**. Un'applicazione SaaS deve toobe competitivi. Uno sviluppatore di applicazioni multi-tenant scegliere toooptimize per ridurre il costo in uso hello delle risorse cloud, ad esempio l'archiviazione e i costi di calcolo.
* **Facilità della metodologia DevOps**. Uno sviluppatore di applicazioni multi-tenant deve protezione isolamento tooincorporate, gestire, monitorare l'integrità di hello della loro applicazione e lo schema del database e risolvere i problemi di tenant. Complessità lo sviluppo di applicazioni e operazione converte direttamente tooincreased costo e verifica con la soddisfazione dei tenant.
* **Scalabilità**. Hello possibilità tooincrementally aggiungere più tenant e la capacità per i tenant che hanno l'esigenza è imperativo tooa operazione SaaS.

Ciascuno di questi fattori è tooanother compromessi confrontati. cloud di costo più basso Hello offerta potrebbero non offrire hello più semplice lo sviluppo. È importante per gli sviluppatori toomake informato scelte queste opzioni e i relativi vantaggi e svantaggi durante il processo di progettazione dell'applicazione hello.

Un modello di distribuzione comuni è toopack più tenant in una o più database. vantaggi di Hello di questo approccio sono un costo inferiore perché si paga per alcuni database e relativa semplicità di hello dell'utilizzo di un numero limitato di database. Nel tempo, tuttavia, uno sviluppatore di applicazioni multi-tenant SaaS comprenderà che questa scelta presenta svantaggi sostanziali a livello di scalabilità e isolamento dei tenant. Se l'isolamento dei tenant diventa importante, sforzo aggiuntivo è necessario tooprotect tenant dati nel servizio di archiviazione condiviso da accessi non autorizzati o rumore router adiacenti. Questo impegno aggiuntivo potrebbe aumentare notevolmente i costi di manutenzione dell'isolamento e l'impegno legato allo sviluppo. Analogamente, se l'aggiunta tenant è necessaria, questo schema progettuale richiede in genere esperienza tooredistribute tenant dati tra il livello database tooproperly scala hello dati di un'applicazione.  

Spesso l'isolamento dei tenant è un requisito fondamentale nelle applicazioni SaaS multi-tenant che soddisfano toobusinesses e organizzazioni. Gli sviluppatori potrebbero essere tentati dagli apparenti vantaggi legati alla semplicità e ai costi, a scapito della scalabilità e dell'isolamento dei tenant. Questo compromesso può risultare complessa e dispendiosa come servizio hello cresce e i requisiti di isolamento tenant diventano più importanti e gestiti a livello di applicazione hello. Tuttavia, nelle applicazioni multi-tenant che forniscono un toocustomers servizio diretto, per consumatori, isolamento dei tenant potrebbe essere una priorità più bassa rispetto all'ottimizzazione per la risorsa cloud.

## <a name="multi-tenant-data-models"></a>Modelli di dati multi-tenant
Le comuni procedure di progettazione per l'inserimento dei dati dei tenant seguono tre modelli distinti, illustrati nella figura 1.

![modelli di dati di applicazioni multi-tenant](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Figura 1: Procedure di progettazione comuni per modelli di dati multi-tenant

* **Database per ogni tenant**. ogni tenant dispone del proprio database. Tutti i dati specifici del tenant è il database del tenant toohello ristretto e isolato da altri tenant e i relativi dati.
* **Database condiviso partizionato**. più tenant condividono uno di più database. Un set distinto di tenant viene assegnato tooeach database utilizzando una strategia di partizionamento come hash, intervallo o elenco di partizionamento. Questa strategia di distribuzione di dati è spesso di partizionamento orizzontale tooas cui viene fatto riferimento.
* **Database condiviso singolo**. un unico database, talvolta di grandi dimensioni, contiene i dati di tutti i tenant, identificati senza ambiguità tramite una colonna ID tenant.

> [!NOTE]
> Uno sviluppatore di applicazioni può scegliere tooplace tenant diversi negli schemi di database diverso e quindi utilizzare hello schema nome toodisambiguate hello diversi tenant. Non è consigliabile questo approccio perché in genere richiede l'uso di hello di SQL dinamico, e non può essere efficace per la memorizzazione nella cache di piano. Nel resto di questo articolo hello esaminato l'approccio tabella hello condiviso per questa categoria di applicazione multi-tenant.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Modelli di dati multi-tenant comuni
Si tratta di tipi diversi di hello tooevaluate importante dei modelli di dati di multi-tenant in termini di hello applicazione progettazione compromessi che è già stato identificato. Questi fattori consentono di caratterizzare hello tre modelli di dati di multi-tenant più comuni descritti in precedenza e l'utilizzo di database, come illustrato nella figura 2.

* **Isolamento**. Hello di isolamento tra tenant può essere una misura di quanto un modello di dati consente di ottenere l'isolamento dei tenant.
* **Costo delle risorse cloud**. quantità di Hello di condivisione delle risorse tra i tenant è possibile ottimizzare il costo di risorse cloud. Una risorsa può essere definita come calcolo hello e i costi di archiviazione.
* **Costo della metodologia DevOps**. facilità di Hello di sviluppo di applicazioni, distribuzione e gestibilità riduce costo complessivo di operazione SaaS.  

Nella figura 2 asse hello Y indica il livello di isolamento del tenant di hello. asse X Hello indica il livello hello di condivisione delle risorse. grigio Hello, freccia diagonale centro hello indica la direzione di hello dei costi DevOps, automatiche tooincrease o riduzione.

![Schemi progettuali comuni per le applicazioni multi-tenant](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Figura 2: Modelli di dati multi-tenant comuni

Hello quadrante in basso a destra nella figura 2 viene illustrato un modello di applicazione che utilizza un solo database potenzialmente di grandi dimensioni, condiviso e hello condiviso tabella (o schema separato) approccio. È utile per la condivisione perché tutti i tenant utilizzano hello stesso database delle risorse (CPU, memoria, input/output) in un singolo database delle risorse. L'isolamento dei tenant è tuttavia limitato. Potrebbe essere necessario tootake passaggi aggiuntivi tooprotect tenant da altra a livello di applicazione hello. Questi passaggi aggiuntivi consente di aumentare notevolmente il costo DevOps hello di sviluppo e la gestione di un'applicazione hello. La scalabilità è limitata dalla scala hello dell'hardware hello che ospita il database di hello.

quadrante in basso a sinistra di Hello nella figura 2 viene illustrata più tenant partizionati in più database (in genere, hardware diverse unità di scala). Ogni database che ospita un subset di tenant, che consente di risolvere problemi di scalabilità hello di altri modelli. Se è necessaria per più tenant maggiore capacità, è possibile inserire facilmente tenant hello nei nuovi database allocati le unità di scala toonew hardware. Tuttavia, viene ridotta quantità hello di condivisione delle risorse. Solo tenant inserita in hello stesso le unità di scala condividono le risorse. Questo approccio garantisce l'isolamento di tootenant miglioramento minimo perché molti tenant in cui vengono collocati ancora senza automaticamente protetti da azioni di altro. La complessità dell'applicazione rimane elevata.

quadrante superiore sinistro Hello nella figura 2 è terzo approccio hello. in cui i dati di ogni tenant vengono inseriti nel relativo database. Questo approccio offre adeguate proprietà di isolamento dei tenant ma riduce la condivisione delle risorse quando ogni database dispone di risorse dedicate. È l'approccio ideale quando tutti i tenant hanno carichi di lavoro prevedibili. Se i carichi di lavoro tenant sono meno prevedibili, provider hello non è possibile ottimizzare la condivisione delle risorse. L'imprevedibilità è comune per le applicazioni SaaS. provider Hello deve essere eccessivamente il provisioning di toomeet richieste o risorse inferiore. in entrambi i casi con maggiori costi o minore soddisfazione dei tenant. Un livello più elevato della risorsa di condivisione tra tenant diventa soluzione hello toomake auspicabile economicamente più vantaggiose. Numero crescente di hello dei database, inoltre, aumenta DevOps costo toodeploy e gestione un'applicazione hello. Nonostante queste problematiche, questo metodo offre hello migliore e più semplice l'isolamento dei tenant.

Questi fattori influiscono anche il modello di struttura hello che un cliente sceglie:

* **Proprietà dei dati dei tenant**. Un'applicazione in cui i tenant mantengono la proprietà dei propri dati Ottimizza per il modello di hello di un singolo database per ogni tenant.
* **Scalabilità**. in un'applicazione destinata a centinaia di migliaia o milioni di tenant viene preferito un approccio di condivisione, come il partizionamento orizzontale del database. I requisiti di isolamento possono tuttavia comportare problemi.
* **Modello aziendale e di valore**. se i ricavi per tenant di un'applicazione sono bassi (inferiori a un dollaro), i requisiti di isolamento diventano meno importanti e viene preferita la condivisione dei database. Se i ricavi per tenant sono maggiori, è più appropriato un modello di database per ogni tenant. Può essere utile a ridurre i costi di sviluppo.

Dato hello progettazione vantaggi e svantaggi illustrati nella figura 2, un modello multi-tenant ideale con, è necessario tooincorporate le proprietà di isolamento tenant buona ottimale condivisione delle risorse tra i tenant. Questo modello si adatta nella categoria hello descritta nella fase di hello angolo superiore destro della figura 2.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Supporto multi-tenancy con il database SQL di Azure
Il database SQL di Azure supporta tutti i modelli di applicazione multi-tenant illustrati dalla figura 2. Il pool elastico, supporta inoltre un modello di applicazione che combina la condivisione delle risorse valida e l'approccio di vantaggi isolamento hello di hello per tenant di database (vedere quadrante superiore destro di hello nella figura 3). Strumenti di database elastico e funzionalità in Database SQL consentono di ridurre toodevelop costo hello e il funzionamento di un'applicazione che dispone di molti database (visualizzati nell'area di hello ombreggiato nella figura 3). Questi strumenti consentono di creare e gestire le applicazioni che utilizzano uno qualsiasi dei modelli di multi-database hello.

![Modelli nel database SQL di Azure](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Figura 3: Modelli di applicazione multi-tenant nel database SQL di Azure

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Modello database per tenant con strumenti e pool elastici
Pool elastici nel Database SQL di combinare l'isolamento dei tenant con condivisione delle risorse tra approccio al tenant database toobetter supporto hello database per tenant. Il database SQL è una soluzione di livello dati destinata ai provider SaaS che realizzano applicazioni multi-tenant. carico Hello della condivisione delle risorse tra tenant passa dal livello di servizio database toohello livello applicazione hello. complessità Hello la gestione e l'esecuzione di query su larga scala tra database è stata semplificata con processi elastici, query elastico, transazioni elastiche e libreria client di database elastico hello.

| Requisiti dell'applicazione | Funzionalità del database SQL |
| --- | --- |
| Isolamento dei tenant e condivisione delle risorse |[Pool elastici](sql-database-elastic-pool.md): assegnazione di un pool di risorse del Database SQL e condividere le risorse di hello nei vari database. Inoltre, i singoli database possono disegnare tante risorse dal pool di hello come picchi di richiesta di capacità necessaria tooaccommodate scadenza toochanges nei carichi di lavoro tenant. i pool elastici Hello stesso può essere scalato verso l'alto o verso il basso in base alle esigenze. Anche i pool elastici fornire semplicità di gestione e monitoraggio e risoluzione dei problemi a livello di pool hello. |
| Facilità di DevOps tra i database |[Pool elastici:](sql-database-elastic-pool.md)come sopra. |
| | [Query elastica:](sql-database-elastic-query-horizontal-partitioning.md)la query viene eseguita tra database a scopo di creazione di report o l'analisi tra tenant. |
| | [I processi elastici](sql-database-elastic-jobs-overview.md): pacchetto e distribuire in modo affidabile le operazioni di manutenzione del database o database toomultiple di modifica dello schema del database. |
| | [Transazioni elastiche](sql-database-elastic-transactions-overview.md): processo di modifica di database tooseveral in modo atomico e isolato. Le transazioni elastiche sono necessarie quando le applicazioni richiedono garanzie di tipo "tutto o niente" su varie operazioni di database. |
| | [Libreria client di database elastico](sql-database-elastic-database-client-library.md): gestire le distribuzioni dei dati e mappa i tenant toodatabases. |

## <a name="shared-models"></a>Modelli condivisi
Come descritto in precedenza, per la maggior parte dei provider SaaS l'approccio con un modello condiviso può rappresentare un problema in termini di isolamento dei tenant, ma anche di complessità nello sviluppo e nella manutenzione delle applicazioni. Tuttavia, per le applicazioni multi-tenant che forniscono un servizio direttamente tenant tooconsumers, i requisiti di isolamento potrebbero non essere una priorità alta come come riduzione dei costi. Potrebbero essere in grado di toopack tenant in uno o più database un costi tooreduce ad alta densità. I modelli di database condivisi che usano un database singolo o più database partizionati possono offrire una maggiore efficienza in termini di condivisione delle risorse e riduzione del costo complessivo. Database SQL di Azure fornisce alcune funzionalità che consentono ai clienti di isolamento per una maggiore sicurezza e la gestione su larga scala nel livello dati hello compilazione.

| Requisiti dell'applicazione | Funzionalità del database SQL |
| --- | --- |
| Funzionalità di isolamento di sicurezza |[Sicurezza a livello di riga](https://msdn.microsoft.com/library/dn765131.aspx) |
| [Schema del database](https://msdn.microsoft.com/library/dd207005.aspx) | |
| Facilità di DevOps tra i database |[Query elastica](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Processi elastici](sql-database-elastic-jobs-overview.md) |
| | [Transazioni elastiche](sql-database-elastic-transactions-overview.md) |
| | [Libreria client dei database elastici](sql-database-elastic-database-client-library.md) |
| | [Divisione e unione dei database elastici](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Riepilogo
I requisiti di isolamento dei tenant sono importanti per la maggior parte delle applicazioni SaaS multi-tenant. isolamento di Hello migliore opzione tooprovide leans frequentemente verso l'approccio di database per tenant hello. Hello altri due approcci richiedono investimenti nei livelli applicazione complessa che richiedono l'isolamento tooprovide di competenze di sviluppo personale, aumentando in modo significativo i costi e i rischi. Se i requisiti di isolamento non vengono conteggiati nelle prime fasi di sviluppo del servizio hello, adattamento essi può essere ancora più costoso nei primi due modelli di hello. Hello svantaggi principali associati a modello di database per tenant hello sono correlati tooincreased costi delle risorse cloud a causa di tooreduced, condivisione e la gestione e la gestione di molti database. Gli sviluppatori di applicazioni SaaS incontrano spesso difficoltà a causa di questi compromessi.

Nonostante i compromessi potrebbero essere ostacoli principali con la maggior parte dei provider di servizi di database cloud, Database SQL di Azure Elimina barriere hello con il pool elastico e funzionalità di database elastico. Gli sviluppatori di SaaS possono combinare caratteristiche di isolamento hello di un modello di database per tenant e ottimizzare la risorsa di condivisione e hello miglioramenti della gestibilità di molti database utilizzando il pool elastico e strumenti associati.

I provider di applicazioni multi-tenant che non hanno requisiti di isolamento dei tenant e che possono inserirli in un database a densità elevata possono usare i modelli di dati condivisi per ottenere maggiore efficienza nella condivisione delle risorse e ridurre il costo complessivo. Gli strumenti di database elastici del database SQL di Azure, le librerie di partizionamento orizzontale e le funzionalità di sicurezza consentono ai provider SaaS di creare e gestire le applicazioni multi-tenant.

## <a name="next-steps"></a>Passaggi successivi
[Introduzione a strumenti di database elastico](sql-database-elastic-scale-get-started.md) con un'app di esempio che illustra la libreria client di hello.

Creare un [dashboard personalizzato del pool elastico per Saas](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) con un'applicazione di esempio che usa i pool elastici per una soluzione di database scalabile e conveniente.

Utilizzare gli strumenti di Database SQL di Azure di hello troppo[migrazione esistente tooscale database out](sql-database-elastic-convert-to-use-elastic-tools.md).

un pool elastico utilizzando toocreate hello Azure portale, vedere [creare un pool elastico](sql-database-elastic-pool-manage-portal.md).  

Informazioni su come troppo[monitorare e gestire un pool elastico](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* [Distribuire ed esplorare un'applicazione multi-tenant che usa il database SQL di Azure - Wingtip SaaS](sql-database-saas-tutorial.md)
* [Che cos'è un pool elastico di Azure?](sql-database-elastic-pool.md)
* [Aumento del numero di istanze con il database SQL di Azure](sql-database-elastic-scale-introduction.md)
* [Applicazioni multi-tenant con strumenti di database elastici e sicurezza a livello di riga](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Authentication in multitenant apps, using Azure Active Directory and OpenID Connect (Autenticazione in app multi-tenant con Azure Active Directory e OpenID Connect)](../guidance/guidance-multitenant-identity-authenticate.md)
* [Informazioni sull'applicazione Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Domande e richieste di funzionalità

Per domande, contattarci hello [forum di Database SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Aggiungere una richiesta di funzionalità in hello [forum sul feedback su Database SQL](https://feedback.azure.com/forums/217321-sql-database/).

