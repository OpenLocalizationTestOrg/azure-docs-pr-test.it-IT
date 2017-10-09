> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b3f3-101">Node.JS</span><span class="sxs-lookup"><span data-stu-id="4b3f3-101">Node.js</span></span>](../articles/iot-hub/iot-hub-node-node-twin-how-to-configure.md)
> * [<span data-ttu-id="4b3f3-102">C#/Node.js</span><span class="sxs-lookup"><span data-stu-id="4b3f3-102">C#/Node.js</span></span>](../articles/iot-hub/iot-hub-csharp-node-twin-how-to-configure.md)
> * [<span data-ttu-id="4b3f3-103">C#</span><span class="sxs-lookup"><span data-stu-id="4b3f3-103">C#</span></span>](../articles/iot-hub/iot-hub-csharp-csharp-twin-how-to-configure.md)
> 
> 

## <a name="introduction"></a><span data-ttu-id="4b3f3-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="4b3f3-104">Introduction</span></span>

<span data-ttu-id="4b3f3-105">In [introduzione gemelli dispositivo IoT Hub][lnk-twin-tutorial], si è appreso come metadati del dispositivo tooset dalla soluzione nuovamente comporta l'utilizzo di *tag*, segnalare le condizioni di dispositivo da un'app del dispositivo utilizzando *segnalati proprietà*ed eseguire query su queste informazioni tramite un linguaggio simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-105">In [Get started with IoT Hub device twins][lnk-twin-tutorial], you learned how tooset device metadata from your solution back end using *tags*, report device conditions from a device app using *reported properties*, and query this information using a SQL-like language.</span></span>

<span data-ttu-id="4b3f3-106">In questa esercitazione si apprenderà come toouse hello del doppi dispositivo hello *le proprietà desiderate* insieme a *segnalati proprietà*, tooremotely configurare App per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-106">In this tutorial, you will learn how toouse hello hello device twin's *desired properties* along with *reported properties*, tooremotely configure device apps.</span></span> <span data-ttu-id="4b3f3-107">In particolare, questa esercitazione viene illustrato come una coppia di dispositivo segnalati e le proprietà desiderate abilitare una configurazione di più passaggi di un'applicazione per dispositivi e forniscano hello visibilità toohello soluzione back-end di stato hello di questa operazione in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-107">More specifically, this tutorial shows how a device twin's reported and desired properties enable a multi-step configuration of a device application, and provide hello visibility toohello solution back end of hello status of this operation across all devices.</span></span> <span data-ttu-id="4b3f3-108">È possibile trovare ulteriori informazioni sul ruolo hello di configurazioni di dispositivo in [Panoramica di gestione dei dispositivi con l'IoT Hub][lnk-dm-overview].</span><span class="sxs-lookup"><span data-stu-id="4b3f3-108">You can find more information regarding hello role of device configurations in [Overview of device management with IoT Hub][lnk-dm-overview].</span></span>

<span data-ttu-id="4b3f3-109">In generale, l'utilizzo di gemelli dispositivo consente hello soluzione back-end toospecify hello configurazione desiderata per i dispositivi gestito hello, anziché inviare comandi specifici.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-109">At a high level, using device twins enables hello solution back end toospecify hello desired configuration for hello managed devices, instead of sending specific commands.</span></span> <span data-ttu-id="4b3f3-110">In questo modo il dispositivo hello responsabile della configurazione tooupdate modo migliore hello relativa configurazione (molto importante in scenari IoT in condizioni di dispositivo specifico influire sul hello possibilità tooimmediately eseguire determinati comandi) durante la restituzione continuamente toohello stato corrente di hello e potenziali condizioni di errore del processo di aggiornamento hello di fine soluzione nuovamente.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-110">This puts hello device in charge of setting up hello best way tooupdate its configuration (very important in IoT scenarios where specific device conditions affect hello ability tooimmediately carry out specific commands), while continually reporting toohello solution back end hello current state and potential error conditions of hello update process.</span></span> <span data-ttu-id="4b3f3-111">Questo modello è strumentale toohello gestione di grandi set di dispositivi, poiché consente hello soluzione back-end toohave completa visibilità dello stato di hello del processo di configurazione hello in tutti i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-111">This pattern is instrumental toohello management of large sets of devices, as it enables hello solution back end toohave full visibility of hello state of hello configuration process across all devices.</span></span>

> [!NOTE]
> <span data-ttu-id="4b3f3-112">Negli scenari in cui i dispositivi sono controllati in modo più interattivo (come nel caso dell'attivazione di una ventola da un'app controllata dall'utente), può essere opportuno usare [metodi diretti][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="4b3f3-112">In scenarios where devices are controlled in a more interactive fashion (turn on a fan from a user-controlled app), consider using [direct methods][lnk-methods].</span></span>
> 
> 

<span data-ttu-id="4b3f3-113">In questa esercitazione, modifiche di back-end di soluzione hello configurazione di telemetria hello di un dispositivo di destinazione e, in seguito che app per dispositivi hello segue tooapply un processo in più passaggi una configurazione di aggiornamento (ad esempio, che richiedono il riavvio modulo software, quale l'oggetto esercitazione simula con un ritardo semplice).</span><span class="sxs-lookup"><span data-stu-id="4b3f3-113">In this tutorial, hello solution back end changes hello telemetry configuration of a target device and, as a result of that, hello device app follows a multi-step process tooapply a configuration update (for example, requiring a software module restart, which this tutorial simulates with a simple delay).</span></span>

<span data-ttu-id="4b3f3-114">back-end di Hello soluzione memorizza la configurazione di hello nelle proprietà desiderato del doppi dispositivo hello hello seguente modo:</span><span class="sxs-lookup"><span data-stu-id="4b3f3-114">hello solution back end stores hello configuration in hello device twin's desired properties in hello following way:</span></span>

        {
            ...
            "properties": {
                ...
                "desired": {
                    "telemetryConfig": {
                        "configId": "{id of hello configuration}",
                        "sendFrequency": "{config}"
                    }
                }
                ...
            }
            ...
        }

> [!NOTE]
> <span data-ttu-id="4b3f3-115">Poiché le configurazioni possono essere oggetti complessi, in genere vengono assegnati un ID univoco (hash o [GUID][lnk-guid]) toosimplify i confronti.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-115">Since configurations can be complex objects, they are usually assigned unique ids (hashes or [GUIDs][lnk-guid]) toosimplify their comparisons.</span></span>
> 
> 

<span data-ttu-id="4b3f3-116">app per dispositivi Hello segnala la configurazione corrente del mirroring proprietà hello desiderato **telemetryConfig** in hello segnalati proprietà:</span><span class="sxs-lookup"><span data-stu-id="4b3f3-116">hello device app reports its current configuration mirroring hello desired property **telemetryConfig** in hello reported properties:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Success",
                    }
                }
                ...
            }
        }

