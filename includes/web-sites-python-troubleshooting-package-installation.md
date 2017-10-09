<span data-ttu-id="a04bd-101">Alcuni pacchetti potrebbero non essere installati tramite pip se eseguiti su Azure.</span><span class="sxs-lookup"><span data-stu-id="a04bd-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="a04bd-102">È possibile semplicemente che il pacchetto di hello non è disponibile in hello indice del pacchetto Python.</span><span class="sxs-lookup"><span data-stu-id="a04bd-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="a04bd-103">È possibile che un compilatore è obbligatorio (un compilatore non è disponibile nel computer in esecuzione hello web app hello in Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="a04bd-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="a04bd-104">In questa sezione verrà esaminato toodeal modi con questo problema.</span><span class="sxs-lookup"><span data-stu-id="a04bd-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="a04bd-105">Richiedere i file wheel</span><span class="sxs-lookup"><span data-stu-id="a04bd-105">Request wheels</span></span>
<span data-ttu-id="a04bd-106">Se l'installazione del pacchetto hello richiede al compilatore, è consigliabile provare a contattare hello pacchetto proprietario toorequest ruote essere rese disponibili per il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="a04bd-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="a04bd-107">Con la disponibilità di recente hello di [compilatore Microsoft Visual C++ per Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], è ora più semplice toobuild i pacchetti con codice nativo per Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="a04bd-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="a04bd-108">Creare i file wheel (richiede Windows)</span><span class="sxs-lookup"><span data-stu-id="a04bd-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="a04bd-109">Nota: Quando si utilizza questa opzione, assicurarsi di pacchetto di hello toocompile che usa un ambiente di Python che corrisponde a hello/architettura/versione della piattaforma che viene utilizzato nell'applicazione web hello in Azure App Service (Windows/32-bit/2.7 o 3.4).</span><span class="sxs-lookup"><span data-stu-id="a04bd-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="a04bd-110">Se il pacchetto di hello non viene installata perché richiede un compilatore, è possibile installare del compilatore hello sul computer locale e compilare una ruota per pacchetto hello, che verranno quindi incluse nel repository.</span><span class="sxs-lookup"><span data-stu-id="a04bd-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="a04bd-111">Gli utenti Mac/Linux: Se non si dispone di computer Windows tooa di accesso, vedere [creare una macchina virtuale che esegue Windows] [ Create a Virtual Machine Running Windows] come toocreate una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="a04bd-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="a04bd-112">È possibile usarlo ruote hello toobuild, aggiungerli toohello repository e annullare hello macchina virtuale se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="a04bd-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="a04bd-113">Per Python 2.7, è possibile installare [compilatore Microsoft Visual C++ per Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="a04bd-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="a04bd-114">Per Python 3.4, è possibile installare [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="a04bd-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="a04bd-115">toobuild ruote, è necessario pacchetto rotellina hello:</span><span class="sxs-lookup"><span data-stu-id="a04bd-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="a04bd-116">Si utilizzerà `pip wheel` toocompile una dipendenza:</span><span class="sxs-lookup"><span data-stu-id="a04bd-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="a04bd-117">Verrà creato un file .whl nella cartella \wheelhouse hello.</span><span class="sxs-lookup"><span data-stu-id="a04bd-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="a04bd-118">Aggiungi cartella \wheelhouse hello e del selettore file tooyour repository.</span><span class="sxs-lookup"><span data-stu-id="a04bd-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="a04bd-119">Modificare il hello tooadd requirements.txt `--find-links` opzione nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="a04bd-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="a04bd-120">In questo modo toolook pip per una corrispondenza esatta nella cartella locale di hello prima di indice del pacchetto python toohello continua.</span><span class="sxs-lookup"><span data-stu-id="a04bd-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="a04bd-121">Se si desidera tooinclude tutte le dipendenze di hello \wheelhouse cartella e non utilizzare hello pacchetto python indice affatto, è possibile forzare l'indice del pacchetto pip tooignore hello aggiungendo `--no-index` toohello cima il requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="a04bd-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="a04bd-122">Personalizzare l'installazione</span><span class="sxs-lookup"><span data-stu-id="a04bd-122">Customize installation</span></span>
<span data-ttu-id="a04bd-123">È possibile personalizzare hello distribuzione script tooinstall un pacchetto nell'ambiente virtuale di hello utilizzando un programma di installazione alternativo, ad esempio semplice\_installare.</span><span class="sxs-lookup"><span data-stu-id="a04bd-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="a04bd-124">Per un esempio impostato come commento, vedere deploy.cmd.  Verificare che tali pacchetti non sono elencate nella requirements.txt, tooprevent pip da eseguirne l'installazione.</span><span class="sxs-lookup"><span data-stu-id="a04bd-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="a04bd-125">Aggiungere questo script di distribuzione toohello:</span><span class="sxs-lookup"><span data-stu-id="a04bd-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="a04bd-126">Potrebbe essere in grado di toouse facile\_installare tooinstall da un programma di installazione exe (alcuni sono zip in modo semplice, compatibile\_installazione supportarle).</span><span class="sxs-lookup"><span data-stu-id="a04bd-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="a04bd-127">Aggiungi repository tooyour programma di installazione di hello e richiamare semplice\_installare passando hello percorso toohello eseguibile.</span><span class="sxs-lookup"><span data-stu-id="a04bd-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="a04bd-128">Aggiungere questo script di distribuzione toohello:</span><span class="sxs-lookup"><span data-stu-id="a04bd-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="a04bd-129">Includere l'ambiente virtuale hello nel repository di hello (richiede Windows)</span><span class="sxs-lookup"><span data-stu-id="a04bd-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="a04bd-130">Nota: Quando si utilizza questa opzione, assicurarsi che toouse un ambiente virtuale corrispondente hello/architettura/versione della piattaforma che viene utilizzato nell'applicazione web hello in Azure App Service (Windows/32-bit/2.7 o 3.4).</span><span class="sxs-lookup"><span data-stu-id="a04bd-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="a04bd-131">Se si include l'ambiente virtuale hello nel repository di hello, è possibile impedire lo script di distribuzione hello dalla gestione dell'ambiente virtuale in Azure tramite la creazione di un file vuoto:</span><span class="sxs-lookup"><span data-stu-id="a04bd-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="a04bd-132">È consigliabile eliminare ambiente virtuale esistente hello in app hello, tooprevent file rimasti dall'ambiente virtuale hello è stato gestito automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a04bd-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
