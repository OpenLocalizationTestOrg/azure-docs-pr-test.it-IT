---
title: prestazioni aaaMonitor di molti database SQL di Azure in un'applicazione SaaS multi-tenant | Documenti Microsoft
description: Monitorare e gestire le prestazioni di database e i pool di app di Azure SQL Database Wingtip SaaS hello
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Monitorare le prestazioni dell'applicazione SaaS Wingtip hello

In questa esercitazione vengono illustrati diversi scenari di gestione delle prestazioni chiave usati nelle applicazioni SaaS. Usa un'attività di toosimulate generatore di carico in tutti i database tenant, vengono illustrate funzionalità di monitoraggio incorporate hello e le funzionalità di avvisi di Database SQL e i pool elastici.

app SaaS Wingtip Hello utilizza un modello di dati single-tenant, in cui per ogni sessione (tenant) ha il proprio database. Come molte applicazioni SaaS, hello previsto modello di carico di lavoro tenant è imprevedibile e sporadico. In altre parole, le vendite di biglietti possono verificarsi in qualsiasi momento. tootake vantaggio di questo modello di utilizzo tipico di database, i database vengono distribuiti nel pool di database elastici tenant. Pool elastici ottimizzare costi hello di una soluzione di condivisione risorse tra più database. Con questo tipo di modello, è importante toomonitor database e tooensure di utilizzo di risorse del pool che carica ragionevolmente sono bilanciati da una serie. È inoltre necessario tooensure che singoli database dispongano risorse adeguate, e che i pool non raggiunge le [eDTU](sql-database-what-is-a-dtu.md) limiti. In questa esercitazione vengono illustrati modi toomonitor e gestire database e i pool e come tootake azione correttiva in risposta toovariations nel carico di lavoro.

In questa esercitazione si apprenderà come:

> [!div class="checklist"]

> * Simulare l'utilizzo nel database tenant hello eseguendo un generatore di carico specificato
> * I database tenant hello Monitor come rispondono toohello aumento del carico
> * Applicare la scalabilità verticale hello pool elastico nel caricamento del database maggiore toohello risposta
> * Eseguire il provisioning di una seconda attività di database di saldo tooload pool elastico


toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toosaas-performance-management-patterns"></a>Modelli di gestione delle prestazioni tooSaaS introduzione

La gestione delle prestazioni del database consiste di compilazione e l'analisi dei dati delle prestazioni e quindi reazione toothis dati modificando i parametri toomaintain tempi di risposta accettabili per l'applicazione. Quando si ospitano più tenant, pool di database elastici sono tooprovide un modo economico e gestire le risorse per un gruppo di database con carichi di lavoro imprevedibile. Con determinati modelli di carico di lavoro, anche solo due database S3 possono trarre vantaggio dalla gestione in un pool.