<span data-ttu-id="4b3f3-117">Si noti la modalità di segnalazione hello **telemetryConfig** ha una proprietà aggiuntiva **stato**, stato hello tooreport del processo di aggiornamento configurazione hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-117">Note how hello reported **telemetryConfig** has an additional property **status**, used tooreport hello state of hello configuration update process.</span></span>

<span data-ttu-id="4b3f3-118">Quando viene ricevuta una nuova configurazione desiderata, hello dispositivo app segnala una configurazione in sospeso modificando hello informazioni:</span><span class="sxs-lookup"><span data-stu-id="4b3f3-118">When a new desired configuration is received, hello device app reports a pending configuration by changing hello information:</span></span>

        {
            "properties": {
                ...
                "reported": {
                    "telemetryConfig": {
                        "changeId": "{id of hello current configuration}",
                        "sendFrequency": "{current configuration}",
                        "status": "Pending",
                        "pendingConfig": {
                            "changeId": "{id of hello pending configuration}",
                            "sendFrequency": "{pending configuration}"
                        }
                    }
                }
                ...
            }
        }

<span data-ttu-id="4b3f3-119">Quindi, in un secondo momento, hello dispositivo app segnalerà hello riuscita o meno dell'operazione aggiornando hello di sopra di proprietà.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-119">Then, at some later time, hello device app will report hello success or failure of this operation by updating hello above property.</span></span>
<span data-ttu-id="4b3f3-120">Si noti come back-end di hello soluzione è in grado di, in qualsiasi momento, lo stato di hello tooquery del processo di configurazione hello in tutti i dispositivi di hello.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-120">Note how hello solution back end is able, at any time, tooquery hello status of hello configuration process across all hello devices.</span></span>

<span data-ttu-id="4b3f3-121">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="4b3f3-121">This tutorial shows you how to:</span></span>

* <span data-ttu-id="4b3f3-122">Creare un'app dispositivo simulato che riceve gli aggiornamenti della configurazione dal back-end di soluzione hello e report più aggiornamenti come *segnalati proprietà* configurazione hello processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-122">Create a simulated device app that receives configuration updates from hello solution back end, and reports multiple updates as *reported properties* on hello configuration update process.</span></span>
* <span data-ttu-id="4b3f3-123">Creare un'app di back-end che gli aggiornamenti hello configurazione desiderata di un dispositivo e quindi query hello il processo di aggiornamento di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4b3f3-123">Create a back-end app that updates hello desired configuration of a device, and then queries hello configuration update process.</span></span>

<!-- links -->

[lnk-methods]: ../articles/iot-hub/iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: ../articles/iot-hub/iot-hub-device-management-overview.md
[lnk-twin-tutorial]: ../articles/iot-hub/iot-hub-node-node-twin-getstarted.md
[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier
