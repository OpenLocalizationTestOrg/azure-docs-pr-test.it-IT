### <a name="create-a-nodejs-application"></a><span data-ttu-id="ce19d-101">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="ce19d-101">Create a Node.js application</span></span>

<span data-ttu-id="ce19d-102">Creare un nuovo file JavaScript denominato `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="ce19d-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="ce19d-103">Aggiungere il pacchetto NPM di inoltro</span><span class="sxs-lookup"><span data-stu-id="ce19d-103">Add the Relay NPM package</span></span>

<span data-ttu-id="ce19d-104">Eseguire `npm install hyco-ws` dal prompt dei comandi di Node nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="ce19d-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="ce19d-105">Scrivere codice per inviare messaggi</span><span class="sxs-lookup"><span data-stu-id="ce19d-105">Write some code to send messages</span></span>

1. <span data-ttu-id="ce19d-106">Aggiungere il valore `constants` seguente alla parte iniziale del file `sender.js`.</span><span class="sxs-lookup"><span data-stu-id="ce19d-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="ce19d-107">Aggiungere le costanti seguenti al file `sender.js` per i dettagli della connessione ibrida.</span><span class="sxs-lookup"><span data-stu-id="ce19d-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="ce19d-108">Sostituire i segnaposto tra parentesi con i valori ottenuti durante la creazione della connessione ibrida.</span><span class="sxs-lookup"><span data-stu-id="ce19d-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="ce19d-109">`const ns`: spazio dei nomi dell'inoltro.</span><span class="sxs-lookup"><span data-stu-id="ce19d-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="ce19d-110">Assicurarsi di usare il nome completo dello spazio dei nomi, ad esempio `{namespace}.servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="ce19d-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="ce19d-111">`const path`: nome della connessione ibrida.</span><span class="sxs-lookup"><span data-stu-id="ce19d-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="ce19d-112">`const keyrule`: nome della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="ce19d-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="ce19d-113">`const key`: valore della chiave di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="ce19d-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="ce19d-114">Aggiungere il codice seguente al file `sender.js`:</span><span class="sxs-lookup"><span data-stu-id="ce19d-114">Add the following code to the `sender.js` file:</span></span>
   
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
    <span data-ttu-id="ce19d-115">Il file sender.js sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ce19d-115">Here is what your sender.js file should look like:</span></span>
   
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

