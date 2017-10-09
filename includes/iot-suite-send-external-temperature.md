## <a name="configure-hello-nodejs-simulated-device"></a>Configura dispositivo simulato di hello Node.js
1. Dashboard di monitoraggio remoto di hello, fare clic su **+ Aggiungi una periferica** e quindi aggiungere un *dispositivo personalizzata*. Nome host, l'id dispositivo e chiave del dispositivo, prendere nota di hello IoT Hub. È necessario più avanti in questa esercitazione quando si prepara un'applicazione hello remote_monitoring.js dispositivo client.
2. Verificare che Node.js 0.12.x o una versione successiva sia installata sul computer di sviluppo. Eseguire `node --version` un prompt dei comandi o in una versione di hello toocheck shell. Per informazioni sull'utilizzo di un tooinstall manager pacchetto Node.js in Linux, vedere [l'installazione di Node.js tramite Gestione pacchetti][node-linux].
3. Dopo aver installato Node.js, clonare hello versione hello [azure iot-sdk-nodi] [ lnk-github-repo] computer di sviluppo tooyour repository. Utilizzare sempre hello **master** ramo per la versione più recente di hello delle librerie di hello e gli esempi.
4. Dalla copia locale di hello [azure iot-sdk-nodi] [ lnk-github-repo] repository, hello copia i seguenti due file dalla cartella vuota tooan cartella dispositivo/nodo/esempi di hello nel computer di sviluppo:
   
   * packages.json
   * remote_monitoring.js
5. Aprire il file remote_monitoring.js hello e cercare hello seguente definizione di variabile:
   
    ```
    var connectionString = "[IoT Hub device connection string]";
    ```
6. Sostituire **[stringa di connessione dispositivo Hub IoT]** con la stringa di connessione del dispositivo. Utilizzare i valori hello per nome host IoT Hub, id dispositivo e nella chiave del dispositivo che è annotata nel passaggio 1. Una stringa di connessione del dispositivo ha hello seguente formato:
   
    ```
    HostName={your IoT Hub hostname};DeviceId={your device id};SharedAccessKey={your device key}
    ```
   
    Se il nome host di IoT Hub è **contoso** e l'id dispositivo **mydevice**, la stringa di connessione sarà simile hello frammento di codice seguente:
   
    ```
    var connectionString = "HostName=contoso.azure-devices.net;DeviceId=mydevice;SharedAccessKey=2s ... =="
    ```
7. Salvare il file hello. Eseguire i seguenti comandi in una shell o un prompt dei comandi nella cartella hello che contiene questi file tooinstall hello pacchetti hello e quindi eseguire l'applicazione di esempio hello:
   
    ```
    npm install
    node remote_monitoring.js
    ```

## <a name="observe-dynamic-telemetry-in-action"></a>Osservare la telemetria dinamica in azione
dashboard di Hello Mostra hello temperatura e umidità dati di telemetria dai dispositivi simulato esistente hello:

![dashboard predefinito Hello][image1]

Se si seleziona il dispositivo simulato di hello Node.js che è stato eseguito nella sezione precedente di hello, vedere temperatura e umidità, dati di telemetria temperatura esterni:

![Aggiungere dashboard toohello temperatura esterno][image2]

soluzione di monitoraggio remoto Hello automaticamente rileva il tipo di dati di telemetria di hello aggiuntive temperatura esterno e lo aggiunge toohello grafico nel dashboard di hello.

[node-linux]: https://github.com/nodejs/node-v0.x-archive/wiki/Installing-Node.js-via-package-manager
[lnk-github-repo]: https://github.com/Azure/azure-iot-sdk-node
[image1]: media/iot-suite-send-external-temperature/image1.png
[image2]: media/iot-suite-send-external-temperature/image2.png