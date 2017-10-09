
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="90cf6-101">toosave costi, è possibile sospendere e riprendere calcolo risorse su richiesta.</span><span class="sxs-lookup"><span data-stu-id="90cf6-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="90cf6-102">Ad esempio, se si prevede di usare database hello durante la notte hello e i fine settimana, è possibile sospenderla durante le ore e riprenderlo giornata hello.</span><span class="sxs-lookup"><span data-stu-id="90cf6-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="90cf6-103">È non verrà addebitato Dwu mentre hello database resta sospesa.</span><span class="sxs-lookup"><span data-stu-id="90cf6-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="90cf6-104">Quando si sospende un database:</span><span class="sxs-lookup"><span data-stu-id="90cf6-104">When you pause a database:</span></span>

* <span data-ttu-id="90cf6-105">Risorse di calcolo e memoria vengono restituite toohello pool di risorse disponibili nel centro dati hello</span><span class="sxs-lookup"><span data-stu-id="90cf6-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="90cf6-106">I costi DWU sono pari a zero per la durata di hello di pausa hello.</span><span class="sxs-lookup"><span data-stu-id="90cf6-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="90cf6-107">L'archivio dati non è interessato e i dati rimangano invariati.</span><span class="sxs-lookup"><span data-stu-id="90cf6-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="90cf6-108">SQL Data Warehouse annulla tutte le operazioni in esecuzione o in coda.</span><span class="sxs-lookup"><span data-stu-id="90cf6-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

