> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0d45-101">Linux</span><span class="sxs-lookup"><span data-stu-id="e0d45-101">Linux</span></span>](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [<span data-ttu-id="e0d45-102">Windows</span><span class="sxs-lookup"><span data-stu-id="e0d45-102">Windows</span></span>](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

<span data-ttu-id="e0d45-103">Questo articolo descrive la procedura dettagliata del [codice di esempio Hello World][lnk-helloworld-sample] per illustrare i componenti fondamentali dell'architettura di [Azure IoT Edge][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="e0d45-103">This article provides a detailed walkthrough of the [Hello World sample code][lnk-helloworld-sample] to illustrate the fundamental components of the [Azure IoT Edge][lnk-iot-edge] architecture.</span></span> <span data-ttu-id="e0d45-104">L'esempio usa Azure IoT Edge per creare un gateway semplice che registri un messaggio "hello world" in un file ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="e0d45-104">The sample uses the Azure IoT Edge to build a simple gateway that logs a "hello world" message to a file every five seconds.</span></span>

<span data-ttu-id="e0d45-105">In questa procedura dettagliata verranno trattati i seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="e0d45-105">This walkthrough covers:</span></span>

* <span data-ttu-id="e0d45-106">**Architettura di esempio Hello World**: descrive in che modo si applicano i [concetti dell'architettura di Azure IoT Edge][lnk-edge-concepts] all'esempio Hello World e come vengono assemblati i componenti.</span><span class="sxs-lookup"><span data-stu-id="e0d45-106">**Hello World sample architecture**: Describes how [Azure IoT Edge architectural concepts][lnk-edge-concepts] apply to the Hello World sample and how the components fit together.</span></span>
* <span data-ttu-id="e0d45-107">**Come compilare l'esempio**: i passaggi richiesti per compilare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e0d45-107">**How to build the sample**: The steps required to build the sample.</span></span>
* <span data-ttu-id="e0d45-108">**Come eseguire l'esempio**: i passaggi richiesti per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e0d45-108">**How to run the sample**: The steps required to run the sample.</span></span> 
* <span data-ttu-id="e0d45-109">**Output tipico**: un esempio del possibile output risultante quando si esegue l'esempio.</span><span class="sxs-lookup"><span data-stu-id="e0d45-109">**Typical output**: An example of the output to expect when you run the sample.</span></span>
* <span data-ttu-id="e0d45-110">**Frammenti di codice**: raccolta di frammenti di codice per mostrare come l'esempio Hello World implementa i componenti principali del gateway IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="e0d45-110">**Code snippets**: A collection of code snippets to show how the Hello World sample implements key IoT Edge gateway components.</span></span>


## <a name="hello-world-sample-architecture"></a><span data-ttu-id="e0d45-111">Architettura di esempio Hello World</span><span class="sxs-lookup"><span data-stu-id="e0d45-111">Hello World sample architecture</span></span>
<span data-ttu-id="e0d45-112">L'esempio Hello World illustra i concetti descritti nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="e0d45-112">The Hello World sample illustrates the concepts described in the previous section.</span></span> <span data-ttu-id="e0d45-113">L'esempio Hello World implementa un gateway IoT Edge la cui pipeline è costituita da due moduli di IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="e0d45-113">The Hello World sample implements a IoT Edge gateway that has a pipeline made up of two IoT Edge modules:</span></span>

* <span data-ttu-id="e0d45-114">Il modulo *hello world* crea un messaggio ogni cinque secondi e lo passa al modulo logger.</span><span class="sxs-lookup"><span data-stu-id="e0d45-114">The *hello world* module creates a message every five seconds and passes it to the logger module.</span></span>
* <span data-ttu-id="e0d45-115">Il modulo *logger* scrive i messaggi che riceve in un file.</span><span class="sxs-lookup"><span data-stu-id="e0d45-115">The *logger* module writes the messages it receives to a file.</span></span>

![Architettura dell'esempio Hello World compilato con Azure IoT Edge][4]

<span data-ttu-id="e0d45-117">Come descritto nella sezione precedente, il modulo Hello World non passa i messaggi direttamente al modulo logger ogni cinque secondi,</span><span class="sxs-lookup"><span data-stu-id="e0d45-117">As described in the previous section, the Hello World module does not pass messages directly to the logger module every five seconds.</span></span> <span data-ttu-id="e0d45-118">ma pubblica un messaggio nel broker ogni cinque secondi.</span><span class="sxs-lookup"><span data-stu-id="e0d45-118">Instead, it publishes a message to the broker every five seconds.</span></span>

<span data-ttu-id="e0d45-119">Il modulo logger riceve il messaggio dal broker e interviene, scrivendo il contenuto del messaggio in un file.</span><span class="sxs-lookup"><span data-stu-id="e0d45-119">The logger module receives the message from the broker and acts upon it, writing the contents of the message to a file.</span></span>

<span data-ttu-id="e0d45-120">Il modulo logger utilizza solo i messaggi provenienti dal broker, senza mai pubblicare nuovi messaggi nel broker.</span><span class="sxs-lookup"><span data-stu-id="e0d45-120">The logger module only consumes messages from the broker, it never publishes new messages to the broker.</span></span>

![Modo in cui il broker indirizza i messaggi tra i moduli in Azure IoT Edge][5]

<span data-ttu-id="e0d45-122">La figura precedente illustra l'architettura dell'esempio Hello World e i percorsi relativi ai file di origine che implementano parti diverse dell'esempio nel [repository][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="e0d45-122">The figure above shows the architecture of the Hello World sample and the relative paths to the source files that implement different portions of the sample in the [repository][lnk-iot-edge].</span></span> <span data-ttu-id="e0d45-123">Esplorare il codice per conto proprio o usare i frammenti di codice seguente come guida.</span><span class="sxs-lookup"><span data-stu-id="e0d45-123">Explore the code on your own, or use the code snippets below as a guide.</span></span>

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md