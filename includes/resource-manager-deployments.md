## <a name="incremental-and-complete-deployments"></a><span data-ttu-id="33675-101">Distribuzioni incrementali e complete</span><span class="sxs-lookup"><span data-stu-id="33675-101">Incremental and complete deployments</span></span>
<span data-ttu-id="33675-102">Quando si distribuisce le risorse, specificare che la distribuzione di hello è un aggiornamento incrementale o un aggiornamento completo.</span><span class="sxs-lookup"><span data-stu-id="33675-102">When deploying your resources, you specify that hello deployment is either an incremental update or a complete update.</span></span> <span data-ttu-id="33675-103">Hello principale differenza tra queste due modalità è come Gestione risorse gestisce le risorse esistenti nel gruppo di risorse hello che non sono presenti nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="33675-103">hello primary difference between these two modes is how Resource Manager handles existing resources in hello resource group that are not in hello template:</span></span>

* <span data-ttu-id="33675-104">In modalità completa, gestione delle risorse **Elimina** le risorse che esisterebbero nel gruppo di risorse hello ma non sono specificate nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="33675-104">In complete mode, Resource Manager **deletes** resources that exist in hello resource group but are not specified in hello template.</span></span> 
* <span data-ttu-id="33675-105">In modalità incrementale, Gestione risorse **lascia invariato** le risorse che esisterebbero nel gruppo di risorse hello ma non sono specificate nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="33675-105">In incremental mode, Resource Manager **leaves unchanged** resources that exist in hello resource group but are not specified in hello template.</span></span>

<span data-ttu-id="33675-106">Per entrambe le modalità, Gestione risorse tenta tooprovision tutte le risorse specificate nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="33675-106">For both modes, Resource Manager attempts tooprovision all resources specified in hello template.</span></span> <span data-ttu-id="33675-107">Se la risorsa hello esiste già nel gruppo di risorse hello e le relative impostazioni sono identiche, operazione hello comporta alcuna modifica.</span><span class="sxs-lookup"><span data-stu-id="33675-107">If hello resource already exists in hello resource group and its settings are unchanged, hello operation results in no change.</span></span> <span data-ttu-id="33675-108">Se si modificano le impostazioni di hello per una risorsa, viene eseguito il provisioning di risorse hello con le nuove impostazioni.</span><span class="sxs-lookup"><span data-stu-id="33675-108">If you change hello settings for a resource, hello resource is provisioned with those new settings.</span></span> <span data-ttu-id="33675-109">Se si tenta di percorso hello tooupdate o un tipo di una risorsa esistente, la distribuzione di hello genera un errore.</span><span class="sxs-lookup"><span data-stu-id="33675-109">If you attempt tooupdate hello location or type of an existing resource, hello deployment fails with an error.</span></span> <span data-ttu-id="33675-110">In alternativa, distribuire una nuova risorsa con il percorso di hello o digitare che è necessario.</span><span class="sxs-lookup"><span data-stu-id="33675-110">Instead, deploy a new resource with hello location or type that you need.</span></span>

<span data-ttu-id="33675-111">Per impostazione predefinita, Gestione risorse Usa modalità incrementale hello.</span><span class="sxs-lookup"><span data-stu-id="33675-111">By default, Resource Manager uses hello incremental mode.</span></span>

<span data-ttu-id="33675-112">differenza hello tooillustrate tra le modalità incrementale e completa, prendere in considerazione hello seguente scenario.</span><span class="sxs-lookup"><span data-stu-id="33675-112">tooillustrate hello difference between incremental and complete modes, consider hello following scenario.</span></span>

<span data-ttu-id="33675-113">Il **gruppo di risorse esistente** contiene:</span><span class="sxs-lookup"><span data-stu-id="33675-113">**Existing Resource Group** contains:</span></span>

* <span data-ttu-id="33675-114">Risorsa A</span><span class="sxs-lookup"><span data-stu-id="33675-114">Resource A</span></span>
* <span data-ttu-id="33675-115">Risorsa B</span><span class="sxs-lookup"><span data-stu-id="33675-115">Resource B</span></span>
* <span data-ttu-id="33675-116">Risorsa C</span><span class="sxs-lookup"><span data-stu-id="33675-116">Resource C</span></span>

<span data-ttu-id="33675-117">Il **modello** definisce:</span><span class="sxs-lookup"><span data-stu-id="33675-117">**Template** defines:</span></span>

* <span data-ttu-id="33675-118">Risorsa A</span><span class="sxs-lookup"><span data-stu-id="33675-118">Resource A</span></span>
* <span data-ttu-id="33675-119">Risorsa B</span><span class="sxs-lookup"><span data-stu-id="33675-119">Resource B</span></span>
* <span data-ttu-id="33675-120">Risorsa D</span><span class="sxs-lookup"><span data-stu-id="33675-120">Resource D</span></span>

<span data-ttu-id="33675-121">Quando vengono distribuiti in **incrementale** modalità gruppo di risorse hello contiene:</span><span class="sxs-lookup"><span data-stu-id="33675-121">When deployed in **incremental** mode, hello resource group contains:</span></span>

* <span data-ttu-id="33675-122">Risorsa A</span><span class="sxs-lookup"><span data-stu-id="33675-122">Resource A</span></span>
* <span data-ttu-id="33675-123">Risorsa B</span><span class="sxs-lookup"><span data-stu-id="33675-123">Resource B</span></span>
* <span data-ttu-id="33675-124">Risorsa C</span><span class="sxs-lookup"><span data-stu-id="33675-124">Resource C</span></span>
* <span data-ttu-id="33675-125">Risorsa D</span><span class="sxs-lookup"><span data-stu-id="33675-125">Resource D</span></span>

<span data-ttu-id="33675-126">Quando viene implementato in modalità **completa**, la risorsa C viene eliminata.</span><span class="sxs-lookup"><span data-stu-id="33675-126">When deployed in **complete** mode, Resource C is deleted.</span></span> <span data-ttu-id="33675-127">il gruppo di risorse di Hello contiene:</span><span class="sxs-lookup"><span data-stu-id="33675-127">hello resource group contains:</span></span>

* <span data-ttu-id="33675-128">Risorsa A</span><span class="sxs-lookup"><span data-stu-id="33675-128">Resource A</span></span>
* <span data-ttu-id="33675-129">Risorsa B</span><span class="sxs-lookup"><span data-stu-id="33675-129">Resource B</span></span>
* <span data-ttu-id="33675-130">Risorsa D</span><span class="sxs-lookup"><span data-stu-id="33675-130">Resource D</span></span>
