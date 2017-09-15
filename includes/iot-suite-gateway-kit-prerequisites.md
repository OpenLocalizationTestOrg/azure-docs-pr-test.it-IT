## <a name="prerequisites"></a><span data-ttu-id="2ecd0-101">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ecd0-101">Prerequisites</span></span>

<span data-ttu-id="2ecd0-102">Per completare l'esercitazione, è necessaria una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="2ecd0-102">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="2ecd0-103">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2ecd0-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ecd0-104">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="2ecd0-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="2ecd0-105">Requisiti software</span><span class="sxs-lookup"><span data-stu-id="2ecd0-105">Required software</span></span>

<span data-ttu-id="2ecd0-106">È necessario un client SSH nel computer desktop per poter accedere in remoto alla riga di comando in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2ecd0-106">You need SSH client on your desktop machine to enable you to remotely access the command line on the Intel NUC.</span></span>

- <span data-ttu-id="2ecd0-107">Windows non include un client SSH.</span><span class="sxs-lookup"><span data-stu-id="2ecd0-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="2ecd0-108">È consigliabile usare [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="2ecd0-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="2ecd0-109">La maggior parte delle distribuzioni Linux e Mac OS includono l'utilità SSH della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="2ecd0-109">Most Linux distributions and Mac OS include the command-line SSH utility.</span></span>

### <a name="required-hardware"></a><span data-ttu-id="2ecd0-110">Requisiti hardware</span><span class="sxs-lookup"><span data-stu-id="2ecd0-110">Required hardware</span></span>

<span data-ttu-id="2ecd0-111">Un computer desktop per potersi connettere in remoto alla riga di comando in Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="2ecd0-111">A desktop computer to enable you to connect remotely to the command line on the Intel NUC.</span></span>

<span data-ttu-id="2ecd0-112">[Kit gateway commerciale IoT][lnk-starter-kits].</span><span class="sxs-lookup"><span data-stu-id="2ecd0-112">[IoT Commercial Gateway Kit][lnk-starter-kits].</span></span> <span data-ttu-id="2ecd0-113">Questa esercitazione usa gli elementi seguenti del kit:</span><span class="sxs-lookup"><span data-stu-id="2ecd0-113">This tutorial uses the following items from the kit:</span></span>

- <span data-ttu-id="2ecd0-114">Intel® NUC Kit DE3815TYKE con 4 GB di memoria e scheda di espansione Bluetooth</span><span class="sxs-lookup"><span data-stu-id="2ecd0-114">Intel® NUC Kit DE3815TYKE with 4G Memory and Bluetooth expansion card</span></span>
- <span data-ttu-id="2ecd0-115">Alimentatore</span><span class="sxs-lookup"><span data-stu-id="2ecd0-115">Power adaptor</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/