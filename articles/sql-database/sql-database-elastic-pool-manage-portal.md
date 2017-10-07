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
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="37708-103">Creare e gestire un pool elastico con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="37708-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="37708-104">In questo argomento illustra come toocreate e gestire scalabile [pool elastici](sql-database-elastic-pool.md) con hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="37708-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="37708-105">È anche possibile creare e gestire un pool elastico Azure con [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello l'API REST o [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="37708-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="37708-106">È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="37708-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="37708-107">Creare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-107">Create an elastic pool</span></span> 

<span data-ttu-id="37708-108">Esistono due modi per creare un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="37708-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="37708-109">È possibile farlo da zero se si conosce il programma di installazione di hello pool desiderato oppure iniziare con un suggerimento dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="37708-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="37708-110">Database SQL prevede intelligence predefinite in cui si consiglia l'installazione di un pool elastico, se è più conveniente in base alle hello oltre telemetria per i database.</span><span class="sxs-lookup"><span data-stu-id="37708-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="37708-111">È possibile creare più pool su un server, ma non è possibile aggiungere i database da server diversi in hello stesso pool.</span><span class="sxs-lookup"><span data-stu-id="37708-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="37708-112">I pool elastici sono disponibili a livello generale in tutte le aree di Azure tranne India occidentale, dove sono attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="37708-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="37708-113">I pool elastici verranno resi disponibili a livello generale in quest'area non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="37708-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="37708-114">Passaggio 1: creare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="37708-115">Creazione di un pool elastico da un oggetto esistente **server** pannello nel portale di hello è hello più semplice modo toomove database esistenti in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="37708-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="37708-116">È inoltre possibile creare un pool elastico eseguendo una ricerca **pool elastico SQL** in hello **Marketplace** o facendo clic su **+ Aggiungi** in hello **pool elastico SQL**Sfoglia blade.</span><span class="sxs-lookup"><span data-stu-id="37708-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="37708-117">Si è in grado di toospecify un server nuovo o esistente tramite il provisioning del flusso di lavoro del pool.</span><span class="sxs-lookup"><span data-stu-id="37708-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="37708-118">In hello [portale di Azure](http://portal.azure.com/), fare clic su **più servizi**  **>**  **istanze di SQL Server**, quindi fare clic su server hello contenente hello database da pool elastico di tooadd tooan.</span><span class="sxs-lookup"><span data-stu-id="37708-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="37708-119">Fare clic su **Nuovo pool**.</span><span class="sxs-lookup"><span data-stu-id="37708-119">Click **New pool**.</span></span>

    ![Aggiungere pool tooa server](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="37708-121">**-OPPURE-**</span><span class="sxs-lookup"><span data-stu-id="37708-121">**-OR-**</span></span>

    <span data-ttu-id="37708-122">Verrà visualizzato un messaggio indicante che vi sono consigliate pool elastici per server hello.</span><span class="sxs-lookup"><span data-stu-id="37708-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="37708-123">Fare clic su hello toosee di messaggio hello consigliato pool in base alle telemetria cronologici del database, quindi scegliere hello livello toosee ulteriori dettagli e personalizzare il pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="37708-124">Vedere [comprendere raccomandazioni per i pool](#understand-elastic-pool-recommendations) più avanti in questo argomento per la modalità hello è stata generata.</span><span class="sxs-lookup"><span data-stu-id="37708-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![pool consigliato](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="37708-126">Hello **pool elastico** pannello viene visualizzato, che è possibile specificare le impostazioni di hello per il pool.</span><span class="sxs-lookup"><span data-stu-id="37708-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="37708-127">Se fa clic su **nuovo pool** nel passaggio precedente hello, hello tariffario è **Standard** per impostazione predefinita e nessun database selezionato.</span><span class="sxs-lookup"><span data-stu-id="37708-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="37708-128">È possibile creare un pool vuoto o specificare un set di database esistenti da tale toomove server nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="37708-129">Se si sta creando un pool consigliati, hello consigliato tariffario, le impostazioni delle prestazioni e sono popolati automaticamente l'elenco dei database, ma è comunque possibile modificarle.</span><span class="sxs-lookup"><span data-stu-id="37708-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configurare un pool elastico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="37708-131">Specificare un nome per il pool elastico hello o lasciare il campo come valore predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="37708-132">Passaggio 2: Scegliere un piano tariffario</span><span class="sxs-lookup"><span data-stu-id="37708-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="37708-133">Hello piano tariffario del pool determina hello funzionalità elastics toohello disponibile nel pool di hello e hello il numero massimo di Edtu (numero massimo di eDTU) e spazio di archiviazione (GB) disponibile tooeach database.</span><span class="sxs-lookup"><span data-stu-id="37708-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="37708-134">Per altre informazioni, vedere Livelli di servizio.</span><span class="sxs-lookup"><span data-stu-id="37708-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="37708-135">Fare clic su toochange hello piano tariffario per il pool di hello **tariffario**, fare clic su hello tariffario desiderato e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="37708-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37708-136">Dopo aver scelto hello a livello di prezzo e confermare le modifiche facendo clic **OK** nell'ultimo passaggio hello, non sarà in grado di toochange hello piano tariffario del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="37708-137">toochange hello piano tariffario per un pool elastico esistente, creare un pool elastico piano tariffario desiderato hello ed eseguire la migrazione hello database toothis nuovo pool.</span><span class="sxs-lookup"><span data-stu-id="37708-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Selezione di un livello di prezzo](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="37708-139">Passaggio 3: Configurare i pool di hello</span><span class="sxs-lookup"><span data-stu-id="37708-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="37708-140">Dopo avere impostato hello a livello di prezzo, fare clic su Configura pool in cui si aggiungono i database, set di Edtu del pool e spazio di archiviazione (GB pool) e si imposta hello min e max numero di Edtu per elastics hello nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="37708-141">Fare clic su **Configura pool**</span><span class="sxs-lookup"><span data-stu-id="37708-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="37708-142">Selezionare il database di hello da tooadd toohello pool.</span><span class="sxs-lookup"><span data-stu-id="37708-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="37708-143">Questo passaggio è facoltativo durante la creazione di pool hello.</span><span class="sxs-lookup"><span data-stu-id="37708-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="37708-144">È possibile aggiungere i database dopo aver creato il pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="37708-145">Fare clic su database tooadd, **Aggiungi database**, fare clic su hello database che si desidera tooadd e quindi fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="37708-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Aggiungi database](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="37708-147">Se si lavora con i database di hello dispongono di dati di telemetria sufficienti all'utilizzo storico, hello **stimato eDTU e GB utilizzo** grafico e hello **utilizzo di eDTU effettivo** grafico a barre toohelp di aggiornamento della configurazione decisioni.</span><span class="sxs-lookup"><span data-stu-id="37708-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="37708-148">Inoltre, servizio hello può fornire un toohelp di messaggi di raccomandazioni per le dimensioni appropriate hello pool.</span><span class="sxs-lookup"><span data-stu-id="37708-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="37708-149">Vedere la sezione [Indicazioni dinamiche](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="37708-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="37708-150">Utilizzare i controlli di hello in hello **configurare pool** pagina tooexplore impostazioni e configurare il pool.</span><span class="sxs-lookup"><span data-stu-id="37708-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="37708-151">Vedere la sezione relativa ai [limiti dei pool elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) per altri dettagli sui limiti per ogni livello di servizio e le [considerazioni su prezzi e prestazioni per i pool elastici](sql-database-elastic-pool.md) per istruzioni dettagliate sul corretto ridimensionamento di un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="37708-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="37708-152">Per altre informazioni sulle impostazioni del pool, vedere [Proprietà del pool elastico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="37708-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configurare un pool elastico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="37708-154">Fare clic su **selezionare** in hello **configurare Pool** pannello dopo la modifica delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="37708-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="37708-155">Fare clic su **OK** pool hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="37708-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="37708-156">Informazioni sulle indicazioni per i pool elastici</span><span class="sxs-lookup"><span data-stu-id="37708-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="37708-157">Hello servizio Database SQL valuta la cronologia di utilizzo e propone di uno o più pool quando è più conveniente rispetto all'uso di singoli database.</span><span class="sxs-lookup"><span data-stu-id="37708-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="37708-158">Ogni raccomandazione è configurato con un subset di database del server hello che meglio si adattano pool hello univoco.</span><span class="sxs-lookup"><span data-stu-id="37708-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![pool consigliato](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="37708-160">indicazione di pool Hello è costituito da:</span><span class="sxs-lookup"><span data-stu-id="37708-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="37708-161">Un piano tariffario per il pool di hello (Basic, Standard, Premium o Premium RS)</span><span class="sxs-lookup"><span data-stu-id="37708-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="37708-162">**eDTU POOL** appropriato, detto anche eDTU max per pool.</span><span class="sxs-lookup"><span data-stu-id="37708-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="37708-163">Hello **eDTU MAX** e **Min eDTU** per ogni database</span><span class="sxs-lookup"><span data-stu-id="37708-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="37708-164">elenco di Hello di database consigliati per il pool di hello</span><span class="sxs-lookup"><span data-stu-id="37708-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37708-165">servizio Hello considerando hello ultimi 30 giorni di dati di telemetria quando consigliando pool.</span><span class="sxs-lookup"><span data-stu-id="37708-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="37708-166">Per un toobe database considerato un candidato valido per un pool elastico, deve esistere per almeno sette giorni.</span><span class="sxs-lookup"><span data-stu-id="37708-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="37708-167">I database che si trovano già in pool elastici non vengono considerati come possibili candidati, in linea con i consigli relativi ai pool elastici.</span><span class="sxs-lookup"><span data-stu-id="37708-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="37708-168">servizio Hello valuta le risorse necessarie ed economicità di hello mobile singolo database in ogni livello di servizio nel pool di hello stesso livello.</span><span class="sxs-lookup"><span data-stu-id="37708-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="37708-169">Ad esempio, vengono valutati tutti i database Standard in un server per l’utilizzo in un pool elastico Standard.</span><span class="sxs-lookup"><span data-stu-id="37708-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="37708-170">Ciò significa servizio hello non indicazioni tra livelli, ad esempio lo spostamento di un database Standard in un pool Premium.</span><span class="sxs-lookup"><span data-stu-id="37708-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="37708-171">Dopo l'aggiunta di pool di database toohello, indicazioni generate dinamicamente in base all'utilizzo storico hello dei database hello che è stato selezionato.</span><span class="sxs-lookup"><span data-stu-id="37708-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="37708-172">Questi suggerimenti vengono visualizzati nel hello eDTU e GB del grafico di utilizzo in un banner di raccomandazione nella parte superiore di hello di hello **configurare pool** blade.</span><span class="sxs-lookup"><span data-stu-id="37708-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="37708-173">Queste raccomandazioni sono tooassist desiderato è la creazione di un pool elastico ottimizzato per i database specifici.</span><span class="sxs-lookup"><span data-stu-id="37708-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![Indicazioni dinamiche](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="37708-175">Gestire e monitorare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="37708-176">È possibile utilizzare hello toomonitor portale Azure e gestire i database di hello nel pool di hello e un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="37708-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="37708-177">Dal portale di hello, è possibile monitorare l'utilizzo di un pool elastico e il database di hello all'interno di tale pool hello.</span><span class="sxs-lookup"><span data-stu-id="37708-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="37708-178">È possibile creare un set di modifiche pool elastico tooyour e inviare tutte le modifiche in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="37708-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="37708-179">Le modifiche includono l'aggiunta o la rimozione di database, la modifica delle impostazioni del pool elastico o la modifica delle impostazioni del database.</span><span class="sxs-lookup"><span data-stu-id="37708-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="37708-180">Hello seguente grafico mostra un pool elastico di esempio.</span><span class="sxs-lookup"><span data-stu-id="37708-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="37708-181">visualizzazione di Hello include:</span><span class="sxs-lookup"><span data-stu-id="37708-181">hello view includes:</span></span>

*  <span data-ttu-id="37708-182">Grafici per il monitoraggio dell'utilizzo delle risorse del pool elastico hello sia i database hello contenuti nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="37708-183">Hello **configura** toomake pulsante pool Cambia pool elastico toohello.</span><span class="sxs-lookup"><span data-stu-id="37708-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="37708-184">Hello **Crea database** pulsante che consente di creare un database e lo aggiunge pool elastico corrente toohello.</span><span class="sxs-lookup"><span data-stu-id="37708-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="37708-185">Processi elastici che consentono di gestire un numero elevato di database tramite l'esecuzione di script Transact SQL in tutti i database in un elenco.</span><span class="sxs-lookup"><span data-stu-id="37708-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Visualizzazione del pool][2]

<span data-ttu-id="37708-187">È possibile passare tooa pool specifico toosee il relativo utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="37708-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="37708-188">Per impostazione predefinita, il pool di hello è tooshow configurato sull'utilizzo di archiviazione e di eDTU per hello ultima ora.</span><span class="sxs-lookup"><span data-stu-id="37708-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="37708-189">grafico Hello può essere configurato tooshow metriche su diversi intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="37708-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="37708-190">Selezionare un pool elastico di toowork con.</span><span class="sxs-lookup"><span data-stu-id="37708-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="37708-191">In **Monitoraggio pool elastico** è presente un grafico con l'etichetta **Utilizzo risorse**.</span><span class="sxs-lookup"><span data-stu-id="37708-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="37708-192">Fare clic su grafico hello.</span><span class="sxs-lookup"><span data-stu-id="37708-192">Click hello chart.</span></span>

    ![Monitoraggio di pool elastici][3]

    <span data-ttu-id="37708-194">Hello **metrica** pannello viene aperto, che mostra una visualizzazione dettagliata di hello specificati metriche su finestra temporale specificata hello.</span><span class="sxs-lookup"><span data-stu-id="37708-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Blade delle metriche][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="37708-196">visualizzazione del grafico hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="37708-196">toocustomize hello chart display</span></span>

<span data-ttu-id="37708-197">È possibile modificare il grafico hello e hello blade metriche toodisplay altre metriche quali Percentuale CPU, percentuale dei / o di dati e percentuale dei / o di log utilizzata.</span><span class="sxs-lookup"><span data-stu-id="37708-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="37708-198">Nel pannello metriche hello, fare clic su **modifica**.</span><span class="sxs-lookup"><span data-stu-id="37708-198">On hello metric blade, click **Edit**.</span></span>

    ![Fare clic su Modifica][6]

2. <span data-ttu-id="37708-200">In hello **Modifica grafico** pannello selezionare un intervallo di tempo (passati oggi, ora o settimana precedente), oppure fare clic su **personalizzato** tooselect qualsiasi data intervallo hello ultime due settimane.</span><span class="sxs-lookup"><span data-stu-id="37708-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="37708-201">Selezionare tipo di grafico hello (riga o barra), quindi selezionare toomonitor risorse hello.</span><span class="sxs-lookup"><span data-stu-id="37708-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="37708-202">Solo le metriche con hello stessa unità di misura possono essere visualizzati in hello del grafico in hello stesso tempo.</span><span class="sxs-lookup"><span data-stu-id="37708-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="37708-203">Ad esempio, se si seleziona "percentuale di eDTU" quindi è possibile solo selezionare altre metriche percentuale come unità di misura di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Fare clic su Modifica](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="37708-205">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="37708-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="37708-206">Gestire e monitorare database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="37708-207">È possibile monitorare anche i singoli database per potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="37708-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="37708-208">In **Monitoraggio database elastico**è disponibile un grafico che mostra le metriche relative a cinque database.</span><span class="sxs-lookup"><span data-stu-id="37708-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="37708-209">Per impostazione predefinita, hello il grafico visualizza hello primi 5 database nel pool di hello per utilizzo di eDTU medio in hello ora precedente.</span><span class="sxs-lookup"><span data-stu-id="37708-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="37708-210">Fare clic su grafico hello.</span><span class="sxs-lookup"><span data-stu-id="37708-210">Click hello chart.</span></span>

    ![Monitoraggio di pool elastici][4]

2. <span data-ttu-id="37708-212">Hello **utilizzo delle risorse di Database** pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="37708-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="37708-213">Ciò offre una visualizzazione dettagliata di utilizzo del database nel pool di hello hello.</span><span class="sxs-lookup"><span data-stu-id="37708-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="37708-214">Griglia hello nella parte inferiore di hello del pannello hello, è possibile selezionare tutti i database in hello pool toodisplay il relativo utilizzo in grafico hello (backup dei database too5).</span><span class="sxs-lookup"><span data-stu-id="37708-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="37708-215">È inoltre possibile personalizzare finestra metrica e l'ora visualizzata nel grafico hello facendo clic, hello **Modifica grafico**.</span><span class="sxs-lookup"><span data-stu-id="37708-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Pannello Utilizzo risorse database][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="37708-217">visualizzazione di hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="37708-217">toocustomize hello view</span></span>

1. <span data-ttu-id="37708-218">In hello **utilizzo delle risorse del Database** pannello, fare clic su **Modifica grafico**.</span><span class="sxs-lookup"><span data-stu-id="37708-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Fare clic su Modifica grafico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="37708-220">In hello **modifica** pannello del grafico, selezionare un intervallo di tempo (passati ora o ultime 24 ore) o fare clic su **personalizzato** tooselect un giorno diverso in hello oltre toodisplay 2 settimane.</span><span class="sxs-lookup"><span data-stu-id="37708-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Fare clic su personalizzato](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="37708-222">Fare clic su hello **confronto dei database da** tooselect elenco a discesa un toouse metrica diversi durante il confronto dei database.</span><span class="sxs-lookup"><span data-stu-id="37708-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Modifica grafico hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="37708-224">tooselect database toomonitor</span><span class="sxs-lookup"><span data-stu-id="37708-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="37708-225">Nell'elenco di database hello in hello **utilizzo delle risorse di Database** pannello, è possibile trovare determinati database, verificare tramite pagine hello nell'elenco di hello o immettere il nome di un database hello.</span><span class="sxs-lookup"><span data-stu-id="37708-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="37708-226">Utilizzare hello casella di controllo tooselect hello database.</span><span class="sxs-lookup"><span data-stu-id="37708-226">Use hello checkbox tooselect hello database.</span></span>

![Ricerca per i database toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="37708-228">Aggiungere una risorsa del pool elastico tooan avviso</span><span class="sxs-lookup"><span data-stu-id="37708-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="37708-229">È possibile aggiungere regole tooan pool elastico che inviano gli endpoint tooURL stringhe toopeople o un avviso di posta elettronica quando il pool elastico hello raggiunga una soglia di utilizzo impostato.</span><span class="sxs-lookup"><span data-stu-id="37708-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="37708-230">**una risorsa tooany avviso tooadd:**</span><span class="sxs-lookup"><span data-stu-id="37708-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="37708-231">Fare clic su hello **utilizzo delle risorse** hello tooopen grafico **metrica** pannello, fare clic su **Aggiungi avviso**e quindi immettere le informazioni di hello in hello **aggiungere un avviso regola** blade (**risorse** viene impostata automaticamente pool hello toobe si lavora con).</span><span class="sxs-lookup"><span data-stu-id="37708-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="37708-232">Digitare un **nome** e **descrizione** che identifica tooyou avviso hello e destinatari hello.</span><span class="sxs-lookup"><span data-stu-id="37708-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="37708-233">Scegliere un **metrica** che si desidera tooalert dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="37708-234">Hello dinamicamente Mostra utilizzo delle risorse per tale metrica toohelp che si sceglie una soglia.</span><span class="sxs-lookup"><span data-stu-id="37708-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="37708-235">Scegliere una **Condizione**, ad esempio maggiore di, minore di e così via, e una **Soglia**.</span><span class="sxs-lookup"><span data-stu-id="37708-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="37708-236">Scegliere un **periodo** di tempo che hello metrica regola deve essere soddisfatti prima di allarmi hello.</span><span class="sxs-lookup"><span data-stu-id="37708-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="37708-237">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="37708-237">Click **OK**.</span></span>

<span data-ttu-id="37708-238">Per altre informazioni, vedere [Usare il portale di Azure per creare avvisi per il database SQL di Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="37708-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="37708-239">Spostare un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="37708-240">È possibile aggiungere o rimuovere i database da un pool esistente.</span><span class="sxs-lookup"><span data-stu-id="37708-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="37708-241">database Hello possono trovarsi in altri pool.</span><span class="sxs-lookup"><span data-stu-id="37708-241">hello databases can be in other pools.</span></span> <span data-ttu-id="37708-242">Tuttavia, è possibile aggiungere solo i database che sono su hello stesso server logico.</span><span class="sxs-lookup"><span data-stu-id="37708-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="37708-243">Nel Pannello di hello per il pool di hello in **i database elastici** fare clic su **configurare pool**.</span><span class="sxs-lookup"><span data-stu-id="37708-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Fare clic su Configura pool][1]

2. <span data-ttu-id="37708-245">In hello **configurare pool** pannello, fare clic su **aggiungere toopool**.</span><span class="sxs-lookup"><span data-stu-id="37708-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Fare clic su Aggiungi toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="37708-247">In hello **aggiungere database** pannello, database selezionare hello o pool di database tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="37708-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="37708-248">Quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="37708-248">Then click **Select**.</span></span>

    ![Selezione database tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="37708-250">Hello **configurare pool** pannello ora elenchi hello database selezionato toobe aggiunto, con il relativo stato impostato troppo**in sospeso**.</span><span class="sxs-lookup"><span data-stu-id="37708-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Aggiunte di pool in sospeso](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="37708-252">In hello **pannello pool configura**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="37708-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="37708-254">Spostare un database da un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="37708-255">In hello **configurare pool** pannello, database selezionare hello o tooremove di database.</span><span class="sxs-lookup"><span data-stu-id="37708-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![elenchi di database](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="37708-257">Fare clic su **Rimuovi dal pool**.</span><span class="sxs-lookup"><span data-stu-id="37708-257">Click **Remove from pool**.</span></span>

    ![elenchi di database](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="37708-259">Hello **configurare pool** pannello ora elenchi hello database selezionato toobe rimossa con il relativo stato impostato troppo**in sospeso**.</span><span class="sxs-lookup"><span data-stu-id="37708-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![anteprima aggiunta e rimozione database](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="37708-261">In hello **pannello pool configura**, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="37708-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="37708-263">Modificare le impostazioni delle prestazioni di un pool elastico</span><span class="sxs-lookup"><span data-stu-id="37708-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="37708-264">Durante il monitoraggio di utilizzo delle risorse di hello di un pool elastico, si potrebbe scoprire che sono necessarie alcune modifiche.</span><span class="sxs-lookup"><span data-stu-id="37708-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="37708-265">Forse pool hello richiede una modifica nei limiti di archiviazione o di prestazioni hello.</span><span class="sxs-lookup"><span data-stu-id="37708-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="37708-266">Probabilmente si desidera toochange impostazioni hello nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="37708-267">È possibile modificare il programma di installazione di hello del pool di hello in qualsiasi momento tooget hello migliore bilanciamento delle prestazioni e costi.</span><span class="sxs-lookup"><span data-stu-id="37708-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="37708-268">Per altre informazioni, vedere [Quando usare un pool elastico](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="37708-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="37708-269">toochange hello Edtu o archiviazione di limiti per ogni pool e di Edtu per database:</span><span class="sxs-lookup"><span data-stu-id="37708-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="37708-270">Aprire hello **configurare pool** blade.</span><span class="sxs-lookup"><span data-stu-id="37708-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="37708-271">In **le impostazioni del pool elastico**, utilizzare le impostazioni del pool hello toochange uno dispositivo di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="37708-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Utilizzo delle risorse del pool elastico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="37708-273">Quando viene modificata l'impostazione di hello, hello visualizzata hello mensile costo stimato del cambiamento di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Aggiornamento di un pool elastico e nuovi costi mensili](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="37708-275">Latenza delle operazioni dei pool elastici</span><span class="sxs-lookup"><span data-stu-id="37708-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="37708-276">Modifica hello min Edtu per database o un numero massimo di Edtu per ogni database in genere viene completata entro 5 minuti o meno.</span><span class="sxs-lookup"><span data-stu-id="37708-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="37708-277">Modifica hello Edtu per pool dipende dalla quantità totale di hello dello spazio utilizzato da tutti i database nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="37708-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="37708-278">Le modifiche richiedono una media di 90 minuti o meno per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="37708-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="37708-279">Ad esempio, se lo spazio totale hello utilizzato da tutti i database nel pool di hello è 200 GB, quindi hello prevista latenza per la modifica hello pool eDTU per pool è 3 ore o minore.</span><span class="sxs-lookup"><span data-stu-id="37708-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37708-280">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37708-280">Next steps</span></span>

- <span data-ttu-id="37708-281">quali un pool elastico, vedere toounderstand [pool elastico SQL Database](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="37708-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="37708-282">Per indicazioni sull'uso dei pool elastici, vedere le [considerazioni su prezzo e prestazioni per i pool elastici](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="37708-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="37708-283">toouse processi elastico toorun Transact-SQL script su qualsiasi numero di database nel pool di hello, vedere [Panoramica processi elastico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37708-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="37708-284">tooquery in qualsiasi numero di database nel pool di hello, vedere [panoramica delle query elastico](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37708-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="37708-285">Per le transazioni di un numero qualsiasi di database nel pool di hello, vedere [transazioni elastiche](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37708-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
