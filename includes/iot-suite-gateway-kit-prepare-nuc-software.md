## <a name="build-iot-edge"></a><span data-ttu-id="46987-101">Compilare IoT Edge</span><span class="sxs-lookup"><span data-stu-id="46987-101">Build IoT Edge</span></span>

<span data-ttu-id="46987-102">Questa esercitazione Usa personalizzata bordo IoT moduli toocommunicate con hello soluzione preconfigurata di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="46987-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="46987-103">Pertanto, è necessario moduli di Edge IoT hello toobuild dal codice sorgente personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46987-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="46987-104">Hello le sezioni seguenti descrivono come tooinstall IoT Edge e compilazione hello modulo IoT bordo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="46987-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="46987-105">Installare IoT Edge</span><span class="sxs-lookup"><span data-stu-id="46987-105">Install IoT Edge</span></span>

<span data-ttu-id="46987-106">Hello passaggi seguenti descrivono come tooinstall hello precompilato software IoT bordo su hello NUC Intel:</span><span class="sxs-lookup"><span data-stu-id="46987-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="46987-107">Configurare repository pacchetto smart hello necessario eseguendo hello seguendo i comandi hello NUC Intel:</span><span class="sxs-lookup"><span data-stu-id="46987-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="46987-108">Immettere `y` quando hello comando richiede troppo**includere questo canale?**.</span><span class="sxs-lookup"><span data-stu-id="46987-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="46987-109">Gestione aggiornamenti hello smart pacchetto eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="46987-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="46987-110">Installare il pacchetto di Azure IoT Edge hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="46987-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="46987-111">Verificare l'installazione di hello, in esecuzione: esempio hello "Hello world".</span><span class="sxs-lookup"><span data-stu-id="46987-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="46987-112">In questo esempio scrive un file di log. txt hello world messaggio toohello ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="46987-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="46987-113">Hello eseguire i comandi seguenti: esempio hello "Hello world":</span><span class="sxs-lookup"><span data-stu-id="46987-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="46987-114">Ignora modifiche **argomento non valido** messaggi quando si arresta l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="46987-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="46987-115">Comando che segue di hello utilizzare contenuto hello tooview hello del file di log:</span><span class="sxs-lookup"><span data-stu-id="46987-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="46987-116">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="46987-116">Troubleshooting</span></span>

<span data-ttu-id="46987-117">Se viene visualizzato l'errore hello "alcun pacchetto vengono fornite util-linux-dev", provare a riavviare hello NUC Intel.</span><span class="sxs-lookup"><span data-stu-id="46987-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
