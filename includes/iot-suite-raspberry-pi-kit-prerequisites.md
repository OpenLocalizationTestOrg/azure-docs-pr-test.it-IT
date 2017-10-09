## <a name="prerequisites"></a><span data-ttu-id="93b41-101">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="93b41-101">Prerequisites</span></span>

<span data-ttu-id="93b41-102">toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="93b41-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="93b41-103">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="93b41-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="93b41-104">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="93b41-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="93b41-105">Requisiti software</span><span class="sxs-lookup"><span data-stu-id="93b41-105">Required software</span></span>

<span data-ttu-id="93b41-106">È necessario client SSH nel tooenable computer desktop è tooremotely accesso hello della riga di comando in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="93b41-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="93b41-107">Windows non include un client SSH.</span><span class="sxs-lookup"><span data-stu-id="93b41-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="93b41-108">È consigliabile usare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="93b41-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="93b41-109">La maggior parte delle distribuzioni di Linux e Mac OS includono hello della riga di comando SSH utilità.</span><span class="sxs-lookup"><span data-stu-id="93b41-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="93b41-110">Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="93b41-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="93b41-111">Requisiti hardware</span><span class="sxs-lookup"><span data-stu-id="93b41-111">Required hardware</span></span>

<span data-ttu-id="93b41-112">Un computer desktop di tooenable tooconnect è in modalità remota toohello della riga di comando in hello Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="93b41-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="93b41-113">[Starter kit di Microsoft Azure IoT per Raspberry Pi 3][lnk-starter-kits] o componenti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="93b41-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="93b41-114">Questa esercitazione vengono utilizzati i seguenti elementi del kit di hello hello:</span><span class="sxs-lookup"><span data-stu-id="93b41-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="93b41-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="93b41-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="93b41-116">Scheda microSD (con NOOBS)</span><span class="sxs-lookup"><span data-stu-id="93b41-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="93b41-117">Un cavo USB mini</span><span class="sxs-lookup"><span data-stu-id="93b41-117">A USB Mini cable</span></span>
- <span data-ttu-id="93b41-118">Un cavo Ethernet</span><span class="sxs-lookup"><span data-stu-id="93b41-118">An Ethernet cable</span></span>
- <span data-ttu-id="93b41-119">Sensore BME280</span><span class="sxs-lookup"><span data-stu-id="93b41-119">BME280 sensor</span></span>
- <span data-ttu-id="93b41-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="93b41-120">Breadboard</span></span>
- <span data-ttu-id="93b41-121">Cavi ponticello</span><span class="sxs-lookup"><span data-stu-id="93b41-121">Jumper wires</span></span>
- <span data-ttu-id="93b41-122">Resistori</span><span class="sxs-lookup"><span data-stu-id="93b41-122">Resistors</span></span>
- <span data-ttu-id="93b41-123">LED</span><span class="sxs-lookup"><span data-stu-id="93b41-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/