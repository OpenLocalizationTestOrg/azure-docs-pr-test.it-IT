
<span data-ttu-id="d57ff-101">In questo video di Azure Friday, con Scott Hanselman e Karthik Raman, Principal Engineering Manager, sono disponibili altre informazioni sulla distribuzione globale in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d57ff-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="d57ff-102">Per informazioni sul funzionamento della replica di database globale in Cosmos DB, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d57ff-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="d57ff-103"><a id="addregion"></a>Aggiungere aree database globale utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d57ff-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="d57ff-104">Azure Cosmos DB è disponibile in tutte le [aree di Azure][azureregions] del mondo.</span><span class="sxs-lookup"><span data-stu-id="d57ff-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="d57ff-105">Dopo aver selezionato a livello di coerenza hello predefinito per l'account di database, è possibile associare uno o più aree (a seconda la scelta delle esigenze di distribuzione globale e a livello di coerenza predefinito).</span><span class="sxs-lookup"><span data-stu-id="d57ff-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="d57ff-106">In hello [portale di Azure](https://portal.azure.com/)in hello barra sinistra, fare clic su **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="d57ff-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="d57ff-107">In hello **Azure Cosmos DB** blade, hello selezionare database account toomodify.</span><span class="sxs-lookup"><span data-stu-id="d57ff-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="d57ff-108">Nel Pannello di hello account, fare clic su **replicare i dati a livello globale** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="d57ff-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="d57ff-109">In hello **replicare i dati a livello globale** pannello selezionare hello aree tooadd o rimuovere, fare clic su aree mappa hello e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="d57ff-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="d57ff-110">È presente un aree tooadding costo, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/documentdb/) o hello [distribuire dati a livello globale con DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="d57ff-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Fare clic su aree hello in hello mappa tooadd o rimuoverli][1]
    
<span data-ttu-id="d57ff-112">Dopo aver aggiunto una seconda area, hello **Failover manuale** opzione è abilitata nei hello **replicare i dati a livello globale** pannello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="d57ff-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="d57ff-113">È possibile utilizzare questo processo di failover di opzione tootest hello o modificare l'area primaria scrittura hello.</span><span class="sxs-lookup"><span data-stu-id="d57ff-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="d57ff-114">Dopo aver aggiunto un'area del terzo, hello **le priorità di Failover** è attivata l'opzione hello pannello stesso in modo che è possibile modificare l'ordine di failover hello per le letture.</span><span class="sxs-lookup"><span data-stu-id="d57ff-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="d57ff-115">Selezionare aree di database globali</span><span class="sxs-lookup"><span data-stu-id="d57ff-115">Selecting global database regions</span></span>
<span data-ttu-id="d57ff-116">Esistono due scenari comuni per la configurazione di due o più aree:</span><span class="sxs-lookup"><span data-stu-id="d57ff-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="d57ff-117">Recapito a bassa latenza accesso agli utenti di tooend toodata indipendentemente da dove si trovano in tutto il mondo hello</span><span class="sxs-lookup"><span data-stu-id="d57ff-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="d57ff-118">Aggiunta di resilienza a livello di area per garantire continuità aziendale e ripristino di emergenza (BCDR)</span><span class="sxs-lookup"><span data-stu-id="d57ff-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="d57ff-119">Per la fornitura a bassa latenza tooend utenti, è consigliabile toodeploy entrambi hello applicazione e aggiungere database Cosmos Azure in aree hello corrispondenti agli utenti dell'applicazione hello toowhere si trovano.</span><span class="sxs-lookup"><span data-stu-id="d57ff-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="d57ff-120">Per BCDR, è consigliabile tooadd aree in base alle coppie di area hello descritte in hello [Business continuità e ripristino di emergenza (BCDR): aree abbinate Azure] [ bcdr] articolo.</span><span class="sxs-lookup"><span data-stu-id="d57ff-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
