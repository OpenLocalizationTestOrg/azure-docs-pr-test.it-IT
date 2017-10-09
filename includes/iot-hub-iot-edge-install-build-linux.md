## <a name="install-hello-prerequisites"></a><span data-ttu-id="9eb97-101">Installare i prerequisiti di hello</span><span class="sxs-lookup"><span data-stu-id="9eb97-101">Install hello prerequisites</span></span>

<span data-ttu-id="9eb97-102">passaggi di Hello in questa esercitazione si presuppone il che uso Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="9eb97-102">hello steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="9eb97-103">Aprire una shell ed eseguire i seguenti pacchetti dei prerequisiti di comandi tooinstall hello hello:</span><span class="sxs-lookup"><span data-stu-id="9eb97-103">Open a shell and run hello following commands tooinstall hello prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="9eb97-104">Nella shell di hello, eseguire hello successivo comando tooclone hello Azure IoT Edge GitHub repository tooyour locale:</span><span class="sxs-lookup"><span data-stu-id="9eb97-104">In hello shell, run hello following command tooclone hello Azure IoT Edge GitHub repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-toobuild-hello-sample"></a><span data-ttu-id="9eb97-105">Come toobuild hello esempio</span><span class="sxs-lookup"><span data-stu-id="9eb97-105">How toobuild hello sample</span></span>

<span data-ttu-id="9eb97-106">È ora possibile generare hello IoT Edge runtime ed esempi sul computer locale:</span><span class="sxs-lookup"><span data-stu-id="9eb97-106">You can now build hello IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="9eb97-107">Aprire una shell.</span><span class="sxs-lookup"><span data-stu-id="9eb97-107">Open a shell.</span></span>

1. <span data-ttu-id="9eb97-108">Esplorazione delle cartelle radice toohello nella copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="9eb97-108">Navigate toohello root folder in your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="9eb97-109">Eseguire lo script di compilazione come segue:</span><span class="sxs-lookup"><span data-stu-id="9eb97-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="9eb97-110">Questo script utilizza il **cmake** toocreate utilità una cartella denominata **compilare** nella cartella radice hello della copia locale del **iot edge** repository e generare un makefile.</span><span class="sxs-lookup"><span data-stu-id="9eb97-110">This script uses the **cmake** utility toocreate a folder called **build** in hello root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="9eb97-111">script Hello quindi compila la soluzione hello, ignorando gli unit test e tooend fine.</span><span class="sxs-lookup"><span data-stu-id="9eb97-111">hello script then builds hello solution, skipping unit tests and end tooend tests.</span></span> <span data-ttu-id="9eb97-112">Se si desidera toobuild e hello unit test, aggiungere hello `--run-unittests` parametro.</span><span class="sxs-lookup"><span data-stu-id="9eb97-112">If you want toobuild and run hello unit tests, add hello `--run-unittests` parameter.</span></span> <span data-ttu-id="9eb97-113">Se si desidera toobuild ed eseguire i test di tooend hello fine, aggiungere hello `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="9eb97-113">If you want toobuild and run hello end tooend tests, add hello `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="9eb97-114">Ogni volta che si esegue hello **build.sh** script, Elimina e ricrea quindi hello **compilare** cartella nella cartella radice hello della copia locale di hello **iot edge** repository.</span><span class="sxs-lookup"><span data-stu-id="9eb97-114">Every time you run hello **build.sh** script, it deletes and then recreates hello **build** folder in hello root folder of your local copy of hello **iot-edge** repository.</span></span>
