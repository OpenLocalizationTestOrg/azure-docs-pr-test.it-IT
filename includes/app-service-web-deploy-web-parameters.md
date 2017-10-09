<span data-ttu-id="294c6-101">Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="294c6-101">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="294c6-102">modello Hello include una sezione denominata parametri che contiene tutti i valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="294c6-102">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="294c6-103">È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello.</span><span class="sxs-lookup"><span data-stu-id="294c6-103">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="294c6-104">Non definire parametri per i valori che saranno sempre hello stesso.</span><span class="sxs-lookup"><span data-stu-id="294c6-104">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="294c6-105">Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite.</span><span class="sxs-lookup"><span data-stu-id="294c6-105">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

<span data-ttu-id="294c6-106">Quando si definiscono i parametri, utilizzare hello **allowedValues** toospecify campo che i valori di un utente può fornire durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="294c6-106">When defining parameters, use hello **allowedValues** field toospecify which values a user can provide during deployment.</span></span> <span data-ttu-id="294c6-107">Hello utilizzare **defaultValue** campo tooassign un parametro di valore toohello, se viene fornito alcun valore durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="294c6-107">Use hello **defaultValue** field tooassign a value toohello parameter, if no value is provided during deployment.</span></span>

<span data-ttu-id="294c6-108">Si descrive ogni parametro di modello hello.</span><span class="sxs-lookup"><span data-stu-id="294c6-108">We will describe each parameter in hello template.</span></span>

### <a name="sitename"></a><span data-ttu-id="294c6-109">siteName</span><span class="sxs-lookup"><span data-stu-id="294c6-109">siteName</span></span>
<span data-ttu-id="294c6-110">nome Hello di hello web app che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="294c6-110">hello name of hello web app that you wish toocreate.</span></span>

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a><span data-ttu-id="294c6-111">hostingPlanName</span><span class="sxs-lookup"><span data-stu-id="294c6-111">hostingPlanName</span></span>
<span data-ttu-id="294c6-112">nome Hello del servizio App hello pianificare toouse per l'hosting hello web app.</span><span class="sxs-lookup"><span data-stu-id="294c6-112">hello name of hello App Service plan toouse for hosting hello web app.</span></span>

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a><span data-ttu-id="294c6-113">sku</span><span class="sxs-lookup"><span data-stu-id="294c6-113">sku</span></span>
<span data-ttu-id="294c6-114">Hello piano tariffario per hello piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="294c6-114">hello pricing tier for hello hosting plan.</span></span>

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

<span data-ttu-id="294c6-115">modello Hello definisce i valori consentiti per questo parametro hello e assegna un valore predefinito (S1) se viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="294c6-115">hello template defines hello values that are permitted for this parameter, and assigns a default value (S1) if no value is specified.</span></span>

### <a name="workersize"></a><span data-ttu-id="294c6-116">workerSize</span><span class="sxs-lookup"><span data-stu-id="294c6-116">workerSize</span></span>
<span data-ttu-id="294c6-117">dimensioni delle istanze Hello di hello (piccola, Media o grande) di piano di hosting.</span><span class="sxs-lookup"><span data-stu-id="294c6-117">hello instance size of hello hosting plan (small, medium, or large).</span></span>

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

<span data-ttu-id="294c6-118">modello Hello definisce i valori hello consentiti per questo parametro (0, 1 o 2) e assegna un valore predefinito (0) se viene specificato alcun valore.</span><span class="sxs-lookup"><span data-stu-id="294c6-118">hello template defines hello values that are permitted for this parameter (0, 1, or 2), and assigns a default value (0) if no value is specified.</span></span> <span data-ttu-id="294c6-119">i valori Hello corrispondono toosmall, medie e grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="294c6-119">hello values correspond toosmall, medium and large.</span></span>

