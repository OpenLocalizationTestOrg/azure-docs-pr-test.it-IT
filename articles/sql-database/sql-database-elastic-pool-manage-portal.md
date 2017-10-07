---
title: 'Portale di Azure: creare e gestire un pool elastico di database SQL | Microsoft Docs'
description: Informazioni su come toouse hello portale di Azure e toomanage intelligence predefinite del Database SQL, monitoraggio e prestazioni del database toooptimize un pool elastico scalabile le dimensioni appropriate e gestire i costi.
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a>Creare e gestire un pool elastico con hello portale di Azure
In questo argomento illustra come toocreate e gestire scalabile [pool elastici](sql-database-elastic-pool.md) con hello portale di Azure. È anche possibile creare e gestire un pool elastico Azure con [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello l'API REST o [c#](sql-database-elastic-pool-manage-csharp.md). È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

## <a name="create-an-elastic-pool"></a>Creare un pool elastico 

Esistono due modi per creare un pool elastico. È possibile farlo da zero se si conosce il programma di installazione di hello pool desiderato oppure iniziare con un suggerimento dal servizio hello. Database SQL prevede intelligence predefinite in cui si consiglia l'installazione di un pool elastico, se è più conveniente in base alle hello oltre telemetria per i database.

È possibile creare più pool su un server, ma non è possibile aggiungere i database da server diversi in hello stesso pool. 

> [!NOTE]
> I pool elastici sono disponibili a livello generale in tutte le aree di Azure tranne India occidentale, dove sono attualmente in anteprima.  I pool elastici verranno resi disponibili a livello generale in quest'area non appena possibile.
>

### <a name="step-1-create-an-elastic-pool"></a>Passaggio 1: creare un pool elastico

Creazione di un pool elastico da un oggetto esistente **server** pannello nel portale di hello è hello più semplice modo toomove database esistenti in un pool elastico.

> [!NOTE]
> È inoltre possibile creare un pool elastico eseguendo una ricerca **pool elastico SQL** in hello **Marketplace** o facendo clic su **+ Aggiungi** in hello **pool elastico SQL**Sfoglia blade. Si è in grado di toospecify un server nuovo o esistente tramite il provisioning del flusso di lavoro del pool.
>
>

1. In hello [portale di Azure](http://portal.azure.com/), fare clic su **più servizi**  **>**  **istanze di SQL Server**, quindi fare clic su server hello contenente hello database da pool elastico di tooadd tooan.
2. Fare clic su **Nuovo pool**.

    ![Aggiungere pool tooa server](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    **-OPPURE-**

    Verrà visualizzato un messaggio indicante che vi sono consigliate pool elastici per server hello. Fare clic su hello toosee di messaggio hello consigliato pool in base alle telemetria cronologici del database, quindi scegliere hello livello toosee ulteriori dettagli e personalizzare il pool di hello. Vedere [comprendere raccomandazioni per i pool](#understand-elastic-pool-recommendations) più avanti in questo argomento per la modalità hello è stata generata.

    ![pool consigliato](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. Hello **pool elastico** pannello viene visualizzato, che è possibile specificare le impostazioni di hello per il pool. Se fa clic su **nuovo pool** nel passaggio precedente hello, hello tariffario è **Standard** per impostazione predefinita e nessun database selezionato. È possibile creare un pool vuoto o specificare un set di database esistenti da tale toomove server nel pool di hello. Se si sta creando un pool consigliati, hello consigliato tariffario, le impostazioni delle prestazioni e sono popolati automaticamente l'elenco dei database, ma è comunque possibile modificarle.

    ![Configurare un pool elastico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. Specificare un nome per il pool elastico hello o lasciare il campo come valore predefinito di hello.

### <a name="step-2-choose-a-pricing-tier"></a>Passaggio 2: Scegliere un piano tariffario

Hello piano tariffario del pool determina hello funzionalità elastics toohello disponibile nel pool di hello e hello il numero massimo di Edtu (numero massimo di eDTU) e spazio di archiviazione (GB) disponibile tooeach database. Per altre informazioni, vedere Livelli di servizio.

Fare clic su toochange hello piano tariffario per il pool di hello **tariffario**, fare clic su hello tariffario desiderato e quindi fare clic su **selezionare**.

> [!IMPORTANT]
> Dopo aver scelto hello a livello di prezzo e confermare le modifiche facendo clic **OK** nell'ultimo passaggio hello, non sarà in grado di toochange hello piano tariffario del pool di hello. toochange hello piano tariffario per un pool elastico esistente, creare un pool elastico piano tariffario desiderato hello ed eseguire la migrazione hello database toothis nuovo pool.
>

![Selezione di un livello di prezzo](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a>Passaggio 3: Configurare i pool di hello

Dopo avere impostato hello a livello di prezzo, fare clic su Configura pool in cui si aggiungono i database, set di Edtu del pool e spazio di archiviazione (GB pool) e si imposta hello min e max numero di Edtu per elastics hello nel pool di hello.

1. Fare clic su **Configura pool**
2. Selezionare il database di hello da tooadd toohello pool. Questo passaggio è facoltativo durante la creazione di pool hello. È possibile aggiungere i database dopo aver creato il pool di hello.
    Fare clic su database tooadd, **Aggiungi database**, fare clic su hello database che si desidera tooadd e quindi fare clic su hello **selezionare** pulsante.

    ![Aggiungi database](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    Se si lavora con i database di hello dispongono di dati di telemetria sufficienti all'utilizzo storico, hello **stimato eDTU e GB utilizzo** grafico e hello **utilizzo di eDTU effettivo** grafico a barre toohelp di aggiornamento della configurazione decisioni. Inoltre, servizio hello può fornire un toohelp di messaggi di raccomandazioni per le dimensioni appropriate hello pool. Vedere la sezione [Indicazioni dinamiche](#understand-elastic-pool-recommendations).

3. Utilizzare i controlli di hello in hello **configurare pool** pagina tooexplore impostazioni e configurare il pool. Vedere la sezione relativa ai [limiti dei pool elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) per altri dettagli sui limiti per ogni livello di servizio e le [considerazioni su prezzi e prestazioni per i pool elastici](sql-database-elastic-pool.md) per istruzioni dettagliate sul corretto ridimensionamento di un pool elastico. Per altre informazioni sulle impostazioni del pool, vedere [Proprietà del pool elastico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).

    ![Configurare un pool elastico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. Fare clic su **selezionare** in hello **configurare Pool** pannello dopo la modifica delle impostazioni.
5. Fare clic su **OK** pool hello toocreate.

## <a name="understand-elastic-pool-recommendations"></a>Informazioni sulle indicazioni per i pool elastici

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

## <a name="manage-and-monitor-an-elastic-pool"></a>Gestire e monitorare un pool elastico

È possibile utilizzare hello toomonitor portale Azure e gestire i database di hello nel pool di hello e un pool elastico. Dal portale di hello, è possibile monitorare l'utilizzo di un pool elastico e il database di hello all'interno di tale pool hello. È possibile creare un set di modifiche pool elastico tooyour e inviare tutte le modifiche in hello stesso tempo. Le modifiche includono l'aggiunta o la rimozione di database, la modifica delle impostazioni del pool elastico o la modifica delle impostazioni del database.

Hello seguente grafico mostra un pool elastico di esempio. visualizzazione di Hello include:

*  Grafici per il monitoraggio dell'utilizzo delle risorse del pool elastico hello sia i database hello contenuti nel pool di hello.
*  Hello **configura** toomake pulsante pool Cambia pool elastico toohello.
*  Hello **Crea database** pulsante che consente di creare un database e lo aggiunge pool elastico corrente toohello.
*  Processi elastici che consentono di gestire un numero elevato di database tramite l'esecuzione di script Transact SQL in tutti i database in un elenco.

![Visualizzazione del pool][2]

È possibile passare tooa pool specifico toosee il relativo utilizzo delle risorse. Per impostazione predefinita, il pool di hello è tooshow configurato sull'utilizzo di archiviazione e di eDTU per hello ultima ora. grafico Hello può essere configurato tooshow metriche su diversi intervalli di tempo.

1. Selezionare un pool elastico di toowork con.
2. In **Monitoraggio pool elastico** è presente un grafico con l'etichetta **Utilizzo risorse**. Fare clic su grafico hello.

    ![Monitoraggio di pool elastici][3]

    Hello **metrica** pannello viene aperto, che mostra una visualizzazione dettagliata di hello specificati metriche su finestra temporale specificata hello.   

    ![Blade delle metriche][9]

### <a name="toocustomize-hello-chart-display"></a>visualizzazione del grafico hello toocustomize

È possibile modificare il grafico hello e hello blade metriche toodisplay altre metriche quali Percentuale CPU, percentuale dei / o di dati e percentuale dei / o di log utilizzata.

1. Nel pannello metriche hello, fare clic su **modifica**.

    ![Fare clic su Modifica][6]

2. In hello **Modifica grafico** pannello selezionare un intervallo di tempo (passati oggi, ora o settimana precedente), oppure fare clic su **personalizzato** tooselect qualsiasi data intervallo hello ultime due settimane. Selezionare tipo di grafico hello (riga o barra), quindi selezionare toomonitor risorse hello.

   > [!Note]
   > Solo le metriche con hello stessa unità di misura possono essere visualizzati in hello del grafico in hello stesso tempo. Ad esempio, se si seleziona "percentuale di eDTU" quindi è possibile solo selezionare altre metriche percentuale come unità di misura di hello.
   >

    ![Fare clic su Modifica](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. Fare quindi clic su **OK**.

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a>Gestire e monitorare database in un pool elastico

È possibile monitorare anche i singoli database per potenziali problemi.

1. In **Monitoraggio database elastico**è disponibile un grafico che mostra le metriche relative a cinque database. Per impostazione predefinita, hello il grafico visualizza hello primi 5 database nel pool di hello per utilizzo di eDTU medio in hello ora precedente. Fare clic su grafico hello.

    ![Monitoraggio di pool elastici][4]

2. Hello **utilizzo delle risorse di Database** pannello viene visualizzato. Ciò offre una visualizzazione dettagliata di utilizzo del database nel pool di hello hello. Griglia hello nella parte inferiore di hello del pannello hello, è possibile selezionare tutti i database in hello pool toodisplay il relativo utilizzo in grafico hello (backup dei database too5). È inoltre possibile personalizzare finestra metrica e l'ora visualizzata nel grafico hello facendo clic, hello **Modifica grafico**.

    ![Pannello Utilizzo risorse database][8]

### <a name="toocustomize-hello-view"></a>visualizzazione di hello toocustomize

1. In hello **utilizzo delle risorse del Database** pannello, fare clic su **Modifica grafico**.

    ![Fare clic su Modifica grafico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. In hello **modifica** pannello del grafico, selezionare un intervallo di tempo (passati ora o ultime 24 ore) o fare clic su **personalizzato** tooselect un giorno diverso in hello oltre toodisplay 2 settimane.

    ![Fare clic su personalizzato](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. Fare clic su hello **confronto dei database da** tooselect elenco a discesa un toouse metrica diversi durante il confronto dei database.

    ![Modifica grafico hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a>tooselect database toomonitor

Nell'elenco di database hello in hello **utilizzo delle risorse di Database** pannello, è possibile trovare determinati database, verificare tramite pagine hello nell'elenco di hello o immettere il nome di un database hello. Utilizzare hello casella di controllo tooselect hello database.

![Ricerca per i database toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Aggiungere una risorsa del pool elastico tooan avviso

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

## <a name="move-a-database-into-an-elastic-pool"></a>Spostare un database in un pool elastico

È possibile aggiungere o rimuovere i database da un pool esistente. database Hello possono trovarsi in altri pool. Tuttavia, è possibile aggiungere solo i database che sono su hello stesso server logico.

1. Nel Pannello di hello per il pool di hello in **i database elastici** fare clic su **configurare pool**.

    ![Fare clic su Configura pool][1]

2. In hello **configurare pool** pannello, fare clic su **aggiungere toopool**.

    ![Fare clic su Aggiungi toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. In hello **aggiungere database** pannello, database selezionare hello o pool di database tooadd toohello. Quindi fare clic su **Seleziona**.

    ![Selezione database tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    Hello **configurare pool** pannello ora elenchi hello database selezionato toobe aggiunto, con il relativo stato impostato troppo**in sospeso**.

    ![Aggiunte di pool in sospeso](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. In hello **pannello pool configura**, fare clic su **salvare**.

    ![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a>Spostare un database da un pool elastico

1. In hello **configurare pool** pannello, database selezionare hello o tooremove di database.

    ![elenchi di database](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. Fare clic su **Rimuovi dal pool**.

    ![elenchi di database](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    Hello **configurare pool** pannello ora elenchi hello database selezionato toobe rimossa con il relativo stato impostato troppo**in sospeso**.

    ![anteprima aggiunta e rimozione database](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. In hello **pannello pool configura**, fare clic su **salvare**.

    ![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a>Modificare le impostazioni delle prestazioni di un pool elastico

Durante il monitoraggio di utilizzo delle risorse di hello di un pool elastico, si potrebbe scoprire che sono necessarie alcune modifiche. Forse pool hello richiede una modifica nei limiti di archiviazione o di prestazioni hello. Probabilmente si desidera toochange impostazioni hello nel pool di hello. È possibile modificare il programma di installazione di hello del pool di hello in qualsiasi momento tooget hello migliore bilanciamento delle prestazioni e costi. Per altre informazioni, vedere [Quando usare un pool elastico](sql-database-elastic-pool.md).

toochange hello Edtu o archiviazione di limiti per ogni pool e di Edtu per database:

1. Aprire hello **configurare pool** blade.

    In **le impostazioni del pool elastico**, utilizzare le impostazioni del pool hello toochange uno dispositivo di scorrimento.

    ![Utilizzo delle risorse del pool elastico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. Quando viene modificata l'impostazione di hello, hello visualizzata hello mensile costo stimato del cambiamento di hello.

    ![Aggiornamento di un pool elastico e nuovi costi mensili](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a>Latenza delle operazioni dei pool elastici
* Modifica hello min Edtu per database o un numero massimo di Edtu per ogni database in genere viene completata entro 5 minuti o meno.
* Modifica hello Edtu per pool dipende dalla quantità totale di hello dello spazio utilizzato da tutti i database nel pool di hello. Le modifiche richiedono una media di 90 minuti o meno per 100 GB. Ad esempio, se lo spazio totale hello utilizzato da tutti i database nel pool di hello è 200 GB, quindi hello prevista latenza per la modifica hello pool eDTU per pool è 3 ore o minore.

## <a name="next-steps"></a>Passaggi successivi

- quali un pool elastico, vedere toounderstand [pool elastico SQL Database](sql-database-elastic-pool.md).
- Per indicazioni sull'uso dei pool elastici, vedere le [considerazioni su prezzo e prestazioni per i pool elastici](sql-database-elastic-pool.md).
- toouse processi elastico toorun Transact-SQL script su qualsiasi numero di database nel pool di hello, vedere [Panoramica processi elastico](sql-database-elastic-jobs-overview.md).
- tooquery in qualsiasi numero di database nel pool di hello, vedere [panoramica delle query elastico](sql-database-elastic-query-overview.md).
- Per le transazioni di un numero qualsiasi di database nel pool di hello, vedere [transazioni elastiche](sql-database-elastic-transactions-overview.md).


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
