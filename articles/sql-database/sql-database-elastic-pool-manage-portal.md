---
title: 'Portale di Azure: creare e gestire un pool elastico di database SQL | Microsoft Docs'
description: "Informazioni su come usare il portale di Azure e le funzionalità di intelligence predefinite del database SQL per gestire, monitorare e dimensionare in modo adeguato un pool elastico scalabile per ottimizzare le prestazioni del database e gestire i costi."
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
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="70580-103">Creare e gestire un pool elastico con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="70580-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="70580-104">Questo argomento illustra come creare e gestire [pool elastici](sql-database-elastic-pool.md) scalabili con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="70580-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="70580-105">È anche possibile creare e gestire un pool elastico di Azure con [PowerShell](sql-database-elastic-pool-manage-powershell.md), l'API REST o [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="70580-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="70580-106">È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="70580-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="70580-107">Creare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-107">Create an elastic pool</span></span> 

<span data-ttu-id="70580-108">Esistono due modi per creare un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="70580-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="70580-109">È possibile farlo da zero se si conosce la configurazione del pool da usare oppure iniziare con una raccomandazione fornita dal servizio.</span><span class="sxs-lookup"><span data-stu-id="70580-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="70580-110">Il database SQL integra informazioni in base alle quali viene suggerita una configurazione del pool elastico nel caso risulti più conveniente secondo i dati di telemetria relativi all'uso precedente dei database.</span><span class="sxs-lookup"><span data-stu-id="70580-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="70580-111">È possibile creare più pool in un server, ma non aggiungere database da diversi server nello stesso pool.</span><span class="sxs-lookup"><span data-stu-id="70580-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="70580-112">I pool elastici sono disponibili a livello generale in tutte le aree di Azure tranne India occidentale, dove sono attualmente in anteprima.</span><span class="sxs-lookup"><span data-stu-id="70580-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="70580-113">I pool elastici verranno resi disponibili a livello generale in quest'area non appena possibile.</span><span class="sxs-lookup"><span data-stu-id="70580-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="70580-114">Passaggio 1: creare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="70580-115">La creazione di un pool elastico da un pannello **server** esistente nel portale è il modo più semplice per trasferire i database esistenti in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="70580-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="70580-116">È anche possibile creare un pool elastico cercando **pool elastico SQL** nel **Marketplace** o facendo clic su **+Aggiungi** nel pannello **Pool elastici SQL**.</span><span class="sxs-lookup"><span data-stu-id="70580-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="70580-117">È possibile specificare un server nuovo o esistente nel flusso di lavoro dei provisioning del pool.</span><span class="sxs-lookup"><span data-stu-id="70580-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="70580-118">Nel [portale di Azure](http://portal.azure.com/) fare clic su **Altri servizi** **>** **SQL Server** e selezionare il server che contiene i database da aggiungere a un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="70580-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="70580-119">Fare clic su **Nuovo pool**.</span><span class="sxs-lookup"><span data-stu-id="70580-119">Click **New pool**.</span></span>

    ![Aggiungere un pool a un server](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="70580-121">**-OPPURE-**</span><span class="sxs-lookup"><span data-stu-id="70580-121">**-OR-**</span></span>

    <span data-ttu-id="70580-122">Potrebbe essere visualizzato un messaggio che informa che sono disponibili pool elastici consigliati per il server.</span><span class="sxs-lookup"><span data-stu-id="70580-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="70580-123">Fare clic sul messaggio per visualizzare i pool consigliati in base ai dati di telemetria cronologici relativi all'utilizzo del database e quindi fare clic sul livello per visualizzare altri dettagli e personalizzare il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="70580-124">Per informazioni su come vengono create le raccomandazioni, vedere [Informazioni sulle raccomandazioni per i pool](#understand-elastic-pool-recommendations) più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="70580-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![pool consigliato](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="70580-126">Verrà visualizzato il pannello **Pool elastico** in cui verranno specificate le impostazioni per il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="70580-127">Se è stata scelta l'opzione **Nuovo pool** nel passaggio precedente, il piano tariffario sarà **Standard** per impostazione predefinita e non sarà selezionato alcun database.</span><span class="sxs-lookup"><span data-stu-id="70580-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="70580-128">È possibile creare un pool vuoto o specificare un set di database esistenti del server da spostare nel pool.</span><span class="sxs-lookup"><span data-stu-id="70580-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="70580-129">Se si sta creando un pool consigliato, il piano tariffario, le impostazioni delle prestazioni e l'elenco di database consigliati appariranno prepopolati ma potranno essere modificati.</span><span class="sxs-lookup"><span data-stu-id="70580-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configurare un pool elastico](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="70580-131">Specificare un nome per il pool elastico o lasciare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="70580-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="70580-132">Passaggio 2: Scegliere un piano tariffario</span><span class="sxs-lookup"><span data-stu-id="70580-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="70580-133">Il piano tariffario del pool determina le funzionalità disponibili per i database elastici nel pool e il numero massimo di eDTU (MAX eDTU) e la memoria (GB) disponibili per ciascun database.</span><span class="sxs-lookup"><span data-stu-id="70580-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="70580-134">Per altre informazioni, vedere Livelli di servizio.</span><span class="sxs-lookup"><span data-stu-id="70580-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="70580-135">Per modificare il piano tariffario per il pool, fare clic su **Piano tariffario**, scegliere il piano e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="70580-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70580-136">Dopo aver scelto il piano tariffario e aver eseguito il commit delle modifiche facendo clic su **OK** nell'ultimo passaggio, non sarà più possibile modificare il piano tariffario del pool.</span><span class="sxs-lookup"><span data-stu-id="70580-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="70580-137">Per modificare il piano tariffario per un pool di database elastici esistente, creare un pool elastico nel piano tariffario desiderato ed eseguire la migrazione dei database in questo nuovo pool.</span><span class="sxs-lookup"><span data-stu-id="70580-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![Selezione di un livello di prezzo](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="70580-139">Passaggio 3: Configurare il pool</span><span class="sxs-lookup"><span data-stu-id="70580-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="70580-140">Dopo avere impostato il piano tariffario, fare clic su Configura pool dove è possibile aggiungere i database, impostare le eDTU e lo spazio di archiviazione (in GB) del pool, nonché il numero minimo e massimo di eDTU per i database elastici nel pool.</span><span class="sxs-lookup"><span data-stu-id="70580-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="70580-141">Fare clic su **Configura pool**</span><span class="sxs-lookup"><span data-stu-id="70580-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="70580-142">Selezionare i database da aggiungere al pool.</span><span class="sxs-lookup"><span data-stu-id="70580-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="70580-143">Questo passaggio è facoltativo durante la creazione del pool.</span><span class="sxs-lookup"><span data-stu-id="70580-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="70580-144">È possibile aggiungere i database dopo aver creato il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="70580-145">Per aggiungere i database, fare clic su **Aggiungi database**, selezionare i database da aggiungere e quindi fare clic sul pulsante **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="70580-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![Aggiungi database](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="70580-147">Se i dati di telemetria cronologici relativi all'utilizzo disponibili per i database correnti sono sufficienti, il grafico **Utilizzo di eDTU e GB** e il grafico a barre **Utilizzo di eDTU effettivo** vengono aggiornati per semplificare le decisioni relative alla configurazione.</span><span class="sxs-lookup"><span data-stu-id="70580-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="70580-148">Il servizio potrebbe anche visualizzare un messaggio di raccomandazione per facilitare la scelta delle dimensioni corrette per il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="70580-149">Vedere la sezione [Indicazioni dinamiche](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="70580-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="70580-150">Usare i controlli nella pagina **Configura pool** per esaminare le impostazioni e configurare il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="70580-151">Vedere la sezione relativa ai [limiti dei pool elastici](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) per altri dettagli sui limiti per ogni livello di servizio e le [considerazioni su prezzi e prestazioni per i pool elastici](sql-database-elastic-pool.md) per istruzioni dettagliate sul corretto ridimensionamento di un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="70580-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="70580-152">Per altre informazioni sulle impostazioni del pool, vedere [Proprietà del pool elastico](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="70580-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configurare un pool elastico](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="70580-154">Fare clic su **Seleziona** in the **Configure Pool** .</span><span class="sxs-lookup"><span data-stu-id="70580-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="70580-155">Fare clic su **OK** per creare il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="70580-156">Informazioni sulle indicazioni per i pool elastici</span><span class="sxs-lookup"><span data-stu-id="70580-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="70580-157">Il servizio di database SQL valuta la cronologia di utilizzo e suggerisce uno o più pool quando questo approccio è più conveniente rispetto all'uso di singoli database.</span><span class="sxs-lookup"><span data-stu-id="70580-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="70580-158">Ogni raccomandazione viene configurata con un subset univoco di database del server che meglio si adatta al pool.</span><span class="sxs-lookup"><span data-stu-id="70580-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![pool consigliato](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="70580-160">La raccomandazione per il pool include:</span><span class="sxs-lookup"><span data-stu-id="70580-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="70580-161">Piano tariffario per il pool (Basic, Standard, Premium o Premium RS)</span><span class="sxs-lookup"><span data-stu-id="70580-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="70580-162">**eDTU POOL** appropriato, detto anche eDTU max per pool.</span><span class="sxs-lookup"><span data-stu-id="70580-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="70580-163">**MAX eDTU** e **Min eDTU** per ogni database.</span><span class="sxs-lookup"><span data-stu-id="70580-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="70580-164">Elenco di database consigliati per il pool.</span><span class="sxs-lookup"><span data-stu-id="70580-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70580-165">Il servizio prende in considerazione la telemetria degli ultimi 30 giorni per la raccomandazione dei pool.</span><span class="sxs-lookup"><span data-stu-id="70580-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="70580-166">Per far sì che un database possa essere considerato un candidato per un pool elastico, deve esistere da almeno 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="70580-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="70580-167">I database che si trovano già in pool elastici non vengono considerati come possibili candidati, in linea con i consigli relativi ai pool elastici.</span><span class="sxs-lookup"><span data-stu-id="70580-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="70580-168">Il servizio valuta le risorse necessarie e la convenienza dello spostamento di singoli database in ogni livello di servizio nei pool dello stesso livello.</span><span class="sxs-lookup"><span data-stu-id="70580-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="70580-169">Ad esempio, vengono valutati tutti i database Standard in un server per l’utilizzo in un pool elastico Standard.</span><span class="sxs-lookup"><span data-stu-id="70580-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="70580-170">Ciò significa che il servizio non effettua consigli relativi a livelli diversi, ad esempio lo spostamento di un database Standard in un pool Premium.</span><span class="sxs-lookup"><span data-stu-id="70580-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="70580-171">Dopo aver aggiunto i database al pool, le indicazioni verranno generate dinamicamente in base all'uso storico dei database selezionati.</span><span class="sxs-lookup"><span data-stu-id="70580-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="70580-172">Queste indicazioni vengono visualizzate nel grafico relativo all'uso di eDTU e GB, oltre che come banner nella parte superiore del pannello **Configura pool**.</span><span class="sxs-lookup"><span data-stu-id="70580-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="70580-173">Queste indicazioni sono concepite per facilitare la creazione di un pool elastico ottimizzato per database specifici.</span><span class="sxs-lookup"><span data-stu-id="70580-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![Indicazioni dinamiche](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="70580-175">Gestire e monitorare un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="70580-176">È possibile usare il portale di Azure per monitorare e gestire un pool elastico e i database nel pool.</span><span class="sxs-lookup"><span data-stu-id="70580-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="70580-177">Dal portale è possibile monitorare l'utilizzo di un pool elastico e dei database al suo interno.</span><span class="sxs-lookup"><span data-stu-id="70580-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="70580-178">È anche possibile apportare un set di modifiche al pool elastico e inviare tutte le modifiche contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="70580-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="70580-179">Le modifiche includono l'aggiunta o la rimozione di database, la modifica delle impostazioni del pool elastico o la modifica delle impostazioni del database.</span><span class="sxs-lookup"><span data-stu-id="70580-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="70580-180">L'immagine seguente illustra un esempio di pool elastico.</span><span class="sxs-lookup"><span data-stu-id="70580-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="70580-181">La visualizzazione include:</span><span class="sxs-lookup"><span data-stu-id="70580-181">The view includes:</span></span>

*  <span data-ttu-id="70580-182">Grafici per il monitoraggio dell'utilizzo delle risorse da parte del pool elastico e dei database al suo interno.</span><span class="sxs-lookup"><span data-stu-id="70580-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="70580-183">Il pulsante **Configura pool** per apportare modifiche al pool elastico.</span><span class="sxs-lookup"><span data-stu-id="70580-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="70580-184">Il pulsante **Crea database** per creare un database e aggiungerlo al pool elastico corrente.</span><span class="sxs-lookup"><span data-stu-id="70580-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="70580-185">Processi elastici che consentono di gestire un numero elevato di database tramite l'esecuzione di script Transact SQL in tutti i database in un elenco.</span><span class="sxs-lookup"><span data-stu-id="70580-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Visualizzazione del pool][2]

<span data-ttu-id="70580-187">È possibile passare a un pool specifico per visualizzarne l'utilizzo delle risorse.</span><span class="sxs-lookup"><span data-stu-id="70580-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="70580-188">Per impostazione predefinita, il pool è configurato per mostrare l'utilizzo di eDTU e risorse di archiviazione relativo all'ultima ora.</span><span class="sxs-lookup"><span data-stu-id="70580-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="70580-189">È possibile configurare il grafico per mostrare diverse metriche in diversi intervalli di tempo.</span><span class="sxs-lookup"><span data-stu-id="70580-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="70580-190">Selezionare un pool elastico da usare.</span><span class="sxs-lookup"><span data-stu-id="70580-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="70580-191">In **Monitoraggio pool elastico** è presente un grafico con l'etichetta **Utilizzo risorse**.</span><span class="sxs-lookup"><span data-stu-id="70580-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="70580-192">Fare clic sul grafico.</span><span class="sxs-lookup"><span data-stu-id="70580-192">Click the chart.</span></span>

    ![Monitoraggio di pool elastici][3]

    <span data-ttu-id="70580-194">Verrà visualizzato il pannello **Metrica** con una visualizzazione dettagliata delle metriche specificate nell'intervallo di tempo indicato.</span><span class="sxs-lookup"><span data-stu-id="70580-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![Blade delle metriche][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="70580-196">Per personalizzare la visualizzazione del grafico</span><span class="sxs-lookup"><span data-stu-id="70580-196">To customize the chart display</span></span>

<span data-ttu-id="70580-197">È possibile modificare il grafico e il pannello Metrica per visualizzare altre metriche, ad esempio la percentuale di CPU, la percentuale di IO dei dati e la percentuale di IO del log usata.</span><span class="sxs-lookup"><span data-stu-id="70580-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="70580-198">Nel pannello Metrica fare clic su **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="70580-198">On the metric blade, click **Edit**.</span></span>

    ![Fare clic su Modifica][6]

2. <span data-ttu-id="70580-200">Nel pannello **Modifica grafico** selezionare un intervallo di tempo, ad esempio ora precedente, oggi o settimana precedente, oppure fare clic su **personalizzato** per impostare un qualsiasi intervallo di tempo nelle due settimane precedenti.</span><span class="sxs-lookup"><span data-stu-id="70580-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="70580-201">Selezionare il tipo di grafico (a barre o a linee), quindi selezionare le risorse da monitorare.</span><span class="sxs-lookup"><span data-stu-id="70580-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="70580-202">Solo le metriche con la stessa unità di misura possono essere visualizzate nel grafico nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="70580-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="70580-203">Se ad esempio si seleziona "eDTU percentage" (Percentuale eDTU), sarà possibile selezionare solo altre metriche con percentuale come unità di misura.</span><span class="sxs-lookup"><span data-stu-id="70580-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![Fare clic su Modifica](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="70580-205">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="70580-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="70580-206">Gestire e monitorare database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="70580-207">È possibile monitorare anche i singoli database per potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="70580-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="70580-208">In **Monitoraggio database elastico**è disponibile un grafico che mostra le metriche relative a cinque database.</span><span class="sxs-lookup"><span data-stu-id="70580-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="70580-209">Per impostazione predefinita, il grafico mostra i primi cinque database nel pool per utilizzo di eDTU medio nell'ora precedente.</span><span class="sxs-lookup"><span data-stu-id="70580-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="70580-210">Fare clic sul grafico.</span><span class="sxs-lookup"><span data-stu-id="70580-210">Click the chart.</span></span>

    ![Monitoraggio di pool elastici][4]

2. <span data-ttu-id="70580-212">Verrà visualizzato il pannello **Utilizzo risorse database**,</span><span class="sxs-lookup"><span data-stu-id="70580-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="70580-213">che fornisce una visualizzazione dettagliata dell'utilizzo del database nel pool.</span><span class="sxs-lookup"><span data-stu-id="70580-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="70580-214">La griglia nella parte inferiore del pannello consente di selezionare fino a cinque database nel pool per visualizzarne l'uso nel grafico.</span><span class="sxs-lookup"><span data-stu-id="70580-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="70580-215">È anche possibile personalizzare le metriche e l'intervallo di tempo visualizzati nel grafico facendo clic su **Modifica grafico**.</span><span class="sxs-lookup"><span data-stu-id="70580-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![Pannello Utilizzo risorse database][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="70580-217">Per personalizzare la visualizzazione</span><span class="sxs-lookup"><span data-stu-id="70580-217">To customize the view</span></span>

1. <span data-ttu-id="70580-218">Nel pannello **Utilizzo risorse database** fare clic su **Modifica grafico**.</span><span class="sxs-lookup"><span data-stu-id="70580-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Fare clic su Modifica grafico](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="70580-220">Nel pannello **Modifica grafico** selezionare un intervallo di tempo, ad esempio ora precedente o ultime 24 ore, oppure fare clic su **personalizzato** per selezionare un giorno diverso nelle 2 settimane precedenti.</span><span class="sxs-lookup"><span data-stu-id="70580-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![Fare clic su personalizzato](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="70580-222">Fare clic sull'elenco a discesa **Confronta database per** e selezionare una metrica diversa da usare per il confronto dei database.</span><span class="sxs-lookup"><span data-stu-id="70580-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![Modificare il grafico](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="70580-224">Per selezionare i database da monitorare</span><span class="sxs-lookup"><span data-stu-id="70580-224">To select databases to monitor</span></span>

<span data-ttu-id="70580-225">Nell'elenco dei database del pannello **Utilizzo risorse database** è possibile trovare database specifici scorrendo le pagine dell'elenco o digitando il nome di un database.</span><span class="sxs-lookup"><span data-stu-id="70580-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="70580-226">Usare la casella di controllo per selezionare il database.</span><span class="sxs-lookup"><span data-stu-id="70580-226">Use the checkbox to select the database.</span></span>

![Cercare i database da monitorare][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="70580-228">Aggiungere un avviso a una risorsa di pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="70580-229">È possibile aggiungere regole a un pool elastico per l'invio di messaggi di posta elettronica a persone oppure stringhe di avviso a endpoint di URL quando il pool elastico raggiunge la soglia d'uso impostata.</span><span class="sxs-lookup"><span data-stu-id="70580-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="70580-230">**Per aggiungere un avviso a una risorsa qualsiasi:**</span><span class="sxs-lookup"><span data-stu-id="70580-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="70580-231">Fare clic sul grafico **Utilizzo risorse** per aprire il pannello **Metrica**. Fare clic su **Aggiungi avviso** e inserire le informazioni nel pannello **Aggiungi una regola di avviso**. La **risorsa** viene impostata automaticamente come il pool corrente.</span><span class="sxs-lookup"><span data-stu-id="70580-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="70580-232">Inserire un **Nome** e una **Descrizione** che serviranno a identificare l'avviso per l'utente e i destinatari.</span><span class="sxs-lookup"><span data-stu-id="70580-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="70580-233">Scegliere una **Metrica** in base alla quale creare un avviso dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="70580-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="70580-234">Il grafico mostra in modo dinamico l'utilizzo delle risorse per la metrica selezionata in modo da scegliere una soglia.</span><span class="sxs-lookup"><span data-stu-id="70580-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="70580-235">Scegliere una **Condizione**, ad esempio maggiore di, minore di e così via, e una **Soglia**.</span><span class="sxs-lookup"><span data-stu-id="70580-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="70580-236">Scegliere un **Periodo** di tempo entro il quale la regola della metrica deve essere soddisfatta prima dell'attivazione dell'avviso.</span><span class="sxs-lookup"><span data-stu-id="70580-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="70580-237">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="70580-237">Click **OK**.</span></span>

<span data-ttu-id="70580-238">Per altre informazioni, vedere [Usare il portale di Azure per creare avvisi per il database SQL di Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="70580-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="70580-239">Spostare un database in un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="70580-240">È possibile aggiungere o rimuovere i database da un pool esistente.</span><span class="sxs-lookup"><span data-stu-id="70580-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="70580-241">I database possono trovarsi in altri pool.</span><span class="sxs-lookup"><span data-stu-id="70580-241">The databases can be in other pools.</span></span> <span data-ttu-id="70580-242">Tuttavia, è possibile aggiungere solo i database che sono nello stesso server logico.</span><span class="sxs-lookup"><span data-stu-id="70580-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="70580-243">Nel pannello del pool, in **Database elastici** fare clic su **Configura pool**.</span><span class="sxs-lookup"><span data-stu-id="70580-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Fare clic su Configura pool][1]

2. <span data-ttu-id="70580-245">Nel pannello **Configura pool** fare clic su **Aggiungi al pool**.</span><span class="sxs-lookup"><span data-stu-id="70580-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![Fare clic su Aggiungi al pool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="70580-247">Nel pannello **Aggiungi database** selezionare uno o più database da aggiungere al pool.</span><span class="sxs-lookup"><span data-stu-id="70580-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="70580-248">Quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="70580-248">Then click **Select**.</span></span>

    ![Selezionare i database da aggiungere](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="70580-250">Il pannello **Configura pool** mostra il database selezionato per l'aggiunta, con lo stato impostato su **In sospeso**.</span><span class="sxs-lookup"><span data-stu-id="70580-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![Aggiunte di pool in sospeso](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="70580-252">Nel pannello **Configura pool** fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="70580-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="70580-254">Spostare un database da un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="70580-255">Nel pannello **Configura pool** selezionare uno o più database da rimuovere.</span><span class="sxs-lookup"><span data-stu-id="70580-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![elenchi di database](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="70580-257">Fare clic su **Rimuovi dal pool**.</span><span class="sxs-lookup"><span data-stu-id="70580-257">Click **Remove from pool**.</span></span>

    ![elenchi di database](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="70580-259">Il pannello **Configura pool** mostra il database selezionato per la rimozione, con lo stato impostato su **In sospeso**.</span><span class="sxs-lookup"><span data-stu-id="70580-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![anteprima aggiunta e rimozione database](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="70580-261">Nel pannello **Configura pool** fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="70580-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![Fare clic su Salva.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="70580-263">Modificare le impostazioni delle prestazioni di un pool elastico</span><span class="sxs-lookup"><span data-stu-id="70580-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="70580-264">Durante il monitoraggio dell'utilizzo delle risorse di un pool elastico possono rendersi necessarie alcune modifiche,</span><span class="sxs-lookup"><span data-stu-id="70580-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="70580-265">ad esempio dei limiti di archiviazione o di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="70580-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="70580-266">Si potrebbe voler modificare le impostazioni del database nel pool.</span><span class="sxs-lookup"><span data-stu-id="70580-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="70580-267">È possibile modificare la configurazione del pool in qualsiasi momento per ottenere il miglior compromesso tra prestazioni e costi.</span><span class="sxs-lookup"><span data-stu-id="70580-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="70580-268">Per altre informazioni, vedere [Quando usare un pool elastico](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="70580-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="70580-269">Per modificare i limiti di archiviazione o eDTU per il pool e il numero di eDTU per il database:</span><span class="sxs-lookup"><span data-stu-id="70580-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="70580-270">Aprire il pannello **Configura pool** .</span><span class="sxs-lookup"><span data-stu-id="70580-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="70580-271">In **Impostazioni pool elastico** usare i dispositivi di scorrimento per modificare le impostazioni del pool.</span><span class="sxs-lookup"><span data-stu-id="70580-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![Utilizzo delle risorse del pool elastico](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="70580-273">Alla modifica dell'impostazione, viene visualizzato il relativo costo mensile stimato.</span><span class="sxs-lookup"><span data-stu-id="70580-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![Aggiornamento di un pool elastico e nuovi costi mensili](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="70580-275">Latenza delle operazioni dei pool elastici</span><span class="sxs-lookup"><span data-stu-id="70580-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="70580-276">La modifica del numero minimo di eDTU per database o del numero massimo di eDTU per database in genere viene completata entro 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="70580-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="70580-277">La modifica del numero di eDTU per pool dipende dallo spazio totale usato da tutti i database nel pool.</span><span class="sxs-lookup"><span data-stu-id="70580-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="70580-278">Le modifiche richiedono una media di 90 minuti o meno per 100 GB.</span><span class="sxs-lookup"><span data-stu-id="70580-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="70580-279">Ad esempio, se lo spazio totale utilizzato da tutti i database nel pool è pari a 200 GB, la latenza prevista per la modifica del numero di eDTU del pool per ogni pool è di 3 ore o meno.</span><span class="sxs-lookup"><span data-stu-id="70580-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70580-280">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70580-280">Next steps</span></span>

- <span data-ttu-id="70580-281">Per informazioni sui pool elastici, vedere [Pool elastico del database SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="70580-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="70580-282">Per indicazioni sull'uso dei pool elastici, vedere le [considerazioni su prezzo e prestazioni per i pool elastici](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="70580-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="70580-283">Per usare i processi elastici per eseguire script Transact-SQL su qualsiasi numero di database nel pool, vedere la [panoramica dei processi elastici](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70580-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="70580-284">Per eseguire query su un numero qualsiasi di database nel pool, vedere la [panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70580-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="70580-285">Per eseguire transazioni su un numero qualsiasi di database nel pool, vedere [Transazioni elastiche](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70580-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
