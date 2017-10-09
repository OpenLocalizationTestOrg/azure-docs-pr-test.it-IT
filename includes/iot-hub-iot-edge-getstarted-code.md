## <a name="typical-output"></a><span data-ttu-id="dc47d-101">Output tipico</span><span class="sxs-lookup"><span data-stu-id="dc47d-101">Typical output</span></span>

<span data-ttu-id="dc47d-102">Hello seguente esempio Mostra output di hello scritto il file di log toohello dall'esempio hello World Hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-102">hello following example shows hello output written toohello log file by hello Hello World sample.</span></span> <span data-ttu-id="dc47d-103">formattazione dell'output di Hello per migliorare la leggibilità:</span><span class="sxs-lookup"><span data-stu-id="dc47d-103">hello output is formatted for legibility:</span></span>

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

## <a name="code-snippets"></a><span data-ttu-id="dc47d-104">Frammenti di codice</span><span class="sxs-lookup"><span data-stu-id="dc47d-104">Code snippets</span></span>

<span data-ttu-id="dc47d-105">Questa sezione vengono illustrate alcune sezioni di codice hello in hello hello chiave\_esempio world.</span><span class="sxs-lookup"><span data-stu-id="dc47d-105">This section discusses some key sections of hello code in hello hello\_world sample.</span></span>

### <a name="iot-edge-gateway-creation"></a><span data-ttu-id="dc47d-106">Creazione del gateway IoT Edge</span><span class="sxs-lookup"><span data-stu-id="dc47d-106">IoT Edge gateway creation</span></span>

<span data-ttu-id="dc47d-107">È necessario implementare un *processo del gateway*.</span><span class="sxs-lookup"><span data-stu-id="dc47d-107">You must implement a *gateway process*.</span></span> <span data-ttu-id="dc47d-108">Questo programma crea l'infrastruttura interna hello (broker hello), carica moduli IoT Edge hello e configura il processo di gateway hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-108">This program creates hello internal infrastructure (hello broker), loads hello IoT Edge modules, and configures hello gateway process.</span></span> <span data-ttu-id="dc47d-109">Bordo IoT fornisce hello **Gateway\_crea\_da\_JSON** funzione tooenable è toobootstrap un gateway da un file JSON.</span><span class="sxs-lookup"><span data-stu-id="dc47d-109">IoT Edge provides hello **Gateway\_Create\_From\_JSON** function tooenable you toobootstrap a gateway from a JSON file.</span></span> <span data-ttu-id="dc47d-110">hello toouse **Gateway\_crea\_da\_JSON** di funzione, passarlo hello percorso tooa file JSON specifica hello tooload moduli IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="dc47d-110">toouse hello **Gateway\_Create\_From\_JSON** function, pass it hello path tooa JSON file that specifies hello IoT Edge modules tooload.</span></span>

<span data-ttu-id="dc47d-111">È possibile trovare codice hello per processo gateway hello hello *Hello World* sample in hello [Main. c] [ lnk-main-c] file.</span><span class="sxs-lookup"><span data-stu-id="dc47d-111">You can find hello code for hello gateway process in hello *Hello World* sample in hello [main.c][lnk-main-c] file.</span></span> <span data-ttu-id="dc47d-112">Per migliorare la leggibilità, hello frammento di codice seguente viene illustrata una versione abbreviata del codice del processo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-112">For legibility, hello following snippet shows an abbreviated version of hello gateway process code.</span></span> <span data-ttu-id="dc47d-113">Il programma di esempio crea un gateway e quindi attende hello di hello utente toopress **invio** chiave prima che elimina gateway hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-113">This example program creates a gateway and then waits for hello user toopress hello **ENTER** key before it tears down hello gateway.</span></span>

```c
int main(int argc, char** argv)
{
    GATEWAY_HANDLE gateway;
    if ((gateway = Gateway_Create_From_JSON(argv[1])) == NULL)
    {
        printf("failed toocreate hello gateway from JSON\n");
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

<span data-ttu-id="dc47d-114">file di impostazioni JSON Hello contiene un elenco di collegamenti di hello tra i moduli di hello e tooload moduli IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="dc47d-114">hello JSON settings file contains a list of IoT Edge modules tooload and hello links between hello modules.</span></span> <span data-ttu-id="dc47d-115">Ogni modulo di IoT Edge deve specificare:</span><span class="sxs-lookup"><span data-stu-id="dc47d-115">Each IoT Edge module must specify a:</span></span>

* <span data-ttu-id="dc47d-116">**nome**: un nome univoco per il modulo hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-116">**name**: a unique name for hello module.</span></span>
* <span data-ttu-id="dc47d-117">**caricatore**: un caricatore che sa come hello tooload desiderato modulo.</span><span class="sxs-lookup"><span data-stu-id="dc47d-117">**loader**: a loader that knows how tooload hello desired module.</span></span> <span data-ttu-id="dc47d-118">I caricatori sono punti di estensione per il caricamento di tipi diversi di moduli.</span><span class="sxs-lookup"><span data-stu-id="dc47d-118">Loaders are an extension point for loading different types of modules.</span></span> <span data-ttu-id="dc47d-119">IoT Edge offre caricatori da usare con moduli scritti in C, Node.js, Java e .NET nativi.</span><span class="sxs-lookup"><span data-stu-id="dc47d-119">IoT Edge provides loaders for use with modules written in native C, Node.js, Java, and .NET.</span></span> <span data-ttu-id="dc47d-120">esempio Hello World Hello utilizza solo caricatore C nativo hello perché tutti i moduli di hello in questo esempio sono librerie dinamiche scritte in C. Per ulteriori informazioni su come i moduli di Edge IoT toouse scritti in linguaggi diversi, vedere hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), o [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) esempi.</span><span class="sxs-lookup"><span data-stu-id="dc47d-120">hello Hello World sample only uses hello native C loader because all hello modules in this sample are dynamic libraries written in C. For more information about how toouse IoT Edge modules written in different languages, see hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), or [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) samples.</span></span>
    * <span data-ttu-id="dc47d-121">**nome**: nome hello del caricatore di hello utilizzato modulo hello tooload.</span><span class="sxs-lookup"><span data-stu-id="dc47d-121">**name**: hello name of hello loader used tooload hello module.</span></span>
    * <span data-ttu-id="dc47d-122">**punto di ingresso**: libreria di toohello hello percorso contenente il modulo hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-122">**entrypoint**: hello path toohello library containing hello module.</span></span> <span data-ttu-id="dc47d-123">In Linux questa libreria è un file con estensione so, in Windows è un file con estensione dll.</span><span class="sxs-lookup"><span data-stu-id="dc47d-123">On Linux this library is a .so file, on Windows this library is a .dll file.</span></span> <span data-ttu-id="dc47d-124">punto di ingresso Hello è il tipo di toohello specifico del caricatore in uso.</span><span class="sxs-lookup"><span data-stu-id="dc47d-124">hello entry point is specific toohello type of loader being used.</span></span> <span data-ttu-id="dc47d-125">Hello punto di ingresso del caricatore di Node.js è un file. js.</span><span class="sxs-lookup"><span data-stu-id="dc47d-125">hello Node.js loader entry point is a .js file.</span></span> <span data-ttu-id="dc47d-126">punto di ingresso del caricatore Java Hello è un percorso di classe e un nome di classe.</span><span class="sxs-lookup"><span data-stu-id="dc47d-126">hello Java loader entry point is a classpath and a class name.</span></span> <span data-ttu-id="dc47d-127">punto di ingresso del caricatore .NET Hello è un nome di assembly e un nome di classe.</span><span class="sxs-lookup"><span data-stu-id="dc47d-127">hello .NET loader entry point is an assembly name and a class name.</span></span>

* <span data-ttu-id="dc47d-128">**args**: necessita di qualsiasi modulo hello informazioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="dc47d-128">**args**: any configuration information hello module needs.</span></span>

<span data-ttu-id="dc47d-129">Hello seguente codice mostra hello JSON utilizzato toodeclare tutti hello moduli IoT bordo per l'esempio Hello World hello in Linux.</span><span class="sxs-lookup"><span data-stu-id="dc47d-129">hello following code shows hello JSON used toodeclare all hello IoT Edge modules for hello Hello World sample on Linux.</span></span> <span data-ttu-id="dc47d-130">Se un modulo richiede argomenti dipende dalla progettazione hello del modulo hello.</span><span class="sxs-lookup"><span data-stu-id="dc47d-130">Whether a module requires any arguments depends on hello design of hello module.</span></span> <span data-ttu-id="dc47d-131">In questo esempio, il modulo di logger hello accetta un argomento di file di output di hello percorso toohello e hello hello\_modulo world non dispone di argomenti.</span><span class="sxs-lookup"><span data-stu-id="dc47d-131">In this example, hello logger module takes an argument that is hello path toohello output file and hello hello\_world module has no arguments.</span></span>

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

<span data-ttu-id="dc47d-132">file JSON Hello contiene anche collegamenti hello tra moduli hello che vengono passati toohello broker.</span><span class="sxs-lookup"><span data-stu-id="dc47d-132">hello JSON file also contains hello links between hello modules that are passed toohello broker.</span></span> <span data-ttu-id="dc47d-133">Un collegamento ha due proprietà:</span><span class="sxs-lookup"><span data-stu-id="dc47d-133">A link has two properties:</span></span>

* <span data-ttu-id="dc47d-134">**origine**: il nome di un modulo da hello `modules` sezione o `\*`.</span><span class="sxs-lookup"><span data-stu-id="dc47d-134">**source**: a module name from hello `modules` section, or `\*`.</span></span>
* <span data-ttu-id="dc47d-135">**sink**: il nome di un modulo da hello `modules` sezione.</span><span class="sxs-lookup"><span data-stu-id="dc47d-135">**sink**: a module name from hello `modules` section.</span></span>

<span data-ttu-id="dc47d-136">Ogni collegamento definisce una route messaggi e una direzione.</span><span class="sxs-lookup"><span data-stu-id="dc47d-136">Each link defines a message route and direction.</span></span> <span data-ttu-id="dc47d-137">I messaggi da hello **origine** modulo recapitati toohello **sink** modulo.</span><span class="sxs-lookup"><span data-stu-id="dc47d-137">Messages from hello **source** module are delivered toohello **sink** module.</span></span> <span data-ttu-id="dc47d-138">È possibile impostare hello **origine** modulo troppo`\*`, che indica che hello **sink** modulo riceve messaggi da qualsiasi modulo.</span><span class="sxs-lookup"><span data-stu-id="dc47d-138">You can set hello **source** module too`\*`, which indicates that hello **sink** module receives messages from any module.</span></span>

<span data-ttu-id="dc47d-139">Hello codice seguente viene illustrato hello JSON utilizzati collegamenti tooconfigure tra moduli hello utilizzati in hello hello\_esempio world in Linux.</span><span class="sxs-lookup"><span data-stu-id="dc47d-139">hello following code shows hello JSON used tooconfigure links between hello modules used in hello hello\_world sample on Linux.</span></span> <span data-ttu-id="dc47d-140">Tutti i messaggi prodotti da hello `hello_world` modulo è utilizzato da hello `logger` modulo.</span><span class="sxs-lookup"><span data-stu-id="dc47d-140">Every message produced by hello `hello_world` module is consumed by hello `logger` module.</span></span>

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a><span data-ttu-id="dc47d-141">Pubblicazione dei messaggi del modulo hello\_world</span><span class="sxs-lookup"><span data-stu-id="dc47d-141">Hello\_world module message publishing</span></span>

<span data-ttu-id="dc47d-142">È possibile trovare il codice hello utilizzato da hello hello\_world modulo toopublish messaggi hello ['hello_world.c'] [ lnk-helloworld-c] file.</span><span class="sxs-lookup"><span data-stu-id="dc47d-142">You can find hello code used by hello hello\_world module toopublish messages in hello ['hello_world.c'][lnk-helloworld-c] file.</span></span> <span data-ttu-id="dc47d-143">Hello frammento seguente mostra una versione modificata del codice hello e i commenti aggiunti alcuni codice rimosso per migliorare la leggibilità di gestione degli errori:</span><span class="sxs-lookup"><span data-stu-id="dc47d-143">hello following snippet shows an amended version of hello code with comments added and some error handling code removed for legibility:</span></span>

```c
int helloWorldThread(void *param)
{
    // create data structures used in function.
    HELLOWORLD_HANDLE_DATA* handleData = param;
    MESSAGE_CONFIG msgConfig;
    MAP_HANDLE propertiesMap = Map_Create(NULL);

    // add a property named "helloWorld" with a value of "from Azure IoT
    // Gateway SDK simple sample!" tooa set of message properties that
    // will be appended toohello message before publishing it. 
    Map_AddOrUpdate(propertiesMap, "helloWorld", "from Azure IoT Gateway SDK simple sample!")

    // set hello content for hello message
    msgConfig.size = strlen(HELLOWORLD_MESSAGE);
    msgConfig.source = HELLOWORLD_MESSAGE;

    // set hello properties for hello message
    msgConfig.sourceProperties = propertiesMap;

    // create a message based on hello msgConfig structure
    MESSAGE_HANDLE helloWorldMessage = Message_Create(&msgConfig);

    while (1)
    {
        if (handleData->stopThread)
        {
            (void)Unlock(handleData->lockHandle);
            break; /*gets out of hello thread*/
        }
        else
        {
            // publish hello message toohello broker
            (void)Broker_Publish(handleData->brokerHandle, helloWorldMessage);
            (void)Unlock(handleData->lockHandle);
        }

        (void)ThreadAPI_Sleep(5000); /*every 5 seconds*/
    }

    Message_Destroy(helloWorldMessage);

    return 0;
}
```

### <a name="helloworld-module-message-processing"></a><span data-ttu-id="dc47d-144">Elaborazione dei messaggi del modulo hello\_world</span><span class="sxs-lookup"><span data-stu-id="dc47d-144">Hello\_world module message processing</span></span>

<span data-ttu-id="dc47d-145">hello Hello\_modulo world non elabora mai i messaggi che altri moduli IoT Edge pubblicano toohello broker.</span><span class="sxs-lookup"><span data-stu-id="dc47d-145">hello hello\_world module never processes messages that other IoT Edge modules publish toohello broker.</span></span> <span data-ttu-id="dc47d-146">Pertanto, hello implementazione del callback messaggio hello in hello hello\_modulo world è una funzione viene eseguita alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="dc47d-146">Therefore, hello implementation of hello message callback in hello hello\_world module is a no-op function.</span></span>

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a><span data-ttu-id="dc47d-147">Elaborazione e pubblicazione dei messaggi del modulo di logger</span><span class="sxs-lookup"><span data-stu-id="dc47d-147">Logger module message publishing and processing</span></span>

<span data-ttu-id="dc47d-148">modulo di logger Hello riceve messaggi dal broker hello e li scrive file tooa.</span><span class="sxs-lookup"><span data-stu-id="dc47d-148">hello logger module receives messages from hello broker and writes them tooa file.</span></span> <span data-ttu-id="dc47d-149">ma non pubblica mai messaggi.</span><span class="sxs-lookup"><span data-stu-id="dc47d-149">It never publishes any messages.</span></span> <span data-ttu-id="dc47d-150">Pertanto, il codice hello del modulo di logger hello non chiama mai hello **Broker_Publish** (funzione).</span><span class="sxs-lookup"><span data-stu-id="dc47d-150">Therefore, hello code of hello logger module never calls hello **Broker_Publish** function.</span></span>

<span data-ttu-id="dc47d-151">Hello **Logger_Receive** funzione hello [logger.c] [ lnk-logger-c] file è broker hello di callback hello richiama modulo logger toohello di toodeliver messaggi.</span><span class="sxs-lookup"><span data-stu-id="dc47d-151">hello **Logger_Receive** function in hello [logger.c][lnk-logger-c] file is hello callback hello broker invokes toodeliver messages toohello logger module.</span></span> <span data-ttu-id="dc47d-152">Hello frammento seguente mostra una versione modificata e i commenti aggiunti alcuni codice rimosso per migliorare la leggibilità di gestione degli errori:</span><span class="sxs-lookup"><span data-stu-id="dc47d-152">hello following snippet shows an amended version with comments added and some error handling code removed for legibility:</span></span>

```c
static void Logger_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{

    time_t temp = time(NULL);
    struct tm* t = localtime(&temp);
    char timetemp[80] = { 0 };

    // Get hello message properties from hello message
    CONSTMAP_HANDLE originalProperties = Message_GetProperties(messageHandle); 
    MAP_HANDLE propertiesAsMap = ConstMap_CloneWriteable(originalProperties);

    // Convert hello collection of properties into a JSON string
    STRING_HANDLE jsonProperties = Map_ToJSON(propertiesAsMap);

    //  base64 encode hello message content
    const CONSTBUFFER * content = Message_GetContent(messageHandle);
    STRING_HANDLE contentAsJSON = Base64_Encode_Bytes(content->buffer, content->size);

    // Start hello construction of hello final string toobe logged by adding
    // hello timestamp
    STRING_HANDLE jsonToBeAppended = STRING_construct(",{\"time\":\"");
    STRING_concat(jsonToBeAppended, timetemp);

    // Add hello message properties
    STRING_concat(jsonToBeAppended, "\",\"properties\":"); 
    STRING_concat_with_STRING(jsonToBeAppended, jsonProperties);

    // Add hello content
    STRING_concat(jsonToBeAppended, ",\"content\":\"");
    STRING_concat_with_STRING(jsonToBeAppended, contentAsJSON);
    STRING_concat(jsonToBeAppended, "\"}]");

    // Write hello formatted string
    LOGGER_HANDLE_DATA *handleData = (LOGGER_HANDLE_DATA *)moduleHandle;
    addJSONString(handleData->fout, STRING_c_str(jsonToBeAppended);
}
```

## <a name="next-steps"></a><span data-ttu-id="dc47d-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc47d-153">Next steps</span></span>

<span data-ttu-id="dc47d-154">In questo articolo è stato eseguito un gateway perimetrale IoT semplice che scrive file di log tooa messaggi.</span><span class="sxs-lookup"><span data-stu-id="dc47d-154">In this article, you ran a simple IoT Edge gateway that writes messages tooa log file.</span></span> <span data-ttu-id="dc47d-155">vedere un esempio che invia messaggi tooIoT Hub, toorun [IoT Edge: inviare i messaggi da dispositivo a cloud con un dispositivo simulato con Linux] [ lnk-gateway-simulated-linux] o [IoT Edge: inviare i messaggi da dispositivo a cloud con un dispositivo simulato mediante Windows][lnk-gateway-simulated-windows].</span><span class="sxs-lookup"><span data-stu-id="dc47d-155">toorun a sample that sends messages tooIoT Hub, see [IoT Edge – send device-to-cloud messages with a simulated device using Linux][lnk-gateway-simulated-linux] or [IoT Edge – send device-to-cloud messages with a simulated device using Windows][lnk-gateway-simulated-windows].</span></span>


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md