## <a name="overview"></a><span data-ttu-id="d5806-101">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d5806-101">Overview</span></span>

<span data-ttu-id="d5806-102">In questa esercitazione è completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d5806-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="d5806-103">Distribuire un'istanza di hello remoto monitoraggio soluzione preconfigurata tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5806-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="d5806-104">Questo passaggio distribuisce e configura automaticamente più servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5806-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="d5806-105">Consente di impostare toocommunicate il dispositivo con il computer e una soluzione di monitoraggio remoto hello.</span><span class="sxs-lookup"><span data-stu-id="d5806-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="d5806-106">Aggiornare hello esempio dispositivo codice tooconnect toohello soluzione di monitoraggio remoto e inviare dati di telemetria simulati che è possibile visualizzare nel dashboard di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="d5806-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5806-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5806-107">Prerequisites</span></span>

<span data-ttu-id="d5806-108">toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="d5806-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="d5806-109">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d5806-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d5806-110">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="d5806-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="d5806-111">Requisiti software</span><span class="sxs-lookup"><span data-stu-id="d5806-111">Required software</span></span>

<span data-ttu-id="d5806-112">È necessario client SSH nel tooenable computer desktop è tooremotely accesso hello della riga di comando in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d5806-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="d5806-113">Windows non include un client SSH.</span><span class="sxs-lookup"><span data-stu-id="d5806-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="d5806-114">È consigliabile usare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="d5806-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="d5806-115">La maggior parte delle distribuzioni di Linux e Mac OS includono hello della riga di comando SSH utilità.</span><span class="sxs-lookup"><span data-stu-id="d5806-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="d5806-116">Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="d5806-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="d5806-117">Requisiti hardware</span><span class="sxs-lookup"><span data-stu-id="d5806-117">Required hardware</span></span>

<span data-ttu-id="d5806-118">Un computer desktop di tooenable tooconnect è in modalità remota toohello della riga di comando in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="d5806-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="d5806-119">[Starter kit di Microsoft Azure IoT per Raspberry Pi 3][lnk-starter-kits] o componenti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="d5806-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="d5806-120">Questa esercitazione vengono utilizzati i seguenti elementi del kit di hello hello:</span><span class="sxs-lookup"><span data-stu-id="d5806-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="d5806-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="d5806-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="d5806-122">Scheda microSD (con NOOBS)</span><span class="sxs-lookup"><span data-stu-id="d5806-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="d5806-123">Un cavo USB mini</span><span class="sxs-lookup"><span data-stu-id="d5806-123">A USB Mini cable</span></span>
- <span data-ttu-id="d5806-124">Un cavo Ethernet</span><span class="sxs-lookup"><span data-stu-id="d5806-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/