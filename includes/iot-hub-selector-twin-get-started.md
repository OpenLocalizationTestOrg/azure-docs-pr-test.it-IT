> [!div class="op_single_selector"]
> * [<span data-ttu-id="af140-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="af140-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-getstarted.md)
> * [<span data-ttu-id="af140-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="af140-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-getstarted.md)
> * [<span data-ttu-id="af140-103">C#</span><span class="sxs-lookup"><span data-stu-id="af140-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-getstarted.md)
> * [<span data-ttu-id="af140-104">Java</span><span class="sxs-lookup"><span data-stu-id="af140-104">Java</span></span>](../articles/iot-hub/iot-hub-java-java-twin-getstarted.md)

<span data-ttu-id="af140-105">I dispositivi gemelli sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni).</span><span class="sxs-lookup"><span data-stu-id="af140-105">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="af140-106">IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooit.</span><span class="sxs-lookup"><span data-stu-id="af140-106">IoT Hub persists a device twin for each device that connects tooit.</span></span>

<span data-ttu-id="af140-107">Usare i dispositivi gemelli per:</span><span class="sxs-lookup"><span data-stu-id="af140-107">Use device twins to:</span></span>

* <span data-ttu-id="af140-108">Archiviare i metadati dei dispositivi dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="af140-108">Store device metadata from your solution back end.</span></span>
* <span data-ttu-id="af140-109">Report informazioni sullo stato corrente, ad esempio le funzionalità disponibili e le condizioni (ad esempio, la connettività metodo hello usato) dall'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="af140-109">Report current state information such as available capabilities and conditions (for example, hello connectivity method used) from your device app.</span></span>
* <span data-ttu-id="af140-110">Sincronizzazione dello stato di hello dei flussi di lavoro di lunga durata (ad esempio aggiornamenti firmware e la configurazione) tra un'app del dispositivo e un'applicazione back-end.</span><span class="sxs-lookup"><span data-stu-id="af140-110">Synchronize hello state of long-running workflows (such as firmware and configuration updates) between a device app and a back-end app.</span></span>
* <span data-ttu-id="af140-111">Eseguire query sui metadati, la configurazione o lo stato dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="af140-111">Query your device metadata, configuration, or state.</span></span>

> [!NOTE]
> <span data-ttu-id="af140-112">I dispositivi gemelli sono progettati per la sincronizzazione e per l'esecuzione di query sulle configurazioni e le condizioni dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="af140-112">Device twins are designed for synchronization and for querying device configurations and conditions.</span></span> <span data-ttu-id="af140-113">Ulteriori informazioni sulle quando gemelli dispositivo toouse sono reperibile [comprendere gemelli dispositivo][lnk-twins].</span><span class="sxs-lookup"><span data-stu-id="af140-113">More informations on when toouse device twins can be found in [Understand device twins][lnk-twins].</span></span>

<span data-ttu-id="af140-114">I dispositivi gemelli vengono archiviati in un hub IoT e contengono gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="af140-114">Device twins are stored in an IoT hub and contain:</span></span>

* <span data-ttu-id="af140-115">*tag*, accessibili solo dal back-end soluzione hello; metadati del dispositivo</span><span class="sxs-lookup"><span data-stu-id="af140-115">*tags*, device metadata accessible only by hello solution back end;</span></span>
* <span data-ttu-id="af140-116">*le proprietà desiderate*, oggetti JSON modificabili dalla soluzione hello indietro end e observable tramite app per dispositivi hello; e</span><span class="sxs-lookup"><span data-stu-id="af140-116">*desired properties*, JSON objects modifiable by hello solution back end and observable by hello device app; and</span></span>
* <span data-ttu-id="af140-117">*proprietà segnalati*, oggetti JSON modificabili per app per dispositivi hello e leggibili dal back-end di hello soluzione.</span><span class="sxs-lookup"><span data-stu-id="af140-117">*reported properties*, JSON objects modifiable by hello device app and readable by hello solution back end.</span></span> <span data-ttu-id="af140-118">I tag e le proprietà non possono contenere matrici, ma gli oggetti possono essere annidati.</span><span class="sxs-lookup"><span data-stu-id="af140-118">Tags and properties cannot contain arrays, but objects can be nested.</span></span>

![][img-twin]

<span data-ttu-id="af140-119">Inoltre, è possibile eseguire hello soluzione back-end query gemelli di dispositivo in base a tutti hello di sopra dei dati.</span><span class="sxs-lookup"><span data-stu-id="af140-119">Additionally, hello solution back end can query device twins based on all hello above data.</span></span>
<span data-ttu-id="af140-120">Fare riferimento troppo[comprendere gemelli dispositivo] [ lnk-twins] per ulteriori informazioni su gemelli di dispositivo e toohello [il linguaggio di query di IoT Hub] [ lnk-query] riferimento Per eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="af140-120">Refer too[Understand device twins][lnk-twins] for more information about device twins, and toohello [IoT Hub query language][lnk-query] reference for querying.</span></span>

> [!NOTE]
> <span data-ttu-id="af140-121">A questo punto, sono accessibili solo da dispositivi che si connettono tooIoT Hub gemelli di dispositivo utilizzando il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="af140-121">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="af140-122">Consultare toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="af140-122">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>

<span data-ttu-id="af140-123">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="af140-123">This tutorial shows you how to:</span></span>

* <span data-ttu-id="af140-124">Creare un'applicazione back-end che aggiunge *tag* tooa gemelli di dispositivo e un'app per dispositivo simulato che segnala la connettività del canale come un *segnalati proprietà* in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="af140-124">Create a back-end app that adds *tags* tooa device twin, and a simulated device app that reports its connectivity channel as a *reported property* on hello device twin.</span></span>
* <span data-ttu-id="af140-125">Eseguire una query dispositivi dall'app back-end utilizzando i filtri tag hello e proprietà creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="af140-125">Query devices from your back-end app using filters on hello tags and properties previously created.</span></span>

<!-- images -->
[img-twin]: media/iot-hub-selector-twin-get-started/twin.png

<!-- links -->
[lnk-query]: ../articles/iot-hub/iot-hub-devguide-query-language.md
[lnk-twins]: ../articles/iot-hub/iot-hub-devguide-device-twins.md
[lnk-d2c]: ../articles/iot-hub/iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: ../articles/iot-hub/iot-hub-mqtt-support.md