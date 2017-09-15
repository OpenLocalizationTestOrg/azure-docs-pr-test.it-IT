## <a name="typical-output"></a><span data-ttu-id="63362-101">Output tipico</span><span class="sxs-lookup"><span data-stu-id="63362-101">Typical output</span></span>

<span data-ttu-id="63362-102">L'esempio seguente mostra l'output scritto nel file di log dall'esempio Hello World.</span><span class="sxs-lookup"><span data-stu-id="63362-102">The following example shows the output written to the log file by the Hello World sample.</span></span> <span data-ttu-id="63362-103">L'output è formattato per migliorare la leggibilità:</span><span class="sxs-lookup"><span data-stu-id="63362-103">The output is formatted for legibility:</span></span>

```json
[{
    "time": "Mon Apr 11 13:48:07 2016",
    "content": "Log started"
}, {
    "time": "Mon Apr 11 13:48:48 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:48:55 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:01 2016",
    "properties": {
        "helloWorld": "from Azure IoT Gateway SDK simple sample!"
    },
    "content": "aGVsbG8gd29ybGQ="
}, {
    "time": "Mon Apr 11 13:49:04 2016",
    "content": "Log stopped"
}]
```

## <a name="code-snippets"></a><span data-ttu-id="63362-104">Frammenti di codice</span><span class="sxs-lookup"><span data-stu-id="63362-104">Code snippets</span></span>

<span data-ttu-id="63362-105">In questa sezione vengono descritte alcune sezioni chiave del codice nell'esempio hello\_world.</span><span class="sxs-lookup"><span data-stu-id="63362-105">This section discusses some key sections of the code in the hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="63362-106">Creazione del gateway IoT Edge</span><span class="sxs-lookup"><span data-stu-id="63362-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="63362-107">È necessario implementare un *processo del gateway*.</span><span class="sxs-lookup"><span data-stu-id="63362-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="63362-108">Questo programma crea l'infrastruttura interna, ovvero il broker, carica i moduli di IoT Edge e configura il processo del gateway.</span><span class="sxs-lookup"><span data-stu-id="63362-108">This program creates the internal infrastructure (the broker), loads the IoT Edge modules, and configures the gateway process.</span></span> <span data-ttu-id="63362-109">IoT Edge specifica la funzione **Gateway\_Create\_From\_JSON** per consentire di avviare un gateway da un file JSON.</span><span class="sxs-lookup"><span data-stu-id="63362-109">IoT Edge provides the **Gateway\_Create\_From\_JSON** function to enable you to bootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="63362-110">Per usare la funzione **Gateway\_Create\_From\_JSON**, chiamarla dal percorso di un file JSON che specifica i moduli di IoT Edge da caricare.</span><span class="sxs-lookup"><span data-stu-id="63362-110">To use the **Gateway\_Create\_From\_JSON** function, pass it the path to a JSON file that specifies the IoT Edge modules to load.</span></span>

