> [!div class="op_single_selector"]
> * [<span data-ttu-id="418c1-101">Linux</span><span class="sxs-lookup"><span data-stu-id="418c1-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="418c1-102">Windows</span><span class="sxs-lookup"><span data-stu-id="418c1-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="418c1-103">Questo articolo fornisce una descrizione dettagliata di hello [codice di esempio Hello World] [ lnk-helloworld-sample] tooillustrate componenti fondamentali di hello di hello [Azure IoT Edge] [ lnk-iot-edge] architettura.</span><span class="sxs-lookup"><span data-stu-id="418c1-103">This article provides a detailed walkthrough of hello [Hello World sample code][lnk-helloworld-sample] tooillustrate hello fundamental components of hello [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="418c1-104">Hello esempio utilizza hello Azure IoT Edge toobuild un gateway semplice che consente di registrare un file di tooa messaggio "hello world" ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="418c1-104">hello sample uses hello Azure IoT Edge toobuild a simple gateway that logs a "hello world" message tooa file every five seconds.</span></span>

<span data-ttu-id="418c1-105">In questa procedura dettagliata verranno trattati i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="418c1-105">This walkthrough covers:</span></span>

* <span data-ttu-id="418c1-106">**Architettura di esempio World Hello**: descrive come [concetti dell'architettura di Azure IoT Edge] [ lnk-edge-concepts] si applicano all'esempio Hello World toohello e la modalità di interazione fra di hello componenti.</span><span class="sxs-lookup"><span data-stu-id="418c1-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply toohello Hello World sample and how hello components fit together.</span></span>
* <span data-ttu-id="418c1-107">**Come toobuild hello esempio**: esempio hello toobuild necessari passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="418c1-107">**How toobuild hello sample**: hello steps required toobuild hello sample.</span></span>
* <span data-ttu-id="418c1-108">**Come toorun hello esempio**: esempio hello toorun necessari passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="418c1-108">**How toorun hello sample**: hello steps required toorun hello sample.</span></span> 
* <span data-ttu-id="418c1-109">**Output tipico**: un esempio di hello output tooexpect quando si esegue l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="418c1-109">**Typical output**: An example of hello output tooexpect when you run hello sample.</span></span>
* <span data-ttu-id="418c1-110">**Frammenti di codice**: una raccolta di tooshow di frammenti di codice come esempio hello World Hello implementa i componenti di gateway di IoT Edge di chiave.</span><span class="sxs-lookup"><span data-stu-id="418c1-110">**Code snippets**: A collection of code snippets tooshow how hello Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="418c1-111">Architettura di esempio Hello World</span><span class="sxs-lookup"><span data-stu-id="418c1-111">Hello World sample architecture</span></span>
<span data-ttu-id="418c1-112">esempio Hello World Hello illustra i concetti di hello descritti nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="418c1-112">hello Hello World sample illustrates hello concepts described in hello previous section.</span></span> <span data-ttu-id="418c1-113">esempio Hello World Hello implementa un gateway perimetrale di IoT che dispone di una pipeline costituita da due moduli IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="418c1-113">hello Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="418c1-114">Hello *HelloWorld* modulo Crea un messaggio ogni cinque secondi e lo passa a modulo logger toohello.</span><span class="sxs-lookup"><span data-stu-id="418c1-114">hello *hello world* module creates a message every five seconds and passes it toohello logger module.</span></span>
* <span data-ttu-id="418c1-115">Hello *logger* modulo scritture hello i messaggi ricevuti tooa file.</span><span class="sxs-lookup"><span data-stu-id="418c1-115">hello *logger* module writes hello messages it receives tooa file.</span></span>

![Architettura dell'esempio Hello World compilato con Azure IoT Edge][4]

<span data-ttu-id="418c1-117">Come descritto nella sezione precedente di hello, hello World Hello modulo non fa passare messaggi direttamente modulo logger toohello ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="418c1-117">As described in hello previous section, hello Hello World module does not pass messages directly toohello logger module every five seconds.</span></span> <span data-ttu-id="418c1-118">Al contrario, pubblica un gestore di messaggi toohello ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="418c1-118">Instead, it publishes a message toohello broker every five seconds.</span></span>

<span data-ttu-id="418c1-119">modulo di logger Hello riceve il messaggio hello dal broker hello e agisce su di esso, scrivere il contenuto del file di tooa hello messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="418c1-119">hello logger module receives hello message from hello broker and acts upon it, writing hello contents of hello message tooa file.</span></span>

<span data-ttu-id="418c1-120">modulo di logger Hello utilizza solo i messaggi da Service broker hello, non pubblicarlo mai broker di toohello nuovi messaggi.</span><span class="sxs-lookup"><span data-stu-id="418c1-120">hello logger module only consumes messages from hello broker, it never publishes new messages toohello broker.</span></span>

![Come broker hello indirizza i messaggi tra i moduli in Azure IoT Edge][5]

<span data-ttu-id="418c1-122">Hello figura precedente hello architettura di esempio hello World Hello e i percorsi relativi hello toohello i file di origine che implementano le parti diverse dell'esempio hello in hello [repository][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="418c1-122">hello figure above shows hello architecture of hello Hello World sample and hello relative paths toohello source files that implement different portions of hello sample in hello [repository][lnk-iot-edge].</span></span> <span data-ttu-id="418c1-123">Esplorare il codice hello autonomamente oppure usare frammenti di codice hello seguente come guida.</span><span class="sxs-lookup"><span data-stu-id="418c1-123">Explore hello code on your own, or use hello code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md