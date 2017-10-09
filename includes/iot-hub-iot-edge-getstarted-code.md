## <a name="typical-output"></a>Output tipico

Hello seguente esempio Mostra output di hello scritto il file di log toohello dall'esempio hello World Hello. formattazione dell'output di Hello per migliorare la leggibilità:

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

## <a name="code-snippets"></a>Frammenti di codice

Questa sezione vengono illustrate alcune sezioni di codice hello in hello hello chiave\_esempio world.

### <a name="iot-edge-gateway-creation"></a>Creazione del gateway IoT Edge

È necessario implementare un *processo del gateway*. Questo programma crea l'infrastruttura interna hello (broker hello), carica moduli IoT Edge hello e configura il processo di gateway hello. Bordo IoT fornisce hello **Gateway\_crea\_da\_JSON** funzione tooenable è toobootstrap un gateway da un file JSON. hello toouse **Gateway\_crea\_da\_JSON** di funzione, passarlo hello percorso tooa file JSON specifica hello tooload moduli IoT Edge.

È possibile trovare codice hello per processo gateway hello hello *Hello World* sample in hello [Main. c] [ lnk-main-c] file. Per migliorare la leggibilità, hello frammento di codice seguente viene illustrata una versione abbreviata del codice del processo gateway hello. Il programma di esempio crea un gateway e quindi attende hello di hello utente toopress **invio** chiave prima che elimina gateway hello.

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

file di impostazioni JSON Hello contiene un elenco di collegamenti di hello tra i moduli di hello e tooload moduli IoT Edge. Ogni modulo di IoT Edge deve specificare:

* **nome**: un nome univoco per il modulo hello.
* **caricatore**: un caricatore che sa come hello tooload desiderato modulo. I caricatori sono punti di estensione per il caricamento di tipi diversi di moduli. IoT Edge offre caricatori da usare con moduli scritti in C, Node.js, Java e .NET nativi. esempio Hello World Hello utilizza solo caricatore C nativo hello perché tutti i moduli di hello in questo esempio sono librerie dinamiche scritte in C. Per ulteriori informazioni su come i moduli di Edge IoT toouse scritti in linguaggi diversi, vedere hello [Node.js](https://github.com/Azure/iot-edge/blob/master/samples/nodejs_simple_sample/), [Java](https://github.com/Azure/iot-edge/tree/master/samples/java_sample), o [.NET](https://github.com/Azure/iot-edge/tree/master/samples/dotnet_binding_sample) esempi.
    * **nome**: nome hello del caricatore di hello utilizzato modulo hello tooload.
    * **punto di ingresso**: libreria di toohello hello percorso contenente il modulo hello. In Linux questa libreria è un file con estensione so, in Windows è un file con estensione dll. punto di ingresso Hello è il tipo di toohello specifico del caricatore in uso. Hello punto di ingresso del caricatore di Node.js è un file. js. punto di ingresso del caricatore Java Hello è un percorso di classe e un nome di classe. punto di ingresso del caricatore .NET Hello è un nome di assembly e un nome di classe.

* **args**: necessita di qualsiasi modulo hello informazioni di configurazione.

Hello seguente codice mostra hello JSON utilizzato toodeclare tutti hello moduli IoT bordo per l'esempio Hello World hello in Linux. Se un modulo richiede argomenti dipende dalla progettazione hello del modulo hello. In questo esempio, il modulo di logger hello accetta un argomento di file di output di hello percorso toohello e hello hello\_modulo world non dispone di argomenti.

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

file JSON Hello contiene anche collegamenti hello tra moduli hello che vengono passati toohello broker. Un collegamento ha due proprietà:

* **origine**: il nome di un modulo da hello `modules` sezione o `\*`.
* **sink**: il nome di un modulo da hello `modules` sezione.

Ogni collegamento definisce una route messaggi e una direzione. I messaggi da hello **origine** modulo recapitati toohello **sink** modulo. È possibile impostare hello **origine** modulo troppo`\*`, che indica che hello **sink** modulo riceve messaggi da qualsiasi modulo.

Hello codice seguente viene illustrato hello JSON utilizzati collegamenti tooconfigure tra moduli hello utilizzati in hello hello\_esempio world in Linux. Tutti i messaggi prodotti da hello `hello_world` modulo è utilizzato da hello `logger` modulo.

```json
"links":
[
    {
        "source": "hello_world",
        "sink": "logger"
    }
]
```

### <a name="helloworld-module-message-publishing"></a>Pubblicazione dei messaggi del modulo hello\_world

È possibile trovare il codice hello utilizzato da hello hello\_world modulo toopublish messaggi hello ['hello_world.c'] [ lnk-helloworld-c] file. Hello frammento seguente mostra una versione modificata del codice hello e i commenti aggiunti alcuni codice rimosso per migliorare la leggibilità di gestione degli errori:

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

### <a name="helloworld-module-message-processing"></a>Elaborazione dei messaggi del modulo hello\_world

hello Hello\_modulo world non elabora mai i messaggi che altri moduli IoT Edge pubblicano toohello broker. Pertanto, hello implementazione del callback messaggio hello in hello hello\_modulo world è una funzione viene eseguita alcuna operazione.

```c
static void HelloWorld_Receive(MODULE_HANDLE moduleHandle, MESSAGE_HANDLE messageHandle)
{
    /* No action, HelloWorld is not interested in any messages. */
}
```

### <a name="logger-module-message-publishing-and-processing"></a>Elaborazione e pubblicazione dei messaggi del modulo di logger

modulo di logger Hello riceve messaggi dal broker hello e li scrive file tooa. ma non pubblica mai messaggi. Pertanto, il codice hello del modulo di logger hello non chiama mai hello **Broker_Publish** (funzione).

Hello **Logger_Receive** funzione hello [logger.c] [ lnk-logger-c] file è broker hello di callback hello richiama modulo logger toohello di toodeliver messaggi. Hello frammento seguente mostra una versione modificata e i commenti aggiunti alcuni codice rimosso per migliorare la leggibilità di gestione degli errori:

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

## <a name="next-steps"></a>Passaggi successivi

In questo articolo è stato eseguito un gateway perimetrale IoT semplice che scrive file di log tooa messaggi. vedere un esempio che invia messaggi tooIoT Hub, toorun [IoT Edge: inviare i messaggi da dispositivo a cloud con un dispositivo simulato con Linux] [ lnk-gateway-simulated-linux] o [IoT Edge: inviare i messaggi da dispositivo a cloud con un dispositivo simulato mediante Windows][lnk-gateway-simulated-windows].


<!-- Links -->
[lnk-main-c]: https://github.com/Azure/iot-edge/blob/master/samples/hello_world/src/main.c
[lnk-helloworld-c]: https://github.com/Azure/iot-edge/blob/master/modules/hello_world/src/hello_world.c
[lnk-logger-c]: https://github.com/Azure/iot-edge/blob/master/modules/logger/src/logger.c
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-gateway-simulated-linux]: ../articles/iot-hub/iot-hub-linux-iot-edge-simulated-device.md
[lnk-gateway-simulated-windows]: ../articles/iot-hub/iot-hub-windows-iot-edge-simulated-device.md