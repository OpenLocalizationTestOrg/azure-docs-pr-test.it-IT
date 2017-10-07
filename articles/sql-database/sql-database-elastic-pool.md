---
title: "aaaWhat sono pool elastico? Gestire più database SQL: Azure | Microsoft Docs"
description: "Gestire e ridimensionare centinaia o migliaia di database SQL usando i pool elastici. Un unico prezzo per le risorse che è possibile distribuire in base alle esigenze."
keywords: "più database, risorse di database, prestazioni di database"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: b46e7fdc-2238-4b3b-a944-8ab36c5bdb8e
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 07/31/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 2098d7817ebe1277b5c131421f23c00803ec78f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-pools-help-you-manage-and-scale-multiple-sql-databases"></a>Gestire e ridimensionare più database SQL usando i pool elastici

I pool elastici di database SQL offrono una soluzione semplice e conveniente per la gestione e il ridimensionamento di più database con esigenze di utilizzo variabili e imprevedibili. Hello e dei database in un pool elastico in un unico server di Database SQL di Azure condividono una serie di risorse ([unità di transazione di Database elastico](sql-database-what-is-a-dtu.md) (Edtu)) a un prezzo di set. Pool elastico in Database SQL di Azure abilitare SaaS sviluppatori toooptimize hello prezzo per un gruppo di database all'interno di un budget prescritto offrendo elasticità delle prestazioni per ogni database.   

> [!NOTE]
> I pool elastici sono disponibili a livello generale in tutte le aree di Azure tranne India occidentale, dove sono attualmente in anteprima.  I pool elastici verranno resi disponibili a livello generale in quest'area non appena possibile.
>

## <a name="what-are-sql-elastic-pools"></a>Definizione di pool elastici SQL 

Gli sviluppatori di SaaS compilano applicazioni basate su livelli di dati su larga scala costituiti da più database. Un modello di applicazione comune è tooprovision un singolo database per ogni cliente. Ma diversi clienti hanno spesso imprevedibili e diversi modelli di utilizzo ed è difficile toopredict requisiti di risorse hello di ogni utente di database singoli. In genere, le opzioni erano due: 

- Effettuare il provisioning di risorse eccessivo in base all'utilizzo massimo e pagare più del necessario, o
- Effettuare il provisioning in difetto toosave costi spese hello di soddisfazione dei clienti e delle prestazioni durante i picchi. 

Pool elastici risolvere questo problema, verificare che i database ottengono risorse hello per le prestazioni che necessarie in qualsiasi momento. Forniscono un meccanismo semplice di allocazione delle risorse che rientra in un budget prevedibile. toolearn ulteriori informazioni sui modelli di progettazione per le applicazioni SaaS con i pool elastici, vedere [modelli di progettazione per le applicazioni SaaS multi-tenant con Database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Elastic-databases-helps-SaaS-developers-tame-explosive-growth/player]
>

Pool elastici abilitare hello developer toopurchase [unità di transazione di Database elastico](sql-database-what-is-a-dtu.md) (Edtu) per un pool condiviso da più periodi imprevedibile in tooaccommodate i database di utilizzo dai singoli database. requisito di Hello eDTU per un pool è determinato dall'utilizzo di aggregazione hello dei relativi database. numero di Hello del pool disponibili toohello Edtu è controllato dal budget developer hello. sviluppatore Hello aggiunge semplicemente pool toohello database, imposta minimo hello e Edtu massimo per i database di hello e quindi imposta hello eDTU del pool di hello in base al loro budget. Uno sviluppatore può utilizzare pool tooseamlessly crescere proprio servizio da un'azienda collaudata tooa di avvio snella in scala crescente.

All'interno di hello, singoli database figurano hello flessibilità tooauto scala all'interno di impostare i parametri. In tal caso, un database può consumare ulteriori Edtu toomeet richiesta. Se invece il carico di lavoro è più leggero, i database in assenza di carico non utilizzano gli eDTU. Provisioning delle risorse per l'intero pool hello anziché per singoli database semplifica le attività di gestione. Inoltre, si dispone di un budget prevedibile per il pool di hello. Edtu aggiuntive possono essere aggiunti a un pool esistente di tooan senza tempi di inattività del database, ad eccezione del fatto che i database hello potrebbe essere necessario spostare toobe hello tooprovide ulteriore risorse per la nuova prenotazione di eDTU hello di calcolo. Analogamente, se gli eDTU aggiuntivi non sono più necessari, è possibile rimuoverli da un pool esistente in qualsiasi momento. Ed è possibile aggiungere o sottrarre pool toohello database. Se si prevede che un database sottoutilizzerà le proprie risorse, è possibile rimuoverlo.

