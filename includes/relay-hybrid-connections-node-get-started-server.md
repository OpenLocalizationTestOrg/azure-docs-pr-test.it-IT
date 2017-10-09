### <a name="create-a-nodejs-application"></a>Creare un'applicazione Node.js

Creare un nuovo file JavaScript denominato `listener.js`.

### <a name="add-hello-relay-npm-package"></a>Aggiungere il pacchetto NPM inoltro hello

Eseguire `npm install hyco-ws` dal prompt dei comandi di Node nella cartella del progetto.

### <a name="write-some-code-tooreceive-messages"></a>Scrivere codice tooreceive messaggi

1. Aggiungere hello seguente toohello costante cima hello `listener.js` file.
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. Aggiungere hello seguenti costanti toohello `listener.js` file per i dettagli della connessione ibrida hello. Sostituire i segnaposto hello tra parentesi quadre con valori di hello ottenuto al momento della creazione connessione ibrida hello.
   
   1. `const ns`-hello inoltro dello spazio dei nomi. Nome completo dello spazio dei nomi di hello che toouse; ad esempio, `{namespace}.servicebus.windows.net`.
   2. `const path`-nome hello della connessione ibrida hello.
   3. `const keyrule`-nome hello della chiave di firma di accesso condiviso di hello.
   4. `const key`-hello valore della chiave di firma di accesso condiviso.

3. Aggiungere i seguenti toohello codice hello `listener.js` file:
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    Il file listener.js sarà simile al seguente:
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

