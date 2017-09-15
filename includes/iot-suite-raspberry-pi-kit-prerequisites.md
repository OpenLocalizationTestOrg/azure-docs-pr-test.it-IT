## <a name="prerequisites"></a><span data-ttu-id="a5e9e-101">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a5e9e-101">Prerequisites</span></span>

<span data-ttu-id="a5e9e-102">Per completare l'esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a5e9e-103">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a5e9e-104">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="a5e9e-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="a5e9e-105">Requisiti software</span><span class="sxs-lookup"><span data-stu-id="a5e9e-105">Required software</span></span>

<span data-ttu-id="a5e9e-106">È necessario un client SSH nel computer desktop per poter accedere in remoto alla riga di comando in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Raspberry Pi.</span></span>

- <span data-ttu-id="a5e9e-107">Windows non include un client SSH.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="a5e9e-108">È consigliabile usare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="a5e9e-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="a5e9e-109">La maggior parte delle distribuzioni Linux e Mac OS includono l'utilità SSH della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span> <span data-ttu-id="a5e9e-110">Per altre informazioni, vedere [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH con Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="a5e9e-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="a5e9e-111">Requisiti hardware</span><span class="sxs-lookup"><span data-stu-id="a5e9e-111">Required hardware</span></span>

<span data-ttu-id="a5e9e-112">Un computer desktop per potersi connettere in remoto alla riga di comando in Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-112">A desktop computer to enable you to connect remotely to the command line on the Raspberry Pi.</span></span>

<span data-ttu-id="a5e9e-113">[Starter kit di Microsoft Azure IoT per Raspberry Pi 3][lnk-starter-kits] o componenti equivalenti.</span><span class="sxs-lookup"><span data-stu-id="a5e9e-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="a5e9e-114">Questa esercitazione usa gli elementi seguenti del kit:</span><span class="sxs-lookup"><span data-stu-id="a5e9e-114">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="a5e9e-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="a5e9e-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="a5e9e-116">Scheda microSD (con NOOBS)</span><span class="sxs-lookup"><span data-stu-id="a5e9e-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="a5e9e-117">Un cavo USB mini</span><span class="sxs-lookup"><span data-stu-id="a5e9e-117">A USB Mini cable</span></span>
- <span data-ttu-id="a5e9e-118">Un cavo Ethernet</span><span class="sxs-lookup"><span data-stu-id="a5e9e-118">An Ethernet cable</span></span>
- <span data-ttu-id="a5e9e-119">Sensore BME280</span><span class="sxs-lookup"><span data-stu-id="a5e9e-119">BME280 sensor</span></span>
- <span data-ttu-id="a5e9e-120">Breadboard</span><span class="sxs-lookup"><span data-stu-id="a5e9e-120">Breadboard</span></span>
- <span data-ttu-id="a5e9e-121">Cavi ponticello</span><span class="sxs-lookup"><span data-stu-id="a5e9e-121">Jumper wires</span></span>
- <span data-ttu-id="a5e9e-122">Resistori</span><span class="sxs-lookup"><span data-stu-id="a5e9e-122">Resistors</span></span>
- <span data-ttu-id="a5e9e-123">LED</span><span class="sxs-lookup"><span data-stu-id="a5e9e-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/