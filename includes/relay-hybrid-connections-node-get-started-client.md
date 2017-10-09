### <a name="create-a-nodejs-application"></a>Creare un'applicazione Node.js

Creare un nuovo file JavaScript denominato `sender.js`.

### <a name="add-hello-relay-npm-package"></a>Aggiungere il pacchetto NPM inoltro hello

Eseguire `npm install hyco-ws` dal prompt dei comandi di Node nella cartella del progetto.

### <a name="write-some-code-toosend-messages"></a>Scrivere codice toosend messaggi

1. Aggiungere il seguente hello `constants` toohello cima hello `sender.js` file.
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. Aggiungere hello seguenti costanti toohello `sender.js` file per i dettagli della connessione ibrida hello. Sostituire i segnaposto hello tra parentesi quadre con valori di hello ottenuto al momento della creazione connessione ibrida hello.
   
   1. `const ns`-hello inoltro dello spazio dei nomi. Nome completo dello spazio dei nomi di hello che toouse; ad esempio, `{namespace}.servicebus.windows.net`.
   2. `const path`-nome hello della connessione ibrida hello.
   3. `const keyrule`-nome hello della chiave di firma di accesso condiviso di hello.
   4. `const key`-hello valore della chiave di firma di accesso condiviso.

3. Aggiungere i seguenti toohello codice hello `sender.js` file:
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    Il file sender.js sarà simile al seguente:
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

