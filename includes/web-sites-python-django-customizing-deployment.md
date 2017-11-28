<span data-ttu-id="bdade-101">Per stabilire se l'applicazione usa Python, Azure verifica se **entrambe le condizioni seguenti sono soddisfatte**:</span><span class="sxs-lookup"><span data-stu-id="bdade-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="bdade-102">Presenza del file requirements.txt nella cartella radice</span><span class="sxs-lookup"><span data-stu-id="bdade-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="bdade-103">Presenza di un qualsiasi file .py nella cartella radice OPPURE di un file runtime.txt in cui viene specificato python</span><span class="sxs-lookup"><span data-stu-id="bdade-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="bdade-104">In tale circostanza, userà uno script di distribuzione specifico di Python che eseguirà la sincronizzazione standard dei file, oltre ad operazioni aggiuntive di Python, tra cui:</span><span class="sxs-lookup"><span data-stu-id="bdade-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="bdade-105">Gestione automatica dell'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="bdade-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="bdade-106">Installazione dei pacchetti elencati in requirements.txt tramite pip</span><span class="sxs-lookup"><span data-stu-id="bdade-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="bdade-107">Creazione del file web.config appropriato sulla base della versione di Python selezionata</span><span class="sxs-lookup"><span data-stu-id="bdade-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="bdade-108">Raccolta di file statici per le applicazioni Django</span><span class="sxs-lookup"><span data-stu-id="bdade-108">Collect static files for Django applications</span></span>

<span data-ttu-id="bdade-109">È possibile controllare determinati aspetti della procedura di distribuzione predefinita senza dover personalizzare lo script.</span><span class="sxs-lookup"><span data-stu-id="bdade-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="bdade-110">Per ignorare tutti i passaggi della distribuzione specifici di Python, è possibile creare questo file vuoto:</span><span class="sxs-lookup"><span data-stu-id="bdade-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="bdade-111">Per ignorare la raccolta dei file statici per l'applicazione Django:</span><span class="sxs-lookup"><span data-stu-id="bdade-111">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="bdade-112">Per un maggiore controllo sulla distribuzione, è possibile eseguire l'override dello script di distribuzione predefinito creando i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdade-112">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="bdade-113">È possibile utilizzare il [interfaccia della riga di comando di Azure] [ Azure command-line interface] per creare i file.</span><span class="sxs-lookup"><span data-stu-id="bdade-113">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="bdade-114">Usare questo comando dalla cartella del progetto:</span><span class="sxs-lookup"><span data-stu-id="bdade-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="bdade-115">Se questi file non esistono, Azure creerà uno script di distribuzione temporaneo e lo eseguirà.</span><span class="sxs-lookup"><span data-stu-id="bdade-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="bdade-116">Tale file è identico a quello creato con il comando precedente.</span><span class="sxs-lookup"><span data-stu-id="bdade-116">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
