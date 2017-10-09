### <a name="create-a-nodejs-application"></a><span data-ttu-id="67d62-101">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="67d62-101">Create a Node.js application</span></span>

<span data-ttu-id="67d62-102">Creare un nuovo file JavaScript denominato `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="67d62-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="67d62-103">Aggiungere il pacchetto NPM inoltro hello</span><span class="sxs-lookup"><span data-stu-id="67d62-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="67d62-104">Eseguire `npm install hyco-ws` dal prompt dei comandi di Node nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="67d62-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="67d62-105">Scrivere codice toosend messaggi</span><span class="sxs-lookup"><span data-stu-id="67d62-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="67d62-106">Aggiungere il seguente hello `constants` toohello cima hello `sender.js` file.</span><span class="sxs-lookup"><span data-stu-id="67d62-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="67d62-107">Aggiungere hello seguenti costanti toohello `sender.js` file per i dettagli della connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="67d62-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="67d62-108">Sostituire i segnaposto hello tra parentesi quadre con valori di hello ottenuto al momento della creazione connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="67d62-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="67d62-109">`const ns`-hello inoltro dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="67d62-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="67d62-110">Nome completo dello spazio dei nomi di hello che toouse; ad esempio, `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="67d62-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="67d62-111">`const path`-nome hello della connessione ibrida hello.</span><span class="sxs-lookup"><span data-stu-id="67d62-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="67d62-112">`const keyrule`-nome hello della chiave di firma di accesso condiviso di hello.</span><span class="sxs-lookup"><span data-stu-id="67d62-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="67d62-113">`const key`-hello valore della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="67d62-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="67d62-114">Aggiungere i seguenti toohello codice hello `sender.js` file:</span><span class="sxs-lookup"><span data-stu-id="67d62-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="67d62-115">Il file sender.js sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="67d62-115">Here is what your sender.js file should look like:</span></span>
   
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

