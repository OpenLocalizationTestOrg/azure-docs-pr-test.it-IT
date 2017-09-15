
<span data-ttu-id="66adb-101">In questo video di Azure Friday, con Scott Hanselman e Karthik Raman, Principal Engineering Manager, sono disponibili altre informazioni sulla distribuzione globale in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="66adb-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="66adb-102">Per informazioni sul funzionamento della replica di database globale in Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="66adb-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="66adb-103"><a id="addregion"></a>Aggiungere aree di database globali tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="66adb-103"><a id="addregion"></a>Add global database regions using the Azure Portal</span></span>
<span data-ttu-id="66adb-104">Azure Cosmos DB è disponibile in tutte le [aree di Azure][azureregions] del mondo.</span><span class="sxs-lookup"><span data-stu-id="66adb-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="66adb-105">Dopo aver selezionato il livello di coerenza predefinito per l'account di database, è possibile associare una o più aree, a seconda del livello di coerenza predefinito e delle esigenze di distribuzione globale scelti.</span><span class="sxs-lookup"><span data-stu-id="66adb-105">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="66adb-106">Nella barra a sinistra del [portale di Azure](https://portal.azure.com/) fare clic su **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="66adb-106">In the [Azure portal](https://portal.azure.com/), in the left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="66adb-107">Nel pannello **Azure Cosmos DB** selezionare l'account di database da modificare.</span><span class="sxs-lookup"><span data-stu-id="66adb-107">In the **Azure Cosmos DB** blade, select the database account to modify.</span></span>
3. <span data-ttu-id="66adb-108">Nel pannello dell'account fare clic su **Replica i dati a livello globale** dal menu.</span><span class="sxs-lookup"><span data-stu-id="66adb-108">In the account blade, click **Replicate data globally** from the menu.</span></span>
4. <span data-ttu-id="66adb-109">Nel pannello **Replica i dati a livello globale** selezionare le aree da aggiungere o rimuovere facendo clic su di esse nella mappa e quindi scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="66adb-109">In the **Replicate data globally** blade, select the regions to add or remove by clicking regions in the map, and then click **Save**.</span></span> <span data-ttu-id="66adb-110">L'aggiunta di aree ha un costo. Per altre informazioni, vedere la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/documentdb/) o l'articolo [Distribuire i dati a livello globale con DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="66adb-110">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Fare clic sulle aree nella mappa per aggiungerle o rimuoverle][1]
    
<span data-ttu-id="66adb-112">Dopo l'aggiunta di una seconda area, nel pannello **Replica i dati a livello globale** del portale viene abilitata l'opzione **Failover manuale**.</span><span class="sxs-lookup"><span data-stu-id="66adb-112">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data globally** blade in the portal.</span></span> <span data-ttu-id="66adb-113">È possibile usare questa opzione per testare il processo di failover o per modificare l'area di scrittura primaria.</span><span class="sxs-lookup"><span data-stu-id="66adb-113">You can use this option to test the failover process or change the primary write region.</span></span> <span data-ttu-id="66adb-114">Dopo avere aggiunto una terza area, l'opzione **Priorità di failover** viene abilitata nello stesso pannello per poter modificare l'ordine di failover per le operazioni di lettura.</span><span class="sxs-lookup"><span data-stu-id="66adb-114">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="66adb-115">Selezionare aree di database globali</span><span class="sxs-lookup"><span data-stu-id="66adb-115">Selecting global database regions</span></span>
<span data-ttu-id="66adb-116">Esistono due scenari comuni per la configurazione di due o più aree:</span><span class="sxs-lookup"><span data-stu-id="66adb-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="66adb-117">Offerta di accesso con bassa latenza ai dati indipendentemente dalla posizione del mondo in cui si trovano gli utenti finali</span><span class="sxs-lookup"><span data-stu-id="66adb-117">Delivering low-latency access to data to end users no matter where they are located around the globe</span></span>
2. <span data-ttu-id="66adb-118">Aggiunta di resilienza a livello di area per garantire continuità aziendale e ripristino di emergenza (BCDR)</span><span class="sxs-lookup"><span data-stu-id="66adb-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="66adb-119">Per offrire l'accesso con bassa latenza agli utenti finali, è consigliabile distribuire l'applicazione e aggiungere Azure Cosmos DB nelle aree corrispondenti alla località in cui si trovano gli utenti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="66adb-119">For delivering low-latency to end-users, it is recommended to deploy both the application and add Azure Cosmos DB in the regions thats correspond to where the application's users are located.</span></span>

<span data-ttu-id="66adb-120">Per finalità BCDR, è consigliabile aggiungere le aree in base alle coppie di aree descritte nell'articolo [Continuità aziendale e ripristino di emergenza nelle aree geografiche abbinate di Azure][bcdr].</span><span class="sxs-lookup"><span data-stu-id="66adb-120">For BCDR, it is recommended to add regions based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **Azure Cosmos DB** blade, select the database account to modify.
2. In the account blade, click **Replicate data globally** from the menu.
3. In the **Replicate data globally** blade, click **Manual Failover** from the top bar.
    ![Change the write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region to become the new write region, click the checkbox to confirm triggering a failover, and click OK
    ![Change the write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