![diagramma](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

I pool e dei database hello in pool, devono essere monitorato tooensure rimangono all'interno di intervalli accettabili di prestazioni. Ottimizzare hello pool toomeet hello esigenze di configurazione del carico di aggregazione hello di tutti i database, garantendo che siano appropriate per hello hello Edtu del pool di carico di lavoro complessivo. Regola hello per ogni database min e per ogni database eDTU max valori tooappropriate i valori per i requisiti specifici dell'applicazione.

### <a name="performance-management-strategies"></a>Strategie per la gestione delle prestazioni

* tooavoid con toomanually monitoraggio delle prestazioni, è più efficace troppo**impostare gli avvisi che attivano quando i database o i pool Cometa fuori intervalli normali**.
* le fluttuazioni tooshort termine toorespond hello aggregazione livello di prestazioni di un pool di hello **livello di eDTU del pool può essere scalata verso l'alto o verso il basso**. Se si verifica a intervalli regolari o prevedibili, questo fluttuazione **ridimensionamento pool hello può essere pianificato toooccur automaticamente**. Ad esempio, ridurre il numero di eDTU quando il carico di lavoro è notoriamente leggero, ad esempio durante la notte o nei fine settimana.
* numero di database, di hello fluttuazioni toolonger termine toorespond o modifiche in **singoli database possono essere spostati in altri pool**.
* termine tooshort toorespond un aumento *singoli* caricamento del database **singoli database possono essere eseguiti da un pool e assegnati un livello di prestazioni singoli**. Una volta che viene ridotto carico hello, database hello può quindi essere restituito toohello pool. Quando è noto in anticipo, database possono essere spostati preventivamente tooensure hello database sono sempre inclusi hello risorse che necessarie e tooavoid impatto su altri database nel pool di hello. Se questo requisito è stimabile, ad esempio un evento che ha rilevato un urgente di vendite ticket per un evento comune, questo comportamento di gestione può essere integrato in un'applicazione hello.

Hello [portale di Azure](https://portal.azure.com) fornisce avvisi nella maggior parte delle risorse e monitoraggio incorporati. Per il database SQL, il monitoraggio e gli avvisi sono disponibili per database e pool. Questo incorporati di monitoraggio e avviso sono specifici delle risorse, pertanto è comodo toouse per un numero limitato di risorse, ma non è molto utile quando si utilizzano molte risorse.

Per gli scenari con volumi elevati in cui si lavora con molte risorse, si può usare [Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md). Si tratta di un servizio di Azure separato che fornisce funzionalità di analisi per log di diagnostica e dati di telemetria raccolti in un'area di lavoro di Log Analytics. Log Analitica possibile raccogliere dati di telemetria da diversi servizi e tooquery utilizzato e impostare gli avvisi.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Ottenere gli script e codice sorgente dell'applicazione hello Wingtip

Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. [I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Eseguire il provisioning di altri tenant

I pool possono essere conveniente con due database S3, hello più database che si trovano in hello pool hello più economica hello Media effettiva diventa. Per comprendere meglio il funzionamento della gestione e del monitoraggio delle prestazioni su larga scala, per questa esercitazione è necessario distribuire almeno 20 database.

Se già stato eseguito il provisioning un batch di tenant in un'esercitazione precedente, ignorare toohello [simulare l'utilizzo in tutti i database tenant](#simulate-usage-on-all-tenant-databases) sezione.

1. Apri... \\Moduli learning\\gestione e monitoraggio delle prestazioni\\*Demo PerformanceMonitoringAndManagement.ps1* in hello *PowerShell ISE*. Mantenere lo script aperto durante l'esecuzione dei vari scenari presentati in questa esercitazione.
1. Impostare **$DemoScenario** = **1**, **Effettuare il provisioning di un batch di tenant**
1. Premere **F5** script hello toorun.

script Hello distribuirà 17 tenant in meno di cinque minuti.

Hello *New TenantBatch* script utilizza un set di nidificata o collegato [Gestione risorse](../azure-resource-manager/index.md) modelli per la creazione di un batch di tenant, che per impostazione predefinita consente di copiare database hello **basetenantdb** hello catalogo server toocreate hello nuovo database tenant, quindi viene registrata nel catalogo di hello e infine li inizializza con il tipo di nome e la sede tenant hello. Ciò è coerente con la modalità di hello hello app esegue il provisioning di un nuovo tenant. Tutte le modifiche apportate troppo*basetenantdb* vengono applicati tooany stato successivamente eseguito il provisioning di nuovi tenant. Vedere hello [esercitazione la gestione dello Schema](sql-database-saas-tutorial-schema-management.md) toosee come schema toomake cambia troppo*esistente* tenant database (inclusi hello *basetenantdb* database).

## <a name="simulate-usage-on-all-tenant-databases"></a>Simulare l'utilizzo in tutti i database tenant

Hello *Demo PerformanceMonitoringAndManagement.ps1* script viene specificato che simula un carico di lavoro in esecuzione su tutti i database tenant. carico Hello viene generato utilizzando uno degli scenari di hello carico disponibili:

| Demo | Scenario |
|:--|:--|
| 2 | Generare un carico di intensità normale (circa 40 DTU) |
| 3 | Generare un carico con picchi più lunghi e più frequenti per ogni database|
| 4 | Generare un carico con picchi DTU maggiori per ogni database (circa 80 DTU)|
| 5 | Generare un carico normale e un carico elevato in un singolo tenant (circa 95 DTU)|
| 6 | Generare un carico non bilanciato su più pool|

Generatore di carico Hello si applica un *sintetica* database tenant tooevery di carico solo della CPU. Generatore di Hello avvia un processo per ogni database tenant, che chiama periodicamente una stored procedure che genera l'errore carico hello. all'interno di intervalli, la durata e livelli di carico hello (in Edtu) in tutti i database, simulando attività tenant imprevedibile.

1. Apri... \\Moduli learning\\gestione e monitoraggio delle prestazioni\\*Demo PerformanceMonitoringAndManagement.ps1* in hello *PowerShell ISE*. Mantenere lo script aperto durante l'esecuzione dei vari scenari presentati in questa esercitazione.
1. Impostare **$DemoScenario** = **2**, *Generare un carico di intensità normale*.
1. Premere **F5** tooapply tooall un carico ai database tenant.

Wingtip è un'applicazione SaaS e carico di lavoro reale hello in un'app SaaS è in genere sporadici e imprevedibili. toosimulate questo hello carico generatore genera un carico casuale distribuito tra tutti i tenant. Hello carico modello tooemerge, eseguire il generatore di carico hello per 3-5 minuti prima di tentare il carico di hello toomonitor in hello le sezioni seguenti sono necessari alcuni minuti.

> [!IMPORTANT]
> Generatore di carico Hello è in esecuzione come una serie di processi nella sessione di PowerShell locale. Mantenere hello *Demo PerformanceMonitoringAndManagement.ps1* scheda aperta. Se si chiude la scheda hello o sospende la macchina, il generatore di carico hello arresta. Generatore di carico Hello rimane in un *chiamata processo* stato in cui genera carico eventuali nuovi tenant sottoposti a provisioning dopo l'avvio del generatore di hello. Utilizzare *Ctrl-C* toostop il richiamo di nuovi processi e script di uscita hello. Generatore di carico Hello continuerà toorun, ma solo per i tenant esistenti.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Monitorare l'utilizzo di risorse utilizzando hello portale di Azure

utilizzo delle risorse di hello toomonitor risultati hello caricare viene applicato, aprire il pool di portale toohello hello che contiene i database tenant hello:

1. Aprire hello [portale di Azure](https://portal.azure.com) ed esplorare toohello *tenants1 -&lt;utente&gt;*  server.
1. Scorrere verso il basso e individuare i pool elastici, quindi fare clic su **Pool1**. Questo pool contiene tutti i database di tenant hello creati finora.

Osservare hello **monitoraggio pool elastico** e **monitoraggio di database elastico** grafici.

Hello utilizzo delle risorse del pool è hello utilizzo di database di aggregazione per tutti i database nel pool di hello. Hello database Mostra hello cinque database interessanti:

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Poiché sono presenti altri database nel pool di hello oltre hello primi cinque, utilizzo pool hello Mostra l'attività che non vengono riportate nel grafico di hello primi cinque database. Per altri dettagli, fare clic su **Utilizzo risorse database**:

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Impostare avvisi sulle prestazioni nel pool di hello

Impostare un avviso per il pool hello che attiva \>75% l'utilizzo come indicato di seguito:

1. Aprire *Pool1* (su hello *tenants1 -\<utente\>*  server) in hello [portale di Azure](https://portal.azure.com).
1. Fare clic su **Regole di avviso** e quindi fare clic su **+ Aggiungi avviso**:

   ![aggiungere un avviso](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Specificare un nome, ad esempio **DTU elevate**.
1. Impostare hello seguenti valori:
   * **Metrica = Percentuale eDTU**
   * **Condizione = maggiore di** .
   * **Soglia = 75**.
   * **Periodo = su hello ultimi 30 minuti**.
1. Aggiungere un toohello indirizzo di posta elettronica *amministratore aggiuntive email(s)* casella e fare clic su **OK**.

   ![impostare l'avviso](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Potenziare un pool con carico eccessivo

Se il livello di carico di aggregazione hello aumenta in un punto di toohello pool che potenzia pool hello e viene raggiunto il 100% eDTU, quindi le prestazioni dei singoli database è interessato, potenzialmente rallentare i tempi di risposta delle query per tutti i database nel pool di hello.

**A breve termine**, prendere in considerazione l'aumento di risorse aggiuntive di hello pool tooprovide o rimozione di database dal pool hello (spostarli tooother pool, o all'esterno di livello di servizio autonomo hello pool tooa).

**Lungo termine**, prendere in considerazione l'ottimizzazione delle query o un indice delle prestazioni del database tooimprove utilizzo. A seconda di hello tooperformance sensibilità dell'applicazione emette relativo tooscale prassi migliori un pool di backup prima di raggiungere l'utilizzo di eDTU 100%. Utilizzare un avviso toowarn è in anticipo.

È possibile simulare un pool occupato dall'incremento del carico hello prodotta dal generatore di hello. Senza modificare i requisiti di hello di singoli database hello, causando hello database tooburst più di frequente e per il carico di aggregazione hello più lungo, incremento nel pool di hello. Ridimensionamento del pool di hello facilmente viene eseguito nel portale di hello o da PowerShell. Questo esercizio Usa il portale di hello.

1. Impostare *$DemoScenario* = **3**, _carico genera con burst più frequenti e più tempo per ogni database_ intensità hello tooincrease di carico di aggregazione hello pool di Hello senza modificare il carico di picco hello necessario per ogni database.
1. Premere **F5** tooapply tooall un carico ai database tenant.

1. Andare troppo**Pool1** in hello portale di Azure.

Hello monitoraggio maggiore utilizzo di eDTU del pool nel grafico superiore hello. Sono necessari alcuni minuti per hello nuovo maggiore carico tookick, ma rapidamente dovrebbe pool hello iniziare utilizzo max toohit e come carico hello steadies nel nuovo modello di hello, esegue l'overload rapidamente pool hello.

1. Fare clic su tooscale pool hello, **configurare pool** nella parte superiore di hello di hello **Pool1** pagina.
1. Regolare hello **eDTU Pool** impostazione troppo**100**. La modifica di eDTU del pool hello non modifica le impostazioni per ogni database hello (che è ancora 50 eDTU massimo per database). È possibile visualizzare le impostazioni per ogni database hello sul lato destro hello di hello **configurare pool** pagina.
1. Fare clic su **salvare** pool hello tooscale di toosubmit hello richiesta.

Tornare indietro troppo**Pool1** > **Panoramica** hello tooview grafici di monitoraggio. Monitorare l'effetto di hello della specifica del pool di hello maggiore quantità di risorse (anche se con un carico casuale e alcuni database non è sempre toosee facile concludere finché non viene eseguito per un certo tempo). Mentre si sta esaminando hello grafici tenere presente il 100% in hello superiore ora grafico rappresenta 100 Edtu, mentre in hello inferiore grafico 100% è ancora 50 Edtu come hello max per ogni database è ancora 50 Edtu.

I database rimangono completamente disponibili durante il processo di hello e online. In hello ultimo momento di ogni database è pronto toobe abilitata con hello nuovo numero di eDTU pool, tutte le connessioni attive vengono interrotte. Il codice dell'applicazione deve sempre scritto connessioni tooretry eliminato, quindi si riconnetterà toohello database nel pool di hello con scalabilità verticale.

## <a name="load-balance-between-pools"></a>Bilanciare il carico tra i pool

Come un'alternativa tooscaling pool hello, creare un pool di secondo e spostare i database in cui vengono toobalance hello caricare tra hello due pool. Questo nuovo pool di hello devono essere creati in toodo hello prima hello nello stesso server.

1. In hello [portale di Azure](https://portal.azure.com)aprire hello **tenants1 -&lt;utente&gt;**  server.
1. Fare clic su **+ nuovo pool** toocreate un pool di server corrente hello.
1. In hello **pool di database elastici** modello:

    1. Impostare **nome** troppo*Pool2*.
    1. Lasciare hello tariffario come **Pool Standard**.
    1. Fare clic su **Configura pool**.
    1. Impostare **eDTU Pool** troppo*eDTU 50*.
    1. Fare clic su **aggiungere database** toosee un elenco di database nel server di hello che può essere aggiunto troppo*Pool2*.
    1. Selezionare qualsiasi toomove 10 database queste toohello nuovo pool e quindi fare clic su **selezionare**. Se si è in esecuzione il generatore di carico hello, servizio hello già sa che il profilo di prestazioni richiede un più ampio pool di dimensioni predefinite del 50 eDTU hello e consiglia di iniziare con un'impostazione di eDTU 100.

    ![Suggerimento](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Per questa esercitazione, lasciare l'impostazione predefinita di hello nella finestra di 50 Edtu e fare clic su **selezionare** nuovamente.
    1. Selezionare **OK** toocreate hello nuovo pool e toomove hello nei database selezionati al suo interno.

Creazione di pool di hello e lo spostamento di database hello richiede alcuni minuti. Come i database vengono spostati che rimangono in linea e completamente accessibili fino a quando l'ultimo momento hello a quel punto vengono chiuse tutte le connessioni aperte. Se si dispone di una logica di tentativi, i client si connettono quindi toohello database nel nuovo pool di hello.

Sfoglia troppo**Pool2** (su hello *tenants1* server) tooopen hello pool e monitorarne le prestazioni. Se non è visualizzata, attendere per il provisioning di hello nuovo pool toocomplete.

Si nota ora una riduzione dell'utilizzo delle risorse di *Pool1* e un carico simile per *Pool2*.

## <a name="manage-performance-of-a-single-database"></a>Gestire le prestazioni di un database singolo

Se un singolo database in un pool di cui si verifichi un elevato carico, a seconda della configurazione del pool di hello, può tendono risorse hello toodominate nel pool di hello e l'impatto di altri database. Se l'attività hello è probabilmente toocontinue per un certo tempo, hello database può essere spostato temporaneamente fuori pool hello. In questo modo hello di hello database toohave risorse aggiuntive necessarie e isola da hello altri database.

Questo esercizio simula l'effetto di hello di Contoso insieme Hall sottoposto a un carico elevato quando i ticket in vendita per un insieme comune.

1. Aprire hello... \\ *Demo PerformanceMonitoringAndManagement.ps1* script.
1. Impostare **$DemoScenario = 5, Generare un carico normale e un carico elevato in un singolo tenant (circa 95 DTU).**
1. Impostare **$SingleTenantDatabaseName = contosoconcerthall**
1. Eseguire tramite script hello **F5**.


1. In hello [portale di Azure](https://portal.azure.com) aprire **Pool1**.
1. Controllare hello **monitoraggio pool elastico** del grafico e cercare hello maggiore utilizzo di eDTU del pool. Dopo un minuto o due, inizieranno tookick in carichi più elevati hello e rapidamente dovrebbe essere che il pool di hello raggiunge l'utilizzo del 100%.
1. Controllare hello **monitoraggio di database elastico** visualizzazione che mostra i database più interessanti hello hello ora precedente. Hello *contosoconcerthall* database non appena vengono visualizzate come uno dei database di hello cinque più interessanti.
1. **Fare clic su monitoraggio di database elastico hello** **grafico** e aprirla hello **utilizzo delle risorse di Database** pagina in cui è possibile monitorare i database hello. Ciò consente di isolare visualizzazione hello per hello *contosoconcerthall* database.
1. Elenco di hello dei database, fare clic su **contosoconcerthall**.
1. Fare clic su **tariffario (scala Dtu)** tooopen hello **configurare prestazioni** pagina in cui è possibile impostare un livello di prestazioni autonome per database hello.
1. Fare clic su hello **Standard** scheda Opzioni di scalabilità hello tooopen nel livello Standard hello.
1. Diapositiva hello **dispositivo di scorrimento DTU** tooright tooselect **100** Dtu. Notare che questo corrisponde l'obiettivo di servizio toohello, **S3**.
1. Fare clic su **applica** toomove hello database dal pool hello e renderlo un *S3 Standard* database.
1. Dopo il ridimensionamento è completata, monitoraggio hello effetto sul database contosoconcerthall hello e Pool1 in pannelli di pool e il database elastici hello.

Una volta che un carico elevato sul database contosoconcerthall hello hello diminuisce è necessario immediatamente restituirla toohello pool tooreduce il costo. Se non è chiaro che verrà eseguito quando è stato possibile impostare un avviso nel database di hello che verrà attivata quando l'utilizzo DTU scende di sotto di hello per ogni database max pool hello. Lo spostamento di un database in un pool è descritto nell'esercizio 5.

## <a name="other-performance-management-patterns"></a>Altri modelli di gestione delle prestazioni

**Scalabilità preventiva** nell'esercizio hello precedente in cui si esplorata come tooscale un database isolato, sapendo quali toolook database per. Se Gestione hello di Contoso insieme Hall era informata Wingtips di vendita ticket imminente hello, database hello potrebbe essere stati spostati all'esterno pool hello preventivamente. In caso contrario, probabile che richiede un avviso in pool hello o hello database toospot Qual era il problema. Se non vuoi toolearn informazioni da hello altri tenant nel pool che segnala che di hello di riduzione delle prestazioni. E se il tenant hello possibile stimare quanti sono necessari ulteriori risorse, è possibile configurare un database di automazione di Azure runbook toomove hello fuori pool hello e quindi di nuovo su una pianificazione definita.

**Tenant self-service scalabilità** perché il ridimensionamento è un'attività denominata facilmente tramite l'API di gestione di hello, è possibile facilmente compilare il possibilità hello database tenant tooscale nell'applicazione Web tenant e offrirlo come una funzionalità del servizio SaaS. Ad esempio, consentire ai tenant self-administer scalabilità verticale e, forse collegati direttamente fatturazione tootheir!

**Scalabilità verticale e un pool ai modelli di utilizzo toomatch pianificazione**

In cui l'utilizzo tenant aggregazione segue modelli di utilizzo stimabile, è possibile utilizzare su e giù tooscale di automazione di Azure un pool in base alla pianificazione. Ad esempio, ridurre le prestazioni dopo le 18 e aumentarle di nuovo prima delle 6 nei giorni della settimana in cui è noto che si verifica un calo delle risorse richieste.



## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Simulare l'utilizzo nel database tenant hello eseguendo un generatore di carico specificato
> * I database tenant hello Monitor come rispondono toohello aumento del carico
> * Applicare la scalabilità verticale hello pool elastico nel caricamento del database maggiore toohello risposta
> * Eseguire il provisioning di un'attività di database hello secondo del saldo tooload pool elastico

[Esercitazione sul ripristino di un tenant singolo](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Risorse aggiuntive

* Ulteriori [esercitazioni in cui si basano su una distribuzione di applicazioni SaaS Wingtip hello](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Pool elastici SQL](sql-database-elastic-pool.md)
* [Automazione di Azure](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) - Esercitazione sulla configurazione e l'uso di Log Analytics
