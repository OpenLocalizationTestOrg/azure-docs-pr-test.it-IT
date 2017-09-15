## <a name="install-the-prerequisites"></a><span data-ttu-id="01e93-101">Installare i prerequisiti</span><span class="sxs-lookup"><span data-stu-id="01e93-101">Install the prerequisites</span></span>

<span data-ttu-id="01e93-102">Per i passaggi di questa esercitazione si presuppone che sia in esecuzione Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="01e93-102">The steps in this tutorial assume you are running Ubuntu Linux.</span></span>

<span data-ttu-id="01e93-103">Aprire una shell ed eseguire i comandi seguenti per installare i pacchetti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="01e93-103">Open a shell and run the following commands to install the prerequisite packages:</span></span>

```bash
sudo apt-get update
sudo apt-get install curl build-essential libcurl4-openssl-dev git cmake libssl-dev uuid-dev valgrind libglib2.0-dev libtool autoconf
```

<span data-ttu-id="01e93-104">Nella shell eseguire il comando seguente per clonare il repository GitHub Azure IoT Edge nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="01e93-104">In the shell, run the following command to clone the Azure IoT Edge GitHub repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure/iot-edge.git
```

## <a name="how-to-build-the-sample"></a><span data-ttu-id="01e93-105">Come compilare l'esempio</span><span class="sxs-lookup"><span data-stu-id="01e93-105">How to build the sample</span></span>

<span data-ttu-id="01e93-106">È ora possibile compilare il runtime e gli esempi di IoT Edge nel computer locale:</span><span class="sxs-lookup"><span data-stu-id="01e93-106">You can now build the IoT Edge runtime and samples on your local machine:</span></span>

1. <span data-ttu-id="01e93-107">Aprire una shell.</span><span class="sxs-lookup"><span data-stu-id="01e93-107">Open a shell.</span></span>

1. <span data-ttu-id="01e93-108">Accedere alla cartella radice nella copia locale del repository **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="01e93-108">Navigate to the root folder in your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="01e93-109">Eseguire lo script di compilazione come segue:</span><span class="sxs-lookup"><span data-stu-id="01e93-109">Run the build script as follows:</span></span>

    ```sh
    tools/build.sh --disable-native-remote-modules
    ```

<span data-ttu-id="01e93-110">Questo script usa l'utilità **cmake** per creare una cartella denominata **build** nella cartella radice della copia locale del repository **iot-edge** e generare un makefile.</span><span class="sxs-lookup"><span data-stu-id="01e93-110">This script uses the **cmake** utility to create a folder called **build** in the root folder of your local copy of the **iot-edge** repository and generate a makefile.</span></span> <span data-ttu-id="01e93-111">Lo script quindi compila la soluzione senza eseguire i test dell'unità e i test end-to-end.</span><span class="sxs-lookup"><span data-stu-id="01e93-111">The script then builds the solution, skipping unit tests and end to end tests.</span></span> <span data-ttu-id="01e93-112">Per compilare ed eseguire unit test, aggiungere il parametro `--run-unittests`.</span><span class="sxs-lookup"><span data-stu-id="01e93-112">If you want to build and run the unit tests, add the `--run-unittests` parameter.</span></span> <span data-ttu-id="01e93-113">Per compilare ed eseguire test end-to-end, aggiungere il parametro `--run-e2e-tests`.</span><span class="sxs-lookup"><span data-stu-id="01e93-113">If you want to build and run the end to end tests, add the `--run-e2e-tests`.</span></span>

> [!NOTE]
> <span data-ttu-id="01e93-114">Ogni volta che si esegue lo script **build.sh**, la cartella **build** viene eliminata e ricreata nella cartella radice della copia locale del repository **iot-edge**.</span><span class="sxs-lookup"><span data-stu-id="01e93-114">Every time you run the **build.sh** script, it deletes and then recreates the **build** folder in the root folder of your local copy of the **iot-edge** repository.</span></span>