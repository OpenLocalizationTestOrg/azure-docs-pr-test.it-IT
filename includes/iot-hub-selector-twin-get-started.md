> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ea58-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="6ea58-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="6ea58-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="6ea58-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="6ea58-103">C#</span><span class="sxs-lookup"><span data-stu-id="6ea58-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="6ea58-104">Java</span><span class="sxs-lookup"><span data-stu-id="6ea58-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="6ea58-105">I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni).</span><span class="sxs-lookup"><span data-stu-id="6ea58-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6ea58-106">L'hub IoT rende permanente un dispositivo gemello per ogni dispositivo che si connette.</span><span class="sxs-lookup"><span data-stu-id="6ea58-106">IoT Hub persists a device twin for each device that connects to it.</span></span>

<span data-ttu-id="6ea58-107">Usare i dispositivi gemelli per:</span><span class="sxs-lookup"><span data-stu-id="6ea58-107">Use device twins to:</span></span>

* <span data-ttu-id="6ea58-108">Archiviare i metadati dei dispositivi dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="6ea58-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="6ea58-109">Segnalare informazioni sullo stato corrente, come funzionalità disponibili e condizioni (ad esempio, il metodo di connettività usato) dall'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6ea58-109">Report current state information such as available capabilities and conditions (for example, the connectivity method used) from your device app.</span></span>
* <span data-ttu-id="6ea58-110">Sincronizzare lo stato dei flussi di lavoro a esecuzione prolungata (come gli aggiornamenti del firmware e della configurazione) tra un'app per dispositivi e un'app di back-end.</span><span class="sxs-lookup"><span data-stu-id="6ea58-110">Synchronize the state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="6ea58-111">Eseguire query sui metadati, la configurazione o lo stato dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6ea58-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea58-112">I dispositivi gemelli sono progettati per la sincronizzazione e per l'esecuzione di query sulle configurazioni e le condizioni dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6ea58-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="6ea58-113">Altre informazioni su quando usare i dispositivi gemelli sono reperibili in [Informazioni sui dispositivi gemelli][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="6ea58-113">More informations on when to use device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="6ea58-114">I dispositivi gemelli vengono archiviati in un hub IoT e contengono gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="6ea58-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="6ea58-115">*Tag*: metadati dei dispositivi accessibili solo dal back-end della soluzione</span><span class="sxs-lookup"><span data-stu-id="6ea58-115">*tags*, device metadata accessible only by the solution back end;</span></span>
* <span data-ttu-id="6ea58-116">*Proprietà desiderate*: oggetti JSON modificabili dal back-end della soluzione e osservabili dall'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="6ea58-116">*desired properties*, JSON objects modifiable by the solution back end and observable by the device app; and</span></span>
* <span data-ttu-id="6ea58-117">*Proprietà segnalate*: oggetti JSON modificabili dall'app per dispositivi e leggibili dal back-end della soluzione</span><span class="sxs-lookup"><span data-stu-id="6ea58-117">*reported properties*, JSON objects modifiable by the device app and readable by the solution back end.</span></span> <span data-ttu-id="6ea58-118">I tag e le proprietà non possono contenere matrici, ma gli oggetti possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="6ea58-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="6ea58-119">Il back-end della soluzione può anche eseguire query sui dispositivi gemelli in base a tutti i dati sopra indicati.</span><span class="sxs-lookup"><span data-stu-id="6ea58-119">Additionally, the solution back end can query device twins based on all the above data.</span></span>
<span data-ttu-id="6ea58-120">Vedere [Informazioni sui dispositivi gemelli][lnk-twins] per altre informazioni sui dispositivi gemelli e [Linguaggio di query per hub IoT][lnk-query] per informazioni sull'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="6ea58-120">Refer to [Understand device twins][lnk-twins] for more information about device twins, and to the [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="6ea58-121">Al momento i dispositivi gemelli sono accessibili solo dai dispositivi che si connettono all'hub IoT tramite il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="6ea58-121">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="6ea58-122">Per istruzioni su come convertire l'app per dispositivo esistente in modo che usi MQTT, vedere l'articolo [Supporto di MQTT][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="6ea58-122">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>

<span data-ttu-id="6ea58-123">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="6ea58-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="6ea58-124">Creare un'app back-end che aggiunge *tag* a un dispositivo gemello e un'app per dispositivo simulato che segnala il proprio canale di connettività come *proprietà segnalata* nel dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="6ea58-124">Create a back-end app that adds *tags* to a device twin, and a simulated device app that reports its connectivity channel as a *reported property* on the device twin.</span></span>
* <span data-ttu-id="6ea58-125">Eseguire query sui dispositivi dall'app back-end con filtri sui tag e sulle proprietà creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6ea58-125">Query devices from your back-end app using filters on the tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md