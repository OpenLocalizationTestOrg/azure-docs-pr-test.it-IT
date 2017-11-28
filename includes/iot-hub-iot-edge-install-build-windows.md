## <a name="install-the-prerequisites"></a><span data-ttu-id="6e943-101">Installare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6e943-101">Install the prerequisites</span></span>

1. <span data-ttu-id="6e943-102">Installare [Visual Studio 2015 o 2017](https://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6e943-102">Install [Visual Studio 2015 or 2017](https://www.visualstudio.com).</span></span> <span data-ttu-id="6e943-103">Se si soddisfano i requisiti di licenza, è possibile usare la versione gratuita Community Edition.</span><span class="sxs-lookup"><span data-stu-id="6e943-103">You can use the free Community Edition if you meet the licensing requirements.</span></span> <span data-ttu-id="6e943-104">Assicurarsi di includere Visual C++ e Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="6e943-104">Be sure to include Visual C++ and NuGet Package Manager.</span></span>

1. <span data-ttu-id="6e943-105">Installare [git](http://www.git-scm.com) e verificare di riuscire a eseguire git.exe dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6e943-105">Install [git](http://www.git-scm.com) and make sure you can run git.exe from the command line.</span></span>

1. <span data-ttu-id="6e943-106">Installare [CMake](https://cmake.org/download/) e verificare di riuscire a eseguire cmake.exe dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6e943-106">Install [CMake](https://cmake.org/download/) and make sure you can run cmake.exe from the command line.</span></span> <span data-ttu-id="6e943-107">È consigliabile usare CMake versione 3.7.2 o successive.</span><span class="sxs-lookup"><span data-stu-id="6e943-107">CMake version 3.7.2 or later is recommended.</span></span> <span data-ttu-id="6e943-108">Il programma di installazione **.msi** è l'opzione più semplice in Windows.</span><span class="sxs-lookup"><span data-stu-id="6e943-108">The **.msi** installer is the easiest option on Windows.</span></span> <span data-ttu-id="6e943-109">Aggiungere CMake alla variabile di ambiente PATH almeno per l'utente corrente quando viene dal programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="6e943-109">Add CMake to the PATH for at least the current user when the installer prompts you.</span></span>

1. <span data-ttu-id="6e943-110">Installare [Python 2.7](https://www.python.org/downloads/release/python-27).</span><span class="sxs-lookup"><span data-stu-id="6e943-110">Install [Python 2.7](https://www.python.org/downloads/release/python-27).</span></span> <span data-ttu-id="6e943-111">Assicurarsi di aggiungere Python alla variabile di ambiente `PATH` in **Pannello di controllo -> Sistema -> Impostazioni di sistema avanzate -> Variabili di ambiente**.</span><span class="sxs-lookup"><span data-stu-id="6e943-111">Make sure you add Python to your `PATH` environment variable in **Control Panel -> System -> Advanced system settings -> Environment Variables**.</span></span>

1. <span data-ttu-id="6e943-112">Al prompt dei comandi, eseguire il comando seguente per clonare il repository GitHub Azure IoT Edge nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="6e943-112">At a command prompt, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

    ```cmd
    git clone https://github.com/Azure/iot-edge.git
    ```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="6e943-113">Come compilare l'esempio</span><span class="sxs-lookup"><span data-stu-id="6e943-113">How to build the sample</span></span>

<span data-ttu-id="6e943-114">È ora possibile compilare il runtime e gli esempi di IoT Edge nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="6e943-114">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="6e943-115">Aprire un **prompt dei comandi per gli sviluppatori per VS 2015** o un **prompt dei comandi per gli sviluppatori per VS 2017**.</span><span class="sxs-lookup"><span data-stu-id="6e943-115">Open a **Developer Command Prompt for VS 2015** or **Developer Command Prompt for VS 2017** command prompt.</span></span>

1. <span data-ttu-id="6e943-116">Accedere alla cartella radice nella copia locale del repository **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="6e943-116">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="6e943-117">Eseguire lo script di compilazione come segue:</span><span class="sxs-lookup"><span data-stu-id="6e943-117">Run the build script as follows:</span></span>

    ```cmd
    tools\build.cmd --disable-native-remote-modules
    ```

<span data-ttu-id="6e943-118">Questo script crea un file di soluzione Visual Studio e compila la soluzione.</span><span class="sxs-lookup"><span data-stu-id="6e943-118">This script creates a Visual Studio solution file and builds the solution.</span></span> <span data-ttu-id="6e943-119">È possibile trovare la soluzione di Visual Studio nella cartella **build** nella copia locale del repository **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="6e943-119">You can find the Visual Studio solution in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="6e943-120">Per compilare ed eseguire unit test, aggiungere il parametro `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="6e943-120">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="6e943-121">Per compilare ed eseguire test end-to-end, aggiungere il parametro `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="6e943-121">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="6e943-122">Ogni volta che si esegue lo script **build.cmd**, la cartella **build** viene eliminata e ricreata nella cartella radice della copia locale del repository **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="6e943-122">Every time you run the **build.cmd** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>