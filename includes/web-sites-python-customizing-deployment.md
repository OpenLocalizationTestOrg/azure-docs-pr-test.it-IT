<span data-ttu-id="db219-101">Per stabilire se l'applicazione usa Python, Azure verifica se **entrambe le condizioni seguenti sono soddisfatte**:</span><span class="sxs-lookup"><span data-stu-id="db219-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="db219-102">Requirements.txt file nella cartella radice hello</span><span class="sxs-lookup"><span data-stu-id="db219-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="db219-103">qualsiasi file py nella cartella radice hello o un runtime.txt che specifica di python</span><span class="sxs-lookup"><span data-stu-id="db219-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="db219-104">Quando è il caso di hello, utilizza uno script di distribuzione specifico Python, che esegue la sincronizzazione di standard hello dei file, nonché altre operazioni di Python, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="db219-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="db219-105">Gestione automatica dell'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="db219-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="db219-106">Installazione dei pacchetti elencati in requirements.txt tramite pip</span><span class="sxs-lookup"><span data-stu-id="db219-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="db219-107">Creazione di Web. config appropriato hello in base a hello selezionato versione di Python.</span><span class="sxs-lookup"><span data-stu-id="db219-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="db219-108">Raccolta di file statici per le applicazioni Django</span><span class="sxs-lookup"><span data-stu-id="db219-108">Collect static files for Django applications</span></span>

<span data-ttu-id="db219-109">È possibile controllare alcuni aspetti di passaggi di distribuzione predefinito hello senza script hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="db219-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="db219-110">Se si desidera tooskip tutti i passaggi di distribuzione di Python, è possibile creare questo file vuoto:</span><span class="sxs-lookup"><span data-stu-id="db219-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="db219-111">Per un maggiore controllo sulla distribuzione, è possibile eseguire l'override di script di distribuzione predefinito hello creando hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="db219-111">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="db219-112">È possibile utilizzare hello [interfaccia della riga di comando di Azure] [ Azure command-line interface] file hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="db219-112">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="db219-113">Usare questo comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="db219-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="db219-114">Se questi file non esistono, Azure creerà uno script di distribuzione temporaneo e lo eseguirà.</span><span class="sxs-lookup"><span data-stu-id="db219-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="db219-115">È identico toohello quello che si crea con hello comando precedente.</span><span class="sxs-lookup"><span data-stu-id="db219-115">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