È possibile creare e gestire un pool elastico utilizzando hello [portale di Azure](sql-database-elastic-pool-manage-portal.md), [PowerShell](sql-database-elastic-pool-manage-powershell.md), [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), [c#](sql-database-elastic-pool-manage-csharp.md), e hello API REST. 

## <a name="when-should-you-consider-a-sql-database-elastic-pool"></a>Quando considerare un pool elastico del database SQL

I pool sono adatti per un numero elevato di database con modelli di utilizzo specifici. Per un determinato database, questo modello è caratterizzato da un utilizzo medio ridotto con picchi di utilizzo relativamente poco frequenti.

Hello più database è possibile aggiungere hello pool tooa diventa il risparmio di spazio maggiore. A seconda del modello di utilizzo di applicazione è risparmi possibili toosee con appena due database S3.  

Hello nelle sezioni seguenti comprendere come tooassess se la raccolta di specifica di database può trarre vantaggio in un pool. esempi di Hello usano pool Standard ma hello stessi principi sono applicabili anche tooBasic e pool Premium.

### <a name="assessing-database-utilization-patterns"></a>Valutazione dei modelli di utilizzo di database

Hello figura riportata di seguito viene illustrato un esempio di un database che impiega molto tempo di inattività, ma anche periodicamente picchi di attività. Si tratta di un modello di utilizzo adatto per un pool:

   ![un database singolo adatto per un pool](./media/sql-database-elastic-pool/one-database.png)

Per hello illustrato intervallo di cinque minuti, DB1 picchi di Dtu too90, ma l'utilizzo medio complessivo è inferiore a cinque Dtu. Un S3 a livello di prestazioni è necessario toorun questo carico di lavoro in un singolo database, ma in questo modo la maggior parte delle risorse hello inutilizzati durante i periodi di minore attività.

Un pool consente questi toobe Dtu inutilizzati condiviso tra più database e quindi ridurre le spese di necessari e complessivo di Dtu hello.

Basandosi sull'esempio precedente hello, si supponga che vi sono ulteriori database con i modelli di utilizzo simili come DB1. In hello successivamente nelle due figure seguenti, l'utilizzo di quattro database di hello e 20 database sono disposti su hello stesso grafico natura non sovrapposti tooillustrate hello del relativo utilizzo nel tempo:

   ![quattro database con un modello di utilizzo adatto per un pool](./media/sql-database-elastic-pool/four-databases.png)

  ![venti database con un modello di utilizzo adatto per un pool](./media/sql-database-elastic-pool/twenty-databases.png)

utilizzo DTU aggregazione di Hello in tutti i database di 20 è illustrata dalla riga hello nero in hello nella figura precedente. Ciò indica che utilizzo DTU aggregazione hello mai supera 100 Dtu e indica che i database di 20 hello possono condividere 100 Edtu in questo periodo di tempo. Ciò comporta una riduzione di 20 x in Dtu e una 13 x prezzo riduzione confrontata tooplacing ogni database hello in livelli di prestazioni S3 per singoli database.

In questo esempio è ideale per hello seguenti motivi:

* Esistono grandi differenze tra i picchi di utilizzo e l'utilizzo medio per ogni database.  
* Hello picchi di utilizzo e per ogni database si verifica in diversi momenti nel tempo.
* Le eDTU vengono condivise tra più database.

prezzo Hello di un pool è una funzione di Edtu del pool hello. Mentre prezzo unitario di eDTU hello per un pool è 1,5 x maggiore del prezzo unitario DTU hello per un singolo database, **Edtu del pool può essere condiviso da molti database e sono necessari un minor numero di Edtu totale**. Queste distinzioni nella determinazione dei prezzi e la condivisione di eDTU si basano hello potenziale risparmio in termini di prezzo hello in grado di fornire i pool di.  

Hello seguenti regole correlate toodatabase count e database di utilizzo della Guida tooensure che offre un pool ridotto costi rispetto toousing i livelli di prestazioni per i singoli database.

### <a name="minimum-number-of-databases"></a>Numero minimo di database

Se più di 1,5 x Edtu hello necessari per il pool di hello somma hello di hello Dtu livelli di prestazioni per i singoli database, un pool elastico è più conveniente. Per le dimensioni disponibili, vedere [Limiti di archiviazione e di eDTU per i pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

***Esempio***<br>
Almeno due database S3 almeno 15 S0 database sono necessari o per un toobe pool 100 eDTU più economico rispetto all'utilizzo di livelli di prestazioni per singoli database.

### <a name="maximum-number-of-concurrently-peaking-databases"></a>Numero massimo di picco contemporaneamente database

Condividendo Edtu, non tutti i database in un pool possono utilizzare contemporaneamente Edtu backup limite toohello disponibili quando si usano livelli di prestazioni per singoli database. salve database meno picchi contemporaneamente, hello inferiore hello numero di eDTU pool può essere impostate e più conveniente hello pool diviene hello. In generale, non più di 2/3 (o % 67) dei database hello nel pool di hello deve picchi contemporaneamente tootheir eDTU limitare.

***Esempio***<br>
i costi tooreduce per tre database S3 in un pool di eDTU 200, al massimo due di questi database possono picchi contemporaneamente nella loro utilizzo. In caso contrario, se più di due di questi quattro database S3 picchi contemporaneamente, il pool di hello avrebbe toomore toobe dimensioni di finestra di 200 Edtu. Se il pool di hello è ridimensionato toomore di 200 Edtu, maggiore di database S3 sarebbe necessario toobe aggiunto toohello pool tookeep i costi inferiori a livelli di prestazioni per i singoli database.

Si noti in questo esempio non considera l'utilizzo di altri database nel pool di hello. Se tutti i database con alcune utilizzo in qualsiasi punto nel tempo, quindi minore di 2/3 (o % 67) dei database hello possibile picchi contemporaneamente.

### <a name="dtu-utilization-per-database"></a>Utilizzo di DTU per ogni database
Una notevole differenza tra l'utilizzo medio di un database e di picco hello indica periodi prolungati di basso utilizzo e brevi periodi di utilizzo elevato. Questo modello di utilizzo è ideale per la condivisione delle risorse tra database. Un database deve essere considerato per un pool quando relativo picchi di utilizzo sono circa 1.5 volte maggiore relativo utilizzo medio.

***Esempio***<br>
Un database di S3 picco too100 Dtu e medio Usa 67 Dtu o less è un buon candidato per la condivisione in un pool di Edtu. In alternativa, un database di S1 picco too20 Dtu e medio utilizza 13 Dtu o less è un buon candidato per un pool.

## <a name="how-do-i-choose-hello-correct-pool-size"></a>Modalità di dimensioni del pool corretto hello

dimensioni ottimali di Hello per un pool dipendono hello aggregazione Edtu e le risorse di archiviazione necessari per tutti i database nel pool di hello. Questo comporta la determinazione hello maggiore dei seguenti hello:

* Dtu massime utilizzate da tutti i database nel pool di hello.
* Byte di archiviazione massima utilizzati da tutti i database nel pool di hello.

Per le dimensioni disponibili, vedere [Limiti di archiviazione e di eDTU per i pool elastici e dei database elastici](#what-are-the-resource-limits-for-elastic-pools).

Database SQL viene valutata sull'utilizzo delle risorse cronologico hello dei database in un server di Database SQL esistente automaticamente e consiglia configurazione pool appropriato hello in hello portale di Azure. Raccomandazioni toohello addizione, un'esperienza incorporata Stima utilizzo di eDTU hello per un gruppo personalizzato di database nel server di hello. Ciò consente di toodo un "" analisi di simulazione, in modo interattivo aggiunta pool toohello database e la rimozione di analisi dell'utilizzo di risorse tooget e suggerimenti di ridimensionamento prima di eseguire il commit delle modifiche. Per le procedure, vedere [Monitorare e gestire un pool di database elastici con il portale di Azure](sql-database-elastic-pool-manage-portal.md).

In casi in cui non è possibile utilizzare gli strumenti seguenti hello dettagliate consentono di stimare se un pool è più conveniente rispetto ai database singoli:

1. Stimare Edtu hello necessari per il pool di hello come indicato di seguito:

   MAX (<*numero totale di database* X *utilizzo medio di DTU per DB*>,<br>
   <*numero di database in picco contemporaneamente* X *picco di utilizzo di DTU per DB*)
2. Stimare lo spazio di archiviazione hello necessario per il pool di hello aggiungendo hello numero di byte necessari per tutti i database nel pool di hello hello. Determinare quindi dimensioni del pool eDTU hello che fornisce la quantità di spazio di archiviazione. Per i limiti di archiviazione del pool in base alla dimensione del pool espressa in eDTU, vedere [Limiti di archiviazione e di eDTU dei pool elastici e dei database elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).
3. Richiedere hello più elevato tra le stime di eDTU hello del passaggio 1 e il passaggio 2.
4. Vedere hello [pagina prezzi del Database SQL](https://azure.microsoft.com/pricing/details/sql-database/) e trova hello più piccolo eDTU per pool dimensioni che è maggiore di stima hello dal passaggio 3.
5. Confrontare i prezzi pool hello dal passaggio 5 toohello prezzo dell'utilizzo di livelli di prestazioni appropriati hello per singoli database.

### <a name="changing-elastic-pool-resources"></a>Modifica delle risorse del pool elastico

È possibile aumentare o diminuire hello risorse disponibili tooan pool elastico in base alle esigenze di risorse.

* Modifica hello min Edtu per database o un numero massimo di Edtu per ogni database in genere viene completata entro 5 minuti o meno.
* Modifica hello Edtu per pool dipende dalla quantità totale di hello dello spazio utilizzato da tutti i database nel pool di hello. Le modifiche richiedono una media di 90 minuti o meno per 100 GB. Ad esempio, se lo spazio totale hello utilizzato da tutti i database nel pool di hello è 200 GB, quindi hello prevista latenza per la modifica hello pool eDTU per pool è 3 ore o minore.

## <a name="what-are-hello-resource-limits-for-elastic-pools"></a>Quali sono i limiti delle risorse per il pool elastico hello?

Hello le tabelle seguenti vengono descritti i limiti delle risorse hello del pool elastico.  Si noti che i limiti delle risorse hello di singoli database nel pool elastici sono in genere hello identico a quello di singoli database di fuori di pool in base alle Dtu e il livello di servizio hello.  Ad esempio, hello max simultanee processi di lavoro per un database di S2 è 120 thread di lavoro.  In tal caso, hello max simultanee processi di lavoro per un database in un pool Standard è anche 120 lavoratori se DTU massimo per ogni database nel pool di hello hello è 50 Dtu (ovvero tooS2 equivalente).

[!INCLUDE [SQL DB service tiers table for elastic pools](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Se vengono utilizzate tutti Dtu di un pool elastico, ogni database nel pool di hello riceve un'uguale quantità di query tooprocess risorse.  Hello servizio Database SQL fornisce l'equità tra database garantendo uguale intervalli di tempo di calcolo di condivisione delle risorse. Condivisione l'equità delle risorse di pool elastico sono inoltre tooany quantità di risorse in caso contrario è garantita tooeach database quando hello minimo DTU per database è impostato un valore diverso da zero tooa.

### <a name="database-properties-for-pooled-databases"></a>Proprietà del database per i database in pool

Hello nella tabella seguente vengono descritte le proprietà di hello per i database in pool.

| Proprietà | Descrizione |
|:--- |:--- |
| Numero massimo di eDTU per database |numero massimo di Hello di Edtu che può utilizzare qualsiasi database nel pool di hello, se disponibili in base all'utilizzo da altri database nel pool di hello.  Il numero massimo di eDTU per database non è una garanzia di risorse per un database.  Questa impostazione è un'impostazione globale che si applica tooall database nel pool di hello. Impostare max Edtu per database toohandle sufficientemente elevato picchi di utilizzo dei database. Un certo grado di overcommit previsto poiché pool hello è in genere si presuppone che di modelli di utilizzo e calda per i database in cui tutti i database sono non raggiungendo contemporaneamente. Si supponga ad esempio hello picchi di utilizzo e per ogni database sono 20 Edtu e solo il 20% dei database hello 100 nel pool di hello sono picco a hello contemporaneamente.  Se hello eDTU massimo per database è impostato too20 Edtu, è ragionevole tooovercommit pool di hello 5 volte e set hello Edtu per pool too400. |
| Numero minimo di eDTU per database |numero minimo di Hello di Edtu che qualsiasi database nel pool di hello è garantito.  Questa impostazione è un'impostazione globale che si applica tooall database nel pool di hello. Hello min eDTU per ogni database può essere impostato too0 ed è anche valore predefinito di hello. Questa proprietà è impostata tooanywhere compreso tra 0 e hello utilizzo di eDTU medio per ogni database. prodotto Hello del numero di hello di database nel pool di hello e hello min Edtu per database non può superare hello Edtu per ogni pool.  Se un pool è 20 database e hello minimo di eDTU per database impostato too10 Edtu, ad esempio, hello Edtu per pool deve essere grande almeno come 200 Edtu. |
| Spazio di archiviazione dati massimo per database |Hello massime di archiviazione per un database in un pool. In pool i database condividono lo spazio di archiviazione del pool, archiviazione del database è limitato toohello più piccolo di archiviazione pool rimanenti e di archiviazione massime per ogni database. Archiviazione massima per ogni database fa riferimento toohello dimensioni massime dei file di dati hello e non include hello lo spazio utilizzato dai file di log. |
|||

## <a name="using-other-sql-database-features-with-elastic-pools"></a>Uso di altre funzionalità del database SQL con i pool elastici

### <a name="elastic-jobs-and-elastic-pools"></a>Processi e pool elastici

L'uso di un pool permette di semplificare le attività di gestione con l'esecuzione di script in **[processi elastici](sql-database-elastic-jobs-overview.md)**. Un processo elastico elimina la maggior parte delle attività ripetitive associate a un elevato numero di database. toobegin, vedere [Guida introduttiva a processi elastici](sql-database-elastic-jobs-getting-started.md).

Per altre informazioni sugli altri strumenti di database per usare più database, vedere [Aumentare il numero di istanze con il database SQL di Azure](sql-database-elastic-scale-introduction.md).

### <a name="business-continuity-options-for-databases-in-an-elastic-pool"></a>Opzioni di continuità aziendale per i database in un pool elastico
In pool di database in genere supporto hello stesso [funzionalità di continuità aziendale](sql-database-business-continuity.md) che sono disponibili toosingle database.

- **Ripristino temporizzato**: punto nel tempo ripristino utilizza toorecover backup automatica del database un database in un momento specifico di pool tooa nel tempo. Vedere [Ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore)

- **Ripristino a livello geografico**: ripristino a livello geografico fornisce recovery-opzione predefinita hello quando un database non è disponibile a causa di un evento imprevisto nell'area di hello in cui è ospitato il database di hello. Vedere [ripristinare tooa un failover o di Database SQL di Azure secondario](sql-database-disaster-recovery.md)

- **Replica geografica attiva**: per le applicazioni che hanno requisiti di ripristino più elevati di quelli supportati dal ripristino geografico, configurare la [replica geografica attiva](sql-database-geo-replication-overview.md).

## <a name="manage-sql-database-elastic-pools-using-hello-azure-portal"></a>Gestire i pool di Database SQL elastico utilizzando hello portale di Azure

### <a name="creating-a-new-sql-database-elastic-pool-using-hello-azure-portal"></a>Creazione di un nuovo pool elastico a Database SQL usando hello portale di Azure

Esistono due modi per creare un pool elastico in hello portale di Azure. È possibile farlo da zero se si conosce il programma di installazione di hello pool desiderato oppure iniziare con un suggerimento dal servizio hello. Database SQL prevede intelligence predefinite in cui si consiglia l'installazione di un pool elastico, se è più conveniente in base alle hello oltre telemetria per i database. 

Creazione di un pool elastico da un oggetto esistente **server** pannello nel portale di hello è hello più semplice modo toomove database esistenti in un pool elastico. È inoltre possibile creare un pool elastico eseguendo una ricerca **pool elastico SQL** in hello **Marketplace** o facendo clic su **+ Aggiungi** in hello **pool elastico SQL**Sfoglia blade. Si è in grado di toospecify un server nuovo o esistente tramite il provisioning del flusso di lavoro del pool.

> [!NOTE]
> È possibile creare più pool su un server, ma non è possibile aggiungere i database da server diversi in hello stesso pool.
>  

Hello piano tariffario del pool determina hello funzionalità elastics toohello disponibile nel pool di hello e hello il numero massimo di Edtu (numero massimo di eDTU) e spazio di archiviazione (GB) disponibile tooeach database. Per altre informazioni, vedere [Livelli di servizio](#edtu-and-storage-limits-for-elastic-pools).

Fare clic su toochange hello piano tariffario per il pool di hello **tariffario**, fare clic su hello tariffario desiderato e quindi fare clic su **selezionare**.

> [!IMPORTANT]
> Dopo aver scelto hello a livello di prezzo e confermare le modifiche facendo clic **OK** nell'ultimo passaggio hello, non sarà in grado di toochange hello piano tariffario del pool di hello. toochange hello piano tariffario per un pool elastico esistente, creare un pool elastico piano tariffario desiderato hello ed eseguire la migrazione hello database toothis nuovo pool.
>

Se si lavora con i database di hello dispongono di dati di telemetria sufficienti all'utilizzo storico, hello **stimato eDTU e GB utilizzo** grafico e hello **utilizzo di eDTU effettivo** grafico a barre toohelp di aggiornamento della configurazione decisioni. Inoltre, servizio hello può fornire un toohelp di messaggi di raccomandazioni per le dimensioni appropriate hello pool.

Hello servizio Database SQL valuta la cronologia di utilizzo e propone di uno o più pool quando è più conveniente rispetto all'uso di singoli database. Ogni raccomandazione è configurato con un subset di database del server hello che meglio si adattano pool hello univoco.

![pool consigliato](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

indicazione di pool Hello è costituito da:

- Un piano tariffario per il pool di hello (Basic, Standard, Premium o Premium RS)
- **eDTU POOL** appropriato, detto anche eDTU max per pool.
- Hello **eDTU MAX** e **Min eDTU** per ogni database
- elenco di Hello di database consigliati per il pool di hello

> [!IMPORTANT]
> servizio Hello considerando hello ultimi 30 giorni di dati di telemetria quando consigliando pool. Per un toobe database considerato un candidato valido per un pool elastico, deve esistere per almeno sette giorni. I database che si trovano già in pool elastici non vengono considerati come possibili candidati, in linea con i consigli relativi ai pool elastici.
>

servizio Hello valuta le risorse necessarie ed economicità di hello mobile singolo database in ogni livello di servizio nel pool di hello stesso livello. Ad esempio, vengono valutati tutti i database Standard in un server per l’utilizzo in un pool elastico Standard. Ciò significa servizio hello non indicazioni tra livelli, ad esempio lo spostamento di un database Standard in un pool Premium.

Dopo l'aggiunta di pool di database toohello, indicazioni generate dinamicamente in base all'utilizzo storico hello dei database hello che è stato selezionato. Questi suggerimenti vengono visualizzati nel hello eDTU e GB del grafico di utilizzo in un banner di raccomandazione nella parte superiore di hello di hello **configurare pool** blade. Queste raccomandazioni sono tooassist desiderato è la creazione di un pool elastico ottimizzato per i database specifici.

![Indicazioni dinamiche](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

### <a name="manage-and-monitor-an-elastic-pool"></a>Gestire e monitorare un pool elastico

Nel portale di Azure hello, è possibile monitorare l'utilizzo di un pool elastico e il database di hello all'interno di tale pool hello. È possibile creare un set di modifiche pool elastico tooyour e inviare tutte le modifiche in hello stesso tempo. Le modifiche includono l'aggiunta o la rimozione di database, la modifica delle impostazioni del pool elastico o la modifica delle impostazioni del database.

Hello seguente grafico mostra un pool elastico di esempio. visualizzazione di Hello include:

*  Grafici per il monitoraggio dell'utilizzo delle risorse del pool elastico hello sia i database hello contenuti nel pool di hello.
*  Hello **configura** toomake pulsante pool Cambia pool elastico toohello.
*  Hello **Crea database** pulsante che consente di creare un database e lo aggiunge pool elastico corrente toohello.
*  Processi elastici che consentono di gestire un numero elevato di database tramite l'esecuzione di script Transact SQL in tutti i database in un elenco.

![Visualizzazione del pool](./media/sql-database-elastic-pool-manage-portal/basic.png)

È possibile passare tooa pool specifico toosee il relativo utilizzo delle risorse. Per impostazione predefinita, il pool di hello è tooshow configurato sull'utilizzo di archiviazione e di eDTU per hello ultima ora. grafico Hello può essere configurato tooshow metriche su diversi intervalli di tempo. Fare clic su hello **utilizzo delle risorse** del grafico in **monitoraggio pool elastico** tooshow una visualizzazione dettagliata di hello specificati metriche su finestra temporale specificata hello.

![Monitoraggio di pool elastici](./media/sql-database-elastic-pool-manage-portal/basic-2.png)

![Blade delle metriche](./media/sql-database-elastic-pool-manage-portal/metric.png)

### <a name="toocustomize-hello-chart-display"></a>visualizzazione del grafico hello toocustomize

È possibile modificare il grafico hello e hello blade metriche toodisplay altre metriche quali Percentuale CPU, percentuale dei / o di dati e percentuale dei / o di log utilizzata.

![Fare clic su Modifica](./media/sql-database-elastic-pool-manage-portal/edit-metric.png)

In hello **Modifica grafico** modulo, è possibile selezionare un intervallo di tempo (passati oggi, ora o settimana precedente) o fare clic su **personalizzato** tooselect qualsiasi data intervallo hello ultime due settimane. È possibile scegliere tra una barra o un grafico a linee e quindi selezionare toomonitor risorse hello.

> [!Note]
> Solo le metriche con hello stessa unità di misura possono essere visualizzati in hello del grafico in hello stesso tempo. Ad esempio, se si seleziona "percentuale di eDTU" quindi è possibile solo selezionare altre metriche percentuale come unità di misura di hello.
>

[Fare clic su Modifica](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

### <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gestire e monitorare database in un pool elastico

È possibile monitorare anche i singoli database per potenziali problemi. In **Monitoraggio database elastico**è disponibile un grafico che mostra le metriche relative a cinque database. Per impostazione predefinita, hello il grafico visualizza hello primi 5 database nel pool di hello per utilizzo di eDTU medio in hello ora precedente. 

![Monitoraggio di pool elastici](./media/sql-database-elastic-pool-manage-portal/basic-3.png)

Fare clic su hello **utilizzo di eDTU per database per hello ora precedente** in **monitoraggio di database elastico**. Verrà visualizzata **utilizzo delle risorse di Database** e offre una visualizzazione dettagliata di utilizzo del database nel pool di hello hello. Griglia hello nella parte inferiore di hello del pannello hello, è possibile selezionare tutti i database in hello pool toodisplay il relativo utilizzo in grafico hello (backup dei database too5). È inoltre possibile personalizzare finestra metrica e l'ora visualizzata nel grafico hello facendo clic, hello **Modifica grafico**.

![Pannello Utilizzo risorse database](./media/sql-database-elastic-pool-manage-portal/db-utilization.png)

### <a name="toocustomize-hello-view"></a>visualizzazione di hello toocustomize

È possibile modificare hello grafico tooselect un intervallo di tempo (passati ora o ultime 24 ore) o fare clic su **personalizzato** tooselect un giorno diverso in hello oltre toodisplay 2 settimane.

![Fare clic su Modifica grafico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

![Fare clic su personalizzato](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

È anche possibile fare clic su hello **confronto dei database da** tooselect elenco a discesa un toouse metrica diversi durante il confronto dei database.

![Modifica grafico hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect database toomonitor

Nell'elenco di database hello in hello **utilizzo delle risorse di Database** pannello, è possibile trovare determinati database, verificare tramite pagine hello nell'elenco di hello o immettere il nome di un database hello. Utilizzare hello casella di controllo tooselect hello database.

![Ricerca per i database toomonitor](./media/sql-database-elastic-pool-manage-portal/select-dbs.png)


### <a name="add-an-alert-tooan-elastic-pool-resource"></a>Aggiungere una risorsa del pool elastico tooan avviso

È possibile aggiungere regole tooan pool elastico che inviano gli endpoint tooURL stringhe toopeople o un avviso di posta elettronica quando il pool elastico hello raggiunga una soglia di utilizzo impostato.

**una risorsa tooany avviso tooadd:**

1. Fare clic su hello **utilizzo delle risorse** hello tooopen grafico **metrica** pannello, fare clic su **Aggiungi avviso**e quindi immettere le informazioni di hello in hello **aggiungere un avviso regola** blade (**risorse** viene impostata automaticamente pool hello toobe si lavora con).
2. Digitare un **nome** e **descrizione** che identifica tooyou avviso hello e destinatari hello.
3. Scegliere un **metrica** che si desidera tooalert dall'elenco di hello.

    Hello dinamicamente Mostra utilizzo delle risorse per tale metrica toohelp che si sceglie una soglia.

4. Scegliere una **Condizione**, ad esempio maggiore di, minore di e così via, e una **Soglia**.
5. Scegliere un **periodo** di tempo che hello metrica regola deve essere soddisfatti prima di allarmi hello.
6. Fare clic su **OK**.

Per altre informazioni, vedere [Usare il portale di Azure per creare avvisi per il database SQL di Azure](sql-database-insights-alerts-portal.md).

### <a name="move-a-database-into-an-elastic-pool"></a>Spostare un database in un pool elastico

È possibile aggiungere o rimuovere i database da un pool esistente. database Hello possono trovarsi in altri pool. Tuttavia, è possibile aggiungere solo i database che sono su hello stesso server logico.

 ![Fare clic su Configura pool](./media/sql-database-elastic-pool-manage-portal/configure-pool.png)

![Fare clic su Aggiungi toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)

![Selezione database tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

![Aggiunte di pool in sospeso](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="move-a-database-out-of-an-elastic-pool"></a>Spostare un database da un pool elastico

![elenchi di database](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

![elenchi di database](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

![anteprima aggiunta e rimozione database](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

### <a name="change-performance-settings-of-an-elastic-pool"></a>Modificare le impostazioni delle prestazioni di un pool elastico

Durante il monitoraggio di utilizzo delle risorse di hello di un pool elastico, si potrebbe scoprire che sono necessarie alcune modifiche. Forse pool hello richiede una modifica nei limiti di archiviazione o di prestazioni hello. Probabilmente si desidera toochange impostazioni hello nel pool di hello. È possibile modificare il programma di installazione di hello del pool di hello in qualsiasi momento tooget hello migliore bilanciamento delle prestazioni e costi. Per altre informazioni, vedere [Quando usare un pool elastico](sql-database-elastic-pool.md).

toochange hello Edtu o archiviazione di limiti per ogni pool e di Edtu per database:

![Utilizzo delle risorse del pool elastico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

![Aggiornamento di un pool elastico e nuovi costi mensili](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="manage-sql-database-elastic-pools-using-powershell"></a>Gestire i pool elastici del database SQL tramite PowerShell

toocreate e gestire pool elastico del Database SQL con Azure PowerShell, usare i cmdlet di PowerShell seguente hello. Se è necessario tooinstall o l'aggiornamento di PowerShell, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps). toocreate e gestire i database, server e le regole firewall, vedere [creare e gestire i server di Database SQL di Azure e database tramite PowerShell](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-powershell). 

> [!TIP]
> Per gli script di esempio di PowerShell, vedere [creare pool elastico e spostare database tra i pool e all'esterno di un pool con PowerShell](scripts/sql-database-move-database-between-pools-powershell.md) e [toomonitor usare PowerShell e la scala pool elastici un SQL nel Database di SQL Azure](scripts/sql-database-monitor-and-scale-pool-powershell.md).
>

| Cmdlet | Descrizione |
| --- | --- |
|[New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool)|Consente di creare un pool di database elastico all'interno del server SQL logico.|
|[Get-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/get-azurermsqlelasticpool)|Consente di ottenere pool elastici e i relativi valori di proprietà in un server SQL logico.|
|[Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool)|Consente di modificare le proprietà di un pool di database elastico all'interno del server SQL logico.|
|[Remove-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/remove-azurermsqlelasticpool)|Consente di eliminare un pool di database elastico all'interno del server SQL logico.|
|[Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity)|Ottiene lo stato di hello delle operazioni in un pool elastico in un server SQL logico.|
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Consente di creare un nuovo database in un pool esistente o in un database singolo. |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Ottiene uno o più database.|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Consente di impostare le proprietà per un database oppure sposta un database esistente all'interno o all'esterno di in un pool elastico.|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Rimuove un database.|

> [!TIP]
> Creazione di molti database in un pool elastico può richiedere tempo al termine della hello portale o i cmdlet di PowerShell che creano solo un singolo database alla volta. creazione di tooautomate in un pool elastico, vedere [CreateOrUpdateElasticPoolAndPopulate](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).
>

## <a name="manage-sql-database-elastic-pools-using-hello-azure-cli"></a>Gestire i pool di Database SQL elastico utilizzando hello CLI di Azure

toocreate e gestire pool elastico del Database SQL con hello [CLI di Azure](/cli/azure/overview), utilizzare la seguente hello [Database SQL di Azure CLI](/cli/azure/sql/db) comandi. Hello utilizzare [Shell Cloud](/azure/cloud-shell/overview) toorun hello CLI nel browser o [installare](/cli/azure/install-azure-cli) sul macOS, Linux o Windows. 

> [!TIP]
> Per gli script di esempio CLI di Azure, vedere [toomove CLI di utilizzare un database SQL di Azure in un pool elastico SQL](scripts/sql-database-move-database-between-pools-cli.md) e [tooscale CLI di Azure Usa un pool elastico SQL nel Database di SQL Azure](scripts/sql-database-scale-pool-cli.md).
>

| Cmdlet | Descrizione |
| --- | --- |
|[az sql elastic-pool create](/cli/azure/sql/elastic-pool#create)|Consente di creare un pool elastico.|
|[az sql elastic-pool list](/cli/azure/sql/elastic-pool#list)|Restituisce un elenco di pool elastici in un server.|
|[az sql elastic-pool list-dbs](/cli/azure/sql/elastic-pool#list-dbs)|Restituisce un elenco di database in un pool elastico.|
|[az sql elastic-pool list-editions](/cli/azure/sql/elastic-pool#list-editions)|Include anche le impostazioni di DTU del pool disponibile, i limiti di archiviazione e per le impostazioni per ogni database. Nel livello di dettaglio tooreduce ordine, i limiti di spazio di archiviazione aggiuntivo e per ogni database impostazioni sono nascosti per impostazione predefinita.|
|[az sql elastic-pool update](/cli/azure/sql/elastic-pool#update)|Consente di aggiornare un pool elastico.|
|[az sql elastic-pool delete](/cli/azure/sql/elastic-pool#delete)|Elimina pool elastico hello.|

## <a name="manage-sql-database-elastic-pools-using-transact-sql"></a>Gestire i pool elastici del database SQL con Transact-SQL

database toocreate e spostamento all'interno di pool elastico esistente o tooreturn informazioni per un pool elastico SQL Database con Transact-SQL, utilizzare hello comandi T-SQL seguente. È possibile eseguire questi comandi utilizzando il portale di Azure, hello [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [codice di Visual Studio](https://code.visualstudio.com/docs), o qualsiasi altro programma che è possibile connettere il server di Database SQL di Azure tooan e passare a Transact-SQL comandi. toocreate e gestire i database, server e le regole firewall, vedere [creare e gestire i server di Database SQL di Azure e i database utilizzando Transact-SQL](sql-database-servers-databases.md#manage-azure-sql-servers-databases-and-firewalls-using-transact-sql).

> [!IMPORTANT]
> Non è possibile creare, aggiornare o eliminare un pool elastico del database SQL di Azure con Transact-SQL. È possibile aggiungere o rimuovere i database da un pool elastico ed è possibile utilizzare viste a gestione dinamica tooreturn informazioni sui pool elastico esistente.
>

| Comando | Descrizione |
| --- | --- |
|[CREATE DATABASE (database SQL di Azure)](/sql/t-sql/statements/create-database-azure-sql-database)|Consente di creare un nuovo database in un pool esistente o in un database singolo. È necessario essere connessi toohello database master toocreate un nuovo database.|
| [ALTER DATABASE (database SQL di Azure)](/sql/t-sql/statements/alter-database-azure-sql-database) |Consente di spostare un database all'interno, all'esterno o tra pool elastici.|
|[DROP DATABASE (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Questo comando elimina un database.|
|[sys.elastic_pool_resource_stats (Database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-elastic-pool-resource-stats-azure-sql-database)|Restituisce statistiche di utilizzo delle risorse per tutti i pool di database elastico hello in un server logico. Per ogni pool di database elastico c'è una riga per ogni finestra di report di 15 secondi, quattro righe per ogni minuto. Sono inclusi CPU, IO, Log, il consumo di archiviazione e utilizzo/sessione di richieste simultanee da tutti i database nel pool di hello.|
|[sys.database_service_objectives (database SQL di Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Restituisce hello edizione (livello di servizio), l'obiettivo di servizio (livello di prezzo) e nome del pool elastico, se presente, per un database SQL di Azure o un Data Warehouse di SQL Azure. Se connesso al database master di toohello in un server di Database SQL di Azure, restituisce informazioni su tutti i database. Per Azure SQL Data Warehouse, è necessario essere connessi toohello database master.|

## <a name="manage-sql-database-elastic-pools-using-hello-rest-api"></a>Gestire pool elastici di Database SQL tramite l'API REST hello

toocreate e gestire i pool elastici di Database SQL tramite hello API REST, vedere [API REST di Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Passaggi successivi

* Un video è disponibile in [Esercitazione video di Microsoft Virtual Academy sulle funzionalità di elasticità del database SQL di Azure](https://mva.microsoft.com/training-courses/elastic-database-capabilities-with-azure-sql-db-16554)
* toolearn ulteriori informazioni sui modelli di progettazione per le applicazioni SaaS con i pool elastici, vedere [modelli di progettazione per le applicazioni SaaS multi-tenant con Database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).
* Per un'esercitazione SaaS con i pool elastici, vedere [toohello introduzione applicazione SaaS Wingtip](sql-database-wtp-overview.md).
