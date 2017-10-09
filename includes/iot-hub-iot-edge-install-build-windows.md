## <a name="install-hello-prerequisites"></a><span data-ttu-id="caeb2-101">Installare i prerequisiti di hello</span><span class="sxs-lookup"><span data-stu-id="caeb2-101">Install hello prerequisites</span></span>

1. <span data-ttu-id="caeb2-102">Installare [Visual Studio 2015 o 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="caeb2-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="caeb2-103">È possibile utilizzare hello libero Community Edition se vengono soddisfatti i requisiti di licenza hello.</span><span class="sxs-lookup"><span data-stu-id="caeb2-103">You can use hello free Community Edition if you meet hello licensing requirements.</span></span> <span data-ttu-id="caeb2-104">Essere tooinclude che Visual C++ e gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="caeb2-104">Be sure tooinclude Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="caeb2-105">Installare [git](http://www.git-scm.com) e assicurarsi che sia possibile eseguire git.exe dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="caeb2-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from hello command line.</span></span>

1. <span data-ttu-id="caeb2-106">Installare [CMake](https://cmake.org/download/) e assicurarsi che sia possibile eseguire cmake.exe dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="caeb2-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from hello command line.</span></span> <span data-ttu-id="caeb2-107">È consigliabile usare CMake versione 3.7.2 o successive.</span><span class="sxs-lookup"><span data-stu-id="caeb2-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="caeb2-108">Hello **con estensione msi** programma di installazione è l'opzione più semplice di hello in Windows.</span><span class="sxs-lookup"><span data-stu-id="caeb2-108">hello **.msi** installer is hello easiest option on Windows.</span></span> <span data-ttu-id="caeb2-109">Aggiungere CMake toohello percorso per hello almeno l'utente corrente quando viene richiesto dal programma di installazione hello.</span><span class="sxs-lookup"><span data-stu-id="caeb2-109">Add CMake toohello PATH for at least hello current user when hello installer prompts you.</span></span>

1. <span data-ttu-id="caeb2-110">Installare [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="caeb2-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="caeb2-111">Assicurarsi di aggiungere Python tooyour `PATH` variabile di ambiente nel **Pannello di controllo -> sistema -> avanzate le impostazioni di sistema -> variabili di ambiente**.</span><span class="sxs-lookup"><span data-stu-id="caeb2-111">Make sure you add Python tooyour `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="caeb2-112">Al prompt dei comandi, eseguire hello comando tooclone hello Azure IoT Edge GitHub repository tooyour locali seguenti:</span><span class="sxs-lookup"><span data-stu-id="caeb2-112">At a command prompt, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="caeb2-113">Come toobuild hello esempio</span><span class="sxs-lookup"><span data-stu-id="caeb2-113">How toobuild hello sample</span></span>

<span data-ttu-id="caeb2-114">È ora possibile generare hello IoT Edge runtime ed esempi sul computer locale:</span><span class="sxs-lookup"><span data-stu-id="caeb2-114">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="caeb2-115">Aprire un **prompt dei comandi per gli sviluppatori per VS 2015** o un **prompt dei comandi per gli sviluppatori per VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="caeb2-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="caeb2-116">Esplorazione delle cartelle radice toohello nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="caeb2-116">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="caeb2-117">Eseguire lo script di compilazione come segue:</span><span class="sxs-lookup"><span data-stu-id="caeb2-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="caeb2-118">Questo script crea un file di soluzione di Visual Studio e compila la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="caeb2-118">This script creates a Visual Studio solution file and builds hello solution.</span></span> <span data-ttu-id="caeb2-119">È possibile trovare una soluzione di Visual Studio hello in hello **compilare** cartella nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="caeb2-119">You can find hello Visual Studio solution in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="caeb2-120">Se si desidera toobuild e hello unit test, aggiungere hello `--run-unittests` parametro.</span><span class="sxs-lookup"><span data-stu-id="caeb2-120">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="caeb2-121">Se si desidera toobuild ed eseguire i test di tooend hello fine, aggiungere hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="caeb2-121">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="caeb2-122">Ogni volta che si esegue hello **build.cmd** script, Elimina e ricrea quindi hello **compilare** cartella nella cartella radice hello della copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="caeb2-122">Every time you run hello **build.cmd** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