<span data-ttu-id="63362-111">È possibile trovare il codice per il processo del gateway nell'esempio *Hello World* nel file [main.c][lnk-main-c].</span><span class="sxs-lookup"><span data-stu-id="63362-111">You can find the code for the gateway process in the *Hello World* sample in the [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="63362-112">Per migliorare la leggibilità, il frammento di codice seguente illustra una versione abbreviata del codice del processo del gateway.</span><span class="sxs-lookup"><span data-stu-id="63362-112">For legibility, the following snippet shows an abbreviated version of the gateway process code.</span></span> <span data-ttu-id="63362-113">Questo programma di esempio crea un gateway e quindi attende che l'utente prema **INVIO** prima di rimuove il gateway.</span><span class="sxs-lookup"><span data-stu-id="63362-113">This example program creates a gateway and then waits for the user to press the **ENTER** key before it tears down the gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed to create the gateway from JSON\n");
    }
    else
    {
        printf("gateway successfully created from JSON\n");
        printf("gateway shall run until ENTER is pressed\n");
        (void)getchar();
        Gateway_LL_Destroy(gateway);
    }
    return 0;
}
```

<span data-ttu-id="63362-114">Il file di impostazioni JSON contiene un elenco di moduli di IoT Edge da caricare e i collegamenti tra i moduli.</span><span class="sxs-lookup"><span data-stu-id="63362-114">The JSON settings file contains a list of IoT Edge modules to load and the links between the modules.</span></span> <span data-ttu-id="63362-115">Ogni modulo di IoT Edge deve specificare:</span><span class="sxs-lookup"><span data-stu-id="63362-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="63362-116">**name**: nome univoco per il modulo.</span><span class="sxs-lookup"><span data-stu-id="63362-116">**name**: a unique name for the module.</span></span>
* <span data-ttu-id="63362-117">**loader**: un caricatore che riesca a caricare il modulo appropriato.</span><span class="sxs-lookup"><span data-stu-id="63362-117">**loader**: a loader that knows how to load the desired module.</span></span> <span data-ttu-id="63362-118">I caricatori sono punti di estensione per il caricamento di tipi diversi di moduli.</span><span class="sxs-lookup"><span data-stu-id="63362-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="63362-119">IoT Edge offre caricatori da usare con moduli scritti in C, Node.js, Java e .NET nativi.</span><span class="sxs-lookup"><span data-stu-id="63362-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="63362-120">L'esempio Hello World usa solo il caricatore C nativo perché tutti i moduli in questo esempio sono librerie dinamiche scritte in C. Per altre informazioni su come usare moduli di IoT Edge scritti in linguaggi diversi, vedere gli esempi [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample) o [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample).</span><span class="sxs-lookup"><span data-stu-id="63362-120">The Hello World sample only uses the native C loader because all the modules in this sample are dynamic libraries written in C. For more information about how to use IoT Edge modules written in different languages, see the [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="63362-121">**name**: nome del caricatore usato per caricare il modulo.</span><span class="sxs-lookup"><span data-stu-id="63362-121">**name**: the name of the loader used to load the module.</span></span>
    * <span data-ttu-id="63362-122">**entrypoint**: percorso della libreria che contiene il modulo.</span><span class="sxs-lookup"><span data-stu-id="63362-122">**entrypoint**: the path to the library containing the module.</span></span> <span data-ttu-id="63362-123">In Linux questa libreria è un file con estensione so, in Windows è un file con estensione dll.</span><span class="sxs-lookup"><span data-stu-id="63362-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="63362-124">Il punto di ingresso è specifico per il tipo di caricatore in uso.</span><span class="sxs-lookup"><span data-stu-id="63362-124">The entry point is specific to the type of loader being used.</span></span> <span data-ttu-id="63362-125">Il punto di ingresso del caricatore Node.js è un file con estensione js.</span><span class="sxs-lookup"><span data-stu-id="63362-125">The Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="63362-126">Il punto di ingresso del caricatore Java è un percorso di classe e un nome di classe.</span><span class="sxs-lookup"><span data-stu-id="63362-126">The Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="63362-127">Il punto di ingresso del caricatore .NET è un nome di assembly e un nome di classe.</span><span class="sxs-lookup"><span data-stu-id="63362-127">The .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="63362-128">**args**: le informazioni di configurazione necessarie per il modulo.</span><span class="sxs-lookup"><span data-stu-id="63362-128">**args**: any configuration information the module needs.</span></span>

<span data-ttu-id="63362-129">Il codice seguente illustra l'uso di JSON per dichiarare tutti i moduli di IoT Edge per l'esempio Hello World in Linux.</span><span class="sxs-lookup"><span data-stu-id="63362-129">The following code shows the JSON used to declare all the IoT Edge modules for the Hello World sample on Linux.</span></span> <span data-ttu-id="63362-130">L'uso di argomenti nei moduli dipende dalla loro struttura.</span><span class="sxs-lookup"><span data-stu-id="63362-130">Whether a module requires any arguments depends on the design of the module.</span></span> <span data-ttu-id="63362-131">In questo esempio, il modulo logger include un argomento che specifica il percorso del file di output e il modulo hello\_world non include nessun argomento.</span><span class="sxs-lookup"><span data-stu-id="63362-131">In this example, the logger module takes an argument that is the path to the output file and the hello\_world module has no arguments.</span></span>

```json
"modules" :
[
    {
        "name" : "logger",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/logger/liblogger.so"
        }
        },
        "args" : {"filename":"log.txt"}
    },
    {
        "name" : "hello_world",
        "loader": {
          "name": "native",
          "entrypoint": {
            "module.path": "./modules/hello_world/libhello_world.so"
        }
        },
        "args" : null
    }
]
```

<span data-ttu-id="63362-132">Il file JSON contiene anche i collegamenti tra i moduli che vengono passati al broker.</span><span class="sxs-lookup"><span data-stu-id="63362-132">The JSON file also contains the links between the modules that are passed to the broker.</span></span> <span data-ttu-id="63362-133">Un collegamento ha due proprietà:</span><span class="sxs-lookup"><span data-stu-id="63362-133">A link has two properties:</span></span>

* <span data-ttu-id="63362-134">**source**: il nome di un modulo dalla sezione `modules` oppure `\*`.</span><span class="sxs-lookup"><span data-stu-id="63362-134">**source**: a module name from the `modules` section, or `\*`.</span></span>
* <span data-ttu-id="63362-135">**sink**: il nome di un modulo dalla sezione `modules`.</span><span class="sxs-lookup"><span data-stu-id="63362-135">**sink**: a module name from the `modules` section.</span></span>

<span data-ttu-id="63362-136">Ogni collegamento definisce una route messaggi e una direzione.</span><span class="sxs-lookup"><span data-stu-id="63362-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="63362-137">I messaggi dal modulo **source** vengono recapitati al modulo **sink**.</span><span class="sxs-lookup"><span data-stu-id="63362-137">Messages from the **source** module are delivered to the **sink** module.</span></span> <span data-ttu-id="63362-138">È possibile impostare il modulo **source** su `\*`, che indica che il modulo **sink** riceve messaggi da qualsiasi modulo.</span><span class="sxs-lookup"><span data-stu-id="63362-138">You can set the **source** module to `\*`, which indicates that the **sink** module receives messages from any module.</span></span>

<span data-ttu-id="63362-139">Il codice seguente illustra l'uso di JSON per configurare i collegamenti tra i moduli usati nell'esempio hello\_world in Linux.</span><span class="sxs-lookup"><span data-stu-id="63362-139">The following code shows the JSON used to configure links between the modules used in the hello\_world sample on Linux.</span></span> <span data-ttu-id="63362-140">Tutti i messaggi generati dal modulo `hello_world` vengono utilizzati dal modulo `logger`.</span><span class="sxs-lookup"><span data-stu-id="63362-140">Every message produced by the `hello_world` module is consumed by the `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="63362-141">Pubblicazione dei messaggi del modulo hello\_world</span><span class="sxs-lookup"><span data-stu-id="63362-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="63362-142">Il codice usato dal modulo hello\_world per pubblicare i messaggi è disponibile nel file ["hello_world.c"][lnk-helloworld-c].</span><span class="sxs-lookup"><span data-stu-id="63362-142">You can find the code used by the hello\_world module to publish messages in the ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="63362-143">Il frammento di codice seguente riporta una versione modificata, per una maggior leggibilità, in cui sono stati aggiunti commenti ed è stata rimossa parte del codice per la gestione degli errori:</span><span class="sxs-lookup"><span data-stu-id="63362-143">The following snippet shows an amended version of the code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" to a set of message properties that
    // will be appended to the message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set the content for the message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set the properties for the message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on the msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of the thread*/
        }
        else
        {
            // publish the message to the broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="63362-144">Elaborazione dei messaggi del modulo hello\_world</span><span class="sxs-lookup"><span data-stu-id="63362-144">Hello\_world module message processing</span></span>

<span data-ttu-id="63362-145">Il modulo hello\_world non elabora mai messaggi pubblicati da altri moduli di IoT Edge nel broker.</span><span class="sxs-lookup"><span data-stu-id="63362-145">The hello\_world module never processes messages that other IoT Edge modules publish to the broker.</span></span> <span data-ttu-id="63362-146">L'implementazione del callback dei messaggi nel modulo hello\_world è quindi una funzione no-op.</span><span class="sxs-lookup"><span data-stu-id="63362-146">Therefore, the implementation of the message callback in the hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="63362-147">Elaborazione e pubblicazione dei messaggi del modulo di logger</span><span class="sxs-lookup"><span data-stu-id="63362-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="63362-148">Il modulo logger riceve messaggi dal broker e li scrive in un file,</span><span class="sxs-lookup"><span data-stu-id="63362-148">The logger module receives messages from the broker and writes them to a file.</span></span> <span data-ttu-id="63362-149">ma non pubblica mai messaggi.</span><span class="sxs-lookup"><span data-stu-id="63362-149">It never publishes any messages.</span></span> <span data-ttu-id="63362-150">Il codice del modulo logger quindi non chiama mai la funzione **Broker_Publish**.</span><span class="sxs-lookup"><span data-stu-id="63362-150">Therefore, the code of the logger module never calls the **Broker_Publish** function.</span></span>

<span data-ttu-id="63362-151">La funzione **Logger_Receive** nel file [logger.c][lnk-logger-c] è il callback che viene richiamato dal broker per recapitare i messaggi al modulo logger.</span><span class="sxs-lookup"><span data-stu-id="63362-151">The **Logger_Receive** function in the [logger.c][lnk-logger-c] file is the callback the broker invokes to deliver messages to the logger module.</span></span> <span data-ttu-id="63362-152">Il frammento di codice seguente riporta una versione modificata, per una maggior leggibilità, in cui sono stati aggiunti commenti ed è stata rimossa parte del codice per la gestione degli errori:</span><span class="sxs-lookup"><span data-stu-id="63362-152">The following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get the message properties from the message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert the collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode the message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start the construction of the final string to be logged by adding
    // the timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add the message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add the content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write the formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="63362-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63362-153">Next steps</span></span>

<span data-ttu-id="63362-154">In questo articolo è stato eseguito un gateway IoT Edge semplice che ha scritto messaggi in un file di log.</span><span class="sxs-lookup"><span data-stu-id="63362-154">In this article, you ran a simple IoT Edge gateway that writes messages to a log file.</span></span> <span data-ttu-id="63362-155">Per eseguire un esempio che invia messaggi all'hub IoT, vedere [IoT Edge: inviare messaggi da dispositivo a cloud con un dispositivo simulato usando Linux][lnk-gateway-simulated-linux] o [IoT Edge: inviare messaggi da dispositivo a cloud con un dispositivo simulato usando Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="63362-155">To run a sample that sends messages to IoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md